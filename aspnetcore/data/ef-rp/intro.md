---
title: "Razor 页面和 Entity Framework Core - 第 1 个教程（共 8 个）"
author: rick-anderson
description: "介绍了如何使用 Entity Framework Core 创建 Razor 页面应用"
manager: wpickett
ms.author: riande
ms.date: 11/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/intro
ms.openlocfilehash: 091f34da347d52ba8e3e87779ddc4aeb790c2800
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a><span data-ttu-id="8be7c-103">Razor 页面和 Entity Framework Core 入门（使用 Visual Studio）（第 1 个教程，共 8 个）</span><span class="sxs-lookup"><span data-stu-id="8be7c-103">Getting started with Razor Pages and Entity Framework Core using Visual Studio (1 of 8)</span></span>

<span data-ttu-id="8be7c-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8be7c-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8be7c-105">Contoso University 示例 Web 应用演示了如何使用 Entity Framework (EF) Core 2.0 和 Visual Studio 2017 创建 ASP.NET Core 2.0 MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8be7c-105">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="8be7c-106">该示例应用是一个虚构的 Contoso University 的网站。</span><span class="sxs-lookup"><span data-stu-id="8be7c-106">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="8be7c-107">其中包括学生录取、课程创建和讲师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="8be7c-107">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="8be7c-108">本页是介绍如何构建 Contoso University 示例应用系列教程中的第一部分。</span><span class="sxs-lookup"><span data-stu-id="8be7c-108">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="8be7c-109">下载或查看已完成的应用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-109">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="8be7c-110">[下载说明](xref:tutorials/index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-110">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8be7c-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="8be7c-111">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

<span data-ttu-id="8be7c-112">熟悉 [Razor 页面](xref:mvc/razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-112">Familiarity with [Razor Pages](xref:mvc/razor-pages/index).</span></span> <span data-ttu-id="8be7c-113">新程序员在开始学习本系列之前，应先完成 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-113">New programmers should complete [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) before starting this series.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8be7c-114">疑难解答</span><span class="sxs-lookup"><span data-stu-id="8be7c-114">Troubleshooting</span></span>

<span data-ttu-id="8be7c-115">如果遇到无法解决的问题，通常可以通过将自己的代码与[已完成阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)或[已完成项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final)进行比较来寻找解决方案。</span><span class="sxs-lookup"><span data-stu-id="8be7c-115">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) or [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span></span> <span data-ttu-id="8be7c-116">有关常见错误列表及其解决办法，请参阅[本系列最后一个教程的疑难解答部分](xref:data/ef-mvc/advanced#common-errors)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-116">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="8be7c-117">如果在该处找不到所需内容，可以在 [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) 上发表有关 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 或 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core) 的问题。</span><span class="sxs-lookup"><span data-stu-id="8be7c-117">If you don't find what you need there, you can post a question to [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="8be7c-118">本系列教程以之前教程中已完成的工作为基础。</span><span class="sxs-lookup"><span data-stu-id="8be7c-118">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="8be7c-119">每次成功完成教程后，请考虑保存项目副本。</span><span class="sxs-lookup"><span data-stu-id="8be7c-119">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="8be7c-120">如果遇到问题，便可以从上一教程重新开始，而无需从头开始。</span><span class="sxs-lookup"><span data-stu-id="8be7c-120">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="8be7c-121">或者可以下载[已完成阶段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)并使用已完成阶段重新开始。</span><span class="sxs-lookup"><span data-stu-id="8be7c-121">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="8be7c-122">Contoso University Web 应用</span><span class="sxs-lookup"><span data-stu-id="8be7c-122">The Contoso University web app</span></span>

<span data-ttu-id="8be7c-123">这些教程中所构建的应用是一个基本的大学网站。</span><span class="sxs-lookup"><span data-stu-id="8be7c-123">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="8be7c-124">用户可以查看和更新学生、课程和讲师信息。</span><span class="sxs-lookup"><span data-stu-id="8be7c-124">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="8be7c-125">以下是在本教程中创建的几个屏幕。</span><span class="sxs-lookup"><span data-stu-id="8be7c-125">Here are a few of the screens created in the tutorial.</span></span>

![“学生索引”页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

<span data-ttu-id="8be7c-128">此网站的 UI 样式与内置模板生成的 UI 样式类似。</span><span class="sxs-lookup"><span data-stu-id="8be7c-128">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="8be7c-129">教程的重点是 EF Core 和 Razor 页面，而非 UI。</span><span class="sxs-lookup"><span data-stu-id="8be7c-129">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="8be7c-130">创建 Razor 页面 Web 应用</span><span class="sxs-lookup"><span data-stu-id="8be7c-130">Create a Razor Pages web app</span></span>

* <span data-ttu-id="8be7c-131">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="8be7c-131">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="8be7c-132">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8be7c-132">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="8be7c-133">将该项目命名为 ContosoUniversity 。</span><span class="sxs-lookup"><span data-stu-id="8be7c-133">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="8be7c-134">务必将该项目命名为 ContosoUniversity，以便复制/粘贴代码时命名空间相匹配。</span><span class="sxs-lookup"><span data-stu-id="8be7c-134">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="8be7c-135">![新建 ASP.NET Core Web 应用程序](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="8be7c-135">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="8be7c-136">在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="8be7c-136">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="8be7c-137">![Web 应用程序（Razor 页面）](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="8be7c-137">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="8be7c-138">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在运行（不附加调试器）</span><span class="sxs-lookup"><span data-stu-id="8be7c-138">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="8be7c-139">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="8be7c-139">Set up the site style</span></span>

<span data-ttu-id="8be7c-140">设置网站菜单、布局和主页时需作少量更改。</span><span class="sxs-lookup"><span data-stu-id="8be7c-140">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="8be7c-141">打开 Pages/_Layout.cshtml 并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="8be7c-141">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="8be7c-142">将“ContosoUniversity”的每个匹配项都改为“Contoso University”。</span><span class="sxs-lookup"><span data-stu-id="8be7c-142">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="8be7c-143">共有三个匹配项。</span><span class="sxs-lookup"><span data-stu-id="8be7c-143">There are three occurrences.</span></span>

* <span data-ttu-id="8be7c-144">添加 Students、Courses、Instructors 和 Departments 菜单项，并删除“联系人”菜单项。</span><span class="sxs-lookup"><span data-stu-id="8be7c-144">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="8be7c-145">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="8be7c-145">The changes are highlighted.</span></span> <span data-ttu-id="8be7c-146">（所有标记均不显示。）</span><span class="sxs-lookup"><span data-stu-id="8be7c-146">(All the markup is *not* displayed.)</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

<span data-ttu-id="8be7c-147">在 Pages/Index.cshtml 中，将文件内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关本应用的文本：</span><span class="sxs-lookup"><span data-stu-id="8be7c-147">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="8be7c-148">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="8be7c-148">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="8be7c-149">将显示主页以及后续教程中创建的标签：</span><span class="sxs-lookup"><span data-stu-id="8be7c-149">The home page is displayed with tabs created in the following tutorials:</span></span>

![Contoso University 主页](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="8be7c-151">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="8be7c-151">Create the data model</span></span>

<span data-ttu-id="8be7c-152">创建 Contoso University 应用的实体类。</span><span class="sxs-lookup"><span data-stu-id="8be7c-152">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="8be7c-153">从以下三个实体开始：</span><span class="sxs-lookup"><span data-stu-id="8be7c-153">Start with the following three entities:</span></span>

![Course-Enrollment-Student 数据模型关系图](intro/_static/data-model-diagram.png)

<span data-ttu-id="8be7c-155">`Student` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="8be7c-155">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="8be7c-156">`Course` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="8be7c-156">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="8be7c-157">一名学生可以报名参加任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="8be7c-157">A student can enroll in any number of courses.</span></span> <span data-ttu-id="8be7c-158">一门课程中可以包含任意数量的学生。</span><span class="sxs-lookup"><span data-stu-id="8be7c-158">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="8be7c-159">以下部分将为这几个实体中的每一个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="8be7c-159">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="8be7c-160">Student 实体</span><span class="sxs-lookup"><span data-stu-id="8be7c-160">The Student entity</span></span>

![Student 实体关系图](intro/_static/student-entity.png)

<span data-ttu-id="8be7c-162">创建 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="8be7c-162">Create a *Models* folder.</span></span> <span data-ttu-id="8be7c-163">在 Models 文件夹中，使用以下代码创建一个名为 Student.cs 的类文件：</span><span class="sxs-lookup"><span data-stu-id="8be7c-163">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="8be7c-164">`ID` 属性成为此类对应的数据库 (DB) 表的主键列。</span><span class="sxs-lookup"><span data-stu-id="8be7c-164">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="8be7c-165">默认情况下，EF Core 将名为 `ID` 或 `classnameID` 的属性视为主键。</span><span class="sxs-lookup"><span data-stu-id="8be7c-165">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="8be7c-166">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="8be7c-166">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="8be7c-167">导航属性链接到与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-167">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="8be7c-168">在这种情况下，`Student entity` 的 `Enrollments` 属性包含与该 `Student` 相关的所有 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-168">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="8be7c-169">例如，如果数据库中的 Student 行有两个相关的 Enrollment 行，则 `Enrollments` 导航属性包含这两个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-169">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="8be7c-170">相关的 `Enrollment` 行是 `StudentID` 列中包含该学生的主键值的行。</span><span class="sxs-lookup"><span data-stu-id="8be7c-170">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="8be7c-171">例如，假设 ID=1 的学生在 `Enrollment` 表中有两行。</span><span class="sxs-lookup"><span data-stu-id="8be7c-171">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="8be7c-172">`Enrollment` 表中有两行的 `StudentID` = 1。</span><span class="sxs-lookup"><span data-stu-id="8be7c-172">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="8be7c-173">`StudentID` 是 `Enrollment` 表中的外键，用于指定 `Student` 表中的学生。</span><span class="sxs-lookup"><span data-stu-id="8be7c-173">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="8be7c-174">如果导航属性包含多个实体，则导航属性必须是列表类型，例如 `ICollection<T>`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-174">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="8be7c-175">可以指定 `ICollection<T>` 或诸如 `List<T>` 或 `HashSet<T>` 的类型。</span><span class="sxs-lookup"><span data-stu-id="8be7c-175">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="8be7c-176">使用 `ICollection<T>` 时，EF Core 会默认创建 `HashSet<T>` 集合。</span><span class="sxs-lookup"><span data-stu-id="8be7c-176">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="8be7c-177">包含多个实体的导航属性来自于多对多和一对多关系。</span><span class="sxs-lookup"><span data-stu-id="8be7c-177">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="8be7c-178">Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="8be7c-178">The Enrollment entity</span></span>

![Enrollment 实体关系图](intro/_static/enrollment-entity.png)

<span data-ttu-id="8be7c-180">在 Models 文件夹中，使用以下代码创建 Enrollment.cs：</span><span class="sxs-lookup"><span data-stu-id="8be7c-180">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="8be7c-181">`EnrollmentID` 属性为主键。</span><span class="sxs-lookup"><span data-stu-id="8be7c-181">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="8be7c-182">`Student` 实体使用的是 `ID` 模式，而本实体使用的是 `classnameID` 模式。</span><span class="sxs-lookup"><span data-stu-id="8be7c-182">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="8be7c-183">通常情况下，开发者会选择一种模式并在整个数据模型中都使用该模式。</span><span class="sxs-lookup"><span data-stu-id="8be7c-183">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="8be7c-184">下一个教程将介绍如何使用不带类名的 ID，以便更轻松地在数据模型中实现集成。</span><span class="sxs-lookup"><span data-stu-id="8be7c-184">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="8be7c-185">`Grade` 属性为 `enum`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-185">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="8be7c-186">`Grade` 类型声明后的问号表明 `Grade` 属性可为 NULL。</span><span class="sxs-lookup"><span data-stu-id="8be7c-186">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="8be7c-187">为 NULL 的年级与零年级不同，NULL 意味着该年级未知或尚未分配。</span><span class="sxs-lookup"><span data-stu-id="8be7c-187">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="8be7c-188">`StudentID` 属性是外键，其对应的导航属性为 `Student`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-188">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="8be7c-189">`Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含一个 `Student` 实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-189">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="8be7c-190">`Student` 实体与 `Student.Enrollments` 导航属性不同，后者包含多个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-190">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="8be7c-191">`CourseID` 属性是外键，其对应的导航属性为 `Course`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-191">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="8be7c-192">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="8be7c-192">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="8be7c-193">如果属性命名为 `<navigation property name><primary key property name>`，EF Core 会将其视为外键。</span><span class="sxs-lookup"><span data-stu-id="8be7c-193">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="8be7c-194">例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-194">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="8be7c-195">还可以将外键属性命名为 `<primary key property name>`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-195">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="8be7c-196">例如 `CourseID`，因为 `Course` 实体的主键为 `CourseID`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-196">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="8be7c-197">Course 实体</span><span class="sxs-lookup"><span data-stu-id="8be7c-197">The Course entity</span></span>

![Course 实体关系图](intro/_static/course-entity.png)

<span data-ttu-id="8be7c-199">在 Models 文件夹中，使用以下代码创建 Course.cs：</span><span class="sxs-lookup"><span data-stu-id="8be7c-199">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="8be7c-200">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="8be7c-200">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="8be7c-201">`Course` 实体可与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="8be7c-201">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="8be7c-202">应用可以通过 `DatabaseGenerated` 特性指定主键，而无需靠数据库生成。</span><span class="sxs-lookup"><span data-stu-id="8be7c-202">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="8be7c-203">创建 SchoolContext 数据库上下文</span><span class="sxs-lookup"><span data-stu-id="8be7c-203">Create the SchoolContext DB context</span></span>

<span data-ttu-id="8be7c-204">数据库上下文类是为给定数据模型协调 EF Core 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="8be7c-204">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="8be7c-205">数据上下文派生自 `Microsoft.EntityFrameworkCore.DbContext`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-205">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="8be7c-206">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-206">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="8be7c-207">在此项目中，类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-207">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="8be7c-208">在项目文件夹中，创建一个名为 Data 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8be7c-208">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="8be7c-209">在 Data 文件夹中，使用以下代码创建 SchoolContext.cs：</span><span class="sxs-lookup"><span data-stu-id="8be7c-209">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="8be7c-210">此代码会为每个实体集创建一个 `DbSet` 属性。</span><span class="sxs-lookup"><span data-stu-id="8be7c-210">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="8be7c-211">在 EF Core 术语中：</span><span class="sxs-lookup"><span data-stu-id="8be7c-211">In EF Core terminology:</span></span>

* <span data-ttu-id="8be7c-212">实体集通常对应一个数据库表。</span><span class="sxs-lookup"><span data-stu-id="8be7c-212">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="8be7c-213">实体对应表中的行。</span><span class="sxs-lookup"><span data-stu-id="8be7c-213">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="8be7c-214">`DbSet<Enrollment>` 和 `DbSet<Course>` 可以省略。</span><span class="sxs-lookup"><span data-stu-id="8be7c-214">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="8be7c-215">EF Core 隐式包含了它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="8be7c-215">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="8be7c-216">在本教程中，将 `DbSet<Enrollment>` 和 `DbSet<Course>` 保留在 `SchoolContext` 中。</span><span class="sxs-lookup"><span data-stu-id="8be7c-216">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="8be7c-217">创建数据库时，EF Core 会创建名称与 `DbSet` 属性名相同的表。</span><span class="sxs-lookup"><span data-stu-id="8be7c-217">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="8be7c-218">集合的属性名通常采用复数形式（使用 Students，而不使用 Student）。</span><span class="sxs-lookup"><span data-stu-id="8be7c-218">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="8be7c-219">开发者对表名称是否应为复数形式意见不一。</span><span class="sxs-lookup"><span data-stu-id="8be7c-219">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="8be7c-220">在这些教程中，在 DbContext 中指定单数形式的表名称会覆盖默认行为。</span><span class="sxs-lookup"><span data-stu-id="8be7c-220">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="8be7c-221">若要指定单数形式的表名称，请添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="8be7c-221">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="8be7c-222">通过依赖关系注入注册上下文</span><span class="sxs-lookup"><span data-stu-id="8be7c-222">Register the context with dependency injection</span></span>

<span data-ttu-id="8be7c-223">ASP.NET Core 包含[依赖关系注入](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-223">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="8be7c-224">服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="8be7c-224">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="8be7c-225">需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="8be7c-225">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="8be7c-226">本教程的后续部分介绍了用于获取数据库上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="8be7c-226">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="8be7c-227">要将 `SchoolContext` 注册为服务，请打开 Startup.cs，并将突出显示的行添加到 `ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="8be7c-227">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="8be7c-228">通过调用 `DbContextOptionsBuilder` 对象上的方法，可将连接字符串的名称传递给上下文。</span><span class="sxs-lookup"><span data-stu-id="8be7c-228">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="8be7c-229">进行本地开发时，[ASP.NET Core 配置系统](xref:fundamentals/configuration/index)会从 appsettings.json 文件读取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="8be7c-229">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="8be7c-230">为 `ContosoUniversity.Data` 和 `Microsoft.EntityFrameworkCore` 命名空间添加 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="8be7c-230">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="8be7c-231">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8be7c-231">Build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="8be7c-232">打开 appsettings.json 文件，并按以下代码所示添加连接字符串：</span><span class="sxs-lookup"><span data-stu-id="8be7c-232">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="8be7c-233">上述连接字符串使用 `ConnectRetryCount=0` 来防止 [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) 挂起。</span><span class="sxs-lookup"><span data-stu-id="8be7c-233">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="8be7c-234">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="8be7c-234">SQL Server Express LocalDB</span></span>

<span data-ttu-id="8be7c-235">连接字符串指定 SQL Server LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-235">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="8be7c-236">LocalDB 是轻型版本 SQL Server Express 数据库引擎，专门针对应用开发，而非生产使用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-236">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="8be7c-237">LocalDB 按需启动并在用户模式下运行，因此没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="8be7c-237">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="8be7c-238">默认情况下，LocalDB 会在 `C:/Users/<user>` 目录中创建 .mdf 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="8be7c-238">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="8be7c-239">添加代码，以使用测试数据初始化该数据库</span><span class="sxs-lookup"><span data-stu-id="8be7c-239">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="8be7c-240">EF Core 会创建一个空的数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-240">EF Core creates an empty DB.</span></span> <span data-ttu-id="8be7c-241">本部分中编写了 Seed 方法来使用测试数据填充该数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-241">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="8be7c-242">在 Data 文件夹中，新建一个名为 DbInitializer.cs 的类文件，并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="8be7c-242">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="8be7c-243">该代码会检查数据库中是否存在任何学生。</span><span class="sxs-lookup"><span data-stu-id="8be7c-243">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="8be7c-244">如果数据库中没有任何学生，则会填充测试数据。</span><span class="sxs-lookup"><span data-stu-id="8be7c-244">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="8be7c-245">它会将测试数据加载到数组中，而不是 `List<T>` 集合中，以便优化性能。</span><span class="sxs-lookup"><span data-stu-id="8be7c-245">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="8be7c-246">`EnsureCreated` 方法自动为数据库上下文创建数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-246">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="8be7c-247">如果数据库已存在，则返回 `EnsureCreated`，并且不修改数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-247">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="8be7c-248">在 Program.cs 中，修改 `Main` 方法以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8be7c-248">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="8be7c-249">从依赖关系注入容器获取数据库上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8be7c-249">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="8be7c-250">调用 seed 方法，并将上下文传递给它。</span><span class="sxs-lookup"><span data-stu-id="8be7c-250">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="8be7c-251">Seed 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="8be7c-251">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="8be7c-252">下面的代码显示更新后的 Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="8be7c-252">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="8be7c-253">第一次运行该应用时，会使用测试数据创建并填充数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-253">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="8be7c-254">更新数据模型时：</span><span class="sxs-lookup"><span data-stu-id="8be7c-254">When the data model is updated:</span></span>
* <span data-ttu-id="8be7c-255">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-255">Delete the DB.</span></span>
* <span data-ttu-id="8be7c-256">更新 seed 方法。</span><span class="sxs-lookup"><span data-stu-id="8be7c-256">Update the seed method.</span></span>
* <span data-ttu-id="8be7c-257">运行该应用，并创建新的种子数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-257">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="8be7c-258">后续教程中，在更改数据模型时会更新该数据库，而不会删除并重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-258">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="8be7c-259">添加基架工具</span><span class="sxs-lookup"><span data-stu-id="8be7c-259">Add scaffold tooling</span></span>

<span data-ttu-id="8be7c-260">本部分中将使用包管理器控制台 (PMC) 来添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="8be7c-260">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="8be7c-261">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="8be7c-261">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="8be7c-262">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="8be7c-262">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="8be7c-263">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="8be7c-263">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="8be7c-264">前一个命令将 NuGet 包添加到 \*.csproj 文件中：</span><span class="sxs-lookup"><span data-stu-id="8be7c-264">The previous command adds the NuGet packages to the \*.csproj file:</span></span>

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="8be7c-265">构架模型</span><span class="sxs-lookup"><span data-stu-id="8be7c-265">Scaffold the model</span></span>

* <span data-ttu-id="8be7c-266">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="8be7c-266">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="8be7c-267">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8be7c-267">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
<span data-ttu-id="8be7c-268">如果生成以下错误：</span><span class="sxs-lookup"><span data-stu-id="8be7c-268">If the following error is generated:</span></span>

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

<span data-ttu-id="8be7c-269">再次运行该命令，并在页面底部添加批注。</span><span class="sxs-lookup"><span data-stu-id="8be7c-269">Run the command again and leave a comment at the bottom of the page.</span></span>

<span data-ttu-id="8be7c-270">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="8be7c-270">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="8be7c-271">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="8be7c-271">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>


<span data-ttu-id="8be7c-272">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8be7c-272">Build the project.</span></span> <span data-ttu-id="8be7c-273">此版本生成如下错误：</span><span class="sxs-lookup"><span data-stu-id="8be7c-273">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="8be7c-274">将 `_context.Student` 全局更改为 `_context.Students`（即向 `Student` 添加一个“s”）。</span><span class="sxs-lookup"><span data-stu-id="8be7c-274">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="8be7c-275">找到并更新 7 个匹配项。</span><span class="sxs-lookup"><span data-stu-id="8be7c-275">7 occurrences are found and updated.</span></span> <span data-ttu-id="8be7c-276">我们计划在下一版本中修复[此 bug](https://github.com/aspnet/Scaffolding/issues/633)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-276">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="8be7c-277">测试应用</span><span class="sxs-lookup"><span data-stu-id="8be7c-277">Test the app</span></span>

<span data-ttu-id="8be7c-278">运行应用并选择“学生”链接。</span><span class="sxs-lookup"><span data-stu-id="8be7c-278">Run the app and select the **Students** link.</span></span> <span data-ttu-id="8be7c-279">“学生”链接将显示在页面顶部，具体取决于浏览器宽度。</span><span class="sxs-lookup"><span data-stu-id="8be7c-279">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="8be7c-280">如果看不到“学生”链接，请单击右上角的导航图标。</span><span class="sxs-lookup"><span data-stu-id="8be7c-280">If the **Students** link isn't visible, click the navigation icon in the upper right corner.</span></span>

![Contoso University 主页宽窄](intro/_static/home-page-narrow.png)

<span data-ttu-id="8be7c-282">测试“创建”，“编辑”和“详细信息”链接。</span><span class="sxs-lookup"><span data-stu-id="8be7c-282">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="8be7c-283">查看数据库</span><span class="sxs-lookup"><span data-stu-id="8be7c-283">View the DB</span></span>

<span data-ttu-id="8be7c-284">启动应用时，`DbInitializer.Initialize` 会调用 `EnsureCreated`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-284">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="8be7c-285">`EnsureCreated` 检测数据库是否存在，并在必要时创建一个数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-285">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="8be7c-286">如果数据库中没有学生，`Initialize` 方法将添加学生。</span><span class="sxs-lookup"><span data-stu-id="8be7c-286">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="8be7c-287">从 Visual Studio 中的“视图”菜单打开 SQL Server 对象资源管理器 (SSOX)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-287">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="8be7c-288">在 SSOX 中，单击“(localdb)\MSSQLLocalDB”>“数据库”>“ContosoUniversity1”。</span><span class="sxs-lookup"><span data-stu-id="8be7c-288">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="8be7c-289">展开“表”节点。</span><span class="sxs-lookup"><span data-stu-id="8be7c-289">Expand the **Tables** node.</span></span>

<span data-ttu-id="8be7c-290">右键单击 Student 表，然后单击“查看数据”，以查看创建的列和插入到表中的行。</span><span class="sxs-lookup"><span data-stu-id="8be7c-290">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="8be7c-291">.mdf 和 .ldf 数据库文件位于 C:\Users\\<yourusername> 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8be7c-291">The *.mdf* and *.ldf* DB files are in the *C:\Users\\<yourusername>* folder.</span></span>

<span data-ttu-id="8be7c-292">启动应用时会调用 `EnsureCreated`，以进行以下工作流：</span><span class="sxs-lookup"><span data-stu-id="8be7c-292">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="8be7c-293">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-293">Delete the DB.</span></span>
* <span data-ttu-id="8be7c-294">更改数据库架构（例如添加一个 `EmailAddress` 字段）。</span><span class="sxs-lookup"><span data-stu-id="8be7c-294">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="8be7c-295">运行应用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-295">Run the app.</span></span>

<span data-ttu-id="8be7c-296">`EnsureCreated` 创建一个带有 `EmailAddress` 列的数据库。</span><span class="sxs-lookup"><span data-stu-id="8be7c-296">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="8be7c-297">约定</span><span class="sxs-lookup"><span data-stu-id="8be7c-297">Conventions</span></span>

<span data-ttu-id="8be7c-298">因为使用了约定或 EF Core 所做的假设，为使 EF Core 创建完整数据库而编写的代码量是最小的。</span><span class="sxs-lookup"><span data-stu-id="8be7c-298">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="8be7c-299">使用 `DbSet` 属性的名称作为表名。</span><span class="sxs-lookup"><span data-stu-id="8be7c-299">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="8be7c-300">若是未被 `DbSet` 属性引用的实体，则使用实体类名作为表名。</span><span class="sxs-lookup"><span data-stu-id="8be7c-300">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="8be7c-301">使用实体属性名作为列名。</span><span class="sxs-lookup"><span data-stu-id="8be7c-301">Entity property names are used for column names.</span></span>

* <span data-ttu-id="8be7c-302">以 ID 或 classnameID 命名的实体属性被视为主键属性。</span><span class="sxs-lookup"><span data-stu-id="8be7c-302">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="8be7c-303">如果属性命名为 <navigation property name><primary key property name>，将视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。</span><span class="sxs-lookup"><span data-stu-id="8be7c-303">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="8be7c-304">可将外键属性命名为 <primary key property name>（例如 `EnrollmentID`，因为 `Enrollment` 实体的主键为 `EnrollmentID`）。</span><span class="sxs-lookup"><span data-stu-id="8be7c-304">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="8be7c-305">可以重写常规行为。</span><span class="sxs-lookup"><span data-stu-id="8be7c-305">Conventional behavior can be overridden.</span></span> <span data-ttu-id="8be7c-306">例如，可以显式指定表名，如本教程中前面部分所示。</span><span class="sxs-lookup"><span data-stu-id="8be7c-306">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="8be7c-307">可以显式设置列名。</span><span class="sxs-lookup"><span data-stu-id="8be7c-307">The column names can be explicitly set.</span></span> <span data-ttu-id="8be7c-308">可以显式设置主键和外键。</span><span class="sxs-lookup"><span data-stu-id="8be7c-308">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="8be7c-309">异步代码</span><span class="sxs-lookup"><span data-stu-id="8be7c-309">Asynchronous code</span></span>

<span data-ttu-id="8be7c-310">异步编程是 ASP.NET Core 和 EF Core 的默认模式。</span><span class="sxs-lookup"><span data-stu-id="8be7c-310">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="8be7c-311">Web 服务器可用的线程数量有限，在高负载情况下，所有可用的线程可能都正在使用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-311">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="8be7c-312">在这种情况下，线程释放之前，服务器无法处理新的请求。</span><span class="sxs-lookup"><span data-stu-id="8be7c-312">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="8be7c-313">若使用同步代码，许多线程在等待 I/O 完成时实际上并未执行任何操作，但仍被占用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-313">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="8be7c-314">若使用异步代码，进程在等待 I/O 完成时其线程会被释放，以便服务器用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="8be7c-314">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="8be7c-315">因此，使用异步代码可以更有效地利用服务器资源，并且可以让服务器在没有延迟的情况下处理更多流量。</span><span class="sxs-lookup"><span data-stu-id="8be7c-315">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="8be7c-316">异步代码会在运行时引入少量开销。</span><span class="sxs-lookup"><span data-stu-id="8be7c-316">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="8be7c-317">流量较低时，对性能的影响可以忽略不计，但流量较高时，潜在的性能改善非常显著。</span><span class="sxs-lookup"><span data-stu-id="8be7c-317">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="8be7c-318">在以下代码中，`async` 关键字、`Task<T>` 返回值、`await` 关键字和 `ToListAsync` 方法让代码异步执行。</span><span class="sxs-lookup"><span data-stu-id="8be7c-318">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="8be7c-319">`async` 关键字让编译器执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8be7c-319">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="8be7c-320">为方法主体的各部分生成回调。</span><span class="sxs-lookup"><span data-stu-id="8be7c-320">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="8be7c-321">自动创建返回的 [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 对象。</span><span class="sxs-lookup"><span data-stu-id="8be7c-321">Automatically create the [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that's returned.</span></span> <span data-ttu-id="8be7c-322">有关详细信息，请参阅[任务返回类型](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-322">For more information, see [Task Return Type](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="8be7c-323">隐式返回类型 `Task` 表示正在进行的工作。</span><span class="sxs-lookup"><span data-stu-id="8be7c-323">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="8be7c-324">`await` 关键字让编译器将该方法拆分为两个部分。</span><span class="sxs-lookup"><span data-stu-id="8be7c-324">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="8be7c-325">第一部分以异步方式启动的操作结束。</span><span class="sxs-lookup"><span data-stu-id="8be7c-325">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="8be7c-326">第二部分被放入一个回调方法中，当操作完成时调用。</span><span class="sxs-lookup"><span data-stu-id="8be7c-326">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="8be7c-327">`ToListAsync` 是 `ToList` 扩展方法的异步版本。</span><span class="sxs-lookup"><span data-stu-id="8be7c-327">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="8be7c-328">编写使用 EF Core 的异步代码时需要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="8be7c-328">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="8be7c-329">只会异步执行导致查询或命令被发送到数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="8be7c-329">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="8be7c-330">这包括 `ToListAsync`、`SingleOrDefaultAsync`、`FirstOrDefaultAsync` 和 `SaveChangesAsync`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-330">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="8be7c-331">不包括只会更改 `IQueryable` 的语句，例如 `var students = context.Students.Where(s => s.LastName == "Davolio")`。</span><span class="sxs-lookup"><span data-stu-id="8be7c-331">It doesn't include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="8be7c-332">EF Core 上下文并非线程安全：请勿尝试并行执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="8be7c-332">An EF Core context isn't thread safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="8be7c-333">若要利用异步代码的性能优势，请验证在调用向数据库发送查询的 EF Core 方法时，库程序包（如用于分页）是否使用异步。</span><span class="sxs-lookup"><span data-stu-id="8be7c-333">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="8be7c-334">有关在 .NET 中进行异步编程的详细信息，请参阅[异步概述](https://docs.microsoft.com/dotnet/articles/standard/async)。</span><span class="sxs-lookup"><span data-stu-id="8be7c-334">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="8be7c-335">下一个教程将介绍基本的 CRUD（创建、读取、更新、删除）操作。</span><span class="sxs-lookup"><span data-stu-id="8be7c-335">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="8be7c-336">下一篇</span><span class="sxs-lookup"><span data-stu-id="8be7c-336">Next</span></span>](xref:data/ef-rp/crud)
