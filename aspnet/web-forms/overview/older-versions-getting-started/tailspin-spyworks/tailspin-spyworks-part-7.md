---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第 7 部分： 添加功能 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 7 部分添加了其他功能，例如查看帐户...
ms.author: aspnetcontent
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: 47402ccdfb702dc1bb1bdb4e634a7cd6f5ebc235
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831643"
---
<a name="part-7-adding-features"></a><span data-ttu-id="2de16-104">第 7 部分： 添加功能</span><span class="sxs-lookup"><span data-stu-id="2de16-104">Part 7: Adding Features</span></span>
====================
<span data-ttu-id="2de16-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="2de16-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="2de16-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="2de16-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="2de16-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="2de16-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="2de16-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="2de16-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="2de16-109">第 7 部分添加了其他功能，如帐户查看、 产品评论和"常用项"和"还已购买"用户控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>


## <a id="_Toc260221673"></a>  <span data-ttu-id="2de16-110">添加功能</span><span class="sxs-lookup"><span data-stu-id="2de16-110">Adding Features</span></span>

<span data-ttu-id="2de16-111">尽管用户可以浏览我们的目录，将项放在其购物车中并完成结帐过程，有大量的支持功能，我们将包括提高我们的站点。</span><span class="sxs-lookup"><span data-stu-id="2de16-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="2de16-112">帐户评审 （列表订单放置和查看详细信息。）</span><span class="sxs-lookup"><span data-stu-id="2de16-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="2de16-113">将一些上下文特定内容添加到首页。</span><span class="sxs-lookup"><span data-stu-id="2de16-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="2de16-114">在目录中添加特定功能，让用户查看的产品。</span><span class="sxs-lookup"><span data-stu-id="2de16-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="2de16-115">创建用户控件以在首页上显示控制的热门项目和位置。</span><span class="sxs-lookup"><span data-stu-id="2de16-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="2de16-116">创建"同时购买"的用户控件并将其添加到产品详细信息页。</span><span class="sxs-lookup"><span data-stu-id="2de16-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="2de16-117">添加联系人页面。</span><span class="sxs-lookup"><span data-stu-id="2de16-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="2de16-118">添加一页。</span><span class="sxs-lookup"><span data-stu-id="2de16-118">Add an About Page.</span></span>
8. <span data-ttu-id="2de16-119">全局错误</span><span class="sxs-lookup"><span data-stu-id="2de16-119">Global Error</span></span>

## <a id="_Toc260221674"></a>  <span data-ttu-id="2de16-120">帐户查看</span><span class="sxs-lookup"><span data-stu-id="2de16-120">Account Review</span></span>

<span data-ttu-id="2de16-121">在"帐户"文件夹中创建一个名为的 OrderList.aspx 和其他命名的 OrderDetails.aspx 的两个.aspx 页</span><span class="sxs-lookup"><span data-stu-id="2de16-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="2de16-122">OrderList.aspx 一样使用以前，我们将利用 GridView 和 EntityDataSoure 控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-122">OrderList.aspx will leverage the GridView and EntityDataSoure controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="2de16-123">EntityDataSoure 用户名已筛选的 Orders 表中选择记录 （请参阅 WhereParameter） 的用户日志时，我们设置会话变量中。</span><span class="sxs-lookup"><span data-stu-id="2de16-123">The EntityDataSoure selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="2de16-124">另请注意这些参数中的 GridView HyperlinkField:</span><span class="sxs-lookup"><span data-stu-id="2de16-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="2de16-125">这些名称指定作为 OrderDetails.aspx 页的查询字符串参数中指定的订单 id 字段的每个产品的订单详细信息视图的链接。</span><span class="sxs-lookup"><span data-stu-id="2de16-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a>  <span data-ttu-id="2de16-126">OrderDetails.aspx</span><span class="sxs-lookup"><span data-stu-id="2de16-126">OrderDetails.aspx</span></span>

<span data-ttu-id="2de16-127">我们将使用 EntityDataSource 控件访问订单和 FormView 以显示订单数据和与 GridView 的另一个 EntityDataSource 可显示所有订单的明细项目。</span><span class="sxs-lookup"><span data-stu-id="2de16-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="2de16-128">代码隐藏文件 (OrderDetails.aspx.cs) 中我们将两个小部分内部管理。</span><span class="sxs-lookup"><span data-stu-id="2de16-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="2de16-129">首先，我们需要确保 OrderDetails 始终获取 OrderId。</span><span class="sxs-lookup"><span data-stu-id="2de16-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="2de16-130">我们还需要计算和显示订单行项总计。</span><span class="sxs-lookup"><span data-stu-id="2de16-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>  <span data-ttu-id="2de16-131">主页页面</span><span class="sxs-lookup"><span data-stu-id="2de16-131">The Home Page</span></span>

<span data-ttu-id="2de16-132">让我们将某些静态内容添加到 Default.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="2de16-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="2de16-133">首先，我将创建一个"内容"文件夹并在该映像文件夹 （和我在这里提供要使用的主页上的图像。）</span><span class="sxs-lookup"><span data-stu-id="2de16-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="2de16-134">到 Default.aspx 页的底部占位符，添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="2de16-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>  <span data-ttu-id="2de16-135">产品评论</span><span class="sxs-lookup"><span data-stu-id="2de16-135">Product Reviews</span></span>

<span data-ttu-id="2de16-136">首先我们将我们可以使用输入产品评论的窗体添加一个具有一个链接按钮。</span><span class="sxs-lookup"><span data-stu-id="2de16-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="2de16-137">请注意我们在查询字符串中传递 ProductID</span><span class="sxs-lookup"><span data-stu-id="2de16-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="2de16-138">下一步让我们将添加名为 ReviewAdd.aspx 页</span><span class="sxs-lookup"><span data-stu-id="2de16-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="2de16-139">此页将使用 ASP.NET AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="2de16-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="2de16-140">如果你尚未做使您能够下载其从[DevExpress](http://devexpress.com/act)并且没有指南上设置用于与 Visual Studio 配合使用此处的工具包[ https://www.asp.net/learn/ajax-videos/video-76.aspx ](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)。</span><span class="sxs-lookup"><span data-stu-id="2de16-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="2de16-141">在设计模式下，从工具箱拖动控件和验证程序并生成类似于下面的窗体。</span><span class="sxs-lookup"><span data-stu-id="2de16-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="2de16-142">标记将如下所示。</span><span class="sxs-lookup"><span data-stu-id="2de16-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="2de16-143">现在，我们可以输入评论，允许在产品页上显示这些评论。</span><span class="sxs-lookup"><span data-stu-id="2de16-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="2de16-144">将此标记添加到 ProductDetails.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="2de16-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="2de16-145">运行应用程序现在并导航到产品显示产品信息包括客户的审阅。</span><span class="sxs-lookup"><span data-stu-id="2de16-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>  <span data-ttu-id="2de16-146">热门项目控件 （创建用户控件）</span><span class="sxs-lookup"><span data-stu-id="2de16-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="2de16-147">为了提高对您的网站的销售我们将添加到"暗示性销售"常用或相关产品的几个功能。</span><span class="sxs-lookup"><span data-stu-id="2de16-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="2de16-148">这些功能的第一个是在我们的产品目录的更多热门产品列表。</span><span class="sxs-lookup"><span data-stu-id="2de16-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="2de16-149">我们将创建一个"用户控件"以显示销售项在主页上我们的应用程序的顶部。</span><span class="sxs-lookup"><span data-stu-id="2de16-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="2de16-150">因为这将为一个控件，所以我们可以使用它在任何页上通过只需拖放控件拖到我们喜欢的任何页面上的 Visual Studio 设计器中。</span><span class="sxs-lookup"><span data-stu-id="2de16-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="2de16-151">在 Visual Studio 的解决方案资源管理器，右键单击解决方案名称并创建一个名为"控件"的新目录。</span><span class="sxs-lookup"><span data-stu-id="2de16-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="2de16-152">虽然不需要执行此操作，我们将帮助使我们的项目中按"控件"目录中创建我们的所有用户控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="2de16-153">右键单击控件文件夹并选择"新建项":</span><span class="sxs-lookup"><span data-stu-id="2de16-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="2de16-154">指定"PopularItems"我们控件的名称。</span><span class="sxs-lookup"><span data-stu-id="2de16-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="2de16-155">请注意，用户控件的文件扩展名是.ascx 不.aspx。</span><span class="sxs-lookup"><span data-stu-id="2de16-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="2de16-156">将按如下所示定义我们的常见项的用户控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="2de16-157">此处我们使用我们没有尚未使用此应用程序中的方法。</span><span class="sxs-lookup"><span data-stu-id="2de16-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="2de16-158">我们使用 repeater 控件，而不使用数据源控件我们将绑定到 LINQ to Entities 查询的结果 Repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="2de16-159">我们的控制代码隐藏中我们执行该操作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2de16-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="2de16-160">另请注意此重要的一行在我们的控件的标记的顶部。</span><span class="sxs-lookup"><span data-stu-id="2de16-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="2de16-161">由于最受欢迎的项不会更改按分钟，因此我们可以添加 aching 的指令以提高我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="2de16-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="2de16-162">此指令将导致该控件的缓存的输出过期时才可执行的控件代码。</span><span class="sxs-lookup"><span data-stu-id="2de16-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="2de16-163">否则，将使用的控件的输出缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="2de16-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="2de16-164">现在我们所要做的就是在我们 Default.aspc 页中包含我们新的控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-164">Now all we have to do is include our new control in our Default.aspc page.</span></span>

<span data-ttu-id="2de16-165">使用拖放打开列的默认窗体中放置控件的实例。</span><span class="sxs-lookup"><span data-stu-id="2de16-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="2de16-166">现在当我们运行我们的应用程序主页上显示的最受欢迎的项。</span><span class="sxs-lookup"><span data-stu-id="2de16-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>  <span data-ttu-id="2de16-167">"同时购买"控件 （使用参数的用户控件）</span><span class="sxs-lookup"><span data-stu-id="2de16-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="2de16-168">我们将创建第二个用户控件需要暗示性通过添加上下文特异性销售一层楼。</span><span class="sxs-lookup"><span data-stu-id="2de16-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="2de16-169">若要计算的前"同时购买"项的逻辑很重要。</span><span class="sxs-lookup"><span data-stu-id="2de16-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="2de16-170">我们"同时购买"的控件将当前所选 productid 选择 （之前购买） 的 OrderDetails 记录并获取有关位于每个唯一订单 Orderid。</span><span class="sxs-lookup"><span data-stu-id="2de16-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="2de16-171">然后我们将选择所有的产品从所有这些订单和购买所需数量的总和。</span><span class="sxs-lookup"><span data-stu-id="2de16-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="2de16-172">我们将通过该数量之和对产品进行排序和显示的前五个项目。</span><span class="sxs-lookup"><span data-stu-id="2de16-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="2de16-173">考虑到此逻辑的复杂性，我们将为存储过程来实现此算法。</span><span class="sxs-lookup"><span data-stu-id="2de16-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="2de16-174">T-SQL 存储过程是按如下所示。</span><span class="sxs-lookup"><span data-stu-id="2de16-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="2de16-175">请注意，当我们在我们的应用程序，我们生成我们指定的除了的表和视图，我们需要实体数据模型的实体数据模型时包括，此存储的过程 (SelectPurchasedWithProducts) 存在于数据库中应包含此存储的过程。</span><span class="sxs-lookup"><span data-stu-id="2de16-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="2de16-176">若要从实体数据模型访问存储的过程，我们需要将函数导入。</span><span class="sxs-lookup"><span data-stu-id="2de16-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="2de16-177">双击实体数据模型在解决方案资源管理器在设计器中打开它并打开模型浏览器，然后在设计器中右键单击并选择"添加函数导入"。</span><span class="sxs-lookup"><span data-stu-id="2de16-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="2de16-178">执行此操作将打开此对话框。</span><span class="sxs-lookup"><span data-stu-id="2de16-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="2de16-179">填写字段，正如您看到的更高版本，选择"SelectPurchasedWithProducts"并使用我们已导入函数的名称的过程名称。</span><span class="sxs-lookup"><span data-stu-id="2de16-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="2de16-180">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="2de16-180">Click "Ok".</span></span>

<span data-ttu-id="2de16-181">完成后此我们可以针对存储过程只是程序，因为我们可能会在模型中的任何其他项。</span><span class="sxs-lookup"><span data-stu-id="2de16-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="2de16-182">因此，我们"控件"文件夹中创建名为 AlsoPurchased.ascx 的新用户控件。</span><span class="sxs-lookup"><span data-stu-id="2de16-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="2de16-183">此控件的标记看上去很眼熟 PopularItems 控制。</span><span class="sxs-lookup"><span data-stu-id="2de16-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="2de16-184">明显的区别是，不缓存的输出，因为项的呈现将因产品。</span><span class="sxs-lookup"><span data-stu-id="2de16-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="2de16-185">产品 id 将是到该控件的"属性"。</span><span class="sxs-lookup"><span data-stu-id="2de16-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="2de16-186">控件的 PreRender 事件处理程序中我们 eed 来做三件事。</span><span class="sxs-lookup"><span data-stu-id="2de16-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="2de16-187">请确保设置 ProductID。</span><span class="sxs-lookup"><span data-stu-id="2de16-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="2de16-188">查看是否存在与当前已购买任何产品。</span><span class="sxs-lookup"><span data-stu-id="2de16-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="2de16-189">输出为在 #2 中确定一些项。</span><span class="sxs-lookup"><span data-stu-id="2de16-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="2de16-190">请注意调用存储的过程通过模型是多么容易。</span><span class="sxs-lookup"><span data-stu-id="2de16-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="2de16-191">确定，那里"还需购买"后我们可以只需绑定 repeater 到由查询返回的结果。</span><span class="sxs-lookup"><span data-stu-id="2de16-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="2de16-192">如果不是"同时购买"的任何项我们只需将从我们的目录中显示其他常用的项。</span><span class="sxs-lookup"><span data-stu-id="2de16-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="2de16-193">若要查看"同时购买"项，请打开 ProductDetails.aspx 页并从解决方案资源管理器拖动 AlsoPurchased 控件，它出现在标记中的此位置。</span><span class="sxs-lookup"><span data-stu-id="2de16-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="2de16-194">执行此操作将在 ProductDetails 页的顶部创建对控件的引用。</span><span class="sxs-lookup"><span data-stu-id="2de16-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="2de16-195">由于 AlsoPurchased 用户控件需要产品 Id 号，因此我们将使用针对页的当前数据模型项的 Eval 语句设置我们的控件的 ProductID 属性。</span><span class="sxs-lookup"><span data-stu-id="2de16-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="2de16-196">当我们构建并立即运行并浏览到某个产品时我们会看到"同时购买"项。</span><span class="sxs-lookup"><span data-stu-id="2de16-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="2de16-197">[上一页](tailspin-spyworks-part-6.md)
> [下一页](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="2de16-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
