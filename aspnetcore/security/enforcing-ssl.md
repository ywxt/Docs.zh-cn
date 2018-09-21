---
title: 强制实施 HTTPS 在 ASP.NET Core
author: rick-anderson
description: 演示如何要求在 ASP.NET Core HTTPS/TLS web 应用。
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 6e16191b1a4627e683fd2281e5556b2a6e84c082
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523137"
---
# <a name="enforce-https-in-aspnet-core"></a>强制实施 HTTPS 在 ASP.NET Core

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本文档演示如何：

* 要求所有请求使用 HTTPS。
* 将所有 HTTP 请求重都定向到 HTTPS。

没有 API 可以防止客户端上的第一个请求发送敏感数据。

> [!WARNING]
> 不要**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。 `RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。 API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。 此类客户端可能会通过 HTTP 发送的信息。 Web Api 应具有下列任一：
>
> * 不侦听 HTTP。
> * 关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。

<a name="require"></a>
## <a name="require-https"></a>要求使用 HTTPS

::: moniker range=">= aspnetcore-2.1"

我们建议所有生产 ASP.NET Core web 应用调用：

* HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 所有 HTTP 请求重定向到 HTTPS。
* [UseHsts](#hsts)，HTTP 严格传输安全协议 (HSTS)。

### <a name="usehttpsredirection"></a>UseHttpsRedirection

下面的代码调用`UseHttpsRedirection`在`Startup`类：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

前面突出显示的代码：

* 使用默认[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`)。
* 使用默认[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)除非被重写 (null)`ASPNETCORE_HTTPS_PORT`环境变量或[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)。

> [!WARNING] 
>端口必须是可用于中间件重定向到 HTTPS。 如果没有端口不可用，则不会发生重定向到 HTTPS。 可以通过任何以下设置指定 HTTPS 端口：
> 
>* `HttpsRedirectionOptions.HttpsPort` 
>* `ASPNETCORE_HTTPS_PORT`环境变量。 
>* 在开发中，在 HTTPS url *launchsettings.json*。 
>* 直接在 Kestrel 或 HttpSys 上配置 HTTPS url。 

以下突出显示的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

调用`AddHttpsRedirection`只是用来更改的值` HttpsPort`或` RedirectStatusCode`;

前面突出显示的代码：

* 集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到`Status307TemporaryRedirect`，这是默认值。
* 设置 HTTPS 端口为 5001。 默认值为 443。

以下机制自动设置端口：

* 中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)时满足以下条件：

   * Kestrel 或 HTTP.sys 直接与 HTTPS 终结点一起使用 （也适用于使用 Visual Studio Code 的调试器中运行应用程序）。
   * 仅**一个 HTTPS 端口**应用使用。

* 使用 visual Studio:
   * IIS Express 已启用 HTTPS。
   * *launchSettings.json*设置`sslPort`IIS express。

> [!NOTE]
> 当应用程序运行时在反向代理 （例如，IIS，IIS Express），后面`IServerAddressesFeature`不可用。 必须手动配置端口。 如果端口未设置，请求不会重定向。

可以通过设置配置端口[https_port Web 主机配置设置](xref:fundamentals/host/web-host#https-port):

**密钥**: https_port  
**类型**：string  
**默认**： 未设置默认值。  
**设置使用**：`UseSetting`  
**环境变量**: `<PREFIX_>HTTPS_PORT` (前缀是`ASPNETCORE_`使用 Web 主机时。)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> 可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。 环境变量配置的服务器，，然后在中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。

如果没有端口设置：

* 请求不会重定向。
* 中间件将记录警告"无法确定重定向的 https 端口。"

> [!NOTE]
> 使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。 `AddRedirectToHttps` 此外可以设置的状态代码和端口时执行重定向。 有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。
>
> 当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。

::: moniker-end

::: moniker range="< aspnetcore-2.1"

[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于要求 HTTPS。 `[RequireHttpsAttribute]` 可以修饰控制器或方法，也可以全局应用。 若要全局应用该属性，将以下代码添加到`ConfigureServices`在`Startup`:

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

前面突出显示的代码要求所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。 以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。 中间件还允许应用执行重定向时设置的状态代码或状态代码和端口。

全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。 将应用`[RequireHttps]`属性设置为所有控制器/Razor 页面不会被视为与需要 HTTPS 全局一样安全。 不能保证`[RequireHttps]`时添加新的控制器和 Razor 页面应用属性。

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a>HTTP 严格传输安全协议 (HSTS)

每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全性 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是通过响应标头使用的 web 应用指定选择的安全增强功能。 当[浏览器支持 HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)收到此标头：

* 在浏览器将会阻止通过 HTTP 发送的任何通信的域的配置存储。 在浏览器强制通过 HTTPS 进行的所有通信。
* 在浏览器可防止用户使用不受信任或无效的证书。 在浏览器禁用允许用户暂时信任此证书的提示。

因为由客户端强制执行 HSTS 它具有一些限制：

* 客户端必须支持 HSTS。
* HSTS 要求至少一个成功的 HTTPS 请求能够建立 HSTS 策略。
* 应用程序必须检查每个 HTTP 请求和重定向或拒绝的 HTTP 请求。

ASP.NET Core 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。 下面的代码调用`UseHsts`时应用不在[开发模式](xref:fundamentals/environments):

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

`UseHsts` 不建议在开发过程中由于 HSTS 设置高度可缓存的浏览器。 默认情况下，`UseHsts`排除本地环回地址。

对于生产环境首次实现 HTTPS 初始 HSTS 将值设置为较小的值。 设置的值从小时数不超过一天的以防到时需要还原 HTTP 到 HTTPS 基础结构。 确信 HTTPS 配置的可持续发展中后，增加 HSTS 最大期限值;常用的值为一年。 

下面的代码：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* 设置预加载严格传输安全性标头的参数。 预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但要预加载 HSTS 站点上执行全新安装的 web 浏览器支持。 有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。
* 使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，这将 HSTS 策略应用到主机的子域。 
* 显式将严格传输安全性标头的最大期限参数设置为 60 天。 如果未设置，默认值为 30 天。 请参阅[最大期限指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。
* 添加`example.com`到主机以排除列表。

`UseHsts` 不包括以下环回主机：

* `localhost` : IPv4 环回地址。
* `127.0.0.1` : IPv4 环回地址。
* `[::1]` : IPv6 环回地址。

前面的示例演示如何添加其他主机。

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a>选择退出的 HTTPS 在项目创建

ASP.NET Core 2.1 或更高版本的 web 应用程序模板 （从 Visual Studio 或 dotnet 命令行） 启用[HTTPS 重定向](#require)和[HSTS](#hsts)。 对于不需要 HTTPS 的部署，你可以选择退出的 HTTPS。 例如，不需要其中 HTTPS 正在从外部在边缘，每个节点，使用 HTTPS 某些后端服务。

若要选择退出的 HTTPS:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

取消选中**配置为支持 HTTPS**复选框。

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

使用 `--no-https` 选项。 例如

```console
dotnet new webapp --no-https
```

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-set-up-a-developer-certificate-for-docker"></a>如何设置适用于 Docker 的开发人员证书

请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。

::: moniker-end

## <a name="additional-information"></a>其他信息

* [OWASP HSTS 浏览器支持](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)
