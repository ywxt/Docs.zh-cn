---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 显示地图中 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在基于映射提供必应、 Google、 Ma 的服务的 ASP.NET Web Pages (Razor) 网站中的页面上显示互动地图...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: cde27c54b11ee91b193dffd61e3a354c6cf2449a
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020979"
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web Pages (Razor) 站点中显示地图
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在基于映射的必应、 Google、 MapQuest 和 Yahoo 提供服务的 ASP.NET Web Pages (Razor) 网站中的页上显示互动地图。
> 
> 你将学习：
> 
> - 如何生成基于地址的映射。
> - 如何生成地图基于纬度和经度坐标。
> - 如何注册必应地图开发人员帐户，并获得用于必应地图密钥。
> 
> 这是引入一文中的 ASP.NET 功能：
> 
> - `Maps`帮助器。
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


在 Web 页中，您可以映射在页面上显示通过使用`Maps`帮助器。 你可以生成基于一个地址或一组的经度和纬度坐标的地图。 `Maps`类，可以包括必应、 Google、 MapQuest 和 Yahoo 的常用映射引擎调用。

向页面添加映射的步骤是相同的调用无论哪个映射引擎的。 只需添加使可用方法显示映射的 JavaScript 文件引用，然后调用的方法`Maps`帮助器。

选择一项基于在其上映射服务`Maps`所使用的帮助器方法。 可以使用其中的任何：

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>安装所需的组件

若要显示映射，需要这些项：

- `Maps`帮助器。 此帮助器是版本 2 的 ASP.NET Web Helpers Library 中。 如果你尚未添加到库，你可以安装它在你的站点中作为 NuGet 包。 有关详细信息，请参阅[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)。 (在库中，搜索`microsoft-web-helpers`包。)
- JQuery 库。 WebMatrix 网站模板的几个已包含中的 jQuery 库及其*脚本*文件夹。 如果您不具备这些库，则可以下载最新的 jQuery 库直接从[jQuery.org](http://jQuery.org)站点。 也可以创建新的站点使用模板 (例如，**入门网站**模板) 然后将 jQuery 文件从该站点复制到当前站点。

最后，如果你想要使用必应地图，必须先创建一个 （免费） 帐户，并获取密钥。 若要获取密钥，请执行以下步骤：

1. 在创建帐户[必应地图开发人员帐户](https://www.microsoft.com/maps/developers/web.aspx)。 必须具有 Microsoft 帐户 (Windows Live ID)。

    您可以指定你想要使用的键**评估/测试**。 如果要在自己计算机上使用 WebMatrix 和 IIS Express 测试映射函数，请转**站点**工作区并记下你站点的 URL (例如， `http://localhost:50408`，尽管端口号可能会不同)。 可以使用此*localhost*为注册时的站点的地址。
2. 注册帐户后，请转到 Bing Maps 帐户中心，然后单击**创建或查看键**:

    ![映射 2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. 记录必应创建的密钥。

## <a name="creating-a-map-based-on-an-address-using-google"></a>创建基于 （使用 Google） 的地址映射

下面的示例演示如何创建一个页面，呈现基于地址的映射。 此示例演示如何使用 Google 地图。

1. 创建名为的文件*MapAddress.cshtml*站点的根目录中。 此页面将生成基于将传递给它的地址的映射。
2. 将以下代码复制到文件中，覆盖现有内容。

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    请注意，页上的以下功能：

    - `<script>`中的元素`<head>`元素。 在示例中，`<script>`元素引用*jquery 1.6.4.min.js*文件，它是 jQuery 库，版本 1.6.4 （压缩） 的简化的版本。 请注意，引用假设 *.js*文件位于*脚本*你的网站的文件夹。 

        > [!NOTE]
        > 如果您使用的 jQuery 库的不同版本，只需确保，所指该版本正确。
    - 对调用`@Maps.GetGoogleHtml`页的正文中。 若要查找某个地址，必须传递地址字符串。 其他映射引擎的方法的工作方式类似 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。
3. 运行该页并输入一个地址。 该页将显示基于 Google 地图，显示你指定的位置的映射。

     ![映射-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>创建地图基于纬度和经度坐标 （使用必应）

此示例演示如何创建基于坐标的映射。 此示例演示如何使用必应地图以及如何包含必应密钥。 （您可以创建基于坐标此外，使用其他映射引擎，而不使用必应密钥映射）。

1. 创建名为的文件*MapCoordinates.cshtml*替换其中包含以下代码和标记的现有内容的站点的根目录中：

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. 替换为`your-key-here`使用先前生成的必应地图密钥。
3. 运行*MapCoordinates.cshtml*页上，输入纬度和经度坐标，然后单击**Map It ！** 按钮。 （如果不知道任何坐标，尝试以下操作。 这是在 Microsoft 雷蒙德园区的位置）。

   - 纬度： 47.6781005859375
   - 经度：-122.158317565918

     使用指定的坐标显示的页。

     ![映射 3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[Microsoft.Maps API 参考](https://msdn.microsoft.com/library/gg427611.aspx)
