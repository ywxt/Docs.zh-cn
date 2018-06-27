---
title: ASP.NET Core 中的 Kestrel Web 服务器实现
author: rick-anderson
description: 了解跨平台 ASP.NET Core Web 服务器 Kestrel。
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/02/2018
uid: fundamentals/servers/kestrel
ms.openlocfilehash: 62649351271deebcf1ed9d2f8b2258bed3478989
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276651"
---
# <a name="kestrel-web-server-implementation-in-aspnet-core"></a>ASP.NET Core 中的 Kestrel Web 服务器实现

作者：[Tom Dykstra](https://github.com/tdykstra)、[Chris Ross](https://github.com/Tratcher) 和 [Stephen Halter](https://twitter.com/halter73)

Kestrel 是一个跨平台的[适用于 ASP.NET Core 的 Web 服务器](xref:fundamentals/servers/index)。 Kestrel 是 Web 服务器，默认包括在 ASP.NET Core 项目模板中。

Kestrel 支持以下功能：

* HTTPS
* 用于启用 [WebSocket](https://github.com/aspnet/websockets) 的不透明升级
* 用于获得 Nginx 高性能的 Unix 套接字

.NET Core 支持的所有平台和版本均支持 Kestrel。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a>何时结合使用 Kestrel 和反向代理

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

可以单独使用 Kestrel，也可以将其与反向代理服务器（如 IIS、Nginx 或 Apache）结合使用。 反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

使用或不使用反向代理服务器进行配置对 ASP.NET Core 2.0 或更高版本的应用来说都是有效且受支持的托管配置。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

如果应用仅接受来自内部网络的请求，则可以将 Kestrel 直接用作该应用的服务器。

![Kestrel 直接与你的内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

如果将应用公开到 Internet，则将 IIS、Nginx 或 Apache 用作反向代理服务器。 反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

出于安全考虑，边缘部署需要使用反向代理（从 Internet 公开到流量）。 Kestrel 的 1.x 版本没有防御攻击的完整补充，例如适当的超时、大小限制以及并发连接限制。

---

具有共享在单个服务器上运行的相同 IP 和端口的多个应用时，需要一个反向代理方案。 Kestrel 不支持此方案，因为 Kestrel 不支持在多个进程之间共享相同的 IP 和端口。 如果将 Kestrel 配置为侦听某个端口，Kestrel 会处理该端口的所有流量（无视请求的主机标头）。 可以共享端口的反向代理能在唯一的 IP 和端口上将请求转发至 Kestrel。

即使不需要反向代理服务器，使用反向代理服务器可能也是个不错的选择：

* 它可以限制所承载的应用中的公开的公共外围应用。
* 它可以提供额外的配置和防护层。
* 它可以更好地与现有基础结构集成。
* 它可以简化负载均衡和 SSL 配置。 仅反向代理服务器需要 SSL 证书，并且该服务器可使用普通 HTTP 在内部网络上与应用服务器通信。

> [!WARNING]
> 如果在启用了主机筛选的情况下不使用反向代理，则必须启用[“主机筛选”](#host-filtering)。

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a>如何在 ASP.NET Core 应用中使用 Kestrel

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[Microsoft.AspNetCore.App 元包] (xref:fundamentals/metapackage-app)中包括 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 包（ASP.NET Core 2.1 或更高版本）。

默认情况下，ASP.NET Core 项目模板使用 Kestrel。 在 Program.cs 中，模板代码调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)，后者在后台调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel)。

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

安装 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 包。

在 `Main` 方法中的 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1) 上调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 扩展方法，指定所需的任何 [Kestrel 选项](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)，如下一部分中所示。

[!code-csharp[](kestrel/samples/1.x/KestrelSample/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a>Kestrel 选项

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

Kestrel Web 服务器具有约束配置选项，这些选项在面向 Internet 的部署中尤其有用。 可以自定义的一些重要限制：

* 客户端最大连接数
* 请求正文最大大小
* 请求正文最小数据速率

可在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 类的 [Limits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) 属性上设置这些约束和其他约束。 `Limits` 属性包含 [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) 类的实例。

**客户端最大连接数**

[MaxConcurrentConnections](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentconnections)  
[MaxConcurrentUpgradedConnections](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentupgradedconnections)

可使用以下代码为整个应用设置并发打开的最大 TCP 连接数：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_Limits&highlight=3)]

对于已从 HTTP 或 HTTPS 升级到另一个协议（例如，Websocket 请求）的连接，有一个单独的限制。 连接升级后，不会计入 `MaxConcurrentConnections` 限制。

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_Limits&highlight=4)]

默认情况下，最大连接数不受限制 (NULL)。

**请求正文最大大小**

[MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)

默认的请求正文最大大小为 30,000,000 字节，大约 28.6 MB。

在 ASP.NET Core MVC 应用中替代限制的推荐方法是在操作方法上使用 [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 属性：

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

以下示例演示如何为每个请求上的应用配置约束：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_Limits&highlight=5)]

可在中间件中替代特定请求的设置：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Startup.cs?name=snippet_Limits&highlight=3-4)]

如果在应用开始读取请求后尝试配置请求限制，则会引发异常。 `IsReadOnly` 属性指示 `MaxRequestBodySize` 属性处于只读状态，意味已经无法再配置限制。

**请求正文最小数据速率**

[MinRequestBodyDataRate](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minrequestbodydatarate)  
[MinResponseDataRate](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minresponsedatarate)

Kestrel 每秒检查一次数据是否以指定的速率（字节/秒）传入。 如果速率低于最小值，则连接超时。宽限期是 Kestrel 提供给客户端用于将其发送速率提升到最小值的时间量；在此期间不会检查速率。 宽限期有助于避免最初由于 TCP 慢启动而以较慢速率发送数据的连接中断。

默认的最小速率为 240 字节/秒，包含 5 秒的宽限期。

最小速率也适用于响应。 除了属性和接口名称中具有 `RequestBody` 或 `Response` 以外，用于设置请求限制和响应限制的代码相同。

以下示例演示如何在 Program.cs 中配置最小数据速率：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_Limits&highlight=6-7)]

可在中间件中配置每个请求的速率：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Startup.cs?name=snippet_Limits&highlight=5-8)]

有关其他 Kestrel 选项和限制的信息，请参阅：

* [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)
* [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits)
* [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

有关 Kestrel 选项和限制的信息，请参阅：

* [KestrelServerOptions 类](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)
* [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserverlimits?view=aspnetcore-1.1)

---

### <a name="endpoint-configuration"></a>终结点配置

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

::: moniker range="= aspnetcore-2.0"
默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。 在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 上调用 [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 或 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 方法，从而配置 Kestrel 的 URL 前缀和端口。 `UseUrls`、`--urls` 命令行参数、`urls` 主机配置键以及 `ASPNETCORE_URLS` 环境变量也有用，但具有本节后面注明的限制。

`urls` 主机配置键必须来自主机配置，而不是应用配置。 将 `urls` 键和值添加到 appsettings.json 不影响主机配置，因为是在从配置文件读取配置时对主机进行完全初始化的。 但是，在主机生成器上可以使用 appsettings.json 中的 `urls` 键以及 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 来配置主机：

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appSettings.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseKestrel()
    .UseConfiguration(config)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseStartup<Startup>()
    .Build();
```

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

默认情况下，ASP.NET Core 绑定到：

* `http://localhost:5000`
* `https://localhost:5001`（存在本地开发证书时）

开发证书会创建于以下情况：

* 安装了 [.NET Core SDK](/dotnet/core/sdk) 时。
* [dev-certs tool](xref:aspnetcore-2.1#https) 用于创建证书。

部分浏览器需要获取信任本地开发证书的显示权限。

ASP.NET Core 2.1 及更高版本的项目模板将应用配置为默认情况下在 HTTPS 上运行，并包括 [HTTPS 重定向和 HSTS 支持](xref:security/enforcing-ssl)。

在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 上调用 [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 或 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 方法，从而配置 Kestrel 的 URL 前缀和端口。

`UseUrls`、`--urls` 命令行参数、`urls` 主机配置键以及 `ASPNETCORE_URLS` 环境变量也有用，但具有本节后面注明的限制（必须要有可用于 HTTPS 终结点配置的默认证书）。

ASP.NET Core 2.1 `KestrelServerOptions` 配置：

**ConfigureEndpointDefaults(Action&lt;ListenOptions&gt;)**  
指定一个为每个指定的终结点运行的配置 `Action`。 多次调用 `ConfigureEndpointDefaults`，用最新指定的 `Action` 替换之前的 `Action`。

**ConfigureHttpsDefaults(Action&lt;HttpsConnectionAdapterOptions&gt;)**  
指定一个为每个 HTTPS 终结点运行的配置 `Action`。 多次调用 `ConfigureHttpsDefaults`，用最新指定的 `Action` 替换之前的 `Action`。

**Configure(IConfiguration)**  
创建配置加载程序，用于设置将 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) 作为输入的 Kestrel。 配置必须针对 Kestrel 的配置节。

**ListenOptions.UseHttps**  
将 Kestrel 配置为使用 HTTPS。

`ListenOptions.UseHttps` 扩展：

* `UseHttps` &ndash; 将 Kestrel 配置为使用 HTTPS，采用默认证书。 如果没有配置默认证书，则会引发异常。
* `UseHttps(string fileName)`
* `UseHttps(string fileName, string password)`
* `UseHttps(string fileName, string password, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(StoreName storeName, string subject)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(X509Certificate2 serverCertificate)`
* `UseHttps(X509Certificate2 serverCertificate, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(Action<HttpsConnectionAdapterOptions> configureOptions)`

`ListenOptions.UseHttps` 参数：

* `filename` 是证书文件的路径和文件名，关联包含应用内容文件的目录。
* `password` 是访问 X.509 证书数据所需的密码。
* `configureOptions` 是配置 `HttpsConnectionAdapterOptions` 的 `Action`。 返回 `ListenOptions`。
* `storeName` 是从中加载证书的证书存储。
* `subject` 是证书的主题名称。
* `allowInvalid` 指示是否存在需要留意的无效证书，例如自签名证书。
* `location` 是从中加载证书的存储位置。
* `serverCertificate` 是 X.509 证书。

在生产中，必须显式配置 HTTPS。 至少必须提供默认证书。

下面要描述的支持的配置：

* 无配置
* 从配置中替换默认证书
* 更改代码中的默认值

*无配置*

Kestrel 在 `http://localhost:5000` 和 `https://localhost:5001` 上进行侦听（如果默认证书可用）。

使用以下内容指定 URL：

* `ASPNETCORE_URLS` 环境变量。
* `--urls` 命令行参数。
* `urls` 主机配置键。
* `UseUrls` 扩展方法。

有关详细信息，请参阅[服务器 URL](xref:fundamentals/host/web-host#server-urls) 和[重写配置](xref:fundamentals/host/web-host#override-configuration)。

采用这些方法提供的值可以是一个或多个 HTTP 和 HTTPS 终结点（如果默认证书可用，则为 HTTPS）。 将值配置为以分号分隔的列表（例如 `"Urls": "http://localhost:8000;http://localhost:8001"`）。

*从配置中替换默认证书*

[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 在默认情况下调用 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 来加载 Kestrel 配置。 Kestrel 可以使用默认 HTTPS 应用设置配置架构。 从磁盘上的文件或从证书存储中配置多个终结点，包括要使用的 URL 和证书。

在以下 appsettings.json 示例中：

* 将 AllowInvalid 设置为 `true`，从而允许使用无效证书（例如自签名证书）。
* 任何未指定证书的 HTTPS 终结点（下例中的 HttpsDefaultCert）会回退至在 Certificates > Default 下定义的证书或开发证书。

```json
{
"Kestrel": {
  "EndPoints": {
    "Http": {
      "Url": "http://localhost:5000"
    },

    "HttpsInlineCertFile": {
      "Url": "https://localhost:5001",
      "Certificate": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    },

    "HttpsInlineCertStore": {
      "Url": "https://localhost:5002",
      "Certificate": {
        "Subject": "<subject; required>",
        "Store": "<certificate store; defaults to My>",
        "Location": "<location; defaults to CurrentUser>",
        "AllowInvalid": "<true or false; defaults to false>"
      }
    },

    "HttpsDefaultCert": {
      "Url": "https://localhost:5003"
    },

    "Https": {
      "Url": "https://*:5004",
      "Certificate": {
      "Path": "<path to .pfx file>",
      "Password": "<certificate password>"
      }
    }
    },
    "Certificates": {
      "Default": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    }
  }
}
```

此外还可以使用任何证书节点的 Path 和 Password，采用证书存储字段指定证书。 例如，可将 Certificates > Default 证书指定为：

```json
"Default": {
  "Subject": "<subject; required>",
  "Store": "<cert store; defaults to My>",
  "Location": "<location; defaults to CurrentUser>",
  "AllowInvalid": "<true or false; defaults to false>"
}
```

架构的注意事项：

* 终结点的名称不区分大小写。 例如，`HTTPS` 和 `Https` 都是有效的。
* 每个终结点都要具备 `Url` 参数。 此参数的格式和顶层 `Urls` 配置参数一样，只不过它只能有单个值。
* 这些终结点不会添加进顶层 `Urls` 配置中定义的终结点，而是替换它们。 通过 `Listen` 在代码中定义的终结点与在配置节中定义的终结点相累积。
* `Certificate` 部分是可选的。 如果为指定 `Certificate` 部分，则使用在之前的方案中定义的默认值。 如果没有可用的默认值，服务器会引发异常且无法启动。
* `Certificate` 支持 Path&ndash;Password 和 Subject&ndash;Store 证书。
* 只要不会导致端口冲突，就能以这种方式定义任何数量的终结点。
* `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 通过 `.Endpoint(string name, options => { })` 方法返回 `KestrelConfigurationLoader`，可以用于补充已配置的终结点设置：

  ```csharp
  serverOptions.Configure(context.Configuration.GetSection("Kestrel"))
      .Endpoint("HTTPS", opt =>
      {
          opt.HttpsOptions.SslProtocols = SslProtocols.Tls12;
      });
  ```

  也可以直接访问 `KestrelServerOptions.ConfigurationLoader` 在现有加载程序上保持迭代，例如由 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 提供的加载程序。

* 每个终结点的配置节都可用于 `Endpoint` 方法中的选项，以便读取自定义设置。
* 通过另一节再次调用 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 可能加载多个配置。 只使用最新配置，除非之前的实例上显式调用了 `Load`。 元包不会调用 `Load`，所以可能会替换它的默认配置节。
* `KestrelConfigurationLoader` 从 `KestrelServerOptions` 将 API 的 `Listen` 簇反射为 `Endpoint` 重载，因此可在同样的位置配置代码和配置终结点。 这些重载不使用名称，且只使用配置中的默认设置。

*更改代码中的默认值*

可以使用 `ConfigureEndpointDefaults` 和 `ConfigureHttpsDefaults` 更改 `ListenOptions` 和 `HttpsConnectionAdapterOptions` 的默认设置，包括重写之前的方案指定的默认证书。 需要在配置任何终结点之前调用 `ConfigureEndpointDefaults` 和 `ConfigureHttpsDefaults`。

```csharp
options.ConfigureEndpointDefaults(opt =>
{
    opt.NoDelay = true;
});

options.ConfigureHttpsDefaults(httpsOptions =>
{
    httpsOptions.SslProtocols = SslProtocols.Tls12;
});
```

*SNI 的 Kestrel 支持*

[服务器名称指示 (SNI)](https://tools.ietf.org/html/rfc6066#section-3) 可用于承载相同 IP 地址和端口上的多个域。 为了运行 SNI，客户端在 TLS 握手过程中将进行安全会话的主机名发送至服务器，从而让服务器可以提供正确的证书。 在 TLS 握手后的安全会话期间，客户端将服务器提供的证书用于与服务器进行加密通信。

Kestrel 通过 `ServerCertificateSelector` 回调支持 SNI。 每次连接调用一次回调，从而允许应用检查主机名并选择合适的证书。

SNI 支持要求：

* 在目标框架 `netcoreapp2.1` 上运行。 在 `netcoreapp2.0` 和 `net461` 上，回调也会调用，但是 `name` 始终为 `null`。 如果客户端未在 TLS 握手过程中提供主机名参数，则 `name` 也为 `null`。
* 所有网站在相同的 Kestrel 实例上运行。 Kestrel 在无反向代理时不支持跨多个实例共享一个 IP 地址和端口。

```csharp
WebHost.CreateDefaultBuilder()
    .UseKestrel((context, options) =>
    {
        options.ListenAnyIP(5005, listenOptions =>
        {
            listenOptions.UseHttps(httpsOptions =>
            {
                var localhostCert = CertificateLoader.LoadFromStoreCert(
                    "localhost", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var exampleCert = CertificateLoader.LoadFromStoreCert(
                    "example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var subExampleCert = CertificateLoader.LoadFromStoreCert(
                    "sub.example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var certs = new Dictionary(StringComparer.OrdinalIgnoreCase);
                certs["localhost"] = localhostCert;
                certs["example.com"] = exampleCert;
                certs["sub.example.com"] = subExampleCert;

                httpsOptions.ServerCertificateSelector = (connectionContext, name) =>
                {
                    if (name != null && certs.TryGetValue(name, out var cert))
                    {
                        return cert;
                    }

                    return exampleCert;
                };
            });
        });
    });
```

::: moniker-end

**绑定到 TCP 套接字**

[Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 方法绑定至 TCP 套接字，并可通过选项 lambda 配置 SSL 证书：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_TCPSocket&highlight=9-16)]

该示例为带有 [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions).的终结点配置 SSL。 可使用相同 API 为特定终结点配置其他 Kestrel 设置。

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

**绑定到 Unix 套接字**

可通过 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 侦听 Unix 套接字以提高 Nginx 的性能，如以下示例所示：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Program.cs?name=snippet_UnixSocket)]

**端口 0**

如果指定端口号 `0`，Kestrel 将动态绑定到可用端口。 以下示例演示如何确定 Kestrel 在运行时实际绑定到的端口：

[!code-csharp[](kestrel/samples/2.x/KestrelSample/Startup.cs?name=snippet_Configure&highlight=3-4,15-21)]

在应用运行时，控制台窗口输出指示可用于访问应用的动态端口：

```console
Listening on the following addresses: http://127.0.0.1:48508
```

**UseUrls、--urls 命令行参数、urls 主机配置键以及 ASPNETCORE_URLS 环境变量的限制**

使用以下方法配置终结点：

* [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
* `--urls` 命令行参数
* `urls` 主机配置键
* `ASPNETCORE_URLS` 环境变量

若要将代码用于 Kestrel 以外的服务器，这些方法非常有用。 但是，请注意以下限制：

* SSL 不能使用这些方法，除非 HTTPS 终结点配置中提供了默认证书（如本主题前面的部分所示，使用 `KestrelServerOptions` 配置或配置文件）。
* 如果同时使用 `Listen` 和 `UseUrls` 方法，`Listen` 终结点将覆盖 `UseUrls` 终结点。

**IIS 终结点配置**

使用 IIS 时，由 `Listen` 或 `UseUrls` 设置用于 IIS 覆盖绑定的 URL 绑定。 有关详细信息，请参阅 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)主题。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。 配置 URL 前缀和 Kestrel 使用的端口：

* [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) 扩展方法
* `--urls` 命令行参数
* `urls` 主机配置键
* ASP.NET Core 配置系统，包括 `ASPNETCORE_URLS` 环境变量

有关这些方法的详细信息，请参阅[承载](xref:fundamentals/host/index)。

**IIS 终结点配置**

使用 IIS 时，由 `UseUrls` 设置用于 IIS 覆盖绑定的 URL 绑定。 有关详细信息，请参阅 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)主题。

---

::: moniker range=">= aspnetcore-2.1"

## <a name="transport-configuration"></a>传输配置

对于 ASP.NET Core 2.1 版，Kestrel 默认传输不再基于 Libuv，而是基于托管的套接字。 这是 ASP.NET Core 2.0 应用升级到 2.1 时的一个重大更改，它调用 [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv) 并依赖于以下包中的一个：

* [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/)（直接包引用）
* [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)

对于使用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)且需要使用 Libuv 的 ASP.NET Core 2.1 或更高版本的项目：

* 将用于 [Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv/) 包的依赖项添加到应用的项目文件：

    ```xml
    <PackageReference Include="Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv" 
                      Version="2.1.0" />
    ```

* 调用 [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv)：

    ```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseLibuv()
                .UseStartup<Startup>();
    }
    ```

::: moniker-end

### <a name="url-prefixes"></a>URL 前缀

如果使用 `UseUrls`、`--urls` 命令行参数、`urls` 主机配置键或 `ASPNETCORE_URLS` 环境变量，URL 前缀可采用以下任意格式。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

仅 HTTP URL 前缀是有效的。 使用 `UseUrls` 配置 URL 绑定时，Kestrel 不支持 SSL。

* 包含端口号的 IPv4 地址

  ```
  http://65.55.39.10:80/
  ```

  `0.0.0.0` 是一种绑定到所有 IPv4 地址的特殊情况。

* 包含端口号的 IPv6 地址

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  ```

  `[::]` 是 IPv4 `0.0.0.0` 的 IPv6 等效项。

* 包含端口号的主机名

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  主机名、`*`和 `+` 并不特殊。 没有识别为有效 IP 地址或 `localhost` 的任何内容都将绑定到所有 IPv4 和 IPv6 IP。 若要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用，请使用 [HTTP.sys](xref:fundamentals/servers/httpsys) 或 IIS、Nginx 或 Apache 等反向代理服务器。

  > [!WARNING]
  > 如果在启用了主机筛选的情况下不使用反向代理，请启用[主机筛选](#host-filtering)。

* 包含端口号的主机 `localhost` 名称或包含端口号的环回 IP

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。 如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。 如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

* 包含端口号的 IPv4 地址

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  `0.0.0.0` 是一种绑定到所有 IPv4 地址的特殊情况。

* 包含端口号的 IPv6 地址

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  https://[0:0:0:0:0:ffff:4137:270a]:443/
  ```

  `[::]` 是 IPv4 `0.0.0.0` 的 IPv6 等效项。

* 包含端口号的主机名

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  主机名、`*` 和 `+` 并不特殊。 不是已识别 IP 地址或 `localhost` 的任何内容都将绑定到所有 IPv4 和 IPv6 IP。 若要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用，请使用 [WebListener](xref:fundamentals/servers/weblistener) 或 IIS、Nginx 或 Apache 等反向代理服务器。

* 包含端口号的主机 `localhost` 名称或包含端口号的环回 IP

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。 如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。 如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。

* Unix 套接字

  ```
  http://unix:/run/dan-live.sock
  ```

**端口 0**

如果指定端口号 `0`，Kestrel 将动态绑定到可用端口。 除 `localhost`外，任何主机名或 IP 都可绑定到端口 `0`。

在应用运行时，控制台窗口输出指示可用于访问应用的动态端口：

```console
Now listening on: http://127.0.0.1:48508
```

**SSL 的 URL 前缀**

如果调用 `https:` 扩展方法，请务必在 URL 前缀中包括 `UseHttps`：

```csharp
var host = new WebHostBuilder()
    .UseKestrel(options =>
    {
        options.UseHttps("testCert.pfx", "testPassword");
    })
   .UseUrls("http://localhost:5000", "https://localhost:5001")
   .UseContentRoot(Directory.GetCurrentDirectory())
   .UseStartup<Startup>()
   .Build();
```

> [!NOTE]
> 不能在相同端口上托管 HTTPS 和 HTTP。

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

---

## <a name="host-filtering"></a>主机筛选

尽管 Kestrel 支持基于前缀的配置（例如 `http://example.com:5000`），但 Kestrel 在很大程度上会忽略主机名。 主机 `localhost` 是一个特殊情况，用于绑定至环回地址。 除了显式 IP 地址以外的所有主机都绑定至所有公共 IP 地址。 这些信息都不用于验证请求 `Host` 标头。

::: moniker range="< aspnetcore-2.0"

解决方法是，使用主机标头筛选的反向代理的主机。 这是 ASP.NET Core 1.x 中唯一的 Kestrel 支持方案。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

解决方法是，使用中间件来根据 `Host` 标头筛选请求：

```csharp
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Primitives;
using Microsoft.Net.Http.Headers;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

// A normal middleware would provide an options type, config binding, extension methods, etc..
// This intentionally does all of the work inside of the middleware so it can be
// easily copy-pasted into docs and other projects.
public class HostFilteringMiddleware
{
    private readonly RequestDelegate _next;
    private readonly IList<string> _hosts;
    private readonly ILogger<HostFilteringMiddleware> _logger;

    public HostFilteringMiddleware(RequestDelegate next, IConfiguration config, ILogger<HostFilteringMiddleware> logger)
    {
        if (config == null)
        {
            throw new ArgumentNullException(nameof(config));
        }

        _next = next ?? throw new ArgumentNullException(nameof(next));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));

        // A semicolon separated list of host names without the port numbers.
        // IPv6 addresses must use the bounding brackets and be in their normalized form.
        _hosts = config["AllowedHosts"]?.Split(new[] { ';' }, StringSplitOptions.RemoveEmptyEntries);
        if (_hosts == null || _hosts.Count == 0)
        {
            throw new InvalidOperationException("No configuration entry found for AllowedHosts.");
        }
    }

    public Task Invoke(HttpContext context)
    {
        if (!ValidateHost(context))
        {
            context.Response.StatusCode = 400;
            _logger.LogDebug("Request rejected due to incorrect Host header.");
            return Task.CompletedTask;
        }

        return _next(context);
    }

    // This does not duplicate format validations that are expected to be performed by the host.
    private bool ValidateHost(HttpContext context)
    {
        StringSegment host = context.Request.Headers[HeaderNames.Host].ToString().Trim();

        if (StringSegment.IsNullOrEmpty(host))
        {
            // Http/1.0 does not require the Host header.
            // Http/1.1 requires the header but the value may be empty.
            return true;
        }

        // Drop the port

        var colonIndex = host.LastIndexOf(':');

        // IPv6 special case
        if (host.StartsWith("[", StringComparison.Ordinal))
        {
            var endBracketIndex = host.IndexOf(']');
            if (endBracketIndex < 0)
            {
                // Invalid format
                return false;
            }
            if (colonIndex < endBracketIndex)
            {
                // No port, just the IPv6 Host
                colonIndex = -1;
            }
        }

        if (colonIndex > 0)
        {
            host = host.Subsegment(0, colonIndex);
        }

        foreach (var allowedHost in _hosts)
        {
            if (StringSegment.Equals(allowedHost, host, StringComparison.OrdinalIgnoreCase))
            {
                return true;
            }

            // Sub-domain wildcards: *.example.com
            if (allowedHost.StartsWith("*.", StringComparison.Ordinal) && host.Length >= allowedHost.Length)
            {
                // .example.com
                var allowedRoot = new StringSegment(allowedHost, 1, allowedHost.Length - 1);

                var hostRoot = host.Subsegment(host.Length - allowedRoot.Length, allowedRoot.Length);
                if (hostRoot.Equals(allowedRoot, StringComparison.OrdinalIgnoreCase))
                {
                    return true;
                }
            }
        }

        return false;
    }
}
```

在 `Startup.Configure` 中注册上述 `HostFilteringMiddleware`。 请注意，[中间件注册的排序](xref:fundamentals/middleware/index#ordering)非常重要。 应在诊断中间件（例如 `app.UseExceptionHandler`）注册完成后立即进行注册。

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseBrowserLink();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseMiddleware<HostFilteringMiddleware>();

    app.UseMvcWithDefaultRoute();
}
```

中间件需要 appsettings.json/appsettings.\<EnvironmentName>.json 中的 `AllowedHosts` 键。 此值是以分号分隔的不带端口号的主机名列表：

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

解决方法是，使用主机筛选中间件。 主机筛选中间件由 [Microsoft.AspNetCore.HostFiltering](https://www.nuget.org/packages/Microsoft.AspNetCore.HostFiltering) 包提供，此包包含在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中（ASP.NET Core 2.1 或更高版本）。 该中间件由 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 添加，可调用 [AddHostFiltering](/dotnet/api/microsoft.aspnetcore.builder.hostfilteringservicesextensions.addhostfiltering)：

[!code-csharp[](kestrel/samples-snapshot/2.x/KestrelSample/Program.cs?name=snippet_Program&highlight=9)]

默认情况下，主机筛选中间件处于禁用状态。 要启用该中间件，请在 appsettings.json/appsettings.\<EnvironmentName>.json 中定义一个 `AllowedHosts` 键。 此值是以分号分隔的不带端口号的主机名列表：

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

appsettings.json：

```json
{
  "AllowedHosts": "example.com;localhost"
}
```

> [!NOTE]
> [转接头中间件](xref:host-and-deploy/proxy-load-balancer)同样提供 [ForwardedHeadersOptions.AllowedHosts](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.allowedhosts) 选项。 转接头中间件和主机筛选中间件具有适合不同方案的相似功能。 如果未保留主机标头，并且使用反向代理服务器或负载均衡器转接请求，则使用转接头中间件设置 `AllowedHosts` 比较合适。 将 Kestrel 用作边缘服务器或直接转接主机标头时，使用主机筛选中间件设置 `AllowedHosts` 比较合适。
>
> 有关转接头中间件的详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。

::: moniker-end

## <a name="additional-resources"></a>其他资源

* [Enforce HTTPS](xref:security/enforcing-ssl)
* [Kestrel 源代码](https://github.com/aspnet/KestrelHttpServer)
* [RFC 7230：消息语法和路由（5.4 节：主机）](https://tools.ietf.org/html/rfc7230#section-5.4)
* [配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)
