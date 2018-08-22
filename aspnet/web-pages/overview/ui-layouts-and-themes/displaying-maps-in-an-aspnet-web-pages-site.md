---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 显示地图中 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何在基于映射提供必应、 Google、 Ma 的服务的 ASP.NET Web Pages (Razor) 网站中的页面上显示互动地图...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 0b0879047bc71057884ebef98a598eed8c28cddf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830066"
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="f247f-103">ASP.NET Web Pages (Razor) 站点中显示地图</span><span class="sxs-lookup"><span data-stu-id="f247f-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="f247f-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f247f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f247f-105">本文介绍如何在基于映射的必应、 Google、 MapQuest 和 Yahoo 提供服务的 ASP.NET Web Pages (Razor) 网站中的页上显示互动地图。</span><span class="sxs-lookup"><span data-stu-id="f247f-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="f247f-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="f247f-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f247f-107">如何生成基于地址的映射。</span><span class="sxs-lookup"><span data-stu-id="f247f-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="f247f-108">如何生成地图基于纬度和经度坐标。</span><span class="sxs-lookup"><span data-stu-id="f247f-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="f247f-109">如何注册必应地图开发人员帐户，并获得用于必应地图密钥。</span><span class="sxs-lookup"><span data-stu-id="f247f-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="f247f-110">这是引入一文中的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="f247f-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="f247f-111">`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="f247f-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f247f-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f247f-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f247f-113">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="f247f-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f247f-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="f247f-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="f247f-115">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="f247f-115">This tutorial also works with WebMatrix 3.</span></span>


<span data-ttu-id="f247f-116">在 Web 页中，您可以映射在页面上显示通过使用`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="f247f-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="f247f-117">你可以生成基于一个地址或一组的经度和纬度坐标的地图。</span><span class="sxs-lookup"><span data-stu-id="f247f-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="f247f-118">`Maps`类，可以包括必应、 Google、 MapQuest 和 Yahoo 的常用映射引擎调用。</span><span class="sxs-lookup"><span data-stu-id="f247f-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="f247f-119">向页面添加映射的步骤是相同的调用无论哪个映射引擎的。</span><span class="sxs-lookup"><span data-stu-id="f247f-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="f247f-120">只需添加使可用方法显示映射的 JavaScript 文件引用，然后调用的方法`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="f247f-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="f247f-121">选择一项基于在其上映射服务`Maps`所使用的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="f247f-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="f247f-122">可以使用其中的任何：</span><span class="sxs-lookup"><span data-stu-id="f247f-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="f247f-123">安装所需的组件</span><span class="sxs-lookup"><span data-stu-id="f247f-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="f247f-124">若要显示映射，需要这些项：</span><span class="sxs-lookup"><span data-stu-id="f247f-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="f247f-125">`Maps`帮助器。</span><span class="sxs-lookup"><span data-stu-id="f247f-125">The `Maps` helper.</span></span> <span data-ttu-id="f247f-126">此帮助器是版本 2 的 ASP.NET Web Helpers Library 中。</span><span class="sxs-lookup"><span data-stu-id="f247f-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="f247f-127">如果你尚未添加到库，你可以安装它在你的站点中作为 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f247f-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="f247f-128">有关详细信息，请参阅[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)。</span><span class="sxs-lookup"><span data-stu-id="f247f-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="f247f-129">(在库中，搜索`microsoft-web-helpers`包。)</span><span class="sxs-lookup"><span data-stu-id="f247f-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="f247f-130">JQuery 库。</span><span class="sxs-lookup"><span data-stu-id="f247f-130">The jQuery library.</span></span> <span data-ttu-id="f247f-131">WebMatrix 网站模板的几个已包含中的 jQuery 库及其*脚本*文件夹。</span><span class="sxs-lookup"><span data-stu-id="f247f-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="f247f-132">如果您不具备这些库，则可以下载最新的 jQuery 库直接从[jQuery.org](http://jQuery.org)站点。</span><span class="sxs-lookup"><span data-stu-id="f247f-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="f247f-133">也可以创建新的站点使用模板 (例如，**入门网站**模板) 然后将 jQuery 文件从该站点复制到当前站点。</span><span class="sxs-lookup"><span data-stu-id="f247f-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="f247f-134">最后，如果你想要使用必应地图，必须先创建一个 （免费） 帐户，并获取密钥。</span><span class="sxs-lookup"><span data-stu-id="f247f-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="f247f-135">若要获取密钥，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="f247f-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="f247f-136">在创建帐户[必应地图开发人员帐户](https://www.microsoft.com/maps/developers/web.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f247f-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="f247f-137">必须具有 Microsoft 帐户 (Windows Live ID)。</span><span class="sxs-lookup"><span data-stu-id="f247f-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="f247f-138">您可以指定你想要使用的键**评估/测试**。</span><span class="sxs-lookup"><span data-stu-id="f247f-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="f247f-139">如果要在自己计算机上使用 WebMatrix 和 IIS Express 测试映射函数，请转**站点**工作区并记下你站点的 URL (例如， `http://localhost:50408`，尽管端口号可能会不同)。</span><span class="sxs-lookup"><span data-stu-id="f247f-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="f247f-140">可以使用此*localhost*为注册时的站点的地址。</span><span class="sxs-lookup"><span data-stu-id="f247f-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="f247f-141">注册帐户后，请转到 Bing Maps 帐户中心，然后单击**创建或查看键**:</span><span class="sxs-lookup"><span data-stu-id="f247f-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![映射 2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="f247f-143">记录必应创建的密钥。</span><span class="sxs-lookup"><span data-stu-id="f247f-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="f247f-144">创建基于 （使用 Google） 的地址映射</span><span class="sxs-lookup"><span data-stu-id="f247f-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="f247f-145">下面的示例演示如何创建一个页面，呈现基于地址的映射。</span><span class="sxs-lookup"><span data-stu-id="f247f-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="f247f-146">此示例演示如何使用 Google 地图。</span><span class="sxs-lookup"><span data-stu-id="f247f-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="f247f-147">创建名为的文件*MapAddress.cshtml*站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="f247f-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="f247f-148">此页面将生成基于将传递给它的地址的映射。</span><span class="sxs-lookup"><span data-stu-id="f247f-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="f247f-149">将以下代码复制到文件中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="f247f-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="f247f-150">请注意，页上的以下功能：</span><span class="sxs-lookup"><span data-stu-id="f247f-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="f247f-151">`<script>`中的元素`<head>`元素。</span><span class="sxs-lookup"><span data-stu-id="f247f-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="f247f-152">在示例中，`<script>`元素引用*jquery 1.6.4.min.js*文件，它是 jQuery 库，版本 1.6.4 （压缩） 的简化的版本。</span><span class="sxs-lookup"><span data-stu-id="f247f-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="f247f-153">请注意，引用假设 *.js*文件位于*脚本*你的网站的文件夹。</span><span class="sxs-lookup"><span data-stu-id="f247f-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="f247f-154">如果您使用的 jQuery 库的不同版本，只需确保，所指该版本正确。</span><span class="sxs-lookup"><span data-stu-id="f247f-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="f247f-155">对调用`@Maps.GetGoogleHtml`页的正文中。</span><span class="sxs-lookup"><span data-stu-id="f247f-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="f247f-156">若要查找某个地址，必须传递地址字符串。</span><span class="sxs-lookup"><span data-stu-id="f247f-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="f247f-157">其他映射引擎的方法的工作方式类似 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。</span><span class="sxs-lookup"><span data-stu-id="f247f-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="f247f-158">运行该页并输入一个地址。</span><span class="sxs-lookup"><span data-stu-id="f247f-158">Run the page and enter an address.</span></span> <span data-ttu-id="f247f-159">该页将显示基于 Google 地图，显示你指定的位置的映射。</span><span class="sxs-lookup"><span data-stu-id="f247f-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![映射-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="f247f-161">创建地图基于纬度和经度坐标 （使用必应）</span><span class="sxs-lookup"><span data-stu-id="f247f-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="f247f-162">此示例演示如何创建基于坐标的映射。</span><span class="sxs-lookup"><span data-stu-id="f247f-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="f247f-163">此示例演示如何使用必应地图以及如何包含必应密钥。</span><span class="sxs-lookup"><span data-stu-id="f247f-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="f247f-164">（您可以创建基于坐标此外，使用其他映射引擎，而不使用必应密钥映射）。</span><span class="sxs-lookup"><span data-stu-id="f247f-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="f247f-165">创建名为的文件*MapCoordinates.cshtml*替换其中包含以下代码和标记的现有内容的站点的根目录中：</span><span class="sxs-lookup"><span data-stu-id="f247f-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="f247f-166">替换为`your-key-here`使用先前生成的必应地图密钥。</span><span class="sxs-lookup"><span data-stu-id="f247f-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="f247f-167">运行*MapCoordinates.cshtml*页上，输入纬度和经度坐标，然后单击**Map It ！**</span><span class="sxs-lookup"><span data-stu-id="f247f-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="f247f-168">按钮。</span><span class="sxs-lookup"><span data-stu-id="f247f-168">button.</span></span> <span data-ttu-id="f247f-169">（如果不知道任何坐标，尝试以下操作。</span><span class="sxs-lookup"><span data-stu-id="f247f-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="f247f-170">这是在 Microsoft 雷蒙德园区的位置）。</span><span class="sxs-lookup"><span data-stu-id="f247f-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="f247f-171">纬度： 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="f247f-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="f247f-172">经度：-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="f247f-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="f247f-173">使用指定的坐标显示的页。</span><span class="sxs-lookup"><span data-stu-id="f247f-173">The page is displayed using the coordinates that you specified.</span></span>

     ![映射 3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f247f-175">其他资源</span><span class="sxs-lookup"><span data-stu-id="f247f-175">Additional Resources</span></span>


[<span data-ttu-id="f247f-176">Microsoft.Maps API 参考</span><span class="sxs-lookup"><span data-stu-id="f247f-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
