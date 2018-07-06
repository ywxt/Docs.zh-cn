---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第 8 部分： 购物车与 Ajax 更新 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 8 部分介绍了购物车与 Ajax 更新。
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 881d47b5b4df5a4d310a1b3a7eec6ee97b0d42ea
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823834"
---
<a name="part-8-shopping-cart-with-ajax-updates"></a>第 8 部分： 购物车与 Ajax 更新
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 8 部分介绍了购物车与 Ajax 更新。


我们将允许用户在其购物车中将唱片集，而无需注册，但它们将需要注册作为完整签出的来宾。 购物和签出进程将分为两个控制器： 允许以匿名方式将项添加到购物车，购物车控制器和签出控制器用于处理在结帐过程。 我们将开始在此部分中，购物车，然后生成下一节中的签出过程。

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>添加购物车、 顺序和 OrderDetail 模型类

我们购物车和签出过程将使用的一些新类。 右键单击模型文件夹并添加具有下面的代码的购物车类 (Cart.cs)。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

此类是非常类似于其他我们使用了目前为止，除了 RecordId 属性 [键] 属性。 我们的购物车项将具有名为 CartID 以允许匿名购物的字符串标识符，但表包含名为记录 Id 的整数主键。 按照约定，Entity Framework 代码优先需要名为购物车的表的主键将是 CartId 或 ID，但我们可以轻松地重写的通过批注或代码如果我们希望。 这是举例说明如何使用简单约定在 Entity Framework 代码优先时适合我们，但我们不受它们时不提供。

接下来，使用以下代码添加 Order 类 (Order.cs)。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

此类跟踪有关订单的摘要和传递信息。 **它不会在尚未编译**，因为它具有一个 OrderDetails 导航属性，具体取决于我们尚未创建的类。 让我们来修复，现在通过添加一个类命名为 OrderDetail.cs，添加以下代码。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

我们将一个最后一次更新到我们 MusicStoreEntities 类，以包括公开这些新的模型类，还包括 DbSet 的 DbSets&lt;艺术家&gt;。 更新后的 MusicStoreEntities 类显示为如下。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>管理购物车业务逻辑

接下来，我们将在模型文件夹中创建的购物车类。 购物车模型处理对购物车表的数据访问。 此外，它将处理业务逻辑与用于添加和从购物车中删除项。

因为我们不希望要求用户注册一个帐户，只是为了向其购物车添加项，我们会将用户分配一个临时的唯一标识符 （使用 GUID 或全局唯一标识符） 时，他们访问购物车。 我们将存储此使用 ASP.NET 会话类的 ID。

*注意： ASP.NET 会话是很方便地存储特定于用户的信息将离开站点后到期。虽然不恰当使用会话状态的可能较大的站点上会影响性能，我们轻度使用将适用于演示目的。*

购物车类提供了以下方法：

**AddToCart**采用唱片集作为参数并将其添加到用户的购物车。 购物车表会跟踪每个唱片集的数量，因为它包括逻辑来根据需要创建一个新行或只是递增数量，如果用户具有已排序的唱片集的一个副本。

**RemoveFromCart**采用唱片集 ID，并将其从用户的购物车中删除。 如果用户仅在其购物车中有一份唱片集，删除的行。

**EmptyCart**从用户的购物车中移除所有项。

**GetCartItems**检索以便进行显示或处理 CartItems 的列表。

**GetCount**检索用户具有在其购物车中的唱片集的总数。

**GetTotal**计算购物车中的所有项的总成本。

**CreateOrder**签出阶段将购物车转换为订单。

**GetCart**是一种静态方法，可允许我们控制器，若要获取的购物车对象。 它使用**GetCartId**方法以处理从用户的会话读取 CartId。 GetCartId 方法，以便它可以从用户的会话中读取用户的 CartId 需要 HttpContextBase。

下面是完整**购物车类**:

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

购物车控制器将需要一些复杂的信息传递给其视图不会完全映射到我们的模型对象。 我们不想要修改我们的模型以满足我们的视图;模型类应表示我们的域，不在用户界面。 一种解决方案是将信息传递到我们使用 ViewBag 类，如我们一样存储管理器下拉列表中的信息，但是通过 ViewBag 传递的大量信息会变得难以管理的视图。

此解决方案是使用*ViewModel*模式。 使用此模式时我们将创建强类型化的类，针对我们特定视图的方案，进行了优化和其公开动态值/内容所需的视图模板的属性。 我们的控制器类可以填充，然后将这些视图优化类传递给我们要使用的视图模板。 这使类型安全、 编译时检查和编辑器 IntelliSense 中查看模板。

我们将在购物车控制器中创建两个视图模型，以用于： ShoppingCartViewModel 将保存用户的购物车的内容和 ShoppingCartRemoveViewModel 用于当用户删除内容时显示确认信息从其购物车。

让我们在我们为了使组织的内容的项目的根目录中创建新的 ViewModels 文件夹。 右键单击项目，选择添加 / 新的文件夹。

![](mvc-music-store-part-8/_static/image1.jpg)

名称 ViewModels 文件夹。

![](mvc-music-store-part-8/_static/image1.png)

接下来，在 Viewmodel 文件夹中添加 ShoppingCartViewModel 类。 它具有两个属性： 车商品和要在购物车中保存的所有项的总价格的十进制值的列表。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

现在添加 ShoppingCartRemoveViewModel ViewModels 文件夹中，使用以下四个属性。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>购物车控制器

购物车控制器有三个主要用途： 将项添加到购物车、 从购物车中，删除项和查看购物车中的项。 它将使用的三个类我们刚刚创建： ShoppingCartViewModel、 ShoppingCartRemoveViewModel 和购物车。 如下所示的 StoreController 和 StoreManagerController，我们将添加一个字段来保存 MusicStoreEntities 的实例。

使用空的控制器模板向项目添加一个新的购物车控制器。

![](mvc-music-store-part-8/_static/image2.png)

下面是完整的购物车控制器。 索引和添加控制器操作应该很熟悉。 删除和 CartSummary 控制器操作处理两种特殊情况，我们将在下一节中讨论。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>使用 jQuery Ajax 更新

接下来，我们将创建强类型化为 ShoppingCartViewModel 并使用列表视图模板使用与之前相同的方法的购物车索引页。

![](mvc-music-store-part-8/_static/image3.png)

但是，而不是使用 Html.ActionLink 从购物车中删除项目，我们将使用 jQuery"绑定"具有 HTML 类 RemoveLink 此视图中的所有链接的 click 事件。 而不是发布窗体，此 click 事件处理程序将只是对我们 RemoveFromCart 控制器操作进行 AJAX 回调。 RemoveFromCart 返回 JSON 序列化结果，其中我们 jQuery 回调，然后分析并执行四个快速更新为使用 jQuery 的页面：

- 1. 从列表中移除已删除的唱片集
- 2. 更新标头中的购物车计数
- 3. 为用户显示一则更新消息
- 4. 更新购物车的总价

由于索引视图中的 Ajax 回调处理删除方案，我们对于 RemoveFromCart 操作不需要的其他视图。 下面是 /ShoppingCart/Index 视图的完整代码：

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

若要对它进行测试，我们需要能够将项添加到我们的购物车。 我们将更新我们**存储详细信息**视图包括"添加到购物车"按钮。 虽然我们解决这个问题时，我们可以包括一些我们已添加唱片集其他信息由于我们上次更新此视图： 流派、 艺术家、 价格和唱片集画面。 更新的存储详细信息视图的代码显示如下所示。

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

现在我们可以单击通过应用商店和测试添加和删除 Album 到和从我们的购物车。 运行应用程序并浏览到存储索引。

![](mvc-music-store-part-8/_static/image4.png)

接下来，单击某个类型，以查看唱片集的列表。

![](mvc-music-store-part-8/_static/image5.png)

单击唱片集标题现在显示了我们已更新的唱片集的详细信息视图，包括"添加到购物车"按钮。

![](mvc-music-store-part-8/_static/image6.png)

单击"添加到购物车"按钮显示购物车索引视图与购物车摘要列表。

![](mvc-music-store-part-8/_static/image7.png)

加载您的购物车之后, 您可以单击在从购物车链接删除以查看放入购物车的 Ajax 更新。

![](mvc-music-store-part-8/_static/image8.png)

我们已构建了一个有效的购物车，它允许未注册的用户将项添加到购物车。 在以下部分中，我们将允许他们注册并完成结帐过程。


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-7.md)
> [下一页](mvc-music-store-part-9.md)
