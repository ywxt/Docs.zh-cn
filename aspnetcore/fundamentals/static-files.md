---
title: "使用 ASP.NET Core 中的静态文件"
author: rick-anderson
description: "了解如何使用 ASP.NET Core 中的静态文件。"
keywords: "ASP.NET Core，静态文件、 静态资产，HTML、 CSS、 JavaScript"
ms.author: riande
manager: wpickett
ms.date: 4/07/2017
ms.topic: article
ms.assetid: e32245c7-4eee-4831-bd2e-915dbf9f5f70
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/static-files
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40c9a799c6ac8a2ce712df4b8fbf3c142ef3fd82
ms.sourcegitcommit: 8f4d4fad1ca27adf9e396f5c205c9875a3963664
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-static-files-in-aspnet-core"></a>使用 ASP.NET Core 中的静态文件

<a name="fundamentals-static-files"></a>

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

静态文件，如HTML，CSS，图像和JavaScript，是ASP.NET Core应用程序可以直接向客户端提供的资产。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="serving-static-files"></a>为静态文件提供服务

静态文件通常位于`web root`（*<content-root>/wwwroot*）文件夹中。 请参阅[内容根目录](xref:fundamentals/index#content-root)和[Web 根目录](xref:fundamentals/index#web-root)获取更多信息。 您通常将内容根目录设置为当前目录，以便在开发过程中找到项目的`web root`目录。

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs?highlight=5&start=12&end=22)]

静态文件可以存储在`web root`目录下的任何文件夹中，并以相对路径访问该根目录。 例如，当您使用 Visual Studio 创建默认 Web 应用程序项目时，在*wwwroot*文件夹中创建了几个文件夹 - *css*，*images* 和 *js*。 访问 *image* 子文件夹中的图像的URI如下：

* `http://<app>/images/<imageFileName>`
* `http://localhost:9189/images/banner3.svg`

为了提供静态文件访问，您必须配置[中间件](middleware.md)以将静态文件添加到管道。 可以通过将 *Microsoft.AspNetCore.StaticFiles* 包的依赖项添加到项目，然后从 `Startup.Configure` 调用 `UseStaticFiles` 扩展方法来配置静态文件中间件：

[!code-csharp[Main](../fundamentals/static-files/sample/StartupStaticFiles.cs?highlight=3&name=snippet1)]

`app.UseStaticFiles();`使`web root`(默认情况下为*wwwroot*) 目录中的文件可用。 稍后我将介绍如何使用 `UseStaticFiles` 来让其他目录中的内容可用。

您必须引用 NuGet 包"Microsoft.AspNetCore.StaticFiles"。

> [!NOTE]
> `web root`默认为 *wwwroot* 目录，但你也可以使用 `UseWebRoot` 来设置 `web root` 目录。

假设您有一个项目层次结构，您希望提供的静态文件位于 `web root` 目录之外。 例如：

* wwwroot
  * css
  * images
  * ...
* MyStaticFiles
  * test.png

对于访问 *test.png* 的请求，请按如下方式配置静态文件中间件：

[!code-csharp[Main](../fundamentals/static-files/sample/StartupTwoStaticFiles.cs?highlight=5,6,7,8,9,10&name=snippet1)]

对请求`http://<app>/StaticFiles/test.png`将提供*test.png*文件。

`StaticFileOptions()` 可以设置响应标头。 例如，下面的代码设置从 `wwwroot` 文件夹提供静态文件，并设置 `Cache-Control` 标头使其可公开缓存10分钟（600秒）：

[!code-csharp[Main](../fundamentals/static-files/sample/StartupAddHeader.cs?name=snippet1)]

[HeaderDictionaryExtensions.Append](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) 方法可从 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 包中获取。 如果该方法不可用，则将 `using Microsoft.AspNetCore.Http;` 添加到您的 *csharp* 文件中。

![响应标头显示已添加 Cache-Control 标头](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a>静态文件授权

静态文件模块**不**提供授权检查。 它所提供的任何文件，包括 *wwwroot* 下的文件都是公开的。 若要基于授权来提供文件：

* 将它们存储在 *wwwroot* 和静态文件中间件可访问的任何目录之外，**并且**

* 通过控制器操作提供它们，返回已应用了授权的 *FileResult*

## <a name="enabling-directory-browsing"></a>启用目录浏览

目录浏览允许您的 Web 应用程序的用户查看指定目录内的目录和文件的列表。默认情况下，目录浏览由于安全原因被禁用（请参阅[注意事项](#considerations)）。 若要启用目录浏览，请从 `Startup.Configure` 调用 `UseDirectoryBrowser` 扩展方法：

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?name=snippet1)]

并通过从 `Startup.ConfigureServices` 中调用 `AddDirectoryBrowser` 扩展方法来添加所需的服务：

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?name=snippet2)]

上面的代码允许使用形如 http://<app>/MyImages 的 URL 来浏览 *wwwroot/images* 目录，以链接到每个文件和文件夹：

![目录浏览](static-files/_static/dir-browse.png)

启用浏览时请参阅有关安全风险的[注意事项](#considerations)。

请注意两个 `app.UseStaticFiles` 调用。 第一个需要在 *wwwroot* 文件夹中提供CSS，图像和JavaScript，第二个调用是为了使用形如 http://<app>/MyImages 的 URL 来浏览 *wwwroot/images* 目录：

[!code-csharp[Main](static-files/sample/StartupBrowse.cs?highlight=3,5&name=snippet1)]

## <a name="serving-a-default-document"></a>提供默认文档

设置一个默认主页可以在站点访问者访问你的站点时提供一个入口。为了让您的 Web 应用程序在不需要用户完全限定 URI 的情况下提供默认页面，请在 `Startup.Configure` 中调用 `UseDefaultFiles` 扩展方法，如下所示。

[!code-csharp[Main](../fundamentals/static-files/sample/StartupEmpty.cs?highlight=3&name=snippet1)]

> [!NOTE]
> `UseDefaultFiles` 必须在 `UseStaticFiles` 之前调用以提供默认文件。 `UseDefaultFiles` 是一个 URL 重写器，并不实际提供该文件。 你必须启用静态文件中间件 (`UseStaticFiles`) 来提供该文件。

使用 `UseDefaultFiles`，对文件夹的请求将搜索：

* default.htm
* default.html
* index.htm
* index.html

从列表中找到的第一个文件将被提供给用户，就像该请求是完全限定的 URI 一样（尽管浏览器的 URL 将继续显示所请求的 URI）。

下面的代码演示如何将默认文件的名称更改为 *mydefault.html*。

[!code-csharp[Main](static-files/sample/StartupDefault.cs?name=snippet1)]

## <a name="usefileserver"></a>UseFileServer

`UseFileServer` 结合了 `UseStaticFiles`，`UseDefaultFiles`，和`UseDirectoryBrowser` 的功能。

下面的代码启用静态文件和默认文件以提供访问，但不允许目录浏览:

```csharp
app.UseFileServer();
   ```

以下代码启用静态文件，默认文件和目录浏览：

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
   ```

在启用浏览时，请参阅有关安全风险的[注意事项](#considerations)。如同使用 `UseStaticFiles`、`UseDefaultFiles` 和 `UseDirectoryBrowser` 一样，如果您希望提供 `web root` 之外的文件，您可以实例化并配置一个 `FileServerOptions` 对象，将其作为参数传递给 `UseFileServer`。例如，在您的 Web 应用程序中给定以下目录层次结构:

* wwwroot

  * css

  * images

  * ...

* MyStaticFiles

  * test.png

  * default.html

使用上面的层次结构示例，您可能想要启用静态文件、默认文件和浏览 `MyStaticFiles` 目录。在下面的代码片段中，这是通过一个对 `FileServerOptions` 的调用完成的。

[!code-csharp[Main](static-files/sample/StartupUseFileServer.cs?highlight=5,6,7,8,9,10,11&name=snippet1)]

如果 `enableDirectoryBrowsing` 设置为 `true`, 您需要从`Startup.ConfigureServices` 调用 `AddDirectoryBrowser` 扩展方法:

[!code-csharp[Main](static-files/sample/StartupUseFileServer.cs?name=snippet2)]

使用上面的文件层次结构和代码：

| URI            |                             响应  |
| ------- | ------|
| `http://<app>/StaticFiles/test.png`    |      MyStaticFiles/test.png |
| `http://<app>/StaticFiles`              |     MyStaticFiles/default.html |

如果在 `MyStaticFiles` 目录中没有默认的命名文件，则 http://<app>/StaticFiles 以可单击的链接返回目录列表:

![静态文件列表](static-files/_static/db2.PNG)

> [!NOTE]
> `UseDefaultFiles` 和 `UseDirectoryBrowser` 将使用没有尾部斜杠的形如 http://<app>/StaticFiles 的 URL，并导致客户端重定向到 http://<app>/StaticFiles/(添加尾部斜杠)。如果没有尾部斜杠，文档中的相对 URL 将是不正确的。

## <a name="fileextensioncontenttypeprovider"></a>FileExtensionContentTypeProvider

`FileExtensionContentTypeProvider` 类包含一个集合，将文件扩展名映射到 MIME 内容类型。在下面的示例中，几个文件扩展名注册为已知的 MIME 类型。“.rtf”被替换。“.mp4”被删除。

[!code-csharp[Main](../fundamentals/static-files/sample/StartupFileExtensionContentTypeProvider.cs?highlight=3,4,5,6,7,8,9,10,11,12,19&name=snippet1)]

请参阅[MIME 内容类型](http://www.iana.org/assignments/media-types/media-types.xhtml)。

## <a name="non-standard-content-types"></a>非标准的内容类型

ASP.NET 静态文件中间件理解近400种已知的文件内容类型。如果用户请求了一个未知文件类型的文件，则静态文件中间件会返回一个 HTTP 404 (Not Found)响应。如果启用了目录浏览，将显示一个指向该文件的链接，但 URI 将返回一个 HTTP 404 错误。

以下代码启用支持未知类型，并将未知文件呈现为图像。

[!code-csharp[Main](static-files/sample/StartupServeUnknownFileTypes.cs?name=snippet1)]

使用上面的代码中，具有未知的内容类型的文件的请求将返回为映像。

>[!WARNING]
> 启用 `ServeUnknownFileTypes` 存在安全风险，并不建议这么做。  `FileExtensionContentTypeProvider`（上文所述）提供了一个更安全的替代方法来为非标准扩展名的文件提供服务。

### <a name="considerations"></a>注意事项

>[!WARNING]
> `UseDirectoryBrowser` 和 `UseStaticFiles` 可能会泄漏机密。我们建议您 **不要** 在生产环境中启用目录浏览。请小心使用 `UseStaticFiles` 或 `UseDirectoryBrowser`，因为整个目录和所有子目录都是可以访问的。我们建议将公共内容保存在自己的目录中，例如<content root>/wwwroot，与应用程序视图、配置文件等分开。

* 使用 `UseDirectoryBrowser`和 `UseStaticFiles` 公开的内容的 URL 受其底层文件系统的大小写敏感性和字符限制。例如，Windows是大小写不敏感的，但是Mac和Linux不是。

* 在IIS中承载的 ASP.NET Core 应用程序使用 ASP.NET Core 模块将所有请求转发到应用程序，包括对静态文件的请求。IIS静态文件处理程序不会被使用，因为在请求被 ASP.NET Core 模块处理之前，它没有机会处理它们。

* 若要删除 IIS 静态文件处理程序 （在服务器或网站级别）：

     * 导航到**Modules**功能

     * 在列表中选择**StaticFileModule**

     * 在**Actions**侧栏中点击**删除**

>[!WARNING]
> 如果启用了IIS静态文件处理程序，**并且** ASP.NET Core 模块(ANCM)未正确配置(例如 *web.config* 未被部署)，将提供静态文件。

* 代码文件(包括 c# 和 Razor)应该放在应用程序项目的 `web root` 之外(默认情况下是*wwwroot*)。这将在应用程序的客户端内容和服务器端源代码之间创建一个清晰的分离，从而防止服务器端代码被泄露。

## <a name="additional-resources"></a>其他资源

* [中间件](middleware.md)

* [ASP.NET Core 简介](../index.md)
