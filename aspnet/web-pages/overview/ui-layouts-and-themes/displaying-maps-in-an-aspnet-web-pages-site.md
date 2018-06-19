---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 在 ASP.NET 网页中显示地图页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 此文章介绍了如何在基于映射提供的必应、 Google、 Ma 服务的 ASP.NET Web 页 (Razor) 网站网页上显示交互式的地图...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 608dab8760bad7b877ab6fd4f89b21e980f5b1db
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30893857"
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3f1ae-103">在 ASP.NET 网站页 (Razor) 中显示地图</span><span class="sxs-lookup"><span data-stu-id="3f1ae-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="3f1ae-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3f1ae-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3f1ae-105">此文章介绍了如何在基于映射通过必应、 Google、 MapQuest 和 Yahoo 提供服务的 ASP.NET Web 页 (Razor) 网站网页上显示交互式的地图。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="3f1ae-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3f1ae-107">如何生成基于地址的映射。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="3f1ae-108">如何生成基于纬度和经度坐标的映射。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="3f1ae-109">如何注册必应地图开发人员帐户，并获取用于 Bing 地图密钥。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="3f1ae-110">这是文章中引入的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="3f1ae-111">`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3f1ae-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3f1ae-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3f1ae-113">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="3f1ae-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="3f1ae-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="3f1ae-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="3f1ae-115">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-115">This tutorial also works with WebMatrix 3.</span></span>


<span data-ttu-id="3f1ae-116">在 Web 页中，你可以映射页面上显示通过使用`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="3f1ae-117">你可以生成基于地址或一组的经度和纬度坐标的地图。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="3f1ae-118">`Maps`类，可以调入常用映射引擎包括必应、 Google、 MapQuest 和 Yahoo。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="3f1ae-119">将映射添加到页的步骤都相同的调用而与所映射引擎。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="3f1ae-120">你只需添加使可用的方法，以显示地图的 JavaScript 文件引用，然后调用的方法`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="3f1ae-121">选择在其上基于的映射服务`Maps`你使用的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="3f1ae-122">你可以使用下列任一：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="3f1ae-123">安装所需的组件</span><span class="sxs-lookup"><span data-stu-id="3f1ae-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="3f1ae-124">若要显示地图，您需要这些部分：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="3f1ae-125">`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-125">The `Maps` helper.</span></span> <span data-ttu-id="3f1ae-126">此帮助程序是版本 2 中的 ASP.NET Web 帮助程序库。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="3f1ae-127">如果你尚未添加到库，你可以安装它在你的网站作为 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="3f1ae-128">有关详细信息，请参阅[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="3f1ae-129">(在库，搜索`microsoft-web-helpers`包。)</span><span class="sxs-lookup"><span data-stu-id="3f1ae-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="3f1ae-130">JQuery 库中。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-130">The jQuery library.</span></span> <span data-ttu-id="3f1ae-131">WebMatrix 网站模板的几个已包含中的 jQuery 库其*脚本*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="3f1ae-132">如果你没有这些库，你可以下载最新的 jQuery 库直接从[jQuery.org](http://jQuery.org)站点。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="3f1ae-133">也可以创建新站点使用模板 (例如，**入门站点**模板) 然后将 jQuery 文件从该站点复制到当前站点。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="3f1ae-134">最后，如果你想要使用必应地图，必须先创建一个 （免费） 帐户，并获取密钥。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="3f1ae-135">获取密钥，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="3f1ae-136">在创建帐户[必应地图开发人员帐户](https://www.microsoft.com/maps/developers/web.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="3f1ae-137">你必须具有 Microsoft 帐户 (Windows Live ID) 以及。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="3f1ae-138">你可以指定你想要使用的键**评估/测试**。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="3f1ae-139">如果你要使用 WebMatrix 和 IIS Express 自己计算机上测试映射函数，请转到**站点**工作区并记下你的站点的 URL (例如， `http://localhost:50408`，尽管端口号可能不同)。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="3f1ae-140">你可以使用此*localhost*作为注册时的站点的地址。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="3f1ae-141">你的帐户注册后，请转到必应地图帐户中心，然后单击**创建或视图键**:</span><span class="sxs-lookup"><span data-stu-id="3f1ae-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![mapping-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="3f1ae-143">记录必应创建的密钥。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="3f1ae-144">创建基于 （使用 Google） 的地址映射</span><span class="sxs-lookup"><span data-stu-id="3f1ae-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="3f1ae-145">下面的示例演示如何创建将基于地址结构图呈现的页。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="3f1ae-146">此示例演示如何使用 Google 映射。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="3f1ae-147">创建名为的文件*MapAddress.cshtml*站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="3f1ae-148">此页将生成基于传递给它的地址映射。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="3f1ae-149">将以下代码复制到文件中，覆盖现有的内容。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="3f1ae-150">请注意页上的以下功能：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="3f1ae-151">`<script>`中的元素`<head>`元素。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="3f1ae-152">在示例中，`<script>`元素引用*jquery 1.6.4.min.js*文件，它是 jQuery 库，版本 1.6.4 的缩减 （压缩） 版本。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="3f1ae-153">请注意引用假定 *.js*文件位于*脚本*网站文件夹。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3f1ae-154">如果你正在使用 jQuery 库的不同版本，只需确保的你要指向该版本正确。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="3f1ae-155">调用`@Maps.GetGoogleHtml`页的正文中。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="3f1ae-156">若要将地址映射，你必须传递地址字符串。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="3f1ae-157">对于其他映射引擎方法的工作原理类似的方式 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="3f1ae-158">运行页面，并输入一个地址。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-158">Run the page and enter an address.</span></span> <span data-ttu-id="3f1ae-159">该页面显示地图中，基于 Google 地图，显示你指定的位置。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![mapping-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="3f1ae-161">创建基于纬度和经度地图坐标 （使用必应）</span><span class="sxs-lookup"><span data-stu-id="3f1ae-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="3f1ae-162">此示例演示如何创建基于坐标的映射。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="3f1ae-163">此示例演示如何使用 Bing 地图以及如何包括你必应的密钥。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="3f1ae-164">（可以创建基于使用的其他映射引擎还，而不使用必应密钥的坐标的映射。）</span><span class="sxs-lookup"><span data-stu-id="3f1ae-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="3f1ae-165">创建名为的文件*MapCoordinates.cshtml*根目录中的站点和替换下面的代码和标记的现有内容：</span><span class="sxs-lookup"><span data-stu-id="3f1ae-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="3f1ae-166">替换`your-key-here`替换先前生成的 Bing 地图密钥。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="3f1ae-167">运行*MapCoordinates.cshtml*页上，输入纬度和经度坐标，然后单击**Map It ！**</span><span class="sxs-lookup"><span data-stu-id="3f1ae-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="3f1ae-168">按钮。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-168">button.</span></span> <span data-ttu-id="3f1ae-169">（如果你不知道任何坐标，请尝试以下。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="3f1ae-170">这是 Microsoft 雷蒙德办公区上的位置）。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="3f1ae-171">纬度： 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="3f1ae-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="3f1ae-172">经度：-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="3f1ae-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="3f1ae-173">将显示的页，使用你指定的坐标。</span><span class="sxs-lookup"><span data-stu-id="3f1ae-173">The page is displayed using the coordinates that you specified.</span></span>

     ![mapping-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3f1ae-175">其他资源</span><span class="sxs-lookup"><span data-stu-id="3f1ae-175">Additional Resources</span></span>


[<span data-ttu-id="3f1ae-176">Microsoft.Maps API 参考</span><span class="sxs-lookup"><span data-stu-id="3f1ae-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
