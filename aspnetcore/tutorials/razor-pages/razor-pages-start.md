---
title: 在 ASP.NET Core 中开始使用 Razor Pages
author: rick-anderson
monikerRange: '>= aspnetcore-2.2'
description: 此系列教程演示了如何在 ASP.NET Core 中使用 Razor Pages。 了解如何创建模型、为 Razor Pages 生成代码、将 Entity Framework Core 和 SQL Server 用于数据访问、添加搜索功能、添加输入验证及使用迁移更新模型。
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 1152ebfcee48a46ecd28c941fce32d3fc1e05c41
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861623"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a>教程：在 ASP.NET Core 中开始使用 Razor Pages

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。

该应用管理电影标题的数据库。 您将学习如何：

> [!div class="checklist"]
> * 创建 Razor 页面 Web 应用。
> * 添加和构架模型。
> * 使用数据库。
> * 添加搜索和验证。

在结束时，你会获得可以管理和显示电影标题项的应用。

[!INCLUDE[](~/includes/rp/download.md)]

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-web-app"></a>创建 Razor Web 应用

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从 Visual Studio“文件”菜单中选择“新建” > “项目”。
* 创建新的 ASP.NET Core Web 应用程序。 将项目命名为“RazorPagesMovie”。 将项目命名为“RazorPagesMovie”，以便命名空间在你复制/粘贴代码时相互匹配。
 ![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2.1.png)

* 在下拉列表中选择“ASP.NET Core 2.2”，然后选择“Web 应用程序”。

  ![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2_2.2.png)

  创建以下初学者项目：

  ![“解决方案资源管理器”](razor-pages-start/_static/se2.2.png)

* 按 **Ctrl-F5** 以在不使用调试程序的情况下运行。

  Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。 地址栏显示 `localhost:port#`，而不是显示 `example.com`。 这是因为 `localhost` 是本地计算机的标准主机名。 Localhost 仅为来自本地计算机的 Web 请求提供服务。 Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。 在上图中，端口号为 5001。 运行应用时，将看到不同的端口号。

  使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。 许多开发人员更喜欢使用非调试模式刷新页面并查看更改。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* 打开[集成终端](https://code.visualstudio.com/docs/editor/integrated-terminal)。
* 将目录更改为 (`cd`) 包含项目的文件夹。
* 运行下面的命令：

   ```console
   dotnet new webapp -o RazorPagesMovie
   code -r RazorPagesMovie
   ```

  * 一个对话框随即出现，其中包含“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”  选择“是”

  * `dotnet new webapp -o RazorPagesMovie`：在 RazorPagesMovie 文件夹中创建新的 Razor Pages 项目。
  * `code -r RazorPagesMovie`：在 Visual Studio Code 中加载 RazorPagesMovie.csproj 项目文件。

### <a name="launch-the-app"></a>启动应用

* 按 **Ctrl-F5** 以在不使用调试程序的情况下运行。

  Visual Studio Code 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5001`。 地址栏显示 `localhost:port:5001`，而不是显示 `example.com`。 这是因为 `localhost` 是本地计算机的标准主机名。 Localhost 仅为来自本地计算机的 Web 请求提供服务。

  使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。 许多开发人员更喜欢使用非调试模式刷新页面并查看更改。

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

从终端运行以下命令：

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

上述命令使用 [.NET Core CLI](/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。 打开浏览器，转到 http://localhost:5000 查看应用程序。

## <a name="open-the-project"></a>打开项目

按 Ctrl+C 关闭应用程序。

在 Visual Studio 中，选择“文件”>“打开”，然后选择“RazorPagesMovie.csproj”文件。

### <a name="launch-the-app"></a>启动应用

选择“运行”>“开始执行(不调试)”以启动应用。 Visual Studio 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5001`。

<!-- End of VS tabs -->

---

* 选择“接受”以同意跟踪。 此应用不会跟踪个人信息。 模板生成的代码包含有助于符合[一般数据保护条例 (GDPR)](xref:security/gdpr) 的资产。

  ![主页或索引页](razor-pages-start/_static/homeGDPR2.2.png)

  下图展示了接受跟踪后的应用：

  ![主页或索引页](razor-pages-start/_static/home2.2.png)

## <a name="project-files-and-folders"></a>项目文件和文件夹

下表列出了项目中的文件和文件夹。 此时在本教程中，Startup.cs 是最有必要了解的文件。 无需查看下面提供的每一个链接。 需要详细了解项目中的某个文件或文件夹时，可参考此处提供的链接。

| 文件或文件夹              | 目标 |
| ----------------- | ------------ |
| *wwwroot* | 包含静态文件。 请参阅[静态文件](xref:fundamentals/static-files)。 |
| *页* | [Razor Pages](xref:razor-pages/index)的文件夹。 |
| *appsettings.json* | [配置](xref:fundamentals/configuration/index) |
| *Program.cs* | [托管](xref:fundamentals/host/index) ASP.NET Core 应用。|
| *Startup.cs* | 配置服务和请求管道。 请参阅[启动](xref:fundamentals/startup)。|

### <a name="the-pages-folder"></a>“页面”文件夹

_Layout.cshtml 文件包含常见的 HTML 元素（脚本和样式表），并设置应用程序的布局。 例如，单击“RazorPagesMovie”、“主页”或“隐私”时，将看到相同的元素。 常见的元素包括顶部的导航菜单和窗口底部的标题。 请参阅[布局](xref:mvc/views/layout)了解详细信息。

_ViewImports.cshtml 文件包含要导入每个 Razor 页面的 Razor 指令。 请参阅[导入共享指令](xref:mvc/views/layout#importing-shared-directives)了解详细信息。

*_ViewStart.cshtml*将 Razor Pages `Layout` 属性设置为使用 *_Layout.cshtml* 文件。 请参阅[布局](xref:mvc/views/layout)了解详细信息。

_ValidationScriptsPartial.cshtml 文件提供对 [jQuery](https://jquery.com/) 验证脚本的引用。 在本教程的后续部分中添加 `Create` 和 `Edit` 页面时，会使用 _ValidationScriptsPartial.cshtml 文件。

提供 `Index`、`Error` 和 `Privacy` 页面以用于：

* `Index`：启动应用。
* `Error`：显示错误信息。
* `Privacy`：指定有关站点隐私策略的详细信息。

对于本教程，不使用前面的页面。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

<a name="f7"></a>
### <a name="use-f7-to-toggle-between-a-razor-page-and-the-pagemodel"></a>使用 F7 在 Razor 页面和 PageModel 之间切换

使用 F7 在 Razor 页面（\*.cshtml 文件）与 C# 文件 (\*.cshtml.cs) 之间切换。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

<!-- TODO review  Need something in these tabs -->

按照约定，Razor 页面（\*.cshtml 文件）和关联 `PageModel` 具有相同的根文件名称。

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

按照约定，Razor 页面（\*.cshtml 文件）和关联 `PageModel` 具有相同的根文件名称。

---

> [!div class="step-by-step"]
> [下一篇：添加模型](xref:tutorials/razor-pages/model)