---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 一部分 9： 注册和签出 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 9 部分介绍如何注册和签出。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: e7e83b70f2508b6dfc0c078b992747a76e4d0ff2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870110"
---
<a name="part-9-registration-and-checkout"></a><span data-ttu-id="32598-104">一部分 9： 注册和签出</span><span class="sxs-lookup"><span data-stu-id="32598-104">Part 9: Registration and Checkout</span></span>
====================
<span data-ttu-id="32598-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="32598-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="32598-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="32598-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="32598-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="32598-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="32598-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="32598-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="32598-109">第 9 部分介绍如何注册和签出。</span><span class="sxs-lookup"><span data-stu-id="32598-109">Part 9 covers Registration and Checkout.</span></span>


<span data-ttu-id="32598-110">在此部分中，我们将创建其购物者的地址和付款信息将收集 CheckoutController。</span><span class="sxs-lookup"><span data-stu-id="32598-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="32598-111">我们将要求用户注册之前签出我们的站点，因此，此控制器将需要授权。</span><span class="sxs-lookup"><span data-stu-id="32598-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="32598-112">用户将转到结帐过程从其购物车通过单击"签出"按钮。</span><span class="sxs-lookup"><span data-stu-id="32598-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="32598-113">如果用户未登录，将到提示他们。</span><span class="sxs-lookup"><span data-stu-id="32598-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="32598-114">一旦成功登录，然后向用户显示的地址和付款视图。</span><span class="sxs-lookup"><span data-stu-id="32598-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="32598-115">后它们已填充该窗体和提交订单，它们将显示订单确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="32598-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="32598-116">尝试查看不存在顺序或不属于你的订单将显示错误视图。</span><span class="sxs-lookup"><span data-stu-id="32598-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="32598-117">迁移购物车</span><span class="sxs-lookup"><span data-stu-id="32598-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="32598-118">尽管购物过程匿名的当用户单击签出按钮时，它们将需要注册和登录名。</span><span class="sxs-lookup"><span data-stu-id="32598-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="32598-119">用户将希望我们将维护之间访问，因此我们将需要在完成注册或登录名时将与用户关联的购物车信息其购物车信息。</span><span class="sxs-lookup"><span data-stu-id="32598-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="32598-120">这是实际为，非常简单，因为我们购物车类已经将与用户名关联当前购物车中的所有项的方法。</span><span class="sxs-lookup"><span data-stu-id="32598-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="32598-121">我们只需调用此方法，当用户完成注册或登录名。</span><span class="sxs-lookup"><span data-stu-id="32598-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="32598-122">打开**AccountController**时我们已设置成员身份和授权我们添加的类。</span><span class="sxs-lookup"><span data-stu-id="32598-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="32598-123">添加 using 语句引用 MvcMusicStore.Models，然后添加以下 MigrateShoppingCart 方法：</span><span class="sxs-lookup"><span data-stu-id="32598-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="32598-124">接下来，修改登录 post 操作，以调用 MigrateShoppingCart 后用户已进行验证，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32598-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="32598-125">进行相同的更改注册后操作，用户帐户已成功创建后立即：</span><span class="sxs-lookup"><span data-stu-id="32598-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="32598-126">就这么简单-现在匿名的购物车将自动传输到在成功注册或登录名后的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="32598-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="32598-127">创建 CheckoutController</span><span class="sxs-lookup"><span data-stu-id="32598-127">Creating the CheckoutController</span></span>

<span data-ttu-id="32598-128">右键单击 Controllers 文件夹，然后将新的控制器添加到名为 CheckoutController 使用空控制器模板的项目。</span><span class="sxs-lookup"><span data-stu-id="32598-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="32598-129">首先，添加 Authorize 属性来要求用户注册之前签出该控制器类声明的上方：</span><span class="sxs-lookup"><span data-stu-id="32598-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="32598-130">*注意： 这是类似于我们先前对 StoreManagerController，所做的更改，但在这种情况下 Authorize 属性所需的用户是管理员角色。在签出控制器中，我们要要求用户身份登录，但不要求，它们管理员。*</span><span class="sxs-lookup"><span data-stu-id="32598-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="32598-131">为简单起见，我们不会处理在本教程中的付款信息。</span><span class="sxs-lookup"><span data-stu-id="32598-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="32598-132">相反，我们允许用户签出使用促销代码。</span><span class="sxs-lookup"><span data-stu-id="32598-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="32598-133">我们将存储此促销代码使用名为 PromoCode 常量。</span><span class="sxs-lookup"><span data-stu-id="32598-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="32598-134">如下所示 StoreController，我们将声明某个字段包含名为 storeDB 的 MusicStoreEntities 类的实例。</span><span class="sxs-lookup"><span data-stu-id="32598-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="32598-135">为了使使用 MusicStoreEntities 类，我们将需要添加 using 语句 MvcMusicStore.Models 命名空间。</span><span class="sxs-lookup"><span data-stu-id="32598-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="32598-136">请查看控制器顶部如下所示。</span><span class="sxs-lookup"><span data-stu-id="32598-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="32598-137">CheckoutController 将具有以下的控制器操作：</span><span class="sxs-lookup"><span data-stu-id="32598-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="32598-138">**AddressAndPayment （GET 方法）** 将显示的窗体，以允许用户输入他们的信息。</span><span class="sxs-lookup"><span data-stu-id="32598-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="32598-139">**AddressAndPayment （POST 方法）** 将验证输入和处理顺序。</span><span class="sxs-lookup"><span data-stu-id="32598-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="32598-140">**完成**将在用户成功完成结帐过程后显示。</span><span class="sxs-lookup"><span data-stu-id="32598-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="32598-141">此视图将包括用户的订单号作为确认。</span><span class="sxs-lookup"><span data-stu-id="32598-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="32598-142">首先，让我们将索引控制器操作 （其中我们创建控制器时生成） 重命名为 AddressAndPayment。</span><span class="sxs-lookup"><span data-stu-id="32598-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="32598-143">此控制器操作只是显示签出窗体中，因此它不需要任何模型信息。</span><span class="sxs-lookup"><span data-stu-id="32598-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="32598-144">我们 AddressAndPayment POST 方法将遵循我们 StoreManagerController 中使用了相同的模式： 它将尝试接受表单提交并完成顺序，并将重新显示窗体，如果失败。</span><span class="sxs-lookup"><span data-stu-id="32598-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="32598-145">验证窗体输入满足订单我们验证要求后，我们将直接检查 PromoCode 窗体值。</span><span class="sxs-lookup"><span data-stu-id="32598-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="32598-146">假设所有内容正确无误，我们将与订单保存更新的信息，让 ShoppingCart 对象完成订单过程中，并将重定向到完成操作。</span><span class="sxs-lookup"><span data-stu-id="32598-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="32598-147">在结帐过程成功完成，用户将重定向到完成控制器操作。</span><span class="sxs-lookup"><span data-stu-id="32598-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="32598-148">此操作将执行验证的顺序未确实属于登录的用户在显示订单号作为一条确认消息之前的简单检查。</span><span class="sxs-lookup"><span data-stu-id="32598-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="32598-149">*注意： 错误视图自动创建为我们 /Views/Shared 文件夹中我们开始项目时。*</span><span class="sxs-lookup"><span data-stu-id="32598-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="32598-150">完整的 CheckoutController 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="32598-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="32598-151">添加 AddressAndPayment 视图</span><span class="sxs-lookup"><span data-stu-id="32598-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="32598-152">现在，让我们创建 AddressAndPayment 视图。</span><span class="sxs-lookup"><span data-stu-id="32598-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="32598-153">右键单击其中一个 AddressAndPayment 控制器操作并添加名为 AddressAndPayment 强类型化为订单并使用编辑模板中，如下所示的视图。</span><span class="sxs-lookup"><span data-stu-id="32598-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="32598-154">此视图将使用的两个生成 StoreManagerEdit 视图时在我们讨论的技术：</span><span class="sxs-lookup"><span data-stu-id="32598-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="32598-155">我们将使用 Html.EditorForModel() 以显示的顺序模型的窗体字段</span><span class="sxs-lookup"><span data-stu-id="32598-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="32598-156">我们将利用 Order 类中使用验证特性的验证规则</span><span class="sxs-lookup"><span data-stu-id="32598-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="32598-157">我们将开始通过更新窗体代码以使用 Html.EditorForModel()，对促销代码跟其他文本框。</span><span class="sxs-lookup"><span data-stu-id="32598-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="32598-158">AddressAndPayment 视图的完整代码所示。</span><span class="sxs-lookup"><span data-stu-id="32598-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="32598-159">为顺序定义验证规则</span><span class="sxs-lookup"><span data-stu-id="32598-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="32598-160">既然我们视图设置，我们将设置验证规则为我们的顺序模型我们像以前唱片集模型一样。</span><span class="sxs-lookup"><span data-stu-id="32598-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="32598-161">右键单击 Models 文件夹，然后添加名为顺序的类。</span><span class="sxs-lookup"><span data-stu-id="32598-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="32598-162">除了我们用于以前唱片集的验证属性，我们将还使用正则表达式来验证用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="32598-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="32598-163">试图提交窗体具有缺少或无效的信息现在将显示错误消息，使用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="32598-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="32598-164">好了，我们已完成大部分结帐过程中; 的复杂工作我们只具有少量机率 and 前端和后端完成。</span><span class="sxs-lookup"><span data-stu-id="32598-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="32598-165">我们需要添加两个简单的视图，并且我们需要负责的登录过程的购物车信息 handoff。</span><span class="sxs-lookup"><span data-stu-id="32598-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="32598-166">添加签出完整的视图</span><span class="sxs-lookup"><span data-stu-id="32598-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="32598-167">签出完整的视图是非常简单，因为它只需要显示订单 id。</span><span class="sxs-lookup"><span data-stu-id="32598-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="32598-168">右键单击完成控制器操作，然后添加名为强类型化为 int 的完成的视图</span><span class="sxs-lookup"><span data-stu-id="32598-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="32598-169">现在我们将更新查看代码，以显示订单 ID，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32598-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="32598-170">更新视图时出错</span><span class="sxs-lookup"><span data-stu-id="32598-170">Updating The Error view</span></span>

<span data-ttu-id="32598-171">默认模板包括在共享 views 文件夹中的错误视图，以便它可以重复使用在其他位置在站点中。</span><span class="sxs-lookup"><span data-stu-id="32598-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="32598-172">此错误视图包含非常简单的错误，并且不使用我们的站点布局，因此我们将更新。</span><span class="sxs-lookup"><span data-stu-id="32598-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="32598-173">由于这是一般性错误页，内容是非常简单。</span><span class="sxs-lookup"><span data-stu-id="32598-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="32598-174">我们将包含一条消息和链接以导航到历史记录中前一页中，如果用户想要重试这些文件的操作。</span><span class="sxs-lookup"><span data-stu-id="32598-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


> [!div class="step-by-step"]
> <span data-ttu-id="32598-175">[上一页](mvc-music-store-part-8.md)
> [下一页](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="32598-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
