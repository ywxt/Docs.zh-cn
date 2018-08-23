---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 为移动设备呈现 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。 你将学习： 您如何...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: 7159283efcd4a82d5dff68f2d9e315f804e7cdcb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832259"
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="ea966-104">为移动设备呈现 ASP.NET Web Pages (Razor) 站点</span><span class="sxs-lookup"><span data-stu-id="ea966-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>
====================
<span data-ttu-id="ea966-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ea966-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ea966-106">本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。</span><span class="sxs-lookup"><span data-stu-id="ea966-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="ea966-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="ea966-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ea966-108">如何使用命名约定指定页专为移动设备。</span><span class="sxs-lookup"><span data-stu-id="ea966-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ea966-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ea966-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ea966-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="ea966-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="ea966-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="ea966-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="ea966-112">ASP.NET Web Pages 中，可以移动或其他设备上创建自定义呈现内容的显示。</span><span class="sxs-lookup"><span data-stu-id="ea966-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="ea966-113">在 ASP.NET Web Pages 站点中创建特定于设备的页面的最简单方法是使用此类文件命名模式：<em>文件名。</em><em>Mobile</em><em>.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="ea966-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: <em>FileName.</em><em>Mobile</em><em>.cshtml</em>.</span></span> <span data-ttu-id="ea966-114">可以创建两个版本的页面 (例如，一个名为<em>MyFile.cshtml</em>另一个名为<em>MyFile.Mobile.cshtml</em>)。</span><span class="sxs-lookup"><span data-stu-id="ea966-114">You can create two versions of a page (for example, one named <em>MyFile.cshtml</em> and one named <em>MyFile.Mobile.cshtml</em>).</span></span> <span data-ttu-id="ea966-115">在运行的时，移动设备的请求时<em>MyFile.cshtml</em>，ASP.NET 将从内容呈现<em>MyFile.Mobile.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="ea966-115">At run time, when a mobile device requests <em>MyFile.cshtml</em>, ASP.NET renders the content from <em>MyFile.Mobile.cshtml</em>.</span></span> <span data-ttu-id="ea966-116">否则为<em>MyFile.cshtml</em>呈现。</span><span class="sxs-lookup"><span data-stu-id="ea966-116">Otherwise, <em>MyFile.cshtml</em> is rendered.</span></span>

<span data-ttu-id="ea966-117">下面的示例演示如何通过添加内容页的移动设备启用移动呈现。</span><span class="sxs-lookup"><span data-stu-id="ea966-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="ea966-118">*Page1.cshtml*包含内容，以及导航侧边栏。</span><span class="sxs-lookup"><span data-stu-id="ea966-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="ea966-119">*Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。</span><span class="sxs-lookup"><span data-stu-id="ea966-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="ea966-120">在 ASP.NET Web Pages 站点中，创建名为的文件*Page1.cshtml*和当前的内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="ea966-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="ea966-121">创建名为的文件*Page1.Mobile.cshtml*和现有内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="ea966-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="ea966-122">请注意，页上的移动版本省略以便更好地呈现在较小屏幕上的导航部分。</span><span class="sxs-lookup"><span data-stu-id="ea966-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="ea966-123">运行桌面浏览器并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="ea966-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="ea966-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ea966-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="ea966-125">运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="ea966-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="ea966-126">(请注意，不包括 *.mobile。*</span><span class="sxs-lookup"><span data-stu-id="ea966-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="ea966-127">作为 URL 的一部分。）即使该请求是对*Page1.cshtml*，ASP.NET 会将*Page1.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="ea966-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="ea966-129">若要测试移动页面，可以使用在桌面计算机运行的移动设备模拟器。</span><span class="sxs-lookup"><span data-stu-id="ea966-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="ea966-130">此工具允许您测试网页，如他们的移动设备上的外观 （即，通常使用小得多显示区域）。</span><span class="sxs-lookup"><span data-stu-id="ea966-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="ea966-131">模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)Mozilla firefox，它可以模拟各种移动浏览器，从桌面版本的 Firefox。</span><span class="sxs-lookup"><span data-stu-id="ea966-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ea966-132">其他资源</span><span class="sxs-lookup"><span data-stu-id="ea966-132">Additional Resources</span></span>


<span data-ttu-id="ea966-133">[Windows Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="ea966-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
