---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: Introducing ASP.NET Web 页面-创建一致布局 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何使用布局来使用 ASP.NET Web Pages 站点上创建一致的外观的页面。 它假定你已完成...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: a6a007678d58547e9987ebda46bd08ae8aea66f7
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021168"
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET 网页简介-创建一致布局
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程演示如何使用*布局*使用 ASP.NET Web Pages 站点上创建一致的外观的页面。 它假定你已完成通过时序[删除数据库数据在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584)。
> 
> 你将学习：
> 
> - 布局页。
> - 如何结合使用动态内容的布局页。
> - 如何将值传递给布局页。


## <a name="about-layouts"></a>关于布局

到目前为止您已创建的页面都有过完成后，独立页面。 它们都属于相同的站点，但它们不具有任何通用元素或标准外观。

大多数站点所拥有的一致的外观和布局。 例如，如果你转到[Microsoft.com/web](https://www.microsoft.com/web/)站点并看看，您看到页面都符合整体布局和视觉主题：

![Microsoft.com/web 站点页面布局的标头、 导航区域中，内容区域和页脚](layouts/_static/image1.png)

*低效*创建此布局的方法可能是定义标头、 导航栏中和页脚分别在每个页面上。 您将会复制相同的标记每个时间。 如果你想要更改某些内容 （例如，更新页脚），必须单独更改每个页面。

这正是*布局页*进入。 ASP.NET Web Pages 中，您可以定义提供站点页面的整体容器布局页面。 例如，布局页可以包含页眉、 导航区域中和页脚。 布局页包括主要内容的位置的占位符。

然后，您可以定义包含标记和仅该页面的代码的各个内容页。 内容页面不必是完整的 HTML 页面; 例如：他们甚至不需要具有`<body>`元素。 它们还具有一行告诉你想要显示中的内容布局页面的 ASP.NET 代码。 下面是大致显示此关系的工作方式的图片：

![显示两个内容页面和布局页容纳其中的概念图](layouts/_static/image2.png)

这种交互很容易地了解观察它的运行时。 在本教程中，你将更改您的电影页面要使用的布局。

## <a name="adding-a-layout-page"></a>添加布局页

您将首先创建定义与标头、 页脚和用于显示主要内容区域的典型页面布局的布局页。 在 WebPagesMovies 站点中，添加名为 CSHTML 页面 *\_Layout.cshtml*。

前导下划线 ( `_` ) 字符非常重要。 如果页面的名称以下划线开头，ASP.NET 不会直接向浏览器发送该页面。 此约定可定义所需的站点，但该用户不能直接请求的页面。

中页面的内容替换为以下：

[!code-html[Main](layouts/samples/sample1.html)]

正如您所看到的此标记是只需使用的 HTML`<div>`元素可多页以及一个定义三个部分`<div>`元素，用以存放的三个部分。 页脚包含少量的 Razor 代码： `@DateTime.Now.Year`，这将在该位置的页中呈现当前年份。

请注意，没有名为的样式表的链接*Movies.css*。 样式表是可在其中定义元素的物理布局的详细信息。 你将在稍后创建的。

在此唯一不寻常的功能 *\_Layout.cshtml*页是`@Render.Body()`行。 这就是此布局合并与另一页面时内容何处的占位符。

## <a name="adding-a-css-file"></a>添加.css 文件

页上定义的元素的实际排列方式 （即，外观） 的首选的方法是使用级联样式表 (CSS) 规则。 因此将创建 *.css*具有新布局的规则文件。

在 WebMatrix 中，选择你的站点的根目录。 然后在**文件**选项卡的功能区中，单击下的箭头**新建**按钮，然后单击**新文件夹**。

![在功能区下新建的新建文件夹选项。](layouts/_static/image3.png)

将新文件夹命名*样式*。

![命名的新文件夹样式](layouts/_static/image4.png)

在新*样式*文件夹中，创建名为的文件*Movies.css*。

![创建新的 Movies.css 文件](layouts/_static/image5.png)

新的内容替换为 *.css*具有以下文件：

[!code-css[Main](layouts/samples/sample2.css)]

我们不会说很多有关这些 CSS 规则，只是想说明两件事情。 一个是，除了设置字体和大小，这些规则使用绝对定位来指定标头、 页脚和主要内容区域的位置。 如果您是初次接触定位在 CSS 中，你可以读取[CSS 定位](http://www.w3schools.com/css/css_positioning.asp)W3Schools 站点教程。

请注意，在底部，我们已复制最初的样式规则中单独定义的另外一点*Movies.cshtml*文件。 这些规则中使用[简介显示数据通过使用 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580)教程，以使`WebGrid`帮助器呈现添加到表中的条带化的标记。 (如果您将使用 *.css*文件有关样式定义，您也可能给整个站点的样式规则中。)

## <a name="updating-the-movies-file-to-use-the-layout"></a>更新要使用布局的电影文件

现在可以更新站点以使用新的布局中的现有文件。 打开*Movies.cshtml*文件。 在顶部，为第一行代码，添加以下代码：

[!code-csharp[Main](layouts/samples/sample3.cs)]

该页面现在开始方式如下：

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

这行代码告诉 ASP.NET，当*电影*页上运行，它应与合并 *\_Layout.cshtml*文件。

由于*Movies.cshtml*文件现在所使用的布局页，可以删除从标记*Movies.cshtml*已处理的页 *\_Layout.cshtml*文件。 拿出`<!DOCTYPE>`， `<html>`，和`<body>`开始和结束标记。 拿出整个`<head>`元素和其内容，包括网格中的样式规则，因为您现在已经获得这些规则 *.css*文件。 既然您在它，请更改现有`<h1>`元素`<h2>`元素; 必须`<h1>`已在布局页面中的元素。 更改`<h2>`"列表 Movies"的文本。

通常情况下不会有内容页中进行这些各种更改。 时使用布局页，可以启动你的站点，请首先创建不包含所有这些元素的内容页面。 在这种情况下，不过，您会转换为独立页面另一个使用一种布局，因此没有进行一些清理。

当您结束， *Movies.cshtml*页面将如下所示：

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>测试布局

现在可以看到布局如下所示。 在 WebMatrix 中，右键单击*Movies.cshtml*页，然后选择**浏览器中启动**。 当浏览器显示页面时，它会查找此页面所示：

![使用一种布局呈现电影页面](layouts/_static/image6.png)

ASP.NET 已合并到 Movies.cshtml 页的内容 *\_Layout.cshtml*页面，在右此处`RenderBody`方法。 当然 *\_Layout.cshtml*页上的引用 *.css*文件，用于定义页面的外观。

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>正在更新 AddMovie 页后，可以使用布局

布局的真正优点是可以使用它们的所有页在你的站点中。 打开*AddMovie.cshtml*页。

你可能会记住*AddMovie.cshtml*页最初在其中以定义查找范围的验证错误消息中发生某些 CSS 规则。 因为必须 *.css*文件中为你的网站现在，可以移动到这些规则 *.css*文件。 从其中移除这些*AddMovie.cshtml*文件，并将其添加到底部*Movies.css*文件。 要移动的以下规则：

[!code-css[Main](layouts/samples/sample6.css)]

现在，进行中的更改的相同排序*AddMovie.cshtml*与针对*Movies.cshtml* — 添加`Layout="~/_Layout.cshtml;`和删除现在是无关的 HTML 标记。 更改`<h1>`元素`<h2>`。 完成后，页上将看起来如下例所示：

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

运行页。 现在看起来类似于此图：

![使用一种布局呈现电影中添加页](layouts/_static/image7.png)

你想要在站点中的页面进行类似的更改 — *EditMovie.cshtml*并*DeleteMovie.cshtml*。 但是，在执行之前，可使另一项更改使更灵活的布局。

## <a name="passing-title-information-to-the-layout-page"></a>传递到布局页的标题信息

*\_Layout.cshtml*创建的页具有`<title>`设置为"My 电影 Site"的元素。 大多数浏览器将此元素的内容显示为一个选项卡上的文本：

![页面的&lt;标题&gt;浏览器选项卡中显示的元素](layouts/_static/image8.png)

此标题信息是泛型方法。 假设你想要将更多特定于当前页的标题文本。 （标题文本还用于通过搜索引擎确定您的页面的内容。）可以将信息从所示的内容页面传递*Movies.cshtml*或*AddMovie.cshtml*到布局页，然后使用该信息以自定义布局页面呈现。

打开*Movies.cshtml*页。 在顶部代码中，添加以下行：

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page`对象是可用于所有 *.cshtml*页，一个用于此目的，即页面和其布局之间共享信息。

打开<em>\_Layout.cshtml</em>页。 更改`<title>`元素，使其看起来像此标记：

[!code-html[Main](layouts/samples/sample9.html)]

此代码将呈现任何处于`Page.Title`坐在该位置的页中的属性。

运行*Movies.cshtml*页。 这一次浏览器选项卡显示您作为值传递`Page.Title`:

![显示标题动态创建一个浏览器选项卡](layouts/_static/image9.png)

如果您想在浏览器中查看页面源文件。 你可以看到`<title>`元素呈现为`<title>List Movies</title>`。

> [!TIP] 
> 
> **Page 对象**
> 
> 一个有用的功能`Page`是它是一个动态对象 —`Title`属性不是固定或保留的名称。 可以使用*任何*名称的值为`Page`对象。 例如，可以轻松传递标题使用名为的属性`Page.CurrentName`或`Page.MyPage`。 唯一的限制是，该名称必须遵循常规的规则来可命名为哪些属性。 （例如，名称不能包含空格。）
> 
> 可以将任意数量的值传递使用`Page`对象。 如果你想要将电影信息传递给布局页，可以通过使用类似于传递值`Page.MovieTitle`并`Page.Genre`和`Page.MovieYear`。 （或者是您发明来存储的信息的任何其他名称。）唯一的要求，这是可能明显 — 是，您必须使用内容页和布局页中的相同名称。
> 
> 使用传递的信息`Page`对象并不局限于只是要布局页上显示的文本。 可以将值传递给布局页中，并在布局页面中的代码然后使用的值来确定是否要显示的页上，部分什么 *.css*文件以使用，等等。 在传递的值`Page`对象是像任何其他值的代码中使用。 它只是源自在内容页中的值，并传递到布局页。


打开*AddMovie.cshtml*页上，并将行添加到代码提供的标题的顶部*AddMovie.cshtml*页：

[!code-csharp[Main](layouts/samples/sample10.cs)]

运行*AddMovie.cshtml*页。 请参阅新标题：

![显示添加电影标题动态创建一个浏览器选项卡](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>更新剩余页面以使用布局

现在可以在你的站点中完成剩余的页，以便它们使用新的布局。 打开*EditMovie.cshtml*并*DeleteMovie.cshtml*又和每个中进行相同的更改。

添加链接到的布局页面的代码行：

[!code-csharp[Main](layouts/samples/sample11.cs)]

添加行以设置页的标题：

[!code-csharp[Main](layouts/samples/sample12.cs)]

或：

[!code-csharp[Main](layouts/samples/sample13.cs)]

删除所有多余的 HTML 标记，基本上，将保留内的位`<body>`元素 （加上在顶部的代码块）。

更改`<h1>`元素为`<h2>`元素。

完成这些更改，测试每个，并确保它正确显示并且标题正确无误。

## <a name="parting-thoughts-about-layout-pages"></a>最后，建议有关布局页

在本教程中创建 *\_Layout.cshtml*页上，使用`RenderBody`方法来合并另一页的内容。 这是在网页中使用的布局的基本模式。

布局页中有我们此处未涉及的其他功能。 例如，可以嵌套布局页中，一个布局页面又可以引用另一个。 嵌套的布局很有用，如果你正在使用的站点需要不同的布局的小节。 此外可以使用其他方法 (例如， `RenderSection`) 若要设置名为布局页中的部分。

布局页的组合并 *.css*文件是功能强大。 正如您将看到在下一步的系列教程中，在 WebMatrix 中您可以创建基于一个站点*模板*，后者提供了的站点中的预生成的功能。 模板很好地利用布局页和 CSS 以创建的网站的外观精美且具有菜单等功能。 下面是主页的从基于模板，显示使用布局页和 CSS 的功能的站点的屏幕截图：

![通过显示标头、 导航区域中，内容区域、 可选部分和登录链接的 WebMatrix 网站模板创建的布局](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>电影页 （已更新为使用布局页） 的完整列表

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>完成页的列表添加影片页 （针对布局更新）

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>删除电影页 （针对布局更新） 的完整页面列表

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>编辑电影页 （针对布局更新） 的完整页面列表

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>即将推出下一步

在下一步的教程中，您将了解如何将您的网站发布到 Internet，以便每个人都可以查看它。

## <a name="additional-resources"></a>其他资源

- [创建一致的查看](https://go.microsoft.com/fwlink/?LinkID=202891)— 提供了更多详细使用信息的布局的项目。 它还介绍了如何将值传递给布局页的显示或隐藏的部分内容。
- [嵌套使用 Razor 布局页](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)— Mike Brind 博客举例说明如何嵌套布局页。 （包括页面的下载。）

> [!div class="step-by-step"]
> [上一页](deleting-data.md)
> [下一页](publishing.md)
