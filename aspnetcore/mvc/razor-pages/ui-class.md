---
title: ASP.NET Core 的类库中的可重用 Razor UI
author: Rick-Anderson
description: 说明如何在类库中创建可重用 Razor UI。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/31/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: advanced
uid: mvc/razor-pages/ui-class
ms.openlocfilehash: 44091ab8ab5d69a5975e191fd00fca1d1d957238
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="create-reusable-ui-using-the-razor-class-library-project-in-aspnet-core"></a>使用 ASP.NET Core 中的 Razor 类库项目创建可重用 UI。

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

Razor 视图、页面、控制器、页模型和数据模型可以创建在 Razor 类库 (RCL) 中。 RCL 可以打包并重复使用。 应用程序可以包括 RCL，并重写其中包含的视图和页面。 如果在 Web 应用和 RCL 中都能找到视图、分部视图或 Razor 页面，则 Web 应用中的 Razor 标记（.cshtml 文件）优先。

此功能需要 [!INCLUDE[](~/includes/2.1-SDK.md)]

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="create-a-class-library-containing-razor-ui"></a>创建一个包含 Razor UI 的类库

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从 Visual Studio“文件”菜单中选择“新建” > “项目”。
* 选择“ASP.NET Core Web 应用程序”。
* 验证是否已选择 ASP.NET Core 2.1 或更高版本。
* 选择“Razor 类库” > “确定”。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

从命令行中运行 `dotnet new razorclasslib`。 例如:

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
```

有关详细信息，请查看 [dotnet new](/dotnet/core/tools/dotnet-new)。

------
将 Razor 文件添加到 RCL。

建议将 RCL 内容转至“区域”文件夹。 


## <a name="referencing-razor-class-library-content"></a>引用 Razor 类库内容

可以通过以下方式引用 RCL：

* NuGet 包。 请参阅[创建 NuGet 包](/nuget/create-packages/creating-a-package)、[dotnet 添加包](/dotnet/core/tools/dotnet-add-package)和[创建和发布 NuGet 包](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)。
* {ProjectName}.csproj。 请查看 [dotnet-add 引用](/dotnet/core/tools/dotnet-add-reference)。

### <a name="partial-files-access-in-the-rcl"></a>RCL 中的分部文件访问

对于 RCL 之外的内容，ASP.NET Core 运行时不会搜索 RCL 中的分部文件。

例如，在示例下载中，不能在 WebApp1\Pages\About.cshtml 中引用 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 分部视图。 然而 RCL (RazorUIClassLib/) 中的页面可以访问 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtm。

## <a name="walkthrough-create-a-razor-class-library-project-and-use-from-a-razor-pages-project"></a>演练：创建 Razor 类库项目并从 Razor 页面项目使用它

可以下载并测试[完整项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)，无需创建项目。 示例下载包含附加代码和链接，以方便测试项目。 可以在[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6098)中留下反馈，评论下载示例和分步说明的对比。

### <a name="test-the-download-app"></a>测试下载应用

如果尚未下载已完成的应用，并更愿意创建演练项目，请跳转至[下一节](#create-a-razor-class-library)。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

在 Visual Studio 中打开 .sln 文件。 运行应用。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

在 cli 目录中的命令提示符下生成 RCL 和 Web 应用。

``` CLI
dotnet build
```

移动至 WebApp1 目录，并运行应用：

``` CLI
dotnet run
```
------

按[“测试 Test WebApp1”](#test)中的说明进行操作

## <a name="create-a-razor-class-library"></a>创建 Razor 类库

本部分创建 Razor 类库 (RCL)。 将 Razor 文件添加到 RCL。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

创建 RCL 项目：

* 从 Visual Studio“文件”菜单中选择“新建” > “项目”。
* 选择“ASP.NET Core Web 应用程序”。
* 将应用命名为 RazorUIClassLib。
* 验证是否已选择 ASP.NET Core 2.1 或更高版本。
* 选择“Razor 类库” > “确定”。

创建 Razor 页面 Web 应用：

* 在解决方案资源管理器中，右键单击解决方案 >“添加” >  “新建项目”。
* 选择“ASP.NET Core Web 应用程序”。
* 将应用命名为 WebApp1。
* 验证是否已选择 ASP.NET Core 2.1 或更高版本。
* 选择“Web 应用程序” > “确定”。

### <a name="add-razor-files-and-folders-to-the-project"></a>将 Razor 文件和文件夹添加到该项目。

* 添加一个名为 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 的 Razor 分部视图文件。
* 使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 中的标记：

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* 将 WebApp1 项目中的 _ViewStart.cshtml 文件复制到 RazorUIClassLib/Areas/MyFeature/Pages/_ViewStart.cshtml。

  使用 Razor 页面项目的布局需要 [Viewstart](xref:mvc/views/layout#running-code-before-each-view) 文件。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

从命令行运行以下命令：

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
dotnet new page -n _Message -np -o RazorUIClassLib/Areas/MyFeature/Pages/Shared
dotnet new viewstart -o RazorUIClassLib/Areas/MyFeature/Pages
```

前面的命令：

* 创建 `RazorUIClassLib` Razor 类库 (RCL)。
* 创建 Razor _Message 页面，并将其添加至 RCL。 `-np` 参数创建不含 `PageModel` 的页面。
* 创建 [viewstart](xref:mvc/views/layout#running-code-before-each-view) 文件并将其添加到 RCL。

使用 Razor 页面项目的布局需要 Viewstart 文件（将在下一节中添加）。

更新 Razor 页面：

* 使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 中的标记：

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* 使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml 中的标记：

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml)]

使用分步视图 (`<partial name="_Message" />`) 需要 `@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`。 可以添加一个 _ViewImports.cshtml 文件，无需包含 `@addTagHelper` 指令。 例如:

``` CLI
dotnet new viewimports -o RazorUIClassLib/Areas/MyFeature/Pages
```

有关 Viewimports 的详细信息，请参阅[导入共享指令](xref:mvc/views/layout#importing-shared-directives)

* 生成类库以验证是否不存在编译器错误：

``` CLI
dotnet build RazorUIClassLib
```

生成输出内容包含 RazorUIClassLib.dll 和 RazorUIClassLib.Views.dll。 RazorUIClassLib.Views.dll 包含已编译的 Razor 内容。

------

### <a name="use-the-razor-ui-library-from-a-razor-pages-project"></a>从 Razor 页面项目使用 Razor UI 库

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 在解决方案资源管理器中，右键单击“WebApp1”，然后选择“设为启动项目”。
* 在解决方案资源管理器中，右键单击“WebApp1”，然后选择“生成依赖项” > “项目依赖项”。
* 将 RazorUIClassLib 勾选为 WebApp1 的依赖项。
* 在解决方案资源管理器中，右键单击“WebApp1”，选择“添加” > “引用”。
* 在“引用管理器”对话框中勾选“RazorUIClassLib” > “确定”。

运行应用。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

创建 Razor 页面 Web 应用和包含 Razor 页面应用和 Razor 类库的解决方案文件：

``` CLI
dotnet new razor -o WebApp1
dotnet new sln
dotnet sln add WebApp1
dotnet sln add RazorUIClassLib
dotnet add WebApp1 reference RazorUIClassLib
```

生成并运行 Web 应用：

``` CLI
cd WebApp1
dotnet run
```

------

<a name="test"></a>

### <a name="test-webapp1"></a>测试 WebApp1

验证正在使用的 Razor UI 类库。

* 浏览到 `/MyFeature/Page1`。

## <a name="override-views-partial-views-and-pages"></a>重写视图、分部视图和页面

如果在 Web 应用和 Razor 类库中都能找到视图、分部视图或 Razor 页面，则 Web 应用中的 Razor 标记（.cshtml 文件）优先。 例如，将 WebApp1/Areas/MyFeature/Pages/Page1.cshtml 添加到 WebApp1，则 WebApp1 中的 Page1 会优先于 Razor 类库中的 Page1。

在示例下载中，将 WebApp1/Areas/MyFeature2 重命名为 WebApp1/Areas/MyFeature 来测试优先级。

将 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 分部视图复制到 WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml。 更新标记以指示新的位置。 生成并运行应用，验证使用部分的应用版本。
