---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第 9 部分： 注册和结帐 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 9 部分介绍如何注册和签出。
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: e521e30cb820d834d57c87538b869861a536657b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812868"
---
<a name="part-9-registration-and-checkout"></a>第 9 部分： 注册和结帐
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 9 部分介绍如何注册和签出。


在本部分中，我们将创建 CheckoutController 会收集购物者的地址和付款信息。 我们将要求用户注册我们的站点之前签出，因此，此控制器将需要授权。

用户将导航到结帐过程从其购物车通过单击"结帐"按钮。

![](mvc-music-store-part-9/_static/image1.jpg)

如果用户未登录，则它们将提示。

![](mvc-music-store-part-9/_static/image1.png)

成功登录后，用户将显示地址和付款视图。

![](mvc-music-store-part-9/_static/image2.png)

它们具有填充窗体并提交订单后，将向他们显示订单确认屏幕。

![](mvc-music-store-part-9/_static/image3.png)

尝试查看，不存在订单或不属于您的订单将显示错误视图。

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>迁移购物车

尽管购物过程是匿名的当用户单击签出按钮时，它们将需要注册和登录名。 用户希望我们在保持其购物车信息之间的访问中，因此我们将需要在它们完成注册或登录名与用户相关联的购物车信息。

这实际上是非常简单，因为我们的购物车类已有一种方法可将与用户名关联在当前的购物车中的所有项。 我们只需调用此方法，当用户完成注册或登录名。

打开**AccountController**时我们已设置的成员身份和授权，我们添加的类。 添加 using 语句引用 MvcMusicStore.Models，然后添加以下 MigrateShoppingCart 方法：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

接下来，修改登录 post 操作调用 MigrateShoppingCart 后已验证用户，如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

做出相同更改到寄存器后操作，用户帐户已成功创建后立即：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

就这么简单-现在匿名的购物车将自动传输到后成功注册或登录名的用户帐户。

## <a name="creating-the-checkoutcontroller"></a>创建 CheckoutController

右键单击 Controllers 文件夹并将新的控制器添加到名为 CheckoutController 使用空的控制器模板的项目。

![](mvc-music-store-part-9/_static/image5.png)

首先，添加控制器类声明，以要求用户在签出之前注册的上面 Authorize 属性：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*注意： 这是类似于我们先前对 StoreManagerController，所做的更改，但在这种情况下 Authorize 属性所需的用户是管理员角色中。在签出控制器中，我们要求用户登录，但不需要它们管理员。*

为简单起见，我们不会处理在本教程中的付款信息。 相反，我们允许用户签出使用促销代码。 我们将存储此促销代码中使用一个名为 PromoCode 常量。

如下所示 StoreController，我们将声明一个字段来保存的名为 storeDB MusicStoreEntities 类实例。 为了使 MusicStoreEntities 类的使用，我们将需要添加一个 using 语句 MvcMusicStore.Models 命名空间。 签出控制器的顶部如下所示。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController 将具有以下控制器操作：

**AddressAndPayment （GET 方法）** 将显示一个窗体以允许用户输入他们的信息。

**AddressAndPayment （POST 方法）** 将验证输入和处理订单。

**完整**用户已成功完成结帐过程后将显示。 此视图将包括用户的订单号，以确认。

首先，让我们将索引控制器操作 （这我们创建控制器时生成） 重命名为 AddressAndPayment。 此控制器操作只是显示签出窗体，因此它不需要任何模型的信息。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

我们 AddressAndPayment POST 方法将遵循我们 StoreManagerController 中使用了相同的模式： 它将尝试接受窗体提交并完成该订单，并将重新显示窗体，如果该操作失败。

验证窗体输入满足我们的订单的验证要求后，我们将直接检查 PromoCode 窗体值。 假定所有内容都正确的我们将与订单保存更新后的信息，告知该购物车对象以完成订单流程中，并将重定向到完成的操作。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

签出过程的成功完成后，用户将重定向到完整的控制器操作。 此操作将执行简单检查以验证该顺序确实属于登录的用户显示订单号作为一条确认消息前。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*注意： 错误视图已自动为我们创建 /Views/Shared 文件夹中我们开始项目时。*

完整的 CheckoutController 代码如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>添加 AddressAndPayment 视图

现在，让我们创建 AddressAndPayment 视图。 右键单击某个 AddressAndPayment 控制器操作并添加名为 AddressAndPayment 将强类型化为订单并使用编辑模板，如下所示的视图。

![](mvc-music-store-part-9/_static/image6.png)

此视图将使用的两个探讨了构建 StoreManagerEdit 视图时的技术：

- 我们将使用 Html.EditorForModel() 来显示窗体字段的顺序模型
- 我们将利用带有验证属性使用 Order 类的验证规则

我们将开始通过更新要使用 Html.EditorForModel()，为促销代码后跟其他文本框的窗体代码。 AddressAndPayment 视图的完整代码如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>定义验证规则的顺序

现在，我们查看设置，我们将设置验证规则的顺序模型如我们以前唱片集模型。 右键单击模型文件夹并添加一个名为 Order 类。 除了我们为唱片集以前使用的验证特性，我们还将正则表达式用于验证用户的电子邮件地址。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

尝试提交窗体缺少或无效的信息现在将显示使用客户端验证错误消息。

![](mvc-music-store-part-9/_static/image7.png)

好了，我们已经完成了大部分的签出进程; 的复杂工作我们大概只需要少量几率 and 前端和后端完成。 我们需要添加两个简单的视图，并且我们需要负责在登录过程中的购物车信息的切换。

## <a name="adding-the-checkout-complete-view"></a>添加签出完整的视图

签出完整的视图是非常简单，因为它只需要显示订单 id。 右键单击完成控制器操作，然后添加一个名为完成为 int 类型，强类型视图

![](mvc-music-store-part-9/_static/image8.png)

现在我们将更新查看代码以显示订单 ID，如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>更新视图时出错

默认模板包括共享视图文件夹中的错误视图，以便它可重用于其他位置在站点中。 此错误视图包含非常简单的错误，并且不使用我们的站点布局，因此我们将更新。

由于这是一般性错误页，内容是非常简单。 我们将包括一条消息和链接以导航到历史记录中前一页，如果用户想要重试这些文件的操作。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-8.md)
> [下一页](mvc-music-store-part-10.md)
