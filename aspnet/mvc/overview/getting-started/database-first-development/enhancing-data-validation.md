---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 增强数据验证 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: a328aa8aec2c512d77ddabec31b3785b8742e018
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376709"
---
<a name="ef-database-first-with-aspnet-mvc-enhancing-data-validation"></a><span data-ttu-id="21fb8-104">第一种使用 ASP.NET MVC 的 EF 数据库： 增强数据验证</span><span class="sxs-lookup"><span data-stu-id="21fb8-104">EF Database First with ASP.NET MVC: Enhancing Data Validation</span></span>
====================
<span data-ttu-id="21fb8-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="21fb8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="21fb8-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="21fb8-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="21fb8-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="21fb8-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="21fb8-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="21fb8-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="21fb8-109">本系列的此部分主要介绍在将数据批注添加到数据模型以指定验证要求和显示格式。</span><span class="sxs-lookup"><span data-stu-id="21fb8-109">This part of the series focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="21fb8-110">它改进了基于注释部分中的用户的反馈。</span><span class="sxs-lookup"><span data-stu-id="21fb8-110">It was improved based on feedback from users in the comments section.</span></span>


## <a name="add-data-annotations"></a><span data-ttu-id="21fb8-111">添加数据批注</span><span class="sxs-lookup"><span data-stu-id="21fb8-111">Add data annotations</span></span>

<span data-ttu-id="21fb8-112">正如您看到在之前主题中，一些数据的验证规则会自动应用到用户输入。</span><span class="sxs-lookup"><span data-stu-id="21fb8-112">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="21fb8-113">例如，可以仅级属性提供一个数字。</span><span class="sxs-lookup"><span data-stu-id="21fb8-113">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="21fb8-114">若要指定多个数据验证规则，可以向 model 类中添加数据批注。</span><span class="sxs-lookup"><span data-stu-id="21fb8-114">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="21fb8-115">这些批注将应用于整个 web 应用程序为指定的属性。</span><span class="sxs-lookup"><span data-stu-id="21fb8-115">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="21fb8-116">您还可以应用更改属性的显示方式; 的格式设置属性例如，更改使用的文本标签的值。</span><span class="sxs-lookup"><span data-stu-id="21fb8-116">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="21fb8-117">在本教程中，您将添加数据注释来限制为 FirstName、 LastName 和 MiddleName 属性提供的值的长度。</span><span class="sxs-lookup"><span data-stu-id="21fb8-117">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="21fb8-118">在数据库中，这些值是 50 个字符;但是，在 web 应用程序中的字符数限制为当前不强制执行。</span><span class="sxs-lookup"><span data-stu-id="21fb8-118">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="21fb8-119">如果用户提供超过 50 个字符，这些值之一，尝试将值保存到数据库时将崩溃页。</span><span class="sxs-lookup"><span data-stu-id="21fb8-119">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="21fb8-120">你还将为介于 0 和 4 之间的值限制级。</span><span class="sxs-lookup"><span data-stu-id="21fb8-120">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="21fb8-121">打开**Student.cs**中的文件**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="21fb8-121">Open the **Student.cs** file in the **Models** folder.</span></span> <span data-ttu-id="21fb8-122">向类添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="21fb8-122">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="21fb8-123">在 Enrollment.cs，添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="21fb8-123">In Enrollment.cs, add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="21fb8-124">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="21fb8-124">Build the solution.</span></span>

<span data-ttu-id="21fb8-125">浏览到用于编辑或创建一个学生页。</span><span class="sxs-lookup"><span data-stu-id="21fb8-125">Browse to a page for editing or creating a student.</span></span> <span data-ttu-id="21fb8-126">如果尝试输入超过 50 个字符，显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="21fb8-126">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![显示错误消息](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="21fb8-128">浏览到页以进行编辑注册，并尝试提供 4 级。</span><span class="sxs-lookup"><span data-stu-id="21fb8-128">Browse to the page for editing enrollments, and attempt to provide a grade above 4.</span></span>

![级范围错误](enhancing-data-validation/_static/image2.png)

<span data-ttu-id="21fb8-130">可以将应用于属性和类的数据验证注释的完整列表，请参阅[System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21fb8-130">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="21fb8-131">添加元数据类</span><span class="sxs-lookup"><span data-stu-id="21fb8-131">Add metadata classes</span></span>

<span data-ttu-id="21fb8-132">当不希望更改; 的数据库时，直接向 model 类添加验证特性有效但是，如果更改了数据库，并且需要重新生成模型类，您将丢失所有已应用于模型类的属性。</span><span class="sxs-lookup"><span data-stu-id="21fb8-132">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="21fb8-133">这种方法可以是非常低效，而且容易丢失重要的验证规则。</span><span class="sxs-lookup"><span data-stu-id="21fb8-133">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="21fb8-134">若要避免此问题，可以添加一个包含属性的元数据类。</span><span class="sxs-lookup"><span data-stu-id="21fb8-134">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="21fb8-135">当将关联到元数据类的模型类时，这些属性应用于该模型。</span><span class="sxs-lookup"><span data-stu-id="21fb8-135">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="21fb8-136">在此方法中，模型类可以重新生成而不会丢失所有已应用于元数据类的属性。</span><span class="sxs-lookup"><span data-stu-id="21fb8-136">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="21fb8-137">在中**模型**文件夹中，添加一个名为类**Metadata.cs**。</span><span class="sxs-lookup"><span data-stu-id="21fb8-137">In the **Models** folder, add a class named **Metadata.cs**.</span></span>

![添加元数据类](enhancing-data-validation/_static/image3.png)

<span data-ttu-id="21fb8-139">将以下代码替换为 Metadata.cs 中的代码。</span><span class="sxs-lookup"><span data-stu-id="21fb8-139">Replace the code in Metadata.cs with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="21fb8-140">这些元数据类包含所有先前应用到模型类的验证特性。</span><span class="sxs-lookup"><span data-stu-id="21fb8-140">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="21fb8-141">**显示**特性用于更改使用的文本标签的值。</span><span class="sxs-lookup"><span data-stu-id="21fb8-141">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="21fb8-142">现在，必须将模型类关联的元数据类。</span><span class="sxs-lookup"><span data-stu-id="21fb8-142">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="21fb8-143">在中**模型**文件夹中，添加一个名为类**PartialClasses.cs**。</span><span class="sxs-lookup"><span data-stu-id="21fb8-143">In the **Models** folder, add a class named **PartialClasses.cs**.</span></span>

<span data-ttu-id="21fb8-144">将以下代码替换为该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="21fb8-144">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="21fb8-145">请注意，每个类标记为`partial`类，并且每个匹配的名称和命名空间为自动生成的类。</span><span class="sxs-lookup"><span data-stu-id="21fb8-145">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="21fb8-146">通过将元数据特性应用到分部类，可确保数据验证属性，将应用到自动生成类。</span><span class="sxs-lookup"><span data-stu-id="21fb8-146">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="21fb8-147">当你重新生成模型类，因为在不重新生成的分部类中应用的元数据特性，这些属性不会丢失。</span><span class="sxs-lookup"><span data-stu-id="21fb8-147">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="21fb8-148">若要重新生成会自动生成的类，请打开 ContosoModel.edmx 文件。</span><span class="sxs-lookup"><span data-stu-id="21fb8-148">To regenerate the automatically-generated classes, open the ContosoModel.edmx file.</span></span> <span data-ttu-id="21fb8-149">再次重申，右键单击设计图面，然后选择**从数据库更新模型**。</span><span class="sxs-lookup"><span data-stu-id="21fb8-149">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="21fb8-150">即使没有更改数据库，此过程将重新生成类。</span><span class="sxs-lookup"><span data-stu-id="21fb8-150">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="21fb8-151">在中**刷新**选项卡上，选择**表**并**完成**。</span><span class="sxs-lookup"><span data-stu-id="21fb8-151">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

![刷新表](enhancing-data-validation/_static/image4.png)

<span data-ttu-id="21fb8-153">保存 ContosoModel.edmx 文件以应用更改。</span><span class="sxs-lookup"><span data-stu-id="21fb8-153">Save the ContosoModel.edmx file to apply the changes.</span></span>

<span data-ttu-id="21fb8-154">打开 Student.cs 文件或 Enrollment.cs 文件，并请注意，您先前应用的数据验证属性将不再在文件中。</span><span class="sxs-lookup"><span data-stu-id="21fb8-154">Open the Student.cs file or the Enrollment.cs file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="21fb8-155">但是，运行该应用程序，并请注意，当输入数据时仍应用验证规则。</span><span class="sxs-lookup"><span data-stu-id="21fb8-155">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="21fb8-156">[上一页](customizing-a-view.md)
> [下一页](publish-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="21fb8-156">[Previous](customizing-a-view.md)
[Next](publish-to-azure.md)</span></span>
