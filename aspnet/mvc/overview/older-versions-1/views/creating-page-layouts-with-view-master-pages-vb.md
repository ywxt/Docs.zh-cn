---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 使用视图母版页 (VB) 创建页面布局 |Microsoft Docs
author: microsoft
description: 在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。 可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ff74b1dc1d83b7ec1c8ecf6eca341a5cd14403f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824437"
---
<a name="creating-page-layouts-with-view-master-pages-vb"></a>使用视图母版页 (VB) 创建页面布局
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。 可用于视图的主页面，例如，定义两列的页面布局和两列布局用于所有 web 应用程序中的页。


## <a name="creating-page-layouts-with-view-master-pages"></a>使用视图母版页创建页面布局

在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。 可用于视图的主页面，例如，定义两列的页面布局和两列布局用于所有 web 应用程序中的页。

您还可以利用视图的主页面，用于跨应用程序中的多个页共享常见的内容。 例如，您可以在视图母版页中将网站徽标、 导航链接和横幅广告。 这样一来，在应用程序中的每一页将自动显示此内容。

在本教程中，您将了解如何创建新视图母版页，并创建新视图内容页基于母版页。

### <a name="creating-a-view-master-page"></a>创建视图母版页

让我们首先创建定义了两列布局视图母版页。 您将添加新视图母版页到 MVC 项目，请右键单击 views/shared 文件夹中，选择菜单选项**添加、 新项**，并选择 MVC 视图母版页模板 （参见图 1）。


[![添加视图母版页](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**图 01**： 添加视图母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))


应用程序中，可以创建多个视图母版页。 每个视图母版页可以定义不同的页面布局。 例如，您可能希望某些页具有两列布局和其他页面具有三列布局。

视图的主页面看起来很像标准的 ASP.NET MVC 视图。 但是，与普通视图中，不同视图母版页包含一个或多个`<asp:ContentPlaceHolder>`标记。 `<contentplaceholder>`标记用于标记可以在单个内容页面中重写的母版页的区域。

例如，在列表 1 中的视图母版页定义两列布局。 它包含两个`<contentplaceholder>`标记。 一个`<ContentPlaceHolder>`的每个列。

**代码清单 1 – `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

在列表 1 中的主页面包含两个视图的正文`<div>`对应于两个列的标记。 级联样式表的列类应用于这两`<div>`标记。 此类定义中声明顶部的主页面的样式表。 您可以预览视图母版页通过切换到设计视图中的呈现方式。 单击左下角的源代码编辑器的设计选项卡 （请参见图 2）。


[![预览设计器中的母版页](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**图 02**： 预览设计器中的母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))


### <a name="creating-a-view-content-page"></a>创建视图内容页

创建视图母版页后，您可以创建一个或多个视图基于视图母版页的内容页面。 例如，可以通过右键单击 views/home 文件夹中，创建主控制器的索引视图内容页选择**添加、 新建项**，选择**MVC 视图内容页**模板中，输入名称 Index.aspx，并单击添加按钮 （请参见图 3）。


[![添加视图内容页](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**图 03**： 添加视图内容页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))


单击添加按钮后，新会出现一个对话框，可用于选择要将视图内容页与相关联的视图主页面 （请参阅图 4）。 您可以导航到 Site.master 视图母版页，我们在上一节中创建。


[![选择母版页](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**图 04**： 选择一个母版页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))


创建新视图内容页基于 Site.master 母版页后，获取代码清单 2 中的文件。

**代码清单 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

请注意，此视图包含`<asp:Content>`对应于每个标记`<asp:ContentPlaceHolder>`视图母版页中的标记。 每个`<asp:Content>`标记包含指向特定 ContentPlaceHolderID 属性`<asp:ContentPlaceHolder>`它重写。

此外，请注意，代码清单 2 中的内容视图页不包含任何普通的开始和结束 HTML 标记。 例如，它不包含在开始和结束`<html>`或`<head>`标记。 正常的开始和结束标记的所有包含在视图母版页。

你想要在视图内容页中显示任何内容必须位于`<asp:Content>`标记。 如果将任何 HTML 或这些标记之外的其他内容，然后当您尝试查看的页面时将会出错。

无需重写每个`<asp:ContentPlaceHolder>`从母版页内容视图页中的标记。 只需重写`<asp:ContentPlaceHolder>`标记时想要将标记替换为特定的内容。

例如，清单 3 中的已修改的索引视图仅包含两个`<asp:Content>`标记。 每个`<asp:Content>`标记包含一些文本。

**代码清单 3 – `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

当请求清单 3 中的视图时，它将呈现在图 5 中的页。 请注意视图呈现的页面包含两个列。 此外，请注意，从视图内容页的内容将与来自视图母版页的内容合并。


[![索引视图内容页](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**图 05**： 该索引视图内容页 ([单击以查看实际尺寸的图像](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))


### <a name="modifying-view-master-page-content"></a>修改查看主页面内容

使用视图母版页时立即几乎会遇到的一个问题是修改视图母版页内容，当请求不同的视图内容页时的问题。 例如，希望每个页面中将 web 应用程序具有唯一的标题。 但是，标题被声明视图母版页中并不在视图内容页。 因此，如何执行自定义每个视图内容页的页面标题？

有两种方法，你可以修改视图内容页所显示的标题。 首先，将分配到的 title 属性页标题`<%@ page %>`指令声明顶部的视图内容页。 例如，如果你想要将页标题"超级出色的网站"分配给索引视图，您可以包括在索引视图的顶部的以下指令：

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

索引视图呈现给浏览器，浏览器标题栏中会显示所需的标题：


[![浏览器标题栏](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)


没有母版视图页中的 title 属性，若要运行的顺序必须满足的一个重要要求。 必须包含视图母版页`<head runat="server">`而不是普通的标记`<head>`其标头标记。 如果`<head>`标记不包含 runat ="server"特性，则不会显示标题。 母版页包含所需的默认视图`<head runat="server">`标记。

从单独的视图内容页修改母版页内容的备用方法是以包装您想要在修改的区域`<asp:ContentPlaceHolder>`标记。 例如，假设你想要更改不仅标题，而且还呈现的母版视图页的 meta 标记。 列表 4 中的母版视图页包含`<asp:ContentPlaceHolder>`标记内其`<head>`标记。

**列表 4 – `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

请注意，`<asp:ContentPlaceHolder>`列表 4 中的标记包括默认内容： 默认标题和默认 meta 标记。 如果不替代这`<asp:ContentPlaceHolder>`标记中单独的视图内容页上，则将显示默认内容。

列表 5 中的内容视图页重写`<asp:ContentPlaceHolder>`以便显示一个自定义标题和自定义 meta 标记的标记。

**列表 5 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>总结

本教程向你提供的基本介绍查看母版页和内容页面。 您学习了如何创建新视图母版页和创建基于它们的视图内容页。 我们还探讨了如何修改视图母版页从特定视图内容页的内容。

> [!div class="step-by-step"]
> [上一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [下一页](passing-data-to-view-master-pages-vb.md)
