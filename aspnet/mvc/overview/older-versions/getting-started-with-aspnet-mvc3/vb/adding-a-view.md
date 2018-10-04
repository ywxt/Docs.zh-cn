---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 添加视图 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 0d6311cac4fe01b2e21b300ff3841b3f2ca6fcf5
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577053"
---
<a name="adding-a-view-vb"></a>添加视图 (VB)
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您愿意 C#，切换到[C# 版本](../cs/adding-a-view.md)本教程。


在本部分中我们要修改`HelloWorldController`类，以使用视图模板文件来顺利封装生成 HTML 响应向客户端的过程。

让我们首先使用视图模板与`Index`中的方法`HelloWorldController`类。 当前`Index`方法将返回一条消息，是控制器类中硬编码的字符串。 更改`Index`方法以返回`View`对象，如在下面的示例所示：

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

让我们现在将视图模板添加到我们的项目，我们可以调用与`Index`方法。 若要执行此操作，右键单击内`Index`方法，并单击**添加视图**。

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

**添加视图**对话框随即出现。 保留默认条目，然后单击**添加**按钮。

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

*MvcMovie\Views\HelloWorld*文件夹并*MvcMovie\Views\HelloWorld\Index.vbhtml*创建文件。 你可以看到它们在**解决方案资源管理器**:

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

添加一些 HTML 下的`<h2>`标记。 已修改*MvcMovie\Views\HelloWorld\Index.vbhtml*文件如下所示。

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

运行应用程序，并浏览到&quot;你好世界&quot;控制器 (`http://localhost:xxxx/HelloWorld`)。 `Index`控制器中的方法未做大量的工作; 它只需运行该语句`return View()`，这表示我们想要使用视图模板文件来呈现到客户端的响应。 因为我们未显式指定要使用的视图模板文件的名称，ASP.NET MVC 的默认设置为使用*Index.vbhtml*视图中的文件*\Views\HelloWorld*文件夹。 下图显示了字符串硬编码的视图中。

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

看起来相当棒。 但请注意，浏览器的标题栏将显示&quot;索引&quot;，并在页上的大标题显示&quot;我的 MVC 应用程序。&quot;让我们将这些更改。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页面

首先，让我们来更改文本&quot;我的 MVC 应用程序。&quot;该文本共享，并显示在每一页。 它实际显示只能在一个位置，在我们的项目，即使它是在我们的应用程序中每一页上。 转到 */视图/共享*中的文件夹**解决方案资源管理器**，然后打开 *\_Layout.vbhtml*文件。 此文件称为布局页，它是共享&quot;shell&quot;所有其他页使用的。

请注意`@RenderBody()`文件底部附近的代码行。 `RenderBody` 是你创建的所有页，都显示的其中一个占位符&quot;包装&quot;在布局页面中。 更改`<h1>`从标题**&quot;** My MVC Application&quot;到&quot;MVC 电影应用&quot;。

[!code-html[Main](adding-a-view/samples/sample3.html)]

运行应用程序，并记下它现在显示&quot;MVC 电影应用&quot;。 单击**有关**链接，然后该页面显示了&quot;MVC 电影应用&quot;、 过。

完整 *\_Layout.vbhtml*文件如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

现在，让我们来更改索引页面 （视图） 的标题。

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

打开*MvcMovie\Views\HelloWorld\Index.vbhtml*。 有两个位置进行更改： 首先，文本显示的标题中的浏览器中，然后在辅助标头 (`<h2>`元素)。 我们将使它们略有不同以便你可以查看哪一段代码将更改应用程序的哪个部分。

运行应用程序，并浏览到`http://localhost:xx/HelloWorld`。 请注意，浏览器标题、主标题和辅助标题已更改。 很容易地对视图进行较小的更改将应用程序中的重大更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

我们一小段&quot;数据&quot;(在这种情况下&quot;Hello World ！&quot;消息) 不过是硬编码。 MVC 应用程序具有 V （视图），我们有 C （控制器），但尚无的 M （模型）。 稍后，我们将演练如何创建数据库并从它检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

我们转到数据库，并讨论模型之前，不过，我们首先讨论一下将信息从控制器传递给视图。 我们想要传递视图模板以呈现给客户端 HTML 响应的需要。 这些对象通常创建并由控制器类传递给视图模板，并且它们应包含视图模板所需数据，并没有更多。

与以前`HelloWorldController`类，`Welcome`操作方法所花`name`和一个`numTimes`参数，然后输出到浏览器使用参数值。 而是与使控制器继续直接将此响应呈现，让我们改为我们将该数据在一个包中视图。 可以使用控制器和视图`ViewBag`对象来存放该数据。 将传递到视图模板自动，并用于呈现 HTML 响应将用作数据的包的内容。 控制器涉及到一件事并与另一个视图模板通过这种方式，使我们能够保持干净&quot;关注点分离&quot;应用程序中。

或者，我们可以定义自定义类、 然后我们自己创建该对象的实例、 用数据填充和将其传递给视图。 通常称为 ViewModel，因为它是自定义模型的视图。 对于少量的数据，但是，ViewBag 运行良好。

返回到*HelloWorldController.vb*文件更改`Welcome`控制器以将消息和 NumTimes 放入 ViewBag 中的方法。 ViewBag 是动态对象。 这意味着您可以随意设置为它。 ViewBag 直到你将内容放在它具有定义的属性。

完整`HelloWorldController.vb`使用同一个文件中的新类。

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

现在我们 ViewBag 包含将通过传递到视图自动的数据。 同样，或者我们可能已通过在我们自己像这样的对象中如果我们喜欢：

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

现在，我们需要`WelcomeView`模板 ！ 运行应用程序，因此编译新代码。 关闭浏览器中，右键单击内`Welcome`方法，并单击**添加视图**。

下面是什么你**添加视图**对话框如下所示。

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

添加以下代码下的`<h2>`元素中的新<em>欢迎。</em>vbhtml 文件。 我们将使一个循环并说&quot;Hello&quot;无数次，用户所说我们应该 ！

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

运行应用程序，并浏览到 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在数据取自 URL 并自动传递到控制器。 在控制器包将数据分成`Model`对象并将该对象传递给视图。 不是以 HTML 的形式向用户显示数据视图。

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

当然，这是一种类型的&quot;M&quot;模型，而不是数据库类。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)
