---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 显示数据项和详细信息 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 2184c04d5f2361526be0409178dc0a6c665ebc4f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833102"
---
<a name="display-data-items-and-details"></a><span data-ttu-id="c5461-103">显示数据项和详细信息</span><span class="sxs-lookup"><span data-stu-id="c5461-103">Display Data Items and Details</span></span>
====================
<span data-ttu-id="c5461-104">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="c5461-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="c5461-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="c5461-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="c5461-106">此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="c5461-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="c5461-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。</span><span class="sxs-lookup"><span data-stu-id="c5461-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="c5461-108">本教程介绍如何显示数据项和使用 ASP.NET Web 窗体和 Entity Framework Code First 数据项详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5461-108">This tutorial describes how to display data items and data item details using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="c5461-109">本教程基于上一教程"UI 和导航"，而是 Wingtip Toy 存储教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="c5461-109">This tutorial builds on the previous tutorial "UI and Navigation" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="c5461-110">完成本教程后，你将能够查看产品上*ProductsList.aspx*页，以及详细信息上的各个产品*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-110">When you've completed this tutorial, you'll be able to see products on the *ProductsList.aspx* page and details about an individual product on the *ProductDetails.aspx* page.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c5461-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="c5461-111">What you'll learn:</span></span>

- <span data-ttu-id="c5461-112">如何添加数据控件用于显示数据库中的产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-112">How to add a data control to display products from the database.</span></span>
- <span data-ttu-id="c5461-113">如何连接到所选数据的数据控件。</span><span class="sxs-lookup"><span data-stu-id="c5461-113">How to connect a data control to the selected data.</span></span>
- <span data-ttu-id="c5461-114">如何添加用来显示产品详细信息，从数据库的数据控件。</span><span class="sxs-lookup"><span data-stu-id="c5461-114">How to add a data control to display product details from the database.</span></span>
- <span data-ttu-id="c5461-115">了解如何从查询字符串中检索值并使用该值来限制从数据库中检索的数据。</span><span class="sxs-lookup"><span data-stu-id="c5461-115">How to retrieve a value from the query string and use that value to limit the data that's retrieved from the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="c5461-116">以下是本教程中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="c5461-116">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="c5461-117">模型绑定</span><span class="sxs-lookup"><span data-stu-id="c5461-117">Model Binding</span></span>
- <span data-ttu-id="c5461-118">值提供程序</span><span class="sxs-lookup"><span data-stu-id="c5461-118">Value providers</span></span>

## <a name="adding-a-data-control-to-display-products"></a><span data-ttu-id="c5461-119">添加用来显示产品的数据控件</span><span class="sxs-lookup"><span data-stu-id="c5461-119">Adding a Data Control to Display Products</span></span>

<span data-ttu-id="c5461-120">当数据绑定到服务器控件，有几个不同选项，可以使用。</span><span class="sxs-lookup"><span data-stu-id="c5461-120">When binding data to a server control, there are a few different options you can use.</span></span> <span data-ttu-id="c5461-121">最常用的选项包括添加数据源控件、 添加代码，或使用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="c5461-121">The most common options include adding a data source control, adding code by hand, or using model binding.</span></span>

### <a name="using-a-data-source-control-to-bind-data"></a><span data-ttu-id="c5461-122">使用数据源控件以将数据绑定</span><span class="sxs-lookup"><span data-stu-id="c5461-122">Using a Data Source Control to Bind Data</span></span>

<span data-ttu-id="c5461-123">添加数据源控件，可将数据源控件链接到显示的数据的控件。</span><span class="sxs-lookup"><span data-stu-id="c5461-123">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="c5461-124">此方法允许你以声明方式服务器端控件直接连接到数据源，而不是使用编程方法。</span><span class="sxs-lookup"><span data-stu-id="c5461-124">This approach allows you to declaratively connect server-side controls directly to data sources, rather than using a programmatic approach.</span></span>

### <a name="coding-by-hand-to-bind-data"></a><span data-ttu-id="c5461-125">手动编写代码以将数据绑定</span><span class="sxs-lookup"><span data-stu-id="c5461-125">Coding By Hand to Bind Data</span></span>

<span data-ttu-id="c5461-126">添加通过手动代码涉及到读取的值、 检查 null 值、 尝试将其转换为适当的类型、 检查转换是否成功，和最后，在查询中使用的值。</span><span class="sxs-lookup"><span data-stu-id="c5461-126">Adding code by hand involves reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="c5461-127">当您需要保留对数据访问逻辑的完全控制时，可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="c5461-127">You would use this approach when you need to retain full control over your data-access logic.</span></span>

### <a name="using-model-binding-to-bind-data"></a><span data-ttu-id="c5461-128">使用模型绑定将数据绑定</span><span class="sxs-lookup"><span data-stu-id="c5461-128">Using Model Binding to Bind Data</span></span>

<span data-ttu-id="c5461-129">使用模型绑定，可将使用很少的代码的结果绑定，并使你能够重复使用在整个应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="c5461-129">Using model binding allows you to bind results using far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="c5461-130">模型绑定的目标是简化使用代码为中心的数据访问逻辑，同时保留一个丰富的数据绑定框架的好处。</span><span class="sxs-lookup"><span data-stu-id="c5461-130">Model binding aims to simplify working with code-focused data-access logic while still retaining the benefits of a rich, data-binding framework.</span></span>

## <a name="displaying-products"></a><span data-ttu-id="c5461-131">显示产品</span><span class="sxs-lookup"><span data-stu-id="c5461-131">Displaying Products</span></span>

<span data-ttu-id="c5461-132">在本教程中，您将使用模型绑定将数据绑定。</span><span class="sxs-lookup"><span data-stu-id="c5461-132">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="c5461-133">若要配置以使用模型绑定选择数据的数据控件，设置控件的`SelectMethod`属性设置为在页面的代码中方法的名称。</span><span class="sxs-lookup"><span data-stu-id="c5461-133">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to the name of a method in the page's code.</span></span> <span data-ttu-id="c5461-134">数据控件在页生命周期中的适当时间调用的方法，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="c5461-134">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="c5461-135">无需显式调用`DataBind`方法。</span><span class="sxs-lookup"><span data-stu-id="c5461-135">There's no need to explicitly call the `DataBind` method.</span></span>

<span data-ttu-id="c5461-136">使用以下步骤，将修改中的标记*ProductList.aspx*页，以便可显示产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-136">Using the steps below, you'll modify the markup in the *ProductList.aspx* page so that the page can display products.</span></span>

1. <span data-ttu-id="c5461-137">在中**解决方案资源管理器**，打开*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-137">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
2. <span data-ttu-id="c5461-138">现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="c5461-138">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="c5461-139">此代码使用**ListView**控件命名为"productList"若要显示的产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-139">This code uses a **ListView** control named "productList" to display the products.</span></span>

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="c5461-140">**ListView**控件通过使用模板和样式定义的格式显示数据。</span><span class="sxs-lookup"><span data-stu-id="c5461-140">The **ListView** control displays data in a format that you define by using templates and styles.</span></span> <span data-ttu-id="c5461-141">它可用于任何重复结构中的数据。</span><span class="sxs-lookup"><span data-stu-id="c5461-141">It is useful for data in any repeating structure.</span></span> <span data-ttu-id="c5461-142">这**ListView**示例只是显示了从数据库中，但是可以让用户可以编辑、 插入和删除数据，并进行排序和页面数据，不需代码的数据。</span><span class="sxs-lookup"><span data-stu-id="c5461-142">This **ListView** example simply shows data from the database, however you can enable users to edit, insert, and delete data, and to sort and page data, all without code.</span></span>

<span data-ttu-id="c5461-143">通过设置`ItemType`中的属性**ListView**控件，数据绑定表达式`Item`可用和控件将成为强类型化。</span><span class="sxs-lookup"><span data-stu-id="c5461-143">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="c5461-144">在上一教程中所述，可以选择使用 IntelliSense，例如，指定的项对象的详细信息`ProductName`:</span><span class="sxs-lookup"><span data-stu-id="c5461-144">As mentioned in the previous tutorial, you can select details of the Item object using IntelliSense, such as specifying the `ProductName`:</span></span>

![显示数据的项和详细信息-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="c5461-146">此外，您使用模型绑定程序指定`SelectMethod`值。</span><span class="sxs-lookup"><span data-stu-id="c5461-146">In addition, you are using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="c5461-147">此值 (`GetProducts`) 将对应于将添加到代码隐藏来显示产品下一步中的方法。</span><span class="sxs-lookup"><span data-stu-id="c5461-147">This value (`GetProducts`) will correspond to the method that you will add to the code behind to display products in the next step.</span></span>

### <a name="adding-code-to-display-products"></a><span data-ttu-id="c5461-148">添加代码以显示产品</span><span class="sxs-lookup"><span data-stu-id="c5461-148">Adding Code to Display Products</span></span>

<span data-ttu-id="c5461-149">在此步骤中，将添加代码以填充**ListView**产品数据库中的数据的控件。</span><span class="sxs-lookup"><span data-stu-id="c5461-149">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="c5461-150">该代码将支持通过单个类别，以及显示所有产品都显示产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-150">The code will support showing products by individual category, as well as showing all products.</span></span>

1. <span data-ttu-id="c5461-151">在中**解决方案资源管理器**，右键单击*ProductList.aspx* ，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="c5461-151">In **Solution Explorer**, right-click *ProductList.aspx* and then click **View Code**.</span></span>
2. <span data-ttu-id="c5461-152">中的现有代码替换*ProductList.aspx.cs*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="c5461-152">Replace the existing code in the *ProductList.aspx.cs* file with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="c5461-153">此代码演示`GetProducts`引用的方法`ItemType`属性**ListView**控制*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-153">This code shows the `GetProducts` method that's referenced by the `ItemType` property of the **ListView** control in the *ProductList.aspx* page.</span></span> <span data-ttu-id="c5461-154">若要将结果限制为在数据库中的特定类别，该代码将设置`categoryId`值从查询字符串值传递给*ProductList.aspx*时页*ProductList.aspx*页导航到。</span><span class="sxs-lookup"><span data-stu-id="c5461-154">To limit the results to a specific category in the database, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="c5461-155">`QueryStringAttribute`类中`System.Web.ModelBinding`命名空间用于检索查询字符串变量 id 的值。这会指示要尝试将值绑定到查询字符串中的模型绑定`categoryId`在运行时参数。</span><span class="sxs-lookup"><span data-stu-id="c5461-155">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable id. This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="c5461-156">有效的类别作为查询字符串传递给页上，当查询的结果被限制为匹配数据库中这些产品`categoryId`值。</span><span class="sxs-lookup"><span data-stu-id="c5461-156">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="c5461-157">例如，如果到 URL *ProductsList.aspx*页是以下：</span><span class="sxs-lookup"><span data-stu-id="c5461-157">For instance, if the URL to the *ProductsList.aspx* page is the following:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="c5461-158">页面仅显示产品其中`category`等于`1`。</span><span class="sxs-lookup"><span data-stu-id="c5461-158">The page displays only the products where the `category` equals `1`.</span></span>

<span data-ttu-id="c5461-159">导航到时，如果没有查询字符串包含*ProductList.aspx*页上，将显示所有产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-159">If no query string is included when navigating to the *ProductList.aspx* page, all products will be displayed.</span></span>

<span data-ttu-id="c5461-160">这些方法的值的源嘿 *值提供程序*(如*查询字符串*)，指示要使用的值提供程序的参数属性称为值提供程序属性 (如"`id`")。</span><span class="sxs-lookup"><span data-stu-id="c5461-160">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as value provider attributes (such as "`id`").</span></span> <span data-ttu-id="c5461-161">ASP.NET Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态，会话状态和配置文件属性中包含值提供程序和所有典型的资源，用户输入的相应属性。</span><span class="sxs-lookup"><span data-stu-id="c5461-161">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="c5461-162">此外可以编写自定义值提供程序。</span><span class="sxs-lookup"><span data-stu-id="c5461-162">You can also write custom value providers.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="c5461-163">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c5461-163">Running the Application</span></span>

<span data-ttu-id="c5461-164">运行应用程序现在，请参阅如何查看所有产品或只是一组有限的按类别的产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-164">Run the application now to see how you can view all of the products or just a set of products limited by category.</span></span>

1. <span data-ttu-id="c5461-165">在中**解决方案资源管理器**，右键单击*Default.aspx*页，然后选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="c5461-165">In the **Solution Explorer**, right-click the *Default.aspx* page and select **View in Browser**.</span></span>  
 <span data-ttu-id="c5461-166">在浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-166">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="c5461-167">选择**汽车**产品类别导航菜单中。</span><span class="sxs-lookup"><span data-stu-id="c5461-167">Select **Cars** from the product category navigation menu.</span></span>  
 <span data-ttu-id="c5461-168">*ProductList.aspx*显示仅"Cars"类别中包含的产品显示页。</span><span class="sxs-lookup"><span data-stu-id="c5461-168">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> <span data-ttu-id="c5461-169">稍后在本教程中，将显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5461-169">Later in this tutorial, you will display product details.</span></span>  

    ![显示数据的项和详细信息-汽车](display_data_items_and_details/_static/image2.png)
3. <span data-ttu-id="c5461-171">选择**产品**从顶部导航菜单。</span><span class="sxs-lookup"><span data-stu-id="c5461-171">Select **Products** from the navigation menu at the top.</span></span>  
 <span data-ttu-id="c5461-172">同样， *ProductList.aspx*页将显示，但这次它显示了产品的完整列表。</span><span class="sxs-lookup"><span data-stu-id="c5461-172">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![显示数据的项和详细信息-产品](display_data_items_and_details/_static/image3.png)
4. <span data-ttu-id="c5461-174">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c5461-174">Close the browser and return to Visual Studio.</span></span>

### <a name="adding-a-data-control-to-display-product-details"></a><span data-ttu-id="c5461-175">添加一个数据控件来显示产品详细信息</span><span class="sxs-lookup"><span data-stu-id="c5461-175">Adding a Data Control to Display Product Details</span></span>

<span data-ttu-id="c5461-176">接下来，将修改中的标记*ProductDetails.aspx*以便页面可以显示各个产品的信息添加上一教程中的页。</span><span class="sxs-lookup"><span data-stu-id="c5461-176">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial so that the page can display information about an individual product.</span></span>

1. <span data-ttu-id="c5461-177">在中**解决方案资源管理器**，打开*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-177">In **Solution Explorer**, open the *ProductDetails.aspx* page.</span></span>
2. <span data-ttu-id="c5461-178">现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="c5461-178">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

<span data-ttu-id="c5461-179">此代码使用**FormView**控件来显示有关单个产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5461-179">This code uses a **FormView** control to display details about an individual product.</span></span> <span data-ttu-id="c5461-180">此标记使用方法，如用于显示数据中的那些*ProductList.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-180">This markup uses methods like those that are used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="c5461-181">**FormView**控件用于从数据源一次显示一条记录。</span><span class="sxs-lookup"><span data-stu-id="c5461-181">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="c5461-182">当你使用**FormView**控件，您创建模板来显示和编辑数据绑定值。</span><span class="sxs-lookup"><span data-stu-id="c5461-182">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="c5461-183">这些模板包含，绑定表达式和格式设置用于定义控件的外观和功能的窗体。</span><span class="sxs-lookup"><span data-stu-id="c5461-183">The templates contain controls, binding expressions, and formatting that define the look and functionality of the form.</span></span>

<span data-ttu-id="c5461-184">若要连接到数据库的更高版本的标记，必须添加到其他代码*ProductDetails.aspx*代码。</span><span class="sxs-lookup"><span data-stu-id="c5461-184">To connect the above markup to the database, you must add additional code to the *ProductDetails.aspx* code.</span></span>

1. <span data-ttu-id="c5461-185">在中**解决方案资源管理器**，右键单击*ProductDetails.aspx* ，然后单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="c5461-185">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="c5461-186">*ProductDetails.aspx.cs*文件将会显示。</span><span class="sxs-lookup"><span data-stu-id="c5461-186">The *ProductDetails.aspx.cs* file will be displayed.</span></span>
2. <span data-ttu-id="c5461-187">用下面的代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="c5461-187">Replace the existing code with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="c5461-188">此代码检查"`productID`"查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="c5461-188">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="c5461-189">如果找到有效的查询字符串值，则将显示匹配的产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-189">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="c5461-190">如果不找到任何查询字符串，或查询字符串值无效，没有任何产品显示在*ProductDetails.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-190">If no query-string is found, or the query-string value is not valid, no product is displayed on the *ProductDetails.aspx* page.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="c5461-191">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c5461-191">Running the Application</span></span>

<span data-ttu-id="c5461-192">现在可以运行应用程序以查看显示的各个产品根据产品的 id。</span><span class="sxs-lookup"><span data-stu-id="c5461-192">Now you can run the application to see an individual product displayed based on the id of the product.</span></span>

1. <span data-ttu-id="c5461-193">按**F5**在 Visual Studio 运行应用程序中。</span><span class="sxs-lookup"><span data-stu-id="c5461-193">Press **F5** while in Visual Studio to run the application.</span></span>  
 <span data-ttu-id="c5461-194">在浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="c5461-194">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="c5461-195">从类别导航菜单中选择"船"。</span><span class="sxs-lookup"><span data-stu-id="c5461-195">Select "Boats" from the category navigation menu.</span></span>  
 <span data-ttu-id="c5461-196">*ProductList.aspx*显示页。</span><span class="sxs-lookup"><span data-stu-id="c5461-196">The *ProductList.aspx* page is displayed.</span></span>
3. <span data-ttu-id="c5461-197">从产品列表中选择"纸张船"产品。</span><span class="sxs-lookup"><span data-stu-id="c5461-197">Select the "Paper Boat" product from the product list.</span></span>  
 <span data-ttu-id="c5461-198">*ProductDetails.aspx*显示页。</span><span class="sxs-lookup"><span data-stu-id="c5461-198">The *ProductDetails.aspx* page is displayed.</span></span>   

    ![显示数据的项和详细信息-产品](display_data_items_and_details/_static/image4.png)
4. <span data-ttu-id="c5461-200">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="c5461-200">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="c5461-201">总结</span><span class="sxs-lookup"><span data-stu-id="c5461-201">Summary</span></span>

<span data-ttu-id="c5461-202">在本教程中的一系列已添加标记和代码以显示产品列表并显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="c5461-202">In this tutorial of the series you have add markup and code to display a product list and to display product details.</span></span> <span data-ttu-id="c5461-203">在此过程介绍了有关强类型化的数据控件、 模型绑定和值提供程序。</span><span class="sxs-lookup"><span data-stu-id="c5461-203">During this process you have learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="c5461-204">在下一步的教程中，你将在 Wingtip Toys 示例应用程序中添加购物车。</span><span class="sxs-lookup"><span data-stu-id="c5461-204">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5461-205">其他资源</span><span class="sxs-lookup"><span data-stu-id="c5461-205">Additional Resources</span></span>

[<span data-ttu-id="c5461-206">检索和使用模型绑定和 web 窗体显示数据</span><span class="sxs-lookup"><span data-stu-id="c5461-206">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

> [!div class="step-by-step"]
> <span data-ttu-id="c5461-207">[上一页](ui_and_navigation.md)
> [下一页](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="c5461-207">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
