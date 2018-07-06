---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 移动功能 |Microsoft Docs
author: Rick-Anderson
description: 现在是通过在部署 ASP.NET MVC 5 移动 Web 应用程序在 Azure 网站的代码示例本教程的 MVC 5 版本。
ms.author: aspnetcontent
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: c852f4a853d14badb6c9a1c2c1ddb7b069bc3441
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806575"
---
<a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="a314f-103">ASP.NET MVC 4 移动功能</span><span class="sxs-lookup"><span data-stu-id="a314f-103">ASP.NET MVC 4 Mobile Features</span></span>
====================
<span data-ttu-id="a314f-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="a314f-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="a314f-105">现在没有的代码示例在本教程的 MVC 5 版本[部署 ASP.NET MVC 5 移动 Web 应用程序上 Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)。</span><span class="sxs-lookup"><span data-stu-id="a314f-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>


<span data-ttu-id="a314f-106">本教程将讲述如何使用 ASP.NET MVC 4 Web 应用程序中的移动功能的基础知识。</span><span class="sxs-lookup"><span data-stu-id="a314f-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="a314f-107">对于本教程中，可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer 或 VWD&quot;)。</span><span class="sxs-lookup"><span data-stu-id="a314f-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="a314f-108">如果已有的可以使用 Visual Studio 的专业版。</span><span class="sxs-lookup"><span data-stu-id="a314f-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="a314f-109">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="a314f-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="a314f-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （推荐） 或 Visual Studio Web Developer Express SP1。</span><span class="sxs-lookup"><span data-stu-id="a314f-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="a314f-111">Visual Studio 2012 包含 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="a314f-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="a314f-112">如果使用 Visual Web Developer 2010，则必须安装[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。</span><span class="sxs-lookup"><span data-stu-id="a314f-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="a314f-113">您还需要移动浏览器模拟器。</span><span class="sxs-lookup"><span data-stu-id="a314f-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="a314f-114">以下任何版本均可：</span><span class="sxs-lookup"><span data-stu-id="a314f-114">Any of the following will work:</span></span>

- <span data-ttu-id="a314f-115">[Windows 7 Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a314f-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="a314f-116">（这是本教程中使用的大部分屏幕快照中的仿真程序）。</span><span class="sxs-lookup"><span data-stu-id="a314f-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="a314f-117">更改用户代理字符串以模拟 iPhone。</span><span class="sxs-lookup"><span data-stu-id="a314f-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="a314f-118">请参阅[这](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)博客文章。</span><span class="sxs-lookup"><span data-stu-id="a314f-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="a314f-119">Opera Mobile Emulator</span><span class="sxs-lookup"><span data-stu-id="a314f-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="a314f-120">[Apple Safari](http://www.apple.com/safari/download/)与用户代理设置为 iPhone。</span><span class="sxs-lookup"><span data-stu-id="a314f-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="a314f-121">有关如何将 Safari 中的用户代理设置为"iPhone"的说明，请参阅[如何让 Safari 模拟 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 的博文。</span><span class="sxs-lookup"><span data-stu-id="a314f-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="a314f-122">使用 C# 源代码的 visual Studio 项目是可随附于本主题：</span><span class="sxs-lookup"><span data-stu-id="a314f-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="a314f-123">初学者项目下载</span><span class="sxs-lookup"><span data-stu-id="a314f-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="a314f-124">已完成项目下载</span><span class="sxs-lookup"><span data-stu-id="a314f-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="a314f-125">你将生成</span><span class="sxs-lookup"><span data-stu-id="a314f-125">What You'll Build</span></span>

<span data-ttu-id="a314f-126">本教程中，您将添加移动功能中提供的简单会议列表应用程序[初学者项目](https://go.microsoft.com/fwlink/?LinkId=228307)。</span><span class="sxs-lookup"><span data-stu-id="a314f-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="a314f-127">以下屏幕截图显示了完整的应用程序标记页上，如中所示[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a314f-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="a314f-128">请参阅[键盘映射为 Windows Phone 仿真程序](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)从而简化了键盘输入。</span><span class="sxs-lookup"><span data-stu-id="a314f-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="a314f-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="a314f-130">可以使用 Internet Explorer 版本 9 或 10，可通过设置开发移动应用程序的 FireFox 或 Chrome[用户代理字符串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)。</span><span class="sxs-lookup"><span data-stu-id="a314f-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="a314f-131">下图显示了已完成本教程使用模拟 iPhone 的 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="a314f-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="a314f-132">可以使用 Internet Explorer F-12 开发人员工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)来帮助调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="a314f-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="a314f-133">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="a314f-133">Skills You'll Learn</span></span>

<span data-ttu-id="a314f-134">下面是你将了解：</span><span class="sxs-lookup"><span data-stu-id="a314f-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="a314f-135">ASP.NET MVC 4 模板如何使用 HTML5`viewport`属性和自适应呈现来改善在移动设备上显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="a314f-136">如何创建移动特定视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="a314f-137">如何创建视图切换器之间移动视图与桌面应用程序的视图，允许用户切换。</span><span class="sxs-lookup"><span data-stu-id="a314f-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="a314f-138">入门</span><span class="sxs-lookup"><span data-stu-id="a314f-138">Getting Started</span></span>

<span data-ttu-id="a314f-139">下载会议列表应用程序初学者项目使用以下链接：[下载](https://go.microsoft.com/fwlink/?LinkId=228307)。</span><span class="sxs-lookup"><span data-stu-id="a314f-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="a314f-140">然后在 Windows 资源管理器中，右键单击*MvcMobile.zip*文件，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="a314f-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="a314f-141">在中**MvcMobile.zip 属性**对话框框中，选择**解除阻止**按钮。</span><span class="sxs-lookup"><span data-stu-id="a314f-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="a314f-142">(取消阻止您尝试使用的安全警告 *.zip*已从 web 下载的文件。)</span><span class="sxs-lookup"><span data-stu-id="a314f-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="a314f-144">右键单击*MvcMobile.zip*文件，然后选择**全部提取**来解压缩该文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="a314f-145">在 Visual Studio 中打开*MvcMobile.sln*文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="a314f-146">按 CTRL + F5 运行应用程序，会将其显示在桌面浏览器中。</span><span class="sxs-lookup"><span data-stu-id="a314f-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="a314f-147">启动移动浏览器模拟器，将会议应用程序的 URL 复制到模拟器，，然后单击**按标记浏览**链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="a314f-148">如果使用的 Windows Phone 仿真程序，在 URL 栏中单击，然后按暂停键来访问键盘。</span><span class="sxs-lookup"><span data-stu-id="a314f-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="a314f-149">下的图显示*AllTags*视图 (选择**按标记浏览**)。</span><span class="sxs-lookup"><span data-stu-id="a314f-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="a314f-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="a314f-151">显示为在移动设备上一目了然。</span><span class="sxs-lookup"><span data-stu-id="a314f-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="a314f-152">选择 ASP.NET 链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="a314f-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="a314f-154">ASP.NET 标签视图是显示非常混乱。</span><span class="sxs-lookup"><span data-stu-id="a314f-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="a314f-155">例如，**日期**列是很难阅读。</span><span class="sxs-lookup"><span data-stu-id="a314f-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="a314f-156">本教程的后面将创建的版本*AllTags*视图，它专门针对移动浏览器并将使显示易读。</span><span class="sxs-lookup"><span data-stu-id="a314f-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="a314f-157">注意： 目前存在一个 bug 中移动缓存引擎。</span><span class="sxs-lookup"><span data-stu-id="a314f-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="a314f-158">对于生产应用程序，必须安装[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes)有用的功能包。</span><span class="sxs-lookup"><span data-stu-id="a314f-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="a314f-159">请参阅[ASP.NET MVC 4 移动缓存 Bug 固定](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)有关解决方法的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a314f-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="a314f-160">CSS 媒体查询</span><span class="sxs-lookup"><span data-stu-id="a314f-160">CSS Media Queries</span></span>

<span data-ttu-id="a314f-161">[CSS 媒体查询](http://www.w3.org/TR/css3-mediaqueries/)CSS 媒体类型的扩展。</span><span class="sxs-lookup"><span data-stu-id="a314f-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="a314f-162">它们允许你创建重写特定浏览器 （用户代理） 的默认 CSS 规则的规则。</span><span class="sxs-lookup"><span data-stu-id="a314f-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="a314f-163">面向移动浏览器的 CSS 的通用规则定义最大屏幕尺寸。</span><span class="sxs-lookup"><span data-stu-id="a314f-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="a314f-164">*Content\Site.css*时创建新的 ASP.NET MVC 4 Internet 项目创建的文件包含以下媒体查询：</span><span class="sxs-lookup"><span data-stu-id="a314f-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="a314f-165">如果浏览器窗口为 850 像素宽或更小，它将使用在此媒体块中的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a314f-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="a314f-166">此类的 CSS 媒体查询可用于更广泛的桌面浏览器显示在设计的默认 CSS 规则比小型 （如移动浏览器） 的浏览器提供 HTML 内容的更好地显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="a314f-167">视区 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="a314f-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="a314f-168">大多数移动浏览器定义虚拟浏览器窗口宽度 (*视区*) 这是比移动设备的实际宽度大得多。</span><span class="sxs-lookup"><span data-stu-id="a314f-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="a314f-169">这样，移动浏览器以适应整个 web 页内的虚拟显示器。</span><span class="sxs-lookup"><span data-stu-id="a314f-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="a314f-170">用户然后可以放大有趣的内容。</span><span class="sxs-lookup"><span data-stu-id="a314f-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="a314f-171">但是，如果视区宽度设置为实际设备宽度时，没有缩放是必需的因为内容适应移动浏览器中。</span><span class="sxs-lookup"><span data-stu-id="a314f-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="a314f-172">在视区`<meta>`ASP.NET MVC 4 布局文件中的标记将视区设置为设备宽。</span><span class="sxs-lookup"><span data-stu-id="a314f-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="a314f-173">以下行显示在视区`<meta>`ASP.NET MVC 4 布局文件中的标记。</span><span class="sxs-lookup"><span data-stu-id="a314f-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="a314f-174">检查 CSS 媒体查询和视区 Meta 标记的效果</span><span class="sxs-lookup"><span data-stu-id="a314f-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="a314f-175">打开*views/shared\\_Layout.cshtml*编辑器并注释掉视区中的文件`<meta>`标记。</span><span class="sxs-lookup"><span data-stu-id="a314f-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="a314f-176">以下标记显示了注释掉的行。</span><span class="sxs-lookup"><span data-stu-id="a314f-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="a314f-177">打开*MvcMobile\Content\Site.css*文件在编辑器中，并将媒体查询中的最大宽度更改为零像素。</span><span class="sxs-lookup"><span data-stu-id="a314f-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="a314f-178">这将防止在移动浏览器中使用的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="a314f-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="a314f-179">以下行显示了修改后的媒体查询：</span><span class="sxs-lookup"><span data-stu-id="a314f-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="a314f-180">保存所做的更改并浏览到移动浏览器模拟器中的会议应用程序。</span><span class="sxs-lookup"><span data-stu-id="a314f-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="a314f-181">在下图中的小文本是删除在视区的结果`<meta>`标记。</span><span class="sxs-lookup"><span data-stu-id="a314f-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="a314f-182">使用没有视区`<meta>`标记，在浏览器时将缩小为默认值视区宽度 (850 像素或宽为大多数移动浏览器。)</span><span class="sxs-lookup"><span data-stu-id="a314f-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="a314f-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="a314f-184">撤消所做的更改，取消注释在视区`<meta>`布局文件中标记并还原为 850 像素中的媒体查询*Site.css*文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="a314f-185">保存所做的更改并刷新移动浏览器中，若要验证已还原适合移动应用显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="a314f-186">在视区`<meta>`标记和 CSS 媒体查询不特定于 ASP.NET MVC 4 中，而您可以在任何 web 应用程序中充分利用这些功能。</span><span class="sxs-lookup"><span data-stu-id="a314f-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="a314f-187">但现在被内置到您创建新的 ASP.NET MVC 4 项目时，将生成的文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="a314f-188">有关视区的详细信息`<meta>`标记中，请参阅[神奇的两个视区 — 第二部分](http://www.quirksmode.org/mobile/viewports2.html)。</span><span class="sxs-lookup"><span data-stu-id="a314f-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="a314f-189">下一节中您将了解如何提供移动浏览器特定视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="a314f-190">重写视图、 布局和分部视图</span><span class="sxs-lookup"><span data-stu-id="a314f-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="a314f-191">在 ASP.NET MVC 4 中的一个重要新功能是针对移动浏览器一般情况下，为单个移动浏览器，或用于任何特定浏览器允许您重写任何视图 （包括布局和分部视图） 的简单机制。</span><span class="sxs-lookup"><span data-stu-id="a314f-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="a314f-192">若要提供移动特定视图，可以复制视图文件并添加 *。移动*到的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="a314f-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="a314f-193">例如，若要创建移动*索引*视图中，复制*Views\Home\Index.cshtml*到*Views\Home\Index.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="a314f-194">在本部分中，将创建一个移动特定布局文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="a314f-195">若要开始，请将复制*views/shared\\_Layout.cshtml*到*views/shared\\_Layout.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="a314f-196">打开 *\_Layout.Mobile.cshtml*并将更改从标题**MVC4 Conference**到**Conference (Mobile)**。</span><span class="sxs-lookup"><span data-stu-id="a314f-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="a314f-197">在每个`Html.ActionLink`调用中，删除"浏览者"中的每个链接*ActionLink*。</span><span class="sxs-lookup"><span data-stu-id="a314f-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="a314f-198">下面的代码显示移动布局文件的已完成的正文部分。</span><span class="sxs-lookup"><span data-stu-id="a314f-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="a314f-199">复制*Views\Home\AllTags.cshtml*的文件*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="a314f-200">打开新文件并更改`<h2>`元素从"Tags"到"Tags (M)":</span><span class="sxs-lookup"><span data-stu-id="a314f-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="a314f-201">浏览到标签页使用桌面浏览器和移动浏览器模拟器。</span><span class="sxs-lookup"><span data-stu-id="a314f-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="a314f-202">移动浏览器模拟器显示你所做的两个更改。</span><span class="sxs-lookup"><span data-stu-id="a314f-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="a314f-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="a314f-204">与此相反，桌面显示并未变化。</span><span class="sxs-lookup"><span data-stu-id="a314f-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="a314f-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="a314f-206">特定于浏览器视图</span><span class="sxs-lookup"><span data-stu-id="a314f-206">Browser-Specific Views</span></span>

<span data-ttu-id="a314f-207">除了移动特定和特定于桌面的视图中，可以创建单个浏览器的视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="a314f-208">例如，您可以创建专门针对 iPhone 浏览器的视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="a314f-209">在本部分中，您将创建为 iPhone 浏览器和 iPhone 版本的布局*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="a314f-210">打开*Global.asax*文件，并将以下代码添加到`Application_Start`方法。</span><span class="sxs-lookup"><span data-stu-id="a314f-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="a314f-211">此代码定义名为"iPhone"，将针对每个传入请求匹配的新显示模式。</span><span class="sxs-lookup"><span data-stu-id="a314f-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="a314f-212">如果传入请求与定义 （即，如果用户代理包含字符串"iPhone"） 的条件相匹配，ASP.NET MVC 将查找名称中包含"iPhone"后缀的视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="a314f-213">在代码中，右键单击`DefaultDisplayMode`，选择**解决**，然后选择`using System.Web.WebPages;`。</span><span class="sxs-lookup"><span data-stu-id="a314f-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="a314f-214">这会添加对的引用`System.Web.WebPages`命名空间，它正是`DisplayModes`和`DefaultDisplayMode`类型定义。</span><span class="sxs-lookup"><span data-stu-id="a314f-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="a314f-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="a314f-216">或者，只需手动添加以下行将对`using`文件部分。</span><span class="sxs-lookup"><span data-stu-id="a314f-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="a314f-217">完整内容*Global.asax*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="a314f-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="a314f-218">保存更改。</span><span class="sxs-lookup"><span data-stu-id="a314f-218">Save the changes.</span></span> <span data-ttu-id="a314f-219">复制*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*的文件*MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="a314f-220">打开新文件，然后将更改`h1`从标题`Conference (Mobile)`到`Conference (iPhone)`。</span><span class="sxs-lookup"><span data-stu-id="a314f-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="a314f-221">复制*MvcMobile\Views\Home\AllTags.Mobile.cshtml*的文件*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="a314f-222">在新的文件中，更改`<h2>`元素从"Tags (M)"为"Tags (iPhone)"。</span><span class="sxs-lookup"><span data-stu-id="a314f-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="a314f-223">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="a314f-223">Run the application.</span></span> <span data-ttu-id="a314f-224">运行移动浏览器模拟器，请确保其用户代理设置为"iPhone"，并浏览到*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="a314f-225">以下屏幕截图显示*AllTags*视图中呈现[Safari](http://www.apple.com/safari/download/)浏览器。</span><span class="sxs-lookup"><span data-stu-id="a314f-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="a314f-226">您可以下载有关 Windows Safari[此处](https://support.apple.com/kb/DL1531)。</span><span class="sxs-lookup"><span data-stu-id="a314f-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="a314f-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="a314f-228">在本部分中我们已了解如何创建移动布局和视图以及如何创建布局和用于特定设备，例如 iPhone 视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="a314f-229">下一节中您将了解如何利用 jQuery Mobile 的多个极具吸引力的移动视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="a314f-230">使用 jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="a314f-230">Using jQuery Mobile</span></span>

<span data-ttu-id="a314f-231">[的 jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)库提供了适用于所有主要移动浏览器用户界面框架。</span><span class="sxs-lookup"><span data-stu-id="a314f-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="a314f-232">jQuery Mobile 适用*渐进式增强*对支持 CSS 和 JavaScript 的移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a314f-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="a314f-233">渐进增强允许所有浏览器显示网页的基本内容，同时允许更强大的浏览器和设备拥有更丰富的显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="a314f-234">附带的 jQuery Mobile 的 JavaScript 和 CSS 文件的样式来适应移动浏览器，无需对标记做任何更改的许多元素。</span><span class="sxs-lookup"><span data-stu-id="a314f-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="a314f-235">在本部分中，你将安装*jQuery.Mobile.MVC* NuGet 包，可安装 jQuery Mobile 和视图切换器小组件。</span><span class="sxs-lookup"><span data-stu-id="a314f-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="a314f-236">若要开始，删除*共享\\_Layout.Mobile.cshtml*并*共享\\_Layout.iPhone.cshtml*前面创建的文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="a314f-237">重命名*Views\Home\AllTags.Mobile.cshtml*并*Views\Home\AllTags.iPhone.cshtml*文件到*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。</span><span class="sxs-lookup"><span data-stu-id="a314f-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="a314f-238">因为文件不再具有 *.cshtml*扩展，它们不会用于 ASP.NET MVC 运行时呈现*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="a314f-239">安装*jQuery.Mobile.MVC* NuGet 包通过执行此操作：</span><span class="sxs-lookup"><span data-stu-id="a314f-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="a314f-240">从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="a314f-240">From the **Tools** menu, select **Library Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="a314f-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="a314f-242">在中**程序包管理器控制台**，输入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="a314f-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="a314f-243">下图显示了添加和更改到 MvcMobile 项目 jQuery.Mobile.MVC NuGet 包的文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="a314f-244">[添加] 追加的文件的名称后添加的文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="a314f-245">图像不会显示 GIF 和 PNG 文件添加到*Content\images*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a314f-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="a314f-246">JQuery.Mobile.MVC NuGet 程序包将安装以下：</span><span class="sxs-lookup"><span data-stu-id="a314f-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="a314f-247">*应用程序\_Start\BundleMobileConfig.cs*文件，该引用添加的 jQuery JavaScript 和 CSS 文件所需文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="a314f-248">必须按照下面的说明并引用该文件中定义的移动捆绑。</span><span class="sxs-lookup"><span data-stu-id="a314f-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="a314f-249">jQuery Mobile CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="a314f-250">一个`ViewSwitcher`控制器小组件 (*Controllers\ViewSwitcherController.cs*)。</span><span class="sxs-lookup"><span data-stu-id="a314f-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="a314f-251">jQuery Mobile JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="a314f-252">JQuery Mobile 样式的布局文件 (*views/shared\\_Layout.Mobile.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="a314f-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="a314f-253">视图切换器分部视图 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*)，它提供要从桌面视图，反之亦然和移动视图切换每个页面顶部的链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="a314f-254">多个<em>.png</em>并<em>.gif</em>图像中的文件<em>Content\images</em>文件夹。</span><span class="sxs-lookup"><span data-stu-id="a314f-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="a314f-255">打开*Global.asax*文件，并添加以下代码的最后一行作为`Application_Start`方法。</span><span class="sxs-lookup"><span data-stu-id="a314f-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="a314f-256">下面的代码演示的完整*Global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="a314f-257">如果使用 Internet Explorer 9，并且未看到`BundleMobileConfig`黄色突出显示上面一行中，单击[兼容性视图按钮](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![（关闭） 的兼容性视图按钮的图片](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "（关闭） 的兼容性视图按钮的图片")在 IE 中来使图标更改大纲![（关闭） 的兼容性视图按钮的图片](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "（关闭） 的兼容性视图按钮的图片")为纯色![（上） 的兼容性视图按钮的图片](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "（上） 的兼容性视图按钮的图片")。</span><span class="sxs-lookup"><span data-stu-id="a314f-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="a314f-258">另外，还可以在 FireFox 或 Chrome 中查看本教程。</span><span class="sxs-lookup"><span data-stu-id="a314f-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>


<span data-ttu-id="a314f-259">打开*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*文件，并添加以下标记直接后的`Html.Partial`调用：</span><span class="sxs-lookup"><span data-stu-id="a314f-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="a314f-260">完整*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="a314f-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="a314f-261">生成应用程序，并在移动浏览器模拟器浏览到*AllTags*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="a314f-262">你看到以下信息：</span><span class="sxs-lookup"><span data-stu-id="a314f-262">You see the following:</span></span>

<span data-ttu-id="a314f-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="a314f-264">您可以调试移动特定代码通过[将用户代理字符串设置](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)对于 IE 或 Chrome 到 iPhone，然后使用 F-12 开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="a314f-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="a314f-265">如果在移动浏览器不会显示**主页**，**演讲者**，**标记**，以及**日期**链接，为按钮、 对 jQuery Mobile 的引用脚本和 CSS 文件可能不会正确。</span><span class="sxs-lookup"><span data-stu-id="a314f-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>


<span data-ttu-id="a314f-266">除了样式发生改变，则请参阅**显示移动视图**以及允许您从移动视图切换到桌面视图的链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="a314f-267">选择**桌面视图**显示链接和桌面视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="a314f-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="a314f-269">桌面视图不提供一种方法来直接导航回移动视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="a314f-270">你将立即解决的问题。</span><span class="sxs-lookup"><span data-stu-id="a314f-270">You'll fix that now.</span></span> <span data-ttu-id="a314f-271">打开*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="a314f-272">只需在页面下`body`元素中，添加以下代码来呈现视图切换器小组件：</span><span class="sxs-lookup"><span data-stu-id="a314f-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="a314f-273">刷新*AllTags*移动浏览器中的视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="a314f-274">你现在可以桌面和移动视图间导航。</span><span class="sxs-lookup"><span data-stu-id="a314f-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="a314f-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="a314f-276">调试注意： 您可以将以下代码添加到 views/shared 末尾\\_ViewSwitcher.cshtml 来帮助调试视图时使用的浏览器用户代理字符串设置为移动设备。</span><span class="sxs-lookup"><span data-stu-id="a314f-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
> 
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
> 
>  <span data-ttu-id="a314f-277">并添加以下发往*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="a314f-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>  
> 
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


<span data-ttu-id="a314f-278">浏览到*AllTags*桌面浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="a314f-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="a314f-279">视图切换器小组件不在桌面浏览器中显示，因为它仅添加到了移动布局页面。</span><span class="sxs-lookup"><span data-stu-id="a314f-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="a314f-280">本教程的后面将看到如何将视图切换器小组件添加到桌面视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="a314f-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="a314f-282">改进发言人列表</span><span class="sxs-lookup"><span data-stu-id="a314f-282">Improving the Speakers List</span></span>

<span data-ttu-id="a314f-283">在移动浏览器中，选择**扬声器**链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="a314f-284">因为没有移动视图 (*AllSpeakers.Mobile.cshtml*)，默认发言人 (*AllSpeakers.cshtml*) 使用移动布局视图呈现 ( *\_Layout.Mobile.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="a314f-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="a314f-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="a314f-286">您可以通过设置全局禁止默认 （非移动） 视图在移动布局内呈现`RequireConsistentDisplayMode`到`true`中*视图\\_ViewStart.cshtml*文件，如下：</span><span class="sxs-lookup"><span data-stu-id="a314f-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="a314f-287">当`RequireConsistentDisplayMode`设置为`true`，移动布局 (<em>\_Layout.Mobile.cshtml</em>) 只用于移动视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="a314f-288">(即，视图文件仅在窗体<em>* * ViewName</em><em>。Mobile.cshtml</em>。)你可能想要设置`RequireConsistentDisplayMode`到`true`如果你的移动布局不太适合你的非移动视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-288">(That is, the view file is of the form <em>**ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="a314f-289">以下屏幕截图显示了如何<em>扬声器</em>呈现页面时`RequireConsistentDisplayMode`设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="a314f-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="a314f-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="a314f-291">可以通过设置禁用视图中一致的显示模式`RequireConsistentDisplayMode`到`false`视图文件中。</span><span class="sxs-lookup"><span data-stu-id="a314f-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="a314f-292">中的以下标记*Views\Home\AllSpeakers.cshtml*文件中设置`RequireConsistentDisplayMode`到`false`:</span><span class="sxs-lookup"><span data-stu-id="a314f-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="a314f-293">创建移动发言人视图</span><span class="sxs-lookup"><span data-stu-id="a314f-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="a314f-294">正如您刚才看到*扬声器*视图虽然可读，但链接字迹小，不易在移动设备上点击。</span><span class="sxs-lookup"><span data-stu-id="a314f-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="a314f-295">在本部分中，您将创建一个移动特定*扬声器*视图看起来像一个现代移动应用程序 — 字迹大、 易于点击链接，而且包含可快速查找发言人的搜索框。</span><span class="sxs-lookup"><span data-stu-id="a314f-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="a314f-296">复制*AllSpeakers.cshtml*到*AllSpeakers.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="a314f-297">打开*AllSpeakers.Mobile.cshtml*文件，移除`<h2>`标题元素。</span><span class="sxs-lookup"><span data-stu-id="a314f-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="a314f-298">在中`<ul>`标记中，添加`data-role`属性，并将其值设置为`listview`。</span><span class="sxs-lookup"><span data-stu-id="a314f-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="a314f-299">像其他[`data-*`特性](http://html5doctor.com/html5-custom-data-attributes/)，`data-role="listview"`使大型列表项更易于点击。</span><span class="sxs-lookup"><span data-stu-id="a314f-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="a314f-300">这是完成的标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="a314f-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="a314f-301">刷新移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a314f-301">Refresh the mobile browser.</span></span> <span data-ttu-id="a314f-302">更新的视图如下所示：</span><span class="sxs-lookup"><span data-stu-id="a314f-302">The updated view looks like this:</span></span>

<span data-ttu-id="a314f-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="a314f-304">尽管移动视图得到了改进，但很难导航长的发言人列表。</span><span class="sxs-lookup"><span data-stu-id="a314f-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="a314f-305">若要解决此问题，在`<ul>`标记中，添加`data-filter`属性，并将其设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="a314f-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="a314f-306">下面的代码显示`ul`标记。</span><span class="sxs-lookup"><span data-stu-id="a314f-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="a314f-307">下图显示了在得到的页面顶部的搜索筛选器框`data-filter`属性。</span><span class="sxs-lookup"><span data-stu-id="a314f-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="a314f-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="a314f-309">在搜索框中键入每个字母，jQuery Mobile 将筛选显示的列表，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="a314f-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="a314f-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="a314f-311">改进标签列表</span><span class="sxs-lookup"><span data-stu-id="a314f-311">Improving the Tags List</span></span>

<span data-ttu-id="a314f-312">类似于默认*扬声器*视图中，*标记*视图虽然可读，但链接字迹小，不易在移动设备上点击。</span><span class="sxs-lookup"><span data-stu-id="a314f-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="a314f-313">在本部分中，需要修复*标记*视图相同的方式已修复*扬声器*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="a314f-314">删除&quot;隐藏&quot;后缀*Views\Home\AllTags.Mobile.cshtml.hide*文件，这样的名称是*Views\Home\AllTags.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="a314f-315">打开重命名的文件，移除`<h2>`元素。</span><span class="sxs-lookup"><span data-stu-id="a314f-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="a314f-316">添加`data-role`并`data-filter`属性到`<ul>`标签，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a314f-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="a314f-317">下图显示了标记页上筛选字母`J`。</span><span class="sxs-lookup"><span data-stu-id="a314f-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="a314f-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="a314f-319">改进日期列表</span><span class="sxs-lookup"><span data-stu-id="a314f-319">Improving the Dates List</span></span>

<span data-ttu-id="a314f-320">可以提高*日期*查看像改进*扬声器*并*标记*视图，以便更轻松地在移动设备上使用。</span><span class="sxs-lookup"><span data-stu-id="a314f-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="a314f-321">复制*Views\Home\AllDates.cshtml*的文件*Views\Home\AllDates.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a314f-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="a314f-322">打开新文件，移除`<h2>`元素。</span><span class="sxs-lookup"><span data-stu-id="a314f-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="a314f-323">添加`data-role="listview"`到`<ul>`标记，如下：</span><span class="sxs-lookup"><span data-stu-id="a314f-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="a314f-324">下图显示了什么**日期**页面的外观`data-role`添加属性。</span><span class="sxs-lookup"><span data-stu-id="a314f-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="a314f-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)的内容替换为*Views\Home\AllDates.Mobile.cshtml*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="a314f-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="a314f-326">此代码按日期分组的所有会话。</span><span class="sxs-lookup"><span data-stu-id="a314f-326">This code groups all sessions by days.</span></span> <span data-ttu-id="a314f-327">它为每个新日期创建的列表分隔符，并列出的下一个分隔线的每一天的所有会话。</span><span class="sxs-lookup"><span data-stu-id="a314f-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="a314f-328">下面是当此代码运行如下所示：</span><span class="sxs-lookup"><span data-stu-id="a314f-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="a314f-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="a314f-330">改进 SessionsTable 视图</span><span class="sxs-lookup"><span data-stu-id="a314f-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="a314f-331">在本部分中，将创建一个移动特定的会话视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="a314f-332">我们做的更改将比在我们创建的其他视图中更广泛。</span><span class="sxs-lookup"><span data-stu-id="a314f-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="a314f-333">在移动浏览器中，点击**演讲者**按钮，然后输入`Sc`在搜索框中。</span><span class="sxs-lookup"><span data-stu-id="a314f-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="a314f-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="a314f-335">点击**Scott Hanselman**链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="a314f-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="a314f-337">正如您所看到的很难读取在移动浏览器显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="a314f-338">日期列难以阅读和标签列也超出了视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="a314f-339">若要解决此问题，将复制*Views\Home\SessionsTable.cshtml*到*Views\Home\SessionsTable.Mobile.cshtml*，然后使用以下代码替换文件的内容：</span><span class="sxs-lookup"><span data-stu-id="a314f-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="a314f-340">该代码移除了 room 和 tag 列，然后竖式标题、 发言人和日期，以便在移动浏览器中阅读所有此类信息。</span><span class="sxs-lookup"><span data-stu-id="a314f-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="a314f-341">下图反映了代码更改。</span><span class="sxs-lookup"><span data-stu-id="a314f-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="a314f-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="a314f-343">改进 SessionByCode 视图</span><span class="sxs-lookup"><span data-stu-id="a314f-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="a314f-344">最后，将创建一个移动特定的视图*SessionByCode*视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="a314f-345">在移动浏览器中，点击**演讲者**按钮，然后输入`Sc`在搜索框中。</span><span class="sxs-lookup"><span data-stu-id="a314f-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="a314f-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="a314f-347">点击**Scott Hanselman**链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="a314f-348">将显示 Scott Hanselman 的会话。</span><span class="sxs-lookup"><span data-stu-id="a314f-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="a314f-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="a314f-350">选择**An Overview of MS Web Stack of Love**链接。</span><span class="sxs-lookup"><span data-stu-id="a314f-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="a314f-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="a314f-352">默认桌面视图虽然不错，但仍可以改进。</span><span class="sxs-lookup"><span data-stu-id="a314f-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="a314f-353">复制*Views\Home\SessionByCode.cshtml*到*Views\Home\SessionByCode.Mobile.cshtml*的内容替换为和*Views\Home\SessionByCode.Mobile.cshtml*文件使用以下标记：</span><span class="sxs-lookup"><span data-stu-id="a314f-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="a314f-354">新的标记使用`data-role`属性改进视图的布局。</span><span class="sxs-lookup"><span data-stu-id="a314f-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="a314f-355">刷新移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a314f-355">Refresh the mobile browser.</span></span> <span data-ttu-id="a314f-356">下图反映你刚才所做的代码更改：</span><span class="sxs-lookup"><span data-stu-id="a314f-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="a314f-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="a314f-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="a314f-358">便捷和评审</span><span class="sxs-lookup"><span data-stu-id="a314f-358">Wrapup and Review</span></span>

<span data-ttu-id="a314f-359">本教程已介绍了 ASP.NET MVC 4 开发者预览版的新移动功能。</span><span class="sxs-lookup"><span data-stu-id="a314f-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="a314f-360">移动功能包括：</span><span class="sxs-lookup"><span data-stu-id="a314f-360">The mobile features include:</span></span>

- <span data-ttu-id="a314f-361">能够在全局以及针对单个视图重写布局、 视图和分部视图。</span><span class="sxs-lookup"><span data-stu-id="a314f-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="a314f-362">控制布局和分部重写强制使用`RequireConsistentDisplayMode`属性。</span><span class="sxs-lookup"><span data-stu-id="a314f-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="a314f-363">移动视图切换器小组件视图比还可以在桌面视图中显示。</span><span class="sxs-lookup"><span data-stu-id="a314f-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="a314f-364">支持特定浏览器，如 iPhone 浏览器的支持。</span><span class="sxs-lookup"><span data-stu-id="a314f-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="a314f-365">请参阅</span><span class="sxs-lookup"><span data-stu-id="a314f-365">See Also</span></span>

- <span data-ttu-id="a314f-366">[jQuery Mobile](http://jquerymobile.com)站点。</span><span class="sxs-lookup"><span data-stu-id="a314f-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="a314f-367">jQuery Mobile 概述</span><span class="sxs-lookup"><span data-stu-id="a314f-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="a314f-368">W3C 建议移动 Web 应用程序的最佳做法</span><span class="sxs-lookup"><span data-stu-id="a314f-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="a314f-369">用于媒体查询的 W3C 候选建议</span><span class="sxs-lookup"><span data-stu-id="a314f-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
