---
title: 强制实施 HTTPS 在 ASP.NET 核心
author: rick-anderson
description: 演示如何要求在 ASP.NET Core HTTPS/TLS web 应用。
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: f49a7846149385125390285e2f1332d8e40642c0
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35725931"
---
# <a name="enforce-https-in-aspnet-core"></a>强制实施 HTTPS 在 ASP.NET 核心

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本文档说明如何：

* 所有请求需要 HTTPS。
* 所有 HTTP 请求重都定向到 HTTPS。

> [!WARNING]
> 执行**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。 `RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。 API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。 此类客户端可能会通过 HTTP 发送信息。 Web Api 应具有下列任一：
>
> * 不在 HTTP 上侦听。
> * 关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。

<a name="require"></a>
## <a name="require-https"></a>需要 HTTPS

::: moniker range=">= aspnetcore-2.1"

我们建议所有 ASP.NET 核心 web 应用都调用 HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 将所有 HTTP 请求重定向到 HTTPS。

下面的代码调用`UseHttpsRedirection`中`Startup`类：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

下面的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

前面的突出显示的代码：

* 集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到`Status307TemporaryRedirect`，这是默认值。 生产应用程序应调用[UseHsts](#hsts)。
* 将 HTTPS 端口设置为 5001。 默认值为 443。

使用以下机制将自动设置端口：

* 该中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)当以下条件适用：
  - 直接与 HTTPS 终结点使用 kestrel 还是 HTTP.sys （也适用于使用 Visual Studio 代码的调试器中运行应用程序）。
  - 仅**一个 HTTPS 端口**应用使用。
* 使用 visual Studio:
  - IIS Express 中包含启用 HTTPS。
  - *launchSettings.json*设置`sslPort`IIS express。

> [!NOTE]
> 反向代理 （例如，IIS，IIS Express），后面运行应用时`IServerAddressesFeature`不可用。 必须手动配置端口。 如果未设置端口，请求不重定向。

可以通过设置配置端口:

* `ASPNETCORE_HTTPS_PORT` 环境变量。
* `http_port` 主机配置项 (例如，通过*hostsettings.json*或命令行自变量)。
* [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)。 请参阅前面的示例演示如何设置为 5001 的端口。

> [!NOTE]
> 可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。 环境变量配置服务器，，然后该中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。

如果没有端口设置：

* 请求没有重定向。
* 该中间件记录警告。

> [!NOTE]
> 使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。 `AddRedirectToHttps` 此外可以设置的状态代码和端口执行重定向时。 有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。
>
> 当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。

::: moniker-end

::: moniker range="< aspnetcore-2.1"

[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于需要 HTTPS。 `[RequireHttpsAttribute]` 可修饰控制器或方法，或可以全局应用。 若要全局应用该属性，以下代码添加到`ConfigureServices`中`Startup`:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

前面的突出显示的代码中需要的所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。 以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。 该中间件还允许应用程序以执行重定向时设置的状态代码或状态代码和端口。

全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。 应用`[RequireHttps]`特性应用到所有控制器/Razor 页面不会被视为尽可能安全全局需要 HTTPS。 你不能保证`[RequireHttps]`添加新控制器和 Razor 页时应用特性。

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a>HTTP 严格的传输安全协议 (HSTS)

每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是由 web 应用程序通过使用特殊的响应标头指定可以选择使用的安全增强。 支持的浏览器收到此标头后该浏览器将阻止从正在通过 HTTP 发送到指定的域的任何通信，并改为将通过 HTTPS 发送的所有通信。 它还可以防止 HTTPS 单击通过在浏览器上的提示。

ASP.NET 核心 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。 下面的代码调用`UseHsts`时应用程序不在[开发模式](xref:fundamentals/environments):

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

`UseHsts` 不建议在开发过程中由于 HSTS 标头是高度可缓存浏览器。 默认情况下，`UseHsts`排除本地环回地址。

下面的代码：

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* 设置预加载参数 Strict 传输安全标头。 预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但若要预加载 HSTS 站点上执行全新安装的 web 浏览器都支持。 有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。
* 使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，该方案 HSTS 策略适用于主机子域。 
* 显式将 Strict 传输安全标头到的最大有效期参数设置为 60 天。 如果未设置，默认值为 30 天。 请参阅[最长时间指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。
* 将添加`example.com`到的主机排除列表。

`UseHsts` 排除以下环回主机：

* `localhost` : IPv4 环回地址。
* `127.0.0.1` : IPv4 环回地址。
* `[::1]` : IPv6 环回地址。

前面的示例演示如何添加其他主机。
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a>选择退出的 HTTPS 在项目创建

ASP.NET 核心 2.1 或更高版本的 web 应用程序模板 （从 Visual Studio 或 dotnet 命令行） 启用[HTTPS 重定向](#require)和[HSTS](#hsts)。 对于不需要 HTTPS 的部署，你可以选择退出的 HTTPS。 例如，不需要其中 HTTPS 正在处理外部在边缘，在每个节点使用 HTTPS 某些后端服务。

若要选择退出的 HTTPS:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

取消选中**针对 HTTPS 配置**复选框。

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

使用 `--no-https` 选项。 例如

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a>如何为 Docker 设置开发人员证书

请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。

::: moniker-end
