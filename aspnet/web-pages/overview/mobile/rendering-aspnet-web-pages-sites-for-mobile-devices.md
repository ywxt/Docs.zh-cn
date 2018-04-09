---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 呈现 ASP.NET Web 页 (Razor) 站点对于移动设备 |Microsoft 文档
author: tfitzmac
description: 本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web 页 (Razor) 站点中创建页面。 你将了解： 你如何...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: 641798c5b835be959d02dd0d854b61ca21d83016
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="a7039-104">移动设备的的呈现 ASP.NET Web 页 (Razor) 站点</span><span class="sxs-lookup"><span data-stu-id="a7039-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>
====================
<span data-ttu-id="a7039-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a7039-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a7039-106">本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web 页 (Razor) 站点中创建页面。</span><span class="sxs-lookup"><span data-stu-id="a7039-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="a7039-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="a7039-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a7039-108">如何使用命名约定指定页专为移动设备设计。</span><span class="sxs-lookup"><span data-stu-id="a7039-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a7039-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a7039-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a7039-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="a7039-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="a7039-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="a7039-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="a7039-112">ASP.NET Web 页中，可以在移动或其他设备上创建自定义呈现内容的显示。</span><span class="sxs-lookup"><span data-stu-id="a7039-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="a7039-113">在 ASP.NET Web Pages 站点中创建设备特定的页上的最简单方法是使用如下的文件命名模式： <em>FileName。</em><em>移动</em><em>.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="a7039-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: <em>FileName.</em><em>Mobile</em><em>.cshtml</em>.</span></span> <span data-ttu-id="a7039-114">你可以创建两个版本的页面 (例如，一个名为<em>MyFile.cshtml</em>和一个名为<em>MyFile.Mobile.cshtml</em>)。</span><span class="sxs-lookup"><span data-stu-id="a7039-114">You can create two versions of a page (for example, one named <em>MyFile.cshtml</em> and one named <em>MyFile.Mobile.cshtml</em>).</span></span> <span data-ttu-id="a7039-115">在运行的时，当移动设备请求<em>MyFile.cshtml</em>，ASP.NET 将从内容呈现<em>MyFile.Mobile.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="a7039-115">At run time, when a mobile device requests <em>MyFile.cshtml</em>, ASP.NET renders the content from <em>MyFile.Mobile.cshtml</em>.</span></span> <span data-ttu-id="a7039-116">否则为<em>MyFile.cshtml</em>呈现。</span><span class="sxs-lookup"><span data-stu-id="a7039-116">Otherwise, <em>MyFile.cshtml</em> is rendered.</span></span>

<span data-ttu-id="a7039-117">下面的示例演示如何通过添加移动设备的内容页中启用移动呈现。</span><span class="sxs-lookup"><span data-stu-id="a7039-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="a7039-118">*Page1.cshtml*包含内容以及导航侧边栏。</span><span class="sxs-lookup"><span data-stu-id="a7039-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="a7039-119">*Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。</span><span class="sxs-lookup"><span data-stu-id="a7039-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="a7039-120">在 ASP.NET Web Pages 站点中，创建名为的文件*Page1.cshtml*并将当前的内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="a7039-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="a7039-121">创建名为的文件*Page1.Mobile.cshtml*并将现有内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="a7039-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="a7039-122">请注意该页面的移动版本省略更好地呈现较小屏幕上的导航部分。</span><span class="sxs-lookup"><span data-stu-id="a7039-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="a7039-123">运行桌面浏览器并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a7039-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="a7039-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a7039-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="a7039-125">运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a7039-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="a7039-126">(请注意，不包括*.mobile。*</span><span class="sxs-lookup"><span data-stu-id="a7039-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="a7039-127">作为 URL 的一部分。）即使该请求是*Page1.cshtml*，ASP.NET 呈现*Page1.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a7039-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="a7039-129">若要测试移动页，可以使用在台式计算机运行的移动设备模拟器。</span><span class="sxs-lookup"><span data-stu-id="a7039-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="a7039-130">此工具允许你测试 web 页面，因为它们将显示在移动设备上 （即，通常通过小得多显示区域）。</span><span class="sxs-lookup"><span data-stu-id="a7039-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="a7039-131">模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)对 Mozilla Firefox，它可让你模拟从桌面版本的 Firefox 的各种移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="a7039-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a7039-132">其他资源</span><span class="sxs-lookup"><span data-stu-id="a7039-132">Additional Resources</span></span>


<span data-ttu-id="a7039-133">[Windows Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="a7039-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
