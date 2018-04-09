---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 显示数据的项，并详细介绍 |Microsoft 文档
author: Erikre
description: 本系列教程将教您生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 5fea654aa5116193cb7496c1b9020ed8e25fc06f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="display-data-items-and-details"></a><span data-ttu-id="b9937-103">显示数据项和详细信息</span><span class="sxs-lookup"><span data-stu-id="b9937-103">Display Data Items and Details</span></span>
====================
<span data-ttu-id="b9937-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="b9937-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="b9937-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9937-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="b9937-106">本系列教程将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="b9937-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="b9937-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)是可以附带本系列教程。</span><span class="sxs-lookup"><span data-stu-id="b9937-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="b9937-108">本教程介绍如何显示数据项和使用 ASP.NET Web 窗体和 Entity Framework Code First 数据项详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9937-108">This tutorial describes how to display data items and data item details using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="b9937-109">本教程以前一教程"UI 和导航"上构建，并为 Wingtip 无实用价值应用商店教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="b9937-109">This tutorial builds on the previous tutorial "UI and Navigation" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="b9937-110">当你已完成本教程时，你将能够查看产品上*ProductsList.aspx*页和有关在上一单个产品的详细信息*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-110">When you've completed this tutorial, you'll be able to see products on the *ProductsList.aspx* page and details about an individual product on the *ProductDetails.aspx* page.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b9937-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="b9937-111">What you'll learn:</span></span>

- <span data-ttu-id="b9937-112">如何添加数据控件用于显示从数据库的产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-112">How to add a data control to display products from the database.</span></span>
- <span data-ttu-id="b9937-113">如何连接到所选数据的数据控件。</span><span class="sxs-lookup"><span data-stu-id="b9937-113">How to connect a data control to the selected data.</span></span>
- <span data-ttu-id="b9937-114">如何添加数据控件以显示从数据库的产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9937-114">How to add a data control to display product details from the database.</span></span>
- <span data-ttu-id="b9937-115">如何检索查询字符串的值并使用该值来限制从数据库中检索的数据。</span><span class="sxs-lookup"><span data-stu-id="b9937-115">How to retrieve a value from the query string and use that value to limit the data that's retrieved from the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="b9937-116">以下是本教程中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="b9937-116">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="b9937-117">模型绑定</span><span class="sxs-lookup"><span data-stu-id="b9937-117">Model Binding</span></span>
- <span data-ttu-id="b9937-118">值在提供程序</span><span class="sxs-lookup"><span data-stu-id="b9937-118">Value providers</span></span>

## <a name="adding-a-data-control-to-display-products"></a><span data-ttu-id="b9937-119">添加一个数据控件来显示产品</span><span class="sxs-lookup"><span data-stu-id="b9937-119">Adding a Data Control to Display Products</span></span>

<span data-ttu-id="b9937-120">当将数据绑定到服务器控件，有几个不同选项，你可以使用。</span><span class="sxs-lookup"><span data-stu-id="b9937-120">When binding data to a server control, there are a few different options you can use.</span></span> <span data-ttu-id="b9937-121">最常用的选项包括添加数据源控件、 进行手动添加代码或使用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="b9937-121">The most common options include adding a data source control, adding code by hand, or using model binding.</span></span>

### <a name="using-a-data-source-control-to-bind-data"></a><span data-ttu-id="b9937-122">使用数据源控件将数据绑定</span><span class="sxs-lookup"><span data-stu-id="b9937-122">Using a Data Source Control to Bind Data</span></span>

<span data-ttu-id="b9937-123">添加数据源控件，可将数据源控件链接到显示的数据的控件。</span><span class="sxs-lookup"><span data-stu-id="b9937-123">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="b9937-124">此方法允许你以声明方式服务器端控件直接连接到数据源，而不是使用编程方法。</span><span class="sxs-lookup"><span data-stu-id="b9937-124">This approach allows you to declaratively connect server-side controls directly to data sources, rather than using a programmatic approach.</span></span>

### <a name="coding-by-hand-to-bind-data"></a><span data-ttu-id="b9937-125">编码手动将数据绑定</span><span class="sxs-lookup"><span data-stu-id="b9937-125">Coding By Hand to Bind Data</span></span>

<span data-ttu-id="b9937-126">添加手动的代码涉及读取的值、 检查有 null 值，尝试将其转换为适当的类型，检查指示转换是否成功，以及最后，在查询中使用的值。</span><span class="sxs-lookup"><span data-stu-id="b9937-126">Adding code by hand involves reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="b9937-127">当你需要保留对你的数据访问逻辑的完全控制时，将使用此方法。</span><span class="sxs-lookup"><span data-stu-id="b9937-127">You would use this approach when you need to retain full control over your data-access logic.</span></span>

### <a name="using-model-binding-to-bind-data"></a><span data-ttu-id="b9937-128">使用模型绑定，使其将数据绑定</span><span class="sxs-lookup"><span data-stu-id="b9937-128">Using Model Binding to Bind Data</span></span>

<span data-ttu-id="b9937-129">使用模型绑定允许你将使用更少代码的结果绑定，而使你能够重复使用在整个应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="b9937-129">Using model binding allows you to bind results using far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="b9937-130">模型绑定旨在简化代码为中心的数据访问逻辑的处理，同时仍然保留丰富、 数据绑定的框架的优点。</span><span class="sxs-lookup"><span data-stu-id="b9937-130">Model binding aims to simplify working with code-focused data-access logic while still retaining the benefits of a rich, data-binding framework.</span></span>

## <a name="displaying-products"></a><span data-ttu-id="b9937-131">显示产品</span><span class="sxs-lookup"><span data-stu-id="b9937-131">Displaying Products</span></span>

<span data-ttu-id="b9937-132">在本教程中，你将使用模型绑定将数据绑定。</span><span class="sxs-lookup"><span data-stu-id="b9937-132">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="b9937-133">若要配置一个数据控件要使用模型绑定来选择数据，你设置的控件的`SelectMethod`属性页的代码中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="b9937-133">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to the name of a method in the page's code.</span></span> <span data-ttu-id="b9937-134">数据控件在页生命周期中适当的时间调用的方法，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="b9937-134">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="b9937-135">没有无需显式调用`DataBind`方法。</span><span class="sxs-lookup"><span data-stu-id="b9937-135">There's no need to explicitly call the `DataBind` method.</span></span>

<span data-ttu-id="b9937-136">使用以下步骤，您将修改中的标记*ProductList.aspx*页，以便所页可以显示产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-136">Using the steps below, you'll modify the markup in the *ProductList.aspx* page so that the page can display products.</span></span>

1. <span data-ttu-id="b9937-137">在**解决方案资源管理器**，打开*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-137">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
2. <span data-ttu-id="b9937-138">将现有的标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="b9937-138">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="b9937-139">此代码使用**ListView**控件名为"productList"若要显示的产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-139">This code uses a **ListView** control named "productList" to display the products.</span></span>

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="b9937-140">**ListView**控件使用的模板和样式定义的格式显示数据。</span><span class="sxs-lookup"><span data-stu-id="b9937-140">The **ListView** control displays data in a format that you define by using templates and styles.</span></span> <span data-ttu-id="b9937-141">它是适用于任何重复结构中的数据。</span><span class="sxs-lookup"><span data-stu-id="b9937-141">It is useful for data in any repeating structure.</span></span> <span data-ttu-id="b9937-142">这**ListView**示例只是显示数据库，但是你可以启用用户能够编辑、 插入和删除数据，并能够排序和页数据，所有操作代码中的数据。</span><span class="sxs-lookup"><span data-stu-id="b9937-142">This **ListView** example simply shows data from the database, however you can enable users to edit, insert, and delete data, and to sort and page data, all without code.</span></span>

<span data-ttu-id="b9937-143">通过设置`ItemType`中的属性**ListView**控制，数据绑定表达式`Item`可用和控件将成为强类型化。</span><span class="sxs-lookup"><span data-stu-id="b9937-143">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="b9937-144">根据前面的教程中所述，你可以选择使用 IntelliSense，例如，指定项对象的详细信息`ProductName`:</span><span class="sxs-lookup"><span data-stu-id="b9937-144">As mentioned in the previous tutorial, you can select details of the Item object using IntelliSense, such as specifying the `ProductName`:</span></span>

![显示数据项数和详细信息的 IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="b9937-146">此外，所使用模型绑定指定`SelectMethod`值。</span><span class="sxs-lookup"><span data-stu-id="b9937-146">In addition, you are using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="b9937-147">此值 (`GetProducts`) 将对应于你将添加到背后的代码在下一步中显示产品的方法。</span><span class="sxs-lookup"><span data-stu-id="b9937-147">This value (`GetProducts`) will correspond to the method that you will add to the code behind to display products in the next step.</span></span>

### <a name="adding-code-to-display-products"></a><span data-ttu-id="b9937-148">添加代码以显示产品</span><span class="sxs-lookup"><span data-stu-id="b9937-148">Adding Code to Display Products</span></span>

<span data-ttu-id="b9937-149">在此步骤中，你将添加代码以填充**ListView**与数据库中的产品数据的控件。</span><span class="sxs-lookup"><span data-stu-id="b9937-149">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="b9937-150">代码将支持单个类别中，以及显示的所有产品都显示产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-150">The code will support showing products by individual category, as well as showing all products.</span></span>

1. <span data-ttu-id="b9937-151">在**解决方案资源管理器**，右键单击*ProductList.aspx* ，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="b9937-151">In **Solution Explorer**, right-click *ProductList.aspx* and then click **View Code**.</span></span>
2. <span data-ttu-id="b9937-152">中的现有代码替换*ProductList.aspx.cs*文件替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b9937-152">Replace the existing code in the *ProductList.aspx.cs* file with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="b9937-153">此代码演示`GetProducts`被引用的方法`ItemType`属性**ListView**中控制*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-153">This code shows the `GetProducts` method that's referenced by the `ItemType` property of the **ListView** control in the *ProductList.aspx* page.</span></span> <span data-ttu-id="b9937-154">若要将结果限制为在数据库中的特定类别，该代码将设置`categoryId`传递给查询字符串值的值*ProductList.aspx*时页*ProductList.aspx*页导航到。</span><span class="sxs-lookup"><span data-stu-id="b9937-154">To limit the results to a specific category in the database, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="b9937-155">`QueryStringAttribute`类`System.Web.ModelBinding`命名空间用于检索查询字符串变量 id 的值。这会指示要尝试将值绑定到查询字符串中的模型绑定`categoryId`在运行时的参数。</span><span class="sxs-lookup"><span data-stu-id="b9937-155">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable id. This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="b9937-156">有效的类别作为查询字符串传递给页上，当查询的结果被限制为这些数据库中的产品的匹配`categoryId`值。</span><span class="sxs-lookup"><span data-stu-id="b9937-156">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="b9937-157">例如，如果的 URL *ProductsList.aspx*页是以下：</span><span class="sxs-lookup"><span data-stu-id="b9937-157">For instance, if the URL to the *ProductsList.aspx* page is the following:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="b9937-158">页仅显示产品其中`category`等于`1`。</span><span class="sxs-lookup"><span data-stu-id="b9937-158">The page displays only the products where the `category` equals `1`.</span></span>

<span data-ttu-id="b9937-159">如果没有查询字符串包括，则导航到时*ProductList.aspx*页上，所有产品都将都显示。</span><span class="sxs-lookup"><span data-stu-id="b9937-159">If no query string is included when navigating to the *ProductList.aspx* page, all products will be displayed.</span></span>

<span data-ttu-id="b9937-160">这些方法的值的源被称为*值提供程序*(如*QueryString*)，并指示要使用的值提供程序的参数属性统称为值提供程序属性 (如"`id`")。</span><span class="sxs-lookup"><span data-stu-id="b9937-160">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as value provider attributes (such as "`id`").</span></span> <span data-ttu-id="b9937-161">ASP.NET Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态、 会话状态和配置文件属性中包括值在提供程序和所有用户输入的典型源的相应属性。</span><span class="sxs-lookup"><span data-stu-id="b9937-161">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="b9937-162">你还可以编写自定义值在提供程序。</span><span class="sxs-lookup"><span data-stu-id="b9937-162">You can also write custom value providers.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="b9937-163">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="b9937-163">Running the Application</span></span>

<span data-ttu-id="b9937-164">运行应用程序现在以查看如何查看所有产品或只是一套产品类别受限制。</span><span class="sxs-lookup"><span data-stu-id="b9937-164">Run the application now to see how you can view all of the products or just a set of products limited by category.</span></span>

1. <span data-ttu-id="b9937-165">在**解决方案资源管理器**，右键单击*Default.aspx*页，选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="b9937-165">In the **Solution Explorer**, right-click the *Default.aspx* page and select **View in Browser**.</span></span>  
 <span data-ttu-id="b9937-166">浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-166">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="b9937-167">选择**汽车**从产品类别导航菜单。</span><span class="sxs-lookup"><span data-stu-id="b9937-167">Select **Cars** from the product category navigation menu.</span></span>  
 <span data-ttu-id="b9937-168">*ProductList.aspx*显示仅"汽车"类别中包含的产品显示页。</span><span class="sxs-lookup"><span data-stu-id="b9937-168">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> <span data-ttu-id="b9937-169">稍后在本教程中，将显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9937-169">Later in this tutorial, you will display product details.</span></span>  

    ![显示数据项数和详细信息-汽车](display_data_items_and_details/_static/image2.png)
3. <span data-ttu-id="b9937-171">选择**产品**从顶部导航菜单。</span><span class="sxs-lookup"><span data-stu-id="b9937-171">Select **Products** from the navigation menu at the top.</span></span>  
 <span data-ttu-id="b9937-172">同样， *ProductList.aspx*页将显示，但这次它显示的产品的整个列表。</span><span class="sxs-lookup"><span data-stu-id="b9937-172">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![显示数据项数和详细信息-产品](display_data_items_and_details/_static/image3.png)
4. <span data-ttu-id="b9937-174">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b9937-174">Close the browser and return to Visual Studio.</span></span>

### <a name="adding-a-data-control-to-display-product-details"></a><span data-ttu-id="b9937-175">添加一个数据控件来显示产品详细信息</span><span class="sxs-lookup"><span data-stu-id="b9937-175">Adding a Data Control to Display Product Details</span></span>

<span data-ttu-id="b9937-176">接下来，将修改中的标记*ProductDetails.aspx*以便页可以显示有关各个产品的信息在前面的教程中添加的页。</span><span class="sxs-lookup"><span data-stu-id="b9937-176">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial so that the page can display information about an individual product.</span></span>

1. <span data-ttu-id="b9937-177">在**解决方案资源管理器**，打开*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-177">In **Solution Explorer**, open the *ProductDetails.aspx* page.</span></span>
2. <span data-ttu-id="b9937-178">将现有的标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="b9937-178">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

<span data-ttu-id="b9937-179">此代码使用**FormView**控件来显示有关各个产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9937-179">This code uses a **FormView** control to display details about an individual product.</span></span> <span data-ttu-id="b9937-180">此标记使用的一样，用于显示中的数据的方法*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-180">This markup uses methods like those that are used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="b9937-181">**FormView**控件用于从数据源一次显示一条记录。</span><span class="sxs-lookup"><span data-stu-id="b9937-181">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="b9937-182">当你使用**FormView**控件，您创建模板，用于显示和编辑数据绑定值。</span><span class="sxs-lookup"><span data-stu-id="b9937-182">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="b9937-183">这些模板包含，绑定表达式和格式设置用于定义控件的外观和表单的功能。</span><span class="sxs-lookup"><span data-stu-id="b9937-183">The templates contain controls, binding expressions, and formatting that define the look and functionality of the form.</span></span>

<span data-ttu-id="b9937-184">若要连接到数据库的上面的标记，必须添加到的其他代码*ProductDetails.aspx*代码。</span><span class="sxs-lookup"><span data-stu-id="b9937-184">To connect the above markup to the database, you must add additional code to the *ProductDetails.aspx* code.</span></span>

1. <span data-ttu-id="b9937-185">在**解决方案资源管理器**，右键单击*ProductDetails.aspx* ，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="b9937-185">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="b9937-186">*ProductDetails.aspx.cs*文件将会显示。</span><span class="sxs-lookup"><span data-stu-id="b9937-186">The *ProductDetails.aspx.cs* file will be displayed.</span></span>
2. <span data-ttu-id="b9937-187">用下面的代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="b9937-187">Replace the existing code with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="b9937-188">此代码检查"`productID`"查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="b9937-188">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="b9937-189">如果找到一个有效的查询字符串值，则将显示匹配的产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-189">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="b9937-190">如果不找到任何查询字符串，或查询字符串值无效，不到产品将显示在*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-190">If no query-string is found, or the query-string value is not valid, no product is displayed on the *ProductDetails.aspx* page.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="b9937-191">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="b9937-191">Running the Application</span></span>

<span data-ttu-id="b9937-192">现在你可以运行应用程序以查看单个产品显示基于产品的 id。</span><span class="sxs-lookup"><span data-stu-id="b9937-192">Now you can run the application to see an individual product displayed based on the id of the product.</span></span>

1. <span data-ttu-id="b9937-193">按**F5** Visual Studio 运行应用程序中时，在。</span><span class="sxs-lookup"><span data-stu-id="b9937-193">Press **F5** while in Visual Studio to run the application.</span></span>  
 <span data-ttu-id="b9937-194">浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="b9937-194">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="b9937-195">从类别导航菜单中选择"船"。</span><span class="sxs-lookup"><span data-stu-id="b9937-195">Select "Boats" from the category navigation menu.</span></span>  
 <span data-ttu-id="b9937-196">*ProductList.aspx*显示页。</span><span class="sxs-lookup"><span data-stu-id="b9937-196">The *ProductList.aspx* page is displayed.</span></span>
3. <span data-ttu-id="b9937-197">从产品列表中选择"纸张船"产品。</span><span class="sxs-lookup"><span data-stu-id="b9937-197">Select the "Paper Boat" product from the product list.</span></span>  
 <span data-ttu-id="b9937-198">*ProductDetails.aspx*显示页。</span><span class="sxs-lookup"><span data-stu-id="b9937-198">The *ProductDetails.aspx* page is displayed.</span></span>   

    ![显示数据项数和详细信息-产品](display_data_items_and_details/_static/image4.png)
4. <span data-ttu-id="b9937-200">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="b9937-200">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="b9937-201">总结</span><span class="sxs-lookup"><span data-stu-id="b9937-201">Summary</span></span>

<span data-ttu-id="b9937-202">在本教程中的序列中，你已添加标记和代码以显示产品列表并显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9937-202">In this tutorial of the series you have add markup and code to display a product list and to display product details.</span></span> <span data-ttu-id="b9937-203">在此过程中，你已了解有关强类型化的数据控件、 模型绑定和值在提供程序。</span><span class="sxs-lookup"><span data-stu-id="b9937-203">During this process you have learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="b9937-204">在下一步的教程中，你将添加购物车 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9937-204">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9937-205">其他资源</span><span class="sxs-lookup"><span data-stu-id="b9937-205">Additional Resources</span></span>

[<span data-ttu-id="b9937-206">检索和显示使用模型的绑定和 web 窗体的数据</span><span class="sxs-lookup"><span data-stu-id="b9937-206">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

> [!div class="step-by-step"]
> <span data-ttu-id="b9937-207">[上一页](ui_and_navigation.md)
> [下一页](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="b9937-207">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
