---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET 网页中显示视频页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本章介绍如何显示在带有 Razor 语法页面 ASP.NET Web Pages 的视频。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: d80fd8ab54bf1c049fa4ee6b7592925ebe0549f8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369381"
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages (Razor) 站点中显示视频
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET Web Pages (Razor) 网站中使用视频 （媒体） 播放机以使用户可以查看存储在站点的视频。 使用 Razor 语法的 ASP.NET 网页，您可以播放 Flash (*.swf*)，Media Player (*.wmv*)，和 Silverlight (*.xap*) 视频。
> 
> 你将学习：
> 
> - 如何选择视频播放器。
> - 如何将视频添加到 web 页。
> - 如何设置视频播放器的属性。
> 
> 这些是 ASP.NET Razor 页面项目中引入的功能：
> 
> - `Video`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。


## <a name="introduction"></a>介绍

你可能想要在站点上显示视频。 若要执行此操作的一种方法是将链接到已有的视频，如 YouTube 的站点。 如果你想要直接在您自己的页面中嵌入这些站点中的视频，可以通常从站点获取 HTML 标记，然后将其复制到您的页面。 例如，下面的示例演示如何嵌入的 YouTube 视频：

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

如果你想要播放的视频，位于您自己的网站 （不在公共视频共享站点），您不能直接链接到它使用嵌入的标记，如下。 但是，通过使用，从你的站点播放视频`Video`帮助器，呈现在页面中直接的媒体播放器。

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>选择视频播放器

有很多的视频文件格式，每个格式通常需要不同的玩家，配置播放机的不同方法。 在 ASP.NET Razor 页中，也可以在网页中使用的视频`Video`帮助器。 `Video`帮助程序简化了网页中嵌入视频，因为它会自动生成的过程`object`和`embed`通常用于将视频添加到页面的 HTML 元素。

`Video`帮助器支持以下媒体播放器：

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash 播放器

`Flash`播放器进行播放`Video`帮助器允许您播放 Flash 视频 (*.swf*文件) 在网页中。 至少，您必须提供的视频文件的路径。 如果不指定任何内容，但路径，播放机将使用设置 Flash 的当前版本的默认值。 典型的默认设置如下：

- 在视频显示时使用它的默认宽度和高度，而无需背景色。
- 在页面加载时，自动播放视频。
- 视频持续循环，直到显式停止。
- 视频进行缩放以显示所有视频中，而不是时会修剪视频以适应特定大小。
- 在窗口中播放视频。

### <a name="the-mediaplayer-player"></a>MediaPlayer 播放器

`MediaPlayer`播放器进行播放`Video`帮助器，可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media 音频 (*.wma*文件)，和 MP3 (*.mp3*文件） 在网页中。 必须包括要播放; 的媒体文件的路径所有其他参数是可选的。 如果您仅指定一个路径，播放机将使用默认设置设置的当前版本的 MediaPlayer，如：

- 在视频显示时使用它的默认宽度和高度。
- 在页面加载时，自动播放视频。
- 视频播放一次 （它不会循环）。
- 播放机在用户界面中显示控件的完整的集合。
- 在窗口中播放视频。

### <a name="the-silverlight-player"></a>Silverlight 播放器

`Silverlight`播放器进行播放`Video`帮助程序，您可以播放 Windows Media 视频 (*.wmv*文件)，Windows Media Audio (*.wma*文件)，和 MP3 (*.mp3*文件）。 必须设置 path 参数以指向基于 Silverlight 的应用程序包 (*.xap*文件)。 此外必须设置宽度和高度参数。 其他所有参数都是可选参数。 使用时 Silverlight 播放器的视频中，如果设置的所有必需的参数，Silverlight 播放器显示视频而不会背景色。

> [!NOTE]
> 如果您还不知道 Silverlight: *.xap*文件是压缩的文件，其中包含中的布局说明 *.xaml*托管的代码程序集以及可选资源文件。 您可以创建 *.xap*为 Silverlight 应用程序项目的 Visual Studio 中的文件。


`Silverlight`视频的播放机使用的播放机提供的设置和中提供的设置都 *.xap*文件。

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME 类型
> 
> 当浏览器下载文件时，在浏览器可确保文件类型与指定要呈现的文档的 MIME 类型相匹配。 MIME 类型是一个文件的内容类型或媒体类型。 `Video`帮助程序会使用以下 MIME 类型：
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>播放 Flash (.swf) 视频

此过程演示如何以名为 Flash 视频播放*sample.swf*。 该过程假定您有一个名为文件夹*媒体*上你的站点 *.swf*文件是在该文件夹中。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。
2. 在网站中，添加一个页面并将其命名*FlashVideo.cshtml*。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. 在浏览器中运行页。 (请确保的页中选择**文件**工作区之前运行它。)将显示的页和自动播放视频。 

    ![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")

可以设置`quality`参数到 Flash 视频`low`， `autolow`， `autohigh`， `medium`， `high`，和`best`:

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

您可以更改闪存视频播放特定大小使用`scale`参数，它可以为以下设置：

- `showall`。 这将使整个视频可见同时保持原始纵横比。 但是，您可能会得到每侧的边框。
- `noorder`。 这会在视频缩放同时保持原始纵横比，但它可能会裁剪。
- `exactfit`。 这将使整个视频可见而无需保留原始纵横比，但会出现失真。

如果未指定`scale`参数，将显示整个视频和原始纵横比会保留而无需任何剪切。 下面的示例演示如何使用`scale`参数：

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash 播放器支持一种视频模式设置命名`windowMode`。 可以将此设置为`window`， `opaque`，和`transparent`。 默认情况下`windowMode`设置为`window`，这在网页上的单独窗口中显示的视频。 `opaque`设置隐藏在网页上的视频背后的所有内容。 `transparent`设置可让 web 页的背景显示通过此视频中，假定该视频的任何部分透明的。

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>播放 MediaPlayer (*.wmv*) 视频

以下过程演示如何播放窗口媒体视频名为*sample.wmv*所在的域*媒体*文件夹。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
2. 创建一个名为的新页*MediaPlayerVideo.cshtml*。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. 在浏览器中运行页。 视频加载，并将自动播放。 

    ![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")

可以设置`playCount`到一个整数，指示自动播放视频次数：

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode`参数可以指定哪些控件显示在用户界面。 可以设置`uiMode`到`invisible`， `none`， `mini`，或`full`。 如果未指定`uiMode`参数，视频会显示与状态窗口，查找栏中，控制按钮和音量控件和视频的窗口。 如果您使用播放机播放音频文件，也会显示这些控件。 下面是举例说明如何使用`uiMode`参数：

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

默认情况下，音频是在视频播放时。 可以通过设置静音音频`mute`参数设为 true:

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

可以通过设置控制 MediaPlayer 视频的音频级别`volume`参数为介于 0 和 100 之间的值。 默认值为 50。 以下是一个示例：

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>播放 Silverlight 视频

此过程演示如何在 Silverlight 中包含的视频播放 *.xap*页上的文件夹中名为*媒体*。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
2. 创建一个名为的新页*SilverlightVideo.cshtml*。
3. 将以下标记添加到页面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. 在浏览器中运行页。 

    ![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[Silverlight 概述](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash 对象和嵌入标记特性](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK PARAM 标记](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
