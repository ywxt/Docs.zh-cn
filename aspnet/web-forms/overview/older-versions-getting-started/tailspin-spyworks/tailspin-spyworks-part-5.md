---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第 5 部分： 业务逻辑 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 5 部分将添加一些业务逻辑。
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: fdb73c01d7b6076bc292c640376aa35cc5f52ea6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827043"
---
<a name="part-5-business-logic"></a>第 5 部分： 业务逻辑
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 5 部分将添加一些业务逻辑。


## <a id="_Toc260221671"></a>  添加一些业务逻辑

我们希望每当有人访问我们的网站可我们购物体验。 访问者将能够浏览并将项添加到购物车，即使它们未注册或登录。 准备好要签出时他们将获得的选项进行身份验证，如果它们不是尚未成员他们将能够创建帐户。

这意味着，我们将需要实现逻辑以将购物车从匿名状态转换到"已注册用户"的状态。

让我们创建一个名为"类"，然后右键单击文件夹并创建名为 MyShoppingCart.cs 的新"类"文件

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

如前面提到过，我们会扩展实现 MyShoppingCart.aspx 页的类，我们将使用执行此类情况的操作。NET 的强大"分部类"构造。

我们 MyShoppingCart.aspx.cf 文件的生成的调用如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

请注意，使用 partial 关键字的使用。

我们只是生成的类文件如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

我们将通过将 partial 关键字添加到此文件合并我们的实现。

现在，我们的新类文件如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

第一种方法，我们将添加到我们的类是"AddItem"方法。 这是将最终用户单击产品列表和产品详细信息页上的"添加到艺术"链接时要调用的方法。

将以下内容追加到使用页面顶部的语句。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

并将以下方法添加到 MyShoppingCart 类。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

我们将使用 LINQ to Entities 来查看该项目是否已在购物车中。 如果因此，我们更新项的订单数量，否则我们创建所选的项的新项

若要调用此方法中，我们将实现不仅类此方法，但然后显示当前购物 = 购物车添加项之后的 AddToCart.aspx 页。

右键单击解决方案资源管理器中的解决方案名称，然后添加和名为 AddToCart.aspx，如我们以前所做的新页。

虽然我们无法使用此页以显示我们的实现如低库存问题等，临时结果，该页将实际上不会呈现，但而不是调用"添加"逻辑，重定向。

若要完成此我们将以下代码添加到页面\_加载事件。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

请注意，我们要检索的产品从查询字符串参数并调用我们的类的 AddItem 方法将添加到购物车。

假设没有错误遇到控制权将传递给我们将完全实现下一步使用 SHoppingCart.aspx 页。 如果应引发异常错误。

目前我们没有实现全局错误处理程序以便此异常将会通过我们的应用程序得到处理，但我们稍后将解决此问题。

另请注意语句 Debug.Fail() （可通过使用 `using System.Diagnostics;)`

是在调试器中运行该应用程序，此方法将显示一个详细的对话框，其中我们指定的错误消息以及应用程序状态信息。

当运行在生产环境 Debug.Fail() 语句中的将被忽略。

您会注意到我们购物车类名"GetShoppingCartId"中的方法调用上方的代码中。

添加代码以实现的方法，如下所示。

请注意，我们还添加了更新和签出按钮和标签，我们可以显示购物车"总计"。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

现在，我们可以将项添加到我们的购物车，但我们尚未实现逻辑以添加一个产品后显示购物车。

因此，MyShoppingCart.aspx 页中我们将添加 EntityDataSource 控件和 GridVire 控件，如下所示。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

调用启动的窗体设计器中，因此，可以双击更新购物车按钮，并生成的单击事件处理程序在标记声明中指定。

更高版本，我们将实现详细信息，但执行此操作会让我们生成并运行我们的应用程序未出现错误。

运行应用程序并将项添加到购物车时将看到此。

![](tailspin-spyworks-part-5/_static/image2.jpg)

请注意，我们没有遵循"默认"网格显示通过实现三个自定义列。

第一个是一种可编辑、"绑定"字段的数量：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

下一步是"计算"列显示行项总计 （项的成本的乘积的数量进行排序）：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

最后，我们有一个包含用户将用于指示应从购物图表移除的项的复选框控件的自定义列。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

正如您所看到的因此，让我们为空总的行的顺序将添加一些逻辑以计算订单总计。

首先，我们将向我们 MyShoppingCart 类实现"GetTotal"方法。

MyShoppingCart.cs 文件中添加以下代码。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

然后在页面\_Load 事件处理程序，我们将可以调用我们 GetTotal 方法。 同时，我们将添加一个测试，以查看购物车是否为空并相应地调整显示，如果它是。

现在如果购物车中没有我们得到如下结果：

![](tailspin-spyworks-part-5/_static/image4.jpg)

如果不是，我们看到我们总共。

![](tailspin-spyworks-part-5/_static/image5.jpg)

但是，此页尚未完成。

我们将需要额外的逻辑，以便重新计算购物车中删除标记为待删除的项和一些可能已更改网格中由用户确定新数量值。

允许添加到购物车类 MyShoppingCart.cs 来处理这种情况，用户将标记为删除的项中的"RemoveItem"方法。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

现在让我们 ad 处理用户只需更改质量 GridView 中进行排序时所处环境的方法。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

与位置中的基本进行删除和更新功能，我们可以实施实际更新购物车中数据库的逻辑。 （在 MyShoppingCart.cs)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

您会注意此方法需要两个参数。 一个购物车 Id，另一个是用户定义类型的对象的数组。

以尽可能减少我们用户接口细节的逻辑的依赖关系，我们定义了可用于将购物车商品传递给我们的代码，而无需我们无需直接访问 GridView 控件的方法的数据结构。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

在我们的 MyShoppingCart.aspx.cs 文件可以使用此结构在我们的更新按钮单击事件处理程序中，如下所示。 请注意，除了更新购物车我们将更新购物车总计以及。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

请注意这行代码与特定的感兴趣：

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues() 是一个特殊的 helper 函数，我们会在中实现 MyShoppingCart.aspx.cs，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

这提供了简洁的方式来访问我们的 GridView 控件中的绑定元素的值。 由于我们的"删除项"复选框控件未绑定，因此我们将通过 FindControl() 方法来访问它。

在此阶段在你的项目的开发过程中我们已准备好实施签出过程。

让我们执行此操作之前使用 Visual Studio 生成成员资格数据库并将用户添加到成员身份存储库。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-4.md)
> [下一页](tailspin-spyworks-part-6.md)
