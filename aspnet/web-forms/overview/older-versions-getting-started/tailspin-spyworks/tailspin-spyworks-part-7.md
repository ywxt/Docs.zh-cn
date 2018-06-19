---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第 7 部分： 添加功能 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 7 部分添加其他功能，如帐户 revie...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 17f068155f6726047901e2f7d580d375a4e07c87
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888388"
---
<a name="part-7-adding-features"></a><span data-ttu-id="e3d79-104">第 7 部分： 添加功能</span><span class="sxs-lookup"><span data-stu-id="e3d79-104">Part 7: Adding Features</span></span>
====================
<span data-ttu-id="e3d79-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="e3d79-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="e3d79-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="e3d79-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="e3d79-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="e3d79-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="e3d79-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="e3d79-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="e3d79-109">第 7 部分添加了其他功能，如帐户评审、 产品评论和"常用项"和"还购买"用户控件。</span><span class="sxs-lookup"><span data-stu-id="e3d79-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>


## <a id="_Toc260221673"></a>  <span data-ttu-id="e3d79-110">添加功能</span><span class="sxs-lookup"><span data-stu-id="e3d79-110">Adding Features</span></span>

<span data-ttu-id="e3d79-111">尽管用户可以浏览我们的目录，将项放在其购物车，和完成结帐过程，有大量的支持功能，我们将包含以改进我们的站点。</span><span class="sxs-lookup"><span data-stu-id="e3d79-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="e3d79-112">帐户查看 （列表订单放置和查看详细信息。）</span><span class="sxs-lookup"><span data-stu-id="e3d79-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="e3d79-113">将一些上下文特定内容添加到首页。</span><span class="sxs-lookup"><span data-stu-id="e3d79-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="e3d79-114">在目录中添加一项功能以使用户可以查看的产品。</span><span class="sxs-lookup"><span data-stu-id="e3d79-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="e3d79-115">创建用户控件在首页上显示控制的常用项和位置。</span><span class="sxs-lookup"><span data-stu-id="e3d79-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="e3d79-116">创建"还购买"的用户控件并将其添加到产品详细信息页。</span><span class="sxs-lookup"><span data-stu-id="e3d79-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="e3d79-117">添加联系人页。</span><span class="sxs-lookup"><span data-stu-id="e3d79-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="e3d79-118">添加有关页面。</span><span class="sxs-lookup"><span data-stu-id="e3d79-118">Add an About Page.</span></span>
8. <span data-ttu-id="e3d79-119">全局错误</span><span class="sxs-lookup"><span data-stu-id="e3d79-119">Global Error</span></span>

## <a id="_Toc260221674"></a>  <span data-ttu-id="e3d79-120">帐户检查</span><span class="sxs-lookup"><span data-stu-id="e3d79-120">Account Review</span></span>

<span data-ttu-id="e3d79-121">在"帐户"文件夹中创建一个命名的 OrderList.aspx 和其他命名的 OrderDetails.aspx 的两个.aspx 页</span><span class="sxs-lookup"><span data-stu-id="e3d79-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="e3d79-122">OrderList.aspx 将利用 GridView 和 EntityDataSoure 控件一样使用我们具有除前面。</span><span class="sxs-lookup"><span data-stu-id="e3d79-122">OrderList.aspx will leverage the GridView and EntityDataSoure controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="e3d79-123">EntityDataSoure 从 Orders 表中在用户名上筛选选择记录 （请参阅 WhereParameter） 的用户登录时在会话变量中我们设置。</span><span class="sxs-lookup"><span data-stu-id="e3d79-123">The EntityDataSoure selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="e3d79-124">另请注意的 GridView HyperlinkField 中的这些参数：</span><span class="sxs-lookup"><span data-stu-id="e3d79-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="e3d79-125">这些名称指定为作为 OrderDetails.aspx 页的查询字符串参数中指定订单 id 字段的每个产品的订单详细信息视图的链接。</span><span class="sxs-lookup"><span data-stu-id="e3d79-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a>  <span data-ttu-id="e3d79-126">OrderDetails.aspx</span><span class="sxs-lookup"><span data-stu-id="e3d79-126">OrderDetails.aspx</span></span>

<span data-ttu-id="e3d79-127">我们将使用 EntityDataSource 控件访问订单和 FormView 以显示订单数据，另一个 EntityDataSource 与一个 GridView，若要显示的顺序的所有行项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="e3d79-128">在代码隐藏文件 (OrderDetails.aspx.cs) 我们具有两个小位的管理。</span><span class="sxs-lookup"><span data-stu-id="e3d79-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="e3d79-129">首先，我们需要确保 OrderDetails 始终获取 OrderId。</span><span class="sxs-lookup"><span data-stu-id="e3d79-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="e3d79-130">我们还需要计算并显示总从行项的顺序。</span><span class="sxs-lookup"><span data-stu-id="e3d79-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>  <span data-ttu-id="e3d79-131">主页页面</span><span class="sxs-lookup"><span data-stu-id="e3d79-131">The Home Page</span></span>

<span data-ttu-id="e3d79-132">让我们将一些静态内容添加到 Default.aspx 页上。</span><span class="sxs-lookup"><span data-stu-id="e3d79-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="e3d79-133">首先，我将创建的"内容"文件夹并在该映像文件夹 （并且将包含要在主页上使用的图像。）</span><span class="sxs-lookup"><span data-stu-id="e3d79-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="e3d79-134">到 Default.aspx 页的底部占位符，添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="e3d79-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>  <span data-ttu-id="e3d79-135">产品评论</span><span class="sxs-lookup"><span data-stu-id="e3d79-135">Product Reviews</span></span>

<span data-ttu-id="e3d79-136">首先我们将向我们可以使用来输入产品评论的窗体添加一个按钮的链接。</span><span class="sxs-lookup"><span data-stu-id="e3d79-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="e3d79-137">请注意我们在查询字符串中传递 ProductID</span><span class="sxs-lookup"><span data-stu-id="e3d79-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="e3d79-138">下一步让我们添加名为 ReviewAdd.aspx 页</span><span class="sxs-lookup"><span data-stu-id="e3d79-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="e3d79-139">此页将使用 ASP.NET AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="e3d79-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="e3d79-140">如果你尚未做以便你可以下载它从[DevExpress](http://devexpress.com/act)和上设置适用于使用 Visual Studio 使用此处的工具包没有指南[ https://www.asp.net/learn/ajax-videos/video-76.aspx ](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)。</span><span class="sxs-lookup"><span data-stu-id="e3d79-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="e3d79-141">在设计模式下，从工具箱中拖动控件和验证程序和生成的窗体，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3d79-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="e3d79-142">标记将如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3d79-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="e3d79-143">现在，我们可以输入评审，允许在产品页面上显示这些评审。</span><span class="sxs-lookup"><span data-stu-id="e3d79-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="e3d79-144">将此标记添加到 ProductDetails.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="e3d79-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="e3d79-145">运行应用程序现在和导航到产品显示产品信息，包括客户评审。</span><span class="sxs-lookup"><span data-stu-id="e3d79-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>  <span data-ttu-id="e3d79-146">（创建用户控件） 的常用项控件</span><span class="sxs-lookup"><span data-stu-id="e3d79-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="e3d79-147">为了提高在网站上的销量我们将将几个功能添加到"暗示销售"常用或相关产品。</span><span class="sxs-lookup"><span data-stu-id="e3d79-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="e3d79-148">这些功能的第一个将在我们的产品目录中更受欢迎的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="e3d79-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="e3d79-149">我们将创建一个"用户控件"来显示最畅销的主页上的我们的应用程序的项目。</span><span class="sxs-lookup"><span data-stu-id="e3d79-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="e3d79-150">因为这将为控件，我们可以使用它任何页上通过简单地拖放控件拖到我们喜欢的任何页面上的 Visual Studio 设计器中。</span><span class="sxs-lookup"><span data-stu-id="e3d79-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="e3d79-151">在 Visual Studio 的解决方案资源管理器中，右键单击解决方案名称，然后创建一个名为"控件"的新目录。</span><span class="sxs-lookup"><span data-stu-id="e3d79-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="e3d79-152">虽然不需要这样做，我们将帮助保持我们的项目中组织通过在"控件"目录中创建所有我们用户控件。</span><span class="sxs-lookup"><span data-stu-id="e3d79-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="e3d79-153">右键单击控件文件夹并选择"新项":</span><span class="sxs-lookup"><span data-stu-id="e3d79-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="e3d79-154">指定"PopularItems"我们控件的名称。</span><span class="sxs-lookup"><span data-stu-id="e3d79-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="e3d79-155">请注意用户控件的文件扩展名是.ascx 不.aspx。</span><span class="sxs-lookup"><span data-stu-id="e3d79-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="e3d79-156">将按以下方式定义我们的常见项用户控制。</span><span class="sxs-lookup"><span data-stu-id="e3d79-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="e3d79-157">此处我们将使用我们没有尚未使用此应用程序中的方法。</span><span class="sxs-lookup"><span data-stu-id="e3d79-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="e3d79-158">我们将使用转发器控件和而不是使用数据源控件我们正在将转发器控件绑定到 LINQ to Entities 查询的结果。</span><span class="sxs-lookup"><span data-stu-id="e3d79-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="e3d79-159">在我们的控制代码隐藏做到这一点，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3d79-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="e3d79-160">另请注意在我们的控制标记顶部重要此行。</span><span class="sxs-lookup"><span data-stu-id="e3d79-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="e3d79-161">因为所有最常用的项不会更改基于分钟我们可以添加一个 aching 指令，用于改进我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="e3d79-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="e3d79-162">此指令将导致控件代码以缓存的输出的控件过期时只能执行。</span><span class="sxs-lookup"><span data-stu-id="e3d79-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="e3d79-163">否则，将使用的控件的输出缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="e3d79-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="e3d79-164">现在我们需要做的就是在我们 Default.aspc 页中包含我们新的控制。</span><span class="sxs-lookup"><span data-stu-id="e3d79-164">Now all we have to do is include our new control in our Default.aspc page.</span></span>

<span data-ttu-id="e3d79-165">使用拖放在我们的默认窗体的打开列放置控件的实例。</span><span class="sxs-lookup"><span data-stu-id="e3d79-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="e3d79-166">现在当我们运行我们的应用程序主页上显示的最常用的项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>  <span data-ttu-id="e3d79-167">"还购买"控制 （带参数的用户控件）</span><span class="sxs-lookup"><span data-stu-id="e3d79-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="e3d79-168">我们将创建第二个用户控件将会暗示通过添加上下文特殊性销售给下一个级别。</span><span class="sxs-lookup"><span data-stu-id="e3d79-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="e3d79-169">若要计算的顶部的"还购买"项的逻辑很重要。</span><span class="sxs-lookup"><span data-stu-id="e3d79-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="e3d79-170">我们"还购买"的控制将为当前所选的 ProductID 选择 （之前购买） 的 OrderDetails 记录，并获取每个唯一订单，它位于订单 id。</span><span class="sxs-lookup"><span data-stu-id="e3d79-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="e3d79-171">然后我们将选择 al 的产品从所有这些订单和购买数量的总和。</span><span class="sxs-lookup"><span data-stu-id="e3d79-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="e3d79-172">我们将按该数量之和的产品和显示的前五个项目。</span><span class="sxs-lookup"><span data-stu-id="e3d79-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="e3d79-173">考虑到此逻辑的复杂性，我们将为存储过程来实现此算法。</span><span class="sxs-lookup"><span data-stu-id="e3d79-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="e3d79-174">存储过程 T-SQL 的是，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3d79-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="e3d79-175">请注意此存储的过程 (SelectPurchasedWithProducts) 存在于数据库中，当我们在我们的应用程序，我们生成我们指定，除了的表和视图，我们需要实体数据模型的实体数据模型时包括应包括此存储的过程。</span><span class="sxs-lookup"><span data-stu-id="e3d79-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="e3d79-176">若要从实体数据模型中访问该存储的过程，我们需要将函数导入。</span><span class="sxs-lookup"><span data-stu-id="e3d79-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="e3d79-177">双击实体数据模型，在解决方案资源管理器，以在设计器中打开它并打开模型浏览器中，然后在设计器中右键单击并选择"添加函数导入"。</span><span class="sxs-lookup"><span data-stu-id="e3d79-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="e3d79-178">这样将打开此对话框。</span><span class="sxs-lookup"><span data-stu-id="e3d79-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="e3d79-179">正如你看到的更高版本，选择"SelectPurchasedWithProducts"填写字段并使用我们导入函数的名称的过程名称。</span><span class="sxs-lookup"><span data-stu-id="e3d79-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="e3d79-180">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="e3d79-180">Click "Ok".</span></span>

<span data-ttu-id="e3d79-181">具有执行此我们可以针对存储过程只需编程，因为我们可能会在模型中的任何其他项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="e3d79-182">因此，我们"控件"文件夹中创建一个名为 AlsoPurchased.ascx 的新用户控件。</span><span class="sxs-lookup"><span data-stu-id="e3d79-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="e3d79-183">对于此控件的标记看上去很眼熟 PopularItems 控制。</span><span class="sxs-lookup"><span data-stu-id="e3d79-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="e3d79-184">显著的区别是，不缓存输出，由于要的项的呈现将按产品而异。</span><span class="sxs-lookup"><span data-stu-id="e3d79-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="e3d79-185">ProductId 将是到控件的"属性"。</span><span class="sxs-lookup"><span data-stu-id="e3d79-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="e3d79-186">控件的 PreRender 事件处理程序中我们 eed 来做三件事。</span><span class="sxs-lookup"><span data-stu-id="e3d79-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="e3d79-187">请确保设置 ProductID。</span><span class="sxs-lookup"><span data-stu-id="e3d79-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="e3d79-188">查看是否存在与当前实例已购买任何产品。</span><span class="sxs-lookup"><span data-stu-id="e3d79-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="e3d79-189">输出为在 #2 中确定某些项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="e3d79-190">请注意调用存储的过程，通过模型是多么容易。</span><span class="sxs-lookup"><span data-stu-id="e3d79-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="e3d79-191">确定的存在"还购买"后我们可以只需将绑定中继器到由查询返回的结果。</span><span class="sxs-lookup"><span data-stu-id="e3d79-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="e3d79-192">如果不存在任何"还购买"项我们只需将从我们目录中显示其他常用的项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="e3d79-193">若要查看"还购买"项，请打开 ProductDetails.aspx 页，并将 AlsoPurchased 控件从解决方案资源管理器，以使其显示在标记中的此位置中。</span><span class="sxs-lookup"><span data-stu-id="e3d79-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="e3d79-194">这样将在 ProductDetails 页的顶部创建对控件的引用。</span><span class="sxs-lookup"><span data-stu-id="e3d79-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="e3d79-195">由于 AlsoPurchased 用户控件还需要大量 ProductId 我们将通过使用 Eval 语句的页的当前数据模型项针对我们的控制将 ProductID 属性设置。</span><span class="sxs-lookup"><span data-stu-id="e3d79-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="e3d79-196">当我们构建并立即运行并浏览到产品我们将看到"还购买"的项。</span><span class="sxs-lookup"><span data-stu-id="e3d79-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="e3d79-197">[上一页](tailspin-spyworks-part-6.md)
> [下一页](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="e3d79-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
