---
title: ASP.NET Core 中的 Razor 页面和 Entity Framework Core - 第 1 个教程（共 8 个）
author: rick-anderson
description: 介绍了如何使用 Entity Framework Core 创建 Razor 页面应用
manager: wpickett
ms.author: riande
ms.date: 11/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/intro
ms.openlocfilehash: 99a8d158c896566c2f6e6c22e4b37b1956e21cbf
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="razor-pages-with-entity-framework-core-in-aspnet-core---tutorial-1-of-8"></a><span data-ttu-id="6b90c-103">ASP.NET Core 中的 Razor 页面和 Entity Framework Core - 第 1 个教程（共 8 个）</span><span class="sxs-lookup"><span data-stu-id="6b90c-103">Razor Pages with Entity Framework Core in ASP.NET Core - Tutorial 1 of 8</span></span>

<span data-ttu-id="6b90c-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6b90c-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6b90c-105">Contoso University 示例 Web 应用演示了如何使用 Entity Framework (EF) Core 2.0 和 Visual Studio 2017 创建 ASP.NET Core 2.0 MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6b90c-105">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="6b90c-106">该示例应用是一个虚构的 Contoso University 的网站。</span><span class="sxs-lookup"><span data-stu-id="6b90c-106">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="6b90c-107">其中包括学生录取、课程创建和讲师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="6b90c-107">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="6b90c-108">本页是介绍如何构建 Contoso University 示例应用系列教程中的第一部分。</span><span class="sxs-lookup"><span data-stu-id="6b90c-108">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="6b90c-109">下载或查看已完成的应用。</span><span class="sxs-lookup"><span data-stu-id="6b90c-109">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="6b90c-110">[下载说明](xref:tutorials/index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-110">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b90c-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="6b90c-111">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

<span data-ttu-id="6b90c-112">熟悉 [Razor 页面](xref:mvc/razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-112">Familiarity with [Razor Pages](xref:mvc/razor-pages/index).</span></span> <span data-ttu-id="6b90c-113">新程序员在开始学习本系列之前，应先完成 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-113">New programmers should complete [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) before starting this series.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6b90c-114">疑难解答</span><span class="sxs-lookup"><span data-stu-id="6b90c-114">Troubleshooting</span></span>

<span data-ttu-id="6b90c-115">如果遇到无法解决的问题，可以通过与[已完成的阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)对比代码来查找解决方案。</span><span class="sxs-lookup"><span data-stu-id="6b90c-115">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots).</span></span> <span data-ttu-id="6b90c-116">常见错误以及对应的解决方案，请参阅 [最新教程中的故障排除](xref:data/ef-mvc/advanced#common-errors)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-116">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="6b90c-117">如果在该处找不到所需内容，可以在 [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) 上发表有关 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 或 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core) 的问题。</span><span class="sxs-lookup"><span data-stu-id="6b90c-117">If you don't find what you need there, you can post a question to [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="6b90c-118">本系列教程以之前教程中已完成的工作为基础。</span><span class="sxs-lookup"><span data-stu-id="6b90c-118">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="6b90c-119">每次成功完成教程后，请考虑保存项目副本。</span><span class="sxs-lookup"><span data-stu-id="6b90c-119">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="6b90c-120">如果遇到问题，便可以从上一教程重新开始，而无需从头开始。</span><span class="sxs-lookup"><span data-stu-id="6b90c-120">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="6b90c-121">或者可以下载[已完成阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)并使用已完成阶段重新开始。</span><span class="sxs-lookup"><span data-stu-id="6b90c-121">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="6b90c-122">Contoso University Web 应用</span><span class="sxs-lookup"><span data-stu-id="6b90c-122">The Contoso University web app</span></span>

<span data-ttu-id="6b90c-123">这些教程中所构建的应用是一个基本的大学网站。</span><span class="sxs-lookup"><span data-stu-id="6b90c-123">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="6b90c-124">用户可以查看和更新学生、课程和讲师信息。</span><span class="sxs-lookup"><span data-stu-id="6b90c-124">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="6b90c-125">以下是在本教程中创建的几个屏幕。</span><span class="sxs-lookup"><span data-stu-id="6b90c-125">Here are a few of the screens created in the tutorial.</span></span>

![“学生索引”页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

<span data-ttu-id="6b90c-128">此网站的 UI 样式与内置模板生成的 UI 样式类似。</span><span class="sxs-lookup"><span data-stu-id="6b90c-128">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="6b90c-129">教程的重点是 EF Core 和 Razor 页面，而非 UI。</span><span class="sxs-lookup"><span data-stu-id="6b90c-129">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="6b90c-130">创建 Razor 页面 Web 应用</span><span class="sxs-lookup"><span data-stu-id="6b90c-130">Create a Razor Pages web app</span></span>

* <span data-ttu-id="6b90c-131">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="6b90c-131">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="6b90c-132">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6b90c-132">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="6b90c-133">将该项目命名为 ContosoUniversity 。</span><span class="sxs-lookup"><span data-stu-id="6b90c-133">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="6b90c-134">务必将该项目命名为 ContosoUniversity，以便复制/粘贴代码时命名空间相匹配。</span><span class="sxs-lookup"><span data-stu-id="6b90c-134">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="6b90c-135">![新建 ASP.NET Core Web 应用程序](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="6b90c-135">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="6b90c-136">在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="6b90c-136">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="6b90c-137">![Web 应用程序（Razor 页面）](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="6b90c-137">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="6b90c-138">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在运行（不附加调试器）</span><span class="sxs-lookup"><span data-stu-id="6b90c-138">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="6b90c-139">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="6b90c-139">Set up the site style</span></span>

<span data-ttu-id="6b90c-140">设置网站菜单、布局和主页时需作少量更改。</span><span class="sxs-lookup"><span data-stu-id="6b90c-140">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="6b90c-141">打开 Pages/_Layout.cshtml 并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="6b90c-141">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="6b90c-142">将“ContosoUniversity”的每个匹配项都改为“Contoso University”。</span><span class="sxs-lookup"><span data-stu-id="6b90c-142">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="6b90c-143">共有三个匹配项。</span><span class="sxs-lookup"><span data-stu-id="6b90c-143">There are three occurrences.</span></span>

* <span data-ttu-id="6b90c-144">添加菜单项 **Students**，**Courses**，**Instructors**，和 **Department**，并删除 **Contact**菜单项。</span><span class="sxs-lookup"><span data-stu-id="6b90c-144">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="6b90c-145">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="6b90c-145">The changes are highlighted.</span></span> <span data-ttu-id="6b90c-146">（所有标记均不显示。）</span><span class="sxs-lookup"><span data-stu-id="6b90c-146">(All the markup is *not* displayed.)</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

<span data-ttu-id="6b90c-147">在 Pages/Index.cshtml 中，将文件内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关本应用的文本：</span><span class="sxs-lookup"><span data-stu-id="6b90c-147">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="6b90c-148">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="6b90c-148">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="6b90c-149">将显示主页以及后续教程中创建的标签：</span><span class="sxs-lookup"><span data-stu-id="6b90c-149">The home page is displayed with tabs created in the following tutorials:</span></span>

![Contoso University 主页](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="6b90c-151">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="6b90c-151">Create the data model</span></span>

<span data-ttu-id="6b90c-152">创建 Contoso University 应用的实体类。</span><span class="sxs-lookup"><span data-stu-id="6b90c-152">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="6b90c-153">从以下三个实体开始：</span><span class="sxs-lookup"><span data-stu-id="6b90c-153">Start with the following three entities:</span></span>

![Course-Enrollment-Student 数据模型关系图](intro/_static/data-model-diagram.png)

<span data-ttu-id="6b90c-155">`Student` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="6b90c-155">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="6b90c-156">`Course` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="6b90c-156">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="6b90c-157">一名学生可以报名参加任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="6b90c-157">A student can enroll in any number of courses.</span></span> <span data-ttu-id="6b90c-158">一门课程中可以包含任意数量的学生。</span><span class="sxs-lookup"><span data-stu-id="6b90c-158">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="6b90c-159">以下部分将为这几个实体中的每一个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="6b90c-159">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="6b90c-160">Student 实体</span><span class="sxs-lookup"><span data-stu-id="6b90c-160">The Student entity</span></span>

![Student 实体关系图](intro/_static/student-entity.png)

<span data-ttu-id="6b90c-162">创建 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6b90c-162">Create a *Models* folder.</span></span> <span data-ttu-id="6b90c-163">在 Models 文件夹中，使用以下代码创建一个名为 Student.cs 的类文件：</span><span class="sxs-lookup"><span data-stu-id="6b90c-163">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="6b90c-164">`ID` 属性成为此类对应的数据库 (DB) 表的主键列。</span><span class="sxs-lookup"><span data-stu-id="6b90c-164">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="6b90c-165">默认情况下，EF Core 将名为 `ID` 或 `classnameID` 的属性视为主键。</span><span class="sxs-lookup"><span data-stu-id="6b90c-165">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span> <span data-ttu-id="6b90c-166">`classnameID` 中的 `classname` 是类的名称，例如上述示例中的 `Student`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-166">In `classnameID`, `classname` is the name of the class, such as `Student` in the preceding example.</span></span>

<span data-ttu-id="6b90c-167">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="6b90c-167">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="6b90c-168">导航属性链接到与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-168">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="6b90c-169">在这种情况下，`Student entity` 的 `Enrollments` 属性包含与该 `Student` 相关的所有 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-169">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="6b90c-170">例如，如果数据库中的 Student 行有两个相关的 Enrollment 行，则 `Enrollments` 导航属性包含这两个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-170">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="6b90c-171">相关的 `Enrollment` 行是 `StudentID` 列中包含该学生的主键值的行。</span><span class="sxs-lookup"><span data-stu-id="6b90c-171">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="6b90c-172">例如，假设 ID=1 的学生在 `Enrollment` 表中有两行。</span><span class="sxs-lookup"><span data-stu-id="6b90c-172">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="6b90c-173">`Enrollment` 表中有两行的 `StudentID` = 1。</span><span class="sxs-lookup"><span data-stu-id="6b90c-173">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="6b90c-174">`StudentID` 是 `Enrollment` 表中的外键，用于指定 `Student` 表中的学生。</span><span class="sxs-lookup"><span data-stu-id="6b90c-174">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="6b90c-175">如果导航属性包含多个实体，则导航属性必须是列表类型，例如 `ICollection<T>`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-175">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="6b90c-176">可以指定 `ICollection<T>` 或诸如 `List<T>` 或 `HashSet<T>` 的类型。</span><span class="sxs-lookup"><span data-stu-id="6b90c-176">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="6b90c-177">使用 `ICollection<T>` 时，EF Core 会默认创建 `HashSet<T>` 集合。</span><span class="sxs-lookup"><span data-stu-id="6b90c-177">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="6b90c-178">包含多个实体的导航属性来自于多对多和一对多关系。</span><span class="sxs-lookup"><span data-stu-id="6b90c-178">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="6b90c-179">Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="6b90c-179">The Enrollment entity</span></span>

![Enrollment 实体关系图](intro/_static/enrollment-entity.png)

<span data-ttu-id="6b90c-181">在 Models 文件夹中，使用以下代码创建 Enrollment.cs：</span><span class="sxs-lookup"><span data-stu-id="6b90c-181">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="6b90c-182">`EnrollmentID` 属性为主键。</span><span class="sxs-lookup"><span data-stu-id="6b90c-182">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="6b90c-183">`Student` 实体使用的是 `ID` 模式，而本实体使用的是 `classnameID` 模式。</span><span class="sxs-lookup"><span data-stu-id="6b90c-183">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="6b90c-184">通常情况下，开发者会选择一种模式并在整个数据模型中都使用该模式。</span><span class="sxs-lookup"><span data-stu-id="6b90c-184">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="6b90c-185">下一个教程将介绍如何使用不带类名的 ID，以便更轻松地在数据模型中实现集成。</span><span class="sxs-lookup"><span data-stu-id="6b90c-185">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="6b90c-186">`Grade` 属性为 `enum`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-186">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="6b90c-187">`Grade` 声明类型后的`?`表示 `Grade` 属性可以为 null。</span><span class="sxs-lookup"><span data-stu-id="6b90c-187">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="6b90c-188">评级为 null 和评级为零是有区别的 --null 意味着评级未知或者尚未分配。</span><span class="sxs-lookup"><span data-stu-id="6b90c-188">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="6b90c-189">`StudentID` 属性是外键，其对应的导航属性为 `Student`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-189">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="6b90c-190">`Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含一个 `Student` 实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-190">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="6b90c-191">`Student` 实体与 `Student.Enrollments` 导航属性不同，后者包含多个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-191">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="6b90c-192">`CourseID` 属性是外键，其对应的导航属性为 `Course`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-192">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="6b90c-193">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="6b90c-193">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="6b90c-194">如果属性命名为 `<navigation property name><primary key property name>`，EF Core 会将其视为外键。</span><span class="sxs-lookup"><span data-stu-id="6b90c-194">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="6b90c-195">例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-195">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="6b90c-196">还可以将外键属性命名为 `<primary key property name>`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-196">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="6b90c-197">例如 `CourseID`，因为 `Course` 实体的主键为 `CourseID`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-197">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="6b90c-198">Course 实体</span><span class="sxs-lookup"><span data-stu-id="6b90c-198">The Course entity</span></span>

![Course 实体关系图](intro/_static/course-entity.png)

<span data-ttu-id="6b90c-200">在 Models 文件夹中，使用以下代码创建 Course.cs：</span><span class="sxs-lookup"><span data-stu-id="6b90c-200">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="6b90c-201">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="6b90c-201">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="6b90c-202">`Course` 实体可与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="6b90c-202">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="6b90c-203">应用可以通过 `DatabaseGenerated` 特性指定主键，而无需靠数据库生成。</span><span class="sxs-lookup"><span data-stu-id="6b90c-203">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="6b90c-204">创建 SchoolContext 数据库上下文</span><span class="sxs-lookup"><span data-stu-id="6b90c-204">Create the SchoolContext DB context</span></span>

<span data-ttu-id="6b90c-205">数据库上下文类是为给定数据模型协调 EF Core 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="6b90c-205">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="6b90c-206">数据上下文派生自 `Microsoft.EntityFrameworkCore.DbContext`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-206">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="6b90c-207">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-207">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="6b90c-208">在此项目中，类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-208">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="6b90c-209">在项目文件夹中，创建一个名为 Data 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="6b90c-209">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="6b90c-210">在 Data 文件夹中，使用以下代码创建 SchoolContext.cs：</span><span class="sxs-lookup"><span data-stu-id="6b90c-210">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="6b90c-211">此代码会为每个实体集创建一个 `DbSet` 属性。</span><span class="sxs-lookup"><span data-stu-id="6b90c-211">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="6b90c-212">在 EF Core 术语中：</span><span class="sxs-lookup"><span data-stu-id="6b90c-212">In EF Core terminology:</span></span>

* <span data-ttu-id="6b90c-213">实体集通常对应一个数据库表。</span><span class="sxs-lookup"><span data-stu-id="6b90c-213">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="6b90c-214">实体对应表中的行。</span><span class="sxs-lookup"><span data-stu-id="6b90c-214">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="6b90c-215">`DbSet<Enrollment>` 和 `DbSet<Course>` 可以省略。</span><span class="sxs-lookup"><span data-stu-id="6b90c-215">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="6b90c-216">EF Core 隐式包含了它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="6b90c-216">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="6b90c-217">在本教程中，将 `DbSet<Enrollment>` 和 `DbSet<Course>` 保留在 `SchoolContext` 中。</span><span class="sxs-lookup"><span data-stu-id="6b90c-217">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="6b90c-218">创建数据库时，EF Core 会创建名称与 `DbSet` 属性名相同的表。</span><span class="sxs-lookup"><span data-stu-id="6b90c-218">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="6b90c-219">集合的属性名通常采用复数形式（使用 Students，而不使用 Student）。</span><span class="sxs-lookup"><span data-stu-id="6b90c-219">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="6b90c-220">开发者对表名称是否应为复数形式意见不一。</span><span class="sxs-lookup"><span data-stu-id="6b90c-220">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="6b90c-221">在这些教程中，在 DbContext 中指定单数形式的表名称会覆盖默认行为。</span><span class="sxs-lookup"><span data-stu-id="6b90c-221">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="6b90c-222">若要指定单数形式的表名称，请添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="6b90c-222">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="6b90c-223">通过依赖关系注入注册上下文</span><span class="sxs-lookup"><span data-stu-id="6b90c-223">Register the context with dependency injection</span></span>

<span data-ttu-id="6b90c-224">ASP.NET Core 包含[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-224">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="6b90c-225">服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="6b90c-225">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="6b90c-226">需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="6b90c-226">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="6b90c-227">本教程的后续部分介绍了用于获取数据库上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="6b90c-227">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="6b90c-228">要将 `SchoolContext` 注册为服务，请打开 Startup.cs，并将突出显示的行添加到 `ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="6b90c-228">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="6b90c-229">通过调用 `DbContextOptionsBuilder` 中的一个方法将数据库连接字符串在配置文件中的名称传递给上下文对象。</span><span class="sxs-lookup"><span data-stu-id="6b90c-229">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="6b90c-230">进行本地开发时，[ASP.NET Core 配置系统](xref:fundamentals/configuration/index)会从 appsettings.json 文件读取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="6b90c-230">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="6b90c-231">为 `ContosoUniversity.Data` 和 `Microsoft.EntityFrameworkCore` 命名空间添加 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="6b90c-231">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="6b90c-232">生成项目。</span><span class="sxs-lookup"><span data-stu-id="6b90c-232">Build the project.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="6b90c-233">打开 appsettings.json 文件，并按以下代码所示添加连接字符串：</span><span class="sxs-lookup"><span data-stu-id="6b90c-233">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="6b90c-234">上述连接字符串使用 `ConnectRetryCount=0` 来防止 [SQLClient](/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) 挂起。</span><span class="sxs-lookup"><span data-stu-id="6b90c-234">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="6b90c-235">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="6b90c-235">SQL Server Express LocalDB</span></span>

<span data-ttu-id="6b90c-236">连接字符串指定 SQL Server LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-236">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="6b90c-237">LocalDB 是轻型版本 SQL Server Express 数据库引擎，专门针对应用开发，而非生产使用。</span><span class="sxs-lookup"><span data-stu-id="6b90c-237">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="6b90c-238">LocalDB 作为按需启动并在用户模式下运行的轻量级数据库没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="6b90c-238">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="6b90c-239">默认情况下，LocalDB 会在 `C:/Users/<user>` 目录中创建 .mdf 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="6b90c-239">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="6b90c-240">添加代码，以使用测试数据初始化该数据库</span><span class="sxs-lookup"><span data-stu-id="6b90c-240">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="6b90c-241">EF Core 会创建一个空的数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-241">EF Core creates an empty DB.</span></span> <span data-ttu-id="6b90c-242">本部分中编写了 Seed 方法来使用测试数据填充该数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-242">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="6b90c-243">在 Data 文件夹中，新建一个名为 DbInitializer.cs 的类文件，并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="6b90c-243">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="6b90c-244">该代码会检查数据库中是否存在任何学生。</span><span class="sxs-lookup"><span data-stu-id="6b90c-244">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="6b90c-245">如果数据库中没有任何学生，则会填充测试数据。</span><span class="sxs-lookup"><span data-stu-id="6b90c-245">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="6b90c-246">它会将测试数据加载到数组中，而不是 `List<T>` 集合中，以便优化性能。</span><span class="sxs-lookup"><span data-stu-id="6b90c-246">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="6b90c-247">`EnsureCreated` 方法自动为数据库上下文创建数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-247">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="6b90c-248">如果数据库已存在，则返回 `EnsureCreated`，并且不修改数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-248">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="6b90c-249">在 Program.cs 中，修改 `Main` 方法以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b90c-249">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="6b90c-250">从依赖关系注入容器获取数据库上下文实例。</span><span class="sxs-lookup"><span data-stu-id="6b90c-250">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="6b90c-251">调用 seed 方法，并将上下文传递给它。</span><span class="sxs-lookup"><span data-stu-id="6b90c-251">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="6b90c-252">Seed 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="6b90c-252">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="6b90c-253">下面的代码显示更新后的 Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="6b90c-253">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="6b90c-254">第一次运行该应用时，会使用测试数据创建并填充数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-254">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="6b90c-255">更新数据模型时：</span><span class="sxs-lookup"><span data-stu-id="6b90c-255">When the data model is updated:</span></span>
* <span data-ttu-id="6b90c-256">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-256">Delete the DB.</span></span>
* <span data-ttu-id="6b90c-257">更新 seed 方法。</span><span class="sxs-lookup"><span data-stu-id="6b90c-257">Update the seed method.</span></span>
* <span data-ttu-id="6b90c-258">运行该应用，并创建新的种子数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-258">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="6b90c-259">后续教程中，在更改数据模型时会更新该数据库，而不会删除并重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-259">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="6b90c-260">添加基架工具</span><span class="sxs-lookup"><span data-stu-id="6b90c-260">Add scaffold tooling</span></span>

<span data-ttu-id="6b90c-261">本部分中将使用包管理器控制台 (PMC) 来添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="6b90c-261">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="6b90c-262">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="6b90c-262">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="6b90c-263">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="6b90c-263">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="6b90c-264">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="6b90c-264">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="6b90c-265">前一个命令将 NuGet 包添加到 \*.csproj 文件中：</span><span class="sxs-lookup"><span data-stu-id="6b90c-265">The previous command adds the NuGet packages to the \*.csproj file:</span></span>

[!code-csharp[](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="6b90c-266">构架模型</span><span class="sxs-lookup"><span data-stu-id="6b90c-266">Scaffold the model</span></span>

* <span data-ttu-id="6b90c-267">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="6b90c-267">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="6b90c-268">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="6b90c-268">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```

<span data-ttu-id="6b90c-269">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="6b90c-269">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="6b90c-270">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="6b90c-270">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>


<span data-ttu-id="6b90c-271">生成项目。</span><span class="sxs-lookup"><span data-stu-id="6b90c-271">Build the project.</span></span> <span data-ttu-id="6b90c-272">此版本生成如下错误：</span><span class="sxs-lookup"><span data-stu-id="6b90c-272">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="6b90c-273">将 `_context.Student` 全局更改为 `_context.Students`（即向 `Student` 添加一个“s”）。</span><span class="sxs-lookup"><span data-stu-id="6b90c-273">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="6b90c-274">找到并更新 7 个匹配项。</span><span class="sxs-lookup"><span data-stu-id="6b90c-274">7 occurrences are found and updated.</span></span> <span data-ttu-id="6b90c-275">我们计划在下一版本中修复[此 bug](https://github.com/aspnet/Scaffolding/issues/633)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-275">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE [model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="6b90c-276">测试应用</span><span class="sxs-lookup"><span data-stu-id="6b90c-276">Test the app</span></span>

<span data-ttu-id="6b90c-277">运行应用并选择“学生”链接。</span><span class="sxs-lookup"><span data-stu-id="6b90c-277">Run the app and select the **Students** link.</span></span> <span data-ttu-id="6b90c-278">“学生”链接将显示在页面顶部，具体取决于浏览器宽度。</span><span class="sxs-lookup"><span data-stu-id="6b90c-278">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="6b90c-279">如果看不到“学生”链接，请单击右上角的导航图标。</span><span class="sxs-lookup"><span data-stu-id="6b90c-279">If the **Students** link isn't visible, click the navigation icon in the upper right corner.</span></span>

![Contoso University 主页宽窄](intro/_static/home-page-narrow.png)

<span data-ttu-id="6b90c-281">测试“创建”，“编辑”和“详细信息”链接。</span><span class="sxs-lookup"><span data-stu-id="6b90c-281">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="6b90c-282">查看数据库</span><span class="sxs-lookup"><span data-stu-id="6b90c-282">View the DB</span></span>

<span data-ttu-id="6b90c-283">启动应用时，`DbInitializer.Initialize` 会调用 `EnsureCreated`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-283">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="6b90c-284">`EnsureCreated` 检测数据库是否存在，并在必要时创建一个数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-284">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="6b90c-285">如果数据库中没有学生，`Initialize` 方法将添加学生。</span><span class="sxs-lookup"><span data-stu-id="6b90c-285">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="6b90c-286">从 Visual Studio 中的“视图”菜单打开 SQL Server 对象资源管理器 (SSOX)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-286">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="6b90c-287">在 SSOX 中，单击“(localdb)\MSSQLLocalDB”>“数据库”>“ContosoUniversity1”。</span><span class="sxs-lookup"><span data-stu-id="6b90c-287">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="6b90c-288">展开“表”节点。</span><span class="sxs-lookup"><span data-stu-id="6b90c-288">Expand the **Tables** node.</span></span>

<span data-ttu-id="6b90c-289">右键单击 Student 表，然后单击“查看数据”，以查看创建的列和插入到表中的行。</span><span class="sxs-lookup"><span data-stu-id="6b90c-289">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="6b90c-290">.mdf 和 .ldf 数据库文件位于 C:\Users\\<yourusername> 文件夹中<em></em>。</span><span class="sxs-lookup"><span data-stu-id="6b90c-290">The <em>.mdf</em> and <em>.ldf</em> DB files are in the <em>C:\Users\\<yourusername></em> folder.</span></span>

<span data-ttu-id="6b90c-291">启动应用时会调用 `EnsureCreated`，以进行以下工作流：</span><span class="sxs-lookup"><span data-stu-id="6b90c-291">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="6b90c-292">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-292">Delete the DB.</span></span>
* <span data-ttu-id="6b90c-293">更改数据库架构（例如添加一个 `EmailAddress` 字段）。</span><span class="sxs-lookup"><span data-stu-id="6b90c-293">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="6b90c-294">运行应用。</span><span class="sxs-lookup"><span data-stu-id="6b90c-294">Run the app.</span></span>

<span data-ttu-id="6b90c-295">`EnsureCreated` 创建一个带有 `EmailAddress` 列的数据库。</span><span class="sxs-lookup"><span data-stu-id="6b90c-295">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="6b90c-296">约定</span><span class="sxs-lookup"><span data-stu-id="6b90c-296">Conventions</span></span>

<span data-ttu-id="6b90c-297">因为使用了约定或 EF Core 所做的假设，为使 EF Core 创建完整数据库而编写的代码量是最小的。</span><span class="sxs-lookup"><span data-stu-id="6b90c-297">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="6b90c-298">使用 `DbSet` 属性的名称作为表名。</span><span class="sxs-lookup"><span data-stu-id="6b90c-298">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="6b90c-299">如果实体未被 `DbSet` 属性引用，实体类名称用作表名称。</span><span class="sxs-lookup"><span data-stu-id="6b90c-299">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="6b90c-300">使用实体属性名作为列名。</span><span class="sxs-lookup"><span data-stu-id="6b90c-300">Entity property names are used for column names.</span></span>

* <span data-ttu-id="6b90c-301">以 ID 或 classnameID 命名的实体属性被视为主键属性。</span><span class="sxs-lookup"><span data-stu-id="6b90c-301">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="6b90c-302">如果属性命名为 <navigation property name><primary key property name>，将视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。</span><span class="sxs-lookup"><span data-stu-id="6b90c-302">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="6b90c-303">可将外键属性命名为 <primary key property name>（例如 `EnrollmentID`，因为 `Enrollment` 实体的主键为 `EnrollmentID`）。</span><span class="sxs-lookup"><span data-stu-id="6b90c-303">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="6b90c-304">可以重写常规行为。</span><span class="sxs-lookup"><span data-stu-id="6b90c-304">Conventional behavior can be overridden.</span></span> <span data-ttu-id="6b90c-305">例如，可以显式指定表名，如本教程中前面部分所示。</span><span class="sxs-lookup"><span data-stu-id="6b90c-305">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="6b90c-306">可以显式设置列名。</span><span class="sxs-lookup"><span data-stu-id="6b90c-306">The column names can be explicitly set.</span></span> <span data-ttu-id="6b90c-307">可以显式设置主键和外键。</span><span class="sxs-lookup"><span data-stu-id="6b90c-307">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="6b90c-308">异步代码</span><span class="sxs-lookup"><span data-stu-id="6b90c-308">Asynchronous code</span></span>

<span data-ttu-id="6b90c-309">异步编程是 ASP.NET Core 和 EF Core 的默认模式。</span><span class="sxs-lookup"><span data-stu-id="6b90c-309">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="6b90c-310">Web 服务器的可用线程是有限的，而在高负载情况下的可能所有线程都被占用。</span><span class="sxs-lookup"><span data-stu-id="6b90c-310">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="6b90c-311">当发生这种情况的时候，服务器就无法处理新请求，直到线程被释放。</span><span class="sxs-lookup"><span data-stu-id="6b90c-311">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="6b90c-312">使用同步代码时，可能会出现多个线程被占用但不能执行任何操作的情况，因为它们正在等待 I/O 完成。</span><span class="sxs-lookup"><span data-stu-id="6b90c-312">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="6b90c-313">使用异步代码时，当进程正在等待 I/O 完成，服务器可以将其线程释放用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="6b90c-313">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="6b90c-314">因此，使用异步代码可以更有效地利用服务器资源，并且可以让服务器在没有延迟的情况下处理更多流量。</span><span class="sxs-lookup"><span data-stu-id="6b90c-314">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="6b90c-315">异步代码会在运行时引入少量开销。</span><span class="sxs-lookup"><span data-stu-id="6b90c-315">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="6b90c-316">流量较低时，对性能的影响可以忽略不计，但流量较高时，潜在的性能改善非常显著。</span><span class="sxs-lookup"><span data-stu-id="6b90c-316">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="6b90c-317">在以下代码中，`async` 关键字、`Task<T>` 返回值、`await` 关键字和 `ToListAsync` 方法让代码异步执行。</span><span class="sxs-lookup"><span data-stu-id="6b90c-317">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="6b90c-318">`async` 关键字让编译器执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b90c-318">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="6b90c-319">为方法主体的各部分生成回调。</span><span class="sxs-lookup"><span data-stu-id="6b90c-319">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="6b90c-320">自动创建返回的 [Task](/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 对象。</span><span class="sxs-lookup"><span data-stu-id="6b90c-320">Automatically create the [Task](/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that's returned.</span></span> <span data-ttu-id="6b90c-321">有关详细信息，请参阅[任务返回类型](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-321">For more information, see [Task Return Type](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="6b90c-322">隐式返回类型 `Task` 表示正在进行的工作。</span><span class="sxs-lookup"><span data-stu-id="6b90c-322">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="6b90c-323">`await` 关键字让编译器将该方法拆分为两个部分。</span><span class="sxs-lookup"><span data-stu-id="6b90c-323">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="6b90c-324">第一部分是以异步方式结束已启动的操作。</span><span class="sxs-lookup"><span data-stu-id="6b90c-324">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="6b90c-325">第二部分是当操作完成时注入调用回调方法的地方。</span><span class="sxs-lookup"><span data-stu-id="6b90c-325">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="6b90c-326">`ToListAsync` 是 `ToList` 扩展方法的异步版本。</span><span class="sxs-lookup"><span data-stu-id="6b90c-326">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="6b90c-327">编写使用 EF Core 的异步代码时需要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="6b90c-327">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="6b90c-328">只会异步执行导致查询或命令被发送到数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="6b90c-328">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="6b90c-329">这包括 `ToListAsync`、`SingleOrDefaultAsync`、`FirstOrDefaultAsync` 和 `SaveChangesAsync`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-329">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="6b90c-330">不包括只会更改 `IQueryable` 的语句，例如 `var students = context.Students.Where(s => s.LastName == "Davolio")`。</span><span class="sxs-lookup"><span data-stu-id="6b90c-330">It doesn't include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="6b90c-331">EF Core 上下文并非线程安全：请勿尝试并行执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="6b90c-331">An EF Core context isn't thread safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="6b90c-332">若要利用异步代码的性能优势，请验证在调用向数据库发送查询的 EF Core 方法时，库程序包（如用于分页）是否使用异步。</span><span class="sxs-lookup"><span data-stu-id="6b90c-332">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="6b90c-333">有关在 .NET 中进行异步编程的详细信息，请参阅[异步概述](/dotnet/articles/standard/async)。</span><span class="sxs-lookup"><span data-stu-id="6b90c-333">For more information about asynchronous programming in .NET, see [Async Overview](/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="6b90c-334">下一个教程将介绍基本的 CRUD（创建、读取、更新、删除）操作。</span><span class="sxs-lookup"><span data-stu-id="6b90c-334">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6b90c-335">下一篇</span><span class="sxs-lookup"><span data-stu-id="6b90c-335">Next</span></span>](xref:data/ef-rp/crud)
