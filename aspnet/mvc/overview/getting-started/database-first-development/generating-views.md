---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 首先使用 ASP.NET MVC 的 EF 数据库： 生成视图 |Microsoft 文档
author: tfitzmac
description: 使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: b60e89a187a879255eb051dc87241714cef6fa63
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879746"
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a><span data-ttu-id="b56fa-104">首先使用 ASP.NET MVC 的 EF 数据库： 生成视图</span><span class="sxs-lookup"><span data-stu-id="b56fa-104">EF Database First with ASP.NET MVC: Generating Views</span></span>
====================
<span data-ttu-id="b56fa-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b56fa-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b56fa-106">使用 MVC、 实体框架和 ASP.NET 基架，可以创建的 web 应用程序提供了一个接口到现有数据库。</span><span class="sxs-lookup"><span data-stu-id="b56fa-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="b56fa-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="b56fa-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="b56fa-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="b56fa-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="b56fa-109">此系列的一部分的重点介绍使用 ASP.NET 基架以生成控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="b56fa-109">This part of the series focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>


## <a name="add-scaffold"></a><span data-ttu-id="b56fa-110">添加基架</span><span class="sxs-lookup"><span data-stu-id="b56fa-110">Add scaffold</span></span>

<span data-ttu-id="b56fa-111">你就可以生成将提供的模型类的标准数据操作的代码。</span><span class="sxs-lookup"><span data-stu-id="b56fa-111">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="b56fa-112">通过添加基架项添加代码。</span><span class="sxs-lookup"><span data-stu-id="b56fa-112">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="b56fa-113">有许多选项可以添加; 基架的类型在本教程中，基架将包括一个控制器和对应于你在上一节中创建了学生和注册模型的视图。</span><span class="sxs-lookup"><span data-stu-id="b56fa-113">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="b56fa-114">若要维护你的项目中的一致性，您将新控制器添加到现有**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="b56fa-114">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="b56fa-115">右键单击**控制器**文件夹，并选择**添加**–**新建基架项**。</span><span class="sxs-lookup"><span data-stu-id="b56fa-115">Right-click the **Controllers** folder, and select **Add** – **New Scaffolded Item**.</span></span>

![添加基架](generating-views/_static/image1.png)

<span data-ttu-id="b56fa-117">选择**数据与视图，MVC 5 控制器使用 Entity Framework**选项。</span><span class="sxs-lookup"><span data-stu-id="b56fa-117">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="b56fa-118">此选项将生成控制器和视图更新、 删除、 创建和显示您的模型中的数据。</span><span class="sxs-lookup"><span data-stu-id="b56fa-118">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![添加 mvc 控制器](generating-views/_static/image2.png)

<span data-ttu-id="b56fa-120">选择**学生**模型类，然后选择**ContosoUniversityEntities**上下文类。</span><span class="sxs-lookup"><span data-stu-id="b56fa-120">Select **Student** for the model class, and select the **ContosoUniversityEntities** for the context class.</span></span> <span data-ttu-id="b56fa-121">保留作为控制器名称**StudentsController**，</span><span class="sxs-lookup"><span data-stu-id="b56fa-121">Keep the controller name as **StudentsController**,</span></span>

![指定控制器](generating-views/_static/image3.png)

<span data-ttu-id="b56fa-123">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="b56fa-123">Click **Add**.</span></span>

<span data-ttu-id="b56fa-124">如果你收到错误，则可能是因为未生成上一节中的项目。</span><span class="sxs-lookup"><span data-stu-id="b56fa-124">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="b56fa-125">如果是这样，请尝试生成项目，然后再添加基架的项。</span><span class="sxs-lookup"><span data-stu-id="b56fa-125">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="b56fa-126">此代码生成过程完成后，你将看到你项目中的新控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="b56fa-126">After the code generation process is complete, you will see a new controller and views in your project.</span></span>

![显示视图](generating-views/_static/image4.png)

<span data-ttu-id="b56fa-128">同样，执行相同的步骤，但添加基架注册类。</span><span class="sxs-lookup"><span data-stu-id="b56fa-128">Perform the same steps again, but add a scaffold for the Enrollment class.</span></span> <span data-ttu-id="b56fa-129">完成后，你应具有**EnrollmentsController.cs**文件和文件夹在**视图**名为**注册**与创建、 删除、 详细信息、 编辑和索引视图。</span><span class="sxs-lookup"><span data-stu-id="b56fa-129">When finished, you should have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

![显示视图](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a><span data-ttu-id="b56fa-131">将链接添加到新视图</span><span class="sxs-lookup"><span data-stu-id="b56fa-131">Add links to new views</span></span>

<span data-ttu-id="b56fa-132">若要使你更轻松地导航到你新视图，可以在索引视图中添加几个超链接，学生和注册。</span><span class="sxs-lookup"><span data-stu-id="b56fa-132">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="b56fa-133">处打开此文件**Views/Home/Index.cshtml**，这是你的站点的主页。</span><span class="sxs-lookup"><span data-stu-id="b56fa-133">Open the file at **Views/Home/Index.cshtml**, which is the home page for your site.</span></span> <span data-ttu-id="b56fa-134">添加 jumbotron 下面的代码。</span><span class="sxs-lookup"><span data-stu-id="b56fa-134">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="b56fa-135">对于 ActionLink 方法中，第一个参数是要显示的链接中的文本。</span><span class="sxs-lookup"><span data-stu-id="b56fa-135">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="b56fa-136">第二个参数是操作，第三个参数是控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="b56fa-136">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="b56fa-137">例如，第一个链接将指向 StudentsController 中的索引操作。</span><span class="sxs-lookup"><span data-stu-id="b56fa-137">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="b56fa-138">实际的超链接将从这些值构造。</span><span class="sxs-lookup"><span data-stu-id="b56fa-138">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="b56fa-139">第一个链接最终将用户导航到**Index.cshtml**文件内**视图/学生**文件夹。</span><span class="sxs-lookup"><span data-stu-id="b56fa-139">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="b56fa-140">显示学生视图</span><span class="sxs-lookup"><span data-stu-id="b56fa-140">Display student views</span></span>

<span data-ttu-id="b56fa-141">你将验证正确添加到你的项目的代码显示学生的列表，并且使用户能够编辑、 创建或删除数据库中的学生记录。</span><span class="sxs-lookup"><span data-stu-id="b56fa-141">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="b56fa-142">右键单击**Views/Home/Index.cshtml**文件中，并选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="b56fa-142">Right-click the **Views/Home/Index.cshtml** file, and select **View in Browser**.</span></span> <span data-ttu-id="b56fa-143">在此页上，单击链接获取学生列表。</span><span class="sxs-lookup"><span data-stu-id="b56fa-143">On this page, click the link for the list of students.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="b56fa-144">在此页上，请注意若要修改此数据的学生和链接的列表。</span><span class="sxs-lookup"><span data-stu-id="b56fa-144">On this page, notice the list of the students and links to modify this data.</span></span>

![学生列表](generating-views/_static/image7.png)

<span data-ttu-id="b56fa-146">单击**新建**链接并为新学生提供一些值。</span><span class="sxs-lookup"><span data-stu-id="b56fa-146">Click the **Create New** link and provide some values for a new student.</span></span>

![创建新的学生](generating-views/_static/image8.png)

<span data-ttu-id="b56fa-148">单击**创建**，并留意新的学生添加到列表。</span><span class="sxs-lookup"><span data-stu-id="b56fa-148">Click **Create**, and notice the new student is added to your list.</span></span>

![与新的名学生的列表](generating-views/_static/image9.png)

<span data-ttu-id="b56fa-150">选择**编辑**链接，并将某些值更改为一名学生。</span><span class="sxs-lookup"><span data-stu-id="b56fa-150">Select the **Edit** link, and change some of the values for a student.</span></span>

![编辑学生](generating-views/_static/image10.png)

<span data-ttu-id="b56fa-152">单击**保存**，并注意学生记录已更改。</span><span class="sxs-lookup"><span data-stu-id="b56fa-152">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="b56fa-153">最后，选择**删除**链接并确认你想要删除的记录，通过单击**删除**按钮。</span><span class="sxs-lookup"><span data-stu-id="b56fa-153">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

![删除学生](generating-views/_static/image11.png)

<span data-ttu-id="b56fa-155">无需编写任何代码，你已经添加对数据的常见操作执行学生表中的视图。</span><span class="sxs-lookup"><span data-stu-id="b56fa-155">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="b56fa-156">你可能已经注意到字段的文本标签，基于数据库属性 (如**LastName**) 这不一定是你想要在网页上显示。</span><span class="sxs-lookup"><span data-stu-id="b56fa-156">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="b56fa-157">例如，您可能想要的标签**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="b56fa-157">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="b56fa-158">你将在本教程的更高版本中修复此显示问题。</span><span class="sxs-lookup"><span data-stu-id="b56fa-158">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="b56fa-159">显示注册视图</span><span class="sxs-lookup"><span data-stu-id="b56fa-159">Display enrollment views</span></span>

<span data-ttu-id="b56fa-160">你的数据库包括学生和注册表中和课程和注册表之间的一个对多关系之间的一个对多关系。</span><span class="sxs-lookup"><span data-stu-id="b56fa-160">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="b56fa-161">注册的视图正确处理这些关系。</span><span class="sxs-lookup"><span data-stu-id="b56fa-161">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="b56fa-162">导航到站点并选择主页**列表注册**链接，然后**新建**链接。</span><span class="sxs-lookup"><span data-stu-id="b56fa-162">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span> <span data-ttu-id="b56fa-163">该视图显示用于创建新的注册记录的表单。</span><span class="sxs-lookup"><span data-stu-id="b56fa-163">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="b56fa-164">具体而言，请注意该窗体包含两个相关表中的值填充的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="b56fa-164">In particular, notice that the form contains two drop-down lists that are populated with values from the related tables.</span></span>

![创建注册](generating-views/_static/image12.png)

<span data-ttu-id="b56fa-166">此外，验证提供的值将自动应用基于字段对数据类型。</span><span class="sxs-lookup"><span data-stu-id="b56fa-166">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="b56fa-167">年级需要一个数字，因此如果你尝试提供不兼容的值显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="b56fa-167">Grade requires a number, so an error message is displayed if you try to provide an incompatible value.</span></span>

![验证消息](generating-views/_static/image13.png)

<span data-ttu-id="b56fa-169">你已验证的自动生成的视图，使用户能够处理数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="b56fa-169">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="b56fa-170">在本系列中下一步教程中，将更新该数据库，并在 web 应用程序中进行相应更改。</span><span class="sxs-lookup"><span data-stu-id="b56fa-170">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b56fa-171">[上一页](creating-the-web-application.md)
> [下一页](changing-the-database.md)</span><span class="sxs-lookup"><span data-stu-id="b56fa-171">[Previous](creating-the-web-application.md)
[Next](changing-the-database.md)</span></span>
