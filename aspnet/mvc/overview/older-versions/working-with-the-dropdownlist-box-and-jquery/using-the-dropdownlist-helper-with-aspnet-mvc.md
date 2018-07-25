---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: 使用 ASP.NET MVC 使用 DropDownList 帮助程序 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6dbffe715990de5c0b3b834e354379e414925816
ms.sourcegitcommit: 8f8924ce4eb9effeaf489f177fb01b66867da16f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2018
ms.locfileid: "39219051"
---
<a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>使用 ASP.NET MVC 使用 DropDownList 帮助程序
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

本教程将教您使用的基础知识[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)帮助器和[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx)中的 ASP.NET MVC Web 应用程序的帮助程序。 可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio，若要遵循本教程的免费版本。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：

- [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack) <a id="post"></a>
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）

如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。 本教程假定你已完成[ASP.NET MVC 简介](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教程或[ASP.NET MVC Music 商店](../mvc-music-store/mvc-music-store-part-1.md)教程或您熟悉 ASP.NET MVC 开发。 本教程开头从修改后的项目[ASP.NET MVC Music 商店](../mvc-music-store/mvc-music-store-part-1.md)教程。 您可以下载初学者项目使用以下链接[下载 C# 版本](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)。

具有已完成本教程的 C# 源代码的 Visual Web Developer 项目是可随附于本主题。 [下载](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)。

### <a name="what-youll-build"></a>你将生成

您将创建的操作方法和视图，供[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx)帮助程序选择类别。 你还将使用**jQuery**添加一个新类别 （如流派或艺术家） 需要时可以使用插入类别对话框。 下面是显示的链接可添加的新流派，并添加新的艺术家的创建视图的屏幕截图。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>你将学习的技能

下面是你将了解：

- 如何使用[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx)帮助器来选择类别数据。
- How to add **jQuery**对话框以添加新类别。

### <a name="getting-started"></a>入门

首先，下载与下面的链接，初学者项目[下载](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)。 在 Windows 资源管理器中，右键单击*DDL\_Starter.zip*文件，并选择属性。 在中**DDL\_Starter.zip 属性**对话框中，选择解除阻止。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

右键单击 DDL\_Starter.zip 文件，然后选择**提取所有**来解压缩该文件。 打开*StartMusicStore.sln* Visual Web Developer 2010 速成版 （"Visual Web 开发人员"或简称"VWD"） 或 Visual Studio 2010 的文件。

按 CTRL + f5 键以运行该应用程序，然后单击**测试**链接。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

选择**选择电影类别 （简单）** 链接。 显示影片类型选择列表，与喜剧所选的值。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

右键单击浏览器并选择查看源中。 显示该页面的 HTML。 下面的代码显示的 HTML select 元素。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

您可以看到每个项的选择列表中具有值 （0 表示操作、 剧本的 1、 2 表示喜剧和科幻小说的 3），并且显示名称 （操作、 戏曲、 喜剧和科幻小说）。 上面的代码是标准 HTML 选择列表。

将选择列表更改为 Drama 和命中**提交**按钮。 在浏览器中的 URL 是`http://localhost:2468/Home/CategoryChosen?MovieType=1`和页将显示**你选择： 1**。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

打开*Controllers\HomeController.cs*文件并检查`SelectCategory`方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)帮助器用于创建 HTML 选择列表需要**IEnumerable&lt;SelectListItem &gt;** ，显式或隐式。 也就是说，您可以将传递**IEnumerable&lt;SelectListItem &gt;** 显式设[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)帮助程序也可以添加**IEnumerable&lt;SelectListItem &gt;** 到[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)使用相同的名称**SelectListItem**为模型属性。 传入**SelectListItem**本教程的下一部分中介绍了隐式和显式。 上面的代码显示了最简单的可能方法创建**IEnumerable&lt;SelectListItem &gt;** 并使用文本和值填充它。 请注意`Comedy` [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)具有[选定](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx)属性设置为**true;** 这将导致呈现选择列表，以显示**喜剧**为列表中选定的项。

**IEnumerable&lt;SelectListItem &gt;** 创建更高版本将添加到[ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) MovieType 同名。 这是我们会将传递给**IEnumerable&lt;SelectListItem &gt;** 隐式为[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx)如下所示的帮助器。

打开*Views\Home\SelectCategory.cshtml*文件，并检查的标记。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

在第三个行中，我们将设置布局为 Views/Shared/\_简单\_Layout.cshtml，这是标准布局文件的简化的版本。 我们这样做可以使显示器保持打开，并呈现简单的 HTML。

在此示例中我们不更改状态的应用程序，因此我们将数据通过提交**HTTP GET**，而非**HTTP POST**。 请参阅 W3C 部分[用于选择 HTTP GET 或 POST 的快速清单](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)。 由于我们不会更改应用程序并发布窗体，因此我们使用[Html.BeginForm](https://msdn.microsoft.com/library/dd460344.aspx)重载，可用于指定操作方法、 控制器和窗体方法 (**HTTP POST**或**HTTP GET**)。 视图中所包含通常[Html.BeginForm](https://msdn.microsoft.com/library/dd505244.aspx)不带参数的重载。 无参数版本默认为发布到相同的操作方法和控制器的 POST 版本窗体数据。

下面的行

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

将传递到一个字符串参数**DropDownList**帮助器。 此字符串中，在本例中为"MovieType"执行两项操作：

- 它提供的键**DropDownList**帮助器以查找**IEnumerable&lt;SelectListItem &gt;** 中**ViewBag**。
- 它是数据绑定到 MovieType 窗体元素。 如果提交方法**HTTP GET**，`MovieType`将是一个查询字符串。 如果提交方法**HTTP POST**，`MovieType`将添加消息正文中。 下图显示了查询字符串，值为 1。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

下面的代码演示`CategoryChosen`窗体提交到的方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

导航回到测试页并选择**HTML SelectList**链接。 HTML 页呈现类似于简单的 ASP.NET MVC 测试页选择元素。 右键单击浏览器窗口，然后选择**查看源**。 选择列表的 HTML 标记是实质上是相同的。 测试 HTML 页上，其工作原理类似的 ASP.NET MVC 操作方法和视图之前进行测试。

### <a name="improving-the-movie-select-list-with-enums"></a>改进与枚举的电影选择列表

如果你的应用程序中的类别固定的并且将不会更改，您可以充分利用枚举以使代码更可靠且易于扩展。 当添加新类别时，生成正确的类别值。 避免了复制和粘贴错误，当您添加新类别，但忘记更新的类别值。

打开*Controllers\HomeController.cs*文件并检查以下代码：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[Enum](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories`捕获的四个电影类型。 `SetViewBagMovieType`方法创建**IEnumerable&lt;SelectListItem &gt;** 从`eMovieCategories`**枚举**，并设置`Selected`从属性`selectedMovie`参数。 `SelectCategoryEnum`操作方法使用同一个视图作为`SelectCategory`操作方法。

导航到测试页并单击`Select Movie Category (Enum)`链接。 这次，而不是所显示的值 （数字），将显示一个字符串，表示枚举。

### <a name="posting-enum-values"></a>发布的枚举值

HTML 窗体通常用于将数据发送到服务器。 下面的代码演示`HTTP GET`并`HTTP POST`版本的`SelectCategoryEnumPost`方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

通过传递`eMovieCategories`到枚举`POST`方法中，我们可以提取类型的枚举值和枚举字符串。 运行示例并导航到测试页。 单击`Select Movie Category(Enum Post)`链接。 选择电影类型，然后点击提交按钮。 屏幕将显示的值和电影类型的名称。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>创建多个部分中选择元素

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx)的 HTML 帮助器的 HTML 呈现`<select>`具有元素`multiple`属性，它允许用户选择多项。 导航到测试链接，然后选择**多选择国家/地区**链接。 呈现的 UI，可选择多个国家/地区。 在下图中，选择加拿大和中国。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>检查 MultiSelectCountry 代码

检查中的以下代码*Controllers\HomeController.cs*文件。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries`方法创建一系列国家/地区，然后将其传递给`MultiSelectList`构造函数。 `MultiSelectList`中使用的构造函数重载`GetCountries`上面方法采用四个参数：

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *项*: [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx)包含列表中的项。 在上面列表的国家/地区的示例。
2. *dataValueField*： 在属性的名称**IEnumerable**包含的值的列表。 在上述示例中，`ID`属性。
3. *dataTextField*： 在属性的名称**IEnumerable**列表，其中包含要显示的信息。 在上述示例中，`name`属性。
4. *selectedValues*： 所选值的列表。

在上述示例中，`MultiSelectCountry`方法传递`null`针对所选国家/地区，以便显示的用户界面时，不选中任何国家/地区的值。 下面的代码显示了 Razor 标记用于呈现`MultiSelectCountry`视图。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

HTML 帮助器[ListBox](https://msdn.microsoft.com/library/dd470200.aspx)采用上面两个参数，模型绑定的属性的名称使用的方法和[MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx)包含选择的选项和值。 `ViewBag.YouSelected`上面的代码用于显示您在提交表单时选择的国家/地区的值。 检查的 HTTP POST 重载`MultiSelectCountry`方法。

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected`动态属性包含所选国家/地区，为获取`Countries`窗体集合中的条目。 在此版本 GetCountries 方法传递一系列所选国家/地区，因此，在`MultiSelectCountry`显示视图中，在 UI 中选择所选国家/地区。

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>进行选择元素友好 Harvest 所选择的 jquery 插件

Harvest[所选](http://harvesthq.github.com/chosen/)jQuery 插件可以添加到对应的 HTML&lt;选择&gt;元素创建的用户友好 UI。 下图演示 Harvest[所选](http://harvesthq.github.com/chosen/)与 jQuery 插件`MultiSelectCountry`视图。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

在下面的两个映像**加拿大**处于选中状态。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

在上图中，选择加拿大，并且它包含**x**可以单击要删除所选内容。 下图显示了加拿大，中国区，并且日本选择。

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>挂接 Harvest 所选择的 jQuery 插件

以下部分是更轻松地遵循如果您没有使用 jQuery 一些经验。 如果你从未使用过 jQuery 之前，你可能想要尝试以下 jQuery 教程之一。

- [JQuery 的工作原理](http://docs.jquery.com/Tutorials:How_jQuery_Works)通过[John Resig](http://ejohn.org/)
- [开始使用 jQuery](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery)通过[Jörn Zaefferer](http://bassistance.de/)
- [Live jQuery 的示例](http://codylindley.com/blogstuff/js/jquery/#)通过[Cody Lindley](http://codylindley.com/)

Starter 和已完成的示例项目附带本教程中包含所选择的插件。 对于本教程只需要使用 jQuery 来将它挂接到 UI。 若要在 ASP.NET MVC 项目中使用所选择的 Harvest jQuery 插件，您必须：

1. 下载所选插件[github](https://github.com/harvesthq/chosen/)。 已为你完成此步骤。
2. 将所选文件夹添加到 ASP.NET MVC 项目。 添加从所选插件在所选文件夹为上一步中下载的资产。 已为你完成此步骤。
3. 挂接到所选的插件**DropDownList**或**ListBox**的 HTML 帮助器。

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>挂接到 MultiSelectCountry 视图所选择的插件。

打开*Views\Home\MultiSelectCountry.cshtml*文件，并添加`htmlAttributes`参数`Html.ListBox`。 您将添加此参数包含选择列表的类名称 (`@class = "chzn-select"`)。 已完成的代码如下所示：

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

在上面的代码中，我们要添加的 HTML 特性和特性值`class = "chzn-select"`。 \@字符前面的类具有与 Razor 视图引擎没有任何关系。 `class` 是[C# 关键字](https://msdn.microsoft.com/library/x53a06bb.aspx)。 C# 关键字不能用作标识符，除非它们包含\@作为前缀。 在上述示例中，`@class`是有效的标识符，但**类**不是因为**类**是一个关键字。

将引用添加到*Chosen/chosen.jquery.js*并*Chosen/chosen.css*文件。 *Chosen/chosen.jquery.js*并实现所选择的插件的功能上。 *Chosen/chosen.css*文件提供了样式。 这些将引用添加到底部*Views\Home\MultiSelectCountry.cshtml*文件。 下面的代码演示如何引用所选择的插件。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

激活使用类名称中使用所选择的插件**Html.ListBox**代码。 在上面的示例中，类名是`chzn-select`。 将以下行添加到底部*Views\Home\MultiSelectCountry.cshtml*视图文件。 此代码行激活所选择的插件。

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

下面的行是调用了 jQuery ready 函数，后者将选择具有类名称的 DOM 元素的语法`chzn-select`。

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

所选的方法的应用设置，则返回从上述调用包装 (`.chosen();`)，它与所选择的插件。

下面的代码演示了已完成*Views\Home\MultiSelectCountry.cshtml*视图文件。

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

运行应用程序并导航到`MultiSelectCountry`视图。 尝试添加和删除国家/地区。 提供的示例下载还包含`MultiCountryVM`方法，并实现 MultiSelectCountry 功能使用视图的视图模型而不是**ViewBag**。

下一节中您将看到与 ASP.NET MVC 基架机制工作原理**DropDownList**帮助器。

> [!div class="step-by-step"]
> [下一篇](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
