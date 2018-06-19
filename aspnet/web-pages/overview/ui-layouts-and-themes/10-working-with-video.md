---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET 网页中显示视频页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 本章介绍如何显示在带有 Razor 语法页 ASP.NET Web Pages 的视频。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 4e7dc50fb60546d1e1f10a16ed863c0b812ec82b
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
ms.locfileid: "29153675"
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="019dd-103">在 ASP.NET 网站页 (Razor) 中显示视频</span><span class="sxs-lookup"><span data-stu-id="019dd-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="019dd-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="019dd-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="019dd-105">此文章介绍了如何在 ASP.NET Web 页 (Razor) 网站中使用的视频 （媒体） 播放器以使用户可以查看存储在站点的视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="019dd-106">使用 Razor 语法的 ASP.NET 网页，您可以播放 Flash (*.swf*)，Media Player (*.wmv*)，和 Silverlight (*.xap*) 视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="019dd-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="019dd-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="019dd-108">如何选择视频播放器。</span><span class="sxs-lookup"><span data-stu-id="019dd-108">How to choose a video player.</span></span>
> - <span data-ttu-id="019dd-109">如何添加到网页上的视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="019dd-110">如何设置视频播放器特性。</span><span class="sxs-lookup"><span data-stu-id="019dd-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="019dd-111">这些是 ASP.NET Razor 页文章中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="019dd-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="019dd-112">`Video`帮助器。</span><span class="sxs-lookup"><span data-stu-id="019dd-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="019dd-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="019dd-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="019dd-114">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="019dd-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="019dd-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="019dd-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="019dd-116">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="019dd-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="019dd-117">介绍</span><span class="sxs-lookup"><span data-stu-id="019dd-117">Introduction</span></span>

<span data-ttu-id="019dd-118">你可能想要显示在你的站点上的视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-118">You might want to display a video on your site.</span></span> <span data-ttu-id="019dd-119">若要这样做的一种方法是链接到网站已视频中的，如 YouTube。</span><span class="sxs-lookup"><span data-stu-id="019dd-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="019dd-120">如果你想要直接在您自己的页面中嵌入这些站点中的视频，可以从站点通常获取 HTML 标记，然后将其复制到你的页面。</span><span class="sxs-lookup"><span data-stu-id="019dd-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="019dd-121">例如，下面的示例演示如何嵌入了 YouTube 视频：</span><span class="sxs-lookup"><span data-stu-id="019dd-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="019dd-122">如果你想要播放的视频，位于您自己的网站 （不在公共视频共享站点），你无法直接链接到它使用类似此嵌入的标记。</span><span class="sxs-lookup"><span data-stu-id="019dd-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="019dd-123">但是，通过使用，从您的网站播放视频`Video`帮助器，呈现直接在页中的媒体播放器。</span><span class="sxs-lookup"><span data-stu-id="019dd-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="019dd-124">选择视频播放器</span><span class="sxs-lookup"><span data-stu-id="019dd-124">Choosing a Video Player</span></span>

<span data-ttu-id="019dd-125">有大量的视频文件格式，并且每种格式通常需要使用不同的玩家和另一种方式配置播放器。</span><span class="sxs-lookup"><span data-stu-id="019dd-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="019dd-126">在 ASP.NET Razor 页中，也可以在网页中使用的视频`Video`帮助器。</span><span class="sxs-lookup"><span data-stu-id="019dd-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="019dd-127">`Video`帮助程序简化的网页中嵌入视频，因为它自动生成过程`object`和`embed`通常用于视频添加到页面的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="019dd-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="019dd-128">`Video`帮助器支持以下媒体播放器：</span><span class="sxs-lookup"><span data-stu-id="019dd-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="019dd-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="019dd-129">Adobe Flash</span></span>
- <span data-ttu-id="019dd-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="019dd-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="019dd-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="019dd-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="019dd-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="019dd-132">The Flash Player</span></span>

<span data-ttu-id="019dd-133">`Flash`播放器的`Video`帮助器，可以播放闪存视频 (*.swf*文件) 网页中。</span><span class="sxs-lookup"><span data-stu-id="019dd-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="019dd-134">至少，你必须提供视频文件的路径。</span><span class="sxs-lookup"><span data-stu-id="019dd-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="019dd-135">如果指定了任何内容但路径，播放器将使用设置 Flash 的当前版本的默认值。</span><span class="sxs-lookup"><span data-stu-id="019dd-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="019dd-136">典型的默认设置如下：</span><span class="sxs-lookup"><span data-stu-id="019dd-136">Typical default settings are:</span></span>

- <span data-ttu-id="019dd-137">使用其默认宽度和高度显示视频和不使用背景颜色。</span><span class="sxs-lookup"><span data-stu-id="019dd-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="019dd-138">加载页面时，会自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="019dd-139">视频循环显式停止之前一直。</span><span class="sxs-lookup"><span data-stu-id="019dd-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="019dd-140">视频扩展以显示所有的视频中，而不是裁剪视频，以适应特定大小。</span><span class="sxs-lookup"><span data-stu-id="019dd-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="019dd-141">在窗口播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="019dd-142">MediaPlayer 播放器</span><span class="sxs-lookup"><span data-stu-id="019dd-142">The MediaPlayer Player</span></span>

<span data-ttu-id="019dd-143">`MediaPlayer`播放器的`Video`帮助器，您可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media 音频 (*.wma*文件)，和 MP3 (*.mp3*文件） 网页中。</span><span class="sxs-lookup"><span data-stu-id="019dd-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="019dd-144">必须包含的要播放; 的媒体文件的路径所有其他参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="019dd-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="019dd-145">如果你仅指定一个路径，播放器将使用默认设置设置 MediaPlayer 的当前版本，如：</span><span class="sxs-lookup"><span data-stu-id="019dd-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="019dd-146">在视频显示时使用其默认宽度和高度。</span><span class="sxs-lookup"><span data-stu-id="019dd-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="019dd-147">加载页面时，会自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="019dd-148">视频播放一次 （它不会循环的）。</span><span class="sxs-lookup"><span data-stu-id="019dd-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="019dd-149">播放器用户界面中显示的完整控件集。</span><span class="sxs-lookup"><span data-stu-id="019dd-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="019dd-150">在窗口播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="019dd-151">Silverlight 播放器</span><span class="sxs-lookup"><span data-stu-id="019dd-151">The Silverlight Player</span></span>

<span data-ttu-id="019dd-152">`Silverlight`播放器的`Video`帮助器，您可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media 音频 (*.wma*文件)，和 MP3 (*.mp3*文件）。</span><span class="sxs-lookup"><span data-stu-id="019dd-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="019dd-153">必须设置 path 参数，以指向基于 Silverlight 的应用程序包 (*.xap*文件)。</span><span class="sxs-lookup"><span data-stu-id="019dd-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="019dd-154">此外必须设置宽度和高度参数。</span><span class="sxs-lookup"><span data-stu-id="019dd-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="019dd-155">其他所有参数都是可选参数。</span><span class="sxs-lookup"><span data-stu-id="019dd-155">All other parameters are optional.</span></span> <span data-ttu-id="019dd-156">当你使用 Silverlight 播放器有关视频，如果设置所需的参数时，Silverlight 播放器显示不带背景颜色的视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="019dd-157">如果您尚不知道 Silverlight: *.xap*文件是一个压缩的文件，其中包含中的布局说明 *.xaml*文件，程序集和可选资源中的托管的代码。</span><span class="sxs-lookup"><span data-stu-id="019dd-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="019dd-158">你可以创建 *.xap*为 Silverlight 应用程序项目的 Visual Studio 中的文件。</span><span class="sxs-lookup"><span data-stu-id="019dd-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="019dd-159">`Silverlight`视频播放器使用两个播放器提供的设置和中提供的设置 *.xap*文件。</span><span class="sxs-lookup"><span data-stu-id="019dd-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="019dd-160">MIME 类型</span><span class="sxs-lookup"><span data-stu-id="019dd-160">MIME Types</span></span>
> 
> <span data-ttu-id="019dd-161">当浏览器下载一个文件时，则浏览器可确保文件类型匹配的文档的呈现为指定的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="019dd-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="019dd-162">MIME 类型是一个文件的内容类型或媒体类型。</span><span class="sxs-lookup"><span data-stu-id="019dd-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="019dd-163">`Video`帮助器使用以下 MIME 类型：</span><span class="sxs-lookup"><span data-stu-id="019dd-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="019dd-164">播放 Flash (.swf) 视频</span><span class="sxs-lookup"><span data-stu-id="019dd-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="019dd-165">此过程演示如何播放闪存视频名为*sample.swf*。</span><span class="sxs-lookup"><span data-stu-id="019dd-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="019dd-166">此过程假设您有一个名为文件夹*媒体*你的站点和上 *.swf*文件是在该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="019dd-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="019dd-167">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。</span><span class="sxs-lookup"><span data-stu-id="019dd-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="019dd-168">在网站中，添加一个页面，并将其命名*FlashVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="019dd-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="019dd-169">向页面添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="019dd-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="019dd-170">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="019dd-170">Run the page in a browser.</span></span> <span data-ttu-id="019dd-171">(请确保页中选择**文件**工作区之前运行它。)将显示的页和自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="019dd-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span><span class="sxs-lookup"><span data-stu-id="019dd-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="019dd-173">你可以设置`quality`参数到闪存视频`low`， `autolow`， `autohigh`， `medium`， `high`，和`best`:</span><span class="sxs-lookup"><span data-stu-id="019dd-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="019dd-174">你可以更改闪存的视频，以播放特定大小使用`scale`参数，您可以对以下设置：</span><span class="sxs-lookup"><span data-stu-id="019dd-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="019dd-175">`showall`。</span><span class="sxs-lookup"><span data-stu-id="019dd-175">`showall`.</span></span> <span data-ttu-id="019dd-176">这将使整个视频可见同时保持原始纵横比。</span><span class="sxs-lookup"><span data-stu-id="019dd-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="019dd-177">但是，你可能会得到与每个边的边框。</span><span class="sxs-lookup"><span data-stu-id="019dd-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="019dd-178">`noorder`。</span><span class="sxs-lookup"><span data-stu-id="019dd-178">`noorder`.</span></span> <span data-ttu-id="019dd-179">这同时保持原始纵横比，缩放视频，但它可能会裁剪。</span><span class="sxs-lookup"><span data-stu-id="019dd-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="019dd-180">`exactfit`。</span><span class="sxs-lookup"><span data-stu-id="019dd-180">`exactfit`.</span></span> <span data-ttu-id="019dd-181">这将使整个视频可见而无需保留原始的纵横比，但可能会发生扭曲。</span><span class="sxs-lookup"><span data-stu-id="019dd-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="019dd-182">如果没有指定`scale`参数，整个视频可以可见，而无需任何裁剪将保留原始的纵横比。</span><span class="sxs-lookup"><span data-stu-id="019dd-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="019dd-183">下面的示例演示如何使用`scale`参数：</span><span class="sxs-lookup"><span data-stu-id="019dd-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="019dd-184">Flash player 支持的视频模式设置命名`windowMode`。</span><span class="sxs-lookup"><span data-stu-id="019dd-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="019dd-185">你可以将此设置为`window`， `opaque`，和`transparent`。</span><span class="sxs-lookup"><span data-stu-id="019dd-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="019dd-186">默认情况下，`windowMode`设置为`window`，它会在网页上的单独窗口中显示视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="019dd-187">`opaque`设置隐藏在网页上的视频后面的所有内容。</span><span class="sxs-lookup"><span data-stu-id="019dd-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="019dd-188">`transparent`设置可让 web 页的背景图像显示视频中，通过假设透明的视频的任何部分。</span><span class="sxs-lookup"><span data-stu-id="019dd-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="019dd-189">播放 MediaPlayer (*.wmv*) 视频</span><span class="sxs-lookup"><span data-stu-id="019dd-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="019dd-190">下面的过程演示如何播放窗口媒体视频名为*sample.wmv* ，位于*媒体*文件夹。</span><span class="sxs-lookup"><span data-stu-id="019dd-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="019dd-191">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未。</span><span class="sxs-lookup"><span data-stu-id="019dd-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="019dd-192">创建一个名为的新页*MediaPlayerVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="019dd-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="019dd-193">向页面添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="019dd-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="019dd-194">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="019dd-194">Run the page in a browser.</span></span> <span data-ttu-id="019dd-195">视频加载，并会自动播放。</span><span class="sxs-lookup"><span data-stu-id="019dd-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="019dd-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span><span class="sxs-lookup"><span data-stu-id="019dd-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="019dd-197">你可以设置`playCount`为整数类型的值，该值指示多少次，以自动播放视频：</span><span class="sxs-lookup"><span data-stu-id="019dd-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="019dd-198">`uiMode`参数允许你指定哪些控件显示在用户界面。</span><span class="sxs-lookup"><span data-stu-id="019dd-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="019dd-199">你可以设置`uiMode`到`invisible`， `none`， `mini`，或`full`。</span><span class="sxs-lookup"><span data-stu-id="019dd-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="019dd-200">如果没有指定`uiMode`参数，视频将显示与状态窗口，查找条形图、 控制按钮和音量控制，除了视频窗口。</span><span class="sxs-lookup"><span data-stu-id="019dd-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="019dd-201">如果你使用播放器播放音频文件，也会显示这些控件。</span><span class="sxs-lookup"><span data-stu-id="019dd-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="019dd-202">下面是如何使用的一个示例`uiMode`参数：</span><span class="sxs-lookup"><span data-stu-id="019dd-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="019dd-203">默认情况下，音频已启用并时播放视频。</span><span class="sxs-lookup"><span data-stu-id="019dd-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="019dd-204">你可以通过设置静音音频`mute`参数为 true:</span><span class="sxs-lookup"><span data-stu-id="019dd-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="019dd-205">你可以通过设置控制 MediaPlayer 视频的音频级别`volume`到 0 和 100 之间的值的参数。</span><span class="sxs-lookup"><span data-stu-id="019dd-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="019dd-206">默认值为 50。</span><span class="sxs-lookup"><span data-stu-id="019dd-206">The default value is 50.</span></span> <span data-ttu-id="019dd-207">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="019dd-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="019dd-208">播放 Silverlight 视频</span><span class="sxs-lookup"><span data-stu-id="019dd-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="019dd-209">此过程演示如何播放视频 Silverlight 中包含 *.xap*页的文件夹中名为*媒体*。</span><span class="sxs-lookup"><span data-stu-id="019dd-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="019dd-210">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未。</span><span class="sxs-lookup"><span data-stu-id="019dd-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="019dd-211">创建一个名为的新页*SilverlightVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="019dd-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="019dd-212">向页面添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="019dd-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="019dd-213">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="019dd-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="019dd-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span><span class="sxs-lookup"><span data-stu-id="019dd-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="019dd-215">其他资源</span><span class="sxs-lookup"><span data-stu-id="019dd-215">Additional Resources</span></span>


<span data-ttu-id="019dd-216">[Silverlight 概述](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="019dd-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="019dd-217">Flash 对象和嵌入标记特性</span><span class="sxs-lookup"><span data-stu-id="019dd-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="019dd-218">[Windows Media Player 11 SDK PARAM 标记](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="019dd-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
