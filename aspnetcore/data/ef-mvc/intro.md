---
title: "ASP.NET Core MVC 和 Entity Framework Core - 第 1 个教程，共 10 个教程"
author: tdykstra
description: 
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/intro
ms.openlocfilehash: 7de43a390ee0e11f6eda811b0774343ab330c53b
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-entity-framework-core-using-visual-studio-1-of-10"></a><span data-ttu-id="4a392-102">ASP.NET Core MVC 和 Entity Framework Core 入门（使用 Visual Studio）（第 1 个教程，共 10 个）</span><span class="sxs-lookup"><span data-stu-id="4a392-102">Getting started with ASP.NET Core MVC and Entity Framework Core using Visual Studio (1 of 10)</span></span>

<span data-ttu-id="4a392-103">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4a392-103">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4a392-104">[此处](xref:data/ef-rp/intro)提供了本教程的 Razor 页面版本。</span><span class="sxs-lookup"><span data-stu-id="4a392-104">A Razor Pages version of this tutorial is available [here](xref:data/ef-rp/intro).</span></span> <span data-ttu-id="4a392-105">Razor 页面版本更加通俗易懂，并介绍了更多 EF 功能。</span><span class="sxs-lookup"><span data-stu-id="4a392-105">The Razor Pages version is easier to follow and covers more EF features.</span></span> <span data-ttu-id="4a392-106">建议阅读[本教程的 Razor 页面版本](xref:data/ef-rp/intro)。</span><span class="sxs-lookup"><span data-stu-id="4a392-106">We recommend you follow the [Razor Pages version of this tutorial](xref:data/ef-rp/intro).</span></span>

<span data-ttu-id="4a392-107">Contoso University 示例 Web 应用程序演示如何使用 Entity Framework (EF) Core 2.0 和 Visual Studio 2017 创建 ASP.NET Core 2.0 MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a392-107">The Contoso University sample web application demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="4a392-108">该示例应用程序是一个虚构的 Contoso University 的网站。</span><span class="sxs-lookup"><span data-stu-id="4a392-108">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="4a392-109">其中包括学生录取、课程创建和讲师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="4a392-109">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="4a392-110">本页是介绍如何从头开始生成 Contoso University 示例应用系列教程中的第一部分。</span><span class="sxs-lookup"><span data-stu-id="4a392-110">This is the first in a series of tutorials that explain how to build the Contoso University sample application from scratch.</span></span>

[<span data-ttu-id="4a392-111">下载或查看已完成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a392-111">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

<span data-ttu-id="4a392-112">EF Core 2.0 是 EF 的最新版本，但尚不具有 EF 6.x 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="4a392-112">EF Core 2.0 is the latest version of EF but doesn't yet have all the features of EF 6.x.</span></span> <span data-ttu-id="4a392-113">有关选择 EF 6.x 还是 EF Core 的信息，请参阅 [比较 EF Core 和EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/)。</span><span class="sxs-lookup"><span data-stu-id="4a392-113">For information about how to choose between EF 6.x and EF Core, see [EF Core vs. EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/).</span></span> <span data-ttu-id="4a392-114">如果选择 EF 6.x，请参阅[本系列教程的上一版本](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。</span><span class="sxs-lookup"><span data-stu-id="4a392-114">If you choose EF 6.x, see [the previous version of this tutorial series](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

> [!NOTE]
> * <span data-ttu-id="4a392-115">有关本教程的 ASP.NET Core 1.1 版本信息，请参阅 [本教程的 VS 2017 第 2 次更新版本（PDF 格式）](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/ef-mvc/intro/_static/efmvc1.1.pdf)。</span><span class="sxs-lookup"><span data-stu-id="4a392-115">For the ASP.NET Core 1.1 version of this tutorial, see the [VS 2017 Update 2 version of this tutorial in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/ef-mvc/intro/_static/efmvc1.1.pdf).</span></span>
> * <span data-ttu-id="4a392-116">有关本教程的 Visual Studio 2015 版本，请参阅 [PDF 格式的 ASP.NET Core 文档的 VS 2015 版本](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf)。</span><span class="sxs-lookup"><span data-stu-id="4a392-116">For the Visual Studio 2015 version of this tutorial, see the [VS 2015 version of ASP.NET Core documentation in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a392-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="4a392-117">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="4a392-118">疑难解答</span><span class="sxs-lookup"><span data-stu-id="4a392-118">Troubleshooting</span></span>

<span data-ttu-id="4a392-119">如果遇到无法解决的问题，通常可以通过将自己的代码与[已完成项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)进行比较来寻找解决方案。</span><span class="sxs-lookup"><span data-stu-id="4a392-119">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final).</span></span> <span data-ttu-id="4a392-120">有关常见错误列表及其解决办法，请参阅[本系列最后一个教程的疑难解答部分](advanced.md#common-errors)。</span><span class="sxs-lookup"><span data-stu-id="4a392-120">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](advanced.md#common-errors).</span></span> <span data-ttu-id="4a392-121">如果在该处找不到所需内容，可以在 StackOverflow.com 上发表有关 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 或 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core) 的问题。</span><span class="sxs-lookup"><span data-stu-id="4a392-121">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP] 
> <span data-ttu-id="4a392-122">本系列共 10 个教程，每个教程都以上一个教程为基础。</span><span class="sxs-lookup"><span data-stu-id="4a392-122">This is a series of 10 tutorials, each of which builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="4a392-123">每次成功完成教程后，请考虑保存项目副本。</span><span class="sxs-lookup"><span data-stu-id="4a392-123">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="4a392-124">这样，如果遇到问题，便可以从上一教程重新开始，而无需从整个系列从头开始。</span><span class="sxs-lookup"><span data-stu-id="4a392-124">Then if you run into problems, you can start over from the previous tutorial instead of going back to the beginning of the whole series.</span></span>

## <a name="the-contoso-university-web-application"></a><span data-ttu-id="4a392-125">Contoso University Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="4a392-125">The Contoso University web application</span></span>

<span data-ttu-id="4a392-126">将在这些教程中构建的应用程序是一个简单的大学网站。</span><span class="sxs-lookup"><span data-stu-id="4a392-126">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="4a392-127">用户可以查看和更新学生、课程和讲师信息。</span><span class="sxs-lookup"><span data-stu-id="4a392-127">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="4a392-128">以下是你将创建的几个屏幕。</span><span class="sxs-lookup"><span data-stu-id="4a392-128">Here are a few of the screens you'll create.</span></span>

![“学生索引”页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

<span data-ttu-id="4a392-131">该网站的 UI 样式与通过内置模板生成的 UI 样式十分接近，因此本教程主要着重介绍如何使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="4a392-131">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="create-an-aspnet-core-mvc-web-application"></a><span data-ttu-id="4a392-132">创建 ASP.NET Core MVC Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="4a392-132">Create an ASP.NET Core MVC web application</span></span>

<span data-ttu-id="4a392-133">打开 Visual Studio 并创建名为“ContosoUniversity”的新 ASP.NET Core C# Web 项目。</span><span class="sxs-lookup"><span data-stu-id="4a392-133">Open Visual Studio and create a new ASP.NET Core C# web project named "ContosoUniversity".</span></span>

* <span data-ttu-id="4a392-134">从“文件”菜单中选择“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="4a392-134">From the **File** menu, select **New > Project**.</span></span>

* <span data-ttu-id="4a392-135">从左窗格中依次选择“已安装”>“Visual C#”>“Web”。</span><span class="sxs-lookup"><span data-stu-id="4a392-135">From the left pane, select **Installed > Visual C# > Web**.</span></span>

* <span data-ttu-id="4a392-136">选择“ASP.NET Core Web 应用程序”项目模板。</span><span class="sxs-lookup"><span data-stu-id="4a392-136">Select the **ASP.NET Core Web Application** project template.</span></span>

* <span data-ttu-id="4a392-137">输入“ContosoUniversity”作为名称，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="4a392-137">Enter **ContosoUniversity** as the name and click **OK**.</span></span>

  ![“新建项目”对话框](intro/_static/new-project.png)

* <span data-ttu-id="4a392-139">等待“新建 ASP.NET Core Web 应用程序(.NET Core)”对话框显示出来</span><span class="sxs-lookup"><span data-stu-id="4a392-139">Wait for the **New ASP.NET Core Web Application (.NET Core)** dialog to appear</span></span>

* <span data-ttu-id="4a392-140">选择“ASP.NET Core 2.0”和“Web 应用程序（模型视图控制器）”模板。</span><span class="sxs-lookup"><span data-stu-id="4a392-140">Select **ASP.NET Core 2.0** and the **Web Application (Model-View-Controller)** template.</span></span>

  <span data-ttu-id="4a392-141">注意：本教程需要 ASP.NET Core 2.0 和 EF Core 2.0 或更高版本，确保未选择 ASP.NET Core 1.1。</span><span class="sxs-lookup"><span data-stu-id="4a392-141">**Note:** This tutorial requires ASP.NET Core 2.0 and EF Core 2.0 or later -- make sure that **ASP.NET Core 1.1** isn't selected.</span></span>

* <span data-ttu-id="4a392-142">确保将“身份验证”设置为“无身份验证”。</span><span class="sxs-lookup"><span data-stu-id="4a392-142">Make sure **Authentication** is set to **No Authentication**.</span></span>

* <span data-ttu-id="4a392-143">单击“确定” </span><span class="sxs-lookup"><span data-stu-id="4a392-143">Click **OK**</span></span>

  ![“新建 ASP.NET 项目”对话框](intro/_static/new-aspnet.png)

## <a name="set-up-the-site-style"></a><span data-ttu-id="4a392-145">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="4a392-145">Set up the site style</span></span>

<span data-ttu-id="4a392-146">设置网站菜单、布局和主页时需作少量简单更改。</span><span class="sxs-lookup"><span data-stu-id="4a392-146">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="4a392-147">打开 Views/Shared/_Layout.cshtml 并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="4a392-147">Open *Views/Shared/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="4a392-148">将“ContosoUniversity”的每个匹配项都改为“Contoso University”。</span><span class="sxs-lookup"><span data-stu-id="4a392-148">Change each occurrence of "ContosoUniversity" to "Contoso University".</span></span> <span data-ttu-id="4a392-149">共有三个匹配项。</span><span class="sxs-lookup"><span data-stu-id="4a392-149">There are three occurrences.</span></span>

* <span data-ttu-id="4a392-150">添加 Students、Courses、Instructors 和 Departments 菜单项，并删除“联系人”菜单项。</span><span class="sxs-lookup"><span data-stu-id="4a392-150">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="4a392-151">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="4a392-151">The changes are highlighted.</span></span>

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,30,36-39,48)]

<span data-ttu-id="4a392-152">在 Views/Home/Index.cshtml 中，将文件内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关本应用程序的文本：</span><span class="sxs-lookup"><span data-stu-id="4a392-152">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

<span data-ttu-id="4a392-153">按 Ctrl+F5 运行项目，或从菜单中依次选择“调试”>“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="4a392-153">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span> <span data-ttu-id="4a392-154">随后将看到主页，主页中包含在这些教程中创建的页面标签。</span><span class="sxs-lookup"><span data-stu-id="4a392-154">You see the home page with tabs for the pages you'll create in these tutorials.</span></span>

![Contoso University 主页](intro/_static/home-page.png)

## <a name="entity-framework-core-nuget-packages"></a><span data-ttu-id="4a392-156">Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4a392-156">Entity Framework Core NuGet packages</span></span>

<span data-ttu-id="4a392-157">要为项目添加 EF Core 支持，请安装需要作为目标的数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="4a392-157">To add EF Core support to a project, install the database provider that you want to target.</span></span> <span data-ttu-id="4a392-158">本教程使用 SQL Server，提供程序包为 [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)。</span><span class="sxs-lookup"><span data-stu-id="4a392-158">This tutorial uses SQL Server, and the provider package is [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/).</span></span> <span data-ttu-id="4a392-159">此包包含在 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 元包中，因此无需另外安装。</span><span class="sxs-lookup"><span data-stu-id="4a392-159">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="4a392-160">此包及其依赖项（`Microsoft.EntityFrameworkCore` 和 `Microsoft.EntityFrameworkCore.Relational`）为 EF 提供运行时支持。</span><span class="sxs-lookup"><span data-stu-id="4a392-160">This package and its dependencies (`Microsoft.EntityFrameworkCore` and `Microsoft.EntityFrameworkCore.Relational`) provide runtime support for EF.</span></span> <span data-ttu-id="4a392-161">之后将在[迁移](migrations.md)教程中添加工具包。</span><span class="sxs-lookup"><span data-stu-id="4a392-161">You'll add a tooling package later, in the [Migrations](migrations.md) tutorial.</span></span> 

<span data-ttu-id="4a392-162">有关为 Entity Framework Core 提供的其他数据库提供程序的信息，请参阅[数据库提供程序](https://docs.microsoft.com/ef/core/providers/)。</span><span class="sxs-lookup"><span data-stu-id="4a392-162">For information about other database providers that are available for Entity Framework Core, see [Database providers](https://docs.microsoft.com/ef/core/providers/).</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="4a392-163">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="4a392-163">Create the data model</span></span>

<span data-ttu-id="4a392-164">接下来将创建 Contoso University 应用程序的实体类。</span><span class="sxs-lookup"><span data-stu-id="4a392-164">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="4a392-165">将从以下三个实体开始。</span><span class="sxs-lookup"><span data-stu-id="4a392-165">You'll start with the following three entities.</span></span>

![Course-Enrollment-Student 数据模型关系图](intro/_static/data-model-diagram.png)

<span data-ttu-id="4a392-167">`Student` 和 `Enrollment` 实体之间存在一对多的关系，`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="4a392-167">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="4a392-168">换言之，一名学生可以登记任意数量的课程，一门课程可以包含任意数量的学生。</span><span class="sxs-lookup"><span data-stu-id="4a392-168">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="4a392-169">以下部分将为这几个实体中的每一个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="4a392-169">In the following sections you'll create a class for each one of these entities.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="4a392-170">Student 实体</span><span class="sxs-lookup"><span data-stu-id="4a392-170">The Student entity</span></span>

![Student 实体关系图](intro/_static/student-entity.png)

<span data-ttu-id="4a392-172">在 Models 文件夹中，创建名为 Student.cs 的类文件，并使用以下代码替换模板代码。</span><span class="sxs-lookup"><span data-stu-id="4a392-172">In the *Models* folder, create a class file named *Student.cs* and replace the template code with the following code.</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="4a392-173">`ID` 属性将成为此类对应的数据库表的主键列。</span><span class="sxs-lookup"><span data-stu-id="4a392-173">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="4a392-174">默认情况下，Entity Framework 将名为 `ID` 或 `classnameID` 的属性视为主键。</span><span class="sxs-lookup"><span data-stu-id="4a392-174">By default, the Entity Framework interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="4a392-175">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="4a392-175">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="4a392-176">导航属性包含与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="4a392-176">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="4a392-177">在这种情况下，`Student entity` 的 `Enrollments` 属性将包含与该 `Student` 实体相关的所有 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="4a392-177">In this case, the `Enrollments` property of a `Student entity` will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="4a392-178">换言之，如果数据库中的给定 Student 行具有两个相关的 Enrollment 行（这两行的 StudentID 外键列包含该学生的外键值），该 `Student` 实体的 `Enrollments` 导航属性将包含这两个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="4a392-178">In other words, if a given Student row in the database has two related Enrollment rows (rows that contain that student's primary key value in their StudentID foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="4a392-179">如果导航属性可包含多个实体（如多对多或一对多关系），则其类型必须是可添加、可删除和可更新实体的列表，如 `ICollection<T>`。</span><span class="sxs-lookup"><span data-stu-id="4a392-179">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection<T>`.</span></span> <span data-ttu-id="4a392-180">可指定 `ICollection<T>` 或诸如 `List<T>` 或 `HashSet<T>` 的类型。</span><span class="sxs-lookup"><span data-stu-id="4a392-180">You can specify `ICollection<T>` or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="4a392-181">如果指定 `ICollection<T>`，EF 默认会创建一个 `HashSet<T>` 集合。</span><span class="sxs-lookup"><span data-stu-id="4a392-181">If you specify `ICollection<T>`, EF creates a `HashSet<T>` collection by default.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="4a392-182">Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="4a392-182">The Enrollment entity</span></span>

![Enrollment 实体关系图](intro/_static/enrollment-entity.png)

<span data-ttu-id="4a392-184">在 Models 文件夹中，创建 Enrollment.cs，并使用以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="4a392-184">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="4a392-185">`EnrollmentID` 属性将成为主键，正如在 `Student` 实体中看到的，此实体使用 `classnameID` 模式，而非 `ID`。</span><span class="sxs-lookup"><span data-stu-id="4a392-185">The `EnrollmentID` property will be the primary key; this entity uses the `classnameID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="4a392-186">通常可选择一个模式，并将其用于整个数据模型。</span><span class="sxs-lookup"><span data-stu-id="4a392-186">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="4a392-187">变体说明可以使用任意模式。</span><span class="sxs-lookup"><span data-stu-id="4a392-187">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="4a392-188">[下一个教程](inheritance.md)将介绍如何使用不带类名的 ID，以便更轻松地在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="4a392-188">In a [later tutorial](inheritance.md), you'll see how using ID without classname makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="4a392-189">`Grade` 属性为 `enum`。</span><span class="sxs-lookup"><span data-stu-id="4a392-189">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="4a392-190">`Grade` 类型声明后的问号表明 `Grade` 属性可为 NULL。</span><span class="sxs-lookup"><span data-stu-id="4a392-190">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="4a392-191">为 NULL 的年级与零年级不同，NULL 意味着该年级未知或尚未分配。</span><span class="sxs-lookup"><span data-stu-id="4a392-191">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="4a392-192">`StudentID` 属性是外键，其对应的导航属性为 `Student`。</span><span class="sxs-lookup"><span data-stu-id="4a392-192">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="4a392-193">`Enrollment` 实体与一个 `Student` 实体相关联，因此属性仅包含单个 `Student` 实体（而不像之前看到的 `Student.Enrollments` 导航属性，可包含多个 `Enrollment` 实体）。</span><span class="sxs-lookup"><span data-stu-id="4a392-193">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="4a392-194">`CourseID` 属性是外键，其对应的导航属性为 `Course`。</span><span class="sxs-lookup"><span data-stu-id="4a392-194">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="4a392-195">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="4a392-195">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="4a392-196">如果属性命名为 `<navigation property name><primary key property name>`，Entity Framework 会将其视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。</span><span class="sxs-lookup"><span data-stu-id="4a392-196">Entity Framework interprets a property as a foreign key property if it's named `<navigation property name><primary key property name>` (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="4a392-197">还可将外键属性简单命名为 `<primary key property name>`（例如可命名为 `CourseID`，因为 `Course` 实体的主键为 `CourseID`）。</span><span class="sxs-lookup"><span data-stu-id="4a392-197">Foreign key properties can also be named simply `<primary key property name>` (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="4a392-198">Course 实体</span><span class="sxs-lookup"><span data-stu-id="4a392-198">The Course entity</span></span>

![Course 实体关系图](intro/_static/course-entity.png)

<span data-ttu-id="4a392-200">在 Models 文件夹中，创建 Course.cs 并使用以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="4a392-200">In the *Models* folder, create *Course.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="4a392-201">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="4a392-201">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="4a392-202">`Course` 实体可与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="4a392-202">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="4a392-203">本系列的[下一个教程](complex-data-model.md)将介绍 `DatabaseGenerated` 特性的更多相关信息。</span><span class="sxs-lookup"><span data-stu-id="4a392-203">We'll say more about the `DatabaseGenerated` attribute in a [later tutorial](complex-data-model.md) in this series.</span></span> <span data-ttu-id="4a392-204">基本上，此特性允许你输入课程的主键，而不是在数据库中生成该主键。</span><span class="sxs-lookup"><span data-stu-id="4a392-204">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="4a392-205">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="4a392-205">Create the Database Context</span></span>

<span data-ttu-id="4a392-206">数据库上下文类是为给定数据模型协调 Entity Framework 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="4a392-206">The main class that coordinates Entity Framework functionality for a given data model is the database context class.</span></span> <span data-ttu-id="4a392-207">将通过从 `Microsoft.EntityFrameworkCore.DbContext` 类派生的方式创建此类。</span><span class="sxs-lookup"><span data-stu-id="4a392-207">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span> <span data-ttu-id="4a392-208">在代码中指定包含在数据模型中的实体。</span><span class="sxs-lookup"><span data-stu-id="4a392-208">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="4a392-209">还可以自定义特定 Entity Framework 行为。</span><span class="sxs-lookup"><span data-stu-id="4a392-209">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="4a392-210">在此项目中，类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="4a392-210">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="4a392-211">在项目文件夹中，创建一个名为 Data 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a392-211">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="4a392-212">在 Data 文件夹中，创建名为 SchoolContext.cs 的新类文件，并使用以下代码替换模板代码：</span><span class="sxs-lookup"><span data-stu-id="4a392-212">In the *Data* folder create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="4a392-213">此代码会为每个实体集创建一个 `DbSet` 属性。</span><span class="sxs-lookup"><span data-stu-id="4a392-213">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="4a392-214">在实体框架术语中，实体集通常与数据库表相对应，实体与表中的行相对应。</span><span class="sxs-lookup"><span data-stu-id="4a392-214">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>

<span data-ttu-id="4a392-215">可能已省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 语句，但其效果相同。</span><span class="sxs-lookup"><span data-stu-id="4a392-215">You could've omitted the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="4a392-216">Entity Framework 可能隐式包含了它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="4a392-216">The Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

<span data-ttu-id="4a392-217">创建数据库时，EF 会创建名称与 `DbSet` 属性名相同的表。</span><span class="sxs-lookup"><span data-stu-id="4a392-217">When the database is created, EF creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="4a392-218">集合的属性名通常为复数形式（Students 而非 Student），但开发者对表名是否应为复数意见不一。</span><span class="sxs-lookup"><span data-stu-id="4a392-218">Property names for collections are typically plural (Students rather than Student), but developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="4a392-219">在这些教程中，在 DbContext 中指定单数形式的表名将会覆盖默认行为。</span><span class="sxs-lookup"><span data-stu-id="4a392-219">For these tutorials you'll override the default behavior by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="4a392-220">要完成这一操作，请在最后的 DbSet 属性后添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="4a392-220">To do that, add the following highlighted code after the last DbSet property.</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="4a392-221">通过依赖关系注入注册上下文</span><span class="sxs-lookup"><span data-stu-id="4a392-221">Register the context with dependency injection</span></span>

<span data-ttu-id="4a392-222">ASP.NET Core 默认实现[依赖关系注入](../../fundamentals/dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="4a392-222">ASP.NET Core implements [dependency injection](../../fundamentals/dependency-injection.md) by default.</span></span> <span data-ttu-id="4a392-223">服务（例如 EF 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="4a392-223">Services (such as the EF database context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="4a392-224">需要这些服务（如 MVC 控制器）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="4a392-224">Components that require these services (such as MVC controllers) are provided these services via constructor parameters.</span></span> <span data-ttu-id="4a392-225">可在本教程的后面部分了解获取上下文实例的控制器构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="4a392-225">You'll see the controller constructor code that gets a context instance later in this tutorial.</span></span>

<span data-ttu-id="4a392-226">要将 `SchoolContext` 注册为服务，请打开 Startup.cs，并将突出显示的行添加到 `ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="4a392-226">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="4a392-227">通过调用 `DbContextOptionsBuilder` 对象上的方法，可将连接字符串的名称传递给上下文。</span><span class="sxs-lookup"><span data-stu-id="4a392-227">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="4a392-228">进行本地开发时，[ASP.NET Core 配置系统](xref:fundamentals/configuration/index)会从 appsettings.json 文件读取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4a392-228">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="4a392-229">为 `ContosoUniversity.Data` 和 `Microsoft.EntityFrameworkCore` 命名空间添加 `using` 语句，然后生成项目。</span><span class="sxs-lookup"><span data-stu-id="4a392-229">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces, and then build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="4a392-230">打开 appsettings.json 文件，并如以下示例所示添加连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4a392-230">Open the *appsettings.json* file and add a connection string as shown in the following example.</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a><span data-ttu-id="4a392-231">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="4a392-231">SQL Server Express LocalDB</span></span>

<span data-ttu-id="4a392-232">连接字符串指定 SQL Server LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-232">The connection string specifies a SQL Server LocalDB database.</span></span> <span data-ttu-id="4a392-233">LocalDB 是轻型版本 SQL Server Express 数据库引擎，专门针对应用程序开发，而非生产使用。</span><span class="sxs-lookup"><span data-stu-id="4a392-233">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for application development, not production use.</span></span> <span data-ttu-id="4a392-234">LocalDB 按需启动并在用户模式下运行，因此没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="4a392-234">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="4a392-235">默认情况下，LocalDB 会在 `C:/Users/<user>` 目录中创建 .mdf 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="4a392-235">By default, LocalDB creates *.mdf* database files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-database-with-test-data"></a><span data-ttu-id="4a392-236">添加代码，以使用测试数据初始化该数据库</span><span class="sxs-lookup"><span data-stu-id="4a392-236">Add code to initialize the database with test data</span></span>

<span data-ttu-id="4a392-237">Entity Framework 将创建一个空数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-237">The Entity Framework will create an empty database for you.</span></span> <span data-ttu-id="4a392-238">本部分中，创建数据库后，写入调用的方法，以使用测试数据填充该数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-238">In this section, you write a method that's called after the database is created in order to populate it with test data.</span></span>

<span data-ttu-id="4a392-239">此处，将使用 `EnsureCreated` 方法自动创建数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-239">Here you'll use the `EnsureCreated` method to automatically create the database.</span></span> <span data-ttu-id="4a392-240">[下一个教程](migrations.md)将介绍如何使用 Code First 迁移处理模型更改，以更改数据库架构而非丢弃或重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-240">In a [later tutorial](migrations.md) you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

<span data-ttu-id="4a392-241">在 Data 文件夹中，创建名为 DbInitializer.cs 的新类文件，使用以下代码替换模板代码，这会导致在需要时以及将测试数据加载到新数据库时创建数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-241">In the *Data* folder, create a new class file named *DbInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="4a392-242">代码检查数据库中是否有任何学生，如果没有，则假定该数据库为新数据库，需填充测试数据。</span><span class="sxs-lookup"><span data-stu-id="4a392-242">The code checks if there are any students in the database, and if not, it assumes the database is new and needs to be seeded with test data.</span></span> <span data-ttu-id="4a392-243">它会将测试数据加载到数组中，而不是 `List<T>` 集合中，以便优化性能。</span><span class="sxs-lookup"><span data-stu-id="4a392-243">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="4a392-244">在 Program.cs 中，修改 `Main` 方法以在应用程序启动时执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="4a392-244">In *Program.cs*, modify the `Main` method to do the following on application startup:</span></span>

* <span data-ttu-id="4a392-245">从依赖关系注入容器获取数据库上下文实例。</span><span class="sxs-lookup"><span data-stu-id="4a392-245">Get a database context instance from the dependency injection container.</span></span>
* <span data-ttu-id="4a392-246">调用 seed 方法，并将上下文传递给它。</span><span class="sxs-lookup"><span data-stu-id="4a392-246">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="4a392-247">Seed 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="4a392-247">Dispose the context when the seed method is done.</span></span>

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

<span data-ttu-id="4a392-248">添加 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="4a392-248">Add `using` statements:</span></span>

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Usings)]

<span data-ttu-id="4a392-249">在旧版教程中，可以在 Startup.cs 中查看 `Configure` 方法的类似代码。</span><span class="sxs-lookup"><span data-stu-id="4a392-249">In older tutorials, you may see similar code in the `Configure` method in *Startup.cs*.</span></span> <span data-ttu-id="4a392-250">建议仅在设置请求管道时使用 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="4a392-250">We recommend that you use the `Configure` method only to set up the request pipeline.</span></span> <span data-ttu-id="4a392-251">应用程序启动代码属于 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="4a392-251">Application startup code belongs in the `Main` method.</span></span>

<span data-ttu-id="4a392-252">首次运行应用程序时，会创建数据库，并为其填充测试数据。</span><span class="sxs-lookup"><span data-stu-id="4a392-252">Now the first time you run the application, the database will be created and seeded with test data.</span></span> <span data-ttu-id="4a392-253">任何时候想要更改数据模型，可删除数据库、更新 seed 方法，并以同样的方式重新启动新的数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-253">Whenever you change your data model, you can delete the database, update your seed method, and start afresh with a new database the same way.</span></span> <span data-ttu-id="4a392-254">下一个教程将介绍如何在更改数据模型时修改该数据库，而不删除并重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-254">In later tutorials, you'll see how to modify the database when the data model changes, without deleting and re-creating it.</span></span>

## <a name="create-a-controller-and-views"></a><span data-ttu-id="4a392-255">创建控制器和视图</span><span class="sxs-lookup"><span data-stu-id="4a392-255">Create a controller and views</span></span>

<span data-ttu-id="4a392-256">接下来，将在 Visual Studio 中使用基架引擎添加 MVC 控制器和视图，以使用 EF 来查询和保存数据。</span><span class="sxs-lookup"><span data-stu-id="4a392-256">Next, you'll use the scaffolding engine in Visual Studio to add an MVC controller and views that will use EF to query and save data.</span></span>

<span data-ttu-id="4a392-257">自动创建 CRUD 操作方法和视图的过程称为构架。</span><span class="sxs-lookup"><span data-stu-id="4a392-257">The automatic creation of CRUD action methods and views is known as scaffolding.</span></span> <span data-ttu-id="4a392-258">构架不同于生成代码，基架代码是可以根据自己需求修改的起点，而通常生成的代码是不能修改的。</span><span class="sxs-lookup"><span data-stu-id="4a392-258">Scaffolding differs from code generation in that the scaffolded code is a starting point that you can modify to suit your own requirements, whereas you typically don't modify generated code.</span></span> <span data-ttu-id="4a392-259">需要自定义生成的代码时，使用分部类，或在情况发生变化时重新生成代码。</span><span class="sxs-lookup"><span data-stu-id="4a392-259">When you need to customize generated code, you use partial classes or you regenerate the code when things change.</span></span>

* <span data-ttu-id="4a392-260">右键单击“解决方案资源管理器”中的 Controllers 文件夹，然后选择“添加”>“新基架项目”。</span><span class="sxs-lookup"><span data-stu-id="4a392-260">Right-click the **Controllers** folder in **Solution Explorer** and select **Add > New Scaffolded Item**.</span></span>

<span data-ttu-id="4a392-261">如果出现“添加 MVC 依赖项”对话框：</span><span class="sxs-lookup"><span data-stu-id="4a392-261">If the **Add MVC Dependencies** dialog appears:</span></span>

* <span data-ttu-id="4a392-262">[将 Visual Studio 更新到最新版本](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="4a392-262">[Update Visual Studio to the latest version](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="4a392-263">15.5 之前的 Visual Studio 版本显示此对话框。</span><span class="sxs-lookup"><span data-stu-id="4a392-263">Visual Studio versions prior to 15.5 show this dialog.</span></span>
* <span data-ttu-id="4a392-264">如果无法更新，请选择“添加”，然后再次按照添加控制器步骤操作。</span><span class="sxs-lookup"><span data-stu-id="4a392-264">If you can't update, select **ADD**, and then follow the add controller steps again.</span></span>

* <span data-ttu-id="4a392-265">在“添加基架”对话框中：</span><span class="sxs-lookup"><span data-stu-id="4a392-265">In the **Add Scaffold** dialog box:</span></span>

  * <span data-ttu-id="4a392-266">选中“视图使用 Entity Framework 的 MVC 控制器”。</span><span class="sxs-lookup"><span data-stu-id="4a392-266">Select **MVC controller with views, using Entity Framework**.</span></span>

  * <span data-ttu-id="4a392-267">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="4a392-267">Click **Add**.</span></span>

* <span data-ttu-id="4a392-268">在“添加控制器”对话框中：</span><span class="sxs-lookup"><span data-stu-id="4a392-268">In the **Add Controller** dialog box:</span></span>

  * <span data-ttu-id="4a392-269">在“模型类”中选择“学生”。</span><span class="sxs-lookup"><span data-stu-id="4a392-269">In **Model class** select **Student**.</span></span>

  * <span data-ttu-id="4a392-270">在“数据上下文类”中选择 SchoolContext。</span><span class="sxs-lookup"><span data-stu-id="4a392-270">In **Data context class** select **SchoolContext**.</span></span>

  * <span data-ttu-id="4a392-271">接受默认的 StudentsController 作为名称。</span><span class="sxs-lookup"><span data-stu-id="4a392-271">Accept the default **StudentsController** as the name.</span></span>

  * <span data-ttu-id="4a392-272">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="4a392-272">Click **Add**.</span></span>

  ![构架 Student](intro/_static/scaffold-student.png)

  <span data-ttu-id="4a392-274">单击“添加”时，Visual Studio 基架引擎会创建 StudentsController.cs 文件和视图集（.cshtml 文件），以与控制器一同使用。</span><span class="sxs-lookup"><span data-stu-id="4a392-274">When you click **Add**, the Visual Studio scaffolding engine creates a *StudentsController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span>

<span data-ttu-id="4a392-275">（如果没有如本教程前面部分介绍的那样事先手动创建数据库上下文，基架引擎还可帮助创建。</span><span class="sxs-lookup"><span data-stu-id="4a392-275">(The scaffolding engine can also create the database context for you if you don't create it manually first as you did earlier for this tutorial.</span></span> <span data-ttu-id="4a392-276">通过单击“数据上下文类”右侧的加号，可在“添加控制器”框中指定新的上下文类。</span><span class="sxs-lookup"><span data-stu-id="4a392-276">You can specify a new context class in the **Add Controller** box by clicking the plus sign to the right of **Data context class**.</span></span>  <span data-ttu-id="4a392-277">然后，Visual Studio 将创建 `DbContext` 类、控制器和视图。）</span><span class="sxs-lookup"><span data-stu-id="4a392-277">Visual Studio will then create your `DbContext` class as well as the controller and views.)</span></span>

<span data-ttu-id="4a392-278">注意控制器将 `SchoolContext` 作为构造函数参数。</span><span class="sxs-lookup"><span data-stu-id="4a392-278">You'll notice that the controller takes a `SchoolContext` as a constructor parameter.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

<span data-ttu-id="4a392-279">ASP.NET 依赖关系注入负责将 `SchoolContext` 的实例传递到控制器中。</span><span class="sxs-lookup"><span data-stu-id="4a392-279">ASP.NET dependency injection will take care of passing an instance of `SchoolContext` into the controller.</span></span> <span data-ttu-id="4a392-280">之前已在 Startup.cs 文件中进行过配置。</span><span class="sxs-lookup"><span data-stu-id="4a392-280">You configured that in the *Startup.cs* file earlier.</span></span>

<span data-ttu-id="4a392-281">该控制器包含一个 `Index` 操作方法，该方法显示数据库中的所有学生。</span><span class="sxs-lookup"><span data-stu-id="4a392-281">The controller contains an `Index` action method, which displays all students in the database.</span></span> <span data-ttu-id="4a392-282">该方法通过读取数据库上下文实例的 `Students` 属性从 Students 实体集获取学生列表：</span><span class="sxs-lookup"><span data-stu-id="4a392-282">The method gets a list of students from the Students entity set by reading the `Students` property of the database context instance:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

<span data-ttu-id="4a392-283">本教程后面部分将介绍此代码中的异步编程元素。</span><span class="sxs-lookup"><span data-stu-id="4a392-283">You'll learn about the asynchronous programming elements in this code later in the tutorial.</span></span>

<span data-ttu-id="4a392-284">Views/Students/Index.cshtml 视图在表中显示此列表：</span><span class="sxs-lookup"><span data-stu-id="4a392-284">The *Views/Students/Index.cshtml* view displays this list in a table:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

<span data-ttu-id="4a392-285">按 Ctrl+F5 运行项目，或从菜单中依次选择“调试”>“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="4a392-285">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span>

<span data-ttu-id="4a392-286">单击“学生”选项卡以查看 `DbInitializer.Initialize` 方法插入的测试数据。</span><span class="sxs-lookup"><span data-stu-id="4a392-286">Click the Students tab to see the test data that the `DbInitializer.Initialize` method inserted.</span></span> <span data-ttu-id="4a392-287">可以在页面顶部查看 `Student` 选项卡链接，或单击右上角的导航图标查看链接，具体取决于浏览器窗口的宽窄。</span><span class="sxs-lookup"><span data-stu-id="4a392-287">Depending on how narrow your browser window is, you'll see the `Student` tab link at the top of the page or you'll have to click the navigation icon in the upper right corner to see the link.</span></span>

![Contoso University 主页宽窄](intro/_static/home-page-narrow.png)

![“学生索引”页](intro/_static/students-index.png)

## <a name="view-the-database"></a><span data-ttu-id="4a392-290">查看数据库</span><span class="sxs-lookup"><span data-stu-id="4a392-290">View the Database</span></span>

<span data-ttu-id="4a392-291">启动应用程序时，`DbInitializer.Initialize` 方法调用 `EnsureCreated`。</span><span class="sxs-lookup"><span data-stu-id="4a392-291">When you started the application, the `DbInitializer.Initialize` method calls `EnsureCreated`.</span></span> <span data-ttu-id="4a392-292">如果 EF 检查到没有数据库时，它会创建一个数据库，然后 `Initialize` 方法代码的其他部分会使用数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-292">EF saw that there was no database and so it created one, then the remainder of the `Initialize` method code populated the database with data.</span></span> <span data-ttu-id="4a392-293">可以使用“SQL Server 对象资源管理器”(SSOX) 查看 Visual Studio 中的数据库。</span><span class="sxs-lookup"><span data-stu-id="4a392-293">You can use **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span>

<span data-ttu-id="4a392-294">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4a392-294">Close the browser.</span></span>

<span data-ttu-id="4a392-295">如果还没有打开 SSOX 窗口，可从 Visual Studio 中的“视图”菜单中选择 SSOX 窗口。</span><span class="sxs-lookup"><span data-stu-id="4a392-295">If the SSOX window isn't already open, select it from the **View** menu in Visual Studio.</span></span>

<span data-ttu-id="4a392-296">在 SSOX 中，单击“(localdb)\MSSQLLocalDB”>“数据库”，然后单击 appsettings.json 文件中连接字符串中的数据库名条目。</span><span class="sxs-lookup"><span data-stu-id="4a392-296">In SSOX, click **(localdb)\MSSQLLocalDB > Databases**, and then click the entry for the database name that's in the connection string in your *appsettings.json* file.</span></span>

<span data-ttu-id="4a392-297">展开“表”节点，查看数据库中的表。</span><span class="sxs-lookup"><span data-stu-id="4a392-297">Expand the **Tables** node to see the tables in your database.</span></span>

![SSOX 中的表](intro/_static/ssox-tables.png)

<span data-ttu-id="4a392-299">右键单击 Student 表，然后单击“查看数据”，以查看创建的列和插入到表中的行。</span><span class="sxs-lookup"><span data-stu-id="4a392-299">Right-click the **Student** table and click **View Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

![SSOX 中的 Student 表](intro/_static/ssox-student-table.png)

<span data-ttu-id="4a392-301">.mdf 和 .ldf 数据库文件位于 C:\Users\<yourusername> 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4a392-301">The *.mdf* and *.ldf* database files are in the *C:\Users\<yourusername>* folder.</span></span>

<span data-ttu-id="4a392-302">由于在应用启动时运行的初始化方法中调用 `EnsureCreated`，现在可对 `Student` 类作出更改，删除数据库，然后再运行应用程序，数据库将自动重新创建以匹配作出的更改。</span><span class="sxs-lookup"><span data-stu-id="4a392-302">Because you're calling `EnsureCreated` in the initializer method that runs on app start, you could now make a change to the `Student` class, delete the database, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="4a392-303">例如，如果向 `Student` 类添加 `EmailAddress` 属性，可以在重新创建的表中看到新的 `EmailAddress` 列。</span><span class="sxs-lookup"><span data-stu-id="4a392-303">For example, if you add an `EmailAddress` property to the `Student` class, you'll see a new `EmailAddress` column in the re-created table.</span></span>

## <a name="conventions"></a><span data-ttu-id="4a392-304">约定</span><span class="sxs-lookup"><span data-stu-id="4a392-304">Conventions</span></span>

<span data-ttu-id="4a392-305">因为约定的使用或 Entity Framework 所做的假设，为使 Entity Framework 能够创建一个完整的数据库，必须写入的代码数量是最少的。</span><span class="sxs-lookup"><span data-stu-id="4a392-305">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of conventions, or assumptions that the Entity Framework makes.</span></span>

* <span data-ttu-id="4a392-306">使用 `DbSet` 属性的名称作为表名。</span><span class="sxs-lookup"><span data-stu-id="4a392-306">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="4a392-307">若是未被 `DbSet` 属性引用的实体，则使用实体类名作为表名。</span><span class="sxs-lookup"><span data-stu-id="4a392-307">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="4a392-308">使用实体属性名作为列名。</span><span class="sxs-lookup"><span data-stu-id="4a392-308">Entity property names are used for column names.</span></span>

* <span data-ttu-id="4a392-309">以 ID 或 classnameID 命名的实体属性被视为主键属性。</span><span class="sxs-lookup"><span data-stu-id="4a392-309">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="4a392-310">如果属性命名为 <navigation property name><primary key property name>，将视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。</span><span class="sxs-lookup"><span data-stu-id="4a392-310">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="4a392-311">还可将外键属性简单命名为 <primary key property name>（例如可命名为 `EnrollmentID`，因为 `Enrollment` 实体的主键为 `EnrollmentID`）。</span><span class="sxs-lookup"><span data-stu-id="4a392-311">Foreign key properties can also be named simply *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="4a392-312">可以重写常规行为。</span><span class="sxs-lookup"><span data-stu-id="4a392-312">Conventional behavior can be overridden.</span></span> <span data-ttu-id="4a392-313">例如，可以按照本教程前面部分所述，明确指定表名。</span><span class="sxs-lookup"><span data-stu-id="4a392-313">For example, you can explicitly specify table names, as you saw earlier in this tutorial.</span></span> <span data-ttu-id="4a392-314">或如本系列[下一个教程](complex-data-model.md)中介绍的，设置列名，并将任何属性设置为主键或外键。</span><span class="sxs-lookup"><span data-stu-id="4a392-314">And you can set column names and set any property as primary key or foreign key, as you'll see in a [later tutorial](complex-data-model.md) in this series.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="4a392-315">异步代码</span><span class="sxs-lookup"><span data-stu-id="4a392-315">Asynchronous code</span></span>

<span data-ttu-id="4a392-316">异步编程是 ASP.NET Core 和 EF Core 的默认模式。</span><span class="sxs-lookup"><span data-stu-id="4a392-316">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="4a392-317">Web 服务器可用的线程数量有限，在高负载情况下，所有可用的线程可能都正在使用。</span><span class="sxs-lookup"><span data-stu-id="4a392-317">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="4a392-318">在这种情况下，线程释放之前，服务器无法处理新的请求。</span><span class="sxs-lookup"><span data-stu-id="4a392-318">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="4a392-319">若使用同步代码，许多线程在等待 I/O 完成时实际上并未执行任何操作，但仍被占用。</span><span class="sxs-lookup"><span data-stu-id="4a392-319">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="4a392-320">若使用异步代码，进程在等待 I/O 完成时其线程会被释放，以便服务器用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="4a392-320">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="4a392-321">因此，使用异步代码可以更有效地利用服务器资源，并且可以让服务器在没有延迟的情况下处理更多流量。</span><span class="sxs-lookup"><span data-stu-id="4a392-321">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="4a392-322">异步代码在运行时会引入少量的开销，流量较低时，对性能的影响可以忽略不计，但流量较高时，潜在的性能改善非常显著。</span><span class="sxs-lookup"><span data-stu-id="4a392-322">Asynchronous code does introduce a small amount of overhead at run time, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="4a392-323">在以下代码中，`async` 关键字、`Task<T>` 返回值、`await` 关键字和 `ToListAsync` 方法让代码异步执行。</span><span class="sxs-lookup"><span data-stu-id="4a392-323">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="4a392-324">`async` 关键字通知编译器为方法主体部分生成回调，并自动创建返回的 `Task<IActionResult>` 对象。</span><span class="sxs-lookup"><span data-stu-id="4a392-324">The `async` keyword tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<IActionResult>` object that's returned.</span></span>

* <span data-ttu-id="4a392-325">返回类型 `Task<IActionResult>` 表示正在进行的工作，其结果是 `IActionResult` 类型。</span><span class="sxs-lookup"><span data-stu-id="4a392-325">The return type `Task<IActionResult>` represents ongoing work with a result of type `IActionResult`.</span></span>

* <span data-ttu-id="4a392-326">`await` 关键字让编译器将该方法拆分为两个部分。</span><span class="sxs-lookup"><span data-stu-id="4a392-326">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="4a392-327">第一部分以异步方式启动的操作结束。</span><span class="sxs-lookup"><span data-stu-id="4a392-327">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="4a392-328">第二部分被放入一个回调方法中，当操作完成时调用。</span><span class="sxs-lookup"><span data-stu-id="4a392-328">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="4a392-329">`ToListAsync` 是 `ToList` 扩展方法的异步版本。</span><span class="sxs-lookup"><span data-stu-id="4a392-329">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="4a392-330">编写使用 Entity Framework 的异步代码时需要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="4a392-330">Some things to be aware of when you are writing asynchronous code that uses the Entity Framework:</span></span>

* <span data-ttu-id="4a392-331">只会异步执行导致查询或命令被发送到数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="4a392-331">Only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="4a392-332">这包括，例如，`ToListAsync``SingleOrDefaultAsync` 和 `SaveChangesAsync`。</span><span class="sxs-lookup"><span data-stu-id="4a392-332">That includes, for example, `ToListAsync`, `SingleOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="4a392-333">不包括只会更改 `IQueryable` 的语句，例如 `var students = context.Students.Where(s => s.LastName == "Davolio")`。</span><span class="sxs-lookup"><span data-stu-id="4a392-333">It doesn't include, for example, statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="4a392-334">EF 上下文并非线程安全：请勿尝试并行执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="4a392-334">An EF context isn't thread safe: don't try to do multiple operations in parallel.</span></span> <span data-ttu-id="4a392-335">调用任何异步 EF 方法时，都始终使用 `await` 关键字。</span><span class="sxs-lookup"><span data-stu-id="4a392-335">When you call any async EF method, always use the `await` keyword.</span></span>

* <span data-ttu-id="4a392-336">如果想利用异步代码的性能优势，请确保正在使用的任何库程序包（如用于分页）也使用异步（如果它们调用任何导致查询发送到数据库的 Entity Framework 方法）。</span><span class="sxs-lookup"><span data-stu-id="4a392-336">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

<span data-ttu-id="4a392-337">有关在 .NET 中进行异步编程的详细信息，请参阅[异步概述](https://docs.microsoft.com/dotnet/articles/standard/async)。</span><span class="sxs-lookup"><span data-stu-id="4a392-337">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

## <a name="summary"></a><span data-ttu-id="4a392-338">摘要</span><span class="sxs-lookup"><span data-stu-id="4a392-338">Summary</span></span>

<span data-ttu-id="4a392-339">现在已创建了一个使用 Entity Framework Core 和 SQL Server Express LocalDB 来存储和显示数据的简单应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a392-339">You've now created a simple application that uses the Entity Framework Core and SQL Server Express LocalDB to store and display data.</span></span> <span data-ttu-id="4a392-340">下一个教程将介绍如何执行基本的 CRUD（创建、读取、更新、删除）操作。</span><span class="sxs-lookup"><span data-stu-id="4a392-340">In the following tutorial, you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="4a392-341">下一篇</span><span class="sxs-lookup"><span data-stu-id="4a392-341">Next</span></span>](crud.md)
