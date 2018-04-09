---
title: 配置 ASP.NET 核心以使用代理服务器和负载平衡器
author: guardrex
description: 了解有关配置的代理服务器和负载平衡器，通常会掩盖重要请求信息后面托管的应用程序。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/26/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/proxy-load-balancer
ms.openlocfilehash: b153a7406ae1b31a2aa453135c6bd0e5ce0b2997
ms.sourcegitcommit: d45d766504c2c5aad2453f01f089bc6b696b5576
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="configure-aspnet-core-to-work-with-proxy-servers-and-load-balancers"></a>配置 ASP.NET 核心以使用代理服务器和负载平衡器

通过[Luke Latham](https://github.com/guardrex)和[Chris 跨](https://github.com/Tratcher)

对于 ASP.NET Core 推荐的配置，在使用 IIS/ASP.NET 核心模块、 Nginx 或 Apache 承载应用程序。 代理服务器、 负载平衡器和其他网络设备中通常在它到达应用程序之前遮盖有关请求的信息：

* 当通过 HTTP HTTPS 请求代理时，原始的方案 (HTTPS) 将丢失，并且必须转发标头中。
* 因为应用程序收到请求时从该代理并不是其源 true 在 Internet 或公司网络上的，还必须在头转发发起的客户端 IP 地址。

此信息可能会在中处理的请求，例如重定向、 身份验证、 链接生成、 策略评估和客户端 geoloation 十分重要。

## <a name="forwarded-headers"></a>转发的标头

按照约定，代理将在 HTTP 头中的信息转发。

| Header | 描述 |
| ------ | ----------- |
| X-Forwarded-For | 包含有关客户端启动的请求和后续代理的代理链中的信息。 此参数可能包含 IP 地址 （和 （可选） 端口号）。 代理服务器链中的第一个参数指示客户端第一次发出请求。 后续代理标识符遵循。 链中的最后一个代理不在列表中的参数。 最后一个代理服务器的 IP 地址和 （可选） 端口号时，都可用作在传输层的远程 IP 地址。 |
| X-Forwarded-Proto | 原始的方案 (HTTP/HTTPS) 的值。 如果请求具有遍历多个代理服务器，则这也可能的方案的列表。 |
| X-Forwarded-Host | 主机标头字段的原始值。 通常情况下，代理无需修改的主机标头。 请参阅[Microsoft 安全公告 CVE-2018年-0787年](https://github.com/aspnet/Announcements/issues/295)有关一个提升特权漏洞，它会影响的系统代理不验证其中或 restict 主机为已知良好的值的标头信息。 |

转发标头中间件，从[Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/)打包、 读取这些标头和关联的字段中填充上[HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)。 

中间件更新中：

* [HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash;使用设置`X-Forwarded-For`标头值。 其他设置会影响该中间件的设置如何`RemoteIpAddress`。 有关详细信息，请参阅[转发标头中间件选项](#forwarded-headers-middleware-options)。
* [HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash;使用设置`X-Forwarded-Proto`标头值。
* [HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash;使用设置`X-Forwarded-Host`标头值。

请注意，并非所有网络设备都添加`X-Forwarded-For`和`X-Forwarded-Proto`标头，而无需其他配置。 如果代理的请求不包含这些标头，在达到应用程序时，请查阅设备制造商提供的指导。

转发标头中间件[默认设置](#forwarded-headers-middleware-options)可以配置。 默认设置如下：

* 只有*一个代理*应用程序和请求的源之间。
* 已知的代理的配置和已知网络仅环回地址。

## <a name="iisiis-express-and-aspnet-core-module"></a>IIS/IIS Express 和 ASP.NET Core 模块

IIS 和 ASP.NET 核心模块后面运行应用时，默认情况下，通过 IIS 集成中间件启用转发标头中间件。 转发的标头中间件激活到 ASP.NET 核心模块由于信任问题与转发标头一起运行第一个与特定的受限配置中间件管道中 (例如， [IP 欺骗](https://www.iplocation.net/ip-spoofing))。 该中间件配置为转发`X-Forwarded-For`和`X-Forwarded-Proto`标头且被限制到单个 localhost 代理。 如果不需要附加配置，请参阅[转发标头中间件选项](#forwarded-headers-middleware-options)。

## <a name="other-proxy-server-and-load-balancer-scenarios"></a>其他代理服务器和负载平衡器方案

除了使用 IIS 集成中间件，默认情况下不启用转发标头中间件。 必须为转发过程标头包含应用程序启用转发标头中间件[UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders)。 如果未启用该中间件后[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)到中间件，默认值指定[ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders)是[ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).

配置与中间件[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)转发`X-Forwarded-For`和`X-Forwarded-Proto`中的标头`Startup.ConfigureServices`。 调用[UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders)中的方法`Startup.Configure`在调用其他中间件之前：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    
    services.Configure<ForwardedHeadersOptions>(options =>
    {
        options.ForwardedHeaders = 
            ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto;
    });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseForwardedHeaders();

    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();
    // In ASP.NET Core 1.x, replace the following line with: app.UseIdentity();
    app.UseAuthentication();
    app.UseMvc();
}
```

> [!NOTE]
> 如果没有[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)中指定`Startup.ConfigureServices`或直接向与该扩展方法[UseForwardedHeaders （IApplicationBuilder，ForwardedHeadersOptions）](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_)，默认值标头以转发[ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)。 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders)属性必须使用要转发的标头进行配置。

## <a name="forwarded-headers-middleware-options"></a>转发的标头中间件选项

[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)控制转发标头中间件的行为：

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardLimit = 2;
    options.KnownProxies.Add(IPAddress.Parse("127.0.10.1"));
    options.ForwardedForHeaderName = "X-Forwarded-For-Custom-Header-Name";
});
```

| 选项 | 描述 |
| ------ | ----------- |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)。<br><br>默认值为 `X-Forwarded-For`。 |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | 标识应处理的转发器。 请参阅[ForwardedHeaders 枚举](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)有关应用的字段的列表。 分配给此属性的典型值为<code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>。<br><br>默认值是[ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)。 |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)。<br><br>默认值为 `X-Forwarded-Host`。 |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)。<br><br>默认值为 `X-Forwarded-Proto`。 |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | 限制在处理标头中的项数。 设置为`null`禁用了限制，但这只应该在`KnownProxies`或`KnownNetworks`配置。<br><br>默认值为 1。 |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | 地址范围的已知的代理，以接受从转发标头。 提供使用无类别域际路由选择 (CIDR) 表示法的 IP 范围。<br><br>默认值是[IList](/dotnet/api/system.collections.generic.ilist-1)\<[ip 网络](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)> 包含为单个条目`IPAddress.Loopback`。 |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | 已知的代理，以接受从转发标头的地址。 使用`KnownProxies`以指定确切的 IP 地址匹配。<br><br>默认值是[IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)> 包含为单个条目`IPAddress.IPv6Loopback`。 |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)。<br><br>默认值为 `X-Original-For`。 |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)。<br><br>默认值为 `X-Original-Host`。 |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | 使用而不是指定的此属性指定的标头[ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)。<br><br>默认值为 `X-Original-Proto`。 |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | 要求的数量的标头的值进行之间同步[ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders)正在处理。<br><br>ASP.NET 核心 1.x 是中的默认值`true`。 默认值在 ASP.NET 核心 2.0 或更高版本是`false`。 |

## <a name="scenarios-and-use-cases"></a>方案和用例

### <a name="when-it-isnt-possible-to-add-forwarded-headers-and-all-requests-are-secure"></a>当无法添加转发标头和所有请求并安全

在某些情况下，它可能不能将转发的头添加到代理到应用程序的请求。 如果代理强制实施所有的公共外部请求 HTTPS，方案可以手动设置`Startup.Configure`在使用任何类型的中间件之前：

```csharp
app.Use((context, next) =>
{
    context.Request.Scheme = "https";
    return next();
});
```

此代码可以使用环境变量或在开发或过渡环境中的其他配置设置来禁用。

### <a name="deal-with-path-base-and-proxies-that-change-the-request-path"></a>处理基路径和更改请求路径的代理

某些代理传递路径不变，但与应用，以便路由应删除的基路径可正常工作。 [UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase)中间件将拆分到路径[HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path)和到的应用程序基路径[HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase)。

如果`/foo`作为传递代理路径是应用程序基路径`/foo/api/1`，中间件集`Request.PathBase`到`/foo`和`Request.Path`到`/api/1`使用以下命令：

```csharp
app.UsePathBase("/foo");
```

原始路径和基路径都将重新应用时按相反的顺序再次调用该中间件。 中间件订单处理的详细信息，请参阅[中间件](xref:fundamentals/middleware/index)。

如果代理修剪路径 (例如，转发`/foo/api/1`到`/api/1`)，修补程序将重定向，并通过设置请求的链接[PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase)属性：

```csharp
app.Use((context, next) =>
{
    context.Request.PathBase = new PathString("/foo");
    return next();
});
```

如果代理添加路径数据，放弃路径重定向和链接使用的进行修复的一部分[StartsWithSegments （PathString，PathString）](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__)并将分配给[路径](/dotnet/api/microsoft.aspnetcore.http.httprequest.path)属性：

```csharp
app.Use((context, next) =>
{
    if (context.Request.Path.StartsWithSegments("/foo", out var remainder))
    {
        context.Request.Path = remainder;
    }

    return next();
});
```

## <a name="troubleshoot"></a>疑难解答

标头不转发按预期方式，当启用[日志记录](xref:fundamentals/logging/index)。 如果日志未提供足够的信息来解决该问题，枚举服务器收到的请求标头。 可以对应用程序响应使用内联中间件编写标头：

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory)
{
    app.Run(async (context) =>
    {
        context.Response.ContentType = "text/plain";

        // Request method, scheme, and path
        await context.Response.WriteAsync(
            $"Request Method: {context.Request.Method}{Environment.NewLine}");
        await context.Response.WriteAsync(
            $"Request Scheme: {context.Request.Scheme}{Environment.NewLine}");
        await context.Response.WriteAsync(
            $"Request Path: {context.Request.Path}{Environment.NewLine}");

        // Headers
        await context.Response.WriteAsync($"Request Headers:{Environment.NewLine}");

        foreach (var header in context.Request.Headers)
        {
            await context.Response.WriteAsync($"{header.Key}: " +
                $"{header.Value}{Environment.NewLine}");
        }

        await context.Response.WriteAsync(Environment.NewLine);

        // Connection: RemoteIp
        await context.Response.WriteAsync(
            $"Request RemoteIp: {context.Connection.RemoteIpAddress}");
    }
}
```

确保转发-X * 预期值与服务器收到标头。 如果给定的标头中有多个值，请注意按相反的顺序从右到左的转发标头中间件进程标头。

请求的原始远程 IP 必须匹配中的条目`KnownProxies`或`KnownNetworks`列出 X-转发-对于处理之前。 这就限制了标头欺骗不接受来自不受信任代理转发器。

## <a name="additional-resources"></a>其他资源

* [Microsoft 安全公告 CVE-2018年-0787: ASP.NET Core 提升特权漏洞](https://github.com/aspnet/Announcements/issues/295)
