---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第 5 部分： 业务逻辑 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 5 部分将添加一些业务逻辑。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: e4342e634ef8c4bcf4e0085650a28f414ab23736
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30885076"
---
<a name="part-5-business-logic"></a><span data-ttu-id="46e7d-104">第 5 部分： 业务逻辑</span><span class="sxs-lookup"><span data-stu-id="46e7d-104">Part 5: Business Logic</span></span>
====================
<span data-ttu-id="46e7d-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="46e7d-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="46e7d-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="46e7d-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="46e7d-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="46e7d-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="46e7d-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="46e7d-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="46e7d-109">第 5 部分将添加一些业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="46e7d-109">Part 5 adds some business logic.</span></span>


## <a id="_Toc260221671"></a>  <span data-ttu-id="46e7d-110">添加一些业务逻辑</span><span class="sxs-lookup"><span data-stu-id="46e7d-110">Adding Some Business Logic</span></span>

<span data-ttu-id="46e7d-111">我们想要可用，每当有人访问我们的网站时我们购物体验。</span><span class="sxs-lookup"><span data-stu-id="46e7d-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="46e7d-112">访问者将能够浏览并将项添加到购物车，即使未注册或登录。</span><span class="sxs-lookup"><span data-stu-id="46e7d-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="46e7d-113">准备好签出时它们将其提供选项进行身份验证并且如果它们不是尚未成员他们将能创建帐户。</span><span class="sxs-lookup"><span data-stu-id="46e7d-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="46e7d-114">这意味着，我们将需要实现逻辑以将购物车从匿名状态转换为"已注册的用户"状态。</span><span class="sxs-lookup"><span data-stu-id="46e7d-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="46e7d-115">让我们创建一个名为"类"目录，然后右键单击文件夹并创建名为 MyShoppingCart.cs 的新"类"文件</span><span class="sxs-lookup"><span data-stu-id="46e7d-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="46e7d-116">如前面所提到，我们将扩展实现 MyShoppingCart.aspx 页的类和我们将使用执行此类情况的操作。NET 的强大"分部类"构造。</span><span class="sxs-lookup"><span data-stu-id="46e7d-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="46e7d-117">对我们 MyShoppingCart.aspx.cf 文件的生成的调用如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="46e7d-118">请注意，使用"分部"关键字。</span><span class="sxs-lookup"><span data-stu-id="46e7d-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="46e7d-119">我们刚生成的类文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="46e7d-120">我们将通过将 partial 关键字添加到此文件以及合并我们实现。</span><span class="sxs-lookup"><span data-stu-id="46e7d-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="46e7d-121">现在，我们的新类文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="46e7d-122">我们将添加到类的第一个方法是"AddItem"方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="46e7d-123">这是当用户单击的产品列表和产品详细信息页上的"添加到画"链接时将最终调用的方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="46e7d-124">将以下内容追加到 using 语句页的顶部。</span><span class="sxs-lookup"><span data-stu-id="46e7d-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="46e7d-125">并将此方法添加到 MyShoppingCart 类。</span><span class="sxs-lookup"><span data-stu-id="46e7d-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="46e7d-126">我们将使用 LINQ to Entities 来查看项是否已在车。</span><span class="sxs-lookup"><span data-stu-id="46e7d-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="46e7d-127">如果这样，我们更新项的数量，否则我们创建的选定项的新项</span><span class="sxs-lookup"><span data-stu-id="46e7d-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="46e7d-128">若要调用此方法中，我们将实现类此方法不仅然后显示当前购物 = 车后已添加项的 AddToCart.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="46e7d-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="46e7d-129">右键单击解决方案资源管理器中的解决方案名称，然后添加和命名 AddToCart.aspx，因为我们以前所做的新页。</span><span class="sxs-lookup"><span data-stu-id="46e7d-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="46e7d-130">尽管我们可以使用此页以显示中间结果类似于低股票问题等，我们实现中，页面将不实际呈现，而是调用"添加"逻辑和重定向。</span><span class="sxs-lookup"><span data-stu-id="46e7d-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="46e7d-131">若要完成此我们将以下代码添加到页面\_加载事件。</span><span class="sxs-lookup"><span data-stu-id="46e7d-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="46e7d-132">请注意，我们在检索要添加到购物车中的查询字符串参数以及调用我们的类的 AddItem 方法的产品。</span><span class="sxs-lookup"><span data-stu-id="46e7d-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="46e7d-133">假设没有错误遇到控制权传递给我们将完全实现下一步的 SHoppingCart.aspx 页面。</span><span class="sxs-lookup"><span data-stu-id="46e7d-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="46e7d-134">如果应我们引发了异常错误。</span><span class="sxs-lookup"><span data-stu-id="46e7d-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="46e7d-135">目前我们没有实现全局错误处理程序以便此异常将进入未处理的我们的应用程序，但我们将很快修正此问题。</span><span class="sxs-lookup"><span data-stu-id="46e7d-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="46e7d-136">另请注意语句 Debug.Fail() （可通过使用 `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="46e7d-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="46e7d-137">是在调试器内部运行该应用程序时，此方法将显示包含的信息以及我们指定的错误消息的应用程序状态详细的对话框。</span><span class="sxs-lookup"><span data-stu-id="46e7d-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="46e7d-138">当运行在生产 Debug.Fail() 语句中的将被忽略。</span><span class="sxs-lookup"><span data-stu-id="46e7d-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="46e7d-139">你将注意到我们购物车类名"GetShoppingCartId"中的方法调用上方的代码中。</span><span class="sxs-lookup"><span data-stu-id="46e7d-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="46e7d-140">添加代码，如下所示实现方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="46e7d-141">请注意，我们还添加了更新和签出按钮和标签我们可以在其中显示购物车"总计"。</span><span class="sxs-lookup"><span data-stu-id="46e7d-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="46e7d-142">现在，我们可以将项添加到我们的购物车，但我们尚未实现的逻辑，以添加产品后显示购物车。</span><span class="sxs-lookup"><span data-stu-id="46e7d-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="46e7d-143">因此，在 MyShoppingCart.aspx 页中我们将添加 EntityDataSource 控件和 GridVire 控件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="46e7d-144">调用的窗体设计器中，以便你可以双击更新购物车按钮和生成在标记中的声明中指定的 click 事件处理。</span><span class="sxs-lookup"><span data-stu-id="46e7d-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="46e7d-145">我们将更高版本实现的详细信息，但执行此操作将告诉我们生成并运行我们的应用程序且未发生错误。</span><span class="sxs-lookup"><span data-stu-id="46e7d-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="46e7d-146">当你运行应用程序，并且将项添加到购物车你将看到此。</span><span class="sxs-lookup"><span data-stu-id="46e7d-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="46e7d-147">请注意，我们未遵从"默认"网格显示通过实现三个自定义列。</span><span class="sxs-lookup"><span data-stu-id="46e7d-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="46e7d-148">第一个是可编辑，按"绑定"字段的数量。</span><span class="sxs-lookup"><span data-stu-id="46e7d-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="46e7d-149">下一步是显示的行项总计 （项的成本的乘积的数量，才能进行排序） 的"计算"列：</span><span class="sxs-lookup"><span data-stu-id="46e7d-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="46e7d-150">最后，我们有包含用户将使用以指示应购物图表中移除的项的复选框控件的自定义列。</span><span class="sxs-lookup"><span data-stu-id="46e7d-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="46e7d-151">如你所见，因此，让我们为空总的行的顺序将添加一些逻辑来计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="46e7d-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="46e7d-152">首先，我们将到 MyShoppingCart 类实现"GetTotal"方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="46e7d-153">MyShoppingCart.cs 文件中添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="46e7d-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="46e7d-154">然后在页\_我们将可以调用我们 GetTotal 方法的 Load 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="46e7d-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="46e7d-155">在同一时间，我们将添加一个测试以查看购物车是否为空并相应地调整显示，如果它是。</span><span class="sxs-lookup"><span data-stu-id="46e7d-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="46e7d-156">现在是否为空购物车我们得到如下：</span><span class="sxs-lookup"><span data-stu-id="46e7d-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="46e7d-157">并且，如果不是，我们看到我们总共。</span><span class="sxs-lookup"><span data-stu-id="46e7d-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="46e7d-158">但是，此页尚未完成。</span><span class="sxs-lookup"><span data-stu-id="46e7d-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="46e7d-159">我们将需要其他逻辑来重新计算购物车，通过删除标记为删除的项，如某些可能已更改网格中由用户确定新数量值。</span><span class="sxs-lookup"><span data-stu-id="46e7d-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="46e7d-160">允许添加到购物车类 MyShoppingCart.cs 来处理这种情况，当用户标记中删除的项目中的"RemoveItem"方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="46e7d-161">现在让我们 ad 方法以处理情况，用户只需更改要按 GridView 排序的质量时。</span><span class="sxs-lookup"><span data-stu-id="46e7d-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="46e7d-162">与就地基本的删除和更新功能，我们可以实现实际更新购物车中数据库的逻辑。</span><span class="sxs-lookup"><span data-stu-id="46e7d-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="46e7d-163">（在 MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="46e7d-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="46e7d-164">你将注意到此方法需要两个参数。</span><span class="sxs-lookup"><span data-stu-id="46e7d-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="46e7d-165">一个是购物车 Id，另一个是用户定义类型的对象的数组。</span><span class="sxs-lookup"><span data-stu-id="46e7d-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="46e7d-166">最小化用户界面细节我们逻辑的依赖关系，以便我们已定义一种数据结构，我们可以用来将购物车项传递给我们的代码，而无需我们无需直接访问 GridView 控件的方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="46e7d-167">在我们的 MyShoppingCart.aspx.cs 文件我们可以使用此结构在我们的更新按钮单击事件处理程序中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="46e7d-168">请注意，除了更新购物车我们将更新购物车总计以及。</span><span class="sxs-lookup"><span data-stu-id="46e7d-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="46e7d-169">请注意特别感兴趣使用此代码行：</span><span class="sxs-lookup"><span data-stu-id="46e7d-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="46e7d-170">GetValues() 是一个特殊的 helper 函数，我们将在中实现 MyShoppingCart.aspx.cs，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46e7d-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="46e7d-171">这提供了用于访问我们的 GridView 控件中的绑定元素的值的全新方法。</span><span class="sxs-lookup"><span data-stu-id="46e7d-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="46e7d-172">由于我们"删除项"复选框控件未绑定我们将通过 FindControl() 方法来访问它。</span><span class="sxs-lookup"><span data-stu-id="46e7d-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="46e7d-173">在你的项目的开发中的此阶段中，我们正在准备实现在结帐过程。</span><span class="sxs-lookup"><span data-stu-id="46e7d-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="46e7d-174">让我们执行此操作之前使用 Visual Studio 生成成员资格数据库并将用户添加到成员身份存储库。</span><span class="sxs-lookup"><span data-stu-id="46e7d-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="46e7d-175">[上一页](tailspin-spyworks-part-4.md)
> [下一页](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="46e7d-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
