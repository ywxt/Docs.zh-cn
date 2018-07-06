---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 更新、 删除和创建数据与模型绑定和 web 窗体 |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 1cf9873db177b67927b579def1eedd08e3e9a762
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821627"
---
<a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="9bfba-104">更新、 删除和创建数据与模型绑定和 web 窗体</span><span class="sxs-lookup"><span data-stu-id="9bfba-104">Updating, deleting, and creating data with model binding and web forms</span></span>
====================
<span data-ttu-id="9bfba-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9bfba-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9bfba-106">本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。</span><span class="sxs-lookup"><span data-stu-id="9bfba-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="9bfba-107">模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。</span><span class="sxs-lookup"><span data-stu-id="9bfba-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="9bfba-108">本系列开始介绍性材料，后续教程将移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="9bfba-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="9bfba-109">本教程演示如何创建、 更新和删除与模型绑定的数据。</span><span class="sxs-lookup"><span data-stu-id="9bfba-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="9bfba-110">您将设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="9bfba-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="9bfba-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="9bfba-111">DeleteMethod</span></span>
> - <span data-ttu-id="9bfba-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="9bfba-112">InsertMethod</span></span>
> - <span data-ttu-id="9bfba-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="9bfba-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="9bfba-114">这些属性接收处理相应的操作的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="9bfba-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="9bfba-115">在该方法中，你提供的逻辑与数据进行交互。</span><span class="sxs-lookup"><span data-stu-id="9bfba-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="9bfba-116">本教程基于第一个中创建的项目[一部分](retrieving-data.md)在本系列。</span><span class="sxs-lookup"><span data-stu-id="9bfba-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="9bfba-117">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。</span><span class="sxs-lookup"><span data-stu-id="9bfba-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="9bfba-118">可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="9bfba-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="9bfba-119">它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。</span><span class="sxs-lookup"><span data-stu-id="9bfba-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="9bfba-120">你将生成</span><span class="sxs-lookup"><span data-stu-id="9bfba-120">What you'll build</span></span>

<span data-ttu-id="9bfba-121">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="9bfba-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="9bfba-122">添加动态数据模板</span><span class="sxs-lookup"><span data-stu-id="9bfba-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="9bfba-123">通过模型绑定方法启用更新和删除数据</span><span class="sxs-lookup"><span data-stu-id="9bfba-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="9bfba-124">将数据验证规则应用-启用在数据库中创建一个新的记录</span><span class="sxs-lookup"><span data-stu-id="9bfba-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="9bfba-125">添加动态数据模板</span><span class="sxs-lookup"><span data-stu-id="9bfba-125">Add dynamic data templates</span></span>

<span data-ttu-id="9bfba-126">若要提供最佳用户体验和最大程度减少代码重复，将使用动态数据模板。</span><span class="sxs-lookup"><span data-stu-id="9bfba-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="9bfba-127">通过安装 NuGet 包可以轻松地将预建的动态数据模板集成到您的现有网站。</span><span class="sxs-lookup"><span data-stu-id="9bfba-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="9bfba-128">从**管理 NuGet 包**，安装**DynamicDataTemplatesCS**。</span><span class="sxs-lookup"><span data-stu-id="9bfba-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![动态数据模板](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="9bfba-130">请注意，你的项目现在包含一个名为文件夹**DynamicData**。</span><span class="sxs-lookup"><span data-stu-id="9bfba-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="9bfba-131">在该文件夹中，您将找到自动应用于 web 窗体中的动态控件的模板。</span><span class="sxs-lookup"><span data-stu-id="9bfba-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![动态数据文件夹](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="9bfba-133">启用更新和删除</span><span class="sxs-lookup"><span data-stu-id="9bfba-133">Enable updating and deleting</span></span>

<span data-ttu-id="9bfba-134">使用户能够更新和删除数据库中的记录是检索数据的过程非常相似。</span><span class="sxs-lookup"><span data-stu-id="9bfba-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="9bfba-135">在中**UpdateMethod**并**DeleteMethod**属性，指定执行这些操作，方法的名称。</span><span class="sxs-lookup"><span data-stu-id="9bfba-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="9bfba-136">GridView 控件后，您还可以指定自动生成的编辑和删除按钮。</span><span class="sxs-lookup"><span data-stu-id="9bfba-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="9bfba-137">以下突出显示的代码显示了对 GridView 代码新增的内容。</span><span class="sxs-lookup"><span data-stu-id="9bfba-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="9bfba-138">在代码隐藏文件中，添加 using 语句**System.Data.Entity.Infrastructure**。</span><span class="sxs-lookup"><span data-stu-id="9bfba-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="9bfba-139">然后，添加以下更新和删除方法。</span><span class="sxs-lookup"><span data-stu-id="9bfba-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="9bfba-140">**TryUpdateModel**方法将 web 窗体中匹配的数据绑定值应用于数据项。</span><span class="sxs-lookup"><span data-stu-id="9bfba-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="9bfba-141">根据 id 参数的值检索数据项目。</span><span class="sxs-lookup"><span data-stu-id="9bfba-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="9bfba-142">强制实施验证要求</span><span class="sxs-lookup"><span data-stu-id="9bfba-142">Enforce validation requirements</span></span>

<span data-ttu-id="9bfba-143">将数据更新时，会自动强制执行应用于 Student 类中的 FirstName、 LastName 和 Year 属性的验证特性。</span><span class="sxs-lookup"><span data-stu-id="9bfba-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="9bfba-144">DynamicField 控件添加验证特性所基于的客户端和服务器验证程序。</span><span class="sxs-lookup"><span data-stu-id="9bfba-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="9bfba-145">FirstName 和 LastName 属性都是必需。</span><span class="sxs-lookup"><span data-stu-id="9bfba-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="9bfba-146">名字不能超过 20 个字符的长度，并且姓氏不能超过 40 个字符。</span><span class="sxs-lookup"><span data-stu-id="9bfba-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="9bfba-147">年份必须是有效的 AcademicYear 枚举值。</span><span class="sxs-lookup"><span data-stu-id="9bfba-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="9bfba-148">如果用户不符合验证要求之一，将不会继续更新。</span><span class="sxs-lookup"><span data-stu-id="9bfba-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="9bfba-149">若要查看错误消息，请添加 GridView 上方的一个 ValidationSummary 控件。</span><span class="sxs-lookup"><span data-stu-id="9bfba-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="9bfba-150">若要显示从模型绑定验证错误，请设置**ShowModelStateErrors**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="9bfba-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="9bfba-151">运行 web 应用程序，并更新和删除的任何记录。</span><span class="sxs-lookup"><span data-stu-id="9bfba-151">Run the web application, and update and delete any of the records.</span></span>

![更新数据](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="9bfba-153">请注意，如果在编辑模式下年属性的值自动呈现为一个下拉列表。</span><span class="sxs-lookup"><span data-stu-id="9bfba-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="9bfba-154">Year 属性是枚举值，并枚举值的动态数据模板指定一个下拉列表以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="9bfba-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="9bfba-155">您可以找到该模板通过打开**枚举\_Edit.ascx**中的文件**DynamicData**/**FieldTemplates**文件夹。</span><span class="sxs-lookup"><span data-stu-id="9bfba-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="9bfba-156">如果你提供有效的值，在更新成功完成。</span><span class="sxs-lookup"><span data-stu-id="9bfba-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="9bfba-157">如果您违反验证要求之一，更新将不会继续并中网格之上显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="9bfba-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![错误消息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="9bfba-159">添加新记录</span><span class="sxs-lookup"><span data-stu-id="9bfba-159">Add new records</span></span>

<span data-ttu-id="9bfba-160">GridView 控件不包括**InsertMethod**属性，因此不能使用与模型绑定添加一个新的记录。</span><span class="sxs-lookup"><span data-stu-id="9bfba-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="9bfba-161">您可以找到在 InsertMethod 属性**FormView**， **DetailsView**，或**ListView**控件。</span><span class="sxs-lookup"><span data-stu-id="9bfba-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="9bfba-162">在本教程中，您将使用 FormView 控件添加新记录。</span><span class="sxs-lookup"><span data-stu-id="9bfba-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="9bfba-163">首先，将链接添加到新页面将创建用于添加新记录。</span><span class="sxs-lookup"><span data-stu-id="9bfba-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="9bfba-164">ValidationSummary 上方添加：</span><span class="sxs-lookup"><span data-stu-id="9bfba-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="9bfba-165">在学生页上的内容的顶部将显示新的链接。</span><span class="sxs-lookup"><span data-stu-id="9bfba-165">The new link will appear at the top of the content for the Students page.</span></span>

![新链接](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="9bfba-167">然后，添加新 web 窗体使用母版页，并将其命名**AddStudent**。</span><span class="sxs-lookup"><span data-stu-id="9bfba-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="9bfba-168">选择 Site.Master 作为主页面。</span><span class="sxs-lookup"><span data-stu-id="9bfba-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="9bfba-169">将呈现用于添加新的学生使用的字段**DynamicEntity**控件。</span><span class="sxs-lookup"><span data-stu-id="9bfba-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="9bfba-170">DynamicEntity 控件呈现 ItemType 属性中指定的类中的可编辑的属性。</span><span class="sxs-lookup"><span data-stu-id="9bfba-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="9bfba-171">StudentID 属性标记有 **[scaffoldcolumn （false)]** 属性以便不呈现。</span><span class="sxs-lookup"><span data-stu-id="9bfba-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="9bfba-172">在 AddStudent 页上的主要内容占位符，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="9bfba-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="9bfba-173">在代码隐藏文件 (AddStudent.aspx.cs) 中，添加**使用**语句**ContosoUniversityModelBinding.Models**命名空间。</span><span class="sxs-lookup"><span data-stu-id="9bfba-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="9bfba-174">然后，添加以下方法来指定如何插入一条新记录和取消按钮的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="9bfba-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="9bfba-175">保存的所有更改。</span><span class="sxs-lookup"><span data-stu-id="9bfba-175">Save all of the changes.</span></span>

<span data-ttu-id="9bfba-176">运行 web 应用程序并创建新的学生。</span><span class="sxs-lookup"><span data-stu-id="9bfba-176">Run the web application and create a new student.</span></span>

![添加新学生](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="9bfba-178">单击**插入**并注意已创建的新学生。</span><span class="sxs-lookup"><span data-stu-id="9bfba-178">Click **Insert** and notice the new student has been created.</span></span>

![显示新学生](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="9bfba-180">结束语</span><span class="sxs-lookup"><span data-stu-id="9bfba-180">Conclusion</span></span>

<span data-ttu-id="9bfba-181">在本教程中，您可以启用更新、 删除和创建数据。</span><span class="sxs-lookup"><span data-stu-id="9bfba-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="9bfba-182">确保验证规则将应用与数据交互时。</span><span class="sxs-lookup"><span data-stu-id="9bfba-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="9bfba-183">在接下来[教程](sorting-paging-and-filtering-data.md)在本系列中，将启用排序、 分页和筛选数据。</span><span class="sxs-lookup"><span data-stu-id="9bfba-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9bfba-184">[上一页](retrieving-data.md)
> [下一页](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="9bfba-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
