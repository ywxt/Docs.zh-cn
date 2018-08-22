---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第 5 部分： 业务逻辑 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 5 部分将添加一些业务逻辑。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: e18acb66dbdb3bd3e0dfa21193f617dad82afc74
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826228"
---
<a name="part-5-business-logic"></a><span data-ttu-id="934fb-104">第 5 部分： 业务逻辑</span><span class="sxs-lookup"><span data-stu-id="934fb-104">Part 5: Business Logic</span></span>
====================
<span data-ttu-id="934fb-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="934fb-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="934fb-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="934fb-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="934fb-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="934fb-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="934fb-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="934fb-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="934fb-109">第 5 部分将添加一些业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="934fb-109">Part 5 adds some business logic.</span></span>


## <a id="_Toc260221671"></a>  <span data-ttu-id="934fb-110">添加一些业务逻辑</span><span class="sxs-lookup"><span data-stu-id="934fb-110">Adding Some Business Logic</span></span>

<span data-ttu-id="934fb-111">我们希望每当有人访问我们的网站可我们购物体验。</span><span class="sxs-lookup"><span data-stu-id="934fb-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="934fb-112">访问者将能够浏览并将项添加到购物车，即使它们未注册或登录。</span><span class="sxs-lookup"><span data-stu-id="934fb-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="934fb-113">准备好要签出时他们将获得的选项进行身份验证，如果它们不是尚未成员他们将能够创建帐户。</span><span class="sxs-lookup"><span data-stu-id="934fb-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="934fb-114">这意味着，我们将需要实现逻辑以将购物车从匿名状态转换到"已注册用户"的状态。</span><span class="sxs-lookup"><span data-stu-id="934fb-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="934fb-115">让我们创建一个名为"类"，然后右键单击文件夹并创建名为 MyShoppingCart.cs 的新"类"文件</span><span class="sxs-lookup"><span data-stu-id="934fb-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="934fb-116">如前面提到过，我们会扩展实现 MyShoppingCart.aspx 页的类，我们将使用执行此类情况的操作。NET 的强大"分部类"构造。</span><span class="sxs-lookup"><span data-stu-id="934fb-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="934fb-117">我们 MyShoppingCart.aspx.cf 文件的生成的调用如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="934fb-118">请注意，使用 partial 关键字的使用。</span><span class="sxs-lookup"><span data-stu-id="934fb-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="934fb-119">我们只是生成的类文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="934fb-120">我们将通过将 partial 关键字添加到此文件合并我们的实现。</span><span class="sxs-lookup"><span data-stu-id="934fb-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="934fb-121">现在，我们的新类文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="934fb-122">第一种方法，我们将添加到我们的类是"AddItem"方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="934fb-123">这是将最终用户单击产品列表和产品详细信息页上的"添加到艺术"链接时要调用的方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="934fb-124">将以下内容追加到使用页面顶部的语句。</span><span class="sxs-lookup"><span data-stu-id="934fb-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="934fb-125">并将以下方法添加到 MyShoppingCart 类。</span><span class="sxs-lookup"><span data-stu-id="934fb-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="934fb-126">我们将使用 LINQ to Entities 来查看该项目是否已在购物车中。</span><span class="sxs-lookup"><span data-stu-id="934fb-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="934fb-127">如果因此，我们更新项的订单数量，否则我们创建所选的项的新项</span><span class="sxs-lookup"><span data-stu-id="934fb-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="934fb-128">若要调用此方法中，我们将实现不仅类此方法，但然后显示当前购物 = 购物车添加项之后的 AddToCart.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="934fb-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="934fb-129">右键单击解决方案资源管理器中的解决方案名称，然后添加和名为 AddToCart.aspx，如我们以前所做的新页。</span><span class="sxs-lookup"><span data-stu-id="934fb-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="934fb-130">虽然我们无法使用此页以显示我们的实现如低库存问题等，临时结果，该页将实际上不会呈现，但而不是调用"添加"逻辑，重定向。</span><span class="sxs-lookup"><span data-stu-id="934fb-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="934fb-131">若要完成此我们将以下代码添加到页面\_加载事件。</span><span class="sxs-lookup"><span data-stu-id="934fb-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="934fb-132">请注意，我们要检索的产品从查询字符串参数并调用我们的类的 AddItem 方法将添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="934fb-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="934fb-133">假设没有错误遇到控制权将传递给我们将完全实现下一步使用 SHoppingCart.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="934fb-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="934fb-134">如果应引发异常错误。</span><span class="sxs-lookup"><span data-stu-id="934fb-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="934fb-135">目前我们没有实现全局错误处理程序以便此异常将会通过我们的应用程序得到处理，但我们稍后将解决此问题。</span><span class="sxs-lookup"><span data-stu-id="934fb-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="934fb-136">另请注意语句 Debug.Fail() （可通过使用 `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="934fb-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="934fb-137">是在调试器中运行该应用程序，此方法将显示一个详细的对话框，其中我们指定的错误消息以及应用程序状态信息。</span><span class="sxs-lookup"><span data-stu-id="934fb-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="934fb-138">当运行在生产环境 Debug.Fail() 语句中的将被忽略。</span><span class="sxs-lookup"><span data-stu-id="934fb-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="934fb-139">您会注意到我们购物车类名"GetShoppingCartId"中的方法调用上方的代码中。</span><span class="sxs-lookup"><span data-stu-id="934fb-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="934fb-140">添加代码以实现的方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="934fb-141">请注意，我们还添加了更新和签出按钮和标签，我们可以显示购物车"总计"。</span><span class="sxs-lookup"><span data-stu-id="934fb-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="934fb-142">现在，我们可以将项添加到我们的购物车，但我们尚未实现逻辑以添加一个产品后显示购物车。</span><span class="sxs-lookup"><span data-stu-id="934fb-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="934fb-143">因此，MyShoppingCart.aspx 页中我们将添加 EntityDataSource 控件和 GridVire 控件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="934fb-144">调用启动的窗体设计器中，因此，可以双击更新购物车按钮，并生成的单击事件处理程序在标记声明中指定。</span><span class="sxs-lookup"><span data-stu-id="934fb-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="934fb-145">更高版本，我们将实现详细信息，但执行此操作会让我们生成并运行我们的应用程序未出现错误。</span><span class="sxs-lookup"><span data-stu-id="934fb-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="934fb-146">运行应用程序并将项添加到购物车时将看到此。</span><span class="sxs-lookup"><span data-stu-id="934fb-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="934fb-147">请注意，我们没有遵循"默认"网格显示通过实现三个自定义列。</span><span class="sxs-lookup"><span data-stu-id="934fb-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="934fb-148">第一个是一种可编辑、"绑定"字段的数量：</span><span class="sxs-lookup"><span data-stu-id="934fb-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="934fb-149">下一步是"计算"列显示行项总计 （项的成本的乘积的数量进行排序）：</span><span class="sxs-lookup"><span data-stu-id="934fb-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="934fb-150">最后，我们有一个包含用户将用于指示应从购物图表移除的项的复选框控件的自定义列。</span><span class="sxs-lookup"><span data-stu-id="934fb-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="934fb-151">正如您所看到的因此，让我们为空总的行的顺序将添加一些逻辑以计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="934fb-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="934fb-152">首先，我们将向我们 MyShoppingCart 类实现"GetTotal"方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="934fb-153">MyShoppingCart.cs 文件中添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="934fb-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="934fb-154">然后在页面\_Load 事件处理程序，我们将可以调用我们 GetTotal 方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="934fb-155">同时，我们将添加一个测试，以查看购物车是否为空并相应地调整显示，如果它是。</span><span class="sxs-lookup"><span data-stu-id="934fb-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="934fb-156">现在如果购物车中没有我们得到如下结果：</span><span class="sxs-lookup"><span data-stu-id="934fb-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="934fb-157">如果不是，我们看到我们总共。</span><span class="sxs-lookup"><span data-stu-id="934fb-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="934fb-158">但是，此页尚未完成。</span><span class="sxs-lookup"><span data-stu-id="934fb-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="934fb-159">我们将需要额外的逻辑，以便重新计算购物车中删除标记为待删除的项和一些可能已更改网格中由用户确定新数量值。</span><span class="sxs-lookup"><span data-stu-id="934fb-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="934fb-160">允许添加到购物车类 MyShoppingCart.cs 来处理这种情况，用户将标记为删除的项中的"RemoveItem"方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="934fb-161">现在让我们 ad 处理用户只需更改质量 GridView 中进行排序时所处环境的方法。</span><span class="sxs-lookup"><span data-stu-id="934fb-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="934fb-162">与位置中的基本进行删除和更新功能，我们可以实施实际更新购物车中数据库的逻辑。</span><span class="sxs-lookup"><span data-stu-id="934fb-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="934fb-163">（在 MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="934fb-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="934fb-164">您会注意此方法需要两个参数。</span><span class="sxs-lookup"><span data-stu-id="934fb-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="934fb-165">一个购物车 Id，另一个是用户定义类型的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="934fb-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="934fb-166">以尽可能减少我们用户接口细节的逻辑的依赖关系，我们定义了可用于将购物车商品传递给我们的代码，而无需我们无需直接访问 GridView 控件的方法的数据结构。</span><span class="sxs-lookup"><span data-stu-id="934fb-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="934fb-167">在我们的 MyShoppingCart.aspx.cs 文件可以使用此结构在我们的更新按钮单击事件处理程序中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="934fb-168">请注意，除了更新购物车我们将更新购物车总计以及。</span><span class="sxs-lookup"><span data-stu-id="934fb-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="934fb-169">请注意这行代码与特定的感兴趣：</span><span class="sxs-lookup"><span data-stu-id="934fb-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="934fb-170">GetValues() 是一个特殊的 helper 函数，我们会在中实现 MyShoppingCart.aspx.cs，如下所示。</span><span class="sxs-lookup"><span data-stu-id="934fb-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="934fb-171">这提供了简洁的方式来访问我们的 GridView 控件中的绑定元素的值。</span><span class="sxs-lookup"><span data-stu-id="934fb-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="934fb-172">由于我们的"删除项"复选框控件未绑定，因此我们将通过 FindControl() 方法来访问它。</span><span class="sxs-lookup"><span data-stu-id="934fb-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="934fb-173">在此阶段在你的项目的开发过程中我们已准备好实施签出过程。</span><span class="sxs-lookup"><span data-stu-id="934fb-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="934fb-174">让我们执行此操作之前使用 Visual Studio 生成成员资格数据库并将用户添加到成员身份存储库。</span><span class="sxs-lookup"><span data-stu-id="934fb-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="934fb-175">[上一页](tailspin-spyworks-part-4.md)
> [下一页](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="934fb-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
