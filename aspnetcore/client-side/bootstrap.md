---
title: "生成使用 Bootstrap 美观、 响应迅速站点"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: client-side/bootstrap
ms.openlocfilehash: dfed5c7a8e103973048295b7607008ecc7e90eeb
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="building-beautiful-responsive-sites-with-bootstrap"></a><span data-ttu-id="2f286-102">生成使用 Bootstrap 美观、 响应迅速站点</span><span class="sxs-lookup"><span data-stu-id="2f286-102">Building beautiful, responsive sites with Bootstrap</span></span>

<a name="bootstrap-index"></a>

<span data-ttu-id="2f286-103">通过[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="2f286-103">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="2f286-104">Bootstrap 目前最常用的 web 框架开发响应式 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f286-104">Bootstrap is currently the most popular web framework for developing responsive web applications.</span></span> <span data-ttu-id="2f286-105">无论您是在前端设计和开发或方面的专家新手，它提供大量的功能和优势，这样可以提高您的网站，用户的体验。</span><span class="sxs-lookup"><span data-stu-id="2f286-105">It offers a number of features and benefits that can improve your users' experience with your web site, whether you're a novice at front-end design and development or an expert.</span></span> <span data-ttu-id="2f286-106">Bootstrap 部署为一组 CSS 和 JavaScript 文件，并旨在从手机有效地帮助你的网站或应用程序缩放，平板电脑和桌面。</span><span class="sxs-lookup"><span data-stu-id="2f286-106">Bootstrap is deployed as a set of CSS and JavaScript files, and is designed to help your website or application scale efficiently from phones to tablets to desktops.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2f286-107">入门</span><span class="sxs-lookup"><span data-stu-id="2f286-107">Getting started</span></span>

<span data-ttu-id="2f286-108">有多种，若要开始使用 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="2f286-108">There are several ways to get started with Bootstrap.</span></span> <span data-ttu-id="2f286-109">如果你在 Visual Studio 中开始新的 web 应用程序，则可以为 ASP.NET Core，区分大小的 Bootstrap 会预安装选择默认初学者模板：</span><span class="sxs-lookup"><span data-stu-id="2f286-109">If you're starting a new web application in Visual Studio, you can choose the default starter template for ASP.NET Core, in which case Bootstrap will come pre-installed:</span></span>

![在初学者模板解决方案视图中启动](bootstrap/_static/bootstrap-in-starter-template.png)

<span data-ttu-id="2f286-111">添加 ASP.NET Core Bootstrap 项目是只需将其添加到*bower.json*作为依赖项：</span><span class="sxs-lookup"><span data-stu-id="2f286-111">Adding Bootstrap to an ASP.NET Core project is simply a matter of adding it to *bower.json* as a dependency:</span></span>

[!code-json[Main](../common/samples/WebApplication1/bower.json?highlight=5)]

<span data-ttu-id="2f286-112">这是 Bootstrap 添加到 ASP.NET 核心项目的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="2f286-112">This is the recommended way to add Bootstrap to an ASP.NET Core project.</span></span>

<span data-ttu-id="2f286-113">你还可以安装使用多个包管理器，例如 Bower、 npm 或 NuGet 之一的 bootstrap。</span><span class="sxs-lookup"><span data-stu-id="2f286-113">You can also install bootstrap using one of several package managers, such as Bower, npm, or NuGet.</span></span> <span data-ttu-id="2f286-114">在每个情况下，该过程是实质上是相同的：</span><span class="sxs-lookup"><span data-stu-id="2f286-114">In each case, the process is essentially the same:</span></span>

### <a name="bower"></a><span data-ttu-id="2f286-115">Bower</span><span class="sxs-lookup"><span data-stu-id="2f286-115">Bower</span></span>

```console
bower install bootstrap
```

### <a name="npm"></a><span data-ttu-id="2f286-116">npm</span><span class="sxs-lookup"><span data-stu-id="2f286-116">npm</span></span>

```console
npm install bootstrap
```

### <a name="nuget"></a><span data-ttu-id="2f286-117">NuGet</span><span class="sxs-lookup"><span data-stu-id="2f286-117">NuGet</span></span>

```console
Install-Package bootstrap
```

> [!NOTE]
> <span data-ttu-id="2f286-118">安装客户端依赖关系，如 ASP.NET Core 中的 Bootstrap 为通过 Bower 的建议的方法 (使用*bower.json*，如上所示)。</span><span class="sxs-lookup"><span data-stu-id="2f286-118">The recommended way to install client-side dependencies like Bootstrap in ASP.NET Core is via Bower (using *bower.json*, as shown above).</span></span> <span data-ttu-id="2f286-119">使用 npm/NuGet 显示来演示如何轻松地 Bootstrap 可以添加到其他类型的 web 应用程序，包括 ASP.NET 的早期版本。</span><span class="sxs-lookup"><span data-stu-id="2f286-119">The use of npm/NuGet are shown to demonstrate how easily Bootstrap can be added to other kinds of web applications, including earlier versions of ASP.NET.</span></span>

<span data-ttu-id="2f286-120">如果您要引用的 Bootstrap 您自己的本地版本，你将需要在将使用它的所有页中引用它们。</span><span class="sxs-lookup"><span data-stu-id="2f286-120">If you're referencing your own local versions of Bootstrap, you'll need to reference them in any pages that will use it.</span></span> <span data-ttu-id="2f286-121">在生产中应引用使用 CDN 的 bootstrap。</span><span class="sxs-lookup"><span data-stu-id="2f286-121">In production you should reference bootstrap using a CDN.</span></span> <span data-ttu-id="2f286-122">在默认 ASP.NET 站点模板中， *_Layout.cshtml*文件因此像这样：</span><span class="sxs-lookup"><span data-stu-id="2f286-122">In the default ASP.NET site template, the *_Layout.cshtml* file does so like this:</span></span>

[!code-html[Main](../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=9,13,51,59)]

> [!NOTE]
> <span data-ttu-id="2f286-123">如果你要使用的任何 Bootstrap 的 jQuery 插件，你将需要引用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="2f286-123">If you're going to be using any of Bootstrap's jQuery plugins, you will also need to reference jQuery.</span></span>

## <a name="basic-templates-and-features"></a><span data-ttu-id="2f286-124">基本的模板和功能</span><span class="sxs-lookup"><span data-stu-id="2f286-124">Basic templates and features</span></span>

<span data-ttu-id="2f286-125">最基本启动模板看起来非常相似*_Layout.cshtml*所示的文件更高版本，并只包括基本菜单用于导航和呈现页面的其余部分的一个位置。</span><span class="sxs-lookup"><span data-stu-id="2f286-125">The most basic Bootstrap template looks very much like the *_Layout.cshtml* file shown above, and simply includes a basic menu for navigation and a place to render the rest of the page.</span></span>

### <a name="basic-navigation"></a><span data-ttu-id="2f286-126">基本导航</span><span class="sxs-lookup"><span data-stu-id="2f286-126">Basic navigation</span></span>

<span data-ttu-id="2f286-127">默认模板使用的一组`<div>`元素来呈现顶部导航栏和页的正文。</span><span class="sxs-lookup"><span data-stu-id="2f286-127">The default template uses a set of `<div>` elements to render a top navbar and the main body of the page.</span></span> <span data-ttu-id="2f286-128">如果你使用 HTML5，则可以将第一个`<div>`使用标记`<nav>`标记来获取相同的效果，但具有更精确的语义。</span><span class="sxs-lookup"><span data-stu-id="2f286-128">If you're using HTML5, you can replace the first `<div>` tag with a `<nav>` tag to get the same effect, but with more precise semantics.</span></span> <span data-ttu-id="2f286-129">此第一部分中`<div>`可以看到有多个其他人。</span><span class="sxs-lookup"><span data-stu-id="2f286-129">Within this first `<div>` you can see there are several others.</span></span> <span data-ttu-id="2f286-130">首先，`<div>`与类的"容器"，然后在中，两个多`<div>`元素:"导航条标头"和"导航栏折叠"。</span><span class="sxs-lookup"><span data-stu-id="2f286-130">First, a `<div>` with a class of "container", and then within that, two more `<div>` elements: "navbar-header" and "navbar-collapse".</span></span> <span data-ttu-id="2f286-131">导航条标头 div 包括时一定最小宽度，显示 3 水平行下面的屏幕，将出现一个按钮 (所谓"汉堡图标")。</span><span class="sxs-lookup"><span data-stu-id="2f286-131">The navbar-header div includes a button that will appear when the screen is below a certain minimum width, showing 3 horizontal lines (a so-called "hamburger icon").</span></span> <span data-ttu-id="2f286-132">使用纯 HTML 和 CSS; 呈现图标没有图像是必需的。</span><span class="sxs-lookup"><span data-stu-id="2f286-132">The icon is rendered using pure HTML and CSS; no image is required.</span></span> <span data-ttu-id="2f286-133">这是显示的图标，与每个代码<span>标记呈现白色条之一：</span><span class="sxs-lookup"><span data-stu-id="2f286-133">This is the code that displays the icon, with each of the <span> tags rendering one of the white bars:</span></span>

```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

<span data-ttu-id="2f286-134">它还包括应用程序名称，将显示在左上角。</span><span class="sxs-lookup"><span data-stu-id="2f286-134">It also includes the application name, which appears in the top left.</span></span> <span data-ttu-id="2f286-135">由呈现的主导航菜单`<ul>`中的第二个 div 元素并包括指向链接为主页，关于，和联系人。</span><span class="sxs-lookup"><span data-stu-id="2f286-135">The main navigation menu is rendered by the `<ul>` element within the second div, and includes links to Home, About, and Contact.</span></span> <span data-ttu-id="2f286-136">通过在行 29 _LoginPartial 行添加注册和登录名的其他链接。</span><span class="sxs-lookup"><span data-stu-id="2f286-136">Additional links for Register and Login are added by the _LoginPartial line on line 29.</span></span> <span data-ttu-id="2f286-137">下面的导航窗格中，主正文中的每个页面呈现在另一个`<div>`、 标记与"容器"和"正文内容"类。</span><span class="sxs-lookup"><span data-stu-id="2f286-137">Below the navigation, the main body of each page is rendered in another `<div>`, marked with the "container" and "body-content" classes.</span></span> <span data-ttu-id="2f286-138">在此处显示简单的默认 _Layout 文件中，页的内容所呈现页面上，，然后选择一个简单与关联的特定视图`<footer>`添加到末尾`<div>`元素。</span><span class="sxs-lookup"><span data-stu-id="2f286-138">In the simple default _Layout file shown here, the contents of the page are rendered by the specific View associated with the page, and then a simple `<footer>` is added to the end of the `<div>` element.</span></span> <span data-ttu-id="2f286-139">你可以看到有关页面内置将显示使用此模板：</span><span class="sxs-lookup"><span data-stu-id="2f286-139">You can see how the built-in About page appears using this template:</span></span>

![有关页面](bootstrap/_static/about-page-wide.png)

<span data-ttu-id="2f286-141">窗口低于一定宽度时，将显示折叠的导航栏中，与在右上角，"汉堡"按钮：</span><span class="sxs-lookup"><span data-stu-id="2f286-141">The collapsed navbar, with "hamburger" button in the top right, appears when the window drops below a certain width:</span></span>

![有关与汉堡菜单的页面](bootstrap/_static/about-page-hamburger.png)

<span data-ttu-id="2f286-143">单击图标将显示从页面顶部向下滑垂直抽屉中的菜单项：</span><span class="sxs-lookup"><span data-stu-id="2f286-143">Clicking the icon reveals the menu items in a vertical drawer that slides down from the top of the page:</span></span>

![有关与汉堡菜单展开页面](bootstrap/_static/about-page-hamburger-open.png)

### <a name="typography-and-links"></a><span data-ttu-id="2f286-145">版式和链接</span><span class="sxs-lookup"><span data-stu-id="2f286-145">Typography and links</span></span>

<span data-ttu-id="2f286-146">Bootstrap 设置了站点的基本版式、 颜色和其 CSS 文件中的格式设置的链接。</span><span class="sxs-lookup"><span data-stu-id="2f286-146">Bootstrap sets up the site's basic typography, colors, and link formatting in its CSS file.</span></span> <span data-ttu-id="2f286-147">此 CSS 文件包括表、 按钮、 窗体元素、 图像和的详细信息的默认样式 ([了解](http://getbootstrap.com/css/))。</span><span class="sxs-lookup"><span data-stu-id="2f286-147">This CSS file includes default styles for tables, buttons, form elements, images, and more ([learn more](http://getbootstrap.com/css/)).</span></span> <span data-ttu-id="2f286-148">一个特别有用功能是，接下来涵盖的网格布局系统。</span><span class="sxs-lookup"><span data-stu-id="2f286-148">One particularly useful feature is the grid layout system, covered next.</span></span>

### <a name="grids"></a><span data-ttu-id="2f286-149">网格</span><span class="sxs-lookup"><span data-stu-id="2f286-149">Grids</span></span>

<span data-ttu-id="2f286-150">Bootstrap 的最流行的功能之一是其网格布局系统。</span><span class="sxs-lookup"><span data-stu-id="2f286-150">One of the most popular features of Bootstrap is its grid layout system.</span></span> <span data-ttu-id="2f286-151">现代 web 应用程序应避免使用`<table>`布局，而将此元素的用途限制为实际的表格数据的标记。</span><span class="sxs-lookup"><span data-stu-id="2f286-151">Modern web applications should avoid using the `<table>` tag for layout, instead restricting the use of this element to actual tabular data.</span></span> <span data-ttu-id="2f286-152">相反，列和行可以进行布局使用一系列`<div>`元素和相应的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="2f286-152">Instead, columns and rows can be laid out using a series of `<div>` elements and the appropriate CSS classes.</span></span> <span data-ttu-id="2f286-153">有许多好处包括能够调整以显示垂直屏幕窄，如在手机上的网格布局，这种方法。</span><span class="sxs-lookup"><span data-stu-id="2f286-153">There are several advantages to this approach, including the ability to adjust the layout of grids to display vertically on narrow screens, such as on phones.</span></span>

<span data-ttu-id="2f286-154">[Bootstrap 的网格布局系统](http://getbootstrap.com/css/#grid)基于 12 个列。</span><span class="sxs-lookup"><span data-stu-id="2f286-154">[Bootstrap's grid layout system](http://getbootstrap.com/css/#grid) is based on twelve columns.</span></span> <span data-ttu-id="2f286-155">已选择此数字，原因是可以为 1、 2、 3 或 4 列均匀划分和到之间变化的列宽可以在 1/12 的垂直屏幕的宽度。</span><span class="sxs-lookup"><span data-stu-id="2f286-155">This number was chosen because it can be divided evenly into 1, 2, 3, or 4 columns, and column widths can vary to within 1/12th of the vertical width of the screen.</span></span> <span data-ttu-id="2f286-156">若要开始使用网格布局系统，你应该开始使用容器`<div>`，然后添加行`<div>`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f286-156">To start using the grid layout system, you should begin with a container `<div>` and then add a row `<div>`, as shown here:</span></span>

```html
<div class="container">
    <div class="row">
        ...
    </div>
</div>
```

<span data-ttu-id="2f286-157">接下来，添加其他`<div>`元素为每个列，并指定的列数，`<div>`应占用 （带 12)"列-md-"开头的 CSS 类的一部分。</span><span class="sxs-lookup"><span data-stu-id="2f286-157">Next, add additional `<div>` elements for each column, and specify the number of columns that `<div>` should occupy (out of 12) as part of a CSS class starting with "col-md-".</span></span> <span data-ttu-id="2f286-158">例如，如果你想要只具有大小相等的两个列，你将为每个使用"列-md-6"的类。</span><span class="sxs-lookup"><span data-stu-id="2f286-158">For instance, if you want to simply have two columns of equal size, you would use a class of "col-md-6" for each one.</span></span> <span data-ttu-id="2f286-159">在这种情况下"md"是短，无法用于"medium"并引用标准尺寸台式计算机的显示大小。</span><span class="sxs-lookup"><span data-stu-id="2f286-159">In this case "md" is short for "medium" and refers to standard-sized desktop computer display sizes.</span></span> <span data-ttu-id="2f286-160">有四个不同选项，你可以选择从，和每个将使用更高版本的宽度除非重写 （因此，如果你想要无论屏幕宽度固定的布局，你可以只需指定 xs 类）。</span><span class="sxs-lookup"><span data-stu-id="2f286-160">There are four different options you can choose from, and each will be used for higher widths unless overridden (so if you want the layout to be fixed regardless of screen width, you can just specify xs classes).</span></span>

<span data-ttu-id="2f286-161">CSS 类前缀</span><span class="sxs-lookup"><span data-stu-id="2f286-161">CSS Class Prefix</span></span> | <span data-ttu-id="2f286-162">设备层</span><span class="sxs-lookup"><span data-stu-id="2f286-162">Device Tier</span></span> | <span data-ttu-id="2f286-163">宽度</span><span class="sxs-lookup"><span data-stu-id="2f286-163">Width</span></span>
:---: | :---: | :---:
<span data-ttu-id="2f286-164">col-xs-</span><span class="sxs-lookup"><span data-stu-id="2f286-164">col-xs-</span></span> | <span data-ttu-id="2f286-165">手机</span><span class="sxs-lookup"><span data-stu-id="2f286-165">Phones</span></span> | <span data-ttu-id="2f286-166">< 768px</span><span class="sxs-lookup"><span data-stu-id="2f286-166">< 768px</span></span>
<span data-ttu-id="2f286-167">col-sm-</span><span class="sxs-lookup"><span data-stu-id="2f286-167">col-sm-</span></span> | <span data-ttu-id="2f286-168">平板电脑</span><span class="sxs-lookup"><span data-stu-id="2f286-168">Tablets</span></span> | <span data-ttu-id="2f286-169">>= 768px</span><span class="sxs-lookup"><span data-stu-id="2f286-169">>= 768px</span></span>
<span data-ttu-id="2f286-170">col-md-</span><span class="sxs-lookup"><span data-stu-id="2f286-170">col-md-</span></span> | <span data-ttu-id="2f286-171">桌面</span><span class="sxs-lookup"><span data-stu-id="2f286-171">Desktops</span></span> | <span data-ttu-id="2f286-172">>= 992px</span><span class="sxs-lookup"><span data-stu-id="2f286-172">>= 992px</span></span>
<span data-ttu-id="2f286-173">col-lg-</span><span class="sxs-lookup"><span data-stu-id="2f286-173">col-lg-</span></span> | <span data-ttu-id="2f286-174">更大的桌面显示</span><span class="sxs-lookup"><span data-stu-id="2f286-174">Larger Desktop Displays</span></span> | <span data-ttu-id="2f286-175">>= 1200px</span><span class="sxs-lookup"><span data-stu-id="2f286-175">>= 1200px</span></span>

<span data-ttu-id="2f286-176">指定的两个列这两个"列-md-6"生成的布局中不会在桌面的解决方法的两个列，但较小的设备 （或在桌面上较窄的浏览器窗口），允许用户轻松地查看上呈现时，这两列将垂直堆叠时而无需水平滚动的内容。</span><span class="sxs-lookup"><span data-stu-id="2f286-176">When specifying two columns both with "col-md-6" the resulting layout will be two columns at desktop resolutions, but these two columns will stack vertically when rendered on smaller devices (or a narrower browser window on a desktop), allowing users to easily view content without the need to scroll horizontally.</span></span>

<span data-ttu-id="2f286-177">Bootstrap 始终默认为单列布局，以便只需指定列，如果希望多个列。</span><span class="sxs-lookup"><span data-stu-id="2f286-177">Bootstrap will always default to a single-column layout, so you only need to specify columns when you want more than one column.</span></span> <span data-ttu-id="2f286-178">你想要显式指定的唯一时间`<div>`占用所有 12 列可以重写更大的设备层的行为。</span><span class="sxs-lookup"><span data-stu-id="2f286-178">The only time you would want to explicitly specify that a `<div>` take up all 12 columns would be to override the behavior of a larger device tier.</span></span> <span data-ttu-id="2f286-179">在指定多个设备层类时，你可能需要重置在某些点列呈现。</span><span class="sxs-lookup"><span data-stu-id="2f286-179">When specifying multiple device tier classes, you may need to reset the column rendering at certain points.</span></span> <span data-ttu-id="2f286-180">添加只会显示某些视区内 clearfix div 可以实现此目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f286-180">Adding a clearfix div that's only visible within a certain viewport can achieve this, as shown here:</span></span>

![窄和宽视区网格](bootstrap/_static/narrow-and-wide-viewport-grid.png)

<span data-ttu-id="2f286-182">在上面的示例中，一个和第二个共享中行"md"布局中，而两个和第三共享"xs"布局中的行。</span><span class="sxs-lookup"><span data-stu-id="2f286-182">In the above example, One and Two share a row in the "md" layout, while Two and Three share a row in the "xs" layout.</span></span> <span data-ttu-id="2f286-183">而无需 clearfix `<div>`，2 和 3 中未显示正确的"xs"视图 （请注意，只有一个、 4 和 5 所示）：</span><span class="sxs-lookup"><span data-stu-id="2f286-183">Without the clearfix `<div>`, Two and Three are not shown correctly in the "xs" view (note that only One, Four, and Five are shown):</span></span>

![而无需使用 clearfix 网格](bootstrap/_static/grid-without-clearfix.png)

<span data-ttu-id="2f286-185">在此示例中，只有一行`<div>`所使用的并且启动仍然主要未正确的操作方面的布局和堆叠的列。</span><span class="sxs-lookup"><span data-stu-id="2f286-185">In this example, only a single row `<div>` was used, and Bootstrap still mostly did the right thing with regard to the layout and stacking of the columns.</span></span> <span data-ttu-id="2f286-186">通常情况下，应指定行`<div>`对于每个水平行布局要求，和当然可以嵌套在另一个的 Bootstrap 网格。</span><span class="sxs-lookup"><span data-stu-id="2f286-186">Typically, you should specify a row `<div>` for each horizontal row your layout requires, and of course you can nest Bootstrap grids within one another.</span></span> <span data-ttu-id="2f286-187">执行操作时，每个嵌套的网格将占用 100%的元素在其中放置它，然后可以通过使用列类细分的宽度。</span><span class="sxs-lookup"><span data-stu-id="2f286-187">When you do, each nested grid will occupy 100% of the width of the element in which it's placed, which can then be subdivided using column classes.</span></span>

### <a name="jumbotron"></a><span data-ttu-id="2f286-188">Jumbotron</span><span class="sxs-lookup"><span data-stu-id="2f286-188">Jumbotron</span></span>

<span data-ttu-id="2f286-189">如果你已使用 Visual Studio 2012 或 2013年中的默认 ASP.NET MVC 模板，你可能已了解 Jumbotron 操作中。</span><span class="sxs-lookup"><span data-stu-id="2f286-189">If you've used the default ASP.NET MVC templates in Visual Studio 2012 or 2013, you've probably seen the Jumbotron in action.</span></span> <span data-ttu-id="2f286-190">它将引用到大型全角部分可以用于显示较大的背景图像，操作、 旋转或类似的元素调用的页。</span><span class="sxs-lookup"><span data-stu-id="2f286-190">It refers to a large full-width section of a page that can be used to display a large background image, a call to action, a rotator, or similar elements.</span></span> <span data-ttu-id="2f286-191">若要添加到页面 jumbotron，只需添加`<div>`并为其提供的类"jumbotron"，然后放置容器`<div>`内并添加你的内容。</span><span class="sxs-lookup"><span data-stu-id="2f286-191">To add a jumbotron to a page, simply add a `<div>` and give it a class of "jumbotron", then place a container `<div>` inside and add your content.</span></span> <span data-ttu-id="2f286-192">我们可以轻松地调整有关页后，可以使用它显示的主要标题 jumbotron 标准：</span><span class="sxs-lookup"><span data-stu-id="2f286-192">We can easily adjust the standard About page to use a jumbotron for the main headings it displays:</span></span>

![jumbotron 示例](bootstrap/_static/jumbotron.png)

### <a name="buttons"></a><span data-ttu-id="2f286-194">按钮</span><span class="sxs-lookup"><span data-stu-id="2f286-194">Buttons</span></span>

<span data-ttu-id="2f286-195">在下图中显示的默认按钮类和它们的颜色。</span><span class="sxs-lookup"><span data-stu-id="2f286-195">The default button classes and their colors are shown in the figure below.</span></span>

![主题的按钮](bootstrap/_static/theme-buttons.png)

### <a name="badges"></a><span data-ttu-id="2f286-197">徽章</span><span class="sxs-lookup"><span data-stu-id="2f286-197">Badges</span></span>

<span data-ttu-id="2f286-198">徽章是指导航项旁边的小，通常为数值标注。</span><span class="sxs-lookup"><span data-stu-id="2f286-198">Badges refer to small, usually numeric callouts next to a navigation item.</span></span> <span data-ttu-id="2f286-199">它们可以指明大量消息或通知等待或更新的状态。</span><span class="sxs-lookup"><span data-stu-id="2f286-199">They can indicate a number of messages or notifications waiting, or the presence of updates.</span></span> <span data-ttu-id="2f286-200">指定此类徽章非常简单，只添加<span>包含文本，与"徽章"的类：</span><span class="sxs-lookup"><span data-stu-id="2f286-200">Specifying such badges is as simple as adding a <span> containing the text, with a class of "badge":</span></span>

![主题徽章](bootstrap/_static/theme-badges.png)

### <a name="alerts"></a><span data-ttu-id="2f286-202">警报</span><span class="sxs-lookup"><span data-stu-id="2f286-202">Alerts</span></span>

<span data-ttu-id="2f286-203">你可能需要向应用程序的用户显示通知、 警报或错误消息的某种类型。</span><span class="sxs-lookup"><span data-stu-id="2f286-203">You may need to display some kind of notification, alert, or error message to your application's users.</span></span> <span data-ttu-id="2f286-204">这是标准的警报类是很有用。</span><span class="sxs-lookup"><span data-stu-id="2f286-204">That's where the standard alert classes are useful.</span></span> <span data-ttu-id="2f286-205">有四个不同的严重级别与关联的颜色方案：</span><span class="sxs-lookup"><span data-stu-id="2f286-205">There are four different severity levels with associated color schemes:</span></span>

![主题的警报](bootstrap/_static/theme-alerts.png)

### <a name="navbars-and-menus"></a><span data-ttu-id="2f286-207">Navbars 和菜单</span><span class="sxs-lookup"><span data-stu-id="2f286-207">Navbars and menus</span></span>

<span data-ttu-id="2f286-208">我们布局已经包括标准的导航栏中，但是的 Bootstrap 主题支持其他样式选项。</span><span class="sxs-lookup"><span data-stu-id="2f286-208">Our layout already includes a standard navbar, but the Bootstrap theme supports additional styling options.</span></span> <span data-ttu-id="2f286-209">我们也很容易可以选择垂直显示导航栏，而不是水平如果，具有首选，以及为添加的子导航中的项弹出菜单。</span><span class="sxs-lookup"><span data-stu-id="2f286-209">We can also easily opt to display the navbar vertically rather than horizontally if that's preferred, as well as adding sub-navigation items in flyout menus.</span></span> <span data-ttu-id="2f286-210">简单导航菜单，选项卡条带，如生成的顶部</span><span class="sxs-lookup"><span data-stu-id="2f286-210">Simple navigation menus, like tab strips, are built on top of</span></span> <ul> <span data-ttu-id="2f286-211">元素。</span><span class="sxs-lookup"><span data-stu-id="2f286-211">elements.</span></span> <span data-ttu-id="2f286-212">这些内容可以创建非常只需通过只需为他们提供的 CSS 类"导航"和"导航选项卡":</span><span class="sxs-lookup"><span data-stu-id="2f286-212">These can be created very simply by just providing them with the CSS classes "nav" and "nav-tabs":</span></span>

![主题 tabstrips](bootstrap/_static/theme-tabstrips.png)

<span data-ttu-id="2f286-214">Navbars 同样，内置，但较之前更复杂。</span><span class="sxs-lookup"><span data-stu-id="2f286-214">Navbars are built similarly, but are a bit more complex.</span></span> <span data-ttu-id="2f286-215">启动时出现`<nav>`或`<div>`"导航栏"容器 div 其中包含的元素的其余部分的类。</span><span class="sxs-lookup"><span data-stu-id="2f286-215">They start with a `<nav>` or `<div>` with a class of "navbar", within which a container div holds the rest of the elements.</span></span> <span data-ttu-id="2f286-216">我们的页面导航栏在其标题中已包括 – 所示只需对此进行扩展，添加对下拉菜单中的支持：</span><span class="sxs-lookup"><span data-stu-id="2f286-216">Our page includes a navbar in its header already – the one shown below simply expands on this, adding support for a dropdown menu:</span></span>

![主题 navbars](bootstrap/_static/theme-navbars.png)

### <a name="additional-elements"></a><span data-ttu-id="2f286-218">其他元素</span><span class="sxs-lookup"><span data-stu-id="2f286-218">Additional elements</span></span>

<span data-ttu-id="2f286-219">此外可以使用默认主题在格式设置精美的样式，包括支持条带化的视图中呈现 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="2f286-219">The default theme can also be used to present HTML tables in a nicely formatted style, including support for striped views.</span></span> <span data-ttu-id="2f286-220">有类似的按钮的样式的标签。</span><span class="sxs-lookup"><span data-stu-id="2f286-220">There are labels with styles that are similar to those of the buttons.</span></span> <span data-ttu-id="2f286-221">你可以创建自定义支持的标准 HTML 之外的其他样式选项的下拉列表菜单`<select>`元素及其 Navbars 我们默认入门站点已在使用所示。</span><span class="sxs-lookup"><span data-stu-id="2f286-221">You can create custom Dropdown menus that support additional styling options beyond the standard HTML `<select>` element, along with Navbars like the one our default starter site is already using.</span></span> <span data-ttu-id="2f286-222">如果你需要一个进度栏，有几种样式可供选择，以及列出组和面板，包括标题和内容。</span><span class="sxs-lookup"><span data-stu-id="2f286-222">If you need a progress bar, there are several styles to choose from, as well as List Groups and panels that include a title and content.</span></span> <span data-ttu-id="2f286-223">浏览标准的 Bootstrap 主题中的其他选项：</span><span class="sxs-lookup"><span data-stu-id="2f286-223">Explore additional options within the standard Bootstrap Theme here:</span></span>

[<span data-ttu-id="2f286-224">http://getbootstrap.com/examples/theme/</span><span class="sxs-lookup"><span data-stu-id="2f286-224">http://getbootstrap.com/examples/theme/</span></span>](http://getbootstrap.com/examples/theme/)

## <a name="more-themes"></a><span data-ttu-id="2f286-225">更多主题</span><span class="sxs-lookup"><span data-stu-id="2f286-225">More themes</span></span>

<span data-ttu-id="2f286-226">你可以通过重写某些或所有其 CSS，扩展的标准的 Bootstrap 主题调整颜色和样式，以满足自己的应用程序的需要。</span><span class="sxs-lookup"><span data-stu-id="2f286-226">You can extend the standard Bootstrap theme by overriding some or all of its CSS, adjusting the colors and styles to suit your own application's needs.</span></span> <span data-ttu-id="2f286-227">如果你想要从头现成的主题，有几个主题库可用联机，在启动主题，例如 WrapBootstrap.com （其的各种商业主题） 和 Bootswatch.com （它提供了可用的主题） 的专用化。</span><span class="sxs-lookup"><span data-stu-id="2f286-227">If you'd like to start from a ready-made theme, there are several theme galleries available online that specialize in Bootstrap themes, such as WrapBootstrap.com (which has a variety of commercial themes) and Bootswatch.com (which offers free themes).</span></span> <span data-ttu-id="2f286-228">某些付费的可用模板提供大量之上的基本的 Bootstrap 主题，如对管理菜单和仪表板的丰富支持的功能丰富的图表和仪表。</span><span class="sxs-lookup"><span data-stu-id="2f286-228">Some of the paid templates available provide a great deal of functionality on top of the basic Bootstrap theme, such as rich support for administrative menus, and dashboards with rich charts and gauges.</span></span> <span data-ttu-id="2f286-229">常用的付费模板示例目前将 Inspinia，$18，其中包括除了 AngularJS 和静态 HTML 版本的 ASP.NET MVC5 模板的销售。</span><span class="sxs-lookup"><span data-stu-id="2f286-229">An example of a popular paid template is Inspinia, currently for sale for $18, which includes an ASP.NET MVC5 template in addition to AngularJS and static HTML versions.</span></span> <span data-ttu-id="2f286-230">示例屏幕快照所示。</span><span class="sxs-lookup"><span data-stu-id="2f286-230">A sample screenshot is shown below.</span></span>

![示例主题 inspinia](bootstrap/_static/theme-inspinia.png)

<span data-ttu-id="2f286-232">如果你想要更改您的 Bootstrap 主题，请将放*bootstrap.css*主题中所需的文件**wwwroot/css**文件夹并将更改中的引用*_Layout.cshtml*以将其指向。</span><span class="sxs-lookup"><span data-stu-id="2f286-232">If you want to change your Bootstrap theme, put the *bootstrap.css* file for the theme you want in the **wwwroot/css** folder and change the references in *_Layout.cshtml* to point it.</span></span> <span data-ttu-id="2f286-233">更改所有环境的链接：</span><span class="sxs-lookup"><span data-stu-id="2f286-233">Change the links for all environments:</span></span>

```html
<environment names="Development">
    <link rel="stylesheet" href="~/css/bootstrap.css" />
```

```html
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/bootstrap.min.css" />
```

<span data-ttu-id="2f286-234">如果你想要生成你自己的仪表板，你可以从提供的免费示例从这里开始： [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/)。</span><span class="sxs-lookup"><span data-stu-id="2f286-234">If you want to build your own dashboard, you can start from the free example available here: [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/).</span></span>

## <a name="components"></a><span data-ttu-id="2f286-235">组件数</span><span class="sxs-lookup"><span data-stu-id="2f286-235">Components</span></span>

<span data-ttu-id="2f286-236">Bootstrap 除了已经讨论了这些元素，包括对各种支持[内置 UI 组件](http://getbootstrap.com/components/)。</span><span class="sxs-lookup"><span data-stu-id="2f286-236">In addition to those elements already discussed, Bootstrap includes support for a variety of [built-in UI components](http://getbootstrap.com/components/).</span></span>

### <a name="glyphicons"></a><span data-ttu-id="2f286-237">Glyphicons</span><span class="sxs-lookup"><span data-stu-id="2f286-237">Glyphicons</span></span>

<span data-ttu-id="2f286-238">Bootstrap 包括从 Glyphicons 图标集 ([http://glyphicons.com](http://glyphicons.com))，与超过 200 个自由可用于启用 Bootstrap 的 web 应用程序中使用的图标。</span><span class="sxs-lookup"><span data-stu-id="2f286-238">Bootstrap includes icon sets from Glyphicons ([http://glyphicons.com](http://glyphicons.com)), with over 200 icons freely available for use within your Bootstrap-enabled web application.</span></span> <span data-ttu-id="2f286-239">下面是只是一个小的示例：</span><span class="sxs-lookup"><span data-stu-id="2f286-239">Here's just a small sample:</span></span>

![Glyphicons](bootstrap/_static/theme-glyphicons.png)

### <a name="input-groups"></a><span data-ttu-id="2f286-241">输入的组</span><span class="sxs-lookup"><span data-stu-id="2f286-241">Input groups</span></span>

<span data-ttu-id="2f286-242">输入的组允许绑定的附加文本或按钮使用输入元素，从而为用户提供更直观的体验：</span><span class="sxs-lookup"><span data-stu-id="2f286-242">Input groups allow bundling of additional text or buttons with an input element, providing the user with a more intuitive experience:</span></span>

![输入的组](bootstrap/_static/input-groups.png)

### <a name="breadcrumbs"></a><span data-ttu-id="2f286-244">痕迹导航</span><span class="sxs-lookup"><span data-stu-id="2f286-244">Breadcrumbs</span></span>

<span data-ttu-id="2f286-245">痕迹导航是用于显示用户，其最新历史记录或在站点的导航层次结构中的深度的常见 UI 组件。</span><span class="sxs-lookup"><span data-stu-id="2f286-245">Breadcrumbs are a common UI component used to show a user their recent history or depth within a site's navigation hierarchy.</span></span> <span data-ttu-id="2f286-246">通过将"痕迹导航"类应用于任何轻松地添加`<ol>`列表元素。</span><span class="sxs-lookup"><span data-stu-id="2f286-246">Add them easily by applying the "breadcrumb" class to any `<ol>` list element.</span></span> <span data-ttu-id="2f286-247">包括内置支持分页上使用"分页"类`<ul>`中的元素`<nav>`。</span><span class="sxs-lookup"><span data-stu-id="2f286-247">Include built-in support for pagination by using the "pagination" class on a `<ul>` element within a `<nav>`.</span></span> <span data-ttu-id="2f286-248">通过使用添加响应嵌入的幻灯片和视频`<iframe>`， `<embed>`， `<video>`，或`<object>`Bootstrap 将自动设置样式的元素。</span><span class="sxs-lookup"><span data-stu-id="2f286-248">Add responsive embedded slideshows and video by using `<iframe>`, `<embed>`, `<video>`, or `<object>` elements, which Bootstrap will style automatically.</span></span> <span data-ttu-id="2f286-249">通过使用特定的类，如"嵌入的响应性-16by9"中指定特定的纵横比。</span><span class="sxs-lookup"><span data-stu-id="2f286-249">Specify a particular aspect ratio by using specific classes like "embed-responsive-16by9".</span></span>

## <a name="javascript-support"></a><span data-ttu-id="2f286-250">JavaScript 支持</span><span class="sxs-lookup"><span data-stu-id="2f286-250">JavaScript support</span></span>

<span data-ttu-id="2f286-251">Bootstrap 的 JavaScript 库包括对包含的组件，使您可以控制其行为以编程方式在你的应用程序的 API 支持。</span><span class="sxs-lookup"><span data-stu-id="2f286-251">Bootstrap's JavaScript library includes API support for the included components, allowing you to control their behavior programmatically within your application.</span></span> <span data-ttu-id="2f286-252">此外， *bootstrap.js*包括超过 12 个自定义 jQuery 插件，提供其他功能，例如转换，模式对话框，向下滚动 （更新样式基于用户具有滚动文档中的何处） 的检测，因此，它们不会滚动出屏幕折叠到窗口的行为、 行李传送带和将附加菜单。</span><span class="sxs-lookup"><span data-stu-id="2f286-252">In addition, *bootstrap.js* includes over a dozen custom jQuery plugins, providing additional features like transitions, modal dialogs, scroll detection (updating styles based on where the user has scrolled in the document), collapse behavior, carousels, and affixing menus to the window so they don't scroll off the screen.</span></span> <span data-ttu-id="2f286-253">没有足够的空间来涵盖所有 Bootstrap – 若要了解详细信息，请访问内置的 JavaScript 外接程序[http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/)。</span><span class="sxs-lookup"><span data-stu-id="2f286-253">There's not sufficient room to cover all of the JavaScript add-ons built into Bootstrap – to learn more please visit [http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/).</span></span>

## <a name="summary"></a><span data-ttu-id="2f286-254">摘要</span><span class="sxs-lookup"><span data-stu-id="2f286-254">Summary</span></span>

<span data-ttu-id="2f286-255">Bootstrap 提供一个可用来快速和高效布局和样式各种网站和应用程序的 web 框架。</span><span class="sxs-lookup"><span data-stu-id="2f286-255">Bootstrap provides a web framework that can be used to quickly and productively lay out and style a wide variety of websites and applications.</span></span> <span data-ttu-id="2f286-256">其基本版式和样式提供通过可以手工编写或商业上购买的自定义主题支持可以容易地操作获得愉快外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="2f286-256">Its basic typography and styles provide a pleasant look and feel that can easily be manipulated through custom theme support, which can be hand-crafted or purchased commercially.</span></span> <span data-ttu-id="2f286-257">它支持的 web 组件在过去会要求昂贵的第三方控件，若要完成，同时支持现代和打开 web 标准的主机。</span><span class="sxs-lookup"><span data-stu-id="2f286-257">It supports a host of web components that in the past would've required expensive third-party controls to accomplish, while supporting modern and open web standards.</span></span>
