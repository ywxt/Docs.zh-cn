---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用实体框架 4.0 和 ObjectDataSource 控件，第 3 部分： 排序和筛选 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 48d859191877ba951e233f19873d52625fe180ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378905"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="af51d-104">使用实体框架 4.0 和 ObjectDataSource 控件，第 3 部分： 排序和筛选</span><span class="sxs-lookup"><span data-stu-id="af51d-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>
====================
<span data-ttu-id="af51d-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="af51d-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="af51d-106">本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。</span><span class="sxs-lookup"><span data-stu-id="af51d-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="af51d-107">如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。</span><span class="sxs-lookup"><span data-stu-id="af51d-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="af51d-108">此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。</span><span class="sxs-lookup"><span data-stu-id="af51d-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="af51d-109">如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="af51d-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="af51d-110">上一教程中实现中使用实体框架的 n 层 web 应用程序的存储库模式和`ObjectDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="af51d-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="af51d-111">本教程演示如何执行排序和筛选和处理主-从方案。</span><span class="sxs-lookup"><span data-stu-id="af51d-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="af51d-112">你将添加到以下增强功能*Departments.aspx*页：</span><span class="sxs-lookup"><span data-stu-id="af51d-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="af51d-113">若要允许用户按名称选择部门文本框。</span><span class="sxs-lookup"><span data-stu-id="af51d-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="af51d-114">在网格中显示每个部门的课程列表。</span><span class="sxs-lookup"><span data-stu-id="af51d-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="af51d-115">通过单击列标题排序功能。</span><span class="sxs-lookup"><span data-stu-id="af51d-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="af51d-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="af51d-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="af51d-117">将功能添加到 GridView 列进行排序</span><span class="sxs-lookup"><span data-stu-id="af51d-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="af51d-118">打开*Departments.aspx*页上，添加`SortParameterName="sortExpression"`归于`ObjectDataSource`控件命名为`DepartmentsObjectDataSource`。</span><span class="sxs-lookup"><span data-stu-id="af51d-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="af51d-119">(稍后将创建`GetDepartments`方法采用参数名为`sortExpression`。)现在，该控件的开始标记的标记类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="af51d-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="af51d-120">添加`AllowSorting="true"`属性的开始标记为`GridView`控件。</span><span class="sxs-lookup"><span data-stu-id="af51d-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="af51d-121">现在，该控件的开始标记的标记类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="af51d-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="af51d-122">在中*Departments.aspx.cs*，通过调用设置默认的排序顺序`GridView`控件的`Sort`方法从`Page_Load`方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="af51d-123">在业务逻辑类或存储库类中，可以添加对进行排序或筛选器的代码。</span><span class="sxs-lookup"><span data-stu-id="af51d-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="af51d-124">如果您执行此操作的业务逻辑类中，排序或筛选工作会执行从数据库检索数据之后由于业务逻辑类使用`IEnumerable`对象返回的存储库。</span><span class="sxs-lookup"><span data-stu-id="af51d-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="af51d-125">如果您添加排序和筛选存储库类中的代码和执行之前的 LINQ 表达式或对象查询转换为`IEnumerable`对象，你的命令将通过传递给数据库进行处理，通常效率更高。</span><span class="sxs-lookup"><span data-stu-id="af51d-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="af51d-126">将在本教程中实现排序和筛选将导致由数据库执行的处理的方式 — 也就是说，存储库中。</span><span class="sxs-lookup"><span data-stu-id="af51d-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="af51d-127">若要添加排序功能，必须将新方法添加到存储库接口和存储库类以及业务逻辑类中。</span><span class="sxs-lookup"><span data-stu-id="af51d-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="af51d-128">在中*ISchoolRepository.cs*文件中，添加一个新`GetDepartments`采用的方法`sortExpression`参数，它将用于排序返回部门列表：</span><span class="sxs-lookup"><span data-stu-id="af51d-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="af51d-129">`sortExpression`参数将指定要作为排序依据的列和排序方向。</span><span class="sxs-lookup"><span data-stu-id="af51d-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="af51d-130">添加到新的方法的代码*SchoolRepository.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="af51d-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="af51d-131">更改现有无参数`GetDepartments`方法调用新方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="af51d-132">在测试项目中，添加以下新方法*MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="af51d-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="af51d-133">如果要创建依赖于此方法返回的已排序的列表的任何单元测试，您需要对列表返回之前对其进行排序。</span><span class="sxs-lookup"><span data-stu-id="af51d-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="af51d-134">你不需要创建测试类似的在本教程中，因此该方法只返回部门的未排序的列表。</span><span class="sxs-lookup"><span data-stu-id="af51d-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="af51d-135">在中*SchoolBL.cs*文件中，将以下新方法添加到业务逻辑类：</span><span class="sxs-lookup"><span data-stu-id="af51d-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="af51d-136">此代码将排序参数传递给存储库方法。</span><span class="sxs-lookup"><span data-stu-id="af51d-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="af51d-137">运行*Departments.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="af51d-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="af51d-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="af51d-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="af51d-139">现在可以单击任何列标题以按该列排序。</span><span class="sxs-lookup"><span data-stu-id="af51d-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="af51d-140">如果已对列进行排序，单击标题反转的排序方向。</span><span class="sxs-lookup"><span data-stu-id="af51d-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="af51d-141">添加搜索框</span><span class="sxs-lookup"><span data-stu-id="af51d-141">Adding a Search Box</span></span>

<span data-ttu-id="af51d-142">将在本部分中添加搜索文本框中，将其链接至`ObjectDataSource`控制使用控件参数，并将方法添加到要支持筛选的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="af51d-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="af51d-143">打开*Departments.aspx*页上，添加以下标记标题和第一个之间`ObjectDataSource`控件：</span><span class="sxs-lookup"><span data-stu-id="af51d-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="af51d-144">在中`ObjectDataSource`名为控件`DepartmentsObjectDataSource`，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="af51d-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="af51d-145">添加`SelectParameters`名为的参数的元素`nameSearchString`获取中输入的值`SearchTextBox`控件。</span><span class="sxs-lookup"><span data-stu-id="af51d-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="af51d-146">更改`SelectMethod`属性值为`GetDepartmentsByName`。</span><span class="sxs-lookup"><span data-stu-id="af51d-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="af51d-147">（您将创建此方法更高版本。）</span><span class="sxs-lookup"><span data-stu-id="af51d-147">(You'll create this method later.)</span></span>

<span data-ttu-id="af51d-148">有关标记`ObjectDataSource`控件现在类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="af51d-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="af51d-149">在中*ISchoolRepository.cs*，添加`GetDepartmentsByName`方法采用两`sortExpression`和`nameSearchString`参数：</span><span class="sxs-lookup"><span data-stu-id="af51d-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="af51d-150">在中*SchoolRepository.cs*，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="af51d-151">此代码使用`Where`方法来选择包含搜索字符串的项。</span><span class="sxs-lookup"><span data-stu-id="af51d-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="af51d-152">如果搜索字符串为空，将选择所有记录。</span><span class="sxs-lookup"><span data-stu-id="af51d-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="af51d-153">请注意，当您指定在此类的一个语句中一起调用的方法 (`Include`，然后`OrderBy`，然后`Where`)，则`Where`方法必须始终为最后一个。</span><span class="sxs-lookup"><span data-stu-id="af51d-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="af51d-154">更改现有`GetDepartments`方法采用`sortExpression`参数来调用新方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="af51d-155">在中*MockSchoolRepository.cs*在测试项目中，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="af51d-156">在中*SchoolBL.cs*，添加以下新方法：</span><span class="sxs-lookup"><span data-stu-id="af51d-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="af51d-157">运行*Departments.aspx*页，并输入搜索字符串以确保选择逻辑可以正常工作。</span><span class="sxs-lookup"><span data-stu-id="af51d-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="af51d-158">将文本框留空，请尝试搜索以确保将返回所有记录。</span><span class="sxs-lookup"><span data-stu-id="af51d-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="af51d-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="af51d-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="af51d-160">为每个网格行中添加详细信息列</span><span class="sxs-lookup"><span data-stu-id="af51d-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="af51d-161">接下来，你想要查看所有右侧的网格单元中显示每个系的课程。</span><span class="sxs-lookup"><span data-stu-id="af51d-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="af51d-162">若要执行此操作，您将使用嵌套`GridView`控制和数据绑定将数据从它`Courses`导航属性`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="af51d-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="af51d-163">打开*Departments.aspx*和中的标记`GridView`控制，请指定处理程序为`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="af51d-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="af51d-164">现在，该控件的开始标记的标记类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="af51d-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="af51d-165">添加一个新`TemplateField`元素后的`Administrator`模板字段：</span><span class="sxs-lookup"><span data-stu-id="af51d-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="af51d-166">此标记创建嵌套`GridView`演示的课程编号和标题的课程列表的控件。</span><span class="sxs-lookup"><span data-stu-id="af51d-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="af51d-167">它不指定数据源，因为将数据绑定中的代码中`RowDataBound`处理程序。</span><span class="sxs-lookup"><span data-stu-id="af51d-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="af51d-168">打开*Departments.aspx.cs*并添加以下处理程序`RowDataBound`事件：</span><span class="sxs-lookup"><span data-stu-id="af51d-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="af51d-169">此代码获取`Department`从事件参数中，实体将转换`Courses`导航属性设置为`List`集合和嵌套的 databinds`GridView`到集合。</span><span class="sxs-lookup"><span data-stu-id="af51d-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="af51d-170">打开*SchoolRepository.cs*文件，并指定预先加载`Courses`导航属性，通过调用`Include`方法中创建的对象查询中`GetDepartmentsByName`方法。</span><span class="sxs-lookup"><span data-stu-id="af51d-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="af51d-171">`return`中的语句`GetDepartmentsByName`方法现在类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="af51d-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="af51d-172">运行页。</span><span class="sxs-lookup"><span data-stu-id="af51d-172">Run the page.</span></span> <span data-ttu-id="af51d-173">排序和筛选你前面添加的功能，除了 GridView 控件现在显示每个部门的嵌套的课程详细信息。</span><span class="sxs-lookup"><span data-stu-id="af51d-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="af51d-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="af51d-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="af51d-175">这将完成排序、 筛选，和母版-详细信息方案的简介。</span><span class="sxs-lookup"><span data-stu-id="af51d-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="af51d-176">在下一步的教程中，您将了解如何处理并发。</span><span class="sxs-lookup"><span data-stu-id="af51d-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="af51d-177">[上一页](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="af51d-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
