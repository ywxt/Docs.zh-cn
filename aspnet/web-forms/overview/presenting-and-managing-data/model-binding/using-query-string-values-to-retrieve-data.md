---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查询字符串值来筛选具有模型绑定的数据和 web 窗体 |Microsoft 文档
author: tfitzmac
description: 本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互详细直接-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 03d20decf0eeff6062fbc6f8dd66f644b405c7cc
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886818"
---
<a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="3ebf7-104">模型绑定和 web 窗体中使用查询字符串值将筛选器数据</span><span class="sxs-lookup"><span data-stu-id="3ebf7-104">Using query string values to filter data with model binding and web forms</span></span>
====================
<span data-ttu-id="3ebf7-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ebf7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3ebf7-106">本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="3ebf7-107">模型绑定使数据交互更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource）。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="3ebf7-108">这一系列开头介绍性材料，更高版本的教程中移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="3ebf7-109">本教程演示如何传递查询字符串中的一个值，并使用该值通过模型绑定中检索数据。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="3ebf7-110">本教程中创建的项目上[早期](retrieving-data.md)的序列部分。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="3ebf7-111">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)在 C# 或 VB.完整项目</span><span class="sxs-lookup"><span data-stu-id="3ebf7-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="3ebf7-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="3ebf7-113">它使用 Visual Studio 2012 模板，这是本教程中所示的 Visual Studio 2013 模板过程稍有不同。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="3ebf7-114">你将生成</span><span class="sxs-lookup"><span data-stu-id="3ebf7-114">What you'll build</span></span>

<span data-ttu-id="3ebf7-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="3ebf7-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="3ebf7-116">添加新的页以显示学生的已注册的课程</span><span class="sxs-lookup"><span data-stu-id="3ebf7-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="3ebf7-117">检索所选基于查询字符串中的值的学生的已注册的课程</span><span class="sxs-lookup"><span data-stu-id="3ebf7-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="3ebf7-118">将带有查询字符串值的超链接从网格视图添加到新的页</span><span class="sxs-lookup"><span data-stu-id="3ebf7-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="3ebf7-119">本教程中的步骤是非常类似于您进行的操作在早期版本[教程](sorting-paging-and-filtering-data.md)来筛选显示的学生基于用户选择下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="3ebf7-120">在该教程中，你使用了**控件**中选择的方法，以指定的参数值来自控件的属性。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="3ebf7-121">在本教程中，你将使用**QueryString**中选择的方法，以指定的参数值来自查询字符串属性。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="3ebf7-122">添加用于显示学生的课程的新页</span><span class="sxs-lookup"><span data-stu-id="3ebf7-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="3ebf7-123">添加新的 web 窗体使用 Site.master 主页上，然后将该页命名**课程**。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="3ebf7-124">在**Courses.aspx**文件中，添加一个网格视图以显示所选学生课程。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="3ebf7-125">定义 select 方法</span><span class="sxs-lookup"><span data-stu-id="3ebf7-125">Define the select method</span></span>

<span data-ttu-id="3ebf7-126">在**Courses.aspx.cs**，你将添加具有在网格视图中指定的名称的选择方法**SelectMethod**属性。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="3ebf7-127">在该方法中，你将定义用于检索学生的课程，查询，并指定参数来自具有相同名称作为参数的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="3ebf7-128">首先，必须添加以下**使用**语句。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="3ebf7-129">然后，将以下代码添加到 Courses.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="3ebf7-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="3ebf7-130">查询字符串属性意味着一个名为 StudentID 的查询字符串值将自动分配给此方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="3ebf7-131">添加查询字符串值以超链接</span><span class="sxs-lookup"><span data-stu-id="3ebf7-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="3ebf7-132">在上 Students.aspx 网格视图中，你将添加链接到你的新课程页面的超链接字段。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="3ebf7-133">超链接将包括具有学生 id 的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="3ebf7-134">在 Students.aspx，将以下字段添加到字段的正下方的网格视图列的总的信用额度。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="3ebf7-135">运行应用程序，并请注意，网格视图现在包含课程链接。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![添加超链接](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="3ebf7-137">当你单击一个链接时，你将看到该学生的已注册的课程。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![显示课程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="3ebf7-139">结束语</span><span class="sxs-lookup"><span data-stu-id="3ebf7-139">Conclusion</span></span>

<span data-ttu-id="3ebf7-140">在本教程中，你添加的链接的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="3ebf7-141">该查询字符串值用于在 select 方法的参数值。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="3ebf7-142">在下一个[教程](adding-business-logic-layer.md)，会将代码隐藏文件的代码移入业务逻辑层和数据访问层。</span><span class="sxs-lookup"><span data-stu-id="3ebf7-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ebf7-143">[上一页](integrating-jquery-ui.md)
> [下一页](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="3ebf7-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
