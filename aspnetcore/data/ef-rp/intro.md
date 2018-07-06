---
title: ASP.NET Core 中的 Razor 页面和 Entity Framework Core - 第 1 个教程（共 8 个）
author: rick-anderson
description: 介绍了如何使用 Entity Framework Core 创建 Razor 页面应用
ms.author: riande
ms.date: 6/31/2017
uid: data/ef-rp/intro
ms.openlocfilehash: a31b3e0ad72964a0c01c0b855a70d2f3e8966ab9
ms.sourcegitcommit: 7003d27b607e529642ded0400aa48ae692a0e666
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37033285"
---
# <a name="razor-pages-with-entity-framework-core-in-aspnet-core---tutorial-1-of-8"></a><span data-ttu-id="dd862-103">ASP.NET Core 中的 Razor 页面和 Entity Framework Core - 第 1 个教程（共 8 个）</span><span class="sxs-lookup"><span data-stu-id="dd862-103">Razor Pages with Entity Framework Core in ASP.NET Core - Tutorial 1 of 8</span></span>

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="dd862-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dd862-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="dd862-105">Contoso University 示例 Web 应用演示了如何使用 Entity Framework (EF) Core 创建 ASP.NET Core Razor Pages 应用。</span><span class="sxs-lookup"><span data-stu-id="dd862-105">The Contoso University sample web app demonstrates how to create an ASP.NET Core Razor Pages app using Entity Framework (EF) Core.</span></span>

<span data-ttu-id="dd862-106">该示例应用是一个虚构的 Contoso University 的网站。</span><span class="sxs-lookup"><span data-stu-id="dd862-106">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="dd862-107">其中包括学生录取、课程创建和讲师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="dd862-107">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="dd862-108">本页是介绍如何构建 Contoso University 示例应用系列教程中的第一部分。</span><span class="sxs-lookup"><span data-stu-id="dd862-108">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="dd862-109">下载或查看已完成的应用。</span><span class="sxs-lookup"><span data-stu-id="dd862-109">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="dd862-110">[下载说明](xref:tutorials/index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="dd862-110">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd862-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="dd862-111">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="dd862-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd862-112">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="dd862-113">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="dd862-113">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="dd862-114">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="dd862-114">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="dd862-115">[!INCLUDE [](~/includes/2.1-SDK.md) [](~/includes/2.1-SDK.md)]</span><span class="sxs-lookup"><span data-stu-id="dd862-115">[!INCLUDE [](~/includes/2.1-SDK.md) [](~/includes/2.1-SDK.md)]</span></span>

------

<span data-ttu-id="dd862-116">熟悉 [Razor 页面](xref:razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="dd862-116">Familiarity with [Razor Pages](xref:razor-pages/index).</span></span> <span data-ttu-id="dd862-117">新程序员在开始学习本系列之前，应先完成 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="dd862-117">New programmers should complete [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) before starting this series.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dd862-118">疑难解答</span><span class="sxs-lookup"><span data-stu-id="dd862-118">Troubleshooting</span></span>

<span data-ttu-id="dd862-119">如果遇到无法解决的问题，可以通过与 [已完成的项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)对比代码来查找解决方案。</span><span class="sxs-lookup"><span data-stu-id="dd862-119">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples).</span></span> <span data-ttu-id="dd862-120">获取帮助的一个好方法是将问题发布到适用于 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 或 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core) 的 [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core)。</span><span class="sxs-lookup"><span data-stu-id="dd862-120">A good way to get help is by posting a question to [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core) for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="dd862-121">Contoso University Web 应用</span><span class="sxs-lookup"><span data-stu-id="dd862-121">The Contoso University web app</span></span>

<span data-ttu-id="dd862-122">这些教程中所构建的应用是一个基本的大学网站。</span><span class="sxs-lookup"><span data-stu-id="dd862-122">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="dd862-123">用户可以查看和更新学生、课程和讲师信息。</span><span class="sxs-lookup"><span data-stu-id="dd862-123">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="dd862-124">以下是在本教程中创建的几个屏幕。</span><span class="sxs-lookup"><span data-stu-id="dd862-124">Here are a few of the screens created in the tutorial.</span></span>

![“学生索引”页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

<span data-ttu-id="dd862-127">此网站的 UI 样式与内置模板生成的 UI 样式类似。</span><span class="sxs-lookup"><span data-stu-id="dd862-127">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="dd862-128">教程的重点是 EF Core 和 Razor 页面，而非 UI。</span><span class="sxs-lookup"><span data-stu-id="dd862-128">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-the-contosouniversity-razor-pages-web-app"></a><span data-ttu-id="dd862-129">创建 ContosoUniversity Razor Pages Web 应用</span><span class="sxs-lookup"><span data-stu-id="dd862-129">Create the ContosoUniversity Razor Pages web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="dd862-130">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd862-130">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="dd862-131">从 Visual Studio“文件”菜单中，选择“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="dd862-131">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="dd862-132">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd862-132">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="dd862-133">将该项目命名为 ContosoUniversity 。</span><span class="sxs-lookup"><span data-stu-id="dd862-133">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="dd862-134">务必将该项目命名为 ContosoUniversity，以便复制/粘贴代码时命名空间相匹配。</span><span class="sxs-lookup"><span data-stu-id="dd862-134">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
* <span data-ttu-id="dd862-135">在下拉列表中选择“ASP.NET Core 2.1”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="dd862-135">Select **ASP.NET Core 2.1** in the dropdown, and then select **Web Application**.</span></span>

<span data-ttu-id="dd862-136">有关上述步骤的图像，请参阅[创建 Razor Web 应用](xref:tutorials/razor-pages/razor-pages-start#create-a-razor-web-app)。</span><span class="sxs-lookup"><span data-stu-id="dd862-136">For images of the preceding steps, see [Create a Razor web app](xref:tutorials/razor-pages/razor-pages-start#create-a-razor-web-app).</span></span>
<span data-ttu-id="dd862-137">运行应用。</span><span class="sxs-lookup"><span data-stu-id="dd862-137">Run the app.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="dd862-138">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="dd862-138">.NET Core CLI</span></span>](#tab/netcore-cli)

```CLI
dotnet new webapp -o ContosoUniversity
cd ContosoUniversity
dotnet run
```

------

## <a name="set-up-the-site-style"></a><span data-ttu-id="dd862-139">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="dd862-139">Set up the site style</span></span>

<span data-ttu-id="dd862-140">设置网站菜单、布局和主页时需作少量更改。</span><span class="sxs-lookup"><span data-stu-id="dd862-140">A few changes set up the site menu, layout, and home page.</span></span> <span data-ttu-id="dd862-141">进行以下更改以更新 Pages/Shared/_Layout.cshtml：</span><span class="sxs-lookup"><span data-stu-id="dd862-141">Update *Pages/Shared/_Layout.cshtml* with the following changes:</span></span>

* <span data-ttu-id="dd862-142">将文件中的"ContosoUniversity"更改为"Contoso University"。</span><span class="sxs-lookup"><span data-stu-id="dd862-142">Change each occurrence of "ContosoUniversity" to "Contoso University".</span></span> <span data-ttu-id="dd862-143">需要更改三个地方。</span><span class="sxs-lookup"><span data-stu-id="dd862-143">There are three occurrences.</span></span>

* <span data-ttu-id="dd862-144">添加菜单项 **Students**，**Courses**，**Instructors**，和 **Department**，并删除 **Contact**菜单项。</span><span class="sxs-lookup"><span data-stu-id="dd862-144">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="dd862-145">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="dd862-145">The changes are highlighted.</span></span> <span data-ttu-id="dd862-146">（所有标记均不显示。）</span><span class="sxs-lookup"><span data-stu-id="dd862-146">(All the markup is *not* displayed.)</span></span>

[!code-html[](intro/samples/cu21/Pages/Shared/_Layout.cshtml?highlight=6,29,35-38,50&name=snippet)]

<span data-ttu-id="dd862-147">在 Pages/Index.cshtml 中，将文件内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关本应用的文本：</span><span class="sxs-lookup"><span data-stu-id="dd862-147">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu21/Pages/Index.cshtml)]

## <a name="create-the-data-model"></a><span data-ttu-id="dd862-148">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="dd862-148">Create the data model</span></span>

<span data-ttu-id="dd862-149">创建 Contoso University 应用的实体类。</span><span class="sxs-lookup"><span data-stu-id="dd862-149">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="dd862-150">从以下三个实体开始：</span><span class="sxs-lookup"><span data-stu-id="dd862-150">Start with the following three entities:</span></span>

![Course-Enrollment-Student 数据模型关系图](intro/_static/data-model-diagram.png)

<span data-ttu-id="dd862-152">`Student` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="dd862-152">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="dd862-153">`Course` 和 `Enrollment` 实体之间存在一对多关系。</span><span class="sxs-lookup"><span data-stu-id="dd862-153">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="dd862-154">一名学生可以报名参加任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="dd862-154">A student can enroll in any number of courses.</span></span> <span data-ttu-id="dd862-155">一门课程中可以包含任意数量的学生。</span><span class="sxs-lookup"><span data-stu-id="dd862-155">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="dd862-156">以下部分将为这几个实体中的每一个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="dd862-156">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="dd862-157">Student 实体</span><span class="sxs-lookup"><span data-stu-id="dd862-157">The Student entity</span></span>

![Student 实体关系图](intro/_static/student-entity.png)

<span data-ttu-id="dd862-159">创建 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd862-159">Create a *Models* folder.</span></span> <span data-ttu-id="dd862-160">在 Models 文件夹中，使用以下代码创建一个名为 Student.cs 的类文件：</span><span class="sxs-lookup"><span data-stu-id="dd862-160">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu21/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="dd862-161">`ID` 属性成为此类对应的数据库 (DB) 表的主键列。</span><span class="sxs-lookup"><span data-stu-id="dd862-161">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="dd862-162">默认情况下，EF Core 将名为 `ID` 或 `classnameID` 的属性视为主键。</span><span class="sxs-lookup"><span data-stu-id="dd862-162">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span> <span data-ttu-id="dd862-163">在 `classnameID` 中，`classname` 为类名称。</span><span class="sxs-lookup"><span data-stu-id="dd862-163">In `classnameID`, `classname` is the name of the class.</span></span> <span data-ttu-id="dd862-164">另一种自动识别的主键是上例中的 `StudentID`。</span><span class="sxs-lookup"><span data-stu-id="dd862-164">The alternative automatically recognized primary key is `StudentID` in the preceding example.</span></span>

<span data-ttu-id="dd862-165">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="dd862-165">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="dd862-166">导航属性链接到与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-166">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="dd862-167">在这种情况下，`Student entity` 的 `Enrollments` 属性包含与该 `Student` 相关的所有 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-167">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="dd862-168">例如，如果数据库中的 Student 行有两个相关的 Enrollment 行，则 `Enrollments` 导航属性包含这两个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-168">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="dd862-169">相关的 `Enrollment` 行是 `StudentID` 列中包含该学生的主键值的行。</span><span class="sxs-lookup"><span data-stu-id="dd862-169">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="dd862-170">例如，假设 ID=1 的学生在 `Enrollment` 表中有两行。</span><span class="sxs-lookup"><span data-stu-id="dd862-170">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="dd862-171">`Enrollment` 表中有两行的 `StudentID` = 1。</span><span class="sxs-lookup"><span data-stu-id="dd862-171">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="dd862-172">`StudentID` 是 `Enrollment` 表中的外键，用于指定 `Student` 表中的学生。</span><span class="sxs-lookup"><span data-stu-id="dd862-172">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="dd862-173">如果导航属性包含多个实体，则导航属性必须是列表类型，例如 `ICollection<T>`。</span><span class="sxs-lookup"><span data-stu-id="dd862-173">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="dd862-174">可以指定 `ICollection<T>` 或诸如 `List<T>` 或 `HashSet<T>` 的类型。</span><span class="sxs-lookup"><span data-stu-id="dd862-174">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="dd862-175">使用 `ICollection<T>` 时，EF Core 会默认创建 `HashSet<T>` 集合。</span><span class="sxs-lookup"><span data-stu-id="dd862-175">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="dd862-176">包含多个实体的导航属性来自于多对多和一对多关系。</span><span class="sxs-lookup"><span data-stu-id="dd862-176">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="dd862-177">Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="dd862-177">The Enrollment entity</span></span>

![Enrollment 实体关系图](intro/_static/enrollment-entity.png)

<span data-ttu-id="dd862-179">在 Models 文件夹中，使用以下代码创建 Enrollment.cs：</span><span class="sxs-lookup"><span data-stu-id="dd862-179">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu21/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="dd862-180">`EnrollmentID` 属性为主键。</span><span class="sxs-lookup"><span data-stu-id="dd862-180">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="dd862-181">`Student` 实体使用的是 `ID` 模式，而本实体使用的是 `classnameID` 模式。</span><span class="sxs-lookup"><span data-stu-id="dd862-181">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="dd862-182">通常情况下，开发者会选择一种模式并在整个数据模型中都使用该模式。</span><span class="sxs-lookup"><span data-stu-id="dd862-182">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="dd862-183">下一个教程将介绍如何使用不带类名的 ID，以便更轻松地在数据模型中实现集成。</span><span class="sxs-lookup"><span data-stu-id="dd862-183">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="dd862-184">`Grade` 属性为 `enum`。</span><span class="sxs-lookup"><span data-stu-id="dd862-184">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="dd862-185">`Grade` 声明类型后的`?`表示 `Grade` 属性可以为 null。</span><span class="sxs-lookup"><span data-stu-id="dd862-185">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="dd862-186">评级为 null 和评级为零是有区别的 --null 意味着评级未知或者尚未分配。</span><span class="sxs-lookup"><span data-stu-id="dd862-186">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="dd862-187">`StudentID` 属性是外键，其对应的导航属性为 `Student`。</span><span class="sxs-lookup"><span data-stu-id="dd862-187">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="dd862-188">`Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含一个 `Student` 实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-188">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="dd862-189">`Student` 实体与 `Student.Enrollments` 导航属性不同，后者包含多个 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-189">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="dd862-190">`CourseID` 属性是外键，其对应的导航属性为 `Course`。</span><span class="sxs-lookup"><span data-stu-id="dd862-190">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="dd862-191">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="dd862-191">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="dd862-192">如果属性命名为 `<navigation property name><primary key property name>`，EF Core 会将其视为外键。</span><span class="sxs-lookup"><span data-stu-id="dd862-192">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="dd862-193">例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`。</span><span class="sxs-lookup"><span data-stu-id="dd862-193">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="dd862-194">还可以将外键属性命名为 `<primary key property name>`。</span><span class="sxs-lookup"><span data-stu-id="dd862-194">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="dd862-195">例如 `CourseID`，因为 `Course` 实体的主键为 `CourseID`。</span><span class="sxs-lookup"><span data-stu-id="dd862-195">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="dd862-196">Course 实体</span><span class="sxs-lookup"><span data-stu-id="dd862-196">The Course entity</span></span>

![Course 实体关系图](intro/_static/course-entity.png)

<span data-ttu-id="dd862-198">在 Models 文件夹中，使用以下代码创建 Course.cs：</span><span class="sxs-lookup"><span data-stu-id="dd862-198">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu21/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="dd862-199">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="dd862-199">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="dd862-200">`Course` 实体可与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="dd862-200">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="dd862-201">应用可以通过 `DatabaseGenerated` 特性指定主键，而无需靠数据库生成。</span><span class="sxs-lookup"><span data-stu-id="dd862-201">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="scaffold-the-student-model"></a><span data-ttu-id="dd862-202">为“学生”模型搭建基架</span><span class="sxs-lookup"><span data-stu-id="dd862-202">Scaffold the student model</span></span>

<span data-ttu-id="dd862-203">本部分将为“学生”模型搭建基架。</span><span class="sxs-lookup"><span data-stu-id="dd862-203">In this section, the student model is scaffolded.</span></span> <span data-ttu-id="dd862-204">确切地说，基架工具将生成页面，用于对“学生”模型执行创建、读取、更新和删除 (CRUD) 操作。</span><span class="sxs-lookup"><span data-stu-id="dd862-204">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the student model.</span></span>

* <span data-ttu-id="dd862-205">生成项目。</span><span class="sxs-lookup"><span data-stu-id="dd862-205">Build the project.</span></span>
* <span data-ttu-id="dd862-206">创建 Pages/Students 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd862-206">Create the *Pages/Students* folder.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="dd862-207">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd862-207">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="dd862-208">在“解决方案资源管理器”中，右键单击“Pages/Students”文件夹>“添加”>“新搭建基架的项目”。</span><span class="sxs-lookup"><span data-stu-id="dd862-208">In **Solution Explorer**, right click on the *Pages/Students* folder > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="dd862-209">在“添加基架”对话框中，选择“使用实体框架生成 Razor Pages (CRUD)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="dd862-209">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **ADD**.</span></span>

<span data-ttu-id="dd862-210">完成“使用实体框架(CRUD)添加 Razor Pages”对话框：</span><span class="sxs-lookup"><span data-stu-id="dd862-210">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="dd862-211">在“模型类”下拉列表中，选择“学生(ContosoUniversity.Models)”。</span><span class="sxs-lookup"><span data-stu-id="dd862-211">In the **Model class** drop-down, select **Student (ContosoUniversity.Models)**.</span></span>
* <span data-ttu-id="dd862-212">在“数据上下文类”行中，选择加号 (+) 并将生成的名称更改为 ContosoUniversity.Models.SchoolContext。</span><span class="sxs-lookup"><span data-stu-id="dd862-212">In the **Data context class** row, select the **+** (plus) sign and change the generated name to **ContosoUniversity.Models.SchoolContext**.</span></span>
* <span data-ttu-id="dd862-213">在“数据上下文类”下拉列表中，选择“ContosoUniversity.Models.SchoolContext”</span><span class="sxs-lookup"><span data-stu-id="dd862-213">In the **Data context class** drop-down,  select **ContosoUniversity.Models.SchoolContext**</span></span>
* <span data-ttu-id="dd862-214">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="dd862-214">Select **Add**.</span></span>

![CRUD 对话框](intro/_static/s1.png)

<span data-ttu-id="dd862-216">如果对前面的步骤有疑问，请参阅[搭建“电影”模型的基架](xref:tutorials/razor-pages/model#scaffold-the-movie-model)。</span><span class="sxs-lookup"><span data-stu-id="dd862-216">See [Scaffold the movie model](xref:tutorials/razor-pages/model#scaffold-the-movie-model) if you have a problem with the preceding step.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="dd862-217">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="dd862-217">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="dd862-218">运行以下命令，搭建“学生”模型的基架。</span><span class="sxs-lookup"><span data-stu-id="dd862-218">Run the following commands to scaffold the student model.</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 2.1.0
dotnet aspnet-codegenerator razorpage -m Student -dc ContosoUniversity.Models.SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
```
------

<span data-ttu-id="dd862-219">搭建基架的过程会创建并更改以下文件：</span><span class="sxs-lookup"><span data-stu-id="dd862-219">The scaffold process created and changed the following files:</span></span>

### <a name="files-created"></a><span data-ttu-id="dd862-220">创建的文件</span><span class="sxs-lookup"><span data-stu-id="dd862-220">Files created</span></span>

* <span data-ttu-id="dd862-221">Pages/Students：“创建”、“删除”、“详细信息”、“编辑”、“索引”。</span><span class="sxs-lookup"><span data-stu-id="dd862-221">*Pages/Students* Create, Delete, Details, Edit, Index.</span></span>
* <span data-ttu-id="dd862-222">Data/ContosoUniversityContext.cs</span><span class="sxs-lookup"><span data-stu-id="dd862-222">*Data/ContosoUniversityContext.cs*</span></span>

### <a name="files-updates"></a><span data-ttu-id="dd862-223">文件更新</span><span class="sxs-lookup"><span data-stu-id="dd862-223">Files updates</span></span>

* <span data-ttu-id="dd862-224">Startup.cs：在下一部分详细介绍对此文件所做更改。</span><span class="sxs-lookup"><span data-stu-id="dd862-224">*Startup.cs* : Changes to this file in are detailed the next section.</span></span>
* <span data-ttu-id="dd862-225">appsettings.json：添加用于连接到本地数据的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="dd862-225">*appsettings.json* : The connection string used to connect to a local database is added.</span></span>

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="dd862-226">检查通过依赖关系注入注册的上下文</span><span class="sxs-lookup"><span data-stu-id="dd862-226">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="dd862-227">ASP.NET Core 通过[依赖关系注入](xref:fundamentals/dependency-injection)进行生成。</span><span class="sxs-lookup"><span data-stu-id="dd862-227">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="dd862-228">服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="dd862-228">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="dd862-229">需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="dd862-229">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="dd862-230">本教程的后续部分介绍了用于获取数据库上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="dd862-230">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="dd862-231">基架工具自动创建 DB 上下文并将其注册到依赖关系注入容器。</span><span class="sxs-lookup"><span data-stu-id="dd862-231">The scaffolding tool automatically created a DB Context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="dd862-232">在 Startup.cs 中检查 `ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="dd862-232">Examine the `ConfigureServices` method in *Startup.cs*.</span></span> <span data-ttu-id="dd862-233">基架添加了突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="dd862-233">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](intro/samples/cu21/Startup.cs?name=snippet_SchoolContext&highlight=13-14)]

<span data-ttu-id="dd862-234">通过调用 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 对象中的一个方法将连接字符串名称传递到上下文。</span><span class="sxs-lookup"><span data-stu-id="dd862-234">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="dd862-235">进行本地开发时， [ASP.NET Core 配置系统](xref:fundamentals/configuration/index) 在 *appsettings.json* 文件中读取数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="dd862-235">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

## <a name="update-main"></a><span data-ttu-id="dd862-236">更新 main</span><span class="sxs-lookup"><span data-stu-id="dd862-236">Update main</span></span>

<span data-ttu-id="dd862-237">在 Program.cs 中，修改 `Main` 方法以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="dd862-237">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="dd862-238">从依赖关系注入容器获取数据库上下文实例。</span><span class="sxs-lookup"><span data-stu-id="dd862-238">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="dd862-239">调用 [EnsureCreated](/dotnet/api/microsoft.entityframeworkcore.infrastructure.databasefacade.ensurecreated#Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_EnsureCreated)。</span><span class="sxs-lookup"><span data-stu-id="dd862-239">Call the  [EnsureCreated](/dotnet/api/microsoft.entityframeworkcore.infrastructure.databasefacade.ensurecreated#Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_EnsureCreated).</span></span>
* <span data-ttu-id="dd862-240">`EnsureCreated` 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="dd862-240">Dispose the context when the `EnsureCreated` method completes.</span></span>

<span data-ttu-id="dd862-241">下面的代码显示更新后的 Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="dd862-241">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[](intro/samples/cu21/Program.cs?name=snippet)]

<span data-ttu-id="dd862-242">`EnsureCreated` 确保存在上下文数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-242">`EnsureCreated` ensures that the database for the context exists.</span></span> <span data-ttu-id="dd862-243">如果存在，则不需要任何操作。</span><span class="sxs-lookup"><span data-stu-id="dd862-243">If it exists, no action is taken.</span></span> <span data-ttu-id="dd862-244">如果不存在，则会创建数据库及其所有架构。</span><span class="sxs-lookup"><span data-stu-id="dd862-244">If it does not exist, then the database and all its schema are created.</span></span> <span data-ttu-id="dd862-245">`EnsureCreated` 不使用迁移创建数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-245">`EnsureCreated` does not use migrations to create the database.</span></span> <span data-ttu-id="dd862-246">使用 `EnsureCreated` 创建的数据库稍后无法使用迁移更新。</span><span class="sxs-lookup"><span data-stu-id="dd862-246">A database that is created with `EnsureCreated` cannot be later updated using migrations.</span></span>

<span data-ttu-id="dd862-247">启动应用时会调用 `EnsureCreated`，以进行以下工作流：</span><span class="sxs-lookup"><span data-stu-id="dd862-247">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="dd862-248">删除数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-248">Delete the DB.</span></span>
* <span data-ttu-id="dd862-249">更改数据库架构（例如添加一个 `EmailAddress` 字段）。</span><span class="sxs-lookup"><span data-stu-id="dd862-249">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="dd862-250">运行应用。</span><span class="sxs-lookup"><span data-stu-id="dd862-250">Run the app.</span></span>
* <span data-ttu-id="dd862-251">`EnsureCreated` 创建一个带有 `EmailAddress` 列的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-251">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

<span data-ttu-id="dd862-252">架构快速演变时，在开发初期使用 `EnsureCreated` 很方便。</span><span class="sxs-lookup"><span data-stu-id="dd862-252">`EnsureCreated` is convenient early in development when the schema is rapidly evolving.</span></span> <span data-ttu-id="dd862-253">本教程后面将删除 DB 并使用迁移。</span><span class="sxs-lookup"><span data-stu-id="dd862-253">Later in the tutorial the DB is deleted and migrations are used.</span></span>

### <a name="test-the-app"></a><span data-ttu-id="dd862-254">测试应用</span><span class="sxs-lookup"><span data-stu-id="dd862-254">Test the app</span></span>

<span data-ttu-id="dd862-255">运行应用并接受 cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="dd862-255">Run the app and accept the cookie policy.</span></span> <span data-ttu-id="dd862-256">此应用不保留个人信息。</span><span class="sxs-lookup"><span data-stu-id="dd862-256">This app doesn't keep personal information.</span></span> <span data-ttu-id="dd862-257">有关 cookie 策略的信息，请参阅[欧盟一般数据保护条例 (GDPR) 支持](xref:security/gdpr)。</span><span class="sxs-lookup"><span data-stu-id="dd862-257">You can read about the cookie policy at [EU General Data Protection Regulation (GDPR) support](xref:security/gdpr).</span></span>

* <span data-ttu-id="dd862-258">依次选择“学生”链接、“新建”。</span><span class="sxs-lookup"><span data-stu-id="dd862-258">Select the **Students** link and then **Create New**.</span></span>
* <span data-ttu-id="dd862-259">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="dd862-259">Test the Edit, Details, and Delete links.</span></span>

## <a name="examine-the-schoolcontext-db-context"></a><span data-ttu-id="dd862-260">检查 SchoolContext DB 上下文</span><span class="sxs-lookup"><span data-stu-id="dd862-260">Examine the SchoolContext DB context</span></span>

<span data-ttu-id="dd862-261">数据库上下文类是为给定数据模型协调 EF Core 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="dd862-261">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="dd862-262">数据上下文派生自 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)。</span><span class="sxs-lookup"><span data-stu-id="dd862-262">The data context is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="dd862-263">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-263">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="dd862-264">在此项目中将数据库上下文类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="dd862-264">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="dd862-265">使用以下代码更新 SchoolContext.cs：</span><span class="sxs-lookup"><span data-stu-id="dd862-265">Update *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu21/Data/SchoolContext.cs?name=snippet_Intro&highlight=12-14)]

<span data-ttu-id="dd862-266">突出显示的代码为每个实体集创建 [DbSet\<TEntity>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 属性。</span><span class="sxs-lookup"><span data-stu-id="dd862-266">The highlighted code creates a [DbSet\<TEntity>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for each entity set.</span></span> <span data-ttu-id="dd862-267">在 EF Core 术语中：</span><span class="sxs-lookup"><span data-stu-id="dd862-267">In EF Core terminology:</span></span>

* <span data-ttu-id="dd862-268">实体集通常对应一个数据库表。</span><span class="sxs-lookup"><span data-stu-id="dd862-268">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="dd862-269">实体对应表中的行。</span><span class="sxs-lookup"><span data-stu-id="dd862-269">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="dd862-270">可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>`。</span><span class="sxs-lookup"><span data-stu-id="dd862-270">`DbSet<Enrollment>` and `DbSet<Course>` could be omitted.</span></span> <span data-ttu-id="dd862-271">EF Core 隐式包含了它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="dd862-271">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="dd862-272">在本教程中，将 `DbSet<Enrollment>` 和 `DbSet<Course>` 保留在 `SchoolContext` 中。</span><span class="sxs-lookup"><span data-stu-id="dd862-272">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="dd862-273">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="dd862-273">SQL Server Express LocalDB</span></span>

<span data-ttu-id="dd862-274">连接字符串指定 [SQL Server LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。</span><span class="sxs-lookup"><span data-stu-id="dd862-274">The connection string specifies [SQL Server LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="dd862-275">LocalDB 是轻型版本 SQL Server Express 数据库引擎，专门针对应用开发，而非生产使用。</span><span class="sxs-lookup"><span data-stu-id="dd862-275">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="dd862-276">LocalDB 作为按需启动并在用户模式下运行的轻量级数据库没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="dd862-276">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="dd862-277">默认情况下，LocalDB 会在 `C:/Users/<user>` 目录中创建 .mdf 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="dd862-277">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="dd862-278">添加代码，以使用测试数据初始化该数据库</span><span class="sxs-lookup"><span data-stu-id="dd862-278">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="dd862-279">EF Core 会创建一个空的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-279">EF Core creates an empty DB.</span></span> <span data-ttu-id="dd862-280">本部分中编写了 `Initialize` 方法来使用测试数据填充该数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-280">In this section, an `Initialize` method is written to populate it with test data.</span></span>

<span data-ttu-id="dd862-281">在 Data 文件夹中，新建一个名为 DbInitializer.cs 的类文件，并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="dd862-281">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[](intro/samples/cu21/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="dd862-282">该代码会检查数据库中是否存在任何学生。</span><span class="sxs-lookup"><span data-stu-id="dd862-282">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="dd862-283">如果 DB 中没有任何学生，则会使用测试数据初始化该 DB。</span><span class="sxs-lookup"><span data-stu-id="dd862-283">If there are no students in the DB, the DB is initialized with test data.</span></span> <span data-ttu-id="dd862-284">代码中使用数组存放测试数据而不是使用 `List<T>` 集合是为了优化性能。</span><span class="sxs-lookup"><span data-stu-id="dd862-284">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="dd862-285">`EnsureCreated` 方法自动为数据库上下文创建数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-285">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="dd862-286">如果数据库已存在，则返回 `EnsureCreated`，并且不修改数据库。</span><span class="sxs-lookup"><span data-stu-id="dd862-286">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="dd862-287">在 Program.cs 中，将 `Main` 方法修改为调用 `Initialize`：</span><span class="sxs-lookup"><span data-stu-id="dd862-287">In *Program.cs*, modify the `Main` method to call `Initialize`:</span></span>

[!code-csharp[](intro/samples/cu21/Program.cs?name=snippet2&highlight=14-15)]

<span data-ttu-id="dd862-288">删除任何学生记录并重启应用。</span><span class="sxs-lookup"><span data-stu-id="dd862-288">Delete any student records and restart the app.</span></span> <span data-ttu-id="dd862-289">如果未初始化 DB，则在 `Initialize` 中设置断点以诊断问题。</span><span class="sxs-lookup"><span data-stu-id="dd862-289">If the DB is not initialized, set a break point in `Initialize` to diagnose the problem.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="dd862-290">查看数据库</span><span class="sxs-lookup"><span data-stu-id="dd862-290">View the DB</span></span>

<span data-ttu-id="dd862-291">从 Visual Studio 中的“视图”菜单打开 SQL Server 对象资源管理器 (SSOX)。</span><span class="sxs-lookup"><span data-stu-id="dd862-291">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="dd862-292">在 SSOX 中，单击“(localdb)\MSSQLLocalDB”>“数据库”>“ContosoUniversity1”。</span><span class="sxs-lookup"><span data-stu-id="dd862-292">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="dd862-293">展开“表”节点。</span><span class="sxs-lookup"><span data-stu-id="dd862-293">Expand the **Tables** node.</span></span>

<span data-ttu-id="dd862-294">右键单击 Student 表，然后单击“查看数据”，以查看创建的列和插入到表中的行。</span><span class="sxs-lookup"><span data-stu-id="dd862-294">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="dd862-295">异步代码</span><span class="sxs-lookup"><span data-stu-id="dd862-295">Asynchronous code</span></span>

<span data-ttu-id="dd862-296">异步编程是 ASP.NET Core 和 EF Core 的默认模式。</span><span class="sxs-lookup"><span data-stu-id="dd862-296">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="dd862-297">Web 服务器的可用线程是有限的，而在高负载情况下的可能所有线程都被占用。</span><span class="sxs-lookup"><span data-stu-id="dd862-297">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="dd862-298">当发生这种情况的时候，服务器就无法处理新请求，直到线程被释放。</span><span class="sxs-lookup"><span data-stu-id="dd862-298">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="dd862-299">使用同步代码时，可能会出现多个线程被占用但不能执行任何操作的情况，因为它们正在等待 I/O 完成。</span><span class="sxs-lookup"><span data-stu-id="dd862-299">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="dd862-300">使用异步代码时，当进程正在等待 I/O 完成，服务器可以将其线程释放用于处理其他请求。</span><span class="sxs-lookup"><span data-stu-id="dd862-300">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="dd862-301">因此，使用异步代码可以更有效地利用服务器资源，并且可以让服务器在没有延迟的情况下处理更多流量。</span><span class="sxs-lookup"><span data-stu-id="dd862-301">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="dd862-302">异步代码会在运行时引入少量开销。</span><span class="sxs-lookup"><span data-stu-id="dd862-302">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="dd862-303">流量较低时，对性能的影响可以忽略不计，但流量较高时，潜在的性能改善非常显著。</span><span class="sxs-lookup"><span data-stu-id="dd862-303">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="dd862-304">在以下代码中，[async](/dotnet/csharp/language-reference/keywords/async) 关键字和 `Task<T>` 返回值，`await` 关键字和 `ToListAsync` 方法让代码异步执行。</span><span class="sxs-lookup"><span data-stu-id="dd862-304">In the following code, the [async](/dotnet/csharp/language-reference/keywords/async) keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[](intro/samples/cu21/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="dd862-305">`async` 关键字让编译器执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="dd862-305">The `async` keyword tells the compiler to:</span></span>
  * <span data-ttu-id="dd862-306">为方法主体的各部分生成回调。</span><span class="sxs-lookup"><span data-stu-id="dd862-306">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="dd862-307">自动创建返回的 [Task](/dotnet/api/system.threading.tasks.task) 对象。</span><span class="sxs-lookup"><span data-stu-id="dd862-307">Automatically create the [Task](/dotnet/api/system.threading.tasks.task) object that's returned.</span></span> <span data-ttu-id="dd862-308">有关详细信息，请参阅[任务返回类型](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)。</span><span class="sxs-lookup"><span data-stu-id="dd862-308">For more information, see [Task Return Type](/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="dd862-309">隐式返回类型 `Task` 表示正在进行的工作。</span><span class="sxs-lookup"><span data-stu-id="dd862-309">The implicit return type `Task` represents ongoing work.</span></span>
* <span data-ttu-id="dd862-310">`await` 关键字让编译器将该方法拆分为两个部分。</span><span class="sxs-lookup"><span data-stu-id="dd862-310">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="dd862-311">第一部分是以异步方式结束已启动的操作。</span><span class="sxs-lookup"><span data-stu-id="dd862-311">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="dd862-312">第二部分是当操作完成时注入调用回调方法的地方。</span><span class="sxs-lookup"><span data-stu-id="dd862-312">The second part is put into a callback method that's called when the operation completes.</span></span>
* <span data-ttu-id="dd862-313">`ToListAsync` 是 `ToList` 扩展方法的异步版本。</span><span class="sxs-lookup"><span data-stu-id="dd862-313">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="dd862-314">编写使用 EF Core 的异步代码时需要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="dd862-314">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="dd862-315">只会异步执行导致查询或命令被发送到数据库的语句。</span><span class="sxs-lookup"><span data-stu-id="dd862-315">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="dd862-316">这包括 `ToListAsync`、`SingleOrDefaultAsync`、`FirstOrDefaultAsync` 和 `SaveChangesAsync`。</span><span class="sxs-lookup"><span data-stu-id="dd862-316">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="dd862-317">不包括只会更改 `IQueryable` 的语句，例如 `var students = context.Students.Where(s => s.LastName == "Davolio")`。</span><span class="sxs-lookup"><span data-stu-id="dd862-317">It doesn't include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>
* <span data-ttu-id="dd862-318">EF Core 上下文并非线程安全：请勿尝试并行执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="dd862-318">An EF Core context isn't thread safe: don't try to do multiple operations in parallel.</span></span>
* <span data-ttu-id="dd862-319">若要利用异步代码的性能优势，请验证在调用向数据库发送查询的 EF Core 方法时，库程序包（如用于分页）是否使用异步。</span><span class="sxs-lookup"><span data-stu-id="dd862-319">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="dd862-320">有关 .NET 中异步编程的详细信息，请参阅[异步概述](/dotnet/articles/standard/async)和[使用 Async 和 Await 的异步编程](/dotnet/csharp/programming-guide/concepts/async/)。</span><span class="sxs-lookup"><span data-stu-id="dd862-320">For more information about asynchronous programming in .NET, see [Async Overview](/dotnet/articles/standard/async) and [Asynchronous programming with async and await](/dotnet/csharp/programming-guide/concepts/async/).</span></span>

<span data-ttu-id="dd862-321">下一个教程将介绍基本的 CRUD（创建、读取、更新、删除）操作。</span><span class="sxs-lookup"><span data-stu-id="dd862-321">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>
::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="dd862-322">下一篇</span><span class="sxs-lookup"><span data-stu-id="dd862-322">Next</span></span>](xref:data/ef-rp/crud)