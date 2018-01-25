---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: "为 ASP.NET MVC 应用程序 (10 的第 4) 创建更复杂的数据模型 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: accb5ddab8df67dfa29038541dc0cd72eaac173c
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a><span data-ttu-id="f51a7-103">为 ASP.NET MVC 应用程序 (10 的第 4) 创建更复杂的数据模型</span><span class="sxs-lookup"><span data-stu-id="f51a7-103">Creating a More Complex Data Model for an ASP.NET MVC Application (4 of 10)</span></span>
====================
<span data-ttu-id="f51a7-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f51a7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f51a7-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="f51a7-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="f51a7-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f51a7-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="f51a7-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="f51a7-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="f51a7-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="f51a7-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="f51a7-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="f51a7-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="f51a7-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="f51a7-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="f51a7-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="f51a7-112">在前面的教程中，你处理简单的数据模型的三个实体组成。</span><span class="sxs-lookup"><span data-stu-id="f51a7-112">In the previous tutorials you worked with a simple data model that was composed of three entities.</span></span> <span data-ttu-id="f51a7-113">在本教程中你将添加多个实体和关系并将通过指定格式设置、 验证和数据库的映射规则自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-113">In this tutorial you'll add more entities and relationships and you'll customize the data model by specifying formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="f51a7-114">你将看到两种方式自定义数据模型： 通过将特性添加到实体类，通过将代码添加到数据库上下文类。</span><span class="sxs-lookup"><span data-stu-id="f51a7-114">You'll see two ways to customize the data model: by adding attributes to entity classes and by adding code to the database context class.</span></span>

<span data-ttu-id="f51a7-115">当完成时，实体类将组成以下图所示的已完成的数据模型：</span><span class="sxs-lookup"><span data-stu-id="f51a7-115">When you're finished, the entity classes will make up the completed data model that's shown in the following illustration:</span></span>

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a><span data-ttu-id="f51a7-117">通过使用属性自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="f51a7-117">Customize the Data Model by Using Attributes</span></span>

<span data-ttu-id="f51a7-118">在本部分中，你将了解如何通过使用指定格式设置，验证和数据库的映射规则的属性来自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-118">In this section you'll see how to customize the data model by using attributes that specify formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="f51a7-119">然后在多个下列各节，你将创建一种完整`School`通过添加数据模型属性的类已在模型中的剩余实体类型的创建和创建新类。</span><span class="sxs-lookup"><span data-stu-id="f51a7-119">Then in several of the following sections you'll create the complete `School` data model by adding attributes to the classes you already created and creating new classes for the remaining entity types in the model.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="f51a7-120">数据类型属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-120">The DataType Attribute</span></span>

<span data-ttu-id="f51a7-121">对于学生注册日期，网页的所有当前显示时间和日期，虽然所有关心为此字段是日期。</span><span class="sxs-lookup"><span data-stu-id="f51a7-121">For student enrollment dates, all of the web pages currently display the time along with the date, although all you care about for this field is the date.</span></span> <span data-ttu-id="f51a7-122">通过使用数据 annotation 特性，你可以使一个代码将在每个视图中显示的数据中修复的显示格式的更改。</span><span class="sxs-lookup"><span data-stu-id="f51a7-122">By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.</span></span> <span data-ttu-id="f51a7-123">若要查看如何执行操作，你将添加到属性的示例`EnrollmentDate`中的属性`Student`类。</span><span class="sxs-lookup"><span data-stu-id="f51a7-123">To see an example of how to do that, you'll add an attribute to the `EnrollmentDate` property in the `Student` class.</span></span>

<span data-ttu-id="f51a7-124">在*Models\Student.cs*，添加`using`语句`System.ComponentModel.DataAnnotations`命名空间并添加`DataType`和`DisplayFormat`特性以`EnrollmentDate`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-124">In *Models\Student.cs*, add a `using` statement for the `System.ComponentModel.DataAnnotations` namespace and add `DataType` and `DisplayFormat` attributes to the `EnrollmentDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

<span data-ttu-id="f51a7-125">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性用于指定比数据库内部类型更具体的数据类型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-125">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="f51a7-126">在这种情况下，我们只想跟踪的日期，不的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="f51a7-126">In this case we only want to keep track of the date, not the date and time.</span></span> <span data-ttu-id="f51a7-127">[DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供多种数据类型，如*日期、 时间、 PhoneNumber、 货币、 电子邮件地址*和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f51a7-127">The [DataType Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) provides for many data types, such as *Date, Time, PhoneNumber, Currency, EmailAddress* and more.</span></span> <span data-ttu-id="f51a7-128">应用程序还可通过 `DataType` 特性自动提供类型特定的功能。</span><span class="sxs-lookup"><span data-stu-id="f51a7-128">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="f51a7-129">例如，`mailto:`链接可以为创建[DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)，和日期选择器可提供用于[DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)中支持的浏览器[HTML5](http://html5.org/).</span><span class="sxs-lookup"><span data-stu-id="f51a7-129">For example, a `mailto:` link can be created for [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), and a date selector can be provided for [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in browsers that support [HTML5](http://html5.org/).</span></span> <span data-ttu-id="f51a7-130">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性发出 HTML 5[数据-](http://ejohn.org/blog/html-5-data-attributes/) (发音为*数据 dash*) HTML 5 浏览器可以理解的属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-130">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes emits HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (pronounced *data dash*) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="f51a7-131">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性不提供任何验证。</span><span class="sxs-lookup"><span data-stu-id="f51a7-131">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes do not provide any validation.</span></span>

<span data-ttu-id="f51a7-132">`DataType.Date` 不指定显示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="f51a7-132">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="f51a7-133">默认情况下，数据字段显示根据基于服务器的默认格式[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-133">By default, the data field is displayed according to the default formats based on the server's [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).</span></span>

<span data-ttu-id="f51a7-134">`DisplayFormat` 特性用于显式指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="f51a7-134">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


<span data-ttu-id="f51a7-135">`ApplyFormatInEditMode`设置指定，指定的格式设置也应该将应用时的值显示在文本框中以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="f51a7-135">The `ApplyFormatInEditMode` setting specifies that the specified formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="f51a7-136">(你可能不想的某些字段 — 例如，货币值，你可能不希望在文本框中的货币符号以进行编辑。)</span><span class="sxs-lookup"><span data-stu-id="f51a7-136">(You might not want that for some fields — for example, for currency values, you might not want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="f51a7-137">你可以使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性通过本身，但它通常是使用一个好办法[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)还属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-137">You can use the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute by itself, but it's generally a good idea to use the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute also.</span></span> <span data-ttu-id="f51a7-138">`DataType`属性传达*语义*的数据作为，而不是如何呈现在屏幕上，然后提供就不会使用了以下好处`DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="f51a7-138">The `DataType` attribute conveys the *semantics* of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with `DisplayFormat`:</span></span>

- <span data-ttu-id="f51a7-139">浏览器可以启用 HTML5 功能 （例如以显示一个日历控件、 区域设置相对应的货币符号、 电子邮件链接，等等）。</span><span class="sxs-lookup"><span data-stu-id="f51a7-139">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, etc.).</span></span>
- <span data-ttu-id="f51a7-140">默认情况下，浏览器将呈现数据使用基于的正确格式你[区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-140">By default, the browser will render data using the correct format based on your [locale](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).</span></span>
- <span data-ttu-id="f51a7-141">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性可以启用 MVC 能够选择要呈现的数据的右侧字段模板 ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)本身如果由使用字符串模板)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-141">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute can enable MVC to choose the right field template to render the data (the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) if used by itself uses the string template).</span></span> <span data-ttu-id="f51a7-142">有关详细信息，请参阅 Brad Wilson [ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-142">For more information, see Brad Wilson's [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="f51a7-143">（尽管为 MVC 2 编写的这篇文章仍适用于 ASP.NET MVC 的当前版本。）</span><span class="sxs-lookup"><span data-stu-id="f51a7-143">(Though written for MVC 2, this article still applies to the current version of ASP.NET MVC.)</span></span>

<span data-ttu-id="f51a7-144">如果你使用`DataType`属性与日期字段中，你必须指定`DisplayFormat`还以确保字段正确呈现在 Chrome 浏览器中的属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-144">If you use the `DataType` attribute with a date field, you have to specify the `DisplayFormat` attribute also in order to ensure that the field renders correctly in Chrome browsers.</span></span> <span data-ttu-id="f51a7-145">有关详细信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-145">For more information, see [this StackOverflow thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).</span></span>

<span data-ttu-id="f51a7-146">再次运行学生索引页，并请注意，注册日期不再显示时间。</span><span class="sxs-lookup"><span data-stu-id="f51a7-146">Run the Student Index page again and notice that times are no longer displayed for the enrollment dates.</span></span> <span data-ttu-id="f51a7-147">相同将适用于使用的任何视图`Student`模型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-147">The same will be true for any view that uses the `Student` model.</span></span>

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a><span data-ttu-id="f51a7-149">StringLengthAttribute</span><span class="sxs-lookup"><span data-stu-id="f51a7-149">The StringLengthAttribute</span></span>

<span data-ttu-id="f51a7-150">你还可以指定数据验证规则和使用属性的消息。</span><span class="sxs-lookup"><span data-stu-id="f51a7-150">You can also specify data validation rules and messages using attributes.</span></span> <span data-ttu-id="f51a7-151">假设你想要确保，用户不超过 50 个字符输入名称。</span><span class="sxs-lookup"><span data-stu-id="f51a7-151">Suppose you want to ensure that users don't enter more than 50 characters for a name.</span></span> <span data-ttu-id="f51a7-152">若要添加此限制，添加[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)特性以`LastName`和`FirstMidName`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-152">To add this limitation, add [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attributes to the `LastName` and `FirstMidName` properties, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

<span data-ttu-id="f51a7-153">[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性不会阻止的用户的空白区域输入一个名称。</span><span class="sxs-lookup"><span data-stu-id="f51a7-153">The [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute won't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="f51a7-154">你可以使用[正则表达式](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)要将限制应用到的输入属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-154">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to apply restrictions to the input.</span></span> <span data-ttu-id="f51a7-155">例如，下面的代码要求的第一个字符是大写且其余的字符是按字母顺序排列：</span><span class="sxs-lookup"><span data-stu-id="f51a7-155">For example the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

<span data-ttu-id="f51a7-156">[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)属性提供与类似的功能[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性但不提供客户端验证。</span><span class="sxs-lookup"><span data-stu-id="f51a7-156">The [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) attribute provides similar functionality to the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute but doesn't provide client side validation.</span></span>

<span data-ttu-id="f51a7-157">运行应用程序，然后单击**学生**选项卡。你收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="f51a7-157">Run the application and click the **Students** tab. You get the following error:</span></span>

<span data-ttu-id="f51a7-158">*数据库创建后，备份 SchoolContext 上下文的模型已更改。请考虑使用 Code First 迁移更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。*</span><span class="sxs-lookup"><span data-stu-id="f51a7-158">*The model backing the 'SchoolContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*</span></span>

<span data-ttu-id="f51a7-159">数据库模型已更改需要在数据库架构中，更改的方式，实体框架检测到。</span><span class="sxs-lookup"><span data-stu-id="f51a7-159">The database model has changed in a way that requires a change in the database schema, and Entity Framework detected that.</span></span> <span data-ttu-id="f51a7-160">你将使用迁移来更新架构，而不丢失任何通过使用 UI 添加到数据库的数据。</span><span class="sxs-lookup"><span data-stu-id="f51a7-160">You'll use migrations to update the schema without losing any data that you added to the database by using the UI.</span></span> <span data-ttu-id="f51a7-161">如果更改数据由`Seed`方法，将会更改回其原始状态由于[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法使用在`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="f51a7-161">If you changed data that was created by the `Seed` method, that will be changed back to its original state because of the [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) method that you're using in the `Seed` method.</span></span> <span data-ttu-id="f51a7-162">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)等效于"upsert"操作从数据库术语。)</span><span class="sxs-lookup"><span data-stu-id="f51a7-162">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) is equivalent to an "upsert" operation from database terminology.)</span></span>

<span data-ttu-id="f51a7-163">在包管理器控制台 (PMC) 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f51a7-163">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

<span data-ttu-id="f51a7-164">`add-migration MaxLengthOnNames`命令创建名为的文件*&lt;时间戳&gt;\_MaxLengthOnNames.cs*。</span><span class="sxs-lookup"><span data-stu-id="f51a7-164">The `add-migration MaxLengthOnNames` command creates a file named *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*.</span></span> <span data-ttu-id="f51a7-165">此文件包含将更新数据库，以匹配当前数据模型的代码。</span><span class="sxs-lookup"><span data-stu-id="f51a7-165">This file contains code that will update the database to match the current data model.</span></span> <span data-ttu-id="f51a7-166">实体框架使用的迁移文件名称前面预置的时间戳以整理迁移。</span><span class="sxs-lookup"><span data-stu-id="f51a7-166">The timestamp prepended to the migrations file name is used by Entity Framework to order the migrations.</span></span> <span data-ttu-id="f51a7-167">如果您删除数据库，创建多个迁移后或在部署项目通过使用迁移，迁移的所有应用于已创建的顺序。</span><span class="sxs-lookup"><span data-stu-id="f51a7-167">After you have created multiple migrations, if you drop the database, or if you deploy the project by using Migrations, all of the migrations are applied in the order in which they were created.</span></span>

<span data-ttu-id="f51a7-168">运行**创建**页，然后输入任一名称超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="f51a7-168">Run the **Create** page, and enter either name longer than 50 characters.</span></span> <span data-ttu-id="f51a7-169">一旦超过 50 个字符时，客户端验证将立即显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="f51a7-169">As soon as you exceed 50 characters, client side validation immediately shows an error message.</span></span>

![客户端端 val 错误](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a><span data-ttu-id="f51a7-171">列属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-171">The Column Attribute</span></span>

<span data-ttu-id="f51a7-172">特性还可用于控制如何类和属性映射到数据库。</span><span class="sxs-lookup"><span data-stu-id="f51a7-172">You can also use attributes to control how your classes and properties are mapped to the database.</span></span> <span data-ttu-id="f51a7-173">假设你已使用名称`FirstMidName`的第一个名称字段，因为该字段还可能包含中间名。</span><span class="sxs-lookup"><span data-stu-id="f51a7-173">Suppose you had used the name `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span> <span data-ttu-id="f51a7-174">但你想要将名为的数据库列`FirstName`，因为将编写针对数据库的即席查询的用户习惯于该名称。</span><span class="sxs-lookup"><span data-stu-id="f51a7-174">But you want the database column to be named `FirstName`, because users who will be writing ad-hoc queries against the database are accustomed to that name.</span></span> <span data-ttu-id="f51a7-175">若要使此映射，你可以使用`Column`属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-175">To make this mapping, you can use the `Column` attribute.</span></span>

<span data-ttu-id="f51a7-176">`Column`属性指定当创建数据库时，列`Student`映射到表`FirstMidName`属性将被命名为`FirstName`。</span><span class="sxs-lookup"><span data-stu-id="f51a7-176">The `Column` attribute specifies that when the database is created, the column of the `Student` table that maps to the `FirstMidName` property will be named `FirstName`.</span></span> <span data-ttu-id="f51a7-177">换而言之，你的代码引用到`Student.FirstMidName`，数据将来自或在中更新`FirstName`列`Student`表。</span><span class="sxs-lookup"><span data-stu-id="f51a7-177">In other words, when your code refers to `Student.FirstMidName`, the data will come from or be updated in the `FirstName` column of the `Student` table.</span></span> <span data-ttu-id="f51a7-178">如果未指定列名称，系统会提供与属性名相同的名称。</span><span class="sxs-lookup"><span data-stu-id="f51a7-178">If you don't specify column names, they are given the same name as the property name.</span></span>

<span data-ttu-id="f51a7-179">添加 using 语句[System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)和列名称属性与`FirstMidName`属性，如以下突出显示的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-179">Add a using statement for [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) and the column name attribute to the `FirstMidName` property, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

<span data-ttu-id="f51a7-180">添加[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)更改备份 SchoolContext，使它不会与数据库相匹配的模型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-180">The addition of the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) changes the model backing the SchoolContext, so it won't match the database.</span></span> <span data-ttu-id="f51a7-181">在创建另一个迁移 PMC 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f51a7-181">Enter the following commands in the PMC to create another migration:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

<span data-ttu-id="f51a7-182">在**服务器资源管理器**(**数据库资源管理器**如果你使用的 Express for Web)，双击*学生*表。</span><span class="sxs-lookup"><span data-stu-id="f51a7-182">In **Server Explorer** (**Database Explorer** if you are using Express for Web), double-click the *Student* table.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="f51a7-183">下图显示原始列名，因为其应用前两个迁移之前。</span><span class="sxs-lookup"><span data-stu-id="f51a7-183">The following image shows the original column name as it was before you applied the first two migrations.</span></span> <span data-ttu-id="f51a7-184">除了从更改的列名称`FirstMidName`到`FirstName`，两个名称列已更改从`MAX`长度为 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="f51a7-184">In addition to the column name changing from `FirstMidName` to `FirstName`, the two name columns have changed from `MAX` length to 50 characters.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="f51a7-185">你还可以进行数据库映射更改使用[Fluent API](https://msdn.microsoft.com/data/jj591617)，如你将看到在此教程的后面。</span><span class="sxs-lookup"><span data-stu-id="f51a7-185">You can also make database mapping changes using the [Fluent API](https://msdn.microsoft.com/data/jj591617), as you'll see later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="f51a7-186">如果您尝试编译之前创建的所有这些实体类完毕后，你可能会收到编译器错误。</span><span class="sxs-lookup"><span data-stu-id="f51a7-186">If you try to compile before you finish creating all of these entity classes, you might get compiler errors.</span></span>


## <a name="create-the-instructor-entity"></a><span data-ttu-id="f51a7-187">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-187">Create the Instructor Entity</span></span>

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="f51a7-189">创建*Models\Instructor.cs*，模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f51a7-189">Create *Models\Instructor.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="f51a7-190">请注意的几个属性都在相同`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-190">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="f51a7-191">在[实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列教程更高版本，你将重构使用继承来消除此冗余。</span><span class="sxs-lookup"><span data-stu-id="f51a7-191">In the [Implementing Inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series, you'll refactor using inheritance to eliminate this redundancy.</span></span>

### <a name="the-required-and-display-attributes"></a><span data-ttu-id="f51a7-192">所需和显示属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-192">The Required and Display Attributes</span></span>

<span data-ttu-id="f51a7-193">上的特性`LastName`属性指定它是必填的字段，在文本框中的标题，应 （而不是属性名称，它将是"LastName"没有空格） 中,"Last Name"和值不能超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="f51a7-193">The attributes on the `LastName` property specify that it's a required field, that the caption for the text box should be "Last Name" (instead of the property name, which would be "LastName" with no space), and that the value can't be longer than 50 characters.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="f51a7-194">[StringLength 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)数据库中设置的最大长度，并提供客户端和服务器端 ASP.NET MVC 的验证。</span><span class="sxs-lookup"><span data-stu-id="f51a7-194">The [StringLength attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) sets the maximum length in the database and provides client side and server side validation for ASP.NET MVC.</span></span> <span data-ttu-id="f51a7-195">你还可以通过以下方式指定最小字符串长度中此特性，但最小值对数据库架构没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="f51a7-195">You can also specify the minimum string length in this attribute, but the minimum value has no impact on the database schema.</span></span> <span data-ttu-id="f51a7-196">[必需的特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)不需要值类型，如 DateTime、 int、 双精度型、 和 float。</span><span class="sxs-lookup"><span data-stu-id="f51a7-196">The [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) is not needed for value types such as DateTime, int, double, and float.</span></span> <span data-ttu-id="f51a7-197">值类型不能被分配 null 值，因此它们都是本质上是必需。</span><span class="sxs-lookup"><span data-stu-id="f51a7-197">Value types cannot be assigned a null value, so they are inherently required.</span></span> <span data-ttu-id="f51a7-198">无法删除[必需的特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)并将其替换的最小长度参数`StringLength`属性：</span><span class="sxs-lookup"><span data-stu-id="f51a7-198">You could remove the [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) and replace it with a minimum length parameter for the `StringLength` attribute:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

<span data-ttu-id="f51a7-199">你可以在一行上，将多个属性，因此你还可以编写教师类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-199">You can put multiple attributes on one line, so you could also write the instructor class as follows:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="f51a7-200">FullName 计算属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-200">The FullName Calculated Property</span></span>

<span data-ttu-id="f51a7-201">`FullName`是返回一个值，通过串联两个其他属性创建一个计算的属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-201">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="f51a7-202">因此只有`get`访问器，但没有`FullName`列将生成数据库中。</span><span class="sxs-lookup"><span data-stu-id="f51a7-202">Therefore it has only a `get` accessor, and no `FullName` column will be generated in the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a><span data-ttu-id="f51a7-203">课程和 OfficeAssignment 导航属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-203">The Courses and OfficeAssignment Navigation Properties</span></span>

<span data-ttu-id="f51a7-204">`Courses`和`OfficeAssignment`属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-204">The `Courses` and `OfficeAssignment` properties are navigation properties.</span></span> <span data-ttu-id="f51a7-205">如前所述，它们通常定义为[虚拟](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，以便它们可以利用称为实体框架功能[延迟加载](https://msdn.microsoft.com/magazine/hh205756.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-205">As was explained earlier, they are typically defined as [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) so that they can take advantage of an Entity Framework feature called [lazy loading](https://msdn.microsoft.com/magazine/hh205756.aspx).</span></span> <span data-ttu-id="f51a7-206">此外，如果导航属性可以具有多个实体，则其类型必须实现[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="f51a7-206">In addition, if a navigation property can hold multiple entities, its type must implement the [ICollection&lt;T&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface.</span></span> <span data-ttu-id="f51a7-207">(例如[IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)但不是限定[IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx)因为`IEnumerable<T>`未实现[添加](https://msdn.microsoft.com/library/63ywd54z.aspx).</span><span class="sxs-lookup"><span data-stu-id="f51a7-207">(For example [IList&lt;T&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifies but not [IEnumerable&lt;T&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) because `IEnumerable<T>` doesn't implement [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).</span></span>

<span data-ttu-id="f51a7-208">一个教师可以教授任意数量的课程，因此`Courses`指一套`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-208">An instructor can teach any number of courses, so `Courses` is defined as a collection of `Course` entities.</span></span> <span data-ttu-id="f51a7-209">我们业务规则状态教师只能有一个 office 最多，因此`OfficeAssignment`定义为单个`OfficeAssignment`实体 (这可能会`null`如果不分配任何 office)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-209">Our business rules state an instructor can only have at most one office, so `OfficeAssignment` is defined as a single `OfficeAssignment` entity (which may be `null` if no office is assigned).</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a><span data-ttu-id="f51a7-210">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-210">Create the OfficeAssignment Entity</span></span>

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="f51a7-212">创建*Models\OfficeAssignment.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f51a7-212">Create *Models\OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="f51a7-213">生成项目时，这将保存所做的更改，验证尚未创建任何副本，并粘贴编译器可以捕获的错误。</span><span class="sxs-lookup"><span data-stu-id="f51a7-213">Build the project, which saves your changes and verifies you haven't made any copy and paste errors the compiler can catch.</span></span>

### <a name="the-key-attribute"></a><span data-ttu-id="f51a7-214">键属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-214">The Key Attribute</span></span>

<span data-ttu-id="f51a7-215">没有之间的对零或一一个关系`Instructor`和`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-215">There's a one-to-zero-or-one relationship between the `Instructor` and the `OfficeAssignment` entities.</span></span> <span data-ttu-id="f51a7-216">相对于其分配给，教师仅存在一个办公室分配，并且因此其主键也是其外的键与`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-216">An office assignment only exists in relation to the instructor it's assigned to, and therefore its primary key is also its foreign key to the `Instructor` entity.</span></span> <span data-ttu-id="f51a7-217">但实体框架无法自动识别`InstructorID`为主因为其名称不遵循此实体键`ID`或*classname* `ID`命名约定。</span><span class="sxs-lookup"><span data-stu-id="f51a7-217">But the Entity Framework can't automatically recognize `InstructorID` as the primary key of this entity because its name doesn't follow the `ID` or *classname* `ID` naming convention.</span></span> <span data-ttu-id="f51a7-218">因此，`Key`属性用于标识作为键：</span><span class="sxs-lookup"><span data-stu-id="f51a7-218">Therefore, the `Key` attribute is used to identify it as the key:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="f51a7-219">你还可以使用`Key`属性如果实体具有其自己的主键，但你想要 name 属性不同于`classnameID`或`ID`。</span><span class="sxs-lookup"><span data-stu-id="f51a7-219">You can also use the `Key` attribute if the entity does have its own primary key but you want to name the property something different than `classnameID` or `ID`.</span></span> <span data-ttu-id="f51a7-220">默认情况下 EF 将密钥视为非数据库生成因为列是标识关系。</span><span class="sxs-lookup"><span data-stu-id="f51a7-220">By default EF treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-foreignkey-attribute"></a><span data-ttu-id="f51a7-221">ForeignKey 属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-221">The ForeignKey Attribute</span></span>

<span data-ttu-id="f51a7-222">没有两个实体之间的一对一关系或一对零或一一个关系时 (此类之间`OfficeAssignment`和`Instructor`)，EF 无法制定关系的一端是主体，取决于哪一个顶点。</span><span class="sxs-lookup"><span data-stu-id="f51a7-222">When there is a one-to-zero-or-one relationship or a one-to-one relationship between two entities (such as between `OfficeAssignment` and `Instructor`), EF can't work out which end of the relationship is the principal and which end is dependent.</span></span> <span data-ttu-id="f51a7-223">一对一关系具有引用导航属性在转换为其他类的每个类。</span><span class="sxs-lookup"><span data-stu-id="f51a7-223">One-to-one relationships have a reference navigation property in each class to the other class.</span></span> <span data-ttu-id="f51a7-224">[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以应用到依赖的类，以建立关系。</span><span class="sxs-lookup"><span data-stu-id="f51a7-224">The [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) can be applied to the dependent class to establish the relationship.</span></span> <span data-ttu-id="f51a7-225">如果省略[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，当你尝试创建迁移时出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="f51a7-225">If you omit the [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), you get the following error when you try to create the migration:</span></span>

<span data-ttu-id="f51a7-226">无法确定类型 ContosoUniversity.Models.OfficeAssignment 和 ContosoUniversity.Models.Instructor 之间的关联的主体端。</span><span class="sxs-lookup"><span data-stu-id="f51a7-226">Unable to determine the principal end of an association between the types 'ContosoUniversity.Models.OfficeAssignment' and 'ContosoUniversity.Models.Instructor'.</span></span> <span data-ttu-id="f51a7-227">必须使用关系 fluent API 或数据注释显式配置此关联的主体端。</span><span class="sxs-lookup"><span data-stu-id="f51a7-227">The principal end of this association must be explicitly configured using either the relationship fluent API or data annotations.</span></span>

<span data-ttu-id="f51a7-228">在教程后面部分中，我们将演示如何使用 fluent API 中配置此关系。</span><span class="sxs-lookup"><span data-stu-id="f51a7-228">Later in the tutorial we'll show how to configure this relationship with the fluent API.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="f51a7-229">教师导航属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-229">The Instructor Navigation Property</span></span>

<span data-ttu-id="f51a7-230">`Instructor`实体具有一个可以为 null`OfficeAssignment`导航属性 （因为教师可能没有一个办公室分配），和`OfficeAssignment`实体具有非 null`Instructor`导航属性 （因为一个办公室分配无法存在，而一个教师-`InstructorID`是不可为 null)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-230">The `Instructor` entity has a nullable `OfficeAssignment` navigation property (because an instructor might not have an office assignment), and the `OfficeAssignment` entity has a non-nullable `Instructor` navigation property (because an office assignment can't exist without an instructor -- `InstructorID` is non-nullable).</span></span> <span data-ttu-id="f51a7-231">当`Instructor`实体具有相关`OfficeAssignment`实体，每个实体将具有对另一个在其导航属性的引用。</span><span class="sxs-lookup"><span data-stu-id="f51a7-231">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity will have a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="f51a7-232">您可以将`[Required]`教师导航属性，指定必须有相关的教师，但不需要这样做是因为 InstructorID 外键 （它也是此表的关键） 是不可为 null 的属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-232">You could put a `[Required]` attribute on the Instructor navigation property to specify that there must be a related instructor, but you don't have to do that because the InstructorID foreign key (which is also the key to this table) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="f51a7-233">修改过程实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-233">Modify the Course Entity</span></span>

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="f51a7-235">在*Models\Course.cs*，你添加的代码更早版本替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f51a7-235">In *Models\Course.cs*, replace the code you added earlier with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="f51a7-236">课程实体具有外键属性`DepartmentID`它指向相关`Department`实体，且没有`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-236">The course entity has a foreign key property `DepartmentID` which points to the related `Department` entity and it has a `Department` navigation property.</span></span> <span data-ttu-id="f51a7-237">实体框架不要求你将外键属性添加到你的数据模型，当你具有相关实体的导航属性时。</span><span class="sxs-lookup"><span data-stu-id="f51a7-237">The Entity Framework doesn't require you to add a foreign key property to your data model when you have a navigation property for a related entity.</span></span> <span data-ttu-id="f51a7-238">EF 会自动在数据库中创建外键在需要的位置。</span><span class="sxs-lookup"><span data-stu-id="f51a7-238">EF automatically creates foreign keys in the database wherever they are needed.</span></span> <span data-ttu-id="f51a7-239">但是，数据模型中具有外键可以使更新更简单、 更高效。</span><span class="sxs-lookup"><span data-stu-id="f51a7-239">But having the foreign key in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="f51a7-240">例如，当提取过程实体，若要编辑，`Department`实体为 null 时，如果你不加载它，当你更新课程实体中，你将需要来首次读取`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-240">For example, when you fetch a course entity to edit, the `Department` entity is null if you don't load it, so when you update the course entity, you would have to first fetch the `Department` entity.</span></span> <span data-ttu-id="f51a7-241">当外键属性`DepartmentID`包含在数据模型中，你无需提取`Department`之后更新的实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-241">When the foreign key property `DepartmentID` is included in the data model, you don't need to fetch the `Department` entity before you update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="f51a7-242">DatabaseGenerated 属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-242">The DatabaseGenerated Attribute</span></span>

<span data-ttu-id="f51a7-243">[DatabaseGenerated 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)与[无](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)参数`CourseID`属性指定主键值是由用户而不是由数据库生成。</span><span class="sxs-lookup"><span data-stu-id="f51a7-243">The [DatabaseGenerated attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) with the [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parameter on the `CourseID` property specifies that primary key values are provided by the user rather than generated by the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="f51a7-244">默认情况下，实体框架将假定主键值都由数据库。</span><span class="sxs-lookup"><span data-stu-id="f51a7-244">By default, the Entity Framework assumes that primary key values are generated by the database.</span></span> <span data-ttu-id="f51a7-245">在大多数情况下要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f51a7-245">That's what you want in most scenarios.</span></span> <span data-ttu-id="f51a7-246">但是，对于`Course`实体，将一个部门，另一个部门，一 2000年系列使用用户指定过程号例如 1000年系列，依次类推。</span><span class="sxs-lookup"><span data-stu-id="f51a7-246">However, for `Course` entities, you'll use a user-specified course number such as a 1000 series for one department, a 2000 series for another department, and so on.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="f51a7-247">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-247">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="f51a7-248">外键属性和中的导航属性`Course`实体反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="f51a7-248">The foreign key properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

- <span data-ttu-id="f51a7-249">课程都将分配到一个部门，因此没有`DepartmentID`外键和一个`Department`上面提到的原因的导航属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-249">A course is assigned to one department, so there's a `DepartmentID` foreign key and a `Department` navigation property for the reasons mentioned above.</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- <span data-ttu-id="f51a7-250">课程可以有任意数量的学生注册，因此`Enrollments`导航属性是集合：</span><span class="sxs-lookup"><span data-stu-id="f51a7-250">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- <span data-ttu-id="f51a7-251">可能由多个教师讲授课程因此`Instructors`导航属性是集合：</span><span class="sxs-lookup"><span data-stu-id="f51a7-251">A course may be taught by multiple instructors, so the `Instructors` navigation property is a collection:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a><span data-ttu-id="f51a7-252">创建部门实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-252">Creating the Department Entity</span></span>

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="f51a7-254">创建*Models\Department.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f51a7-254">Create *Models\Department.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a><span data-ttu-id="f51a7-255">列属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-255">The Column Attribute</span></span>

<span data-ttu-id="f51a7-256">前面使用[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)若要更改列名称映射。</span><span class="sxs-lookup"><span data-stu-id="f51a7-256">Earlier you used the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) to change column name mapping.</span></span> <span data-ttu-id="f51a7-257">中的代码`Department`实体，`Column`属性用于更改 SQL 数据类型映射，以便将将列定义使用的 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx)数据库中的类型：</span><span class="sxs-lookup"><span data-stu-id="f51a7-257">In the code for the `Department` entity, the `Column` attribute is being used to change SQL data type mapping so that the column will be defined using the SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) type in the database:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="f51a7-258">列映射通常不是必需的因为实体框架通常选择基于你定义的属性的 CLR 类型的相应 SQL Server 数据类型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-258">Column mapping is generally not required, because the Entity Framework usually chooses the appropriate SQL Server data type based on the CLR type that you define for the property.</span></span> <span data-ttu-id="f51a7-259">CLR`decimal`类型映射到 SQL Server`decimal`类型。</span><span class="sxs-lookup"><span data-stu-id="f51a7-259">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="f51a7-260">但在这种情况下你知道列将包含货币金额和[money](https://msdn.microsoft.com/library/ms179882.aspx)数据类型是更适合。</span><span class="sxs-lookup"><span data-stu-id="f51a7-260">But in this case you know that the column will be holding currency amounts, and the [money](https://msdn.microsoft.com/library/ms179882.aspx) data type is more appropriate for that.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="f51a7-261">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-261">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="f51a7-262">外键和导航属性反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="f51a7-262">The foreign key and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="f51a7-263">部门可能或可能没有管理员，并且管理员始终是一个教师。</span><span class="sxs-lookup"><span data-stu-id="f51a7-263">A department may or may not have an administrator, and an administrator is always an instructor.</span></span> <span data-ttu-id="f51a7-264">因此`InstructorID`属性是作为外键与包含`Instructor`后添加了实体，以及一个问号`int`键入标记用于将标记为可为 null 的属性。导航属性名为`Administrator`但保留`Instructor`实体：</span><span class="sxs-lookup"><span data-stu-id="f51a7-264">Therefore the `InstructorID` property is included as the foreign key to the `Instructor` entity, and a question mark is added after the `int` type designation to mark the property as nullable.The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- <span data-ttu-id="f51a7-265">部门可能有许多课程，因此`Courses`导航属性：</span><span class="sxs-lookup"><span data-stu-id="f51a7-265">A department may have many courses, so there's a `Courses` navigation property:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

 > [!NOTE]
 > <span data-ttu-id="f51a7-266">按照约定，实体框架使级联删除对于不可为 null 的外键以及多对多关系。</span><span class="sxs-lookup"><span data-stu-id="f51a7-266">By convention, the Entity Framework enables cascade delete for non-nullable foreign keys and for many-to-many relationships.</span></span> <span data-ttu-id="f51a7-267">这可能导致循环的级联删除规则，初始值设定项代码运行时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="f51a7-267">This can result in circular cascade delete rules, which will cause an exception when your initializer code runs.</span></span> <span data-ttu-id="f51a7-268">例如，如果你未定义`Department.InstructorID`为可为 null 的属性，你会收到以下异常消息的初始值设定项运行时:"的引用关系会导致不允许循环引用。"</span><span class="sxs-lookup"><span data-stu-id="f51a7-268">For example, if you didn't define the `Department.InstructorID` property as nullable, you'd get the following exception message when the initializer runs: "The referential relationship will result in a cyclical reference that's not allowed."</span></span> <span data-ttu-id="f51a7-269">如果您的业务规则需要`InstructorID`作为不可为 null 的属性，你将需要使用以下 fluent API 若要禁用的关系上的级联删除：</span><span class="sxs-lookup"><span data-stu-id="f51a7-269">If your business rules required `InstructorID` property as non-nullable, you would have to use the following fluent API to disable cascade delete on the relationship:</span></span> 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]


## <a name="modifying-the-student-entity"></a><span data-ttu-id="f51a7-270">修改学生实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-270">Modifying the Student Entity</span></span>

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="f51a7-272">在*Models\Student.cs*，更早版本将你添加的代码替换为下面的代码。</span><span class="sxs-lookup"><span data-stu-id="f51a7-272">In *Models\Student.cs*, replace the code you added earlier with the following code.</span></span> <span data-ttu-id="f51a7-273">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f51a7-273">The changes are highlighted.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a><span data-ttu-id="f51a7-274">注册实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-274">The Enrollment Entity</span></span>

 <span data-ttu-id="f51a7-275">在*Models\Enrollment.cs*，更早版本将你添加的代码替换为下面的代码</span><span class="sxs-lookup"><span data-stu-id="f51a7-275">In *Models\Enrollment.cs*, replace the code you added earlier with the following code</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="f51a7-276">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="f51a7-276">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="f51a7-277">外键属性和导航属性反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="f51a7-277">The foreign key properties and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="f51a7-278">注册记录已经是单个的课程，因此`CourseID`外键属性和`Course`导航属性：</span><span class="sxs-lookup"><span data-stu-id="f51a7-278">An enrollment record is for a single course, so there's a `CourseID` foreign key property and a `Course` navigation property:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- <span data-ttu-id="f51a7-279">因此，注册记录将适用于单个学生，`StudentID`外键属性和`Student`导航属性：</span><span class="sxs-lookup"><span data-stu-id="f51a7-279">An enrollment record is for a single student, so there's a `StudentID` foreign key property and a `Student` navigation property:</span></span> 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a><span data-ttu-id="f51a7-280">多对多关系</span><span class="sxs-lookup"><span data-stu-id="f51a7-280">Many-to-Many Relationships</span></span>

<span data-ttu-id="f51a7-281">没有之间的多对多关系`Student`和`Course`实体，与`Enrollment`实体充当多对多联接表*具有负载*数据库中。</span><span class="sxs-lookup"><span data-stu-id="f51a7-281">There's a many-to-many relationship between the `Student` and `Course` entities, and the `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="f51a7-282">这意味着，`Enrollment`表包含用于联接的表的外键除了其他数据 (在这种情况下，主键和`Grade`属性)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-282">This means that the `Enrollment` table contains additional data besides foreign keys for the joined tables (in this case, a primary key and a `Grade` property).</span></span>

<span data-ttu-id="f51a7-283">下图显示这些关系中的实体关系图的外观。</span><span class="sxs-lookup"><span data-stu-id="f51a7-283">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="f51a7-284">(此关系图生成使用[实体框架 Power 工具](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); 创建关系图不属于本教程，只需使用此处为说明。)</span><span class="sxs-lookup"><span data-stu-id="f51a7-284">(This diagram was generated using the [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); creating the diagram isn't part of the tutorial, it's just being used here as an illustration.)</span></span>

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

<span data-ttu-id="f51a7-286">每个关系行已在一台端和星号 1 (\*) 在另一个，，该值指示一个对多关系。</span><span class="sxs-lookup"><span data-stu-id="f51a7-286">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="f51a7-287">如果`Enrollment`表没有包括年级信息，它只需包含两个外键`CourseID`和`StudentID`。</span><span class="sxs-lookup"><span data-stu-id="f51a7-287">If the `Enrollment` table didn't include grade information, it would only need to contain the two foreign keys `CourseID` and `StudentID`.</span></span> <span data-ttu-id="f51a7-288">在这种情况下，它将对应的多对多联接表*而无需负载*(或*纯联接表*) 在数据库中，并且您不需要在所有为它创建一个模型类。</span><span class="sxs-lookup"><span data-stu-id="f51a7-288">In that case, it would correspond to a many-to-many join table *without payload* (or a *pure join table*) in the database, and you wouldn't have to create a model class for it at all.</span></span> <span data-ttu-id="f51a7-289">`Instructor`和`Course`实体具有这种多对多关系，并且如你所见，它们之间没有任何实体类：</span><span class="sxs-lookup"><span data-stu-id="f51a7-289">The `Instructor` and `Course` entities have that kind of many-to-many relationship, and as you can see, there is no entity class between them:</span></span>

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="f51a7-291">联接表需要在数据库中，但是，以下数据库关系图中所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-291">A join table is required in the database, however, as shown in the following database diagram:</span></span>

![Instructor-Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

<span data-ttu-id="f51a7-293">实体框架会自动创建`CourseInstructor`表和你读取和更新到通过读取和更新的间接`Instructor.Courses`和`Course.Instructors`导航属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-293">The Entity Framework automatically creates the `CourseInstructor` table, and you read and update it indirectly by reading and updating the `Instructor.Courses` and `Course.Instructors` navigation properties.</span></span>

## <a name="entity-diagram-showing-relationships"></a><span data-ttu-id="f51a7-294">关系图显示关系的实体</span><span class="sxs-lookup"><span data-stu-id="f51a7-294">Entity Diagram Showing Relationships</span></span>

<span data-ttu-id="f51a7-295">下图显示为已完成的 School 模型的实体框架 Power 工具创建的关系图。</span><span class="sxs-lookup"><span data-stu-id="f51a7-295">The following illustration shows the diagram that the Entity Framework Power Tools create for the completed School model.</span></span>

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="f51a7-297">除了多对多关系线 (\*到\*) 和一个对多关系行 (1 到\*)，你可以在此处看到对零或一一个关系行 (1 对 0.1) 之间`Instructor`和`OfficeAssignment`实体和零-或--一对多关系行 (0.1 对\*) 教师和部门实体之间。</span><span class="sxs-lookup"><span data-stu-id="f51a7-297">Besides the many-to-many relationship lines (\* to \*) and the one-to-many relationship lines (1 to \*), you can see here the one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities and the zero-or-one-to-many relationship line (0..1 to \*) between the Instructor and Department entities.</span></span>

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a><span data-ttu-id="f51a7-298">通过将代码添加到数据库上下文中自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="f51a7-298">Customize the Data Model by adding Code to the Database Context</span></span>

<span data-ttu-id="f51a7-299">接下来你将添加到新的实体`SchoolContext`类和自定义的映射使用某些[fluent API](https://msdn.microsoft.com/data/jj591617)调用。</span><span class="sxs-lookup"><span data-stu-id="f51a7-299">Next you'll add the new entities to the `SchoolContext` class and customize some of the mapping using [fluent API](https://msdn.microsoft.com/data/jj591617) calls.</span></span> <span data-ttu-id="f51a7-300">（API 是"fluent"因为它通常用于通过连接一系列方法调用一起成一条语句。）</span><span class="sxs-lookup"><span data-stu-id="f51a7-300">(The API is "fluent" because it's often used by stringing a series of method calls together into a single statement.)</span></span>

<span data-ttu-id="f51a7-301">在本教程中将仅为不能具有属性的数据库映射中使用 fluent API。</span><span class="sxs-lookup"><span data-stu-id="f51a7-301">In this tutorial you'll use the fluent API only for database mapping that you can't do with attributes.</span></span> <span data-ttu-id="f51a7-302">但是，你可以使用 fluent API 指定的格式、 验证和映射规则，你可以通过使用特性执行大多数。</span><span class="sxs-lookup"><span data-stu-id="f51a7-302">However, you can also use the fluent API to specify most of the formatting, validation, and mapping rules that you can do by using attributes.</span></span> <span data-ttu-id="f51a7-303">某些属性，如`MinimumLength`不能使用 fluent API 应用。</span><span class="sxs-lookup"><span data-stu-id="f51a7-303">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="f51a7-304">如前所述，`MinimumLength`不会更改架构，它仅适用于客户端和服务器端验证规则</span><span class="sxs-lookup"><span data-stu-id="f51a7-304">As mentioned previously, `MinimumLength` doesn't change the schema, it only applies a client and server side validation rule</span></span>

<span data-ttu-id="f51a7-305">一些开发人员更愿意使用 fluent API 以独占方式，以便它们能够获得它们的实体类"清理"。</span><span class="sxs-lookup"><span data-stu-id="f51a7-305">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="f51a7-306">如果你想，并且有几个仅可由使用 fluent API 中完成的自定义项，可以混合属性和 fluent API，但建议的做法通常是选择这两种方法之一，并使用该一致地尽可能多地。</span><span class="sxs-lookup"><span data-stu-id="f51a7-306">You can mix attributes and fluent API if you want, and there are a few customizations that can only be done by using fluent API, but in general the recommended practice is to choose one of these two approaches and use that consistently as much as possible.</span></span>

<span data-ttu-id="f51a7-307">若要添加新的实体数据模型和执行未通过使用属性执行操作的数据库映射中的代码替换*DAL\SchoolContext.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f51a7-307">To add the new entities to the data model and perform database mapping that you didn't do by using attributes, replace the code in *DAL\SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="f51a7-308">中的新语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法配置多对多联接表：</span><span class="sxs-lookup"><span data-stu-id="f51a7-308">The new statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method configures the many-to-many join table:</span></span>

- <span data-ttu-id="f51a7-309">之间的多对多关系`Instructor`和`Course`实体，该代码指定联接表的表和列名称。</span><span class="sxs-lookup"><span data-stu-id="f51a7-309">For the many-to-many relationship between the `Instructor` and `Course` entities, the code specifies the table and column names for the join table.</span></span> <span data-ttu-id="f51a7-310">代码首先可以配置多对多关系为你不使用此代码，但如果你不调用它，你将获取默认名称类似于`InstructorInstructorID`为`InstructorID`列。</span><span class="sxs-lookup"><span data-stu-id="f51a7-310">Code First can configure the many-to-many relationship for you without this code, but if you don't call it, you will get default names such as `InstructorInstructorID` for the `InstructorID` column.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="f51a7-311">以下代码举例说明如何你本来也可以使用 fluent API 而不是特性来指定之间的关系`Instructor`和`OfficeAssignment`实体：</span><span class="sxs-lookup"><span data-stu-id="f51a7-311">The following code provides an example of how you could have used fluent API instead of attributes to specify the relationship between the `Instructor` and `OfficeAssignment` entities:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

<span data-ttu-id="f51a7-312">有关在幕后做什么"fluent API"语句的信息，请参阅[Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx)博客文章。</span><span class="sxs-lookup"><span data-stu-id="f51a7-312">For information about what "fluent API" statements are doing behind the scenes, see the [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog post.</span></span>

## <a name="seed-the-database-with-test-data"></a><span data-ttu-id="f51a7-313">种子使用测试数据的数据库</span><span class="sxs-lookup"><span data-stu-id="f51a7-313">Seed the Database with Test Data</span></span>

<span data-ttu-id="f51a7-314">中的代码替换*Migrations\Configuration.cs*文件替换为以下代码，以便为你已创建的新实体提供种子数据。</span><span class="sxs-lookup"><span data-stu-id="f51a7-314">Replace the code in the *Migrations\Configuration.cs* file with the following code in order to provide seed data for the new entities you've created.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

<span data-ttu-id="f51a7-315">正如你看到的第一个教程中，大多数的此代码只需更新或创建新的实体对象并将示例数据加载到所需的测试的属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-315">As you saw in the first tutorial, most of this code simply updates or creates new entity objects and loads sample data into properties as required for testing.</span></span> <span data-ttu-id="f51a7-316">但请注意如何`Course`实体，具有多对多关系与`Instructor`实体，进行处理：</span><span class="sxs-lookup"><span data-stu-id="f51a7-316">However, notice how the `Course` entity, which has a many-to-many relationship with the `Instructor` entity, is handled:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

<span data-ttu-id="f51a7-317">当你创建`Course`对象，初始化`Instructors`导航属性为空集合使用的代码`Instructors = new List<Instructor>()`。</span><span class="sxs-lookup"><span data-stu-id="f51a7-317">When you create a `Course` object, you initialize the `Instructors` navigation property as an empty collection using the code `Instructors = new List<Instructor>()`.</span></span> <span data-ttu-id="f51a7-318">这样便能添加`Instructor`与此相关的实体`Course`使用`Instructors.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="f51a7-318">This makes it possible to add `Instructor` entities that are related to this `Course` by using the `Instructors.Add` method.</span></span> <span data-ttu-id="f51a7-319">如果你尚未创建一个空列表，你将无法添加这些关系，因为`Instructors`属性将为 null，并且将不会有`Add`方法。</span><span class="sxs-lookup"><span data-stu-id="f51a7-319">If you didn't create an empty list, you wouldn't be able to add these relationships, because the `Instructors` property would be null and wouldn't have an `Add` method.</span></span> <span data-ttu-id="f51a7-320">你还可以向构造函数添加的列表初始化。</span><span class="sxs-lookup"><span data-stu-id="f51a7-320">You could also add the list initialization to the constructor.</span></span>

## <a name="add-a-migration-and-update-the-database"></a><span data-ttu-id="f51a7-321">添加迁移并更新数据库</span><span class="sxs-lookup"><span data-stu-id="f51a7-321">Add a Migration and Update the Database</span></span>

<span data-ttu-id="f51a7-322">从 PMC，输入`add-migration`命令：</span><span class="sxs-lookup"><span data-stu-id="f51a7-322">From the PMC, enter the `add-migration` command:</span></span>

`PM> add-Migration Chap4`

<span data-ttu-id="f51a7-323">如果你尝试在此时更新数据库，你将收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="f51a7-323">If you try to update the database at this point, you'll get the following error:</span></span>

<span data-ttu-id="f51a7-324">*ALTER TABLE 语句与外键约束冲突"FK\_dbo。课程\_dbo。部门\_DepartmentID"。冲突发生于数据库"ContosoUniversity"表"dbo。部门"，列 DepartmentID。*</span><span class="sxs-lookup"><span data-stu-id="f51a7-324">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Course\_dbo.Department\_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.*</span></span>

<span data-ttu-id="f51a7-325">编辑&lt;*时间戳&gt;\_Chap4.cs*文件中，并进行下面的代码更改 (将添加 SQL 语句和修改`AddColumn`语句):</span><span class="sxs-lookup"><span data-stu-id="f51a7-325">Edit the &lt;*timestamp&gt;\_Chap4.cs* file, and make the following code changes (you'll add a SQL statement and modify an `AddColumn` statement):</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

<span data-ttu-id="f51a7-326">(请确保注释掉或删除现有`AddColumn`行添加新库项，或当你输入时，将收到错误时`update-database`命令。)</span><span class="sxs-lookup"><span data-stu-id="f51a7-326">(Make sure that you comment out or delete the existing `AddColumn` line when you add the new one, or you'll get an error when you enter the `update-database` command.)</span></span>

<span data-ttu-id="f51a7-327">有时时执行现有数据的迁移，你需要存根 （stub） 数据插入到数据库以满足外键约束，并且现在你要做。</span><span class="sxs-lookup"><span data-stu-id="f51a7-327">Sometimes when you execute migrations with existing data, you need to insert stub data into the database to satisfy foreign key constraints, and that's what you're doing now.</span></span> <span data-ttu-id="f51a7-328">生成的代码将添加不可为 null`DepartmentID`外的键与`Course`表。</span><span class="sxs-lookup"><span data-stu-id="f51a7-328">The generated code adds a non-nullable `DepartmentID` foreign key to the `Course` table.</span></span> <span data-ttu-id="f51a7-329">如果已有中行`Course`表当代码运行，`AddColumn`操作将失败，因为 SQL Server 并不知道要放入中不能为 null 的列的值。</span><span class="sxs-lookup"><span data-stu-id="f51a7-329">If there are already rows in the `Course` table when the code runs, the `AddColumn` operation would fail because SQL Server doesn't know what value to put in the column that can't be null.</span></span> <span data-ttu-id="f51a7-330">因此，你已更改的代码，为新列提供默认值，并创建了名为"Temp"使其作为默认部门的存根 （stub） 部门。</span><span class="sxs-lookup"><span data-stu-id="f51a7-330">Therefore you've changed the code to give the new column a default value, and you've created a stub department named "Temp" to act as the default department.</span></span> <span data-ttu-id="f51a7-331">因此，如果存在`Course`行时此代码运行时，它们将所有相关到"Temp"部门。</span><span class="sxs-lookup"><span data-stu-id="f51a7-331">As a result, if there are existing `Course` rows when this code runs, they will all be related to the "Temp" department.</span></span>

<span data-ttu-id="f51a7-332">当`Seed`方法运行时，它将插入中行`Department`表和它将与现有`Course`到这些新行`Department`行。</span><span class="sxs-lookup"><span data-stu-id="f51a7-332">When the `Seed` method runs, it will insert rows in the `Department` table and it will relate existing `Course` rows to those new `Department` rows.</span></span> <span data-ttu-id="f51a7-333">如果你尚未添加任何课程，在 UI 中，则不再需要"Temp"部门或默认值上`Course.DepartmentID`列。</span><span class="sxs-lookup"><span data-stu-id="f51a7-333">If you haven't added any courses in the UI, you would then no longer need the "Temp" department or the default value on the `Course.DepartmentID` column.</span></span> <span data-ttu-id="f51a7-334">若要允许是否可能会出现，有人可能添加课程使用应用程序，你还想要更新`Seed`方法代码，以确保所有`Course`行 (而不仅仅是由早期的运行插入`Seed`方法) 具有有效`DepartmentID`值之前，请删除默认值列中的值并删除"Temp"部门。</span><span class="sxs-lookup"><span data-stu-id="f51a7-334">To allow for the possibility that someone might have added courses by using the application, you'd also want to update the `Seed` method code to ensure that all `Course` rows (not just the ones inserted by earlier runs of the `Seed` method) have valid `DepartmentID` values before you remove the default value from the column and delete the "Temp" department.</span></span>

<span data-ttu-id="f51a7-335">完成编辑后&lt;*时间戳&gt;\_Chap4.cs*文件中，输入`update-database`命令 PMC 执行迁移。</span><span class="sxs-lookup"><span data-stu-id="f51a7-335">After you have finished editing the &lt;*timestamp&gt;\_Chap4.cs* file, enter the `update-database` command in the PMC to execute the migration.</span></span>

> [!NOTE]
> <span data-ttu-id="f51a7-336">很可能会迁移数据和进行架构更改时获得其他错误。</span><span class="sxs-lookup"><span data-stu-id="f51a7-336">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="f51a7-337">如果您无法解析的迁移错误，您可以更改中的连接字符串*Web.config*文件或删除数据库。</span><span class="sxs-lookup"><span data-stu-id="f51a7-337">If you get migration errors you can't resolve, you can either change the connection string in the *Web.config* file or delete the database.</span></span> <span data-ttu-id="f51a7-338">最简单方法是在数据库重命名*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f51a7-338">The simplest approach is to rename the database in *Web.config* file.</span></span> <span data-ttu-id="f51a7-339">例如，将数据库名称更改为 CU\_测试如在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f51a7-339">For example, change the database name to CU\_test as shown in the following:</span></span>
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
>  <span data-ttu-id="f51a7-340">与新数据库，没有数据迁移，和`update-database`命令是更可能完成且未发生错误。</span><span class="sxs-lookup"><span data-stu-id="f51a7-340">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="f51a7-341">有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-341">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span>


<span data-ttu-id="f51a7-342">打开中的数据库**服务器资源管理器**未更早版本，以及展开**表**节点以查看是否已创建的所有表。</span><span class="sxs-lookup"><span data-stu-id="f51a7-342">Open the database in **Server Explorer** as you did earlier, and expand the **Tables** node to see that all of the tables have been created.</span></span> <span data-ttu-id="f51a7-343">(如果仍有**服务器资源管理器**打开从较早的时间，请单击**刷新**按钮。)</span><span class="sxs-lookup"><span data-stu-id="f51a7-343">(If you still have **Server Explorer** open from the earlier time, click the **Refresh** button.)</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="f51a7-344">你未创建的模型类`CourseInstructor`表。</span><span class="sxs-lookup"><span data-stu-id="f51a7-344">You didn't create a model class for the `CourseInstructor` table.</span></span> <span data-ttu-id="f51a7-345">如前面所述，这是之间的多对多关系的联接表`Instructor`和`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="f51a7-345">As explained earlier, this is a join table for the many-to-many relationship between the `Instructor` and `Course` entities.</span></span>

<span data-ttu-id="f51a7-346">右键单击`CourseInstructor`表，然后选择**显示表数据**以验证它的结果中有数据`Instructor`添加到实体`Course.Instructors`导航属性。</span><span class="sxs-lookup"><span data-stu-id="f51a7-346">Right-click the `CourseInstructor` table and select **Show Table Data** to verify that it has data in it as a result of the `Instructor` entities you added to the `Course.Instructors` navigation property.</span></span>

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a><span data-ttu-id="f51a7-348">摘要</span><span class="sxs-lookup"><span data-stu-id="f51a7-348">Summary</span></span>

<span data-ttu-id="f51a7-349">现在将具有更复杂的数据模型和相应的数据库。</span><span class="sxs-lookup"><span data-stu-id="f51a7-349">You now have a more complex data model and corresponding database.</span></span> <span data-ttu-id="f51a7-350">在以下教程中你将了解有关访问相关的数据的不同方式的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f51a7-350">In the following tutorial you'll learn more about different ways to access related data.</span></span>

<span data-ttu-id="f51a7-351">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="f51a7-351">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f51a7-352">[上一页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[下一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="f51a7-352">[Previous](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
