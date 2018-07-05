---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 添加视图 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: e9496f801024bd2d4a135eefbb79b162017197b7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366211"
---
<a name="adding-a-view-c"></a>添加视图 (C#)
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。
> 
> 
> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。


在本部分中想要修改`HelloWorldController`类，以使用视图模板文件来顺利封装生成 HTML 响应向客户端的过程。

将创建使用新的视图模板文件[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)使用 ASP.NET MVC 3 引入了。 基于 razor 的视图模板具有 *.cshtml*文件扩展名，并提供创建 HTML 输出使用 C# 的简洁方法。 Razor 字符和击键时编写视图模板，所需的数量降至最低，并启用编码工作流即快速、 流畅。

使用视图模板与启动`Index`中的方法`HelloWorldController`类。 当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。 更改`Index`方法以返回`View`对象，如在下面的示例所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

此代码使用视图模板来生成 HTML 响应到浏览器。 在项目中，添加可用于查看模板`Index`方法。 若要执行此操作，右键单击内`Index`方法，并单击**添加视图**。

![](adding-a-view/_static/image1.png)

**添加视图**对话框随即出现。 保留默认值的方式变，并单击**添加**按钮：

![](adding-a-view/_static/image2.png)

*MvcMovie\Views\HelloWorld*文件夹并*MvcMovie\Views\HelloWorld\Index.cshtml*创建文件。 你可以看到它们在**解决方案资源管理器**:

![](adding-a-view/_static/image3.png)

如下所示*Index.cshtml*已创建的文件：

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

添加一些 HTML 下的`<h2>`标记。 已修改*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

运行应用程序，并浏览到`HelloWorld`控制器 (`http://localhost:xxxx/HelloWorld`)。 `Index`控制器中的方法未做大量的工作; 它只需运行该语句`return View()`，其指定该方法应使用视图模板文件来呈现到浏览器的响应。 由于未显式指定要使用的视图模板文件的名称，ASP.NET MVC 的默认设置为使用*Index.cshtml*视图中的文件*\Views\HelloWorld*文件夹。 下图显示了字符串硬编码的视图中。

![](adding-a-view/_static/image6.png)

看起来相当棒。 但是，请注意，浏览器的标题栏将显示"Index"，并在页上的大标题显示"我 MVC 应用程序。" 让我们将这些更改。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页面

首先，你想要更改页面顶部的"My MVC Application"标题。 该文本是通用的每一页。 它实际上被实现只能在一个位置，在项目中，即使它在应用程序中每一页显示。 转到 */视图/共享*中的文件夹**解决方案资源管理器**，然后打开 *\_Layout.cshtml*文件。 此文件称为*布局页*是共享的"shell"，所有其他页面使用。

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

布局模板可用于在一个位置指定您的网站的 HTML 容器布局，然后将其应用于你的站点中多个页面。 请注意`@RenderBody()`文件底部附近的行。 `RenderBody` 是，您创建的所有特定于视图的页面显示，"包装"在布局页面中的占位符。 更改布局模板从"My MVC Application"到"MVC 电影应用"中的标题标头。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

运行应用程序，请注意它现在显示"MVC 电影应用"。 单击**有关**链接，并且您看到如何该页面显示"MVC 电影应用"，过。 我们能够在布局模板中一次进行更改，并具有在站点上的所有页面都反映新标题。

![](adding-a-view/_static/image9.png)

完整 *\_Layout.cshtml*文件如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

现在，让我们来更改索引页面 （视图） 的标题。

打开*MvcMovie\Views\HelloWorld\Index.cshtml*。 有两个位置进行更改： 首先，文本显示的标题中的浏览器中，然后在辅助标头 (`<h2>`元素)。 稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

若要指示显示集上面的代码的 HTML 标题`Title`的属性`ViewBag`对象 (后者位于*Index.cshtml*视图模板)。 如果回顾一下布局模板的源代码，您会注意到，该模板使用此值在`<title>`元素作为的一部分`<head>`HTML 的一部分。 使用此方法，可以在视图模板和布局文件之间轻松传递其他参数。

运行应用程序，并浏览到`http://localhost:xx/HelloWorld`。 请注意，浏览器标题、主标题和辅助标题已更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）

此外会注意到了中的内容*Index.cshtml*视图的模板已与合并 *\_Layout.cshtml*视图模板和单个 HTML 响应已发送到浏览器。 凭借布局模板可以很容易地对应用程序中所有页面进行更改。

![](adding-a-view/_static/image10.png)

但我们这一点点“数据”（在此示例中为“Hello from our View Template!” 消息）是硬编码的。 MVC 应用程序有一个“V”（视图），而你已有一个“C”（控制器），但还没有“M”（模型）。 稍后，我们将演练如何创建数据库并从它检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

我们转到数据库，并讨论模型之前，不过，我们首先讨论一下将信息从控制器传递给视图。 控制器类调用以响应传入的 URL 请求。 控制器类是响应的编写代码，用于处理传入的参数，从数据库检索数据并最终决定将哪些类型发送回浏览器的位置。 查看模板然后可从控制器来生成并格式化对浏览器的 HTML 响应。

控制器负责提供使视图模板能够呈现到浏览器的响应所需的任何数据或对象。 视图模板应永远不会执行业务逻辑，或直接与数据库交互。 相反，它应使用仅由控制器提供给它的数据。 维护此"关注点分离"有助于保持代码干净且更易于维护。

目前，`Welcome`操作方法中的`HelloWorldController`类采用`name`和一个`numTimes`参数，然后输出直接向浏览器的值。 而不是使控制器将作为一个字符串，此响应呈现，让我们更改控制器以改为使用视图模板。 视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。 可以为此，需要查看模板的动态数据放置在控制器`ViewBag`视图模板稍后可以访问的对象。

返回到*HelloWorldController.cs*文件，并更改`Welcome`方法以添加`Message`并`NumTimes`值设为`ViewBag`对象。 `ViewBag` 是一个动态对象，这意味着您可以随意设置其中;`ViewBag`对象具有定义的属性，直到你将内容放在它。 完整的 HelloWorldController.cs 文件如下所示：

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

现在`ViewBag`对象包含将自动传递给视图的数据。

接下来，需要一个欢迎使用视图模板 ！ 在中**调试**菜单中，选择**生成 MvcMovie**以确保编译项目。

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

然后在右键单击`Welcome`方法，并单击**添加视图**。 下面是什么**添加视图**对话框如下所示：

![](adding-a-view/_static/image13.png)

单击**外**，然后添加以下代码`<h2>`中的新元素*Welcome.cshtml*文件。 你将创建无数次，用户所说它应显示"Hello"的循环。 完整*Welcome.cshtml*文件如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

运行应用程序并浏览到以下 URL:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在数据取自 URL 并自动传递到控制器。 控制器将数据打包到`ViewBag`对象并将该对象传递给视图。 该视图然后会以 html 格式的数据向用户显示。

![](adding-a-view/_static/image14.png)

当然，这是模型的一种“M”类型，而不是数据库类。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)
