---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 生成视图 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: 58f8be181f80f5b27353e9ef5cafe48bcb370e29
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399605"
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a><span data-ttu-id="c2b92-104">第一种使用 ASP.NET MVC 的 EF 数据库： 生成视图</span><span class="sxs-lookup"><span data-stu-id="c2b92-104">EF Database First with ASP.NET MVC: Generating Views</span></span>
====================
<span data-ttu-id="c2b92-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c2b92-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c2b92-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c2b92-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="c2b92-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="c2b92-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="c2b92-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="c2b92-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="c2b92-109">本系列的此部分重点介绍使用 ASP.NET 基架生成控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="c2b92-109">This part of the series focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>


## <a name="add-scaffold"></a><span data-ttu-id="c2b92-110">添加基架</span><span class="sxs-lookup"><span data-stu-id="c2b92-110">Add scaffold</span></span>

<span data-ttu-id="c2b92-111">已准备好生成将提供标准数据操作，以便在 model 类的代码。</span><span class="sxs-lookup"><span data-stu-id="c2b92-111">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="c2b92-112">通过添加基架项添加代码。</span><span class="sxs-lookup"><span data-stu-id="c2b92-112">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="c2b92-113">有许多选项的类型的基架可以添加;在本教程中，基架将包括控制器和对应于上一节中创建的 Student 和注册模型的视图。</span><span class="sxs-lookup"><span data-stu-id="c2b92-113">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="c2b92-114">若要维护你的项目中的一致性，将添加新控制器到现有**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="c2b92-114">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="c2b92-115">右键单击**控制器**文件夹，然后选择**添加**–**新基架项**。</span><span class="sxs-lookup"><span data-stu-id="c2b92-115">Right-click the **Controllers** folder, and select **Add** – **New Scaffolded Item**.</span></span>

![添加基架](generating-views/_static/image1.png)

<span data-ttu-id="c2b92-117">选择**包含的 MVC 5 控制器视图，使用实体框架**选项。</span><span class="sxs-lookup"><span data-stu-id="c2b92-117">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="c2b92-118">此选项将生成控制器和视图更新、 删除、 创建和显示模型中的数据。</span><span class="sxs-lookup"><span data-stu-id="c2b92-118">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![添加 mvc 控制器](generating-views/_static/image2.png)

<span data-ttu-id="c2b92-120">选择**学生**模型类，然后选择**ContosoUniversityEntities**上下文类。</span><span class="sxs-lookup"><span data-stu-id="c2b92-120">Select **Student** for the model class, and select the **ContosoUniversityEntities** for the context class.</span></span> <span data-ttu-id="c2b92-121">保留作为控制器名称**StudentsController**，</span><span class="sxs-lookup"><span data-stu-id="c2b92-121">Keep the controller name as **StudentsController**,</span></span>

![指定控制器](generating-views/_static/image3.png)

<span data-ttu-id="c2b92-123">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="c2b92-123">Click **Add**.</span></span>

<span data-ttu-id="c2b92-124">如果收到错误，则可能是因为未生成上一节中的项目。</span><span class="sxs-lookup"><span data-stu-id="c2b92-124">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="c2b92-125">如果是这样，请尝试生成项目，，然后再次添加基架的项。</span><span class="sxs-lookup"><span data-stu-id="c2b92-125">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="c2b92-126">代码生成过程完成后，您将在项目中看到新的控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="c2b92-126">After the code generation process is complete, you will see a new controller and views in your project.</span></span>

![显示视图](generating-views/_static/image4.png)

<span data-ttu-id="c2b92-128">同样，执行相同的步骤，但添加注册类的基本框架。</span><span class="sxs-lookup"><span data-stu-id="c2b92-128">Perform the same steps again, but add a scaffold for the Enrollment class.</span></span> <span data-ttu-id="c2b92-129">完成后，应拥有**EnrollmentsController.cs**文件和文件夹下的**视图**名为**注册**与创建、 删除、 详细信息、 编辑和索引视图。</span><span class="sxs-lookup"><span data-stu-id="c2b92-129">When finished, you should have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

![显示视图](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a><span data-ttu-id="c2b92-131">将链接添加到新的视图</span><span class="sxs-lookup"><span data-stu-id="c2b92-131">Add links to new views</span></span>

<span data-ttu-id="c2b92-132">若要使你更轻松地导航到新视图，可以索引视图中添加几个超链接，面向学生和注册。</span><span class="sxs-lookup"><span data-stu-id="c2b92-132">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="c2b92-133">打开的文件**Views/Home/Index.cshtml**，这是你的站点的主页。</span><span class="sxs-lookup"><span data-stu-id="c2b92-133">Open the file at **Views/Home/Index.cshtml**, which is the home page for your site.</span></span> <span data-ttu-id="c2b92-134">添加 jumbotron 下面的代码。</span><span class="sxs-lookup"><span data-stu-id="c2b92-134">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="c2b92-135">对于 ActionLink 方法中，第一个参数是要显示的链接中的文本。</span><span class="sxs-lookup"><span data-stu-id="c2b92-135">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="c2b92-136">第二个参数是操作，第三个参数是控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="c2b92-136">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="c2b92-137">例如，第一个链接指向 StudentsController 中的索引操作。</span><span class="sxs-lookup"><span data-stu-id="c2b92-137">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="c2b92-138">实际的超链接，这些值从构造。</span><span class="sxs-lookup"><span data-stu-id="c2b92-138">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="c2b92-139">第一个链接最终用户可转到**Index.cshtml**文件内**视图/学生**文件夹。</span><span class="sxs-lookup"><span data-stu-id="c2b92-139">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="c2b92-140">显示学生视图</span><span class="sxs-lookup"><span data-stu-id="c2b92-140">Display student views</span></span>

<span data-ttu-id="c2b92-141">将验证正确添加到你的项目的代码显示学生列表，并使用户能够编辑、 创建或删除数据库中的学生记录。</span><span class="sxs-lookup"><span data-stu-id="c2b92-141">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="c2b92-142">右键单击**Views/Home/Index.cshtml**文件，并选择**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="c2b92-142">Right-click the **Views/Home/Index.cshtml** file, and select **View in Browser**.</span></span> <span data-ttu-id="c2b92-143">在此页上，单击学生列表的链接。</span><span class="sxs-lookup"><span data-stu-id="c2b92-143">On this page, click the link for the list of students.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="c2b92-144">在此页上，请注意，若要修改此数据的学生和链接的列表。</span><span class="sxs-lookup"><span data-stu-id="c2b92-144">On this page, notice the list of the students and links to modify this data.</span></span>

![学生列表](generating-views/_static/image7.png)

<span data-ttu-id="c2b92-146">单击**创建新**链接并为新的学生提供一些值。</span><span class="sxs-lookup"><span data-stu-id="c2b92-146">Click the **Create New** link and provide some values for a new student.</span></span>

![创建新学生](generating-views/_static/image8.png)

<span data-ttu-id="c2b92-148">单击**创建**，并请注意，新学生添加到列表。</span><span class="sxs-lookup"><span data-stu-id="c2b92-148">Click **Create**, and notice the new student is added to your list.</span></span>

![具有新学生列表](generating-views/_static/image9.png)

<span data-ttu-id="c2b92-150">选择**编辑**链接，并更改值的一些学生。</span><span class="sxs-lookup"><span data-stu-id="c2b92-150">Select the **Edit** link, and change some of the values for a student.</span></span>

![编辑学生](generating-views/_static/image10.png)

<span data-ttu-id="c2b92-152">单击**保存**，您会发现已更改学生记录。</span><span class="sxs-lookup"><span data-stu-id="c2b92-152">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="c2b92-153">最后，选择**删除**链接，然后确认你想要通过单击删除的记录**删除**按钮。</span><span class="sxs-lookup"><span data-stu-id="c2b92-153">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

![删除学生](generating-views/_static/image11.png)

<span data-ttu-id="c2b92-155">无需编写任何代码，您已添加在 Student 表中执行常见操作的数据的视图。</span><span class="sxs-lookup"><span data-stu-id="c2b92-155">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="c2b92-156">您可能已经注意到一个字段的文本标签基于的数据库属性 (如**LastName**) 这不一定是你想要在网页上显示。</span><span class="sxs-lookup"><span data-stu-id="c2b92-156">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="c2b92-157">例如，可能想要进行的标签**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="c2b92-157">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="c2b92-158">本教程的后面，则将修复此显示问题。</span><span class="sxs-lookup"><span data-stu-id="c2b92-158">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="c2b92-159">显示注册视图</span><span class="sxs-lookup"><span data-stu-id="c2b92-159">Display enrollment views</span></span>

<span data-ttu-id="c2b92-160">你的数据库包括一个对多关系学生和注册表中与 Course 和 Enrollment 表之间的一个对多关系之间。</span><span class="sxs-lookup"><span data-stu-id="c2b92-160">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="c2b92-161">为注册视图正确处理这些关系。</span><span class="sxs-lookup"><span data-stu-id="c2b92-161">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="c2b92-162">导航到站点并选择主页**注册列表**链接，然后**创建新**链接。</span><span class="sxs-lookup"><span data-stu-id="c2b92-162">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span> <span data-ttu-id="c2b92-163">该视图显示用于创建新的注册记录的窗体。</span><span class="sxs-lookup"><span data-stu-id="c2b92-163">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="c2b92-164">具体而言，请注意该窗体包含两个相关表中的值填充的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="c2b92-164">In particular, notice that the form contains two drop-down lists that are populated with values from the related tables.</span></span>

![创建注册](generating-views/_static/image12.png)

<span data-ttu-id="c2b92-166">此外，验证所提供的值将自动应用基于字段的数据类型。</span><span class="sxs-lookup"><span data-stu-id="c2b92-166">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="c2b92-167">等级需要一个数字，因此如果你尝试提供不兼容的值显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="c2b92-167">Grade requires a number, so an error message is displayed if you try to provide an incompatible value.</span></span>

![验证消息](generating-views/_static/image13.png)

<span data-ttu-id="c2b92-169">您已验证的自动生成的视图使用户能够处理在数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="c2b92-169">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="c2b92-170">在本系列中下一个教程中，将更新数据库，并在 web 应用程序中进行相应更改。</span><span class="sxs-lookup"><span data-stu-id="c2b92-170">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c2b92-171">[上一页](creating-the-web-application.md)
> [下一页](changing-the-database.md)</span><span class="sxs-lookup"><span data-stu-id="c2b92-171">[Previous](creating-the-web-application.md)
[Next](changing-the-database.md)</span></span>
