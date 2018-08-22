---
title: 使用 ASP.NET Core 和 Bootstrap 构建响应灵敏、布局美观的网站
author: ardalis
description: 了解如何开发使用 ASP.NET Core 的响应式 web 应用程序使用 Bootstrap。
ms.author: riande
ms.date: 10/14/2016
uid: client-side/bootstrap
ms.openlocfilehash: 1ccf33b299739f5aa963a53feb70b44b290443ca
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830225"
---
# <a name="build-beautiful-responsive-sites-with-bootstrap-and-aspnet-core"></a>使用 ASP.NET Core 和 Bootstrap 构建响应灵敏、布局美观的网站

<a name="bootstrap-index"></a>

作者：[Steve Smith](https://ardalis.com/)

Bootstrap 是目前用于开发响应式 web 应用程序最常用的 web 框架。 它在改进网站用户体验方面具有多种优势并提供多种相关功能，无论是前沿设计和开发领域中的新手还是专家，都能够利用这些优势和功能。 Bootstrap 部署为一组 CSS 和 JavaScript 文件，旨在帮助网站和应用程序跨电话、平板电脑、台式计算机等多种设备高效灵活地缩放规模。

## <a name="get-started"></a>入门

可采用多种方式来了解和学习如何使用 Bootstrap。 如果是从 Visual Studio 中的新 web 应用程序开始，可选择用于 ASP.NET Core 的默认启动器模板，这样便可通过预安装的方式获取 Bootstrap：

![初学者模板解决方案视图中启动](bootstrap/_static/bootstrap-in-starter-template.png)

添加 ASP.NET Core Bootstrap 项目是只需将其添加到*bower.json*作为依赖项：

[!code-json[](../common/samples/WebApplication1/bower.json?highlight=5)]

这是 Bootstrap 添加到 ASP.NET Core 项目的建议的方法。

此外可以安装使用多个包管理器，例如 Bower、 npm、 或 NuGet 之一的 bootstrap。 每种情况下，该过程是实质上是相同的：

### <a name="bower"></a>Bower

```console
bower install bootstrap
```

### <a name="npm"></a>npm

```console
npm install bootstrap
```

### <a name="nuget"></a>NuGet

```console
Install-Package bootstrap
```

> [!NOTE]
> 安装客户端依赖关系，如 ASP.NET Core 中的 Bootstrap 为通过 Bower 的建议的方法 (使用*bower.json*，如上所示)。 使用 npm/NuGet 显示来演示如何轻松地 Bootstrap 添加到其他类型的 web 应用程序，包括 ASP.NET 的早期版本。

如果引用自己的 Bootstrap 的本地版本，你将需要使用它的任何页面中引用它们。 在生产环境中应该引用 bootstrap 使用 CDN。 在默认 ASP.NET Core 站点模板，请 *_Layout.cshtml*文件因此像这样：

[!code-html[](../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=9,13,51,59)]

> [!NOTE]
> 如果你打算使用的任何 Bootstrap 的 jQuery 插件，还需要引用 jQuery。

## <a name="basic-templates-and-features"></a>基本模板和功能

最基本的引导模板看起来很像 *_Layout.cshtml*文件所示更高版本，并只包括用于导航，可以在这里要呈现的页的其余部分的基本菜单。

### <a name="basic-navigation"></a>基本导航

默认模板使用的一组`<div>`元素来呈现顶部导航栏和页面的主要部分。 如果使用的 HTML5，您可以替换第一个`<div>`标记`<nav>`标记以获取相同的效果，但具有更精确的语义。 此第一部分中`<div>`可以看到有其他几种。 首先，`<div>`类的"容器"，然后在该，另外两个`<div>`元素:"导航条标头"和"折叠导航栏"。 导航条标头 div 包括时某些最小宽度，显示 3 个水平行下面的屏幕，将显示一个按钮 (所谓"汉堡图标")。 使用纯 HTML 和 CSS; 呈现图标没有图像是必需的。 这是显示的图标，与每个代码<span>呈现一个白色条的标记：

```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

它还包括应用程序名称，通过在左上角中出现。 主导航菜单呈现的`<ul>`中的第二个 div 元素，包括为主页，大约，和联系人的链接。 下方导航窗格中，每个页面的主要部分呈现在另一个`<div>`、 标记与"容器"和"正文内容"类。 在默认的简单\_页的内容呈现的页上，然后一个简单相关联的特定视图，如下所示的布局文件`<footer>`添加到末尾`<div>`元素。 您可以看到内置有关页面将显示使用此模板：

![有关页](bootstrap/_static/about-page-wide.png)

折叠导航栏中的，使用"汉堡"按钮，在右上角，将显示在窗口低于一定宽度时：

![有关带汉堡菜单的页面](bootstrap/_static/about-page-hamburger.png)

单击该图标将显示向下滑从页面顶部垂直抽屉中的菜单项：

![有关页面与展开的 hamburger 菜单](bootstrap/_static/about-page-hamburger-open.png)

### <a name="typography-and-links"></a>版式和链接

Bootstrap 设置站点的基本版式、 颜色和格式设置在其 CSS 文件中的链接。 此 CSS 文件包含默认样式表、 按钮、 窗体元素、 图像和的详细信息 ([了解详细信息](http://getbootstrap.com/css/))。 一个特别有用的功能是网格布局系统，接下来介绍。

### <a name="grids"></a>网格

Bootstrap 的最热门的功能之一是其网格布局系统。 新式 web 应用程序应避免使用`<table>`布局，而将使用此元素限制为实际的表格数据的标记。 相反，列和行可以进行布局使用一系列`<div>`元素和相应的 CSS 类。 有几个优点包括能够调整的网格显示垂直屏幕较窄，例如在手机布局，这种方法。

[Bootstrap 的网格布局系统](http://getbootstrap.com/css/#grid)基于十二个列。 选择此数字是因为可以为 1、 2、 3 或 4 列均匀划分和列宽异中 1 到 12 的垂直屏幕的宽度 /。 若要开始使用网格布局系统，你应该开始使用容器`<div>`，然后添加一行`<div>`，如下所示：

```html
<div class="container">
    <div class="row">
        ...
    </div>
</div>
```

接下来，添加其他`<div>`为每个列的元素和指定的列数的`<div>`应占用 （共 12) 作为"col-md-"开头的 CSS 类的一部分。 例如，如果你想要仅需提供两个大小相等的列，您将为每个使用"列-md-6"的类。 在这种情况下"md"的缩写"medium"，指的是标准大小的台式计算机的显示大小。 有四个不同的选项可以选择从，并且每个将会使用的更高版本的宽度，除非重写 （因此如果你想要而不考虑屏幕宽度固定的布局，则可以只指定 xs 类）。

CSS 类前缀 | 设备层 | 宽度
:---: | :---: | :---:
col-xs- | 手机 | < 768px
col-sm- | 平板电脑 | >= 768px
col-md- | 台式计算机 | >= 992px
col-lg- | 更大的桌面显示 | > = 1200px

指定两个列将同时使用"列-md-6"生成的布局中将两个列在桌面的解决方法，但较小的设备 （或更窄浏览器窗口在桌面上），使用户能够轻松地查看上呈现报表时，这两个列将垂直堆叠时而无需以进行水平滚动的内容。

Bootstrap 始终默认为单列布局，因此您只需要指定的列，如果希望多个列。 你想要显式指定的唯一时间`<div>`占用所有的 12 列会重写的行为更大的设备层。 在指定多个设备层类时，您可能需要重置列呈现在特定时间点。 将仅在某一特定视区中可见的 clearfix div 添加可以实现此目的，如下所示：

![窄和宽视区网格](bootstrap/_static/narrow-and-wide-viewport-grid.png)

在上述示例中，一个和第二个共享"md"布局中的某一行而 2 和 3 共享"xs"布局中的行。 而无需 clearfix `<div>`，两个和第三个不能正确显示在"xs"视图中 （请注意，只有一个，4 和 5 所示）：

![而无需使用 clearfix 网格](bootstrap/_static/grid-without-clearfix.png)

在此示例中，只有一行`<div>`时使用的并启动仍然主要是未正确的操作方面的布局和堆叠的列。 通常情况下，应指定行`<div>`对于每个水平行布局要求，和当然可以嵌套在另一个的 Bootstrap 网格。 执行操作时，每个嵌套的网格将占用 100%的在放置它，然后可以通过使用列类细分的元素的宽度。

### <a name="jumbotron"></a>Jumbotron

如果使用过 Visual Studio 2012 或 2013年中的默认 ASP.NET Core MVC 模板，您可能已注意 Jumbotron 中操作。 它是指可用于显示较大的背景图像，对操作、 轮显或类似的元素的调用的页的大型全角部分。 若要向页面添加 jumbotron，只需添加`<div>`并为其提供的类"jumbotron"，然后放置容器`<div>`内，并添加你的内容。 我们可以轻松调整有关页后，可以使用它将显示在主标题 jumbotron 标准：

![jumbotron 示例](bootstrap/_static/jumbotron.png)

### <a name="buttons"></a>按钮

下图中显示的默认按钮类和其颜色。

![主题化按钮](bootstrap/_static/theme-buttons.png)

### <a name="badges"></a>徽章

徽章是指导航项旁边的小，通常为数值标注。 它们可以指示大量消息或通知等待或存在更新。 指定此类徽章是添加简单`<span>`包含文本"徽章"的类：

![主题化徽章](bootstrap/_static/theme-badges.png)

### <a name="alerts"></a>警报

您可能需要向应用程序的用户显示某种类型的通知、 警报或错误消息。 这是标准的警报类是非常有用。 有四个不同的严重级别，与关联的颜色方案：

![主题警报](bootstrap/_static/theme-alerts.png)

### <a name="navbars-and-menus"></a>导航栏和菜单

我们的布局已包含标准的导航栏中，但的 Bootstrap 主题支持其他样式选项。 我们可以方便地选择垂直显示导航栏，而不是水平如果偏向，也正在添加子导航项飞出式菜单中。 简单的导航菜单，如选项卡条带，构建的`<ul>`元素。 这些内容可以创建非常简单的只为他们提供了 CSS 类"nav"和"导航栏选项卡":

![主题化 tabstrip 控件](bootstrap/_static/theme-tabstrips.png)

Navbars 类似的方式，构建，但会稍微有些复杂。 他们开口`<nav>`或`<div>`"导航栏中"，在其中容器 div 包含的元素的其余部分的类。 我们的页面页眉中包括导航栏已 – 如下所示的一个只需对此进行扩展，添加对下拉列表菜单的支持：

![主题化 navbars](bootstrap/_static/theme-navbars.png)

### <a name="additional-elements"></a>其他元素

此外可以使用默认主题以呈现格式精美的样式，包括支持条带化视图的 HTML 表。 有类似按钮的样式标签。 您可以创建自定义支持其他样式选项，而标准的 HTML 下拉列表菜单`<select>`元素，类似于我们默认入门网站已在使用 Navbars 和。 如果你需要一个进度栏，有几种样式可供选择，以及列出组和包含标题和内容的面板。 浏览的标准的 Bootstrap 主题中的其他选项：

[http://getbootstrap.com/examples/theme/](http://getbootstrap.com/examples/theme/)

## <a name="more-themes"></a>更多主题

可以通过重写部分或全部其 CSS 扩展标准的 Bootstrap 主题，调整颜色和样式，以满足自己的应用程序的需要。 如果你想要开始从现成的主题，有几个主题库可用联机的 Bootstrap 主题，例如 WrapBootstrap.com （它具有多种商业主题） 和 Bootswatch.com （它提供了免费的主题） 中的专用化。 某些付费模板可提供大量之上的基本的 Bootstrap 主题，例如管理菜单和仪表板的丰富支持功能丰富的图表和仪表。 热门付费模板的一个示例是 Inspinia，以下屏幕截图所示：

![示例主题 inspinia](bootstrap/_static/theme-inspinia.png)

如果你想要更改您的 Bootstrap 主题，请将放*bootstrap.css*主题中所需的文件**wwwroot/css**文件夹并更改中的引用 *_Layout.cshtml*若要将其指定。 更改所有环境的链接：

```html
<environment names="Development">
    <link rel="stylesheet" href="~/css/bootstrap.css" />
```

```html
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/bootstrap.min.css" />
```

如果你想要构建自己的仪表板，你可以从提供的免费示例从这里开始： [ http://getbootstrap.com/examples/dashboard/ ](http://getbootstrap.com/examples/dashboard/)。

## <a name="components"></a>组件数

除了已经讨论过这些元素，Bootstrap 包括对各种支持[内置 UI 组件](http://getbootstrap.com/components/)。

### <a name="glyphicons"></a>Glyphicons

Bootstrap 包括 glyphicons 的图标集 ([http://glyphicons.com](http://glyphicons.com))，使用超过 200 个免费提供支持 Bootstrap 的 web 应用程序中使用的图标。 下面是一个小型示例：

![Glyphicons](bootstrap/_static/theme-glyphicons.png)

### <a name="input-groups"></a>输入的组

输入的组允许绑定的附加文本或按钮与输入元素，从而为用户提供更直观的体验：

![输入的组](bootstrap/_static/input-groups.png)

### <a name="breadcrumbs"></a>路径导航

痕迹导航栏是一个常见 UI 组件，用于显示用户，其最新历史记录或站点的导航层次结构中的深度。 通过将"痕迹导航"类应用于任何轻松添加`<ol>`列表元素。 通过使用"分页"类上包括用于分页的内置支持`<ul>`元素内的`<nav>`。 使用添加响应式嵌入幻灯片放映、 视频`<iframe>`， `<embed>`， `<video>`，或`<object>`Bootstrap 将自动设置样式的元素。 使用特定的类，如"嵌入的响应式-16by9"指定特定的纵横比。

## <a name="javascript-support"></a>JavaScript 支持

Bootstrap 的 JavaScript 库包括对包含的组件，您可以控制其行为以编程方式在应用程序中的 API 支持。 此外， *bootstrap.js*包含数十个针对自定义 jQuery 插件，提供其他功能，例如转换，模式对话框，向下滚动 （正在更新样式基于用户具有滚动文档中的何处） 的检测，因此它们不会滚动出屏幕折叠到窗口的行为、 轮播、 和附加菜单。 没有足够的空间来涵盖所有 Bootstrap – 若要了解详细信息，请访问内置 JavaScript 外接程序[ http://getbootstrap.com/javascript/ ](http://getbootstrap.com/javascript/)。

## <a name="summary"></a>总结

Bootstrap 提供了一个 web 框架，可用于快速和高效地布局和样式各种网站和应用程序。 其基本版式和样式提供愉快的外观和感觉，可轻松地通过自定义主题支持，可以是手工或购买商业上操作。 它支持 web 组件，在过去会昂贵的第三方控件来完成，同时支持现代和开放 web 标准要求的主机。
