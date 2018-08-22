---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第 9 部分： 注册和结帐 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 9 部分介绍如何注册和签出。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: b3babf1d935774b0ef93d6ab02c8b295998f8afc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826008"
---
<a name="part-9-registration-and-checkout"></a><span data-ttu-id="a06e4-104">第 9 部分： 注册和结帐</span><span class="sxs-lookup"><span data-stu-id="a06e4-104">Part 9: Registration and Checkout</span></span>
====================
<span data-ttu-id="a06e4-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="a06e4-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="a06e4-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="a06e4-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="a06e4-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="a06e4-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="a06e4-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="a06e4-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="a06e4-109">第 9 部分介绍如何注册和签出。</span><span class="sxs-lookup"><span data-stu-id="a06e4-109">Part 9 covers Registration and Checkout.</span></span>


<span data-ttu-id="a06e4-110">在本部分中，我们将创建 CheckoutController 会收集购物者的地址和付款信息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="a06e4-111">我们将要求用户注册我们的站点之前签出，因此，此控制器将需要授权。</span><span class="sxs-lookup"><span data-stu-id="a06e4-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="a06e4-112">用户将导航到结帐过程从其购物车通过单击"结帐"按钮。</span><span class="sxs-lookup"><span data-stu-id="a06e4-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="a06e4-113">如果用户未登录，则它们将提示。</span><span class="sxs-lookup"><span data-stu-id="a06e4-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="a06e4-114">成功登录后，用户将显示地址和付款视图。</span><span class="sxs-lookup"><span data-stu-id="a06e4-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="a06e4-115">它们具有填充窗体并提交订单后，将向他们显示订单确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="a06e4-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="a06e4-116">尝试查看，不存在订单或不属于您的订单将显示错误视图。</span><span class="sxs-lookup"><span data-stu-id="a06e4-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="a06e4-117">迁移购物车</span><span class="sxs-lookup"><span data-stu-id="a06e4-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="a06e4-118">尽管购物过程是匿名的当用户单击签出按钮时，它们将需要注册和登录名。</span><span class="sxs-lookup"><span data-stu-id="a06e4-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="a06e4-119">用户希望我们在保持其购物车信息之间的访问中，因此我们将需要在它们完成注册或登录名与用户相关联的购物车信息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="a06e4-120">这实际上是非常简单，因为我们的购物车类已有一种方法可将与用户名关联在当前的购物车中的所有项。</span><span class="sxs-lookup"><span data-stu-id="a06e4-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="a06e4-121">我们只需调用此方法，当用户完成注册或登录名。</span><span class="sxs-lookup"><span data-stu-id="a06e4-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="a06e4-122">打开**AccountController**时我们已设置的成员身份和授权，我们添加的类。</span><span class="sxs-lookup"><span data-stu-id="a06e4-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="a06e4-123">添加 using 语句引用 MvcMusicStore.Models，然后添加以下 MigrateShoppingCart 方法：</span><span class="sxs-lookup"><span data-stu-id="a06e4-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="a06e4-124">接下来，修改登录 post 操作调用 MigrateShoppingCart 后已验证用户，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06e4-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="a06e4-125">做出相同更改到寄存器后操作，用户帐户已成功创建后立即：</span><span class="sxs-lookup"><span data-stu-id="a06e4-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="a06e4-126">就这么简单-现在匿名的购物车将自动传输到后成功注册或登录名的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a06e4-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="a06e4-127">创建 CheckoutController</span><span class="sxs-lookup"><span data-stu-id="a06e4-127">Creating the CheckoutController</span></span>

<span data-ttu-id="a06e4-128">右键单击 Controllers 文件夹并将新的控制器添加到名为 CheckoutController 使用空的控制器模板的项目。</span><span class="sxs-lookup"><span data-stu-id="a06e4-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="a06e4-129">首先，添加控制器类声明，以要求用户在签出之前注册的上面 Authorize 属性：</span><span class="sxs-lookup"><span data-stu-id="a06e4-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="a06e4-130">*注意： 这是类似于我们先前对 StoreManagerController，所做的更改，但在这种情况下 Authorize 属性所需的用户是管理员角色中。在签出控制器中，我们要求用户登录，但不需要它们管理员。*</span><span class="sxs-lookup"><span data-stu-id="a06e4-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="a06e4-131">为简单起见，我们不会处理在本教程中的付款信息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="a06e4-132">相反，我们允许用户签出使用促销代码。</span><span class="sxs-lookup"><span data-stu-id="a06e4-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="a06e4-133">我们将存储此促销代码中使用一个名为 PromoCode 常量。</span><span class="sxs-lookup"><span data-stu-id="a06e4-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="a06e4-134">如下所示 StoreController，我们将声明一个字段来保存的名为 storeDB MusicStoreEntities 类实例。</span><span class="sxs-lookup"><span data-stu-id="a06e4-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="a06e4-135">为了使 MusicStoreEntities 类的使用，我们将需要添加一个 using 语句 MvcMusicStore.Models 命名空间。</span><span class="sxs-lookup"><span data-stu-id="a06e4-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="a06e4-136">签出控制器的顶部如下所示。</span><span class="sxs-lookup"><span data-stu-id="a06e4-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="a06e4-137">CheckoutController 将具有以下控制器操作：</span><span class="sxs-lookup"><span data-stu-id="a06e4-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="a06e4-138">**AddressAndPayment （GET 方法）** 将显示一个窗体以允许用户输入他们的信息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="a06e4-139">**AddressAndPayment （POST 方法）** 将验证输入和处理订单。</span><span class="sxs-lookup"><span data-stu-id="a06e4-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="a06e4-140">**完整**用户已成功完成结帐过程后将显示。</span><span class="sxs-lookup"><span data-stu-id="a06e4-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="a06e4-141">此视图将包括用户的订单号，以确认。</span><span class="sxs-lookup"><span data-stu-id="a06e4-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="a06e4-142">首先，让我们将索引控制器操作 （这我们创建控制器时生成） 重命名为 AddressAndPayment。</span><span class="sxs-lookup"><span data-stu-id="a06e4-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="a06e4-143">此控制器操作只是显示签出窗体，因此它不需要任何模型的信息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="a06e4-144">我们 AddressAndPayment POST 方法将遵循我们 StoreManagerController 中使用了相同的模式： 它将尝试接受窗体提交并完成该订单，并将重新显示窗体，如果该操作失败。</span><span class="sxs-lookup"><span data-stu-id="a06e4-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="a06e4-145">验证窗体输入满足我们的订单的验证要求后，我们将直接检查 PromoCode 窗体值。</span><span class="sxs-lookup"><span data-stu-id="a06e4-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="a06e4-146">假定所有内容都正确的我们将与订单保存更新后的信息，告知该购物车对象以完成订单流程中，并将重定向到完成的操作。</span><span class="sxs-lookup"><span data-stu-id="a06e4-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="a06e4-147">签出过程的成功完成后，用户将重定向到完整的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a06e4-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="a06e4-148">此操作将执行简单检查以验证该顺序确实属于登录的用户显示订单号作为一条确认消息前。</span><span class="sxs-lookup"><span data-stu-id="a06e4-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="a06e4-149">*注意： 错误视图已自动为我们创建 /Views/Shared 文件夹中我们开始项目时。*</span><span class="sxs-lookup"><span data-stu-id="a06e4-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="a06e4-150">完整的 CheckoutController 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06e4-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="a06e4-151">添加 AddressAndPayment 视图</span><span class="sxs-lookup"><span data-stu-id="a06e4-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="a06e4-152">现在，让我们创建 AddressAndPayment 视图。</span><span class="sxs-lookup"><span data-stu-id="a06e4-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="a06e4-153">右键单击某个 AddressAndPayment 控制器操作并添加名为 AddressAndPayment 将强类型化为订单并使用编辑模板，如下所示的视图。</span><span class="sxs-lookup"><span data-stu-id="a06e4-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="a06e4-154">此视图将使用的两个探讨了构建 StoreManagerEdit 视图时的技术：</span><span class="sxs-lookup"><span data-stu-id="a06e4-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="a06e4-155">我们将使用 Html.EditorForModel() 来显示窗体字段的顺序模型</span><span class="sxs-lookup"><span data-stu-id="a06e4-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="a06e4-156">我们将利用带有验证属性使用 Order 类的验证规则</span><span class="sxs-lookup"><span data-stu-id="a06e4-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="a06e4-157">我们将开始通过更新要使用 Html.EditorForModel()，为促销代码后跟其他文本框的窗体代码。</span><span class="sxs-lookup"><span data-stu-id="a06e4-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="a06e4-158">AddressAndPayment 视图的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="a06e4-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="a06e4-159">定义验证规则的顺序</span><span class="sxs-lookup"><span data-stu-id="a06e4-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="a06e4-160">现在，我们查看设置，我们将设置验证规则的顺序模型如我们以前唱片集模型。</span><span class="sxs-lookup"><span data-stu-id="a06e4-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="a06e4-161">右键单击模型文件夹并添加一个名为 Order 类。</span><span class="sxs-lookup"><span data-stu-id="a06e4-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="a06e4-162">除了我们为唱片集以前使用的验证特性，我们还将正则表达式用于验证用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="a06e4-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="a06e4-163">尝试提交窗体缺少或无效的信息现在将显示使用客户端验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="a06e4-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="a06e4-164">好了，我们已经完成了大部分的签出进程; 的复杂工作我们大概只需要少量几率 and 前端和后端完成。</span><span class="sxs-lookup"><span data-stu-id="a06e4-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="a06e4-165">我们需要添加两个简单的视图，并且我们需要负责在登录过程中的购物车信息的切换。</span><span class="sxs-lookup"><span data-stu-id="a06e4-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="a06e4-166">添加签出完整的视图</span><span class="sxs-lookup"><span data-stu-id="a06e4-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="a06e4-167">签出完整的视图是非常简单，因为它只需要显示订单 id。</span><span class="sxs-lookup"><span data-stu-id="a06e4-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="a06e4-168">右键单击完成控制器操作，然后添加一个名为完成为 int 类型，强类型视图</span><span class="sxs-lookup"><span data-stu-id="a06e4-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="a06e4-169">现在我们将更新查看代码以显示订单 ID，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a06e4-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="a06e4-170">更新视图时出错</span><span class="sxs-lookup"><span data-stu-id="a06e4-170">Updating The Error view</span></span>

<span data-ttu-id="a06e4-171">默认模板包括共享视图文件夹中的错误视图，以便它可重用于其他位置在站点中。</span><span class="sxs-lookup"><span data-stu-id="a06e4-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="a06e4-172">此错误视图包含非常简单的错误，并且不使用我们的站点布局，因此我们将更新。</span><span class="sxs-lookup"><span data-stu-id="a06e4-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="a06e4-173">由于这是一般性错误页，内容是非常简单。</span><span class="sxs-lookup"><span data-stu-id="a06e4-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="a06e4-174">我们将包括一条消息和链接以导航到历史记录中前一页，如果用户想要重试这些文件的操作。</span><span class="sxs-lookup"><span data-stu-id="a06e4-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


> [!div class="step-by-step"]
> <span data-ttu-id="a06e4-175">[上一页](mvc-music-store-part-8.md)
> [下一页](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="a06e4-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
