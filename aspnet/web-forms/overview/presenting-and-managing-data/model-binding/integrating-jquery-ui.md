---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 使用模型的绑定和 web 窗体中集成 JQuery UI Datepicker |Microsoft 文档
author: tfitzmac
description: 本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互详细直接-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 126262b440f3e914a7fac3f0b7eeadb4f648d2bb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887907"
---
<a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="f3037-104">使用模型的绑定和 web 窗体中集成 JQuery UI Datepicker</span><span class="sxs-lookup"><span data-stu-id="f3037-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>
====================
<span data-ttu-id="f3037-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f3037-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f3037-106">本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="f3037-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="f3037-107">模型绑定使数据交互更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource）。</span><span class="sxs-lookup"><span data-stu-id="f3037-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="f3037-108">这一系列开头介绍性材料，更高版本的教程中移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="f3037-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="f3037-109">本教程演示如何将添加 JQuery UI [Datepicker 小组件](http://jqueryui.com/datepicker/)到 Web 窗体，并使用模型绑定，使其使用所选值更新数据库。</span><span class="sxs-lookup"><span data-stu-id="f3037-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="f3037-110">本教程中创建的项目上[第一个](retrieving-data.md)和[第二个](updating-deleting-and-creating-data.md)的序列部分。</span><span class="sxs-lookup"><span data-stu-id="f3037-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="f3037-111">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)在 C# 或 VB.完整项目</span><span class="sxs-lookup"><span data-stu-id="f3037-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="f3037-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="f3037-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="f3037-113">它使用 Visual Studio 2012 模板，这是本教程中所示的 Visual Studio 2013 模板过程稍有不同。</span><span class="sxs-lookup"><span data-stu-id="f3037-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="f3037-114">你将生成</span><span class="sxs-lookup"><span data-stu-id="f3037-114">What you'll build</span></span>

<span data-ttu-id="f3037-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="f3037-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="f3037-116">将属性添加到你的模型来记录学生的注册日期</span><span class="sxs-lookup"><span data-stu-id="f3037-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="f3037-117">使用户可选择使用 JQuery UI Datepicker 小组件的注册日期</span><span class="sxs-lookup"><span data-stu-id="f3037-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="f3037-118">注册日期实施验证规则</span><span class="sxs-lookup"><span data-stu-id="f3037-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="f3037-119">JQuery UI Datepicker 小组件使用户能够轻松地从在用户交互的字段时弹出日历中选择一个日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="f3037-120">使用此小组件可能会更便于用户比手动键入日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="f3037-121">将包含 Datepicker 小组件集成到的数据操作中使用模型绑定的页面要求只有少量的额外的工作。</span><span class="sxs-lookup"><span data-stu-id="f3037-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="f3037-122">将新属性添加到模型</span><span class="sxs-lookup"><span data-stu-id="f3037-122">Add a new property to the model</span></span>

<span data-ttu-id="f3037-123">首先，你将添加**Datetime**属性设置为你学生模型和迁移到数据库所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f3037-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="f3037-124">打开**UniversityModels.cs**，并将突出显示的代码添加到学生模型。</span><span class="sxs-lookup"><span data-stu-id="f3037-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="f3037-125">**RangeAttribute**目的是为了实施的属性的验证规则。</span><span class="sxs-lookup"><span data-stu-id="f3037-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="f3037-126">对于本教程中，我们将假定 Contoso 大学成立于 2013 年 1 月 1 日，并因此早期注册日期不是有效。</span><span class="sxs-lookup"><span data-stu-id="f3037-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="f3037-127">在包管理窗口中，通过运行命令添加迁移**添加迁移 AddEnrollmentDate**。</span><span class="sxs-lookup"><span data-stu-id="f3037-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="f3037-128">请注意，迁移代码会将新的日期时间列添加到学生表。</span><span class="sxs-lookup"><span data-stu-id="f3037-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="f3037-129">以匹配你在 RangeAttribute 中指定的值，添加以下突出显示的代码中所示的新列的默认值。</span><span class="sxs-lookup"><span data-stu-id="f3037-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="f3037-130">将所做的更改保存到的迁移文件。</span><span class="sxs-lookup"><span data-stu-id="f3037-130">Save your change to the migration file.</span></span>

<span data-ttu-id="f3037-131">不需要再次种子数据。</span><span class="sxs-lookup"><span data-stu-id="f3037-131">You do not need to seed the data again.</span></span> <span data-ttu-id="f3037-132">因此，打开**Configuration.cs** Migrations 文件夹中，删除或注释掉中的代码**种子**方法。</span><span class="sxs-lookup"><span data-stu-id="f3037-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="f3037-133">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="f3037-133">Save and close the file.</span></span>

<span data-ttu-id="f3037-134">现在，运行命令**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="f3037-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="f3037-135">请注意，此列现在存在于数据库并且所有现有记录 EnrollmentDate 对于具有默认值。</span><span class="sxs-lookup"><span data-stu-id="f3037-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="f3037-136">注册日期添加动态控件</span><span class="sxs-lookup"><span data-stu-id="f3037-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="f3037-137">现在，你将添加用于显示和编辑注册日期的控件。</span><span class="sxs-lookup"><span data-stu-id="f3037-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="f3037-138">此时，通过在文本框中编辑该值。</span><span class="sxs-lookup"><span data-stu-id="f3037-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="f3037-139">更高版本在教程中，将更改文本框中，为 JQuery Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="f3037-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="f3037-140">首先，务必请注意，不需要进行任何更改到**AddStudent.aspx**文件。</span><span class="sxs-lookup"><span data-stu-id="f3037-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="f3037-141">DynamicEntity 控件会自动呈现新属性。</span><span class="sxs-lookup"><span data-stu-id="f3037-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="f3037-142">打开**Students.aspx**，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="f3037-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="f3037-143">运行应用程序，并请注意，你可以通过键入日期设置注册日期的值。</span><span class="sxs-lookup"><span data-stu-id="f3037-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="f3037-144">当添加新的学生：</span><span class="sxs-lookup"><span data-stu-id="f3037-144">When adding a new student:</span></span>

![设置的日期](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="f3037-146">或者，编辑现有值：</span><span class="sxs-lookup"><span data-stu-id="f3037-146">Or, editing an existing value:</span></span>

![编辑日期](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="f3037-148">键入日期工作原理，但它可能不是你想要提供的客户体验。</span><span class="sxs-lookup"><span data-stu-id="f3037-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="f3037-149">在下一步的部分中，将启用选择通过日历日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="f3037-150">安装 NuGet 包才能使用 JQuery UI</span><span class="sxs-lookup"><span data-stu-id="f3037-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="f3037-151">**汁 UI** NuGet 包更方便地将 JQuery UI 小组件集成到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3037-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="f3037-152">若要使用此包，请通过 NuGet 安装它。</span><span class="sxs-lookup"><span data-stu-id="f3037-152">To use this package, install it through NuGet.</span></span>

![添加汁 UI](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="f3037-154">你安装的汁 UI 的版本可能与你的应用程序中的 JQuery 版本冲突。</span><span class="sxs-lookup"><span data-stu-id="f3037-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="f3037-155">然后再继续进行本教程，请尝试运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f3037-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="f3037-156">如果你遇到 JavaScript 错误，则需要进行对帐 JQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="f3037-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="f3037-157">你可以将 JQuery 的预期的版本添加到脚本文件夹 （版本 1.8.2 在编写本教程的时），或在 Site.master 指定 JQuery 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="f3037-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="f3037-158">自定义 DateTime 模板以包括包含 Datepicker 小组件</span><span class="sxs-lookup"><span data-stu-id="f3037-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="f3037-159">将将包含 Datepicker 小组件添加到动态数据模板进行编辑的日期时间值。</span><span class="sxs-lookup"><span data-stu-id="f3037-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="f3037-160">通过将小组件添加到模板，它会自动呈现在添加新的学生的这两个窗体并在网格视图中编辑学生版。</span><span class="sxs-lookup"><span data-stu-id="f3037-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="f3037-161">打开**DateTime\_Edit.ascx**，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="f3037-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="f3037-162">在代码隐藏文件中，你将会包含 DatePicker 设置的最小和最大日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="f3037-163">通过设置这些值，将阻止用户导航到无效的日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="f3037-164">将检索的最小和最大值**RangeAttribute** DateTime 属性，如果其中一个提供。</span><span class="sxs-lookup"><span data-stu-id="f3037-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="f3037-165">打开**DateTime\_Edit.ascx.cs**，并将以下突出显示的代码添加到页\_加载方法。</span><span class="sxs-lookup"><span data-stu-id="f3037-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="f3037-166">运行 web 应用程序并导航到 AddStudent 页。</span><span class="sxs-lookup"><span data-stu-id="f3037-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="f3037-167">为字段提供值，请注意当你在文本框中单击针对注册日期时，会显示日历。</span><span class="sxs-lookup"><span data-stu-id="f3037-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![日期选取器](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="f3037-169">选择日期，并单击**插入**。</span><span class="sxs-lookup"><span data-stu-id="f3037-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="f3037-170">RangeAttribute 强制进行服务器上的验证。</span><span class="sxs-lookup"><span data-stu-id="f3037-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="f3037-171">通过设置 Datepicker minDate 属性，您在客户端还应用验证。</span><span class="sxs-lookup"><span data-stu-id="f3037-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="f3037-172">日历不允许用户导航到之前的 minDate 值的日期。</span><span class="sxs-lookup"><span data-stu-id="f3037-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="f3037-173">当您编辑网格视图中的记录时，还会显示日历。</span><span class="sxs-lookup"><span data-stu-id="f3037-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![在 GridView 的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="f3037-175">结束语</span><span class="sxs-lookup"><span data-stu-id="f3037-175">Conclusion</span></span>

<span data-ttu-id="f3037-176">在本教程中，您学习了如何将 JQuery 小组件合并到使用模型绑定的 web 窗体。</span><span class="sxs-lookup"><span data-stu-id="f3037-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="f3037-177">在下一个[教程](using-query-string-values-to-retrieve-data.md)，选择数据时，将使用的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="f3037-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3037-178">[上一页](sorting-paging-and-filtering-data.md)
> [下一页](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="f3037-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
