---
uid: web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
title: 运行不同版本的 ASP.NET Web Pages (Razor) 同时 |Microsoft Docs
author: Rick-Anderson
description: 此文章介绍了如何在同一个计算机或服务器上运行 ASP.NET Web Pages (Razor) 网站，网站配置为使用不同版本时...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: a861409b-4ae6-4868-9e09-87edfac3535f
msc.legacyurl: /web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
msc.type: authoredcontent
ms.openlocfilehash: e587398b430795c12a1dcee394852b4e2b8a0e44
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021166"
---
<a name="running-different-versions-of-aspnet-web-pages-razor-side-by-side"></a>并行运行不同版本的 ASP.NET 网页 (Razor)
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在网站配置为使用不同版本的 ASP.NET Web Pages 时相同的计算机或服务器上运行 ASP.NET Web Pages (Razor) 网站。
> 
> 你将学习：
> 
> - 什么的默认行为是在 ASP.NET 中，有时生成与 ASP.NET Web Pages 站点。
> - 如何配置新站点以使用较旧版本的 ASP.NET Web Pages 运行。
>   
> 
> 这是引入一文中的 ASP.NET 功能：
> 
> - `webPages:Version`配置设置。
>   
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。


ASP.NET Web Pages 支持能够运行网站并排显示。 这样可以继续运行较旧的 ASP.NET Web Pages 应用程序，构建新的 ASP.NET Web Pages 应用程序，并在同一台计算机上运行所有这些。

下面是要使用 WebMatrix 安装 Web 页时，应注意一些事项：

- 默认情况下，现有的 Web Pages 应用程序将在计算机上运行的最新版本。 （程序集在全局程序集缓存 (GAC) 中安装和自动使用。）
- 如果你想要运行使用不同版本的 ASP.NET Web Pages 站点，可以配置要执行此操作的站点。 如果您的网站还没有*web.config*文件位于站点的根目录中，创建一个新，并将以下 XML 复制到其中，覆盖现有内容。 如果站点中已包含*web.config*文件中，添加`<appSettings>`元素到如下`<configuration>`部分。

    [!code-xml[Main](running-v1-and-v2-sites-side-by-side/samples/sample1.xml)]
  -如果未指定的版本中*web.config*文件中，将站点部署为最新版本。 (程序集复制到*bin*已部署站点中的文件夹。)
- 创建使用 Web Matrix 中的站点模板的新应用程序在站点中包括网页版程序集*bin*文件夹。

一般情况下，您可以始终控制 Web 页以使用你的网站，通过使用 NuGet 将相应的程序集安装到站点的哪些版本*bin*文件夹。 若要查找程序包，请访问[NuGet.org](http://NuGet.org)。

## <a name="additional-resources"></a>其他资源

[ASP.NET Web Pages 2 中的常用功能](top-features-in-web-pages-2.md)
