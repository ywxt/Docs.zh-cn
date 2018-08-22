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
# <a name="build-beautiful-responsive-sites-with-bootstrap-and-aspnet-core"></a><span data-ttu-id="ad6e3-103">使用 ASP.NET Core 和 Bootstrap 构建响应灵敏、布局美观的网站</span><span class="sxs-lookup"><span data-stu-id="ad6e3-103">Build beautiful, responsive sites with Bootstrap and ASP.NET Core</span></span>

<a name="bootstrap-index"></a>

<span data-ttu-id="ad6e3-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="ad6e3-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="ad6e3-105">Bootstrap 是目前用于开发响应式 web 应用程序最常用的 web 框架。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-105">Bootstrap is currently the most popular web framework for developing responsive web applications.</span></span> <span data-ttu-id="ad6e3-106">它在改进网站用户体验方面具有多种优势并提供多种相关功能，无论是前沿设计和开发领域中的新手还是专家，都能够利用这些优势和功能。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-106">It offers a number of features and benefits that can improve your users' experience with your web site, whether you're a novice at front-end design and development or an expert.</span></span> <span data-ttu-id="ad6e3-107">Bootstrap 部署为一组 CSS 和 JavaScript 文件，旨在帮助网站和应用程序跨电话、平板电脑、台式计算机等多种设备高效灵活地缩放规模。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-107">Bootstrap is deployed as a set of CSS and JavaScript files, and is designed to help your website or application scale efficiently from phones to tablets to desktops.</span></span>

## <a name="get-started"></a><span data-ttu-id="ad6e3-108">入门</span><span class="sxs-lookup"><span data-stu-id="ad6e3-108">Get started</span></span>

<span data-ttu-id="ad6e3-109">可采用多种方式来了解和学习如何使用 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-109">There are several ways to get started with Bootstrap.</span></span> <span data-ttu-id="ad6e3-110">如果是从 Visual Studio 中的新 web 应用程序开始，可选择用于 ASP.NET Core 的默认启动器模板，这样便可通过预安装的方式获取 Bootstrap：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-110">If you're starting a new web application in Visual Studio, you can choose the default starter template for ASP.NET Core, in which case Bootstrap will come pre-installed:</span></span>

![初学者模板解决方案视图中启动](bootstrap/_static/bootstrap-in-starter-template.png)

<span data-ttu-id="ad6e3-112">添加 ASP.NET Core Bootstrap 项目是只需将其添加到*bower.json*作为依赖项：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-112">Adding Bootstrap to an ASP.NET Core project is simply a matter of adding it to *bower.json* as a dependency:</span></span>

[!code-json[](../common/samples/WebApplication1/bower.json?highlight=5)]

<span data-ttu-id="ad6e3-113">这是 Bootstrap 添加到 ASP.NET Core 项目的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-113">This is the recommended way to add Bootstrap to an ASP.NET Core project.</span></span>

<span data-ttu-id="ad6e3-114">此外可以安装使用多个包管理器，例如 Bower、 npm、 或 NuGet 之一的 bootstrap。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-114">You can also install bootstrap using one of several package managers, such as Bower, npm, or NuGet.</span></span> <span data-ttu-id="ad6e3-115">每种情况下，该过程是实质上是相同的：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-115">In each case, the process is essentially the same:</span></span>

### <a name="bower"></a><span data-ttu-id="ad6e3-116">Bower</span><span class="sxs-lookup"><span data-stu-id="ad6e3-116">Bower</span></span>

```console
bower install bootstrap
```

### <a name="npm"></a><span data-ttu-id="ad6e3-117">npm</span><span class="sxs-lookup"><span data-stu-id="ad6e3-117">npm</span></span>

```console
npm install bootstrap
```

### <a name="nuget"></a><span data-ttu-id="ad6e3-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="ad6e3-118">NuGet</span></span>

```console
Install-Package bootstrap
```

> [!NOTE]
> <span data-ttu-id="ad6e3-119">安装客户端依赖关系，如 ASP.NET Core 中的 Bootstrap 为通过 Bower 的建议的方法 (使用*bower.json*，如上所示)。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-119">The recommended way to install client-side dependencies like Bootstrap in ASP.NET Core is via Bower (using *bower.json*, as shown above).</span></span> <span data-ttu-id="ad6e3-120">使用 npm/NuGet 显示来演示如何轻松地 Bootstrap 添加到其他类型的 web 应用程序，包括 ASP.NET 的早期版本。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-120">The use of npm/NuGet are shown to demonstrate how easily Bootstrap can be added to other kinds of web applications, including earlier versions of ASP.NET.</span></span>

<span data-ttu-id="ad6e3-121">如果引用自己的 Bootstrap 的本地版本，你将需要使用它的任何页面中引用它们。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-121">If you're referencing your own local versions of Bootstrap, you'll need to reference them in any pages that will use it.</span></span> <span data-ttu-id="ad6e3-122">在生产环境中应该引用 bootstrap 使用 CDN。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-122">In production you should reference bootstrap using a CDN.</span></span> <span data-ttu-id="ad6e3-123">在默认 ASP.NET Core 站点模板，请 *_Layout.cshtml*文件因此像这样：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-123">In the default ASP.NET Core site template, the *_Layout.cshtml* file does so like this:</span></span>

[!code-html[](../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=9,13,51,59)]

> [!NOTE]
> <span data-ttu-id="ad6e3-124">如果你打算使用的任何 Bootstrap 的 jQuery 插件，还需要引用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-124">If you're going to be using any of Bootstrap's jQuery plugins, you will also need to reference jQuery.</span></span>

## <a name="basic-templates-and-features"></a><span data-ttu-id="ad6e3-125">基本模板和功能</span><span class="sxs-lookup"><span data-stu-id="ad6e3-125">Basic templates and features</span></span>

<span data-ttu-id="ad6e3-126">最基本的引导模板看起来很像 *_Layout.cshtml*文件所示更高版本，并只包括用于导航，可以在这里要呈现的页的其余部分的基本菜单。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-126">The most basic Bootstrap template looks very much like the *_Layout.cshtml* file shown above, and simply includes a basic menu for navigation and a place to render the rest of the page.</span></span>

### <a name="basic-navigation"></a><span data-ttu-id="ad6e3-127">基本导航</span><span class="sxs-lookup"><span data-stu-id="ad6e3-127">Basic navigation</span></span>

<span data-ttu-id="ad6e3-128">默认模板使用的一组`<div>`元素来呈现顶部导航栏和页面的主要部分。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-128">The default template uses a set of `<div>` elements to render a top navbar and the main body of the page.</span></span> <span data-ttu-id="ad6e3-129">如果使用的 HTML5，您可以替换第一个`<div>`标记`<nav>`标记以获取相同的效果，但具有更精确的语义。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-129">If you're using HTML5, you can replace the first `<div>` tag with a `<nav>` tag to get the same effect, but with more precise semantics.</span></span> <span data-ttu-id="ad6e3-130">此第一部分中`<div>`可以看到有其他几种。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-130">Within this first `<div>` you can see there are several others.</span></span> <span data-ttu-id="ad6e3-131">首先，`<div>`类的"容器"，然后在该，另外两个`<div>`元素:"导航条标头"和"折叠导航栏"。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-131">First, a `<div>` with a class of "container", and then within that, two more `<div>` elements: "navbar-header" and "navbar-collapse".</span></span> <span data-ttu-id="ad6e3-132">导航条标头 div 包括时某些最小宽度，显示 3 个水平行下面的屏幕，将显示一个按钮 (所谓"汉堡图标")。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-132">The navbar-header div includes a button that will appear when the screen is below a certain minimum width, showing 3 horizontal lines (a so-called "hamburger icon").</span></span> <span data-ttu-id="ad6e3-133">使用纯 HTML 和 CSS; 呈现图标没有图像是必需的。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-133">The icon is rendered using pure HTML and CSS; no image is required.</span></span> <span data-ttu-id="ad6e3-134">这是显示的图标，与每个代码<span>呈现一个白色条的标记：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-134">This is the code that displays the icon, with each of the <span> tags rendering one of the white bars:</span></span>

```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

<span data-ttu-id="ad6e3-135">它还包括应用程序名称，通过在左上角中出现。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-135">It also includes the application name, which appears in the top left.</span></span> <span data-ttu-id="ad6e3-136">主导航菜单呈现的`<ul>`中的第二个 div 元素，包括为主页，大约，和联系人的链接。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-136">The main navigation menu is rendered by the `<ul>` element within the second div, and includes links to Home, About, and Contact.</span></span> <span data-ttu-id="ad6e3-137">下方导航窗格中，每个页面的主要部分呈现在另一个`<div>`、 标记与"容器"和"正文内容"类。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-137">Below the navigation, the main body of each page is rendered in another `<div>`, marked with the "container" and "body-content" classes.</span></span> <span data-ttu-id="ad6e3-138">在默认的简单\_页的内容呈现的页上，然后一个简单相关联的特定视图，如下所示的布局文件`<footer>`添加到末尾`<div>`元素。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-138">In the simple default \_Layout file shown here, the contents of the page are rendered by the specific View associated with the page, and then a simple `<footer>` is added to the end of the `<div>` element.</span></span> <span data-ttu-id="ad6e3-139">您可以看到内置有关页面将显示使用此模板：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-139">You can see how the built-in About page appears using this template:</span></span>

![有关页](bootstrap/_static/about-page-wide.png)

<span data-ttu-id="ad6e3-141">折叠导航栏中的，使用"汉堡"按钮，在右上角，将显示在窗口低于一定宽度时：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-141">The collapsed navbar, with "hamburger" button in the top right, appears when the window drops below a certain width:</span></span>

![有关带汉堡菜单的页面](bootstrap/_static/about-page-hamburger.png)

<span data-ttu-id="ad6e3-143">单击该图标将显示向下滑从页面顶部垂直抽屉中的菜单项：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-143">Clicking the icon reveals the menu items in a vertical drawer that slides down from the top of the page:</span></span>

![有关页面与展开的 hamburger 菜单](bootstrap/_static/about-page-hamburger-open.png)

### <a name="typography-and-links"></a><span data-ttu-id="ad6e3-145">版式和链接</span><span class="sxs-lookup"><span data-stu-id="ad6e3-145">Typography and links</span></span>

<span data-ttu-id="ad6e3-146">Bootstrap 设置站点的基本版式、 颜色和格式设置在其 CSS 文件中的链接。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-146">Bootstrap sets up the site's basic typography, colors, and link formatting in its CSS file.</span></span> <span data-ttu-id="ad6e3-147">此 CSS 文件包含默认样式表、 按钮、 窗体元素、 图像和的详细信息 ([了解详细信息](http://getbootstrap.com/css/))。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-147">This CSS file includes default styles for tables, buttons, form elements, images, and more ([learn more](http://getbootstrap.com/css/)).</span></span> <span data-ttu-id="ad6e3-148">一个特别有用的功能是网格布局系统，接下来介绍。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-148">One particularly useful feature is the grid layout system, covered next.</span></span>

### <a name="grids"></a><span data-ttu-id="ad6e3-149">网格</span><span class="sxs-lookup"><span data-stu-id="ad6e3-149">Grids</span></span>

<span data-ttu-id="ad6e3-150">Bootstrap 的最热门的功能之一是其网格布局系统。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-150">One of the most popular features of Bootstrap is its grid layout system.</span></span> <span data-ttu-id="ad6e3-151">新式 web 应用程序应避免使用`<table>`布局，而将使用此元素限制为实际的表格数据的标记。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-151">Modern web applications should avoid using the `<table>` tag for layout, instead restricting the use of this element to actual tabular data.</span></span> <span data-ttu-id="ad6e3-152">相反，列和行可以进行布局使用一系列`<div>`元素和相应的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-152">Instead, columns and rows can be laid out using a series of `<div>` elements and the appropriate CSS classes.</span></span> <span data-ttu-id="ad6e3-153">有几个优点包括能够调整的网格显示垂直屏幕较窄，例如在手机布局，这种方法。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-153">There are several advantages to this approach, including the ability to adjust the layout of grids to display vertically on narrow screens, such as on phones.</span></span>

<span data-ttu-id="ad6e3-154">[Bootstrap 的网格布局系统](http://getbootstrap.com/css/#grid)基于十二个列。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-154">[Bootstrap's grid layout system](http://getbootstrap.com/css/#grid) is based on twelve columns.</span></span> <span data-ttu-id="ad6e3-155">选择此数字是因为可以为 1、 2、 3 或 4 列均匀划分和列宽异中 1 到 12 的垂直屏幕的宽度 /。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-155">This number was chosen because it can be divided evenly into 1, 2, 3, or 4 columns, and column widths can vary to within 1/12th of the vertical width of the screen.</span></span> <span data-ttu-id="ad6e3-156">若要开始使用网格布局系统，你应该开始使用容器`<div>`，然后添加一行`<div>`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-156">To start using the grid layout system, you should begin with a container `<div>` and then add a row `<div>`, as shown here:</span></span>

```html
<div class="container">
    <div class="row">
        ...
    </div>
</div>
```

<span data-ttu-id="ad6e3-157">接下来，添加其他`<div>`为每个列的元素和指定的列数的`<div>`应占用 （共 12) 作为"col-md-"开头的 CSS 类的一部分。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-157">Next, add additional `<div>` elements for each column, and specify the number of columns that `<div>` should occupy (out of 12) as part of a CSS class starting with "col-md-".</span></span> <span data-ttu-id="ad6e3-158">例如，如果你想要仅需提供两个大小相等的列，您将为每个使用"列-md-6"的类。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-158">For instance, if you want to simply have two columns of equal size, you would use a class of "col-md-6" for each one.</span></span> <span data-ttu-id="ad6e3-159">在这种情况下"md"的缩写"medium"，指的是标准大小的台式计算机的显示大小。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-159">In this case "md" is short for "medium" and refers to standard-sized desktop computer display sizes.</span></span> <span data-ttu-id="ad6e3-160">有四个不同的选项可以选择从，并且每个将会使用的更高版本的宽度，除非重写 （因此如果你想要而不考虑屏幕宽度固定的布局，则可以只指定 xs 类）。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-160">There are four different options you can choose from, and each will be used for higher widths unless overridden (so if you want the layout to be fixed regardless of screen width, you can just specify xs classes).</span></span>

<span data-ttu-id="ad6e3-161">CSS 类前缀</span><span class="sxs-lookup"><span data-stu-id="ad6e3-161">CSS Class Prefix</span></span> | <span data-ttu-id="ad6e3-162">设备层</span><span class="sxs-lookup"><span data-stu-id="ad6e3-162">Device Tier</span></span> | <span data-ttu-id="ad6e3-163">宽度</span><span class="sxs-lookup"><span data-stu-id="ad6e3-163">Width</span></span>
:---: | :---: | :---:
<span data-ttu-id="ad6e3-164">col-xs-</span><span class="sxs-lookup"><span data-stu-id="ad6e3-164">col-xs-</span></span> | <span data-ttu-id="ad6e3-165">手机</span><span class="sxs-lookup"><span data-stu-id="ad6e3-165">Phones</span></span> | <span data-ttu-id="ad6e3-166">< 768px</span><span class="sxs-lookup"><span data-stu-id="ad6e3-166">< 768px</span></span>
<span data-ttu-id="ad6e3-167">col-sm-</span><span class="sxs-lookup"><span data-stu-id="ad6e3-167">col-sm-</span></span> | <span data-ttu-id="ad6e3-168">平板电脑</span><span class="sxs-lookup"><span data-stu-id="ad6e3-168">Tablets</span></span> | <span data-ttu-id="ad6e3-169">>= 768px</span><span class="sxs-lookup"><span data-stu-id="ad6e3-169">>= 768px</span></span>
<span data-ttu-id="ad6e3-170">col-md-</span><span class="sxs-lookup"><span data-stu-id="ad6e3-170">col-md-</span></span> | <span data-ttu-id="ad6e3-171">台式计算机</span><span class="sxs-lookup"><span data-stu-id="ad6e3-171">Desktops</span></span> | <span data-ttu-id="ad6e3-172">>= 992px</span><span class="sxs-lookup"><span data-stu-id="ad6e3-172">>= 992px</span></span>
<span data-ttu-id="ad6e3-173">col-lg-</span><span class="sxs-lookup"><span data-stu-id="ad6e3-173">col-lg-</span></span> | <span data-ttu-id="ad6e3-174">更大的桌面显示</span><span class="sxs-lookup"><span data-stu-id="ad6e3-174">Larger Desktop Displays</span></span> | <span data-ttu-id="ad6e3-175">> = 1200px</span><span class="sxs-lookup"><span data-stu-id="ad6e3-175">>= 1200px</span></span>

<span data-ttu-id="ad6e3-176">指定两个列将同时使用"列-md-6"生成的布局中将两个列在桌面的解决方法，但较小的设备 （或更窄浏览器窗口在桌面上），使用户能够轻松地查看上呈现报表时，这两个列将垂直堆叠时而无需以进行水平滚动的内容。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-176">When specifying two columns both with "col-md-6" the resulting layout will be two columns at desktop resolutions, but these two columns will stack vertically when rendered on smaller devices (or a narrower browser window on a desktop), allowing users to easily view content without the need to scroll horizontally.</span></span>

<span data-ttu-id="ad6e3-177">Bootstrap 始终默认为单列布局，因此您只需要指定的列，如果希望多个列。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-177">Bootstrap will always default to a single-column layout, so you only need to specify columns when you want more than one column.</span></span> <span data-ttu-id="ad6e3-178">你想要显式指定的唯一时间`<div>`占用所有的 12 列会重写的行为更大的设备层。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-178">The only time you would want to explicitly specify that a `<div>` take up all 12 columns would be to override the behavior of a larger device tier.</span></span> <span data-ttu-id="ad6e3-179">在指定多个设备层类时，您可能需要重置列呈现在特定时间点。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-179">When specifying multiple device tier classes, you may need to reset the column rendering at certain points.</span></span> <span data-ttu-id="ad6e3-180">将仅在某一特定视区中可见的 clearfix div 添加可以实现此目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-180">Adding a clearfix div that's only visible within a certain viewport can achieve this, as shown here:</span></span>

![窄和宽视区网格](bootstrap/_static/narrow-and-wide-viewport-grid.png)

<span data-ttu-id="ad6e3-182">在上述示例中，一个和第二个共享"md"布局中的某一行而 2 和 3 共享"xs"布局中的行。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-182">In the above example, One and Two share a row in the "md" layout, while Two and Three share a row in the "xs" layout.</span></span> <span data-ttu-id="ad6e3-183">而无需 clearfix `<div>`，两个和第三个不能正确显示在"xs"视图中 （请注意，只有一个，4 和 5 所示）：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-183">Without the clearfix `<div>`, Two and Three are not shown correctly in the "xs" view (note that only One, Four, and Five are shown):</span></span>

![而无需使用 clearfix 网格](bootstrap/_static/grid-without-clearfix.png)

<span data-ttu-id="ad6e3-185">在此示例中，只有一行`<div>`时使用的并启动仍然主要是未正确的操作方面的布局和堆叠的列。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-185">In this example, only a single row `<div>` was used, and Bootstrap still mostly did the right thing with regard to the layout and stacking of the columns.</span></span> <span data-ttu-id="ad6e3-186">通常情况下，应指定行`<div>`对于每个水平行布局要求，和当然可以嵌套在另一个的 Bootstrap 网格。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-186">Typically, you should specify a row `<div>` for each horizontal row your layout requires, and of course you can nest Bootstrap grids within one another.</span></span> <span data-ttu-id="ad6e3-187">执行操作时，每个嵌套的网格将占用 100%的在放置它，然后可以通过使用列类细分的元素的宽度。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-187">When you do, each nested grid will occupy 100% of the width of the element in which it's placed, which can then be subdivided using column classes.</span></span>

### <a name="jumbotron"></a><span data-ttu-id="ad6e3-188">Jumbotron</span><span class="sxs-lookup"><span data-stu-id="ad6e3-188">Jumbotron</span></span>

<span data-ttu-id="ad6e3-189">如果使用过 Visual Studio 2012 或 2013年中的默认 ASP.NET Core MVC 模板，您可能已注意 Jumbotron 中操作。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-189">If you've used the default ASP.NET Core MVC templates in Visual Studio 2012 or 2013, you've probably seen the Jumbotron in action.</span></span> <span data-ttu-id="ad6e3-190">它是指可用于显示较大的背景图像，对操作、 轮显或类似的元素的调用的页的大型全角部分。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-190">It refers to a large full-width section of a page that can be used to display a large background image, a call to action, a rotator, or similar elements.</span></span> <span data-ttu-id="ad6e3-191">若要向页面添加 jumbotron，只需添加`<div>`并为其提供的类"jumbotron"，然后放置容器`<div>`内，并添加你的内容。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-191">To add a jumbotron to a page, simply add a `<div>` and give it a class of "jumbotron", then place a container `<div>` inside and add your content.</span></span> <span data-ttu-id="ad6e3-192">我们可以轻松调整有关页后，可以使用它将显示在主标题 jumbotron 标准：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-192">We can easily adjust the standard About page to use a jumbotron for the main headings it displays:</span></span>

![jumbotron 示例](bootstrap/_static/jumbotron.png)

### <a name="buttons"></a><span data-ttu-id="ad6e3-194">按钮</span><span class="sxs-lookup"><span data-stu-id="ad6e3-194">Buttons</span></span>

<span data-ttu-id="ad6e3-195">下图中显示的默认按钮类和其颜色。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-195">The default button classes and their colors are shown in the figure below.</span></span>

![主题化按钮](bootstrap/_static/theme-buttons.png)

### <a name="badges"></a><span data-ttu-id="ad6e3-197">徽章</span><span class="sxs-lookup"><span data-stu-id="ad6e3-197">Badges</span></span>

<span data-ttu-id="ad6e3-198">徽章是指导航项旁边的小，通常为数值标注。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-198">Badges refer to small, usually numeric callouts next to a navigation item.</span></span> <span data-ttu-id="ad6e3-199">它们可以指示大量消息或通知等待或存在更新。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-199">They can indicate a number of messages or notifications waiting, or the presence of updates.</span></span> <span data-ttu-id="ad6e3-200">指定此类徽章是添加简单`<span>`包含文本"徽章"的类：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-200">Specifying such badges is as simple as adding a `<span>` containing the text, with a class of "badge":</span></span>

![主题化徽章](bootstrap/_static/theme-badges.png)

### <a name="alerts"></a><span data-ttu-id="ad6e3-202">警报</span><span class="sxs-lookup"><span data-stu-id="ad6e3-202">Alerts</span></span>

<span data-ttu-id="ad6e3-203">您可能需要向应用程序的用户显示某种类型的通知、 警报或错误消息。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-203">You may need to display some kind of notification, alert, or error message to your application's users.</span></span> <span data-ttu-id="ad6e3-204">这是标准的警报类是非常有用。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-204">That's where the standard alert classes are useful.</span></span> <span data-ttu-id="ad6e3-205">有四个不同的严重级别，与关联的颜色方案：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-205">There are four different severity levels with associated color schemes:</span></span>

![主题警报](bootstrap/_static/theme-alerts.png)

### <a name="navbars-and-menus"></a><span data-ttu-id="ad6e3-207">导航栏和菜单</span><span class="sxs-lookup"><span data-stu-id="ad6e3-207">Navbars and menus</span></span>

<span data-ttu-id="ad6e3-208">我们的布局已包含标准的导航栏中，但的 Bootstrap 主题支持其他样式选项。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-208">Our layout already includes a standard navbar, but the Bootstrap theme supports additional styling options.</span></span> <span data-ttu-id="ad6e3-209">我们可以方便地选择垂直显示导航栏，而不是水平如果偏向，也正在添加子导航项飞出式菜单中。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-209">We can also easily opt to display the navbar vertically rather than horizontally if that's preferred, as well as adding sub-navigation items in flyout menus.</span></span> <span data-ttu-id="ad6e3-210">简单的导航菜单，如选项卡条带，构建的`<ul>`元素。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-210">Simple navigation menus, like tab strips, are built on top of `<ul>` elements.</span></span> <span data-ttu-id="ad6e3-211">这些内容可以创建非常简单的只为他们提供了 CSS 类"nav"和"导航栏选项卡":</span><span class="sxs-lookup"><span data-stu-id="ad6e3-211">These can be created very simply by just providing them with the CSS classes "nav" and "nav-tabs":</span></span>

![主题化 tabstrip 控件](bootstrap/_static/theme-tabstrips.png)

<span data-ttu-id="ad6e3-213">Navbars 类似的方式，构建，但会稍微有些复杂。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-213">Navbars are built similarly, but are a bit more complex.</span></span> <span data-ttu-id="ad6e3-214">他们开口`<nav>`或`<div>`"导航栏中"，在其中容器 div 包含的元素的其余部分的类。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-214">They start with a `<nav>` or `<div>` with a class of "navbar", within which a container div holds the rest of the elements.</span></span> <span data-ttu-id="ad6e3-215">我们的页面页眉中包括导航栏已 – 如下所示的一个只需对此进行扩展，添加对下拉列表菜单的支持：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-215">Our page includes a navbar in its header already – the one shown below simply expands on this, adding support for a dropdown menu:</span></span>

![主题化 navbars](bootstrap/_static/theme-navbars.png)

### <a name="additional-elements"></a><span data-ttu-id="ad6e3-217">其他元素</span><span class="sxs-lookup"><span data-stu-id="ad6e3-217">Additional elements</span></span>

<span data-ttu-id="ad6e3-218">此外可以使用默认主题以呈现格式精美的样式，包括支持条带化视图的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-218">The default theme can also be used to present HTML tables in a nicely formatted style, including support for striped views.</span></span> <span data-ttu-id="ad6e3-219">有类似按钮的样式标签。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-219">There are labels with styles that are similar to those of the buttons.</span></span> <span data-ttu-id="ad6e3-220">您可以创建自定义支持其他样式选项，而标准的 HTML 下拉列表菜单`<select>`元素，类似于我们默认入门网站已在使用 Navbars 和。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-220">You can create custom Dropdown menus that support additional styling options beyond the standard HTML `<select>` element, along with Navbars like the one our default starter site is already using.</span></span> <span data-ttu-id="ad6e3-221">如果你需要一个进度栏，有几种样式可供选择，以及列出组和包含标题和内容的面板。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-221">If you need a progress bar, there are several styles to choose from, as well as List Groups and panels that include a title and content.</span></span> <span data-ttu-id="ad6e3-222">浏览的标准的 Bootstrap 主题中的其他选项：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-222">Explore additional options within the standard Bootstrap Theme here:</span></span>

[http://getbootstrap.com/examples/theme/](http://getbootstrap.com/examples/theme/)

## <a name="more-themes"></a><span data-ttu-id="ad6e3-223">更多主题</span><span class="sxs-lookup"><span data-stu-id="ad6e3-223">More themes</span></span>

<span data-ttu-id="ad6e3-224">可以通过重写部分或全部其 CSS 扩展标准的 Bootstrap 主题，调整颜色和样式，以满足自己的应用程序的需要。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-224">You can extend the standard Bootstrap theme by overriding some or all of its CSS, adjusting the colors and styles to suit your own application's needs.</span></span> <span data-ttu-id="ad6e3-225">如果你想要开始从现成的主题，有几个主题库可用联机的 Bootstrap 主题，例如 WrapBootstrap.com （它具有多种商业主题） 和 Bootswatch.com （它提供了免费的主题） 中的专用化。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-225">If you'd like to start from a ready-made theme, there are several theme galleries available online that specialize in Bootstrap themes, such as WrapBootstrap.com (which has a variety of commercial themes) and Bootswatch.com (which offers free themes).</span></span> <span data-ttu-id="ad6e3-226">某些付费模板可提供大量之上的基本的 Bootstrap 主题，例如管理菜单和仪表板的丰富支持功能丰富的图表和仪表。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-226">Some of the paid templates available provide a great deal of functionality on top of the basic Bootstrap theme, such as rich support for administrative menus, and dashboards with rich charts and gauges.</span></span> <span data-ttu-id="ad6e3-227">热门付费模板的一个示例是 Inspinia，以下屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-227">An example of a popular paid template is Inspinia, which is shown in the following screenshot:</span></span>

![示例主题 inspinia](bootstrap/_static/theme-inspinia.png)

<span data-ttu-id="ad6e3-229">如果你想要更改您的 Bootstrap 主题，请将放*bootstrap.css*主题中所需的文件**wwwroot/css**文件夹并更改中的引用 *_Layout.cshtml*若要将其指定。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-229">If you want to change your Bootstrap theme, put the *bootstrap.css* file for the theme you want in the **wwwroot/css** folder and change the references in *_Layout.cshtml* to point it.</span></span> <span data-ttu-id="ad6e3-230">更改所有环境的链接：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-230">Change the links for all environments:</span></span>

```html
<environment names="Development">
    <link rel="stylesheet" href="~/css/bootstrap.css" />
```

```html
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/bootstrap.min.css" />
```

<span data-ttu-id="ad6e3-231">如果你想要构建自己的仪表板，你可以从提供的免费示例从这里开始： [ http://getbootstrap.com/examples/dashboard/ ](http://getbootstrap.com/examples/dashboard/)。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-231">If you want to build your own dashboard, you can start from the free example available here: [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/).</span></span>

## <a name="components"></a><span data-ttu-id="ad6e3-232">组件数</span><span class="sxs-lookup"><span data-stu-id="ad6e3-232">Components</span></span>

<span data-ttu-id="ad6e3-233">除了已经讨论过这些元素，Bootstrap 包括对各种支持[内置 UI 组件](http://getbootstrap.com/components/)。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-233">In addition to those elements already discussed, Bootstrap includes support for a variety of [built-in UI components](http://getbootstrap.com/components/).</span></span>

### <a name="glyphicons"></a><span data-ttu-id="ad6e3-234">Glyphicons</span><span class="sxs-lookup"><span data-stu-id="ad6e3-234">Glyphicons</span></span>

<span data-ttu-id="ad6e3-235">Bootstrap 包括 glyphicons 的图标集 ([http://glyphicons.com](http://glyphicons.com))，使用超过 200 个免费提供支持 Bootstrap 的 web 应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-235">Bootstrap includes icon sets from Glyphicons ([http://glyphicons.com](http://glyphicons.com)), with over 200 icons freely available for use within your Bootstrap-enabled web application.</span></span> <span data-ttu-id="ad6e3-236">下面是一个小型示例：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-236">Here's just a small sample:</span></span>

![Glyphicons](bootstrap/_static/theme-glyphicons.png)

### <a name="input-groups"></a><span data-ttu-id="ad6e3-238">输入的组</span><span class="sxs-lookup"><span data-stu-id="ad6e3-238">Input groups</span></span>

<span data-ttu-id="ad6e3-239">输入的组允许绑定的附加文本或按钮与输入元素，从而为用户提供更直观的体验：</span><span class="sxs-lookup"><span data-stu-id="ad6e3-239">Input groups allow bundling of additional text or buttons with an input element, providing the user with a more intuitive experience:</span></span>

![输入的组](bootstrap/_static/input-groups.png)

### <a name="breadcrumbs"></a><span data-ttu-id="ad6e3-241">路径导航</span><span class="sxs-lookup"><span data-stu-id="ad6e3-241">Breadcrumbs</span></span>

<span data-ttu-id="ad6e3-242">痕迹导航栏是一个常见 UI 组件，用于显示用户，其最新历史记录或站点的导航层次结构中的深度。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-242">Breadcrumbs are a common UI component used to show a user their recent history or depth within a site's navigation hierarchy.</span></span> <span data-ttu-id="ad6e3-243">通过将"痕迹导航"类应用于任何轻松添加`<ol>`列表元素。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-243">Add them easily by applying the "breadcrumb" class to any `<ol>` list element.</span></span> <span data-ttu-id="ad6e3-244">通过使用"分页"类上包括用于分页的内置支持`<ul>`元素内的`<nav>`。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-244">Include built-in support for pagination by using the "pagination" class on a `<ul>` element within a `<nav>`.</span></span> <span data-ttu-id="ad6e3-245">使用添加响应式嵌入幻灯片放映、 视频`<iframe>`， `<embed>`， `<video>`，或`<object>`Bootstrap 将自动设置样式的元素。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-245">Add responsive embedded slideshows and video by using `<iframe>`, `<embed>`, `<video>`, or `<object>` elements, which Bootstrap will style automatically.</span></span> <span data-ttu-id="ad6e3-246">使用特定的类，如"嵌入的响应式-16by9"指定特定的纵横比。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-246">Specify a particular aspect ratio by using specific classes like "embed-responsive-16by9".</span></span>

## <a name="javascript-support"></a><span data-ttu-id="ad6e3-247">JavaScript 支持</span><span class="sxs-lookup"><span data-stu-id="ad6e3-247">JavaScript support</span></span>

<span data-ttu-id="ad6e3-248">Bootstrap 的 JavaScript 库包括对包含的组件，您可以控制其行为以编程方式在应用程序中的 API 支持。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-248">Bootstrap's JavaScript library includes API support for the included components, allowing you to control their behavior programmatically within your application.</span></span> <span data-ttu-id="ad6e3-249">此外， *bootstrap.js*包含数十个针对自定义 jQuery 插件，提供其他功能，例如转换，模式对话框，向下滚动 （正在更新样式基于用户具有滚动文档中的何处） 的检测，因此它们不会滚动出屏幕折叠到窗口的行为、 轮播、 和附加菜单。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-249">In addition, *bootstrap.js* includes over a dozen custom jQuery plugins, providing additional features like transitions, modal dialogs, scroll detection (updating styles based on where the user has scrolled in the document), collapse behavior, carousels, and affixing menus to the window so they don't scroll off the screen.</span></span> <span data-ttu-id="ad6e3-250">没有足够的空间来涵盖所有 Bootstrap – 若要了解详细信息，请访问内置 JavaScript 外接程序[ http://getbootstrap.com/javascript/ ](http://getbootstrap.com/javascript/)。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-250">There's not sufficient room to cover all of the JavaScript add-ons built into Bootstrap – to learn more please visit [http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/).</span></span>

## <a name="summary"></a><span data-ttu-id="ad6e3-251">总结</span><span class="sxs-lookup"><span data-stu-id="ad6e3-251">Summary</span></span>

<span data-ttu-id="ad6e3-252">Bootstrap 提供了一个 web 框架，可用于快速和高效地布局和样式各种网站和应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-252">Bootstrap provides a web framework that can be used to quickly and productively lay out and style a wide variety of websites and applications.</span></span> <span data-ttu-id="ad6e3-253">其基本版式和样式提供愉快的外观和感觉，可轻松地通过自定义主题支持，可以是手工或购买商业上操作。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-253">Its basic typography and styles provide a pleasant look and feel that can easily be manipulated through custom theme support, which can be hand-crafted or purchased commercially.</span></span> <span data-ttu-id="ad6e3-254">它支持 web 组件，在过去会昂贵的第三方控件来完成，同时支持现代和开放 web 标准要求的主机。</span><span class="sxs-lookup"><span data-stu-id="ad6e3-254">It supports a host of web components that in the past would've required expensive third-party controls to accomplish, while supporting modern and open web standards.</span></span>
