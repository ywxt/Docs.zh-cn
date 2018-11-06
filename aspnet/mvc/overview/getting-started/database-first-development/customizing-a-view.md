---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 自定义视图 |Microsoft Docs
author: Rick-Anderson
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: riande
ms.date: 10/01/2014
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: f66e097d53514ab3842e04cd545ca626c652478a
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021205"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a><span data-ttu-id="7185f-104">第一种使用 ASP.NET MVC 的 EF 数据库： 自定义视图</span><span class="sxs-lookup"><span data-stu-id="7185f-104">EF Database First with ASP.NET MVC: Customizing a View</span></span>
====================
<span data-ttu-id="7185f-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7185f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7185f-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7185f-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="7185f-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="7185f-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="7185f-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="7185f-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="7185f-109">本系列的此部分重点介绍更改的自动生成的视图，以增强此演示文稿。</span><span class="sxs-lookup"><span data-stu-id="7185f-109">This part of the series focuses on changing the automatically-generated views to enhance the presentation.</span></span>


## <a name="add-enrolled-courses-to-student-details"></a><span data-ttu-id="7185f-110">将已注册的课程添加到学生详细信息</span><span class="sxs-lookup"><span data-stu-id="7185f-110">Add enrolled courses to student details</span></span>

<span data-ttu-id="7185f-111">生成的代码为应用程序提供很好的起点，但它不一定提供全部所需应用程序中的功能。</span><span class="sxs-lookup"><span data-stu-id="7185f-111">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="7185f-112">可以自定义代码来满足你的应用程序的特定要求。</span><span class="sxs-lookup"><span data-stu-id="7185f-112">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="7185f-113">目前，你的应用程序不显示所选学生的已注册的课程。</span><span class="sxs-lookup"><span data-stu-id="7185f-113">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="7185f-114">在本部分中，您将添加已注册的课程到每个学生**详细信息**学生的视图。</span><span class="sxs-lookup"><span data-stu-id="7185f-114">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="7185f-115">打开**Students/Details.cshtml**，和最后一个下方&lt;/dl&gt;选项卡上，但在关闭前&lt;/div&gt;标记中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="7185f-115">Open **Students/Details.cshtml**, and below the last &lt;/dl&gt; tab, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="7185f-116">此代码将创建所选学生 Enrollment 表中显示为每个记录的行的表。</span><span class="sxs-lookup"><span data-stu-id="7185f-116">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="7185f-117">**显示**方法表示表达式的对象 (modelItem) 将呈现 HTML。</span><span class="sxs-lookup"><span data-stu-id="7185f-117">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="7185f-118">使用 Display 方法 （而不是只需在代码中嵌入的属性值） 以确保设置的值格式正确基于其类型和该类型的模板。</span><span class="sxs-lookup"><span data-stu-id="7185f-118">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="7185f-119">在此示例中，从当前记录在循环中，每个表达式返回的单个属性和值是基元类型的呈现为文本。</span><span class="sxs-lookup"><span data-stu-id="7185f-119">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

<span data-ttu-id="7185f-120">再次浏览到学生/索引视图并选择**详细信息**一个学生。</span><span class="sxs-lookup"><span data-stu-id="7185f-120">Browse to the Students/Index view again and select **Details** for one of the students.</span></span> <span data-ttu-id="7185f-121">你将看到在视图中包含了已注册的课程。</span><span class="sxs-lookup"><span data-stu-id="7185f-121">You will see the enrolled courses have been included in the view.</span></span>

![与注册的学生](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="7185f-123">[上一页](changing-the-database.md)
> [下一页](enhancing-data-validation.md)</span><span class="sxs-lookup"><span data-stu-id="7185f-123">[Previous](changing-the-database.md)
[Next](enhancing-data-validation.md)</span></span>
