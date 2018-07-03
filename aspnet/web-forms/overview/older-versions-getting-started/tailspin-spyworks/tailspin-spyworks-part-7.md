---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第 7 部分： 添加功能 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 7 部分添加了其他功能，例如查看帐户...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 8cdde10981835877e5ac2f65860010920a68d0a2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389171"
---
<a name="part-7-adding-features"></a>第 7 部分： 添加功能
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 7 部分添加了其他功能，如帐户查看、 产品评论和"常用项"和"还已购买"用户控件。


## <a id="_Toc260221673"></a>  添加功能

尽管用户可以浏览我们的目录，将项放在其购物车中并完成结帐过程，有大量的支持功能，我们将包括提高我们的站点。

1. 帐户评审 （列表订单放置和查看详细信息。）
2. 将一些上下文特定内容添加到首页。
3. 在目录中添加特定功能，让用户查看的产品。
4. 创建用户控件以在首页上显示控制的热门项目和位置。
5. 创建"同时购买"的用户控件并将其添加到产品详细信息页。
6. 添加联系人页面。
7. 添加一页。
8. 全局错误

## <a id="_Toc260221674"></a>  帐户查看

在"帐户"文件夹中创建一个名为的 OrderList.aspx 和其他命名的 OrderDetails.aspx 的两个.aspx 页

OrderList.aspx 一样使用以前，我们将利用 GridView 和 EntityDataSoure 控件。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSoure 用户名已筛选的 Orders 表中选择记录 （请参阅 WhereParameter） 的用户日志时，我们设置会话变量中。

另请注意这些参数中的 GridView HyperlinkField:

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

这些名称指定作为 OrderDetails.aspx 页的查询字符串参数中指定的订单 id 字段的每个产品的订单详细信息视图的链接。

## <a id="_Toc260221675"></a>  OrderDetails.aspx

我们将使用 EntityDataSource 控件访问订单和 FormView 以显示订单数据和与 GridView 的另一个 EntityDataSource 可显示所有订单的明细项目。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

代码隐藏文件 (OrderDetails.aspx.cs) 中我们将两个小部分内部管理。

首先，我们需要确保 OrderDetails 始终获取 OrderId。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

我们还需要计算和显示订单行项总计。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>  主页页面

让我们将某些静态内容添加到 Default.aspx 页。

首先，我将创建一个"内容"文件夹并在该映像文件夹 （和我在这里提供要使用的主页上的图像。）

到 Default.aspx 页的底部占位符，添加以下标记。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>  产品评论

首先我们将我们可以使用输入产品评论的窗体添加一个具有一个链接按钮。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

请注意我们在查询字符串中传递 ProductID

下一步让我们将添加名为 ReviewAdd.aspx 页

此页将使用 ASP.NET AJAX 控件工具包。 如果你尚未做使您能够下载其从[DevExpress](http://devexpress.com/act)并且没有指南上设置用于与 Visual Studio 配合使用此处的工具包[ https://www.asp.net/learn/ajax-videos/video-76.aspx ](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)。

在设计模式下，从工具箱拖动控件和验证程序并生成类似于下面的窗体。

![](tailspin-spyworks-part-7/_static/image2.jpg)

标记将如下所示。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

现在，我们可以输入评论，允许在产品页上显示这些评论。

将此标记添加到 ProductDetails.aspx 页。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

运行应用程序现在并导航到产品显示产品信息包括客户的审阅。

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>  热门项目控件 （创建用户控件）

为了提高对您的网站的销售我们将添加到"暗示性销售"常用或相关产品的几个功能。

这些功能的第一个是在我们的产品目录的更多热门产品列表。

我们将创建一个"用户控件"以显示销售项在主页上我们的应用程序的顶部。 因为这将为一个控件，所以我们可以使用它在任何页上通过只需拖放控件拖到我们喜欢的任何页面上的 Visual Studio 设计器中。

在 Visual Studio 的解决方案资源管理器，右键单击解决方案名称并创建一个名为"控件"的新目录。 虽然不需要执行此操作，我们将帮助使我们的项目中按"控件"目录中创建我们的所有用户控件。

右键单击控件文件夹并选择"新建项":

![](tailspin-spyworks-part-7/_static/image4.jpg)

指定"PopularItems"我们控件的名称。 请注意，用户控件的文件扩展名是.ascx 不.aspx。

将按如下所示定义我们的常见项的用户控件。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

此处我们使用我们没有尚未使用此应用程序中的方法。 我们使用 repeater 控件，而不使用数据源控件我们将绑定到 LINQ to Entities 查询的结果 Repeater 控件。

我们的控制代码隐藏中我们执行该操作，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

另请注意此重要的一行在我们的控件的标记的顶部。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

由于最受欢迎的项不会更改按分钟，因此我们可以添加 aching 的指令以提高我们的应用程序的性能。 此指令将导致该控件的缓存的输出过期时才可执行的控件代码。 否则，将使用的控件的输出缓存的版本。

现在我们所要做的就是在我们 Default.aspc 页中包含我们新的控件。

使用拖放打开列的默认窗体中放置控件的实例。

![](tailspin-spyworks-part-7/_static/image5.jpg)

现在当我们运行我们的应用程序主页上显示的最受欢迎的项。

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>  "同时购买"控件 （使用参数的用户控件）

我们将创建第二个用户控件需要暗示性通过添加上下文特异性销售一层楼。

若要计算的前"同时购买"项的逻辑很重要。

我们"同时购买"的控件将当前所选 productid 选择 （之前购买） 的 OrderDetails 记录并获取有关位于每个唯一订单 Orderid。

然后我们将选择所有的产品从所有这些订单和购买所需数量的总和。 我们将通过该数量之和对产品进行排序和显示的前五个项目。

考虑到此逻辑的复杂性，我们将为存储过程来实现此算法。

T-SQL 存储过程是按如下所示。

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

请注意，当我们在我们的应用程序，我们生成我们指定的除了的表和视图，我们需要实体数据模型的实体数据模型时包括，此存储的过程 (SelectPurchasedWithProducts) 存在于数据库中应包含此存储的过程。

若要从实体数据模型访问存储的过程，我们需要将函数导入。

双击实体数据模型在解决方案资源管理器在设计器中打开它并打开模型浏览器，然后在设计器中右键单击并选择"添加函数导入"。

![](tailspin-spyworks-part-7/_static/image1.png)

执行此操作将打开此对话框。

![](tailspin-spyworks-part-7/_static/image2.png)

填写字段，正如您看到的更高版本，选择"SelectPurchasedWithProducts"并使用我们已导入函数的名称的过程名称。

单击"确定"。

完成后此我们可以针对存储过程只是程序，因为我们可能会在模型中的任何其他项。

因此，我们"控件"文件夹中创建名为 AlsoPurchased.ascx 的新用户控件。

此控件的标记看上去很眼熟 PopularItems 控制。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

明显的区别是，不缓存的输出，因为项的呈现将因产品。

产品 id 将是到该控件的"属性"。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

控件的 PreRender 事件处理程序中我们 eed 来做三件事。

1. 请确保设置 ProductID。
2. 查看是否存在与当前已购买任何产品。
3. 输出为在 #2 中确定一些项。

请注意调用存储的过程通过模型是多么容易。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

确定，那里"还需购买"后我们可以只需绑定 repeater 到由查询返回的结果。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

如果不是"同时购买"的任何项我们只需将从我们的目录中显示其他常用的项。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

若要查看"同时购买"项，请打开 ProductDetails.aspx 页并从解决方案资源管理器拖动 AlsoPurchased 控件，它出现在标记中的此位置。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

执行此操作将在 ProductDetails 页的顶部创建对控件的引用。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

由于 AlsoPurchased 用户控件需要产品 Id 号，因此我们将使用针对页的当前数据模型项的 Eval 语句设置我们的控件的 ProductID 属性。

![](tailspin-spyworks-part-7/_static/image3.png)

当我们构建并立即运行并浏览到某个产品时我们会看到"同时购买"项。

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-6.md)
> [下一页](tailspin-spyworks-part-8.md)
