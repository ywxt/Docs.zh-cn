---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET 网页中显示视频页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本章介绍如何显示在带有 Razor 语法页面 ASP.NET Web Pages 的视频。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 28884d8c4998ea5b00a60bf094f41b915b565bd8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834286"
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a9550-103">在 ASP.NET Web Pages (Razor) 站点中显示视频</span><span class="sxs-lookup"><span data-stu-id="a9550-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="a9550-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a9550-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a9550-105">本文介绍如何在 ASP.NET Web Pages (Razor) 网站中使用视频 （媒体） 播放机以使用户可以查看存储在站点的视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="a9550-106">使用 Razor 语法的 ASP.NET 网页，您可以播放 Flash (*.swf*)，Media Player (*.wmv*)，和 Silverlight (*.xap*) 视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="a9550-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="a9550-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a9550-108">如何选择视频播放器。</span><span class="sxs-lookup"><span data-stu-id="a9550-108">How to choose a video player.</span></span>
> - <span data-ttu-id="a9550-109">如何将视频添加到 web 页。</span><span class="sxs-lookup"><span data-stu-id="a9550-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="a9550-110">如何设置视频播放器的属性。</span><span class="sxs-lookup"><span data-stu-id="a9550-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="a9550-111">这些是 ASP.NET Razor 页面项目中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="a9550-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a9550-112">`Video`帮助器。</span><span class="sxs-lookup"><span data-stu-id="a9550-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a9550-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a9550-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a9550-114">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="a9550-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a9550-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="a9550-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="a9550-116">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="a9550-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="a9550-117">介绍</span><span class="sxs-lookup"><span data-stu-id="a9550-117">Introduction</span></span>

<span data-ttu-id="a9550-118">你可能想要在站点上显示视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-118">You might want to display a video on your site.</span></span> <span data-ttu-id="a9550-119">若要执行此操作的一种方法是将链接到已有的视频，如 YouTube 的站点。</span><span class="sxs-lookup"><span data-stu-id="a9550-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="a9550-120">如果你想要直接在您自己的页面中嵌入这些站点中的视频，可以通常从站点获取 HTML 标记，然后将其复制到您的页面。</span><span class="sxs-lookup"><span data-stu-id="a9550-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="a9550-121">例如，下面的示例演示如何嵌入的 YouTube 视频：</span><span class="sxs-lookup"><span data-stu-id="a9550-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="a9550-122">如果你想要播放的视频，位于您自己的网站 （不在公共视频共享站点），您不能直接链接到它使用嵌入的标记，如下。</span><span class="sxs-lookup"><span data-stu-id="a9550-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="a9550-123">但是，通过使用，从你的站点播放视频`Video`帮助器，呈现在页面中直接的媒体播放器。</span><span class="sxs-lookup"><span data-stu-id="a9550-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="a9550-124">选择视频播放器</span><span class="sxs-lookup"><span data-stu-id="a9550-124">Choosing a Video Player</span></span>

<span data-ttu-id="a9550-125">有很多的视频文件格式，每个格式通常需要不同的玩家，配置播放机的不同方法。</span><span class="sxs-lookup"><span data-stu-id="a9550-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="a9550-126">在 ASP.NET Razor 页中，也可以在网页中使用的视频`Video`帮助器。</span><span class="sxs-lookup"><span data-stu-id="a9550-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="a9550-127">`Video`帮助程序简化了网页中嵌入视频，因为它会自动生成的过程`object`和`embed`通常用于将视频添加到页面的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="a9550-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="a9550-128">`Video`帮助器支持以下媒体播放器：</span><span class="sxs-lookup"><span data-stu-id="a9550-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="a9550-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="a9550-129">Adobe Flash</span></span>
- <span data-ttu-id="a9550-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="a9550-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="a9550-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="a9550-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="a9550-132">Flash 播放器</span><span class="sxs-lookup"><span data-stu-id="a9550-132">The Flash Player</span></span>

<span data-ttu-id="a9550-133">`Flash`播放器进行播放`Video`帮助器允许您播放 Flash 视频 (*.swf*文件) 在网页中。</span><span class="sxs-lookup"><span data-stu-id="a9550-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="a9550-134">至少，您必须提供的视频文件的路径。</span><span class="sxs-lookup"><span data-stu-id="a9550-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="a9550-135">如果不指定任何内容，但路径，播放机将使用设置 Flash 的当前版本的默认值。</span><span class="sxs-lookup"><span data-stu-id="a9550-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="a9550-136">典型的默认设置如下：</span><span class="sxs-lookup"><span data-stu-id="a9550-136">Typical default settings are:</span></span>

- <span data-ttu-id="a9550-137">在视频显示时使用它的默认宽度和高度，而无需背景色。</span><span class="sxs-lookup"><span data-stu-id="a9550-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="a9550-138">在页面加载时，自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="a9550-139">视频持续循环，直到显式停止。</span><span class="sxs-lookup"><span data-stu-id="a9550-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="a9550-140">视频进行缩放以显示所有视频中，而不是时会修剪视频以适应特定大小。</span><span class="sxs-lookup"><span data-stu-id="a9550-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="a9550-141">在窗口中播放视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="a9550-142">MediaPlayer 播放器</span><span class="sxs-lookup"><span data-stu-id="a9550-142">The MediaPlayer Player</span></span>

<span data-ttu-id="a9550-143">`MediaPlayer`播放器进行播放`Video`帮助器，可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media 音频 (*.wma*文件)，和 MP3 (*.mp3*文件） 在网页中。</span><span class="sxs-lookup"><span data-stu-id="a9550-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="a9550-144">必须包括要播放; 的媒体文件的路径所有其他参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="a9550-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="a9550-145">如果您仅指定一个路径，播放机将使用默认设置设置的当前版本的 MediaPlayer，如：</span><span class="sxs-lookup"><span data-stu-id="a9550-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="a9550-146">在视频显示时使用它的默认宽度和高度。</span><span class="sxs-lookup"><span data-stu-id="a9550-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="a9550-147">在页面加载时，自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="a9550-148">视频播放一次 （它不会循环）。</span><span class="sxs-lookup"><span data-stu-id="a9550-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="a9550-149">播放机在用户界面中显示控件的完整的集合。</span><span class="sxs-lookup"><span data-stu-id="a9550-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="a9550-150">在窗口中播放视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="a9550-151">Silverlight 播放器</span><span class="sxs-lookup"><span data-stu-id="a9550-151">The Silverlight Player</span></span>

<span data-ttu-id="a9550-152">`Silverlight`播放器进行播放`Video`帮助程序，您可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media Audio (*.wma*文件)，和 MP3 (*.mp3*文件）。</span><span class="sxs-lookup"><span data-stu-id="a9550-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="a9550-153">必须设置 path 参数以指向基于 Silverlight 的应用程序包 (*.xap*文件)。</span><span class="sxs-lookup"><span data-stu-id="a9550-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="a9550-154">此外必须设置宽度和高度参数。</span><span class="sxs-lookup"><span data-stu-id="a9550-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="a9550-155">其他所有参数都是可选参数。</span><span class="sxs-lookup"><span data-stu-id="a9550-155">All other parameters are optional.</span></span> <span data-ttu-id="a9550-156">使用时 Silverlight 播放器的视频中，如果设置的所有必需的参数，Silverlight 播放器显示视频而不会背景色。</span><span class="sxs-lookup"><span data-stu-id="a9550-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="a9550-157">如果您还不知道 Silverlight: *.xap*文件是压缩的文件，其中包含中的布局说明 *.xaml*托管的代码程序集以及可选资源文件。</span><span class="sxs-lookup"><span data-stu-id="a9550-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="a9550-158">您可以创建 *.xap*为 Silverlight 应用程序项目的 Visual Studio 中的文件。</span><span class="sxs-lookup"><span data-stu-id="a9550-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="a9550-159">`Silverlight`视频的播放机使用的播放机提供的设置和中提供的设置都 *.xap*文件。</span><span class="sxs-lookup"><span data-stu-id="a9550-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="a9550-160">MIME 类型</span><span class="sxs-lookup"><span data-stu-id="a9550-160">MIME Types</span></span>
> 
> <span data-ttu-id="a9550-161">当浏览器下载文件时，在浏览器可确保文件类型与指定要呈现的文档的 MIME 类型相匹配。</span><span class="sxs-lookup"><span data-stu-id="a9550-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="a9550-162">MIME 类型是一个文件的内容类型或媒体类型。</span><span class="sxs-lookup"><span data-stu-id="a9550-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="a9550-163">`Video`帮助程序会使用以下 MIME 类型：</span><span class="sxs-lookup"><span data-stu-id="a9550-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="a9550-164">播放 Flash (.swf) 视频</span><span class="sxs-lookup"><span data-stu-id="a9550-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="a9550-165">此过程演示如何以名为 Flash 视频播放*sample.swf*。</span><span class="sxs-lookup"><span data-stu-id="a9550-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="a9550-166">该过程假定您有一个名为文件夹*媒体*上你的站点 *.swf*文件是在该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a9550-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="a9550-167">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。</span><span class="sxs-lookup"><span data-stu-id="a9550-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="a9550-168">在网站中，添加一个页面并将其命名*FlashVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a9550-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="a9550-169">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="a9550-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="a9550-170">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a9550-170">Run the page in a browser.</span></span> <span data-ttu-id="a9550-171">(请确保的页中选择**文件**工作区之前运行它。)将显示的页和自动播放视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="a9550-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span><span class="sxs-lookup"><span data-stu-id="a9550-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="a9550-173">可以设置`quality`参数到 Flash 视频`low`， `autolow`， `autohigh`， `medium`， `high`，和`best`:</span><span class="sxs-lookup"><span data-stu-id="a9550-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="a9550-174">您可以更改闪存视频播放特定大小使用`scale`参数，它可以为以下设置：</span><span class="sxs-lookup"><span data-stu-id="a9550-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="a9550-175">`showall`。</span><span class="sxs-lookup"><span data-stu-id="a9550-175">`showall`.</span></span> <span data-ttu-id="a9550-176">这将使整个视频可见同时保持原始纵横比。</span><span class="sxs-lookup"><span data-stu-id="a9550-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="a9550-177">但是，您可能会得到每侧的边框。</span><span class="sxs-lookup"><span data-stu-id="a9550-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="a9550-178">`noorder`。</span><span class="sxs-lookup"><span data-stu-id="a9550-178">`noorder`.</span></span> <span data-ttu-id="a9550-179">这会在视频缩放同时保持原始纵横比，但它可能会裁剪。</span><span class="sxs-lookup"><span data-stu-id="a9550-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="a9550-180">`exactfit`。</span><span class="sxs-lookup"><span data-stu-id="a9550-180">`exactfit`.</span></span> <span data-ttu-id="a9550-181">这将使整个视频可见而无需保留原始纵横比，但会出现失真。</span><span class="sxs-lookup"><span data-stu-id="a9550-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="a9550-182">如果未指定`scale`参数，将显示整个视频和原始纵横比会保留而无需任何剪切。</span><span class="sxs-lookup"><span data-stu-id="a9550-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="a9550-183">下面的示例演示如何使用`scale`参数：</span><span class="sxs-lookup"><span data-stu-id="a9550-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="a9550-184">Flash 播放器支持一种视频模式设置命名`windowMode`。</span><span class="sxs-lookup"><span data-stu-id="a9550-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="a9550-185">可以将此设置为`window`， `opaque`，和`transparent`。</span><span class="sxs-lookup"><span data-stu-id="a9550-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="a9550-186">默认情况下`windowMode`设置为`window`，这在网页上的单独窗口中显示的视频。</span><span class="sxs-lookup"><span data-stu-id="a9550-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="a9550-187">`opaque`设置隐藏在网页上的视频背后的所有内容。</span><span class="sxs-lookup"><span data-stu-id="a9550-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="a9550-188">`transparent`设置可让 web 页的背景显示通过此视频中，假定该视频的任何部分透明的。</span><span class="sxs-lookup"><span data-stu-id="a9550-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="a9550-189">播放 MediaPlayer (*.wmv*) 视频</span><span class="sxs-lookup"><span data-stu-id="a9550-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="a9550-190">以下过程演示如何播放窗口媒体视频名为*sample.wmv*所在的域*媒体*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a9550-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="a9550-191">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。</span><span class="sxs-lookup"><span data-stu-id="a9550-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="a9550-192">创建一个名为的新页*MediaPlayerVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a9550-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="a9550-193">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="a9550-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="a9550-194">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a9550-194">Run the page in a browser.</span></span> <span data-ttu-id="a9550-195">视频加载，并将自动播放。</span><span class="sxs-lookup"><span data-stu-id="a9550-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="a9550-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span><span class="sxs-lookup"><span data-stu-id="a9550-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="a9550-197">可以设置`playCount`到一个整数，指示自动播放视频次数：</span><span class="sxs-lookup"><span data-stu-id="a9550-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="a9550-198">`uiMode`参数可以指定哪些控件显示在用户界面。</span><span class="sxs-lookup"><span data-stu-id="a9550-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="a9550-199">可以设置`uiMode`到`invisible`， `none`， `mini`，或`full`。</span><span class="sxs-lookup"><span data-stu-id="a9550-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="a9550-200">如果未指定`uiMode`参数，视频会显示与状态窗口，查找栏中，控制按钮和音量控件和视频的窗口。</span><span class="sxs-lookup"><span data-stu-id="a9550-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="a9550-201">如果您使用播放机播放音频文件，也会显示这些控件。</span><span class="sxs-lookup"><span data-stu-id="a9550-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="a9550-202">下面是举例说明如何使用`uiMode`参数：</span><span class="sxs-lookup"><span data-stu-id="a9550-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="a9550-203">默认情况下，音频是在视频播放时。</span><span class="sxs-lookup"><span data-stu-id="a9550-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="a9550-204">可以通过设置静音音频`mute`参数设为 true:</span><span class="sxs-lookup"><span data-stu-id="a9550-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="a9550-205">可以通过设置控制 MediaPlayer 视频的音频级别`volume`参数为介于 0 和 100 之间的值。</span><span class="sxs-lookup"><span data-stu-id="a9550-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="a9550-206">默认值为 50。</span><span class="sxs-lookup"><span data-stu-id="a9550-206">The default value is 50.</span></span> <span data-ttu-id="a9550-207">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="a9550-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="a9550-208">播放 Silverlight 视频</span><span class="sxs-lookup"><span data-stu-id="a9550-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="a9550-209">此过程演示如何在 Silverlight 中包含的视频播放 *.xap*页上的文件夹中名为*媒体*。</span><span class="sxs-lookup"><span data-stu-id="a9550-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="a9550-210">将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。</span><span class="sxs-lookup"><span data-stu-id="a9550-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="a9550-211">创建一个名为的新页*SilverlightVideo.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="a9550-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="a9550-212">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="a9550-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="a9550-213">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="a9550-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="a9550-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span><span class="sxs-lookup"><span data-stu-id="a9550-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a9550-215">其他资源</span><span class="sxs-lookup"><span data-stu-id="a9550-215">Additional Resources</span></span>


<span data-ttu-id="a9550-216">[Silverlight 概述](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="a9550-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="a9550-217">Flash 对象和嵌入标记特性</span><span class="sxs-lookup"><span data-stu-id="a9550-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="a9550-218">[Windows Media Player 11 SDK PARAM 标记](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="a9550-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
