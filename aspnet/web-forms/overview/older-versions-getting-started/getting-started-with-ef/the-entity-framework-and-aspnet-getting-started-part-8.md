---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: f5ad2c1caf6036a0d8ee2ebbd07de60009090f1b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374047"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="b9087-104">Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分</span><span class="sxs-lookup"><span data-stu-id="b9087-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>
====================
<span data-ttu-id="b9087-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b9087-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="b9087-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9087-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="b9087-107">有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="b9087-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="b9087-108">使用动态数据功能进行格式化和验证数据</span><span class="sxs-lookup"><span data-stu-id="b9087-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="b9087-109">在上一教程中，您将实现存储的过程。</span><span class="sxs-lookup"><span data-stu-id="b9087-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="b9087-110">本教程将演示如何动态数据功能可提供以下优势：</span><span class="sxs-lookup"><span data-stu-id="b9087-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="b9087-111">字段是自动的基于其数据类型的显示格式。</span><span class="sxs-lookup"><span data-stu-id="b9087-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="b9087-112">字段将自动验证基于其数据类型。</span><span class="sxs-lookup"><span data-stu-id="b9087-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="b9087-113">可以在要自定义格式设置和验证行为的数据模型中添加元数据。</span><span class="sxs-lookup"><span data-stu-id="b9087-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="b9087-114">当执行此操作，可以只在一个位置添加格式设置和验证规则，并且它们正在自动应用无处不在您访问使用动态数据控件字段。</span><span class="sxs-lookup"><span data-stu-id="b9087-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="b9087-115">为了阐释其工作方式，将更改用于显示和编辑现有字段的控件*Students.aspx*页上，并且您会将格式设置和验证元数据添加到的名称和日期字段`Student`实体类型。</span><span class="sxs-lookup"><span data-stu-id="b9087-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="b9087-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="b9087-117">使用 DynamicField 和 DynamicControl 控件</span><span class="sxs-lookup"><span data-stu-id="b9087-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="b9087-118">打开*Students.aspx*页并在`StudentsGridView`控件替换**名称**并**注册日期**`TemplateField`元素使用以下标记：</span><span class="sxs-lookup"><span data-stu-id="b9087-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="b9087-119">此标记使用`DynamicControl`控件来代替`TextBox`并`Label`学生中的控件名称模板字段，并使用`DynamicField`注册日期的控件。</span><span class="sxs-lookup"><span data-stu-id="b9087-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="b9087-120">不指定任何格式字符串。</span><span class="sxs-lookup"><span data-stu-id="b9087-120">No format strings are specified.</span></span>

<span data-ttu-id="b9087-121">添加`ValidationSummary`后控制`StudentsGridView`控件。</span><span class="sxs-lookup"><span data-stu-id="b9087-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="b9087-122">在`SearchGridView`控件替换的标记**名称**并**注册日期**作为您的列中的操作`StudentsGridView`控件，但省略`EditItemTemplate`元素。</span><span class="sxs-lookup"><span data-stu-id="b9087-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="b9087-123">`Columns`元素的`SearchGridView`控件现在包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="b9087-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="b9087-124">打开*Students.aspx.cs*并添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="b9087-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="b9087-125">添加一个处理程序的页面的`Init`事件：</span><span class="sxs-lookup"><span data-stu-id="b9087-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="b9087-126">此代码指定动态数据将提供格式设置和在这些数据绑定控件中的字段的验证`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="b9087-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="b9087-127">如果在运行页面时收到一条错误消息，如下例所示，则通常意味着已忘记调用`EnableDynamicData`中的方法`Page_Init`:</span><span class="sxs-lookup"><span data-stu-id="b9087-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="b9087-128">运行页。</span><span class="sxs-lookup"><span data-stu-id="b9087-128">Run the page.</span></span>

<span data-ttu-id="b9087-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="b9087-130">在中**注册日期**列中，因为属性类型为时间除了日期显示`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="b9087-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="b9087-131">需要修复的更高版本。</span><span class="sxs-lookup"><span data-stu-id="b9087-131">You'll fix that later.</span></span>

<span data-ttu-id="b9087-132">现在，请注意，动态数据自动提供了基本的数据验证。</span><span class="sxs-lookup"><span data-stu-id="b9087-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="b9087-133">例如，单击**编辑**，清除日期字段中，单击**更新**，并查看，动态数据自动使此必填的字段因为值不是数据模型中可以为 null。</span><span class="sxs-lookup"><span data-stu-id="b9087-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="b9087-134">字段和中的错误消息后，该页面显示星号`ValidationSummary`控件：</span><span class="sxs-lookup"><span data-stu-id="b9087-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="b9087-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="b9087-136">可以省略`ValidationSummary`管理，因为您可以将鼠标指针拖通过星号可查看错误消息：</span><span class="sxs-lookup"><span data-stu-id="b9087-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="b9087-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="b9087-138">动态数据还将验证输入中的数据**注册日期**字段是有效的日期：</span><span class="sxs-lookup"><span data-stu-id="b9087-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="b9087-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="b9087-140">正如您所看到的这是一般性错误消息。</span><span class="sxs-lookup"><span data-stu-id="b9087-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="b9087-141">下一节中您将了解如何自定义消息，以及验证和格式设置规则。</span><span class="sxs-lookup"><span data-stu-id="b9087-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="b9087-142">将元数据添加到数据模型</span><span class="sxs-lookup"><span data-stu-id="b9087-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="b9087-143">通常情况下，你想要自定义动态数据提供的功能。</span><span class="sxs-lookup"><span data-stu-id="b9087-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="b9087-144">例如，可能会更改数据的显示方式和错误消息的内容。</span><span class="sxs-lookup"><span data-stu-id="b9087-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="b9087-145">你通常还自定义数据验证规则，以提供比动态数据提供更多的功能自动基于数据类型。</span><span class="sxs-lookup"><span data-stu-id="b9087-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="b9087-146">若要执行此操作，您创建对应于实体类型的分部类。</span><span class="sxs-lookup"><span data-stu-id="b9087-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="b9087-147">在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，选择**添加引用**，并添加对引用`System.ComponentModel.DataAnnotations`。</span><span class="sxs-lookup"><span data-stu-id="b9087-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="b9087-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="b9087-149">在中*DAL*文件夹中，创建一个新类文件，将其命名*Student.cs*，并在其中的模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="b9087-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="b9087-150">此代码将创建的分部类`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="b9087-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="b9087-151">`MetadataType`特性应用于此分部类标识你要用于指定元数据的类。</span><span class="sxs-lookup"><span data-stu-id="b9087-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="b9087-152">元数据类可以具有任何名称，但使用实体名称加"元数据"是一种常见做法。</span><span class="sxs-lookup"><span data-stu-id="b9087-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="b9087-153">应用于元数据类中的属性的属性指定格式化、 验证、 规则和错误消息。</span><span class="sxs-lookup"><span data-stu-id="b9087-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="b9087-154">如下所示的属性将具有以下结果：</span><span class="sxs-lookup"><span data-stu-id="b9087-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="b9087-155">`EnrollmentDate` 将显示为日期 （不含时间）。</span><span class="sxs-lookup"><span data-stu-id="b9087-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="b9087-156">这两个名称字段必须是 25 个字符或小于长度和自定义错误消息中提供。</span><span class="sxs-lookup"><span data-stu-id="b9087-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="b9087-157">这两个名称字段是必需的并提供自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="b9087-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="b9087-158">运行*Students.aspx*页，并查看现在没有时间的情况下显示日期：</span><span class="sxs-lookup"><span data-stu-id="b9087-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="b9087-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="b9087-160">编辑行并尝试进行清除名称字段中的值。</span><span class="sxs-lookup"><span data-stu-id="b9087-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="b9087-161">只要将一个字段，然后再单击显示，指示字段错误星号**更新**。</span><span class="sxs-lookup"><span data-stu-id="b9087-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="b9087-162">当您单击**更新**，页将显示你指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="b9087-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="b9087-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="b9087-164">尝试输入长度超过 25 个字符的名称，单击**更新**，和页显示您指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="b9087-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="b9087-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="b9087-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="b9087-166">现在，已设置了数据模型元数据中的这些格式设置和验证规则，规则将自动应用，用于显示或允许对这些字段，更改每一页上，只要您使用`DynamicControl`或`DynamicField`控件。</span><span class="sxs-lookup"><span data-stu-id="b9087-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="b9087-167">这将减少必须编写，后者将编程和测试更加轻松、 冗余代码量，它可确保数据格式设置和验证是在应用程序保持一致。</span><span class="sxs-lookup"><span data-stu-id="b9087-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="b9087-168">详细信息</span><span class="sxs-lookup"><span data-stu-id="b9087-168">More Information</span></span>

<span data-ttu-id="b9087-169">本系列如何开始使用实体框架的教程到此结束。</span><span class="sxs-lookup"><span data-stu-id="b9087-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="b9087-170">对于可帮助你了解如何使用实体框架的更多资源，请继续[下一步的实体框架教程系列中的第一个教程](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)或访问以下站点：</span><span class="sxs-lookup"><span data-stu-id="b9087-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="b9087-171">实体框架常见问题</span><span class="sxs-lookup"><span data-stu-id="b9087-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="b9087-172">实体框架团队博客</span><span class="sxs-lookup"><span data-stu-id="b9087-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="b9087-173">MSDN 库中的实体框架</span><span class="sxs-lookup"><span data-stu-id="b9087-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="b9087-174">MSDN 数据开发人员中心中的实体框架</span><span class="sxs-lookup"><span data-stu-id="b9087-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="b9087-175">MSDN 库中的 EntityDataSource Web 服务器控件概述</span><span class="sxs-lookup"><span data-stu-id="b9087-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="b9087-176">EntityDataSource 控件的 MSDN Library 中的 API 参考</span><span class="sxs-lookup"><span data-stu-id="b9087-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="b9087-177">MSDN 上的 entity Framework 论坛</span><span class="sxs-lookup"><span data-stu-id="b9087-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="b9087-178">Julie Lerman 的博客</span><span class="sxs-lookup"><span data-stu-id="b9087-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="b9087-179">上一篇</span><span class="sxs-lookup"><span data-stu-id="b9087-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
