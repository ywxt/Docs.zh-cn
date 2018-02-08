---
title: "ASP.NET Core 中的 HTTP.sys Web 服务器实现"
author: rick-anderson
description: "介绍 Windows 上适用于 ASP.NET Core 的 Web 服务器 HTTP.sys。 HTTP.sys 构建于 Http.Sys 内核模式驱动程序之上，是 Kestrel 的一种替代选择，可用来直接连接到 Internet，而无需使用 IIS。"
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: f36a86fc67e715165afd0c38992f9767f90cf3b4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a>ASP.NET Core 中的 HTTP.sys Web 服务器实现

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Chris Ross](https://github.com/Tratcher)

> [!NOTE]
> 本主题仅适用于 ASP.NET Core 2.0 及更高版本。 在早期版本的 ASP.NET Core 的中，HTTP.sys 被命名为 [WebListener](xref:fundamentals/servers/weblistener)。

HTTP.sys 是仅在 Windows 上运行的[适用于 ASP.NET Core 的 Web 服务器](index.md)。 它构建于 [Http.Sys 内核模式驱动程序](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)之上。 HTTP.sys 是 [Kestrel](kestrel.md) 的替代选择，提供了一些 Kestel 所没有的功能。 HTTP.sys 不能与 IIS 或 IIS Express 结合使用，因为它与 [ASP.NET Core 模块](aspnet-core-module.md)不兼容。

HTTP.sys 支持以下功能：

- [Windows 身份验证](xref:security/authentication/windowsauth)
- 端口共享
- 具有 SNI 的 HTTPS
- 基于 TLS 的 HTTP/2 (Windows 10)
- 直接文件传输
- 响应缓存
- WebSocket (Windows 8)

受支持的 Windows 版本：

- Windows 7 和 Windows Server 2008 R2 及更高版本

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="when-to-use-httpsys"></a>何时使用 HTTP.sys

对于需要将服务器直接公开到 Internet 而不使用 IIS 的部署，HTTP.sys 非常有用。

![HTTP.sys 直接与 Internet 进行通信](httpsys/_static/httpsys-to-internet.png)

由于 HTTP.sys 构建于 Http.Sys 之上，因此不需要反向代理服务器来抵御攻击。 Http.Sys 是一项成熟的技术，可以抵御多种攻击，并提供可靠、安全、可伸缩的全功能 Web 服务器。 IIS 本身作为 Http.Sys 之上的 HTTP 侦听器运行。 

当你需要 Kestrel 中没有的功能（如 Windows 身份验证）时，HTTP.sys 是内部部署的不错选择。

![HTTP.sys 直接与你的内部网络进行通信](httpsys/_static/httpsys-to-internal.png)

## <a name="how-to-use-httpsys"></a>如何使用 HTTP.sys

下面是主机操作系统和 ASP.NET Core 应用程序的安装任务概述。

### <a name="configure-windows-server"></a>配置 Windows Server

* 安装应用程序要求的 .NET 版本，例如 [.NET Core](https://www.microsoft.com/net/download/core) 或 [.NET Framework](https://www.microsoft.com/net/download/framework)。

* 预先注册 URL 前缀以绑定到 HTTP.sys，并设置 SSL 证书

   如果在 Windows 中不预先注册 URL 前缀，则必须使用管理员权限运行应用程序。 唯一的例外是，如果你使用端口号大于 1024 的 HTTP（不是 HTTPS）绑定到 localhost；在这种情况下不需要管理员权限。

   有关详细信息，请参阅本文后续部分的[如何预先注册前缀和配置 SSL](#preregister-url-prefixes-and-configure-ssl)。

* 打开防火墙端口以允许流量到达 HTTP.sys。

   可使用 netsh.exe 或 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)。

此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。

### <a name="configure-your-aspnet-core-application-to-use-httpsys"></a>配置 ASP.NET Core 应用程序以使用 HTTP.sys

* 如果使用 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 元包，则不需要安装包。 元包中包括 [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) 包。

* 在 `WebHostBuilder` 上调用 `Main` 方法中的 `UseHttpSys` 扩展方法，指定所需的任何 [HTTP.sys 选项](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)，如以下示例所示：

  [!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=11-19)]

### <a name="configure-httpsys-options"></a>配置 HTTP.sys 选项

以下是一些可以配置的 HTTP.sys 设置和限制。

**客户端最大连接数**

可使用 Program.cs 中的以下代码为整个应用程序设置并发打开 TCP 的最大连接数：

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=5)]

默认情况下，最大连接数不受限制 (NULL)。

**请求正文最大大小**

默认的请求正文最大大小为 30,000,000 字节，大约 28.6MB。

在 ASP.NET Core MVC 应用中替代限制的推荐方法是在操作方法上使用 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 属性：

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

以下示例演示如何为整个应用程序和每个请求配置约束：

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=6)]

可在 Startup.cs 中替代特定请求的设置：

[!code-csharp[](httpsys/sample/Startup.cs?name=snippet_Configure&highlight=9-10)]
 
如果在应用程序开始读取请求后尝试配置请求限制，则会引发异常。 通过 `IsReadOnly` 属性可知道，如果 `MaxRequestBodySize` 属性处于只读状态，则意味着配置限制已经太迟了。

有关其他 HTTP.sys 选项的信息，请参阅 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)。 

### <a name="configure-urls-and-ports-to-listen-on"></a>配置要侦听的 URL 和端口 

默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。 要配置 URL 前缀和端口，可使用 `UseUrls` 扩展方法、`urls` 命令行参数、ASPNETCORE_URLS 环境变量或 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs) 上的 `UrlPrefixes` 属性。 下面的代码示例使用 `UrlPrefixes`。

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=17)]

`UrlPrefixes` 的优点是，如果尝试添加格式错误的前缀，则会立即收到错误消息。 `UseUrls`（与 `urls` 和 ASPNETCORE_URLS 共享）的优点是，可在 Kestrel 和 HTTP.sys 之间更轻松地切换。

如果同时使用 `UseUrls`（`urls` 或 ASPNETCORE_URLS）和 `UrlPrefixes`，`UrlPrefixes` 中的设置会替代 `UseUrls` 中的设置。 有关详细信息，请参阅[托管](xref:fundamentals/hosting)。

HTTP.sys 使用 [HTTP 服务器 API UrlPrefix 字符串格式](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)。

> [!NOTE]
> 请确保在服务器上预先注册的 `UseUrls` 或 `UrlPrefixes` 中指定相同的前缀字符串。 

### <a name="dont-use-iis"></a>不使用 IIS

请确保应用程序未配置为运行 IIS 或 IIS Express。

在 Visual Studio 中，默认启动配置文件是针对 IIS Express 的。 若要作为控制台应用程序运行该项目，请手动更改所选配置文件，如以下屏幕截图中所示。

![选择控制台应用配置文件](httpsys/_static/vs-choose-profile.png)

## <a name="preregister-url-prefixes-and-configure-ssl"></a>预先注册 URL 前缀和配置 SSL

IIS 和 HTTP.sys 都依赖于基础 Http.Sys 内核模式驱动程序，以便侦听请求和执行初始化处理。 在 IIS 中，管理 UI 提供一种相对简单的方法来配置所有内容。 但是，需要自己配置 Http.Sys。 执行该操作的内置工具是 netsh.exe。 

通过 netsh.exe，可保留 URL 前缀并分配 SSL 证书。 该工具需要管理权限。

以下示例演示保留 80 和 443 端口的 URL 前缀所需的最低要求：

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

以下示例演示如何分配 SSL 证书：

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
```

下面是 netsh.exe 的参考文档：

* [Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)（超文本传输协议 (HTTP) 的 Netsh 命令）
* [UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)（UrlPrefix 字符串）

以下资源提供几个方案的详细说明。 涉及 HttpListener 的文章同样适用于 HTTP.sys，因为两者都基于 Http.Sys。

* [如何：使用 SSL 证书配置端口](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* [HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html)（HTTPS 通信 - 基于 HttpListener 的托管和客户端证书）这是很久之前的一个第三方博客，但仍有一些有用的信息。
* [How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/)（如何：使用 HttpListener 或 HTTP 服务器非托管代码 (C++) 作为 SSL 简单服务器进行演练），这也是很久之前的一个博客，但仍有一些有用的信息。

以下是一些比 netsh.exe 命令行更易使用的第三方工具。 它们不是由 Microsoft 提供或认可的。 默认情况下，这些工具以管理员身份运行，因为 netsh.exe 本身需要管理员权限。

* [http.sys 管理器](http://httpsysmanager.codeplex.com/)提供用于列出和配置 SSL 证书和选项、前缀保留和证书信任列表的 UI。 
* [HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) 允许用户列出或配置 SSL 证书和 URL 前缀。 UI 比 http.sys 管理器更加完善并且提供更多的配置选项，但在其他方面它提供类似的功能。 它不能创建新的证书信任列表 (CTL)，但可以分配现有证书信任列表。

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

## <a name="next-steps"></a>后续步骤

有关更多信息，请参见以下资源：

* [本文的示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)
* [HTTP.sys 源代码](https://github.com/aspnet/HttpSysServer/)
* [承载](xref:fundamentals/hosting)
