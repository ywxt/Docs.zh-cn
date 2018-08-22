---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第 3 部分： 布局和类别菜单 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 3 部分介绍如何添加布局和类别菜单。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: f55b29a271dbdb72d3e2249ed74517b77d78cf5e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825048"
---
<a name="part-3-layout-and-category-menu"></a>第 3 部分： 布局和类别菜单
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 3 部分介绍如何添加布局和类别菜单。


## <a id="_Toc260221669"></a>  添加一些布局和类别菜单

在我们站点的主页面中，我们将添加将包含我们的产品类别菜单的左侧和右侧列的 div。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

请注意，将由我们添加到我们 Style.css 文件的 CSS 类提供所需的对齐和其他格式设置。

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

产品类别菜单将动态创建在运行时通过查询商务数据库的现有产品类别以及创建菜单项和相应的链接。

若要完成此我们将使用两个 ASP。NET 的功能强大的数据控件。 "实体数据源"控件和"ListView"控件。

![](tailspin-spyworks-part-3/_static/image1.jpg)

让我们切换到"设计视图"和帮助程序用于配置我们的控件。

![](tailspin-spyworks-part-3/_static/image2.jpg)

让我们将 EntityDataSource ID 属性设置为 EDS\_类别\_菜单，并单击"配置数据源"。

![](tailspin-spyworks-part-3/_static/image3.jpg)

选择我们为我们的商务数据库创建实体数据源模型时为我们创建的 CommerceEntities 连接，然后单击"下一步"。

![](tailspin-spyworks-part-3/_static/image4.jpg)

选择"类别"实体集名称，并将其余选项为默认值。 单击"完成"。

现在让我们在我们对 ListView 的页面放置的 ListView 控件实例的 ID 属性设置\_ProductsMenu 并激活其帮助程序。

![](tailspin-spyworks-part-3/_static/image5.jpg)

不过我们可以使用控制选项设置数据的项显示的格式和格式设置，我们创建了菜单将只需要简单的标记以便将源视图中输入代码。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

请注意"Eval"语句： &lt;%# Eval("CategoryName") %&gt;

ASP.NET 语法&lt;%# %&gt;是指示运行时执行任何包含在中，输出结果"行"的速记约定。

语句 Eval("CategoryName") 指示，当前项的数据项时，绑定集合中提取实体模型项名称的值"CatagoryName"。 这是一个非常强大的功能的简洁语法。

让我们运行应用程序现在。

![](tailspin-spyworks-part-3/_static/image6.jpg)

请注意，现在显示我们的产品类别菜单和时我们将鼠标悬停在通过一个我们可以看到我们必须尚未实现的页的菜单项链接点的类别菜单项名为 ProductsList.aspx 并且，我们已经构建了一个动态查询字符串参数，包含 类别 id。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-2.md)
> [下一页](tailspin-spyworks-part-4.md)
