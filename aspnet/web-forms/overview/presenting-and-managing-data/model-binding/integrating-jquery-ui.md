---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 与模型绑定和 web 窗体集成 JQuery UI Datepicker |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: fc278575615e63af2fc7284e51814cf318165110
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807572"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="c3477-104">与模型绑定和 web 窗体集成 JQuery UI Datepicker</span><span class="sxs-lookup"><span data-stu-id="c3477-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>
====================
<span data-ttu-id="c3477-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c3477-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c3477-106">本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。</span><span class="sxs-lookup"><span data-stu-id="c3477-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="c3477-107">模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。</span><span class="sxs-lookup"><span data-stu-id="c3477-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="c3477-108">本系列开始介绍性材料，后续教程将移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="c3477-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="c3477-109">本教程演示如何添加 JQuery UI[小组件](http://jqueryui.com/datepicker/)Web 窗体和使用模型绑定将使用所选的值更新数据库。</span><span class="sxs-lookup"><span data-stu-id="c3477-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="c3477-110">本教程中创建的项目为基础[第一个](retrieving-data.md)并[第二个](updating-deleting-and-creating-data.md)在本系列的部分。</span><span class="sxs-lookup"><span data-stu-id="c3477-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="c3477-111">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。</span><span class="sxs-lookup"><span data-stu-id="c3477-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="c3477-112">可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="c3477-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="c3477-113">它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。</span><span class="sxs-lookup"><span data-stu-id="c3477-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="c3477-114">你将生成</span><span class="sxs-lookup"><span data-stu-id="c3477-114">What you'll build</span></span>

<span data-ttu-id="c3477-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="c3477-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="c3477-116">将属性添加到您的模型以记录该学生注册日期</span><span class="sxs-lookup"><span data-stu-id="c3477-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="c3477-117">使用户可选择使用 JQuery UI Datepicker 小组件的注册日期</span><span class="sxs-lookup"><span data-stu-id="c3477-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="c3477-118">个注册日期执行验证规则</span><span class="sxs-lookup"><span data-stu-id="c3477-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="c3477-119">JQuery UI Datepicker 小组件使用户能够轻松地从用户交互的字段时弹出一个日历选择一个日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="c3477-120">使用此小组件可能会更便于用户比手动键入的日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="c3477-121">将小组件集成到页面的数据操作中使用模型绑定要求只有少量的额外工作。</span><span class="sxs-lookup"><span data-stu-id="c3477-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="c3477-122">将新属性添加到模型</span><span class="sxs-lookup"><span data-stu-id="c3477-122">Add a new property to the model</span></span>

<span data-ttu-id="c3477-123">首先，您将添加**Datetime**让学生的属性的模型和迁移到数据库所做的更改。</span><span class="sxs-lookup"><span data-stu-id="c3477-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="c3477-124">打开**UniversityModels.cs**，并将突出显示的代码添加到学生模型。</span><span class="sxs-lookup"><span data-stu-id="c3477-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="c3477-125">**RangeAttribute**是包括在内，以强制实施验证规则的属性。</span><span class="sxs-lookup"><span data-stu-id="c3477-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="c3477-126">对于本教程中，我们将假定 Contoso University 成立于 2013 年 1 月 1 日，并因此早期注册日期不是有效。</span><span class="sxs-lookup"><span data-stu-id="c3477-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="c3477-127">在包管理窗口中，添加通过运行命令的迁移**添加迁移 AddEnrollmentDate**。</span><span class="sxs-lookup"><span data-stu-id="c3477-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="c3477-128">请注意，迁移代码向 Student 表中添加新的日期时间列。</span><span class="sxs-lookup"><span data-stu-id="c3477-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="c3477-129">若要匹配 RangeAttribute 中指定的值，将以下突出显示的代码中所示添加新列中，默认值。</span><span class="sxs-lookup"><span data-stu-id="c3477-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="c3477-130">将所做的更改保存到迁移文件。</span><span class="sxs-lookup"><span data-stu-id="c3477-130">Save your change to the migration file.</span></span>

<span data-ttu-id="c3477-131">不需要再次生成种子数据。</span><span class="sxs-lookup"><span data-stu-id="c3477-131">You do not need to seed the data again.</span></span> <span data-ttu-id="c3477-132">因此，打开**Configuration.cs** Migrations 文件夹中并删除或注释掉中的代码**种子**方法。</span><span class="sxs-lookup"><span data-stu-id="c3477-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="c3477-133">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="c3477-133">Save and close the file.</span></span>

<span data-ttu-id="c3477-134">现在，运行命令**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="c3477-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="c3477-135">请注意，现在存在于数据库中列的所有现有记录具有默认值为 EnrollmentDate。</span><span class="sxs-lookup"><span data-stu-id="c3477-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="c3477-136">将动态控件添加个注册日期</span><span class="sxs-lookup"><span data-stu-id="c3477-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="c3477-137">现在，您将添加用于显示和编辑注册日期的控件。</span><span class="sxs-lookup"><span data-stu-id="c3477-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="c3477-138">现在，通过文本框中编辑值。</span><span class="sxs-lookup"><span data-stu-id="c3477-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="c3477-139">在本教程后面将更改文本框中，为 JQuery Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="c3477-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="c3477-140">首先，务必请注意，不需要进行任何更改**AddStudent.aspx**文件。</span><span class="sxs-lookup"><span data-stu-id="c3477-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="c3477-141">DynamicEntity 控件将自动呈现新属性。</span><span class="sxs-lookup"><span data-stu-id="c3477-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="c3477-142">打开**Students.aspx**，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="c3477-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="c3477-143">运行应用程序，请注意，您可以通过键入日期设置注册日期的值。</span><span class="sxs-lookup"><span data-stu-id="c3477-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="c3477-144">添加新学生时：</span><span class="sxs-lookup"><span data-stu-id="c3477-144">When adding a new student:</span></span>

![设置的日期](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="c3477-146">或者，编辑现有值：</span><span class="sxs-lookup"><span data-stu-id="c3477-146">Or, editing an existing value:</span></span>

![编辑日期](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="c3477-148">键入日期的工作原理，但它可能不是您希望提供的客户体验。</span><span class="sxs-lookup"><span data-stu-id="c3477-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="c3477-149">在下一部分中，您将启用选择通过日历日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="c3477-150">安装 NuGet 包以使用 JQuery UI</span><span class="sxs-lookup"><span data-stu-id="c3477-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="c3477-151">**汁 UI** NuGet 程序包可启用的 JQuery UI 小组件的轻松集成到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3477-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="c3477-152">若要使用此包，请通过 NuGet 安装它。</span><span class="sxs-lookup"><span data-stu-id="c3477-152">To use this package, install it through NuGet.</span></span>

![添加汁 UI](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="c3477-154">汁 UI 安装的版本可能与应用程序中的 JQuery 版本冲突。</span><span class="sxs-lookup"><span data-stu-id="c3477-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="c3477-155">本教程前，请尝试运行您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3477-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="c3477-156">如果遇到 JavaScript 错误，您需要协调的 JQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="c3477-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="c3477-157">可以将 JQuery 的预期的版本添加到脚本文件夹 （版本 1.8.2 在编写本教程中的时），或在 Site.master 指定 JQuery 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="c3477-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="c3477-158">自定义日期时间模板以包括小组件</span><span class="sxs-lookup"><span data-stu-id="c3477-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="c3477-159">会将小组件添加到动态数据模板以进行编辑的日期时间值。</span><span class="sxs-lookup"><span data-stu-id="c3477-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="c3477-160">通过将小组件添加到模板，自动呈现中添加新学生的这两个窗体和编辑学生在网格视图中。</span><span class="sxs-lookup"><span data-stu-id="c3477-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="c3477-161">打开**DateTime\_Edit.ascx**，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="c3477-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="c3477-162">在代码隐藏文件中，您将为 DatePicker 设置的最小和最大日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="c3477-163">通过设置这些值，将阻止用户导航到无效的日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="c3477-164">将检索中的最小和最大值**RangeAttribute**上的日期时间属性，如果提供。</span><span class="sxs-lookup"><span data-stu-id="c3477-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="c3477-165">打开**DateTime\_Edit.ascx.cs**，并将以下突出显示的代码添加到页面\_负载方法。</span><span class="sxs-lookup"><span data-stu-id="c3477-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="c3477-166">运行 web 应用程序并导航到 AddStudent 页面。</span><span class="sxs-lookup"><span data-stu-id="c3477-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="c3477-167">为字段提供值，请注意，如果您单击文本框中的注册日期，将显示日历。</span><span class="sxs-lookup"><span data-stu-id="c3477-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![日期选取器](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="c3477-169">选择日期，并单击**插入**。</span><span class="sxs-lookup"><span data-stu-id="c3477-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="c3477-170">RangeAttribute 强制进行验证的服务器上。</span><span class="sxs-lookup"><span data-stu-id="c3477-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="c3477-171">通过设置 Datepicker minDate 属性，您在客户端上还应用验证。</span><span class="sxs-lookup"><span data-stu-id="c3477-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="c3477-172">日历不允许用户导航到之前的 minDate 值的日期。</span><span class="sxs-lookup"><span data-stu-id="c3477-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="c3477-173">当您编辑网格视图中的记录时，还会显示日历。</span><span class="sxs-lookup"><span data-stu-id="c3477-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![在 GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="c3477-175">结束语</span><span class="sxs-lookup"><span data-stu-id="c3477-175">Conclusion</span></span>

<span data-ttu-id="c3477-176">在本教程中，您学习了如何使用模型绑定的 web 窗体中纳入 JQuery 小组件。</span><span class="sxs-lookup"><span data-stu-id="c3477-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="c3477-177">在接下来[教程](using-query-string-values-to-retrieve-data.md)，选择数据时，将使用查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="c3477-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3477-178">[上一页](sorting-paging-and-filtering-data.md)
> [下一页](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="c3477-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
