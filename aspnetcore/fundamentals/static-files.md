---
title: "使用 ASP.NET Core 中的静态文件"
author: rick-anderson
description: "了解如何处理和保护静态文件，并配置承载 ASP.NET 核心 web 应用中的中间件行为的静态文件。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/18/2018
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/static-files
ms.openlocfilehash: 60b205bf0a45e2965f9dab46f46956947ae513fd
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="work-with-static-files-in-aspnet-core"></a>使用 ASP.NET Core 中的静态文件

通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Scott Addie](https://twitter.com/Scott_Addie)

静态文件，如 HTML、 CSS、 映像和 JavaScript，作为的资产直接向客户端提供 ASP.NET Core 应用。 不需要若要启用对这些文件提供一些配置。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="serve-static-files"></a>为静态文件服务

静态文件存储在你的项目的 web 根目录。 默认目录是 *\<content_root > / wwwroot*，但它可以通过更改[UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_)方法。 请参阅[内容根](xref:fundamentals/index#content-root)和[Web 根](xref:fundamentals/index#web-root)有关详细信息。

应用程序的 web 主机必须让知道的内容的根目录。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

`WebHost.CreateDefaultBuilder`方法设置的内容的根到当前目录：

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

设置为当前目录的内容的根，通过调用[UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_)内`Program.Main`:

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

---

静态文件都可以访问通过相对于 web 根的路径。 例如， **Web 应用程序**项目模板包含多个文件夹内的*wwwroot*文件夹：

* **wwwroot**
  * **css**
  * **images**
  * **js**

要访问中的文件的 URI 格式*映像*子文件夹是*http://\<server_address > /images/\<image_file_name >*。 例如， *http://localhost:9189/images/banner3.svg*。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

如果面向.NET Framework，添加[Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/)包到你的项目。 如果面向的.NET 核心[Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)包括此包。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

添加[Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/)包到你的项目。

---

配置[中间件](xref:fundamentals/middleware)这样的静态文件提供服务。

### <a name="serve-files-inside-of-web-root"></a>为在 web 根目录内的文件服务

调用[UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_)方法内的`Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

无参数`UseStaticFiles`方法重载将标记为 servable web 根目录中的文件。 以下标记引用*wwwroot/images/banner1.svg*:

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

### <a name="serve-files-outside-of-web-root"></a>为在 web 根目录之外的文件服务

请考虑在 web 根目录之外的静态文件提供驻留在其中的目录层次结构：

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*

请求可以访问*banner1.svg*文件通过配置静态文件中间件，如下所示：

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

在前面的代码中， *MyStaticFiles*通过公开公开目录层次结构*StaticFiles* URI 段。 对请求*http://\<server_address > /StaticFiles/images/banner1.svg*提供*banner1.svg*文件。

以下标记引用*MyStaticFiles/images/banner1.svg*:

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a>设置 HTTP 响应标头

A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions)对象可以用于设置 HTTP 响应标头。 除了配置从 web 根的静态文件服务，以下代码将设置`Cache-Control`标头：

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append)方法中存在[Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/)包。

文件进行了公开可缓存 10 分钟 （600 秒）：

![已添加显示的缓存控制标头的响应标头](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a>静态文件授权

静态文件中间件不提供授权检查。 由它提供任何文件包括正在*wwwroot*，是可公开访问。 若要为文件服务基于授权：

* 将其外部存储*wwwroot*和访问静态文件中间件任何目录**和**
* 通过向其应用授权的操作方法提供它们。 返回[FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult)对象：

[!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a>启用目录浏览

目录浏览使你的 web 应用的用户看到的目录列表，以及在指定的目录内文件。 默认情况下，出于安全原因禁用目录浏览 (请参阅[注意事项](#considerations))。 启用目录浏览通过调用[UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_)中的方法`Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

添加所需的服务通过调用[AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_)方法从`Startup.ConfigureServices`:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

前面的代码中允许目录浏览的*wwwroot/images*文件夹使用 URL *http://\<server_address > / MyImages*，以链接到每个文件和文件夹：

![目录浏览](static-files/_static/dir-browse.png)

请参阅[注意事项](#considerations)上启用浏览时安全风险。

请注意两个`UseStaticFiles`调用在下面的示例。 第一次调用启用中的静态文件提供*wwwroot*文件夹。 第二个调用启用目录浏览的*wwwroot/images*文件夹使用 URL *http://\<server_address > / MyImages*:

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a>服务默认的文档

设置默认主页上提供了访问者的逻辑起点时访问您的网站。 若要为默认页上，而用户完全限定 URI 提供服务，调用[UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_)方法从`Startup.Configure`:

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> `UseDefaultFiles`前必须调用`UseStaticFiles`用于默认文件。 `UseDefaultFiles`是不实际处理该文件 URL 重写者。 启用通过静态文件中间件`UseStaticFiles`来处理该文件。

与`UseDefaultFiles`，文件夹搜索到的请求：

* *default.htm*
* *default.html*
* *index.htm*
* *index.html*

从列表中找到的第一个文件，就好像该请求是完全限定的 URI 提供服务。 浏览器 URL 将继续以反映所请求的 URI。

下面的代码更改到的默认文件名称*mydefault.html*:

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a>UseFileServer

[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_)将功能组合`UseStaticFiles`， `UseDefaultFiles`，和`UseDirectoryBrowser`。

以下代码允许静态文件和默认的文件的服务。 未启用目录浏览。

```csharp
app.UseFileServer();
```

下面的代码基于通过启用目录浏览的无参数的重载：

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

请考虑以下目录层次结构：

* **wwwroot**
  * **css**
  * **images**
  * **js**
* **MyStaticFiles**
  * **images**
      * *banner1.svg*
  * *default.html*

下面的代码使静态文件、 默认文件和目录浏览的`MyStaticFiles`:

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

`AddDirectoryBrowser`时，必须调用`EnableDirectoryBrowsing`属性值是`true`:

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

使用的文件层次结构和前面的代码，Url 被解析为，如下所示：

| URI            |                             响应  |
| ------- | ------|
| *http://\<server_address>/StaticFiles/images/banner1.svg*    |      MyStaticFiles/images/banner1.svg |
| *http://\<server_address>/StaticFiles*             |     MyStaticFiles/default.html |

如果没有默认已命名的文件存在于*MyStaticFiles*目录中， *http://\<server_address > / StaticFiles*返回具有可单击链接列出的目录：

![静态文件列表](static-files/_static/db2.png)

> [!NOTE]
> `UseDefaultFiles`和`UseDirectoryBrowser`使用 URL *http://\<server_address > / StaticFiles*不尾部反斜杠来触发客户端的情况下将重定向到*http://\<server_address > /StaticFiles /*。 请注意添加尾部反斜杠。 在文档中的相对 Url 被视为无效而无需尾随斜杠。

## <a name="fileextensioncontenttypeprovider"></a>FileExtensionContentTypeProvider

[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider)类包含`Mappings`充当 MIME 内容类型的文件扩展名的映射的属性。 在下面的示例中，多个文件扩展名有注册到已知的 MIME 类型。 *.Rtf*替换扩展，和*.mp4*中删除。

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

请参阅[MIME 内容类型](http://www.iana.org/assignments/media-types/media-types.xhtml)。

## <a name="non-standard-content-types"></a>非标准的内容类型

静态文件中间件理解几乎 400 已知的文件内容类型。 如果用户请求了未知的文件类型的文件，静态文件中间件将返回 HTTP 404 （未找到） 响应。 如果启用目录浏览，将显示文件的链接。 URI 将返回 HTTP 404 错误。

下面的代码启用为未知的类型，并呈现为图像未知的文件：

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

与前面的代码中，具有未知的内容类型的文件的请求返回作为映像。

> [!WARNING]
> 启用[ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes)存在安全风险。 默认情况下，处于禁用状态，建议不要其使用。 [FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider)提供为文件提供服务使用非标准扩展到更安全的替代方法。

### <a name="considerations"></a>注意事项

> [!WARNING]
> `UseDirectoryBrowser`和`UseStaticFiles`可能会泄漏机密。 强烈建议禁用目录浏览在生产环境中。 请仔细查看的目录启用通过`UseStaticFiles`或`UseDirectoryBrowser`。 整个目录和其子目录变得可公开访问。 应用商店中的文件适用于向公众提供一个专用的目录，如 *\<content_root > / wwwroot*。 这些文件分开 MVC 视图，Razor 页 (仅 2.x) 配置文件，等等。

* 通过公开的内容的 Url`UseDirectoryBrowser`和`UseStaticFiles`受到的区分大小写和基础文件系统的字符限制。 例如，Windows 不区分&mdash;Mac 和 Linux 不是。

* 承载于 IIS 使用 ASP.NET Core 应用[ASP.NET 核心模块 (ANCM)](xref:fundamentals/servers/aspnet-core-module)转发到应用程序，包括静态文件请求的所有请求。 IIS 静态文件处理程序未使用。 它具有没有机会之前通过 ANCM 处理这些处理请求。

* 完成以下步骤在 IIS 管理器来删除 IIS 静态文件处理程序在服务器或网站级别：
    1. 导航到**模块**功能。
    1. 选择**StaticFileModule**列表中。
    1. 单击**删除**中**操作**侧栏。

> [!WARNING]
> 如果启用了 IIS 静态文件处理程序**和**ANCM 配置不正确，静态文件提供服务。 发生这种情况，例如，如果*web.config*文件未部署。

* 放置代码文件 (包括*.cs*和*.cshtml*) 在应用程序项目的 web 根目录之外。 因此应用程序的客户端的内容与基于服务器的代码之间创建逻辑分隔。 这可防止服务器端代码被泄露。

## <a name="additional-resources"></a>其他资源

* [中间件](xref:fundamentals/middleware)

* [ASP.NET Core 简介](xref:index)
