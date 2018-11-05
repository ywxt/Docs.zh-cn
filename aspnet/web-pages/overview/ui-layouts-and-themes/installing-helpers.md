---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 安装帮助程序在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中安装一个帮助程序。 帮助器是包含代码和每个标记的可重用组件...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 5ad717cd7c64e830ce66d5e1361d0eb6ef3cbbec
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021360"
---
<a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages (Razor) 站点中安装一个帮助程序
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中安装一个帮助程序。 一个*帮助器*是一个可重用的组件，包括代码和标记来执行可能繁琐或复杂的任务。
> 
> 你将学习：
> 
> - 如何使用 WebMatrix 3 创建的网站中安装一个帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - WebMatrix 3


## <a name="overview-of-helpers"></a>帮助程序的概述

人们通常希望为在网页上某些任务需要大量的代码，或需要额外知识。 示例包括显示的图的数据;在页上; 中放置一个 Twitter"关注"按钮从你的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。 若要能够轻松执行此类目的，ASP.NET Web Pages 使您可以使用*帮助程序*。 帮助器是组件，安装适用于站点和，可让你使用只需一两行或 Razor 代码的两个执行的典型任务。

ASP.NET Web Pages 具有内置的几个帮助程序。 但是，使用 NuGet 包管理器提供的包 （加载项） 中提供了许多帮助程序。 NuGet，可以选择要安装的程序包，然后它就会完成安装的所有详细信息。

## <a name="installing-a-helper-in-webmatrix-3"></a>在 WebMatrix 3 中安装帮助程序

1. 在 WebMatrix 3 中，单击**NuGet**按钮。

    ![在 WebMatrix 中的 NuGet 库对话框](installing-helpers/_static/image1.png)
2. 这会启动 NuGet 包管理器，并显示可用的包。 在搜索框中，输入你想要安装的帮助器关键字。

    ![在 WebMatrix 中的 NuGet 库对话框](installing-helpers/_static/image2.png)
3. 选择包，然后单击**安装**。 单击**是**当系统询问你是否想要安装包，并指示接受条款。

     如果这是首次安装一个帮助程序，NuGet 在您的网站用于组成帮助程序的代码中创建文件夹。
4. 若要卸载程序的帮助程序，请单击**库**按钮，再单击**已安装**选项卡，然后选择你想要卸载的程序包。

## <a name="installing-the-twitter-helper"></a>安装 Twitter 帮助程序

Twitter API 的最新版本不兼容与 Twitter 帮助程序通过 NuGet 安装。 相反，请参阅[Twitter 帮助程序使用 WebMatrix](twitter-helper.md)主题，了解有关如何设置你的项目中的 Twitter 帮助程序的信息。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


[Introducing ASP.NET Web Pages 2-编程基础知识](../getting-started/introducing-razor-syntax-c.md)

[Twitter WebMatrix 帮助的器](twitter-helper.md)
