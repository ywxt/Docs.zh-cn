---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 排序、 分页和筛选数据与模型绑定和 web 窗体 |Microsoft Docs
author: Rick-Anderson
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: 624f98cea6030e0b7b022f86c4c1aa37f1db9726
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020945"
---
<a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="3a135-104">排序、 分页和筛选数据与模型绑定和 web 窗体</span><span class="sxs-lookup"><span data-stu-id="3a135-104">Sorting, paging, and filtering data with model binding and web forms</span></span>
====================
<span data-ttu-id="3a135-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3a135-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3a135-106">本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。</span><span class="sxs-lookup"><span data-stu-id="3a135-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="3a135-107">模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。</span><span class="sxs-lookup"><span data-stu-id="3a135-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="3a135-108">本系列开始介绍性材料，后续教程将移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="3a135-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="3a135-109">本教程演示如何添加排序、 分页和筛选数据，通过模型绑定。</span><span class="sxs-lookup"><span data-stu-id="3a135-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="3a135-110">本教程基于第一个中创建的项目[一部分](retrieving-data.md)在本系列。</span><span class="sxs-lookup"><span data-stu-id="3a135-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="3a135-111">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。</span><span class="sxs-lookup"><span data-stu-id="3a135-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="3a135-112">可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="3a135-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="3a135-113">它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。</span><span class="sxs-lookup"><span data-stu-id="3a135-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="3a135-114">你将生成</span><span class="sxs-lookup"><span data-stu-id="3a135-114">What you'll build</span></span>

<span data-ttu-id="3a135-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="3a135-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="3a135-116">启用排序和分页的数据</span><span class="sxs-lookup"><span data-stu-id="3a135-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="3a135-117">启用基于用户选择的数据的筛选</span><span class="sxs-lookup"><span data-stu-id="3a135-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="3a135-118">添加排序</span><span class="sxs-lookup"><span data-stu-id="3a135-118">Add sorting</span></span>

<span data-ttu-id="3a135-119">启用在 GridView 中排序是非常简单。</span><span class="sxs-lookup"><span data-stu-id="3a135-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="3a135-120">在 Student.aspx 文件中，只需将设置**AllowSorting**到**true** GridView 中。</span><span class="sxs-lookup"><span data-stu-id="3a135-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="3a135-121">不需要设置**SortExpression**自动使用数据字段值的每个列。</span><span class="sxs-lookup"><span data-stu-id="3a135-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="3a135-122">GridView 修改查询以包含所选值对数据进行排序。</span><span class="sxs-lookup"><span data-stu-id="3a135-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="3a135-123">以下突出显示的代码显示如何添加你需要进行启用排序。</span><span class="sxs-lookup"><span data-stu-id="3a135-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="3a135-124">运行 web 应用程序，并测试排序学生记录不同列中的值。</span><span class="sxs-lookup"><span data-stu-id="3a135-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![排序学生](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="3a135-126">添加分页</span><span class="sxs-lookup"><span data-stu-id="3a135-126">Add paging</span></span>

<span data-ttu-id="3a135-127">启用分页也是非常简单。</span><span class="sxs-lookup"><span data-stu-id="3a135-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="3a135-128">在 GridView 中，将**AllowPaging**属性设置为**true**并设置**PageSize**属性设置为你想要在每个页上显示的记录数。</span><span class="sxs-lookup"><span data-stu-id="3a135-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="3a135-129">在本教程中，可以将其设置为 4。</span><span class="sxs-lookup"><span data-stu-id="3a135-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="3a135-130">运行 web 应用程序，并请注意，现在与在单页上显示不超过 4 个记录，通过多个页面分割记录。</span><span class="sxs-lookup"><span data-stu-id="3a135-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![添加分页](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="3a135-132">延迟的执行查询可以提高应用程序效率。</span><span class="sxs-lookup"><span data-stu-id="3a135-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="3a135-133">而不是检索整个数据集，GridView 修改查询以检索仅为当前页的记录。</span><span class="sxs-lookup"><span data-stu-id="3a135-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="3a135-134">按用户所选内容筛选记录</span><span class="sxs-lookup"><span data-stu-id="3a135-134">Filter records by user selection</span></span>

<span data-ttu-id="3a135-135">模型绑定将添加几个属性使您能够指定如何在模型绑定方法中设置某个参数的值。</span><span class="sxs-lookup"><span data-stu-id="3a135-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="3a135-136">这些属性位于**System.Web.ModelBinding**命名空间。</span><span class="sxs-lookup"><span data-stu-id="3a135-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="3a135-137">它们包括：</span><span class="sxs-lookup"><span data-stu-id="3a135-137">They include:</span></span>

- <span data-ttu-id="3a135-138">控件</span><span class="sxs-lookup"><span data-stu-id="3a135-138">Control</span></span>
- <span data-ttu-id="3a135-139">Cookie</span><span class="sxs-lookup"><span data-stu-id="3a135-139">Cookie</span></span>
- <span data-ttu-id="3a135-140">窗体</span><span class="sxs-lookup"><span data-stu-id="3a135-140">Form</span></span>
- <span data-ttu-id="3a135-141">配置文件</span><span class="sxs-lookup"><span data-stu-id="3a135-141">Profile</span></span>
- <span data-ttu-id="3a135-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="3a135-142">QueryString</span></span>
- <span data-ttu-id="3a135-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="3a135-143">RouteData</span></span>
- <span data-ttu-id="3a135-144">会话</span><span class="sxs-lookup"><span data-stu-id="3a135-144">Session</span></span>
- <span data-ttu-id="3a135-145">用户配置文件</span><span class="sxs-lookup"><span data-stu-id="3a135-145">UserProfile</span></span>
- <span data-ttu-id="3a135-146">视图状态</span><span class="sxs-lookup"><span data-stu-id="3a135-146">ViewState</span></span>

<span data-ttu-id="3a135-147">在本教程中，您将使用控件的值来筛选 GridView 中显示的记录。</span><span class="sxs-lookup"><span data-stu-id="3a135-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="3a135-148">您将添加**控制**属性为先前创建的查询方法。</span><span class="sxs-lookup"><span data-stu-id="3a135-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="3a135-149">在中[更高版本](using-query-string-values-to-retrieve-data.md)教程中，您将应用**QueryString**属性用于指定参数值来自查询字符串值的参数。</span><span class="sxs-lookup"><span data-stu-id="3a135-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="3a135-150">首先，上面 ValidationSummary，添加一个下拉列表筛选显示的学生。</span><span class="sxs-lookup"><span data-stu-id="3a135-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="3a135-151">在代码隐藏文件中，修改选择的方法，以接收来自控件的值和参数的名称设置为提供的值的控件的名称。</span><span class="sxs-lookup"><span data-stu-id="3a135-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="3a135-152">必须添加**使用**语句**System.Web.ModelBinding**要解析的控件属性命名空间。</span><span class="sxs-lookup"><span data-stu-id="3a135-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="3a135-153">下面的代码演示重新致力于筛选返回的数据基于值的下拉列表选择方法。</span><span class="sxs-lookup"><span data-stu-id="3a135-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="3a135-154">参数指定此参数的值来自具有相同名称的控件之前，将添加的控件属性。</span><span class="sxs-lookup"><span data-stu-id="3a135-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="3a135-155">运行 web 应用程序，并从下拉列表以筛选学生列表中选择不同的值。</span><span class="sxs-lookup"><span data-stu-id="3a135-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![筛选器学生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="3a135-157">结束语</span><span class="sxs-lookup"><span data-stu-id="3a135-157">Conclusion</span></span>

<span data-ttu-id="3a135-158">在本教程中，您将启用排序和分页的数据。</span><span class="sxs-lookup"><span data-stu-id="3a135-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="3a135-159">你还启用了通过将控件的值筛选数据。</span><span class="sxs-lookup"><span data-stu-id="3a135-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="3a135-160">在接下来[教程](integrating-jquery-ui.md)将将 JQuery UI 小组件集成到动态数据模板来增强 UI。</span><span class="sxs-lookup"><span data-stu-id="3a135-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3a135-161">[上一页](updating-deleting-and-creating-data.md)
> [下一页](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="3a135-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
