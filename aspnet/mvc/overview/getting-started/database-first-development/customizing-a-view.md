---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 首先使用 ASP.NET MVC 的 EF 数据库： 自定义视图 |Microsoft 文档
author: tfitzmac
description: 使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 8338603e032329ad03d47c6392e508aa07c6858e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30867653"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a><span data-ttu-id="ac27d-104">首先使用 ASP.NET MVC 的 EF 数据库： 自定义视图</span><span class="sxs-lookup"><span data-stu-id="ac27d-104">EF Database First with ASP.NET MVC: Customizing a View</span></span>
====================
<span data-ttu-id="ac27d-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ac27d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ac27d-106">使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。</span><span class="sxs-lookup"><span data-stu-id="ac27d-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="ac27d-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="ac27d-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="ac27d-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="ac27d-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="ac27d-109">此系列的一部分的重点介绍更改要增强演示文稿的自动生成的视图。</span><span class="sxs-lookup"><span data-stu-id="ac27d-109">This part of the series focuses on changing the automatically-generated views to enhance the presentation.</span></span>


## <a name="add-enrolled-courses-to-student-details"></a><span data-ttu-id="ac27d-110">将已注册的课程添加到学生详细信息</span><span class="sxs-lookup"><span data-stu-id="ac27d-110">Add enrolled courses to student details</span></span>

<span data-ttu-id="ac27d-111">生成的代码应用程序提供一个良好的起始点，但它不一定提供所有应用程序中需要的功能。</span><span class="sxs-lookup"><span data-stu-id="ac27d-111">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="ac27d-112">你可以自定义代码以满足你的应用程序的特定要求。</span><span class="sxs-lookup"><span data-stu-id="ac27d-112">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="ac27d-113">目前，你的应用程序不显示有关所选学生的已注册的课程。</span><span class="sxs-lookup"><span data-stu-id="ac27d-113">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="ac27d-114">本部分中，在中，你将添加已注册的课程到每个学生**详细信息**学生的视图。</span><span class="sxs-lookup"><span data-stu-id="ac27d-114">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="ac27d-115">打开**Students/Details.cshtml**，和最后一个下方&lt;/dl&gt;选项卡上，但在关闭前&lt;/div&gt;标记中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="ac27d-115">Open **Students/Details.cshtml**, and below the last &lt;/dl&gt; tab, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="ac27d-116">此代码将创建所选学生注册表中显示为每个记录的行的表。</span><span class="sxs-lookup"><span data-stu-id="ac27d-116">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="ac27d-117">**显示**方法表示表达式的对象 (modelItem) 上呈现 HTML。</span><span class="sxs-lookup"><span data-stu-id="ac27d-117">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="ac27d-118">使用显示方法 （而不是只需在代码中嵌入的属性值） 以确保值的格式正确基于其类型和该类型的模板。</span><span class="sxs-lookup"><span data-stu-id="ac27d-118">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="ac27d-119">在此示例中，每个表达式从当前记录在循环中，返回的单个属性和值是指呈现为文本的基元类型。</span><span class="sxs-lookup"><span data-stu-id="ac27d-119">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

<span data-ttu-id="ac27d-120">再次浏览到学生/索引视图并选择**详细信息**学生之一。</span><span class="sxs-lookup"><span data-stu-id="ac27d-120">Browse to the Students/Index view again and select **Details** for one of the students.</span></span> <span data-ttu-id="ac27d-121">你将看到已注册的课程已包含在视图中。</span><span class="sxs-lookup"><span data-stu-id="ac27d-121">You will see the enrolled courses have been included in the view.</span></span>

![学生的注册](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="ac27d-123">[上一页](changing-the-database.md)
> [下一页](enhancing-data-validation.md)</span><span class="sxs-lookup"><span data-stu-id="ac27d-123">[Previous](changing-the-database.md)
[Next](enhancing-data-validation.md)</span></span>
