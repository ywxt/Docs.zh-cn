---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 将社交网络添加到 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 这一章介绍了如何将您的网站与社交网络服务集成。 在本章中，您将学习如何让人们书签/链接你的网站...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 684fcfdde0aefeb168398bdf7a42f9fdbd6e48b3
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830460"
---
<a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>添加社交网络到 ASP.NET 网页 (Razor) 站点
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何将适用于 Facebook、 Twitter、 Reddit 和 Digg 的社交网络链接添加到页面中的 ASP.NET Web Pages (Razor) 网站，以及如何包含 Twitter 源、 Xbox 玩家卡和 Gravatar 图像。
> 
> 你将学习：
> 
> - 如何让人们书签/链接你的站点。
> - 如何添加 Twitter 源。
> - 如何添加 Facebook**如**到页的按钮。
> - 如何呈现 Gravatar.com 图像。
> - 如何在站点上显示的 Xbox 玩家卡。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - ASP.NET Web 帮助程序库 （NuGet 包）
>   
> 
> 本教程还适用于 ASP.NET 网页 3，但 ASP.NET Web 帮助程序库使用的部分除外。


<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>链接你的网站上社交网络网站

如果用户喜欢你的站点上的某些内容，他们通常想要与朋友共享。 您可以通过使其轻松显示用户可以单击要共享的页，Digg、 Reddit、 Facebook、 Twitter 或类似的网站的标志符号 （图标）。

若要显示这些标志符号，请添加`LinkSharecode`到页面的帮助器。 访问您的页面的用户可以单击单个标志符号。 如果他们的帐户拥有的社交网站，它们可以在该站点上中发布您的页面的链接。

![图 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。-创建一个名为页*ListLinkShare.cshtml*并添加以下标记：

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    在此示例中，当`LinkShare`帮助程序运行时，页面标题传递作为参数，再将传递到社交网络站点的页面标题。 但是，你可以传递所需的任何字符串。 此示例还指定要包含在列表中的社交网站。 您可以指定与你的站点相关的社交网络站点。
2. 运行*ListLinkShare.cshtml*页在浏览器中。 (请确保的页中选择**文件**工作区之前运行它。)
3. 单击其中一个已注册了站点的标志符号。 链接将您转至页面上所选的社交网络站点可以在其中共享链接。 例如，如果单击 Reddit 链接，您会转到`submit to reddit`Reddit 网站上的页。

     ![图 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>添加 Twitter 源

有关使用与 Twitter API 的当前版本兼容的 Twitter 帮助程序的信息，请参阅[Twitter 帮助程序](../ui-layouts-and-themes/twitter-helper.md)。 此示例演示如何编写您自己的帮助程序，因此可以轻松地重复使用很多页中的代码。

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>显示是 Facebook&quot;如&quot;按钮

在某些情况下，最好的选择是，直接从社交网络提供程序，而无需依赖于一个帮助程序获取的代码。 这是特别是当社交网络提供商不是帮助程序更新更快地更新其自己的选项。

若要将 Facebook 功能 （如 Like 按钮） 添加到你的站点，可以检索从代码片段[developers.facebook.com](https://developers.facebook.com/)站点。 在 Facebook 网站上，使用其工具生成了与你的站点相关的代码段。

以下突出显示的代码是从 developers.facebook.com 站点上的喜欢按钮工具中检索到的代码。 必须提供应用程序 id。

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>呈现 Gravatar 图像

一个*Gravatar* (&quot;全局识别虚拟形象&quot;) 是可以为您的头像的多个网站使用的图像&#8212;，即表示您的图像。 例如，Gravatar 可以识别一个人在论坛文章中，在博客评论中，依次类推。 (您可以注册在 Gravatar 网站在自己 Gravatar [ http://www.gravatar.com/ ](http://www.gravatar.com/)。)如果你想要在网站上显示人的名称或电子邮件地址旁边的图像，可以使用 Gravatar 帮助器。

在此示例中，您将自己表示单个 Gravatar。 使用 Gravatar 另一种方法是让它们在站点上注册时指定其 Gravatar 地址的人。 (您可以了解如何让用户在注册[添加安全性和 ASP.NET Web Pages 站点的成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。)然后每当显示为该用户的信息，您可以只需将 Gravatar 添加到其中显示用户的名称。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
2. 创建一个名为的新 web 页*Gravatar.cshtml*。
3. 将以下标记添加到文件： 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml`方法，该页显示 Gravatar 图像。 若要更改图像的大小，可以作为第二个参数包含一个数字。 默认大小为 80。 数字少于 80 使映像更小。 大于 80 使映像更大的数字。
4. 在中`Gravatar.GetHtml`方法，将替换`<Your Gravatar account here>`Gravatar 帐户使用的电子邮件地址。 （如果没有 Gravatar 帐户，你可以使用能力的人员合作的电子邮件的地址）。
5. 在浏览器中运行页。 该页面显示您指定的电子邮件地址的两个 Gravatar 图像。 第二个图像是比第一个较小。 

    ![图 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>显示 Xbox 玩家卡

当人们可以玩 Microsoft Xbox 联机游戏时，每个用户具有唯一的 id。 为玩家卡，其中显示其信誉、 玩家分数，最近播放游戏的窗体中的每个玩家保留统计信息。 如果你是 Xbox 玩家，可以显示玩家卡在你的站点中的页上通过使用`GamerCard`帮助器。

1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
2. 创建一个名为的新页*XboxGamer.cshtml*并添加以下标记。

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    您使用`GamerCard.GetHtml`属性来指定要显示的玩家卡片的别名。
3. 在浏览器中运行页。 该页面显示您指定的 Xbox 玩家卡。

    ![图 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
