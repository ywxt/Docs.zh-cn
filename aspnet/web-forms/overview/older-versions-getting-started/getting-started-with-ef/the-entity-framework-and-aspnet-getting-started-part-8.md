---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: "如何开始使用实体框架 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建 ASP.NET Web 窗体应用程序使用实体框架。 该示例应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: 323ee44f43f6d4081bd9ba50791755696bc9128f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="d0138-104">如何开始使用实体框架 4.0 数据库和 ASP.NET 4 Web 窗体的第 8 部分</span><span class="sxs-lookup"><span data-stu-id="d0138-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>
====================
<span data-ttu-id="d0138-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d0138-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="d0138-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="d0138-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="d0138-107">有关教程系列的信息，请参阅[序列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="d0138-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="d0138-108">使用动态数据功能进行格式化和验证数据</span><span class="sxs-lookup"><span data-stu-id="d0138-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="d0138-109">在以前的教程，你将实现存储的过程。</span><span class="sxs-lookup"><span data-stu-id="d0138-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="d0138-110">本教程将演示如何动态数据功能可以提供以下好处：</span><span class="sxs-lookup"><span data-stu-id="d0138-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="d0138-111">字段的显示基于其数据类型的自动格式设置。</span><span class="sxs-lookup"><span data-stu-id="d0138-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="d0138-112">字段将自动验证基于其数据类型。</span><span class="sxs-lookup"><span data-stu-id="d0138-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="d0138-113">你可以在要自定义格式设置和验证行为的数据模型中添加元数据。</span><span class="sxs-lookup"><span data-stu-id="d0138-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="d0138-114">在执行此操作时，可以将格式设置和验证规则添加只在一个位置，并且它们正在自动应用无处不在你访问使用动态数据控件字段。</span><span class="sxs-lookup"><span data-stu-id="d0138-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="d0138-115">若要查看此工作原理，你将更改用于显示和编辑中的现有字段的控件*Students.aspx*页上，并且你将添加格式设置和验证元数据的名称和日期字段`Student`实体类型。</span><span class="sxs-lookup"><span data-stu-id="d0138-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="d0138-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="d0138-117">使用 DynamicField 和 DynamicControl 控件</span><span class="sxs-lookup"><span data-stu-id="d0138-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="d0138-118">打开*Students.aspx*页并在`StudentsGridView`控件替换**名称**和**注册日期**`TemplateField`元素替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="d0138-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="d0138-119">此标记使用`DynamicControl`代替了控制`TextBox`和`Label`学生中的控件名称模板字段，并使用`DynamicField`注册日期的控件。</span><span class="sxs-lookup"><span data-stu-id="d0138-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="d0138-120">指定无格式字符串。</span><span class="sxs-lookup"><span data-stu-id="d0138-120">No format strings are specified.</span></span>

<span data-ttu-id="d0138-121">添加`ValidationSummary`后控制`StudentsGridView`控件。</span><span class="sxs-lookup"><span data-stu-id="d0138-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="d0138-122">在`SearchGridView`控件替换的标记**名称**和**注册日期**作为你的列未`StudentsGridView`控制，但省略`EditItemTemplate`元素。</span><span class="sxs-lookup"><span data-stu-id="d0138-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="d0138-123">`Columns`元素`SearchGridView`控件现在包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="d0138-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="d0138-124">打开*Students.aspx.cs*并添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="d0138-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="d0138-125">添加的处理程序已在页面的`Init`事件：</span><span class="sxs-lookup"><span data-stu-id="d0138-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="d0138-126">此代码指定格式设置和字段的这些数据绑定控件中的验证，将提供动态数据`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="d0138-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="d0138-127">如果运行页面时，你收到一条错误消息如下例所示，这通常意味着你忘记了调用`EnableDynamicData`中的方法`Page_Init`:</span><span class="sxs-lookup"><span data-stu-id="d0138-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="d0138-128">运行页面。</span><span class="sxs-lookup"><span data-stu-id="d0138-128">Run the page.</span></span>

<span data-ttu-id="d0138-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="d0138-130">在**注册日期**列中，时间显示了日期，因为该属性类型是`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="d0138-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="d0138-131">你将更高版本修复此问题。</span><span class="sxs-lookup"><span data-stu-id="d0138-131">You'll fix that later.</span></span>

<span data-ttu-id="d0138-132">现在，请注意，动态数据自动提供了基本的数据验证。</span><span class="sxs-lookup"><span data-stu-id="d0138-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="d0138-133">例如，单击**编辑**，清除日期字段中，单击**更新**，并且你看到，动态数据自动使此必填的字段因为该值不是数据模型中可以为 null。</span><span class="sxs-lookup"><span data-stu-id="d0138-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="d0138-134">字段和采用的错误消息后的页显示一个星号`ValidationSummary`控件：</span><span class="sxs-lookup"><span data-stu-id="d0138-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="d0138-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="d0138-136">可以省略`ValidationSummary`管理，因为你还可以通过以下方式将鼠标指针悬停星号以查看错误消息：</span><span class="sxs-lookup"><span data-stu-id="d0138-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="d0138-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="d0138-138">动态数据还将验证输入中的数据**注册日期**字段为有效日期：</span><span class="sxs-lookup"><span data-stu-id="d0138-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="d0138-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="d0138-140">如你所见，这是一般性错误消息。</span><span class="sxs-lookup"><span data-stu-id="d0138-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="d0138-141">在下一部分中，你将看到如何自定义消息，以及验证规则和格式设置规则。</span><span class="sxs-lookup"><span data-stu-id="d0138-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="d0138-142">将元数据添加到数据模型</span><span class="sxs-lookup"><span data-stu-id="d0138-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="d0138-143">通常情况下，你想要自定义所提供的动态数据功能。</span><span class="sxs-lookup"><span data-stu-id="d0138-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="d0138-144">例如，你可能会更改数据的显示方式以及错误消息的内容。</span><span class="sxs-lookup"><span data-stu-id="d0138-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="d0138-145">你通常还自定义数据验证规则来提供比动态数据提供更多的功能自动基于数据类型。</span><span class="sxs-lookup"><span data-stu-id="d0138-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="d0138-146">若要执行此操作，你可以创建对应于实体类型的分部类。</span><span class="sxs-lookup"><span data-stu-id="d0138-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="d0138-147">在**解决方案资源管理器**，右键单击**ContosoUniversity**项目，依次选择**添加引用**，并添加对引用`System.ComponentModel.DataAnnotations`。</span><span class="sxs-lookup"><span data-stu-id="d0138-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="d0138-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="d0138-149">在*DAL*文件夹中，创建一个新的类文件，将其命名为*Student.cs*，并替换为以下代码将在其中的模板代码。</span><span class="sxs-lookup"><span data-stu-id="d0138-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="d0138-150">此代码将创建一个分部类`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="d0138-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="d0138-151">`MetadataType`应用于此分部类的属性标识要用于指定元数据的类。</span><span class="sxs-lookup"><span data-stu-id="d0138-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="d0138-152">元数据类可以有任何名称，但使用的实体名称加上"元数据"是常见的做法。</span><span class="sxs-lookup"><span data-stu-id="d0138-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="d0138-153">应用于元数据类中的属性的特性指定格式设置、 验证、 规则和错误消息。</span><span class="sxs-lookup"><span data-stu-id="d0138-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="d0138-154">此处显示的属性将具有以下结果：</span><span class="sxs-lookup"><span data-stu-id="d0138-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="d0138-155">`EnrollmentDate`将显示为日期 （不含时间）。</span><span class="sxs-lookup"><span data-stu-id="d0138-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="d0138-156">这两个名称字段必须是 25 个字符或者小于长度，以及自定义错误消息中提供。</span><span class="sxs-lookup"><span data-stu-id="d0138-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="d0138-157">这两个名称字段是必需的并提供自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="d0138-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="d0138-158">运行*Students.aspx*页，并且你看到没有时间的情况下要现在显示日期：</span><span class="sxs-lookup"><span data-stu-id="d0138-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="d0138-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="d0138-160">编辑行和尝试清除名称字段中的值。</span><span class="sxs-lookup"><span data-stu-id="d0138-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="d0138-161">将字段，保留之前单击时，就会立即显示，该值指示字段错误星号**更新**。</span><span class="sxs-lookup"><span data-stu-id="d0138-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="d0138-162">当你单击**更新**，页会显示你指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="d0138-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="d0138-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="d0138-164">尝试输入超过 25 个字符的名称，请单击**更新**，并页显示你指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="d0138-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="d0138-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="d0138-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="d0138-166">现在，你已设置的数据模型元数据中这些格式设置和验证规则，规则将自动应用于每一页，用于显示或允许对这些字段中，所做更改处理程序，但前提是你使用`DynamicControl`或`DynamicField`控件。</span><span class="sxs-lookup"><span data-stu-id="d0138-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="d0138-167">这将减少你必须编写，后者将编程和测试更加轻松、 的冗余代码量，并确保数据格式设置和验证是在应用程序保持一致。</span><span class="sxs-lookup"><span data-stu-id="d0138-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="d0138-168">详细信息</span><span class="sxs-lookup"><span data-stu-id="d0138-168">More Information</span></span>

<span data-ttu-id="d0138-169">这一系列的 Entity Framework 入门教程到此结束。</span><span class="sxs-lookup"><span data-stu-id="d0138-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="d0138-170">对于可帮助你了解如何使用实体框架的更多资源，请继续[下一步的实体框架教程系列中的第一个教程](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)或访问以下站点：</span><span class="sxs-lookup"><span data-stu-id="d0138-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="d0138-171">实体框架常见问题</span><span class="sxs-lookup"><span data-stu-id="d0138-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="d0138-172">实体框架团队博客</span><span class="sxs-lookup"><span data-stu-id="d0138-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="d0138-173">MSDN 库中的实体框架</span><span class="sxs-lookup"><span data-stu-id="d0138-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="d0138-174">在 MSDN 数据开发人员中心的实体框架</span><span class="sxs-lookup"><span data-stu-id="d0138-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="d0138-175">MSDN 库中的 EntityDataSource Web 服务器控件概述</span><span class="sxs-lookup"><span data-stu-id="d0138-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="d0138-176">EntityDataSource 控件 MSDN 库中的 API 参考</span><span class="sxs-lookup"><span data-stu-id="d0138-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="d0138-177">MSDN 上的实体框架论坛</span><span class="sxs-lookup"><span data-stu-id="d0138-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="d0138-178">Julie Lerman 博客</span><span class="sxs-lookup"><span data-stu-id="d0138-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

>[!div class="step-by-step"]
[<span data-ttu-id="d0138-179">上一篇</span><span class="sxs-lookup"><span data-stu-id="d0138-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
