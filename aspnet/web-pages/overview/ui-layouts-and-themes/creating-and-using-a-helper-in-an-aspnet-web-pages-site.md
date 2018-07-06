---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 创建和使用一个帮助程序的 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中创建一个帮助程序。 帮助器是包含代码和标记对性能的可重用组件...
ms.author: aspnetcontent
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: c2edc10e01f4d2358dd0b0bdf450348f01eb2bfa
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811894"
---
<a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>创建和使用 ASP.NET 网页 (Razor) 站点中的一个帮助程序
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中创建一个帮助程序。 一个*帮助器*是一个可重用的组件，包括代码和标记来执行可能繁琐或复杂的任务。
> 
> **你将学习：** 
> 
> - 如何创建和使用简单的帮助程序。
> 
> 下面是在本文中引入的 ASP.NET 功能：
> 
> - `@helper`语法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


## <a name="overview-of-helpers"></a>帮助程序的概述

如果需要在站点中的不同页上执行相同的任务，可以使用一个帮助程序。 ASP.NET 网页包括大量的帮助程序，并且有许多数据越多，您可以下载并安装。 (一组内置帮助程序 ASP.NET Web Pages 中所示[ASP.NET API 快速参考](https://go.microsoft.com/fwlink/?LinkId=202907)。)如果现有的帮助程序都不能满足您的需要，可以创建自己的帮助器。

一个帮助程序允许您使用的多个页面的一个常见的代码块。 假设在您的页面通常要创建的注意项目的设置除了普通段落。 注意为创建的可能是`<div>`元素，具有的样式设置为具有边框的框。 而不是每次想要显示注释，此相同的标记添加到页面，可打包为一个帮助程序标记。 然后，您可以插入便笺的一行代码需要的任意位置。

使用此类的一个帮助程序使每个页面中的代码，更简单、 更容易阅读。 它还使得它更易于维护你的站点，因为如果需要更改外观的说明，你可以在一个位置的标记。

## <a name="creating-a-helper"></a>创建一个帮助程序

此过程演示如何创建帮助程序将创建便笺，按前面所述。 这是一个简单的示例，但自定义帮助程序可以包含任何标记和所需的 ASP.NET 代码。

1. 在该网站的根文件夹中，创建名为的文件夹*应用程序\_代码*。 这是在 ASP.NET 中的保留的文件夹名称可以放置的组件，如帮助程序的代码。
2. 在中*应用程序\_代码*文件夹中创建一个新 *.cshtml*文件并将其命名*MyHelpers.cshtml*。
3. 使用以下内容替换现有内容：

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    该代码使用`@helper`语法来声明一个新的帮助程序，名为`MakeNote`。 此特定的帮助器，可以传递参数名为`content`，可以包含的文本和标记组合。 帮助器将字符串插入到注意正文使用`@content`变量。

    请注意，该文件命名*MyHelpers.cshtml*，但帮助者名为`MakeNote`。 可以将多个自定义帮助程序放入单个文件。
4. 保存并关闭文件。

## <a name="using-the-helper-in-a-page"></a>在页面中使用该帮助器

1. 在根文件夹中，创建新的空白文件称为*TestHelper.cshtml*。
2. 向文件中添加以下代码：

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    若要调用帮助器创建，使用`@`跟的文件名，该帮助器位置后，一个点，然后帮助程序名称。 (如果在具有多个文件夹*应用程序\_代码*文件夹中，可以使用语法`@FolderName.FileName.HelperName`调用帮助者内任何嵌套的文件夹级别)。 在括号中的引号中添加的文本是说明的帮助程序将显示在网页中的一部分的文本。
3. 保存页面，并在浏览器中运行它。 帮助程序生成的注意项直接调用帮助程序的位置： 两个段落间。

    ![在浏览器以及如何帮助程序生成标记放入指定的文本周围的框中显示的页面的屏幕截图。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.jpg)

## <a name="additional-resources"></a>其他资源


[为 Razor 帮助器的水平菜单](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。 由 Mike 教皇此博客文章显示了如何创建使用标记、 CSS 和代码的帮助程序作为一个水平菜单。

[利用 ASP.NET Web 中的 HTML5 页帮助程序适用于 WebMatrix 和 ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。 由 Sam Abraham 此博客文章显示了一个帮助程序，将呈现一个 HTML5`Canvas`元素。

[之间的差异@Helpers并@Functions在 WebMatrix 中](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。 由 Mike Brind 此博客条目描述`@helper`语法和`@function`语法以及何时使用每个。
