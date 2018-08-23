---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第 4 部分： 列出了所有产品 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 4 部分介绍了列出产品使用 GridView contr....
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: ca7eccd684473d9a1ec4a8adfd8690b291fe702f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834276"
---
<a name="part-4-listing-products"></a>第 4 部分： 列出产品
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 4 部分介绍如何列出产品使用 GridView 控件。


## <a id="_Toc260221670"></a>  列出了所有产品使用 GridView 控件

让我们开始在我们的解决方案，并选择"添加"和"新建项"通过"右键单击"实现我们 ProductsList.aspx 页。

![](tailspin-spyworks-part-4/_static/image1.jpg)

选择"Web 窗体使用母版页"并输入页名称为 ProductsList.aspx"。

单击"添加"。

![](tailspin-spyworks-part-4/_static/image2.jpg)

接下来选择其中我们放置 Site.Master 页的"样式"文件夹并从"文件夹的内容"窗口中选择它。

![](tailspin-spyworks-part-4/_static/image3.jpg)

单击"确定"以创建页。

我们的数据库填充产品数据，如下所示。

![](tailspin-spyworks-part-4/_static/image4.jpg)

创建我们的页面后我们将再次使用实体数据源来访问该产品数据，但我们需要在此实例中选择的产品实体，我们需要限制为仅所选类别返回的项。

若要完成此我们将告诉 EntityDataSource 到自动生成 WHERE 子句，并且我们将指定 WhereParameter。

您会记得，我们在我们"产品类别菜单"中创建菜单项时我们动态生成链接通过将 CatagoryID 添加到每个链接在查询字符串。 我们将告诉实体数据源为位置参数派生的查询字符串参数。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

接下来，我们将配置 ListView 控件来显示产品列表。 若要创建最佳购物体验，我们将压缩到我们 ListVew 中显示的每个产品的几种简洁的功能。

- 产品名称将是该产品的详细信息视图的链接。
- 将显示产品的价格。
- 将显示产品的图像，我们将动态选择的图像目录 images 目录从我们的应用程序中。
- 我们将包含一个链接，立即将特定的产品添加到购物车。

下面是我们 ListView 控件实例的标记。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

我们正在动态创建每个显示的产品的多个的链接。

此外，我们测试自己的新页面之前我们需要创建目录结构的产品目录映像，如下所示。

![](tailspin-spyworks-part-4/_static/image1.png)

访问我们产品的映像后我们可以测试我们的产品列表页面。

![](tailspin-spyworks-part-4/_static/image5.jpg)

在站点的主页上，单击其中一个类别列表链接。

![](tailspin-spyworks-part-4/_static/image6.jpg)

现在，我们需要实现 ProductDetials.apsx 页和 AddToCart 功能。

使用文件-&gt;新建以创建页名称 ProductDetails.aspx 我们像以前一样使用站点的母版页。

我们将再次使用 EntityDataSource 控件来访问数据库中的特定产品记录，我们将运用 ASP.NET FormView 控件来显示产品数据，如下所示。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

如果格式设置一个看起来有点很好笑，您不必担心。 上面的标记留出空间显示布局中的几个更高版本，我们将实现的功能。

购物车将表示在应用程序中更复杂的逻辑。 若要开始，使用文件-&gt;新建以创建名为 MyShoppingCart.aspx 页。

请注意，我们不会选择 ShoppingCart.aspx 的名称。

我们的数据库包含名为"ShoppingCart"的表。 我们生成实体数据模型时为数据库中每个表已创建的类。 因此，实体数据模型生成一个名为"ShoppingCart"的实体类。 我们无法编辑该模型，以便我们可以使用我们的购物车实现该名称或将其扩展为我们的需求，但我们将避免发生冲突的名称只需选择在前面为改为选择。

它也是值得注意的，我们将创建简单购物车和购物车显示嵌入的购物车逻辑。 我们还可以选择在完全独立的业务层中实现我们的购物车。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-3.md)
> [下一页](tailspin-spyworks-part-5.md)
