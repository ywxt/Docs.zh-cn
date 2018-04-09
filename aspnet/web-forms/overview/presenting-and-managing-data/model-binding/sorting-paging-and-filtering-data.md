---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 排序、 分页和筛选使用模型的绑定和 web 窗体的数据 |Microsoft 文档
author: tfitzmac
description: 本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互详细直接-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: d63ebecadd392877e4cb1d1dffe9db2d1d231190
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="41eb5-104">排序、 分页和筛选使用模型的绑定和 web 窗体的数据</span><span class="sxs-lookup"><span data-stu-id="41eb5-104">Sorting, paging, and filtering data with model binding and web forms</span></span>
====================
<span data-ttu-id="41eb5-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="41eb5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="41eb5-106">本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="41eb5-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="41eb5-107">模型绑定使数据交互更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource）。</span><span class="sxs-lookup"><span data-stu-id="41eb5-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="41eb5-108">这一系列开头介绍性材料，更高版本的教程中移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="41eb5-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="41eb5-109">本教程演示如何添加排序、 分页和筛选数据，通过模型绑定。</span><span class="sxs-lookup"><span data-stu-id="41eb5-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="41eb5-110">本教程基于第一个中创建的项目[一部分](retrieving-data.md)的序列。</span><span class="sxs-lookup"><span data-stu-id="41eb5-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="41eb5-111">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)在 C# 或 VB.完整项目</span><span class="sxs-lookup"><span data-stu-id="41eb5-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="41eb5-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="41eb5-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="41eb5-113">它使用 Visual Studio 2012 模板，这是本教程中所示的 Visual Studio 2013 模板过程稍有不同。</span><span class="sxs-lookup"><span data-stu-id="41eb5-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="41eb5-114">你将生成</span><span class="sxs-lookup"><span data-stu-id="41eb5-114">What you'll build</span></span>

<span data-ttu-id="41eb5-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="41eb5-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="41eb5-116">启用排序和分页的数据</span><span class="sxs-lookup"><span data-stu-id="41eb5-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="41eb5-117">启用筛选数据，根据用户的选择</span><span class="sxs-lookup"><span data-stu-id="41eb5-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="41eb5-118">添加排序</span><span class="sxs-lookup"><span data-stu-id="41eb5-118">Add sorting</span></span>

<span data-ttu-id="41eb5-119">启用在 GridView 中排序是非常简单。</span><span class="sxs-lookup"><span data-stu-id="41eb5-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="41eb5-120">在 Student.aspx 文件中，只需设置**AllowSorting**到**true**中 GridView。</span><span class="sxs-lookup"><span data-stu-id="41eb5-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="41eb5-121">不需要设置**SortExpression** DataField 会自动使用值为每个列。</span><span class="sxs-lookup"><span data-stu-id="41eb5-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="41eb5-122">GridView 修改查询以包含所选值通过对数据进行排序。</span><span class="sxs-lookup"><span data-stu-id="41eb5-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="41eb5-123">突出显示的以下代码显示如何添加需要进行启用排序。</span><span class="sxs-lookup"><span data-stu-id="41eb5-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="41eb5-124">运行 web 应用程序，并测试排序学生记录不同的列中的值。</span><span class="sxs-lookup"><span data-stu-id="41eb5-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![排序学生版](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="41eb5-126">将分页添加</span><span class="sxs-lookup"><span data-stu-id="41eb5-126">Add paging</span></span>

<span data-ttu-id="41eb5-127">启用分页也是非常简单的。</span><span class="sxs-lookup"><span data-stu-id="41eb5-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="41eb5-128">在 GridView，集中**AllowPaging**属性**true**并设置**PageSize**属性设置为你想要在每个页面上显示的记录数。</span><span class="sxs-lookup"><span data-stu-id="41eb5-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="41eb5-129">在本教程中，可以将其设置为 4。</span><span class="sxs-lookup"><span data-stu-id="41eb5-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="41eb5-130">运行 web 应用程序，并请注意，现在不能超过 4 记录在单个页面上显示多个页通过划分记录。</span><span class="sxs-lookup"><span data-stu-id="41eb5-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![将分页添加](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="41eb5-132">延迟的执行查询提高了应用程序效率。</span><span class="sxs-lookup"><span data-stu-id="41eb5-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="41eb5-133">而不是检索整个数据集，GridView 修改查询以检索仅针对当前页的记录。</span><span class="sxs-lookup"><span data-stu-id="41eb5-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="41eb5-134">按用户选择筛选记录</span><span class="sxs-lookup"><span data-stu-id="41eb5-134">Filter records by user selection</span></span>

<span data-ttu-id="41eb5-135">模型绑定将添加多个特性使你可以指定如何在模型绑定方法中设置参数的值。</span><span class="sxs-lookup"><span data-stu-id="41eb5-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="41eb5-136">这些特性是在**System.Web.ModelBinding**命名空间。</span><span class="sxs-lookup"><span data-stu-id="41eb5-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="41eb5-137">它们包括：</span><span class="sxs-lookup"><span data-stu-id="41eb5-137">They include:</span></span>

- <span data-ttu-id="41eb5-138">控件</span><span class="sxs-lookup"><span data-stu-id="41eb5-138">Control</span></span>
- <span data-ttu-id="41eb5-139">Cookie</span><span class="sxs-lookup"><span data-stu-id="41eb5-139">Cookie</span></span>
- <span data-ttu-id="41eb5-140">窗体</span><span class="sxs-lookup"><span data-stu-id="41eb5-140">Form</span></span>
- <span data-ttu-id="41eb5-141">配置文件</span><span class="sxs-lookup"><span data-stu-id="41eb5-141">Profile</span></span>
- <span data-ttu-id="41eb5-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="41eb5-142">QueryString</span></span>
- <span data-ttu-id="41eb5-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="41eb5-143">RouteData</span></span>
- <span data-ttu-id="41eb5-144">会话</span><span class="sxs-lookup"><span data-stu-id="41eb5-144">Session</span></span>
- <span data-ttu-id="41eb5-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="41eb5-145">UserProfile</span></span>
- <span data-ttu-id="41eb5-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="41eb5-146">ViewState</span></span>

<span data-ttu-id="41eb5-147">在本教程中，你将使用控件的值来筛选的记录会显示在 GridView。</span><span class="sxs-lookup"><span data-stu-id="41eb5-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="41eb5-148">你将添加**控件**属性设为你创建了前面的查询方法。</span><span class="sxs-lookup"><span data-stu-id="41eb5-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="41eb5-149">在[更高版本](using-query-string-values-to-retrieve-data.md)教程中，你将应用**QueryString**属性设为参数来指定参数值来自查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="41eb5-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="41eb5-150">首先，ValidationSummary，上面添加的下拉列表进行筛选的列表显示哪些学生。</span><span class="sxs-lookup"><span data-stu-id="41eb5-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="41eb5-151">在代码隐藏文件中，修改选择的方法，以接收值，通过控件，并将参数的名称为提供的值的控件的名称。</span><span class="sxs-lookup"><span data-stu-id="41eb5-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="41eb5-152">你必须添加**使用**语句**System.Web.ModelBinding**命名空间，若要解决控件属性。</span><span class="sxs-lookup"><span data-stu-id="41eb5-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="41eb5-153">下面的代码演示 select 方法重新处理来筛选返回的数据的下拉列表中的值。</span><span class="sxs-lookup"><span data-stu-id="41eb5-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="41eb5-154">一个参数指定此参数的值来自具有相同名称的控件之前，将添加控件属性。</span><span class="sxs-lookup"><span data-stu-id="41eb5-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="41eb5-155">运行 web 应用程序并从下拉列表来筛选学生列表中选择不同的值。</span><span class="sxs-lookup"><span data-stu-id="41eb5-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![筛选器学生版](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="41eb5-157">结束语</span><span class="sxs-lookup"><span data-stu-id="41eb5-157">Conclusion</span></span>

<span data-ttu-id="41eb5-158">在本教程中，你可以启用排序和分页的数据。</span><span class="sxs-lookup"><span data-stu-id="41eb5-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="41eb5-159">你也可以启用控件的值筛选数据。</span><span class="sxs-lookup"><span data-stu-id="41eb5-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="41eb5-160">在下一个[教程](integrating-jquery-ui.md)您将通过将 JQuery UI 小组件集成到动态数据模板来增强 UI。</span><span class="sxs-lookup"><span data-stu-id="41eb5-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="41eb5-161">[上一页](updating-deleting-and-creating-data.md)
> [下一页](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="41eb5-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
