---
title: "与 EF 核心-数据模型-5 8 razor 页"
author: rick-anderson
description: "在本教程中添加更多实体和关系，并通过指定格式设置、 验证和数据库的映射规则自定义数据模型。"
ms.author: riande
manager: wpickett
ms.date: 10/25/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: 2446f4734e9bb1ab6829001f6e7888c4c14ee1b7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="creating-a-complex-data-model---ef-core-with-razor-pages-tutorial-5-of-8"></a><span data-ttu-id="5c9fd-103">创建复杂的数据模型的 EF 核心 Razor 页教程 (5 的 8)</span><span class="sxs-lookup"><span data-stu-id="5c9fd-103">Creating a complex data model - EF Core with Razor Pages tutorial (5 of 8)</span></span>

<span data-ttu-id="5c9fd-104">通过[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5c9fd-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="5c9fd-105">与基本数据模型的三个实体组成合作，前面的教程。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-105">The previous tutorials worked with a basic data model that was composed of three entities.</span></span> <span data-ttu-id="5c9fd-106">在本教程中：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-106">In this tutorial:</span></span>

* <span data-ttu-id="5c9fd-107">添加更多实体和关系。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-107">More entities and relationships are added.</span></span>
* <span data-ttu-id="5c9fd-108">通过指定格式设置、 验证和数据库的映射规则自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-108">The data model is customized by specifying formatting, validation, and database mapping rules.</span></span>

<span data-ttu-id="5c9fd-109">已完成的数据模型的实体类是在下图中所示：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-109">The entity classes for the completed data model is shown in the following illustration:</span></span>

![实体关系图](complex-data-model/_static/diagram.png)

<span data-ttu-id="5c9fd-111">如果你遇到无法解决的问题，请下载[对此阶段已完成应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-111">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex).</span></span>

## <a name="customize-the-data-model-with-attributes"></a><span data-ttu-id="5c9fd-112">自定义数据模型具有属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-112">Customize the data model with attributes</span></span>

<span data-ttu-id="5c9fd-113">在此部分中，数据模型是使用自定义属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-113">In this section, the data model is customized using attributes.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="5c9fd-114">数据类型属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-114">The DataType attribute</span></span>

<span data-ttu-id="5c9fd-115">学生页当前显示的注册日期的时间。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-115">The student pages currently displays the time of the enrollment date.</span></span> <span data-ttu-id="5c9fd-116">通常情况下，日期字段显示仅显示日期而非时间。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-116">Typically, date fields show only the date and not the time.</span></span>

<span data-ttu-id="5c9fd-117">更新*Models/Student.cs*替换为以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-117">Update *Models/Student.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

<span data-ttu-id="5c9fd-118">[DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1)属性指定比数据库内部类型更具体的数据类型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-118">The [DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) attribute specifies a data type that's more specific than the database intrinsic type.</span></span> <span data-ttu-id="5c9fd-119">在此情况下应显示仅显示日期，不的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-119">In this case only the date should be displayed, not the date and time.</span></span> <span data-ttu-id="5c9fd-120">[DataType 枚举](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1)提供对于许多数据类型，例如日期、 时间、 电话号码、 货币、 电子邮件地址，等等。`DataType`属性还可以启用该应用程序自动提供特定类型的功能。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-120">The [DataType Enumeration](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, etc. The `DataType` attribute can also enable the app to automatically provide type-specific features.</span></span> <span data-ttu-id="5c9fd-121">例如:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-121">For example:</span></span>

* <span data-ttu-id="5c9fd-122">`mailto:`为自动创建链接`DataType.EmailAddress`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-122">The `mailto:` link is automatically created for `DataType.EmailAddress`.</span></span>
* <span data-ttu-id="5c9fd-123">为提供的日期选择器`DataType.Date`大多数浏览器中。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-123">The date selector is provided for `DataType.Date` in most browsers.</span></span>

<span data-ttu-id="5c9fd-124">`DataType`属性发出 HTML 5 `data-` HTML 5 浏览器使用的 (读作的数据 dash) 属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-124">The `DataType` attribute emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="5c9fd-125">`DataType`属性不提供验证。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-125">The `DataType` attributes don't provide validation.</span></span>

<span data-ttu-id="5c9fd-126">`DataType.Date`未指定的日期的显示格式。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-126">`DataType.Date` doesn't specify the format of the date that's displayed.</span></span> <span data-ttu-id="5c9fd-127">默认情况下，日期字段显示根据基于服务器的默认格式[CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-127">By default, the date field is displayed according to the default formats based on the server's [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support).</span></span>

<span data-ttu-id="5c9fd-128">`DisplayFormat` 特性用于显式指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-128">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

<span data-ttu-id="5c9fd-129">`ApplyFormatInEditMode`设置指定的格式设置也应该将应用到编辑 UI。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-129">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied to the edit UI.</span></span> <span data-ttu-id="5c9fd-130">某些字段不应使用`ApplyFormatInEditMode`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-130">Some fields shouldn't use `ApplyFormatInEditMode`.</span></span> <span data-ttu-id="5c9fd-131">例如，货币符号应通常不会显示在编辑文本框中。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-131">For example, the currency symbol should generally not be displayed in an edit text box.</span></span>

<span data-ttu-id="5c9fd-132">`DisplayFormat`属性可由本身。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-132">The `DisplayFormat` attribute can be used by itself.</span></span> <span data-ttu-id="5c9fd-133">它通常是使用一个好办法`DataType`特性与`DisplayFormat`属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-133">It's generally a good idea to use the `DataType` attribute with the `DisplayFormat` attribute.</span></span> <span data-ttu-id="5c9fd-134">`DataType`属性传达数据而不是如何在屏幕上呈现其的语义。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-134">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen.</span></span> <span data-ttu-id="5c9fd-135">`DataType`属性提供中均不提供了以下好处`DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-135">The `DataType` attribute provides the following benefits that are not available in `DisplayFormat`:</span></span>

* <span data-ttu-id="5c9fd-136">浏览器可以启用 HTML5 功能。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-136">The browser can enable HTML5 features.</span></span> <span data-ttu-id="5c9fd-137">例如，显示一个日历控件、 区域设置相对应的货币符号、 电子邮件链接，客户端进行输入的验证，等等。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-137">For example, show a calendar control, the locale-appropriate currency symbol, email links, client-side input validation, etc.</span></span>
* <span data-ttu-id="5c9fd-138">默认情况下，浏览器呈现使用基于的区域设置的正确格式的数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-138">By default, the browser renders data using the correct format based on the locale.</span></span>

<span data-ttu-id="5c9fd-139">有关详细信息，请参阅[\<输入 > 标记帮助器文档](xref:mvc/views/working-with-forms#the-input-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-139">For more information, see the [\<input> Tag Helper documentation](xref:mvc/views/working-with-forms#the-input-tag-helper).</span></span>

<span data-ttu-id="5c9fd-140">运行应用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-140">Run the app.</span></span> <span data-ttu-id="5c9fd-141">导航到学生索引页。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-141">Navigate to the Students Index page.</span></span> <span data-ttu-id="5c9fd-142">不再显示时间。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-142">Times are no longer displayed.</span></span> <span data-ttu-id="5c9fd-143">每个视图中使用`Student`模型显示无时间的日期。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-143">Every view that uses the `Student` model displays the date without time.</span></span>

![显示日期而无需时间的学生索引页](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a><span data-ttu-id="5c9fd-145">StringLength 属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-145">The StringLength attribute</span></span>

<span data-ttu-id="5c9fd-146">具有属性，可以指定数据验证规则和验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-146">Data validation rules and validation error messages can be specified with attributes.</span></span> <span data-ttu-id="5c9fd-147">[StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1)属性指定数据字段中允许的字符的最小和最大长度。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-147">The [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) attribute specifies the minimum and maximum length of characters that are allowed in a data field.</span></span> <span data-ttu-id="5c9fd-148">`StringLength`特性还提供对客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-148">The `StringLength` attribute also provides client-side and server-side validation.</span></span> <span data-ttu-id="5c9fd-149">最小值对数据库架构没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-149">The minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="5c9fd-150">更新`Student`模型替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-150">Update the `Student` model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

<span data-ttu-id="5c9fd-151">前面的代码限制为不超过 50 个字符的名称。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-151">The preceding code limits names to no more than 50 characters.</span></span> <span data-ttu-id="5c9fd-152">`StringLength`属性不会阻止用户从空白区域输入一个名称。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-152">The `StringLength` attribute doesn't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="5c9fd-153">[正则表达式](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1)特性用于将限制应用到的输入。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-153">The [RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) attribute is used to apply restrictions to the input.</span></span> <span data-ttu-id="5c9fd-154">例如，下面的代码要求的第一个字符是大写且其余的字符是按字母顺序排列：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-154">For example, the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]
```

<span data-ttu-id="5c9fd-155">运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-155">Run the app:</span></span>

* <span data-ttu-id="5c9fd-156">导航到学生页。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-156">Navigate to the Students page.</span></span>
* <span data-ttu-id="5c9fd-157">选择**新建**，并输入的名称超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-157">Select **Create New**, and enter a name longer than 50 characters.</span></span>
* <span data-ttu-id="5c9fd-158">选择**创建**，客户端验证显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-158">Select **Create**, client-side validation shows an error message.</span></span>

![学生索引页显示的字符串长度错误](complex-data-model/_static/string-length-errors.png)

<span data-ttu-id="5c9fd-160">在**SQL Server 对象资源管理器**(SSOX)，通过双击打开学生表设计器**学生**表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-160">In **SQL Server Object Explorer** (SSOX), open the Student table designer by double-clicking the **Student** table.</span></span>

![在 SSOX 中迁移前的学生表](complex-data-model/_static/ssox-before-migration.png)

<span data-ttu-id="5c9fd-162">上图显示的架构`Student`表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-162">The preceding image shows the schema for the `Student` table.</span></span> <span data-ttu-id="5c9fd-163">名称字段具有类型`nvarchar(MAX)`由于尚未在数据库上运行迁移。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-163">The name fields have type `nvarchar(MAX)` because migrations has not been run on the DB.</span></span> <span data-ttu-id="5c9fd-164">在本教程中稍后运行迁移时，名称字段将成为`nvarchar(50)`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-164">When migrations are run later in this tutorial, the name fields become `nvarchar(50)`.</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="5c9fd-165">列属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-165">The Column attribute</span></span>

<span data-ttu-id="5c9fd-166">属性可以控制如何类和属性映射到数据库。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-166">Attributes can control how classes and properties are mapped to the database.</span></span> <span data-ttu-id="5c9fd-167">在本部分中，`Column`属性用于将映射的名称`FirstMidName`属性设置为"FirstName"在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-167">In this section, the `Column` attribute is used to map the name of the `FirstMidName` property to "FirstName" in the DB.</span></span>

<span data-ttu-id="5c9fd-168">创建数据库后，将在模型上的属性名称用于列名称 (时除外`Column`属性，则使用)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-168">When the DB is created, property names on the model are used for column names (except when the `Column` attribute is used).</span></span>

<span data-ttu-id="5c9fd-169">`Student`模型使用`FirstMidName`的第一个名称字段，因为该字段还可能包含中间名。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-169">The `Student` model uses `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span>

<span data-ttu-id="5c9fd-170">更新*Student.cs*替换为以下突出显示代码文件：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-170">Update the *Student.cs* file with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

<span data-ttu-id="5c9fd-171">进行上述更改后，`Student.FirstMidName`在应用程序映射到`FirstName`列`Student`表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-171">With the preceding change, `Student.FirstMidName` in the app maps to the `FirstName` column of the `Student` table.</span></span>

<span data-ttu-id="5c9fd-172">添加`Column`属性将更改模型后备`SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-172">The addition of the `Column` attribute changes the model backing the `SchoolContext`.</span></span> <span data-ttu-id="5c9fd-173">模型后备`SchoolContext`不再与数据库相匹配。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-173">The model backing the `SchoolContext` no longer matches the database.</span></span> <span data-ttu-id="5c9fd-174">如果在应用迁移之前运行该应用，则会生成以下异常：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-174">If the app is run before applying migrations, the following exception is generated:</span></span>

```SQL
SqlException: Invalid column name 'FirstName'.
```
<span data-ttu-id="5c9fd-175">更新数据库：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-175">To update the DB:</span></span>

* <span data-ttu-id="5c9fd-176">生成项目。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-176">Build the project.</span></span>
* <span data-ttu-id="5c9fd-177">在项目文件夹中打开命令窗口。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-177">Open a command window in the project folder.</span></span> <span data-ttu-id="5c9fd-178">输入以下命令以创建新的迁移和更新数据库：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-178">Enter the following commands to create a new migration and update the DB:</span></span>

    ```console
    dotnet ef migrations add ColumnFirstName
    dotnet ef database update
    ```

<span data-ttu-id="5c9fd-179">`dotnet ef migrations add ColumnFirstName`命令将生成以下警告消息：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-179">The `dotnet ef migrations add ColumnFirstName` command generates the following warning message:</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

<span data-ttu-id="5c9fd-180">会生成警告，因为名称字段现在是限制为 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-180">The warning is generated because the name fields are now limited to 50 characters.</span></span> <span data-ttu-id="5c9fd-181">如果在数据库中的名称必须超过 50 个字符，到最后一个字符 51 将会丢失。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-181">If a name in the DB had more than 50 characters, the 51 to last character would be lost.</span></span>

* <span data-ttu-id="5c9fd-182">测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-182">Test the app.</span></span>

<span data-ttu-id="5c9fd-183">在 SSOX 中打开学生表：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-183">Open the Student table in SSOX:</span></span>

![在 SSOX 中后迁移的学生表](complex-data-model/_static/ssox-after-migration.png)

<span data-ttu-id="5c9fd-185">类型的迁移已应用之前，已名称列[nvarchar (max)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-185">Before migration was applied, the name columns were of type [nvarchar(MAX)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql).</span></span> <span data-ttu-id="5c9fd-186">名称列现`nvarchar(50)`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-186">The name columns are now `nvarchar(50)`.</span></span> <span data-ttu-id="5c9fd-187">列名称已更改，不再`FirstMidName`到`FirstName`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-187">The column name has changed from `FirstMidName` to `FirstName`.</span></span>

> [!Note]
> <span data-ttu-id="5c9fd-188">在以下部分中，某些阶段时生成的应用程序会生成编译器错误。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-188">In the following section, building the app at some stages generates compiler errors.</span></span> <span data-ttu-id="5c9fd-189">说明中指定何时生成该应用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-189">The instructions specify when to build the app.</span></span>

## <a name="student-entity-update"></a><span data-ttu-id="5c9fd-190">学生实体更新</span><span class="sxs-lookup"><span data-stu-id="5c9fd-190">Student entity update</span></span>

![学生实体](complex-data-model/_static/student-entity.png)

<span data-ttu-id="5c9fd-192">更新*Models/Student.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-192">Update *Models/Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a><span data-ttu-id="5c9fd-193">必需的特性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-193">The Required attribute</span></span>

<span data-ttu-id="5c9fd-194">`Required`特性使名称属性必填的字段。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-194">The `Required` attribute makes the name properties required fields.</span></span> <span data-ttu-id="5c9fd-195">`Required`属性不所需的不可为 null 的类型，如值类型 (`DateTime`， `int`，`double`等。)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-195">The `Required` attribute isn't needed for non-nullable types such as value types (`DateTime`, `int`, `double`, etc.).</span></span> <span data-ttu-id="5c9fd-196">不能为 null 的类型是自动被视为必填字段。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-196">Types that can't be null are automatically treated as required fields.</span></span>

<span data-ttu-id="5c9fd-197">`Required`属性无法替换中的最小长度参数`StringLength`属性：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-197">The `Required` attribute could be replaced with a minimum length parameter in the `StringLength` attribute:</span></span>

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a><span data-ttu-id="5c9fd-198">显示属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-198">The Display attribute</span></span>

<span data-ttu-id="5c9fd-199">`Display`属性指定文本框的标题应为"名字"、"姓氏"、"全名"和"注册日期"。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-199">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date."</span></span> <span data-ttu-id="5c9fd-200">默认标题不包含空格除以词，例如"Lastname。"</span><span class="sxs-lookup"><span data-stu-id="5c9fd-200">The default captions had no space dividing the words, for example "Lastname."</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="5c9fd-201">计算的 FullName 属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-201">The FullName calculated property</span></span>

<span data-ttu-id="5c9fd-202">`FullName`是返回一个值，通过串联两个其他属性创建一个计算的属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-202">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="5c9fd-203">`FullName`不能设置，它具有仅一个 get 访问器。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-203">`FullName` cannot be set, it has only a get accessor.</span></span> <span data-ttu-id="5c9fd-204">不`FullName`在数据库中创建列。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-204">No `FullName` column is created in the database.</span></span>

## <a name="create-the-instructor-entity"></a><span data-ttu-id="5c9fd-205">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-205">Create the Instructor Entity</span></span>

![Instructor 实体](complex-data-model/_static/instructor-entity.png)

<span data-ttu-id="5c9fd-207">创建*Models/Instructor.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-207">Create *Models/Instructor.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

<span data-ttu-id="5c9fd-208">请注意的几个属性都在相同`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-208">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="5c9fd-209">在更高版本在本系列中的实现继承教程中，此代码将重构以消除冗余。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-209">In the Implementing Inheritance tutorial later in this series, this code is refactored to eliminate the redundancy.</span></span>

<span data-ttu-id="5c9fd-210">多个属性可在一行上。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-210">Multiple attributes can be on one line.</span></span> <span data-ttu-id="5c9fd-211">`HireDate`属性可以进行编写，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-211">The `HireDate` attributes could be written as follows:</span></span>

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a><span data-ttu-id="5c9fd-212">CourseAssignments 和 OfficeAssignment 导航属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-212">The CourseAssignments and OfficeAssignment navigation properties</span></span>

<span data-ttu-id="5c9fd-213">`CourseAssignments`和`OfficeAssignment`属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-213">The `CourseAssignments` and `OfficeAssignment` properties are navigation properties.</span></span>

<span data-ttu-id="5c9fd-214">一个教师可以教授任意数量的课程，因此`CourseAssignments`定义为集合。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-214">An instructor can teach any number of courses, so `CourseAssignments` is defined as a collection.</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="5c9fd-215">如果导航属性包含多个实体：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-215">If a navigation property holds multiple entities:</span></span>

* <span data-ttu-id="5c9fd-216">它必须是列表类型，可以添加、 删除和更新条目。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-216">It must be a list type where the entries can be added, deleted, and updated.</span></span>

<span data-ttu-id="5c9fd-217">导航属性类型包括：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-217">Navigation property types include:</span></span>

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

<span data-ttu-id="5c9fd-218">如果`ICollection<T>`EF 核心创建的指定`HashSet<T>`默认情况下的集合。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-218">If `ICollection<T>` is specified, EF Core creates a `HashSet<T>` collection by default.</span></span>

<span data-ttu-id="5c9fd-219">`CourseAssignment`实体部分所述对多对多关系。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-219">The `CourseAssignment` entity is explained in the section on many-to-many relationships.</span></span>

<span data-ttu-id="5c9fd-220">Contoso 大学业务规则，一个教师可以有最多一个 office 的状态。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-220">Contoso University business rules state that an instructor can have at most one office.</span></span> <span data-ttu-id="5c9fd-221">`OfficeAssignment`属性包含单个`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-221">The `OfficeAssignment` property holds a single `OfficeAssignment` entity.</span></span> <span data-ttu-id="5c9fd-222">`OfficeAssignment`如果没有 office 分配，为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-222">`OfficeAssignment` is null if no office is assigned.</span></span>

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a><span data-ttu-id="5c9fd-223">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-223">Create the OfficeAssignment entity</span></span>

![OfficeAssignment 实体](complex-data-model/_static/officeassignment-entity.png)

<span data-ttu-id="5c9fd-225">创建*Models/OfficeAssignment.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-225">Create *Models/OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a><span data-ttu-id="5c9fd-226">键属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-226">The Key attribute</span></span>

<span data-ttu-id="5c9fd-227">`[Key]`属性用于标识属性作为的主键 (PK) 时的属性名称而非 classnameID 或 id。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-227">The `[Key]` attribute is used to identify a property as the primary key (PK) when the property name is something other than classnameID or ID.</span></span>

<span data-ttu-id="5c9fd-228">没有之间的对零或一一个关系`Instructor`和`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-228">There's a one-to-zero-or-one relationship between the `Instructor` and `OfficeAssignment` entities.</span></span> <span data-ttu-id="5c9fd-229">相对于分配给教师仅存在一个办公室分配。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-229">An office assignment only exists in relation to the instructor it's assigned to.</span></span> <span data-ttu-id="5c9fd-230">`OfficeAssignment` PK 是还其外键 (FK) 到`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-230">The `OfficeAssignment` PK is also its foreign key (FK) to the `Instructor` entity.</span></span> <span data-ttu-id="5c9fd-231">无法自动识别 EF 核心`InstructorID`作为的 PK`OfficeAssignment`因为：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-231">EF Core can't automatically recognize `InstructorID` as the PK of `OfficeAssignment` because:</span></span>

* <span data-ttu-id="5c9fd-232">`InstructorID`未遵循 ID 或 classnameID 命名约定。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-232">`InstructorID` doesn't follow the ID or classnameID naming convention.</span></span>

<span data-ttu-id="5c9fd-233">因此，`Key`属性用于标识`InstructorID`PK 作为：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-233">Therefore, the `Key` attribute is used to identify `InstructorID` as the PK:</span></span>

```csharp
[Key]
public int InstructorID { get; set; }
```

<span data-ttu-id="5c9fd-234">默认情况下，EF 核心将密钥视为非数据库生成因为列是标识关系。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-234">By default, EF Core treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="5c9fd-235">教师导航属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-235">The Instructor navigation property</span></span>

<span data-ttu-id="5c9fd-236">`OfficeAssignment`导航属性进行`Instructor`实体是可以为 null 因为：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-236">The `OfficeAssignment` navigation property for the `Instructor` entity is nullable because:</span></span>

* <span data-ttu-id="5c9fd-237">引用类型 （如类都可以为 null）。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-237">Reference types (such as classes are nullable).</span></span>
* <span data-ttu-id="5c9fd-238">一个教师可能没有一个办公室分配。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-238">An instructor might not have an office assignment.</span></span>


<span data-ttu-id="5c9fd-239">`OfficeAssignment`实体具有非 null`Instructor`导航属性因为：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-239">The `OfficeAssignment` entity has a non-nullable `Instructor` navigation property because:</span></span>

* <span data-ttu-id="5c9fd-240">`InstructorID`是不可为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-240">`InstructorID` is non-nullable.</span></span>
* <span data-ttu-id="5c9fd-241">一个办公室分配不存在一个教师不存在。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-241">An office assignment can't exist without an instructor.</span></span>

<span data-ttu-id="5c9fd-242">当`Instructor`实体具有相关`OfficeAssignment`实体，每个实体都有对另一个在其导航属性的引用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-242">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity has a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="5c9fd-243">`[Required]`特性可以应用到`Instructor`导航属性：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-243">The `[Required]` attribute could be applied to the `Instructor` navigation property:</span></span>

```csharp
[Required]
public Instructor Instructor { get; set; }
```

<span data-ttu-id="5c9fd-244">前面的代码指定必须是相关的教师。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-244">The preceding code specifies that there must be a related instructor.</span></span> <span data-ttu-id="5c9fd-245">前面的代码是不必要因为`InstructorID`外键 （它也是在 PK） 是不可为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-245">The preceding code is unnecessary because the `InstructorID` foreign key (which is also the PK) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="5c9fd-246">修改过程实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-246">Modify the Course Entity</span></span>

![课程实体](complex-data-model/_static/course-entity.png)

<span data-ttu-id="5c9fd-248">更新*Models/Course.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-248">Update *Models/Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

<span data-ttu-id="5c9fd-249">`Course`实体具有外键 (FK) 属性`DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-249">The `Course` entity has a foreign key (FK) property `DepartmentID`.</span></span> <span data-ttu-id="5c9fd-250">`DepartmentID`指向相关`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-250">`DepartmentID` points to the related `Department` entity.</span></span> <span data-ttu-id="5c9fd-251">`Course`实体具有`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-251">The `Course` entity has a `Department` navigation property.</span></span>

<span data-ttu-id="5c9fd-252">该模型具有相关实体的导航属性时，EF 核心不会为数据模型需要 FK 属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-252">EF Core doesn't require a FK property for a data model when the model has a navigation property for a related entity.</span></span>

<span data-ttu-id="5c9fd-253">EF 核心在任何位置在需要自动将 FKs 创建数据库中。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-253">EF Core automatically creates FKs in the database wherever they're needed.</span></span> <span data-ttu-id="5c9fd-254">EF 核心创建[隐藏属性](https://docs.microsoft.com/ef/core/modeling/shadow-properties)的自动创建 FKs。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-254">EF Core creates [shadow properties](https://docs.microsoft.com/ef/core/modeling/shadow-properties) for automatically created FKs.</span></span> <span data-ttu-id="5c9fd-255">更简单、 更高效，FK 采用数据模型可以进行更新。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-255">Having the FK in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="5c9fd-256">例如，考虑一个模型其中 FK 属性`DepartmentID`是*不*包含。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-256">For example, consider a model where the FK property `DepartmentID` is *not* included.</span></span> <span data-ttu-id="5c9fd-257">当过程实体被提取编辑：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-257">When a course entity is fetched to edit:</span></span>

* <span data-ttu-id="5c9fd-258">`Department`实体是未显式加载的情况下为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-258">The `Department` entity is null if it's not explicitly loaded.</span></span>
* <span data-ttu-id="5c9fd-259">若要更新过程实体，`Department`必须先提取实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-259">To update the course entity, the `Department` entity must first be fetched.</span></span>

<span data-ttu-id="5c9fd-260">当 FK 属性`DepartmentID`包含在数据模型中，没有必要提取`Department`之前更新的实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-260">When the FK property `DepartmentID` is included in the data model, there's no need to fetch the `Department` entity before an update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="5c9fd-261">DatabaseGenerated 属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-261">The DatabaseGenerated attribute</span></span>

<span data-ttu-id="5c9fd-262">`[DatabaseGenerated(DatabaseGeneratedOption.None)]`属性指定在 PK 是应用程序提供而不是由数据库生成。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-262">The `[DatabaseGenerated(DatabaseGeneratedOption.None)]` attribute specifies that the PK is provided by the application rather than generated by the database.</span></span>

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

<span data-ttu-id="5c9fd-263">默认情况下，EF 核心假定 PK 值都由数据库。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-263">By default, EF Core assumes that PK values are generated by the DB.</span></span> <span data-ttu-id="5c9fd-264">DB 生成 PK 值通常是最佳的方法。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-264">DB generated PK values is generally the best approach.</span></span> <span data-ttu-id="5c9fd-265">有关`Course`实体，用户指定 PK.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-265">For `Course` entities, the user specifies the PK.</span></span> <span data-ttu-id="5c9fd-266">例如，如数学部门的 1000年系列值，则将英语部门 2000年系列课程数。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-266">For example, a course number such as a 1000 series for the math department, a 2000 series for the English department.</span></span>

<span data-ttu-id="5c9fd-267">`DatabaseGenerated`属性还可以用于生成默认值。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-267">The `DatabaseGenerated` attribute can also be used to generate default values.</span></span> <span data-ttu-id="5c9fd-268">例如，数据库可以自动生成要记录的创建或更新行的日期的日期字段。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-268">For example, the DB can automatically generate a date field to record the date a row was created or updated.</span></span> <span data-ttu-id="5c9fd-269">有关详细信息，请参阅[生成属性](https://docs.microsoft.com/ef/core/modeling/generated-properties)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-269">For more information, see [Generated Properties](https://docs.microsoft.com/ef/core/modeling/generated-properties).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="5c9fd-270">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-270">Foreign key and navigation properties</span></span>

<span data-ttu-id="5c9fd-271">外键 (FK) 属性和中的导航属性`Course`实体反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-271">The foreign key (FK) properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

<span data-ttu-id="5c9fd-272">课程都将分配到一个部门，因此没有`DepartmentID`FK 和`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-272">A course is assigned to one department, so there's a `DepartmentID` FK and a `Department` navigation property.</span></span>

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

<span data-ttu-id="5c9fd-273">课程可以有任意数量的学生注册，因此`Enrollments`导航属性是集合：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-273">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

<span data-ttu-id="5c9fd-274">可能由多个教师讲授课程因此`CourseAssignments`导航属性是集合：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-274">A course may be taught by multiple instructors, so the `CourseAssignments` navigation property is a collection:</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="5c9fd-275">`CourseAssignment`解释了[更高版本](#many-to-many-relationships)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-275">`CourseAssignment` is explained [later](#many-to-many-relationships).</span></span>

## <a name="create-the-department-entity"></a><span data-ttu-id="5c9fd-276">创建部门实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-276">Create the Department entity</span></span>

![部门实体](complex-data-model/_static/department-entity.png)

<span data-ttu-id="5c9fd-278">创建*Models/Department.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-278">Create *Models/Department.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a><span data-ttu-id="5c9fd-279">列属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-279">The Column attribute</span></span>

<span data-ttu-id="5c9fd-280">以前`Column`属性用于更改列名称映射。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-280">Previously the `Column` attribute was used to change column name mapping.</span></span> <span data-ttu-id="5c9fd-281">中的代码`Department`实体，`Column`属性用于更改 SQL 数据类型映射。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-281">In the code for the `Department` entity, the `Column` attribute is used to change SQL data type mapping.</span></span> <span data-ttu-id="5c9fd-282">`Budget` DB 中使用 SQL Server money 类型定义列：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-282">The `Budget` column is defined using the SQL Server money type in the DB:</span></span>

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

<span data-ttu-id="5c9fd-283">列映射则通常不需要。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-283">Column mapping is generally not required.</span></span> <span data-ttu-id="5c9fd-284">EF 核心通常选择基于属性的 CLR 类型的相应 SQL Server 数据类型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-284">EF Core generally chooses the appropriate SQL Server data type based on the CLR type for the property.</span></span> <span data-ttu-id="5c9fd-285">CLR`decimal`类型映射到 SQL Server`decimal`类型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-285">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="5c9fd-286">`Budget`为货币，是更适合于货币 money 数据类型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-286">`Budget` is for currency, and the money data type is more appropriate for currency.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="5c9fd-287">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-287">Foreign key and navigation properties</span></span>

<span data-ttu-id="5c9fd-288">FK 和导航属性反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-288">The FK and navigation properties reflect the following relationships:</span></span>

* <span data-ttu-id="5c9fd-289">部门可能或可能没有管理员。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-289">A department may or may not have an administrator.</span></span>
* <span data-ttu-id="5c9fd-290">管理员始终是一个教师。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-290">An administrator is always an instructor.</span></span> <span data-ttu-id="5c9fd-291">因此`InstructorID`属性是作为到 FK 包含`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-291">Therefore the `InstructorID` property is included as the FK to the `Instructor` entity.</span></span>

<span data-ttu-id="5c9fd-292">导航属性名为`Administrator`但保留`Instructor`实体：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-292">The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

<span data-ttu-id="5c9fd-293">在前面的代码问号 （？） 指定属性可以为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-293">The question mark (?) in the preceding code specifies the property is nullable.</span></span>

<span data-ttu-id="5c9fd-294">部门可能会产生许多课程，因此课程导航属性：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-294">A department may have many courses, so there's a Courses navigation property:</span></span>

```csharp
public ICollection<Course> Courses { get; set; }
```

<span data-ttu-id="5c9fd-295">注意： 按照约定，EF 核心使级联删除对于不可为 null FKs 以及多对多关系。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-295">Note: By convention, EF Core enables cascade delete for non-nullable FKs and for many-to-many relationships.</span></span> <span data-ttu-id="5c9fd-296">级联 delete 可能会导致循环的级联删除规则。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-296">Cascading delete can result in circular cascade delete rules.</span></span> <span data-ttu-id="5c9fd-297">循环的级联删除规则原因添加迁移时，此异常。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-297">Circular cascade delete rules causes an exception when a migration is added.</span></span>

<span data-ttu-id="5c9fd-298">例如，如果`Department.InstructorID`属性未定义为可以为 null:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-298">For example, if the `Department.InstructorID` property wasn't defined as nullable:</span></span>

* <span data-ttu-id="5c9fd-299">EF 核心配置一个级联删除规则，以删除部门时删除教师。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-299">EF Core configures a cascade delete rule to delete the instructor when the department is deleted.</span></span>
* <span data-ttu-id="5c9fd-300">删除部门时删除教师不的预期的行为。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-300">Deleting the instructor when the department is deleted isn't the intended behavior.</span></span>

<span data-ttu-id="5c9fd-301">如果业务规则需要`InstructorID`属性为不可为 null，请使用以下 fluent API 语句：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-301">If business rules required the `InstructorID` property be non-nullable, use the following fluent API statement:</span></span>

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

<span data-ttu-id="5c9fd-302">前面的代码中禁用部门教师关系上的级联删除。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-302">The preceding code disables cascade delete on the department-instructor relationship.</span></span>

## <a name="update-the-enrollment-entity"></a><span data-ttu-id="5c9fd-303">更新注册实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-303">Update the Enrollment entity</span></span>

<span data-ttu-id="5c9fd-304">注册记录适用于一个执行的一名学生课程。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-304">An enrollment record is for a one course taken by one student.</span></span>

![注册实体](complex-data-model/_static/enrollment-entity.png)

<span data-ttu-id="5c9fd-306">更新*Models/Enrollment.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-306">Update *Models/Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="5c9fd-307">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="5c9fd-307">Foreign key and navigation properties</span></span>

<span data-ttu-id="5c9fd-308">FK 属性和导航属性反映了以下关系：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-308">The FK properties and navigation properties reflect the following relationships:</span></span>

<span data-ttu-id="5c9fd-309">注册记录为一个过程中，因此`CourseID`FK 属性和`Course`导航属性：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-309">An enrollment record is for one course, so there's a `CourseID` FK property and a `Course` navigation property:</span></span>

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

<span data-ttu-id="5c9fd-310">注册记录是一名学生的因此`StudentID`FK 属性和`Student`导航属性：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-310">An enrollment record is for one student, so there's a `StudentID` FK property and a `Student` navigation property:</span></span>

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a><span data-ttu-id="5c9fd-311">多对多关系</span><span class="sxs-lookup"><span data-stu-id="5c9fd-311">Many-to-Many Relationships</span></span>

<span data-ttu-id="5c9fd-312">没有之间的多对多关系`Student`和`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-312">There's a many-to-many relationship between the `Student` and `Course` entities.</span></span> <span data-ttu-id="5c9fd-313">`Enrollment`实体充当多对多联接表*具有负载*数据库中。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-313">The `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="5c9fd-314">"使用负载"意味着`Enrollment`表包含更多数据除了 FKs 联接的表 (在此情况下，在 PK 和`Grade`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-314">"With payload" means that the `Enrollment` table contains additional data besides FKs for the joined tables (in this case, the PK and `Grade`).</span></span>

<span data-ttu-id="5c9fd-315">下图显示这些关系中的实体关系图的外观。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-315">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="5c9fd-316">(此关系图生成使用 EF Power Tools for EF 6.x。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-316">(This diagram was generated using EF Power Tools for EF 6.x.</span></span> <span data-ttu-id="5c9fd-317">创建关系图并不在本教程的一部分。）</span><span class="sxs-lookup"><span data-stu-id="5c9fd-317">Creating the diagram isn't part of the tutorial.)</span></span>

![学生课程多对多关系](complex-data-model/_static/student-course.png)

<span data-ttu-id="5c9fd-319">每个关系行已在其他，，指示一个对多关系一端和星号 （\*） 1。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-319">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="5c9fd-320">如果`Enrollment`表没有包括年级信息，它只需包含两个 FKs (`CourseID`和`StudentID`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-320">If the `Enrollment` table didn't include grade information, it would only need to contain the two FKs (`CourseID` and `StudentID`).</span></span> <span data-ttu-id="5c9fd-321">没有负载的多对多联接表有时称为纯联接表 (PJT)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-321">A many-to-many join table without payload is sometimes called a pure join table (PJT).</span></span>

<span data-ttu-id="5c9fd-322">`Instructor`和`Course`实体具有使用纯联接表的多对多关系。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-322">The `Instructor` and `Course` entities have a many-to-many relationship using a pure join table.</span></span>

<span data-ttu-id="5c9fd-323">注意： EF 6.x 支持隐式联接表的多对多关系，但 EF 核心不会。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-323">Note: EF 6.x supports implicit join tables for many-to-many relationships, but EF Core doesn't.</span></span> <span data-ttu-id="5c9fd-324">有关详细信息，请参阅[多对多关系在 EF 核心 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-324">For more information, see [Many-to-many relationships in EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).</span></span>

## <a name="the-courseassignment-entity"></a><span data-ttu-id="5c9fd-325">CourseAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-325">The CourseAssignment entity</span></span>

![CourseAssignment 实体](complex-data-model/_static/courseassignment-entity.png)

<span data-ttu-id="5c9fd-327">创建*Models/CourseAssignment.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-327">Create *Models/CourseAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a><span data-ttu-id="5c9fd-328">教师课程</span><span class="sxs-lookup"><span data-stu-id="5c9fd-328">Instructor-to-Courses</span></span>

![教师课程多对多](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="5c9fd-330">教师课程多对多关系：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-330">The Instructor-to-Courses many-to-many relationship:</span></span>

* <span data-ttu-id="5c9fd-331">要求必须由一个实体集表示一个联接表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-331">Requires a join table that must be represented by an entity set.</span></span>
* <span data-ttu-id="5c9fd-332">是纯联接表 （表而无需负载）。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-332">Is a pure join table (table without payload).</span></span>

<span data-ttu-id="5c9fd-333">很普遍命名联接实体`EntityName1EntityName2`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-333">It's common to name a join entity `EntityName1EntityName2`.</span></span> <span data-ttu-id="5c9fd-334">例如，使用此模式对教师课程联接表是`CourseInstructor`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-334">For example, the Instructor-to-Courses join table using this pattern is `CourseInstructor`.</span></span> <span data-ttu-id="5c9fd-335">但是，我们建议使用描述的关系的名称。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-335">However, we recommend using a name that describes the relationship.</span></span>

<span data-ttu-id="5c9fd-336">数据模型按简单启动和增长。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-336">Data models start out simple and grow.</span></span> <span data-ttu-id="5c9fd-337">否负载联接 (PJTs) 经常发展以包括负载。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-337">No-payload joins (PJTs) frequently evolve to include payload.</span></span> <span data-ttu-id="5c9fd-338">通过启动具有描述性的实体名称，名称不需要联接表发生更改时更改。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-338">By starting with a descriptive entity name, the name doesn't need to change when the join table changes.</span></span> <span data-ttu-id="5c9fd-339">理想情况下，联接实体将业务域中具有其自己自然的 （可能是单个单词） 名称。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-339">Ideally, the join entity would have its own natural (possibly single word) name in the business domain.</span></span> <span data-ttu-id="5c9fd-340">例如，无法与联接实体调用分级链接丛书和客户。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-340">For example, Books and Customers could be linked with a join entity called Ratings.</span></span> <span data-ttu-id="5c9fd-341">对于教师课程多对多关系，`CourseAssignment`是优于`CourseInstructor`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-341">For the Instructor-to-Courses many-to-many relationship, `CourseAssignment` is preferred over `CourseInstructor`.</span></span>

### <a name="composite-key"></a><span data-ttu-id="5c9fd-342">复合密钥</span><span class="sxs-lookup"><span data-stu-id="5c9fd-342">Composite key</span></span>

<span data-ttu-id="5c9fd-343">FKs 不可以为 null。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-343">FKs are not nullable.</span></span> <span data-ttu-id="5c9fd-344">在两个 FKs `CourseAssignment` (`InstructorID`和`CourseID`) 一起唯一标识的每一行`CourseAssignment`表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-344">The two FKs in `CourseAssignment` (`InstructorID` and `CourseID`) together uniquely identify each row of the `CourseAssignment` table.</span></span> <span data-ttu-id="5c9fd-345">`CourseAssignment`不需要专用的 PK.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-345">`CourseAssignment` doesn't require a dedicated PK.</span></span> <span data-ttu-id="5c9fd-346">`InstructorID`和`CourseID`属性用作复合 PK.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-346">The `InstructorID` and `CourseID` properties function as a composite PK.</span></span> <span data-ttu-id="5c9fd-347">若要指定到 EF 核心的复合 Pk 的唯一方法是使用*fluent API*。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-347">The only way to specify composite PKs to EF Core is with the *fluent API*.</span></span> <span data-ttu-id="5c9fd-348">下一节演示如何配置复合 PK.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-348">The next section shows how to configure the composite PK.</span></span>

<span data-ttu-id="5c9fd-349">复合密钥可确保：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-349">The composite key ensures:</span></span>

* <span data-ttu-id="5c9fd-350">一个课程允许多个行。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-350">Multiple rows are allowed for one course.</span></span>
* <span data-ttu-id="5c9fd-351">一个教师允许多个行。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-351">Multiple rows are allowed for one instructor.</span></span>
* <span data-ttu-id="5c9fd-352">不允许为相同的教师和过程的多个行。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-352">Multiple rows for the same instructor and course isn't allowed.</span></span>

<span data-ttu-id="5c9fd-353">`Enrollment`联接实体定义其自己的主键，因此可能会出现这种重复项。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-353">The `Enrollment` join entity defines its own PK, so duplicates of this sort are possible.</span></span> <span data-ttu-id="5c9fd-354">若要防止此类重复：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-354">To prevent such duplicates:</span></span>

* <span data-ttu-id="5c9fd-355">上的 FK 字段中，添加一个唯一索引或</span><span class="sxs-lookup"><span data-stu-id="5c9fd-355">Add a unique index on the FK fields, or</span></span>
* <span data-ttu-id="5c9fd-356">配置`Enrollment`带有复合主键类似于`CourseAssignment`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-356">Configure `Enrollment` with a primary composite key similar to `CourseAssignment`.</span></span> <span data-ttu-id="5c9fd-357">有关详细信息，请参阅[索引](https://docs.microsoft.com/ef/core/modeling/indexes)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-357">For more information, see [Indexes](https://docs.microsoft.com/ef/core/modeling/indexes).</span></span>

## <a name="update-the-db-context"></a><span data-ttu-id="5c9fd-358">更新数据库上下文</span><span class="sxs-lookup"><span data-stu-id="5c9fd-358">Update the DB context</span></span>

<span data-ttu-id="5c9fd-359">添加以下突出显示的代码*Data/SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-359">Add the following highlighted code to *Data/SchoolContext.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

<span data-ttu-id="5c9fd-360">前面的代码中添加新的实体，并配置`CourseAssignment`实体的复合 PK.</span><span class="sxs-lookup"><span data-stu-id="5c9fd-360">The preceding code adds the new entities and configures the `CourseAssignment` entity's composite PK.</span></span>

## <a name="fluent-api-alternative-to-attributes"></a><span data-ttu-id="5c9fd-361">属性 fluent API 替代方法</span><span class="sxs-lookup"><span data-stu-id="5c9fd-361">Fluent API alternative to attributes</span></span>

<span data-ttu-id="5c9fd-362">`OnModelCreating`方法在前面的代码使用*fluent API*配置 EF 核心行为。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-362">The `OnModelCreating` method in the preceding code uses the *fluent API* to configure EF Core behavior.</span></span> <span data-ttu-id="5c9fd-363">API 称为"fluent"，因为它通常用于通过连接一系列组合在一起成为单个语句的方法调用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-363">The API is called "fluent" because it's often used by stringing a series of method calls together into a single statement.</span></span> <span data-ttu-id="5c9fd-364">[下面的代码](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)是 fluent API 的示例：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-364">The [following code](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) is an example of the fluent API:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

<span data-ttu-id="5c9fd-365">在本教程中，仅为不能具有属性完成的 DB 映射使用 fluent API。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-365">In this tutorial, the fluent API is used only for DB mapping that can't be done with attributes.</span></span> <span data-ttu-id="5c9fd-366">但是，fluent API 可以指定的格式、 验证和可通过属性的映射规则的大多数。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-366">However, the fluent API can specify most of the formatting, validation, and mapping rules that can be done with attributes.</span></span>

<span data-ttu-id="5c9fd-367">某些属性，如`MinimumLength`不能使用 fluent API 应用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-367">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="5c9fd-368">`MinimumLength`不会更改架构，它仅适用于最小长度验证规则。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-368">`MinimumLength` doesn't change the schema, it only applies a minimum length validation rule.</span></span>

<span data-ttu-id="5c9fd-369">一些开发人员更愿意使用 fluent API 以独占方式，以便它们能够获得它们的实体类"清理"。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-369">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="5c9fd-370">可以混合属性和 fluent API。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-370">Attributes and the fluent API can be mixed.</span></span> <span data-ttu-id="5c9fd-371">有一些可仅可通过 fluent API （在指定组合主键） 的配置。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-371">There are some configurations that can only be done with the fluent API (specifying a composite PK).</span></span> <span data-ttu-id="5c9fd-372">有一些只能具有属性的配置 (`MinimumLength`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-372">There are some configurations that can only be done with attributes (`MinimumLength`).</span></span> <span data-ttu-id="5c9fd-373">使用 fluent API 或属性的建议的做法：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-373">The recommended practice for using fluent API or attributes:</span></span>

* <span data-ttu-id="5c9fd-374">选择这两种方法之一。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-374">Choose one of these two approaches.</span></span>
* <span data-ttu-id="5c9fd-375">使用一致地尽可能多选的方法。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-375">Use the chosen approach consistently as much as possible.</span></span>

<span data-ttu-id="5c9fd-376">某些特性在此教程适用于：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-376">Some of the attributes used in the this tutorial are used for:</span></span>

* <span data-ttu-id="5c9fd-377">仅验证 (例如， `MinimumLength`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-377">Validation only (for example, `MinimumLength`).</span></span>
* <span data-ttu-id="5c9fd-378">EF 核心配置 (例如， `HasKey`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-378">EF Core configuration only (for example, `HasKey`).</span></span>
* <span data-ttu-id="5c9fd-379">验证和 EF 核心配置 (例如， `[StringLength(50)]`)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-379">Validation and EF Core configuration (for example, `[StringLength(50)]`).</span></span>

<span data-ttu-id="5c9fd-380">有关与 fluent API 的特性的详细信息，请参阅[方法配置](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-380">For more information about attributes vs. fluent API, see [Methods of configuration](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration).</span></span>

## <a name="entity-diagram-showing-relationships"></a><span data-ttu-id="5c9fd-381">关系图显示关系的实体</span><span class="sxs-lookup"><span data-stu-id="5c9fd-381">Entity Diagram Showing Relationships</span></span>

<span data-ttu-id="5c9fd-382">下图显示关系图用于 EF Power Tools 创建的已完成的 School 模型。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-382">The following illustration shows the diagram that EF Power Tools create for the completed School model.</span></span>

![实体关系图](complex-data-model/_static/diagram.png)

<span data-ttu-id="5c9fd-384">上图中显示：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-384">The preceding diagram shows:</span></span>

* <span data-ttu-id="5c9fd-385">一个对多关系的多个行 (1 到\*)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-385">Several one-to-many relationship lines (1 to \*).</span></span>
* <span data-ttu-id="5c9fd-386">对零或一一个关系行 (1 对 0..1) 之间`Instructor`和`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-386">The one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities.</span></span>
* <span data-ttu-id="5c9fd-387">零-或--一对多关系行 (0..1 对 \*) 之间`Instructor`和`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-387">The zero-or-one-to-many relationship line (0..1 to \*) between the `Instructor` and `Department` entities.</span></span>

## <a name="seed-the-db-with-test-data"></a><span data-ttu-id="5c9fd-388">种子使用测试数据的数据库</span><span class="sxs-lookup"><span data-stu-id="5c9fd-388">Seed the DB with Test Data</span></span>

<span data-ttu-id="5c9fd-389">更新中的代码*Data/DbInitializer.cs*:</span><span class="sxs-lookup"><span data-stu-id="5c9fd-389">Update the code in *Data/DbInitializer.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

<span data-ttu-id="5c9fd-390">前面的代码中为新实体提供了种子数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-390">The preceding code provides seed data for the new entities.</span></span> <span data-ttu-id="5c9fd-391">大多数的此代码创建新的实体对象，并加载示例数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-391">Most of this code creates new entity objects and loads sample data.</span></span> <span data-ttu-id="5c9fd-392">示例数据用于测试。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-392">The sample data is used for testing.</span></span> <span data-ttu-id="5c9fd-393">前面的代码将创建以下多对多关系：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-393">The preceding code creates the following many-to-many relationships:</span></span>

* `Enrollments`
* `CourseAssignment`

<span data-ttu-id="5c9fd-394">注意： [EF 核心 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap)将支持[数据种子设定](https://github.com/aspnet/EntityFrameworkCore/issues/629)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-394">Note: [EF Core 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) will support [data seeding](https://github.com/aspnet/EntityFrameworkCore/issues/629).</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="5c9fd-395">添加迁移</span><span class="sxs-lookup"><span data-stu-id="5c9fd-395">Add a migration</span></span>

<span data-ttu-id="5c9fd-396">生成项目。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-396">Build the project.</span></span> <span data-ttu-id="5c9fd-397">在项目文件夹中打开命令窗口并输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-397">Open a command window in the project folder and enter the following command:</span></span>

```console
dotnet ef migrations add ComplexDataModel
```

<span data-ttu-id="5c9fd-398">前一个命令显示有关可能造成数据丢失的警告。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-398">The preceding command displays a warning about possible data loss.</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="5c9fd-399">如果`database update`运行命令，则会生成以下错误：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-399">If the `database update` command is run, the following error is produced:</span></span>

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

<span data-ttu-id="5c9fd-400">迁移运行时与现有数据，可能有不能满足与正在退出的数据的 FK 约束。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-400">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="5c9fd-401">对于本教程中，创建新数据库，因此没有任何 FK 约束冲突。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-401">For this tutorial, a new DB is created, so there are no FK constraint violations.</span></span> <span data-ttu-id="5c9fd-402">请参阅[修复与旧的数据的外键约束](#fk)有关如何解决 FK 冲突在当前数据库上的说明。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-402">See [Fixing foreign key constraints with legacy data](#fk) for instructions on how to fix the FK violations on the current DB.</span></span>

## <a name="change-the-connection-string-and-update-the-db"></a><span data-ttu-id="5c9fd-403">更改连接字符串并更新数据库</span><span class="sxs-lookup"><span data-stu-id="5c9fd-403">Change the connection string and update the DB</span></span>

<span data-ttu-id="5c9fd-404">中已更新的代码`DbInitializer`添加新的实体的种子数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-404">The code in the updated `DbInitializer` adds seed data for the new entities.</span></span> <span data-ttu-id="5c9fd-405">若要强制 EF 核心以创建新的空数据库：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-405">To force EF Core to create a new empty DB:</span></span>

* <span data-ttu-id="5c9fd-406">更改中的数据库连接字符串名称*appsettings.json*到 ContosoUniversity3。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-406">Change the DB connection string name in *appsettings.json* to ContosoUniversity3.</span></span> <span data-ttu-id="5c9fd-407">新名称必须是未在计算机已使用的名称。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-407">The new name must be a name that hasn't been used on the computer.</span></span>

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
      },
    ```

* <span data-ttu-id="5c9fd-408">或者，删除数据库使用：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-408">Alternatively, delete the DB using:</span></span>

    * <span data-ttu-id="5c9fd-409">**SQL Server 对象资源管理器**(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-409">**SQL Server Object Explorer** (SSOX).</span></span>
    * <span data-ttu-id="5c9fd-410">`database drop` CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-410">The `database drop` CLI command:</span></span>

   ```console
   dotnet ef database drop
   ```

<span data-ttu-id="5c9fd-411">运行`database update`命令窗口中：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-411">Run `database update` in the command window:</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="5c9fd-412">前一个命令运行所有迁移。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-412">The preceding command runs all the migrations.</span></span>

<span data-ttu-id="5c9fd-413">运行应用。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-413">Run the app.</span></span> <span data-ttu-id="5c9fd-414">运行应用程序运行`DbInitializer.Initialize`方法。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-414">Running the app runs the `DbInitializer.Initialize` method.</span></span> <span data-ttu-id="5c9fd-415">`DbInitializer.Initialize`填充新数据库。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-415">The `DbInitializer.Initialize` populates the new DB.</span></span>

<span data-ttu-id="5c9fd-416">在 SSOX 中打开数据库：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-416">Open the DB in SSOX:</span></span>

* <span data-ttu-id="5c9fd-417">展开**表**节点。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-417">Expand the **Tables** node.</span></span> <span data-ttu-id="5c9fd-418">显示创建的表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-418">The created tables are displayed.</span></span>
* <span data-ttu-id="5c9fd-419">如果 SSOX 以前已打开，请单击**刷新**按钮。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-419">If SSOX was opened previously, click the **Refresh** button.</span></span>

![在 SSOX 中的表](complex-data-model/_static/ssox-tables.png)

<span data-ttu-id="5c9fd-421">检查**CourseAssignment**表：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-421">Examine the **CourseAssignment** table:</span></span>

* <span data-ttu-id="5c9fd-422">右键单击**CourseAssignment**表，然后选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-422">Right-click the **CourseAssignment** table and select **View Data**.</span></span>
* <span data-ttu-id="5c9fd-423">验证**CourseAssignment**表包含数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-423">Verify the **CourseAssignment** table contains data.</span></span>

![在 SSOX 中 CourseAssignment 数据](complex-data-model/_static/ssox-ci-data.png)

<a name="fk"></a>

## <a name="fixing-foreign-key-constraints-with-legacy-data"></a><span data-ttu-id="5c9fd-425">与旧数据修复外键约束</span><span class="sxs-lookup"><span data-stu-id="5c9fd-425">Fixing foreign key constraints with legacy data</span></span>

<span data-ttu-id="5c9fd-426">本部分是可选的。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-426">This section is optional.</span></span>

<span data-ttu-id="5c9fd-427">迁移运行时与现有数据，可能有不能满足与正在退出的数据的 FK 约束。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-427">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="5c9fd-428">使用生产数据，必须采取步骤来将现有数据迁移。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-428">With production data, steps must be taken to migrate the existing data.</span></span> <span data-ttu-id="5c9fd-429">本部分提供修复 FK 约束冲突的一个示例。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-429">This section provides an example of fixing FK constraint violations.</span></span> <span data-ttu-id="5c9fd-430">不进行不备份这些代码更改。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-430">Don't make these code changes without a backup.</span></span> <span data-ttu-id="5c9fd-431">不进行这些代码更改，如果在完成上一节，并更新数据库。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-431">Don't make these code changes if you completed the previous section and updated the database.</span></span>

<span data-ttu-id="5c9fd-432">*{Timestamp}_ComplexDataModel.cs*文件包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-432">The *{timestamp}_ComplexDataModel.cs* file contains the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

<span data-ttu-id="5c9fd-433">前面的代码将添加不可为 null`DepartmentID`到 FK`Course`表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-433">The preceding code adds a non-nullable `DepartmentID` FK to the `Course` table.</span></span> <span data-ttu-id="5c9fd-434">从以前的教程，DB 包含中的行`Course`，因此无法迁移通过更新该表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-434">The DB from the previous tutorial contains rows in `Course`, so that table cannot be updated by migrations.</span></span>

<span data-ttu-id="5c9fd-435">若要使`ComplexDataModel`使用现有数据迁移工作：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-435">To make the `ComplexDataModel` migration work with existing data:</span></span>

* <span data-ttu-id="5c9fd-436">更改代码以提供新的列 (`DepartmentID`) 默认值。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-436">Change the code to give the new column (`DepartmentID`) a default value.</span></span>
* <span data-ttu-id="5c9fd-437">创建名为"Temp"使其作为默认部门的假部门。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-437">Create a fake department named "Temp" to act as the default department.</span></span>

### <a name="fix-the-foreign-key-constraints"></a><span data-ttu-id="5c9fd-438">修复外键约束</span><span class="sxs-lookup"><span data-stu-id="5c9fd-438">Fix the foreign key constraints</span></span>

<span data-ttu-id="5c9fd-439">更新`ComplexDataModel`类`Up`方法：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-439">Update the `ComplexDataModel` classes `Up` method:</span></span>

* <span data-ttu-id="5c9fd-440">打开*{timestamp}_ComplexDataModel.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-440">Open the *{timestamp}_ComplexDataModel.cs* file.</span></span>
* <span data-ttu-id="5c9fd-441">注释掉的添加的代码行`DepartmentID`列`Course`表。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-441">Comment out the line of code that adds the `DepartmentID` column to the `Course` table.</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

<span data-ttu-id="5c9fd-442">添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-442">Add the following highlighted code.</span></span> <span data-ttu-id="5c9fd-443">新的代码会进入后`.CreateTable( name: "Department"`块：[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span><span class="sxs-lookup"><span data-stu-id="5c9fd-443">The new code goes after the `.CreateTable( name: "Department"` block: [!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span></span>

<span data-ttu-id="5c9fd-444">与前面的更改，现有`Course`将与"Temp"部门后相关行`ComplexDataModel``Up`方法运行。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-444">With the preceding changes, existing `Course` rows will be related to the "Temp" department after the `ComplexDataModel` `Up` method runs.</span></span>

<span data-ttu-id="5c9fd-445">生产应用，则应该：</span><span class="sxs-lookup"><span data-stu-id="5c9fd-445">A production app would:</span></span>

* <span data-ttu-id="5c9fd-446">包括代码或脚本添加`Department`行以及相关`Course`对新的行`Department`行。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-446">Include code or scripts to add `Department` rows and related `Course` rows to the new `Department` rows.</span></span>
* <span data-ttu-id="5c9fd-447">使用"Temp"部门或的默认值为`Course.DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-447">Not use the "Temp" department or the default value for `Course.DepartmentID`.</span></span>

<span data-ttu-id="5c9fd-448">下一步教程介绍如何相关的数据。</span><span class="sxs-lookup"><span data-stu-id="5c9fd-448">The next tutorial covers related data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="5c9fd-449">[上一页](xref:data/ef-rp/migrations)
[下一页](xref:data/ef-rp/read-related-data)</span><span class="sxs-lookup"><span data-stu-id="5c9fd-449">[Previous](xref:data/ef-rp/migrations)
[Next](xref:data/ef-rp/read-related-data)</span></span>
