---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 为移动设备呈现 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。 你将学习： 您如何...
ms.author: aspnetcontent
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: dcc44e0d78814ef9a8537b01efa17259a12e9c76
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816334"
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>为移动设备呈现 ASP.NET Web Pages (Razor) 站点
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。
> 
> 你将学习：
> 
> - 如何使用命名约定指定页专为移动设备。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


ASP.NET Web Pages 中，可以移动或其他设备上创建自定义呈现内容的显示。

在 ASP.NET Web Pages 站点中创建特定于设备的页面的最简单方法是使用此类文件命名模式：<em>文件名。</em><em>Mobile</em><em>.cshtml</em>。 可以创建两个版本的页面 (例如，一个名为<em>MyFile.cshtml</em>另一个名为<em>MyFile.Mobile.cshtml</em>)。 在运行的时，移动设备的请求时<em>MyFile.cshtml</em>，ASP.NET 将从内容呈现<em>MyFile.Mobile.cshtml</em>。 否则为<em>MyFile.cshtml</em>呈现。

下面的示例演示如何通过添加内容页的移动设备启用移动呈现。 *Page1.cshtml*包含内容，以及导航侧边栏。 *Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。

1. 在 ASP.NET Web Pages 站点中，创建名为的文件*Page1.cshtml*和当前的内容替换为以下标记。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. 创建名为的文件*Page1.Mobile.cshtml*和现有内容替换为以下标记。 请注意，页上的移动版本省略以便更好地呈现在较小屏幕上的导航部分。

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. 运行桌面浏览器并浏览到*Page1.cshtml*。 ![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. 运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。 (请注意，不包括 *.mobile。* 作为 URL 的一部分。）即使该请求是对*Page1.cshtml*，ASP.NET 会将*Page1.Mobile.cshtml*。

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> 若要测试移动页面，可以使用在桌面计算机运行的移动设备模拟器。 此工具允许您测试网页，如他们的移动设备上的外观 （即，通常使用小得多显示区域）。 模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)Mozilla firefox，它可以模拟各种移动浏览器，从桌面版本的 Firefox。


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[Windows Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
