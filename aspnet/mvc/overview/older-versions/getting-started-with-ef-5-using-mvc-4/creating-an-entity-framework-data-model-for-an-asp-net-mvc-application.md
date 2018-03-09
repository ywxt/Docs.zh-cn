---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: "为 ASP.NET MVC 应用程序 (第 1 个 10) 创建的实体框架数据模型 |Microsoft 文档"
author: tdykstra
description: "本系列教程的较新版本可用，则 Visual Studio 2013、 Entity Framework 6 和 MVC 5。 Contoso 大学示例 web 应用程序 de..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8c9971ccc70cb4b966abb64086b1b5420fc6c72a
ms.sourcegitcommit: 53ee14b9c8200f44705d8997c3619fa874192d45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
<a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a><span data-ttu-id="e1396-104">为 ASP.NET MVC 应用程序 (第 1 个 10) 创建的实体框架数据模型</span><span class="sxs-lookup"><span data-stu-id="e1396-104">Creating an Entity Framework Data Model for an ASP.NET MVC Application (1 of 10)</span></span>
====================
<span data-ttu-id="e1396-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e1396-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e1396-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="e1396-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > <span data-ttu-id="e1396-107">A[较新版本的本系列教程](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)可用，Visual Studio 2013、 Entity Framework 6 和 MVC 5。</span><span class="sxs-lookup"><span data-stu-id="e1396-107">A [newer version of this tutorial series](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) is available, for Visual Studio 2013, Entity Framework 6, and MVC 5.</span></span>
> 
> 
> <span data-ttu-id="e1396-108">Contoso 大学示例 web 应用程序演示如何创建使用实体框架 5 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e1396-108">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 and Visual Studio 2012.</span></span> <span data-ttu-id="e1396-109">该示例应用程序是一个虚构的 Contoso University 的网站。</span><span class="sxs-lookup"><span data-stu-id="e1396-109">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="e1396-110">其中包括学生录取、课程创建和讲师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="e1396-110">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="e1396-111">本系列教程说明如何生成 Contoso 大学示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="e1396-111">This tutorial series explains how to build the Contoso University sample application.</span></span> <span data-ttu-id="e1396-112">你可以[下载已完成的应用程序](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)。</span><span class="sxs-lookup"><span data-stu-id="e1396-112">You can [download the completed application](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8).</span></span>
> 
> ## <a name="code-first"></a><span data-ttu-id="e1396-113">Code First</span><span class="sxs-lookup"><span data-stu-id="e1396-113">Code First</span></span>
> 
> <span data-ttu-id="e1396-114">有三种方法可以使用的实体框架中的数据： *Database First*， *Model First*，和*Code First*。</span><span class="sxs-lookup"><span data-stu-id="e1396-114">There are three ways you can work with data in the Entity Framework: *Database First*, *Model First*, and *Code First*.</span></span> <span data-ttu-id="e1396-115">此教程适用于第一个代码。</span><span class="sxs-lookup"><span data-stu-id="e1396-115">This tutorial is for Code First.</span></span> <span data-ttu-id="e1396-116">有关如何为你的方案选择最佳这些工作流和指南之间的差异信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。</span><span class="sxs-lookup"><span data-stu-id="e1396-116">For information about the differences between these workflows and guidance on how to choose the best one for your scenario, see [Entity Framework Development Workflows](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>
> 
> ## <a name="mvc"></a><span data-ttu-id="e1396-117">MVC</span><span class="sxs-lookup"><span data-stu-id="e1396-117">MVC</span></span>
> 
> <span data-ttu-id="e1396-118">示例应用程序基于[ASP.NET MVC](../../../index.md)。</span><span class="sxs-lookup"><span data-stu-id="e1396-118">The sample application is built on [ASP.NET MVC](../../../index.md).</span></span> <span data-ttu-id="e1396-119">如果想要使用的 ASP.NET Web 窗体模型，请参阅[模型绑定和 Web 窗体](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md)教程系列和[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="e1396-119">If you prefer to work with the ASP.NET Web Forms model, see the [Model Binding and Web Forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) tutorial series and [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="e1396-120">软件版本</span><span class="sxs-lookup"><span data-stu-id="e1396-120">Software versions</span></span>
> 
> | <span data-ttu-id="e1396-121">**本教程中所示**</span><span class="sxs-lookup"><span data-stu-id="e1396-121">**Shown in the tutorial**</span></span> | <span data-ttu-id="e1396-122">**也适用于**</span><span class="sxs-lookup"><span data-stu-id="e1396-122">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="e1396-123">Windows 8</span><span class="sxs-lookup"><span data-stu-id="e1396-123">Windows 8</span></span> | <span data-ttu-id="e1396-124">Windows 7</span><span class="sxs-lookup"><span data-stu-id="e1396-124">Windows 7</span></span> |
> | <span data-ttu-id="e1396-125">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e1396-125">Visual Studio 2012</span></span> | <span data-ttu-id="e1396-126">Visual Studio 2012 Express for Web.</span><span class="sxs-lookup"><span data-stu-id="e1396-126">Visual Studio 2012 Express for Web.</span></span> <span data-ttu-id="e1396-127">这会自动安装 Windows Azure sdk，如果你还没有 VS 2012 或 VS 2012 Express for Web。</span><span class="sxs-lookup"><span data-stu-id="e1396-127">This is automatically installed by the Windows Azure SDK if you don't already have VS 2012 or VS 2012 Express for Web.</span></span> <span data-ttu-id="e1396-128">应运行 visual Studio 2013，但本教程未进行测试，并且某些菜单选项和对话框都有所不同。</span><span class="sxs-lookup"><span data-stu-id="e1396-128">Visual Studio 2013 should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> <span data-ttu-id="e1396-129">[VS 2013 版本的 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510)是 Windows Azure 部署所必需的。</span><span class="sxs-lookup"><span data-stu-id="e1396-129">The [VS 2013 version of the Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510) is required for Windows Azure deployment.</span></span> |
> | <span data-ttu-id="e1396-130">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e1396-130">.NET 4.5</span></span> | <span data-ttu-id="e1396-131">大多数所示的功能将适用于.NET 4 中，但某些不会。</span><span class="sxs-lookup"><span data-stu-id="e1396-131">Most of the features shown will work in .NET 4, but some won't.</span></span> <span data-ttu-id="e1396-132">例如，EF 中的枚举支持需要.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="e1396-132">For example, enum support in EF requires .NET 4.5.</span></span> |
> | <span data-ttu-id="e1396-133">实体框架 5</span><span class="sxs-lookup"><span data-stu-id="e1396-133">Entity Framework 5</span></span> |  |
> | [<span data-ttu-id="e1396-134">Windows Azure SDK 2.1</span><span class="sxs-lookup"><span data-stu-id="e1396-134">Windows Azure SDK 2.1</span></span>](https://go.microsoft.com/fwlink/p/?linkid=323511) | <span data-ttu-id="e1396-135">如果你跳过 Windows Azure 部署步骤，则不需要 SDK。</span><span class="sxs-lookup"><span data-stu-id="e1396-135">If you skip the Windows Azure deployment steps, you don't need the SDK.</span></span> <span data-ttu-id="e1396-136">当发布新版本的 SDK 后时，该链接将安装较新版本。</span><span class="sxs-lookup"><span data-stu-id="e1396-136">When a new version of the SDK is released, the link will install the newer version.</span></span> <span data-ttu-id="e1396-137">在这种情况下，你可能需要调整某些新 UI 和功能的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="e1396-137">In that case, you might have to adapt some of the instructions to new UI and features.</span></span> |
> 
> ## <a name="questions"></a><span data-ttu-id="e1396-138">问题</span><span class="sxs-lookup"><span data-stu-id="e1396-138">Questions</span></span>
> 
> <span data-ttu-id="e1396-139">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)、[实体框架和 LINQ to Entities 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="e1396-139">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx), the [Entity Framework and LINQ to Entities forum](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), or [StackOverflow.com](http://stackoverflow.com/).</span></span>
> 
> ## <a name="acknowledgments"></a><span data-ttu-id="e1396-140">致谢</span><span class="sxs-lookup"><span data-stu-id="e1396-140">Acknowledgments</span></span>
> 
> <span data-ttu-id="e1396-141">请参阅中的序列的最后一个教程[确认和有关 VB 注释](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)。</span><span class="sxs-lookup"><span data-stu-id="e1396-141">See the last tutorial in the series for [acknowledgments and a note about VB](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments).</span></span>
> 
> ## <a name="original-version-of-the-tutorial"></a><span data-ttu-id="e1396-142">本教程的原始版本</span><span class="sxs-lookup"><span data-stu-id="e1396-142">Original version of the tutorial</span></span>
> 
> <span data-ttu-id="e1396-143">本教程的原始版本位于[EF 4.1 / MVC 3 电子书](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)。</span><span class="sxs-lookup"><span data-stu-id="e1396-143">The original version of the tutorial is available in the [EF 4.1 / MVC 3 e-book](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC).</span></span>


## <a name="the-contoso-university-web-application"></a><span data-ttu-id="e1396-144">Contoso 大学 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e1396-144">The Contoso University Web Application</span></span>

<span data-ttu-id="e1396-145">将在这些教程中构建的应用程序是一个简单的大学网站。</span><span class="sxs-lookup"><span data-stu-id="e1396-145">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="e1396-146">用户可以查看和更新学生、课程和讲师信息。</span><span class="sxs-lookup"><span data-stu-id="e1396-146">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="e1396-147">以下是你将创建的几个屏幕。</span><span class="sxs-lookup"><span data-stu-id="e1396-147">Here are a few of the screens you'll create.</span></span>

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="e1396-149">该网站的 UI 样式与通过内置模板生成的 UI 样式十分接近，因此本教程主要着重介绍如何使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="e1396-149">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1396-150">系统必备</span><span class="sxs-lookup"><span data-stu-id="e1396-150">Prerequisites</span></span>

<span data-ttu-id="e1396-151">说明和屏幕快照，在本教程假定你使用的[Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads)或[Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)、 使用最新的更新和 Azure SDK for.NET 截至 7 月，安装2013。</span><span class="sxs-lookup"><span data-stu-id="e1396-151">The directions and screen shots in this tutorial assume that you're using [Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) or [Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131), with the latest update and Azure SDK for .NET installed as of July, 2013.</span></span> <span data-ttu-id="e1396-152">你可以获得所有这些都可以通过以下链接：</span><span class="sxs-lookup"><span data-stu-id="e1396-152">You can get all of this with the following link:</span></span>

[<span data-ttu-id="e1396-153">Azure SDK for.NET (Visual Studio 2012)</span><span class="sxs-lookup"><span data-stu-id="e1396-153">Azure SDK for .NET (Visual Studio 2012)</span></span>](https://go.microsoft.com/fwlink/?LinkId=254364)

<span data-ttu-id="e1396-154">如果你安装了 Visual Studio，上面的链接将安装缺少的任何组件。</span><span class="sxs-lookup"><span data-stu-id="e1396-154">If you have Visual Studio installed, the link above will install any missing components.</span></span> <span data-ttu-id="e1396-155">如果你没有 Visual Studio，该链接将安装 Visual Studio 2012 Express for Web。</span><span class="sxs-lookup"><span data-stu-id="e1396-155">If you don't have Visual Studio, the link will install Visual Studio 2012 Express for Web.</span></span> <span data-ttu-id="e1396-156">可以使用 Visual Studio 2013 中，但某些必需的过程和屏幕将有所不同。</span><span class="sxs-lookup"><span data-stu-id="e1396-156">You can use Visual Studio 2013, but some of the required procedures and screens will differ.</span></span>

## <a name="create-an-mvc-web-application"></a><span data-ttu-id="e1396-157">创建 MVC Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e1396-157">Create an MVC Web Application</span></span>

<span data-ttu-id="e1396-158">打开 Visual Studio 并创建一个新 C# 项目名为"ContosoUniversity"使用**ASP.NET MVC 4 Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="e1396-158">Open Visual Studio and create a new C# project named "ContosoUniversity" using the **ASP.NET MVC 4 Web Application** template.</span></span> <span data-ttu-id="e1396-159">请确保针对**.NET Framework 4.5** (你将使用[`enum`属性](https://msdn.microsoft.com/data/hh859576.aspx)，并且需要.NET 4.5)。</span><span class="sxs-lookup"><span data-stu-id="e1396-159">Make sure you target **.NET Framework 4.5** (you'll be using [`enum` properties](https://msdn.microsoft.com/data/hh859576.aspx), and that requires .NET 4.5).</span></span>

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="e1396-161">在**新建 ASP.NET MVC 4 项目**对话框框中，选择**Internet 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="e1396-161">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template.</span></span>

<span data-ttu-id="e1396-162">保留**Razor**查看引擎选择，并使**创建单元测试项目**清除复选框。</span><span class="sxs-lookup"><span data-stu-id="e1396-162">Leave the **Razor** view engine selected, and leave the **Create a unit test project** check box cleared.</span></span>

<span data-ttu-id="e1396-163">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="e1396-163">Click **OK**.</span></span>

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a><span data-ttu-id="e1396-165">设置站点样式</span><span class="sxs-lookup"><span data-stu-id="e1396-165">Set Up the Site Style</span></span>

<span data-ttu-id="e1396-166">设置网站菜单、布局和主页时需作少量简单更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-166">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="e1396-167">打开*views/shared\\_Layout.cshtml*，并将文件的内容替换下面的代码。</span><span class="sxs-lookup"><span data-stu-id="e1396-167">Open *Views\Shared\\_Layout.cshtml*, and replace the contents of the file with the following code.</span></span> <span data-ttu-id="e1396-168">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-168">The changes are highlighted.</span></span>

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

<span data-ttu-id="e1396-169">此代码会更改以下内容：</span><span class="sxs-lookup"><span data-stu-id="e1396-169">This code makes the following changes:</span></span>

- <span data-ttu-id="e1396-170">使用"Contoso 大学"替换"My ASP.NET MVC Application"和"your logo here"的模板实例。</span><span class="sxs-lookup"><span data-stu-id="e1396-170">Replaces the template instances of "My ASP.NET MVC Application" and "your logo here" with "Contoso University".</span></span>
- <span data-ttu-id="e1396-171">添加将在本教程后面部分使用的多个操作链接。</span><span class="sxs-lookup"><span data-stu-id="e1396-171">Adds several action links that will be used later in the tutorial.</span></span>

<span data-ttu-id="e1396-172">在*Views\Home\Index.cshtml*，将文件的内容替换为以下代码以消除有关 ASP.NET 和 MVC 模板段落：</span><span class="sxs-lookup"><span data-stu-id="e1396-172">In *Views\Home\Index.cshtml*, replace the contents of the file with the following code to eliminate the template paragraphs about ASP.NET and MVC:</span></span>

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

<span data-ttu-id="e1396-173">在*Controllers\HomeController.cs*，更改的值`ViewBag.Message`中`Index`到"欢迎使用 Contoso 大学 ！"，如下面的示例中所示的操作方法：</span><span class="sxs-lookup"><span data-stu-id="e1396-173">In *Controllers\HomeController.cs*, change the value for `ViewBag.Message` in the `Index` Action method to "Welcome to Contoso University!", as shown in the following example:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

<span data-ttu-id="e1396-174">按 CTRL + F5 以运行该站点。</span><span class="sxs-lookup"><span data-stu-id="e1396-174">Press CTRL+F5 to run the site.</span></span> <span data-ttu-id="e1396-175">你看到与主菜单的主页。</span><span class="sxs-lookup"><span data-stu-id="e1396-175">You see the home page with the main menu.</span></span>

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a><span data-ttu-id="e1396-177">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="e1396-177">Create the Data Model</span></span>

<span data-ttu-id="e1396-178">接下来将创建 Contoso University 应用程序的实体类。</span><span class="sxs-lookup"><span data-stu-id="e1396-178">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="e1396-179">你将从开始以下三个实体：</span><span class="sxs-lookup"><span data-stu-id="e1396-179">You'll start with the following three entities:</span></span>

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="e1396-181">`Student` 和 `Enrollment` 实体之间存在一对多的关系，`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="e1396-181">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="e1396-182">换言之，一名学生可以登记任意数量的课程，一门课程可以包含任意数量的学生。</span><span class="sxs-lookup"><span data-stu-id="e1396-182">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="e1396-183">以下部分将为这几个实体中的每一个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="e1396-183">In the following sections you'll create a class for each one of these entities.</span></span>

> [!NOTE]
> <span data-ttu-id="e1396-184">如果你尝试编译项目，然后完成创建所有这些实体类，将收到编译器错误。</span><span class="sxs-lookup"><span data-stu-id="e1396-184">If you try to compile the project before you finish creating all of these entity classes, you'll get compiler errors.</span></span>


### <a name="the-student-entity"></a><span data-ttu-id="e1396-185">学生实体</span><span class="sxs-lookup"><span data-stu-id="e1396-185">The Student Entity</span></span>

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="e1396-187">在*模型*文件夹中，创建*Student.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="e1396-187">In the *Models* folder, create *Student.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="e1396-188">`StudentID` 属性将成为此类对应的数据库表的主键列。</span><span class="sxs-lookup"><span data-stu-id="e1396-188">The `StudentID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="e1396-189">默认情况下，实体框架将解释一个属性，名为`ID`或*classname* `ID`为主键。</span><span class="sxs-lookup"><span data-stu-id="e1396-189">By default, the Entity Framework interprets a property that's named `ID` or *classname* `ID` as the primary key.</span></span>

<span data-ttu-id="e1396-190">`Enrollments`属性是*导航属性*。</span><span class="sxs-lookup"><span data-stu-id="e1396-190">The `Enrollments` property is a *navigation property*.</span></span> <span data-ttu-id="e1396-191">导航属性包含与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="e1396-191">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="e1396-192">在这种情况下，`Enrollments`属性`Student`实体将保留所有`Enrollment`与该订阅相关的实体`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="e1396-192">In this case, the `Enrollments` property of a `Student` entity will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="e1396-193">换而言之，如果给定`Student`数据库中的行具有两个相关`Enrollment`行 (包含该学生的主键的行值在其`StudentID`外键列)，则该`Student`实体的`Enrollments`导航属性将包含这两个`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="e1396-193">In other words, if a given `Student` row in the database has two related `Enrollment` rows (rows that contain that student's primary key value in their `StudentID` foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="e1396-194">导航属性通常定义为`virtual`，以便它们可以充分利用某些实体框架功能，如*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="e1396-194">Navigation properties are typically defined as `virtual` so that they can take advantage of certain Entity Framework functionality such as *lazy loading*.</span></span> <span data-ttu-id="e1396-195">(将解释延迟加载更高版本，在[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)更高版本中这一系列教程。</span><span class="sxs-lookup"><span data-stu-id="e1396-195">(Lazy loading will be explained later, in the [Reading Related Data](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series.</span></span>

<span data-ttu-id="e1396-196">如果导航属性可包含多个实体（如多对多或一对多关系），则其类型必须是可添加、可删除和可更新实体的列表，如 `ICollection`。</span><span class="sxs-lookup"><span data-stu-id="e1396-196">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection`.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="e1396-197">注册实体</span><span class="sxs-lookup"><span data-stu-id="e1396-197">The Enrollment Entity</span></span>

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="e1396-199">在 Models 文件夹中，创建 Enrollment.cs，并使用以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="e1396-199">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="e1396-200">年级属性是[枚举](https://msdn.microsoft.com/data/hh859576.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1396-200">The Grade property is an [enum](https://msdn.microsoft.com/data/hh859576.aspx).</span></span> <span data-ttu-id="e1396-201">后问号`Grade`类型声明指示`Grade`属性是[可以为 null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1396-201">The question mark after the `Grade` type declaration indicates that the `Grade` property is [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx).</span></span> <span data-ttu-id="e1396-202">为 null 的等级是不同于零年级-null 意味着一个等级而言未知的或未尚未分配。</span><span class="sxs-lookup"><span data-stu-id="e1396-202">A grade that's null is different from a zero grade — null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="e1396-203">`StudentID` 属性是外键，其对应的导航属性为 `Student`。</span><span class="sxs-lookup"><span data-stu-id="e1396-203">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="e1396-204">`Enrollment` 实体与一个 `Student` 实体相关联，因此属性仅包含单个 `Student` 实体（而不像之前看到的 `Student.Enrollments` 导航属性，可包含多个 `Enrollment` 实体）。</span><span class="sxs-lookup"><span data-stu-id="e1396-204">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="e1396-205">`CourseID` 属性是外键，其对应的导航属性为 `Course`。</span><span class="sxs-lookup"><span data-stu-id="e1396-205">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="e1396-206">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="e1396-206">An `Enrollment` entity is associated with one `Course` entity.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="e1396-207">课程实体</span><span class="sxs-lookup"><span data-stu-id="e1396-207">The Course Entity</span></span>

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="e1396-209">在*模型*文件夹中，创建*Course.cs*，替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="e1396-209">In the *Models* folder, create *Course.cs*, replacing the existing code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="e1396-210">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="e1396-210">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="e1396-211">`Course` 实体可与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="e1396-211">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="e1396-212">我们举例更多有关 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)。无）] 特性在下一步的教程。</span><span class="sxs-lookup"><span data-stu-id="e1396-212">We'll say more about the [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx).None)] attribute in the next tutorial.</span></span> <span data-ttu-id="e1396-213">基本上，此特性允许你输入课程的主键，而不是在数据库中生成该主键。</span><span class="sxs-lookup"><span data-stu-id="e1396-213">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="e1396-214">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="e1396-214">Create the Database Context</span></span>

<span data-ttu-id="e1396-215">协调为给定的数据模型的实体框架功能的主类是*数据库上下文*类。</span><span class="sxs-lookup"><span data-stu-id="e1396-215">The main class that coordinates Entity Framework functionality for a given data model is the *database context* class.</span></span> <span data-ttu-id="e1396-216">通过派生自创建此类[System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)类。</span><span class="sxs-lookup"><span data-stu-id="e1396-216">You create this class by deriving from the [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) class.</span></span> <span data-ttu-id="e1396-217">在代码中指定包含在数据模型中的实体。</span><span class="sxs-lookup"><span data-stu-id="e1396-217">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="e1396-218">还可以自定义特定 Entity Framework 行为。</span><span class="sxs-lookup"><span data-stu-id="e1396-218">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="e1396-219">在此项目中，类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="e1396-219">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="e1396-220">创建名为的文件夹*DAL* （适用于数据访问层）。</span><span class="sxs-lookup"><span data-stu-id="e1396-220">Create a folder named *DAL* (for Data Access Layer).</span></span> <span data-ttu-id="e1396-221">在该文件夹中创建名为的新类文件*SchoolContext.cs*，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e1396-221">In that folder create a new class file named *SchoolContext.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="e1396-222">此代码将创建[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)每个实体集的属性。</span><span class="sxs-lookup"><span data-stu-id="e1396-222">This code creates a [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) property for each entity set.</span></span> <span data-ttu-id="e1396-223">在实体框架术语中，*实体集*通常对应于一个数据库表，和*实体*对应于表中的行。</span><span class="sxs-lookup"><span data-stu-id="e1396-223">In Entity Framework terminology, an *entity set* typically corresponds to a database table, and an *entity* corresponds to a row in the table.</span></span>

<span data-ttu-id="e1396-224">`modelBuilder.Conventions.Remove`中的语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)的方法阻止从正在变为复数形式的表名称。</span><span class="sxs-lookup"><span data-stu-id="e1396-224">The `modelBuilder.Conventions.Remove` statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method prevents table names from being pluralized.</span></span> <span data-ttu-id="e1396-225">如果你未执行此操作，生成的表将被命名为`Students`， `Courses`，和`Enrollments`。</span><span class="sxs-lookup"><span data-stu-id="e1396-225">If you didn't do this, the generated tables would be named `Students`, `Courses`, and `Enrollments`.</span></span> <span data-ttu-id="e1396-226">相反，则表名将为`Student`， `Course`，和`Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="e1396-226">Instead, the table names will be `Student`, `Course`, and `Enrollment`.</span></span> <span data-ttu-id="e1396-227">开发者对表名称是否应为复数意见不一。</span><span class="sxs-lookup"><span data-stu-id="e1396-227">Developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="e1396-228">本教程使用单数形式，但重要的一点是，可以选择你的首选，通过包括或忽略这行代码的任何一个窗体。</span><span class="sxs-lookup"><span data-stu-id="e1396-228">This tutorial uses the singular form, but the important point is that you can select whichever form you prefer by including or omitting this line of code.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="e1396-229">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="e1396-229">SQL Server Express LocalDB</span></span>

<span data-ttu-id="e1396-230">[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)是 SQL Server Express 数据库引擎的按需启动并在用户模式下运行的轻量版本。</span><span class="sxs-lookup"><span data-stu-id="e1396-230">[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="e1396-231">LocalDB 运行中的 SQL Server Express，可用于处理数据库作为一种特殊的执行模式*.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-231">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="e1396-232">通常，将 LocalDB 数据库文件保存在*应用\_数据*web 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e1396-232">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span> <span data-ttu-id="e1396-233">在 SQL Server Express 用户实例功能还可以使您能够使用*.mdf*文件，但用户实例功能已弃用; 因此，使用建议 LocalDB *.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-233">The user instance feature in SQL Server Express also enables you to work with *.mdf* files, but the user instance feature is deprecated; therefore, LocalDB is recommended for working with *.mdf* files.</span></span>

<span data-ttu-id="e1396-234">通常 SQL Server Express 不用于生产 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e1396-234">Typically SQL Server Express is not used for production web applications.</span></span> <span data-ttu-id="e1396-235">LocalDB 具体而言不是建议生产使用与 web 应用程序由于它不是使用 IIS。</span><span class="sxs-lookup"><span data-stu-id="e1396-235">LocalDB in particular is not recommended for production use with a web application because it is not designed to work with IIS.</span></span>

<span data-ttu-id="e1396-236">在 Visual Studio 2012 和更高版本中，默认情况下，使用 Visual Studio 安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="e1396-236">In Visual Studio 2012 and later versions, LocalDB is installed by default with Visual Studio.</span></span> <span data-ttu-id="e1396-237">在 Visual Studio 2010 和早期版本中，在使用 Visual Studio; 默认情况下安装 SQL Server Express （而不是 LocalDB)你必须手动安装，如果你使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="e1396-237">In Visual Studio 2010 and earlier versions, SQL Server Express (without LocalDB) is installed by default with Visual Studio; you have to install it manually if you're using Visual Studio 2010.</span></span>

<span data-ttu-id="e1396-238">在本教程中你将使用 LocalDB，以便数据库可以存储在*应用\_数据*文件夹作为*.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-238">In this tutorial you'll work with LocalDB so that the database can be stored in the *App\_Data* folder as an *.mdf* file.</span></span> <span data-ttu-id="e1396-239">打开根*Web.config*文件并添加到新的连接字符串`connectionStrings`集合，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="e1396-239">Open the root *Web.config* file and add a new connection string to the `connectionStrings` collection, as shown in the following example.</span></span> <span data-ttu-id="e1396-240">(请确保你更新*Web.config*根项目文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-240">(Make sure you update the *Web.config* file in the root project folder.</span></span> <span data-ttu-id="e1396-241">此外，还有*Web.config*文件位于*视图*无需更新的子文件夹。)</span><span class="sxs-lookup"><span data-stu-id="e1396-241">There's also a *Web.config* file is in the *Views* subfolder that you don't need to update.)</span></span>

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

<span data-ttu-id="e1396-242">默认情况下，实体框架将查找名为相同的连接字符串`DbContext`类 (`SchoolContext`为此项目)。</span><span class="sxs-lookup"><span data-stu-id="e1396-242">By default, the Entity Framework looks for a connection string named the same as the `DbContext` class (`SchoolContext` for this project).</span></span> <span data-ttu-id="e1396-243">你已添加的连接字符串指定一个名为的 LocalDB 数据库*ContosoUniversity.mdf*位于*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="e1396-243">The connection string you've added specifies a LocalDB database named *ContosoUniversity.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="e1396-244">有关详细信息，请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1396-244">For more information, see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="e1396-245">实际上不需要指定连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e1396-245">You don't actually need to specify the connection string.</span></span> <span data-ttu-id="e1396-246">如果你不提供的连接字符串，实体框架将为你创建一个;但是，数据库可能未采用*应用\_数据*应用程序文件夹。</span><span class="sxs-lookup"><span data-stu-id="e1396-246">If you don't supply a connection string, Entity Framework will create one for you; however, the database might not be in the *App\_data* folder of your app.</span></span> <span data-ttu-id="e1396-247">有关将在其中创建数据库的信息，请参阅[到新数据库 Code First](https://msdn.microsoft.com/data/jj193542)。</span><span class="sxs-lookup"><span data-stu-id="e1396-247">For information on where the database will be created, see [Code First to a New Database](https://msdn.microsoft.com/data/jj193542).</span></span>

<span data-ttu-id="e1396-248">`connectionStrings`集合还具有一个名为的连接字符串`DefaultConnection`用于成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-248">The `connectionStrings` collection also has a connection string named `DefaultConnection` which is used for the membership database.</span></span> <span data-ttu-id="e1396-249">将不在本教程中使用了成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-249">You won't be using the membership database in this tutorial.</span></span> <span data-ttu-id="e1396-250">两个连接字符串之间的唯一区别是数据库名称和名称属性值。</span><span class="sxs-lookup"><span data-stu-id="e1396-250">The only difference between the two connection strings is the database name and the name attribute value.</span></span>

## <a name="set-up-and-execute-a-code-first-migration"></a><span data-ttu-id="e1396-251">设置和执行代码的第一次迁移</span><span class="sxs-lookup"><span data-stu-id="e1396-251">Set up and Execute a Code First Migration</span></span>

<span data-ttu-id="e1396-252">当你首次开始开发应用程序时，你的数据模型更改通常情况下，和每次获取与数据库不同步的模型更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-252">When you first start to develop an application, your data model changes frequently, and each time the model changes it gets out of sync with the database.</span></span> <span data-ttu-id="e1396-253">你可以配置实体框架可以自动除去并重新创建数据库每次更改数据模型。</span><span class="sxs-lookup"><span data-stu-id="e1396-253">You can configure the Entity Framework to automatically drop and re-create the database each time you change the data model.</span></span> <span data-ttu-id="e1396-254">这不是尽早中开发的问题，因为测试数据很轻松地重新创建，但部署到生产环境后通常需要更新数据库架构，而不删除数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-254">This is not a problem early in development because test data is easily re-created, but after you have deployed to production you usually want to update the database schema without dropping the database.</span></span> <span data-ttu-id="e1396-255">使用迁移功能，Code First 更新而无需删除并重新创建它的数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-255">The Migrations feature enables Code First to update the database without dropping and re-creating it.</span></span> <span data-ttu-id="e1396-256">在新项目的开发周期的初期你可能想要使用[DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx)要删除、 重新创建重新植入到数据库每次将模型更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-256">Early in the development cycle of a new project you might want to use [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) to drop, recreate and re-seed the database each time the model changes.</span></span> <span data-ttu-id="e1396-257">一个你准备好部署应用程序，你可以将其转换为的迁移方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-257">One you get ready to deploy your application, you can convert to the migrations approach.</span></span> <span data-ttu-id="e1396-258">对于本教程中，你将仅使用迁移。</span><span class="sxs-lookup"><span data-stu-id="e1396-258">For this tutorial you'll only use migrations.</span></span> <span data-ttu-id="e1396-259">有关详细信息，请参阅[Code First 迁移](https://msdn.microsoft.com/data/jj591621)和[迁移段视频系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1396-259">For more information, see [Code First Migrations](https://msdn.microsoft.com/data/jj591621) and [Migrations Screencast Series](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx).</span></span>

### <a name="enable-code-first-migrations"></a><span data-ttu-id="e1396-260">启用 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="e1396-260">Enable Code First Migrations</span></span>

1. <span data-ttu-id="e1396-261">从**工具**菜单上，单击**库程序包管理器**然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="e1396-261">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span>

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. <span data-ttu-id="e1396-263">在`PM>`提示符处输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e1396-263">At the `PM>` prompt enter the following command:</span></span>

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![enable-migrations 命令](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    <span data-ttu-id="e1396-265">此命令创建*迁移*文件夹 ContosoUniversity 项目中，且在该文件夹中放入*Configuration.cs*可编辑以配置迁移的文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-265">This command creates a *Migrations* folder in the ContosoUniversity project, and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span>

    ![迁移文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    <span data-ttu-id="e1396-267">`Configuration`类包括`Seed`创建数据库时和每次更新后的数据模型更改时调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-267">The `Configuration` class includes a `Seed` method that is called when the database is created and every time it is updated after a data model change.</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    <span data-ttu-id="e1396-268">这样做的目的`Seed`方法是让你 Code First 将创建它或更新后，将测试数据插入数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-268">The purpose of this `Seed` method is to enable you to insert test data into the database after Code First creates it or updates it.</span></span>

### <a name="set-up-the-seed-method"></a><span data-ttu-id="e1396-269">设置 Seed 方法</span><span class="sxs-lookup"><span data-stu-id="e1396-269">Set up the Seed Method</span></span>

<span data-ttu-id="e1396-270">[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法运行 Code First 迁移创建数据库时和每次它更新到最新的迁移的数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-270">The [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs when Code First Migrations creates the database and every time it updates the database to the latest migration.</span></span> <span data-ttu-id="e1396-271">Seed 方法的目的是为了使您能够将数据插入到你的表之前应用程序将首次访问数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-271">The purpose of the Seed method is to enable you to insert data into your tables before the application accesses the database for the first time.</span></span>

<span data-ttu-id="e1396-272">在早期版本的 Code First，迁移已发布之前，这是常见的`Seed`方法来插入测试数据，因为与在开发过程中的每个模型更改，数据库没有完全删除和重新创建从零开始。</span><span class="sxs-lookup"><span data-stu-id="e1396-272">In earlier versions of Code First, before Migrations was released, it was common for `Seed` methods to insert test data, because with every model change during development the database had to be completely deleted and re-created from scratch.</span></span> <span data-ttu-id="e1396-273">使用 Code First 迁移，数据保留在数据库更改后的测试，因此包括中的测试数据[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法通常不是必需。</span><span class="sxs-lookup"><span data-stu-id="e1396-273">With Code First Migrations, test data is retained after database changes, so including test data in the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method is typically not necessary.</span></span> <span data-ttu-id="e1396-274">事实上，你不希望`Seed`方法插入测试数据，如果你将使用迁移来将数据库部署到生产环境，因为`Seed`方法将在生产中运行。</span><span class="sxs-lookup"><span data-stu-id="e1396-274">In fact, you don't want the `Seed` method to insert test data if you'll be using Migrations to deploy the database to production, because the `Seed` method will run in production.</span></span> <span data-ttu-id="e1396-275">在这种情况下你想`Seed`方法以将你想要在生产中插入的数据插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-275">In that case you want the `Seed` method to insert into the database only the data that you want to be inserted in production.</span></span> <span data-ttu-id="e1396-276">例如，你可能想要包括在实际部门名称的数据库`Department`表应用程序在生产环境中可用时。</span><span class="sxs-lookup"><span data-stu-id="e1396-276">For example, you might want the database to include actual department names in the `Department` table when the application becomes available in production.</span></span>

<span data-ttu-id="e1396-277">对于本教程，你将在使用迁移部署，但你`Seed`方法将是否仍要插入测试数据，以更加轻松地查看应用程序功能而无需手动插入大量数据的工作原理。</span><span class="sxs-lookup"><span data-stu-id="e1396-277">For this tutorial, you'll be using Migrations for deployment, but your `Seed` method will insert test data anyway in order to make it easier to see how application functionality works without having to manually insert a lot of data.</span></span>

1. <span data-ttu-id="e1396-278">内容替换*Configuration.cs*替换为以下代码，将测试数据加载到新数据库的文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-278">Replace the contents of the *Configuration.cs* file with the following code, which will load test data into the new database.</span></span> 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    <span data-ttu-id="e1396-279">[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法采用数据库上下文对象作为输入参数，并方法中的代码使用该对象将新实体添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-279">The [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method takes the database context object as an input parameter, and the code in the method uses that object to add new entities to the database.</span></span> <span data-ttu-id="e1396-280">对于每个实体类型的代码将创建新的实体的集合，将它们添加到相应[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)属性，然后将保存到数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-280">For each entity type, the code creates a collection of new entities, adds them to the appropriate [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) property, and then saves the changes to the database.</span></span> <span data-ttu-id="e1396-281">无需调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)后的实体的每个组的方法，按上文所述，但执行该操作可帮助你找到问题的源，如果代码写入数据库时发生异常。</span><span class="sxs-lookup"><span data-stu-id="e1396-281">It isn't necessary to call the [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) method after each group of entities, as is done here, but doing that helps you locate the source of a problem if an exception occurs while the code is writing to the database.</span></span>

    <span data-ttu-id="e1396-282">一些插入数据的语句使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法来执行"upsert"操作。</span><span class="sxs-lookup"><span data-stu-id="e1396-282">Some of the statements that insert data use the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method to perform an "upsert" operation.</span></span> <span data-ttu-id="e1396-283">因为`Seed`方法运行与每个迁移时，不能只是插入数据，因为你尝试添加的行已将存在后创建数据库的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="e1396-283">Because the `Seed` method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="e1396-284">"Upsert"操作可以防止如果你尝试插入的行已存在，但它会发生的错误***重写***对测试应用程序时可能已做的数据的任何更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-284">The "upsert" operation prevents errors that would happen if you try to insert a row that already exists, but it ***overrides*** any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="e1396-285">使用某些表中的测试数据您可能不希望这种情况： 在某些情况下在测试期间更改数据时所需更改后数据库更新保留。</span><span class="sxs-lookup"><span data-stu-id="e1396-285">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="e1396-286">在这种情况下要执行条件的插入操作： 仅当它尚不存在插入行。</span><span class="sxs-lookup"><span data-stu-id="e1396-286">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span> <span data-ttu-id="e1396-287">Seed 方法使用这两种方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-287">The Seed method uses both approaches.</span></span>

    <span data-ttu-id="e1396-288">第一个参数传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法指定要用于检查行是否已存在的属性。</span><span class="sxs-lookup"><span data-stu-id="e1396-288">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="e1396-289">你要提供，测试学生数据`LastName`属性可以用于此目的，因为每个列表中的最后一个名称是唯一的：</span><span class="sxs-lookup"><span data-stu-id="e1396-289">For the test student data that you are providing, the `LastName` property can be used for this purpose since each last name in the list is unique:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    <span data-ttu-id="e1396-290">此代码假定最后一个名称是唯一的。</span><span class="sxs-lookup"><span data-stu-id="e1396-290">This code assumes that last names are unique.</span></span> <span data-ttu-id="e1396-291">如果你手动添加具有重复的最后一名学生，你将获得以下异常下次执行迁移。</span><span class="sxs-lookup"><span data-stu-id="e1396-291">If you manually add a student with a duplicate last name, you'll get the following exception the next time you perform a migration.</span></span>

    <span data-ttu-id="e1396-292">序列包含多个元素</span><span class="sxs-lookup"><span data-stu-id="e1396-292">Sequence contains more than one element</span></span>

    <span data-ttu-id="e1396-293">有关详细信息`AddOrUpdate`方法，请参阅[负责使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)Julie Lerman 博客上。</span><span class="sxs-lookup"><span data-stu-id="e1396-293">For more information about the `AddOrUpdate` method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) on Julie Lerman's blog.</span></span>

    <span data-ttu-id="e1396-294">添加的代码`Enrollment`实体不使用`AddOrUpdate`方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-294">The code that adds `Enrollment` entities doesn't use the `AddOrUpdate` method.</span></span> <span data-ttu-id="e1396-295">它会检查实体是否已存在，以及插入该实体，如果它不存在。</span><span class="sxs-lookup"><span data-stu-id="e1396-295">It checks if an entity already exists and inserts the entity if it doesn't exist.</span></span> <span data-ttu-id="e1396-296">此方法将保留在迁移运行时，注册年级所做的更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-296">This approach will preserve changes you make to an enrollment grade when migrations run.</span></span> <span data-ttu-id="e1396-297">此代码循环访问的每个成员`Enrollment`[列表](https://msdn.microsoft.com/library/6sh2ey19.aspx)和如果数据库中未找到注册，它将注册添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-297">The code loops through each member of the `Enrollment`[List](https://msdn.microsoft.com/library/6sh2ey19.aspx) and if the enrollment is not found in the database, it adds the enrollment to the database.</span></span> <span data-ttu-id="e1396-298">第一次更新数据库，数据库将为空，，因此它会将添加每个注册。</span><span class="sxs-lookup"><span data-stu-id="e1396-298">The first time you update the database, the database will be empty, so it will add each enrollment.</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    <span data-ttu-id="e1396-299">有关如何调试信息`Seed`方法以及如何处理冗余数据，如两个学生名为"Alexander Carson"，请参阅[进行种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)Rick Anderson 博客上。</span><span class="sxs-lookup"><span data-stu-id="e1396-299">For information about how to debug the `Seed` method and how to handle redundant data such as two students named "Alexander Carson", see [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) on Rick Anderson's blog.</span></span>
2. <span data-ttu-id="e1396-300">生成项目。</span><span class="sxs-lookup"><span data-stu-id="e1396-300">Build the project.</span></span>

### <a name="create-and-execute-the-first-migration"></a><span data-ttu-id="e1396-301">创建和执行第一次迁移</span><span class="sxs-lookup"><span data-stu-id="e1396-301">Create and Execute the First Migration</span></span>

1. <span data-ttu-id="e1396-302">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e1396-302">In the Package Manager Console window, enter the following commands:</span></span> 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    <span data-ttu-id="e1396-303">`add-migration`命令将添加到迁移文件夹*[日期时间戳]\_InitialCreate.cs*包含代码将创建数据库的文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-303">The `add-migration` command adds to the Migrations folder a *[DateStamp]\_InitialCreate.cs* file that contains code which creates the database.</span></span> <span data-ttu-id="e1396-304">第一个参数 (`InitialCreate)`用于文件命名，并可以是任何所需内容; 你通常要选择的单词或短语，总结了中迁移正在进行的内容。</span><span class="sxs-lookup"><span data-stu-id="e1396-304">The first parameter (`InitialCreate)` is used for the file name and can be whatever you want; you typically choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="e1396-305">例如，你可能会将更高版本迁移&quot;AddDepartmentTable&quot;。</span><span class="sxs-lookup"><span data-stu-id="e1396-305">For example, you might name a later migration &quot;AddDepartmentTable&quot;.</span></span>

    ![初始迁移的迁移文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    <span data-ttu-id="e1396-307">`Up`方法`InitialCreate`类创建对应的数据模型实体集，将数据库表和`Down`方法将其删除。</span><span class="sxs-lookup"><span data-stu-id="e1396-307">The `Up` method of the `InitialCreate` class creates the database tables that correspond to the data model entity sets, and the `Down` method deletes them.</span></span> <span data-ttu-id="e1396-308">迁移调用 `Up` 方法为迁移实现数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="e1396-308">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="e1396-309">输入用于回退更新的命令时，迁移调用 `Down` 方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-309">When you enter a command to roll back the update, Migrations calls the `Down` method.</span></span> <span data-ttu-id="e1396-310">下面的代码演示的内容`InitialCreate`文件：</span><span class="sxs-lookup"><span data-stu-id="e1396-310">The following code shows the contents of the `InitialCreate` file:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    <span data-ttu-id="e1396-311">`update-database`命令将运行`Up`方法，创建数据库然后运行`Seed`方法来填充数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-311">The `update-database` command runs the `Up` method to create the database and then it runs the `Seed` method to populate the database.</span></span>

<span data-ttu-id="e1396-312">现在已为你的数据模型创建的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-312">A SQL Server database has now been created for your data model.</span></span> <span data-ttu-id="e1396-313">数据库的名称是*ContosoUniversity*，和*.mdf*文件位于项目的*应用\_数据*文件夹，因为它是你在中指定你连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e1396-313">The name of the database is *ContosoUniversity*, and the *.mdf* file is in your project's *App\_Data* folder because that's what you specified in your connection string.</span></span>

<span data-ttu-id="e1396-314">你可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**(SSOX) 若要查看 Visual Studio 中的数据库。</span><span class="sxs-lookup"><span data-stu-id="e1396-314">You can use either **Server Explorer** or **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span> <span data-ttu-id="e1396-315">对于本教程将使用**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="e1396-315">For this tutorial you'll use **Server Explorer**.</span></span> <span data-ttu-id="e1396-316">在 Visual Studio Express 2012 for Web，**服务器资源管理器**称为**数据库资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="e1396-316">In Visual Studio Express 2012 for Web, **Server Explorer** is called **Database Explorer**.</span></span>

1. <span data-ttu-id="e1396-317">从**视图**菜单上，单击**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="e1396-317">From the **View** menu, click **Server Explorer**.</span></span>
2. <span data-ttu-id="e1396-318">单击**添加连接**图标。</span><span class="sxs-lookup"><span data-stu-id="e1396-318">Click the **Add Connection** icon.</span></span>

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. <span data-ttu-id="e1396-319">如果系统会提示你**选择数据源**对话框中，单击**Microsoft SQL Server**，然后单击**继续**。</span><span class="sxs-lookup"><span data-stu-id="e1396-319">If you are prompted with the **Choose Data Source** dialog, click **Microsoft SQL Server**, and then click **Continue**.</span></span>  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. <span data-ttu-id="e1396-320">在**添加连接**对话框框中，输入**(localdb) \v11.0**为**服务器名称**。</span><span class="sxs-lookup"><span data-stu-id="e1396-320">In the **Add Connection** dialog box, enter **(localdb)\v11.0** for the **Server Name**.</span></span> <span data-ttu-id="e1396-321">下**选择或输入数据库名称**，选择**ContosoUniversity。**</span><span class="sxs-lookup"><span data-stu-id="e1396-321">Under **Select or enter a database name**, select **ContosoUniversity.**</span></span>  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. <span data-ttu-id="e1396-322">单击“确定” </span><span class="sxs-lookup"><span data-stu-id="e1396-322">Click **OK.**</span></span>
6. <span data-ttu-id="e1396-323">展开**SchoolContext**然后展开**表**。</span><span class="sxs-lookup"><span data-stu-id="e1396-323">Expand **SchoolContext** and then expand **Tables**.</span></span>  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. <span data-ttu-id="e1396-324">右键单击**学生**表，然后单击**显示表数据**若要查看已创建的列和已插入到表的行。</span><span class="sxs-lookup"><span data-stu-id="e1396-324">Right-click the **Student** table and click **Show Table Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

    ![学生表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a><span data-ttu-id="e1396-326">正在创建学生控制器和视图</span><span class="sxs-lookup"><span data-stu-id="e1396-326">Creating a Student Controller and Views</span></span>

<span data-ttu-id="e1396-327">下一步是在你的应用程序可以与这些表中的一个创建 ASP.NET MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="e1396-327">The next step is to create an ASP.NET MVC controller and views in your application that can work with one of these tables.</span></span>

1. <span data-ttu-id="e1396-328">若要创建`Student`控制器上，右键单击**控制器**文件夹中的**解决方案资源管理器**，选择**添加**，然后单击**控制器**.</span><span class="sxs-lookup"><span data-stu-id="e1396-328">To create a `Student` controller, right-click the **Controllers** folder in **Solution Explorer**, select **Add**, and then click **Controller**.</span></span> <span data-ttu-id="e1396-329">在**添加控制器**对话框框中，选择下列选项，然后单击**添加**:</span><span class="sxs-lookup"><span data-stu-id="e1396-329">In the **Add Controller** dialog box, make the following selections and then click **Add**:</span></span> 

    - <span data-ttu-id="e1396-330">控制器名称： **StudentController**。</span><span class="sxs-lookup"><span data-stu-id="e1396-330">Controller name: **StudentController**.</span></span>
    - <span data-ttu-id="e1396-331">模板：**具有读/写操作和视图使用 Entity Framework 的 MVC 控制器**。</span><span class="sxs-lookup"><span data-stu-id="e1396-331">Template: **MVC controller with read/write actions and views, using Entity Framework**.</span></span>
    - <span data-ttu-id="e1396-332">模型类：**学生 (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="e1396-332">Model class: **Student (ContosoUniversity.Models)**.</span></span> <span data-ttu-id="e1396-333">（如果你没有看见此选项在下拉列表中的，生成项目并重试。）</span><span class="sxs-lookup"><span data-stu-id="e1396-333">(If you don't see this option in the drop-down list, build the project and try again.)</span></span>
    - <span data-ttu-id="e1396-334">数据上下文类： **SchoolContext (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="e1396-334">Data context class: **SchoolContext (ContosoUniversity.Models)**.</span></span>
    - <span data-ttu-id="e1396-335">视图： **Razor (CSHTML)**。</span><span class="sxs-lookup"><span data-stu-id="e1396-335">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="e1396-336">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="e1396-336">(The default.)</span></span>

    ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
- <span data-ttu-id="e1396-338">Visual Studio 将打开*Controllers\StudentController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="e1396-338">Visual Studio opens the *Controllers\StudentController.cs* file.</span></span> <span data-ttu-id="e1396-339">你看到类变量具有已创建可实例化数据库上下文对象：</span><span class="sxs-lookup"><span data-stu-id="e1396-339">You see a class variable has been created that instantiates a database context object:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

    <span data-ttu-id="e1396-340">`Index`操作方法获取从学生列表*学生*实体集通过阅读`Students`数据库上下文实例属性：</span><span class="sxs-lookup"><span data-stu-id="e1396-340">The `Index` action method gets a list of students from the *Students* entity set by reading the `Students` property of the database context instance:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

    <span data-ttu-id="e1396-341">*Student\Index.cshtml*视图在表中显示此列表：</span><span class="sxs-lookup"><span data-stu-id="e1396-341">The *Student\Index.cshtml* view displays this list in a table:</span></span>

    [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
- <span data-ttu-id="e1396-342">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="e1396-342">Press CTRL+F5 to run the project.</span></span>

    <span data-ttu-id="e1396-343">单击**学生**选项卡以查看测试数据，`Seed`插入的方法。</span><span class="sxs-lookup"><span data-stu-id="e1396-343">Click the **Students** tab to see the test data that the `Seed` method inserted.</span></span>

    ![学生索引页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a><span data-ttu-id="e1396-345">约定</span><span class="sxs-lookup"><span data-stu-id="e1396-345">Conventions</span></span>

<span data-ttu-id="e1396-346">你必须编写实体框架能够为你创建完整的数据库中的代码量很短的因为使用了*约定*，或使实体框架的假设。</span><span class="sxs-lookup"><span data-stu-id="e1396-346">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of *conventions*, or assumptions that the Entity Framework makes.</span></span> <span data-ttu-id="e1396-347">其中一些已经指出：</span><span class="sxs-lookup"><span data-stu-id="e1396-347">Some of them have already been noted:</span></span>

- <span data-ttu-id="e1396-348">实体类名称 pluralized 窗体用作表名称。</span><span class="sxs-lookup"><span data-stu-id="e1396-348">The pluralized forms of entity class names are used as table names.</span></span>
- <span data-ttu-id="e1396-349">使用实体属性名作为列名。</span><span class="sxs-lookup"><span data-stu-id="e1396-349">Entity property names are used for column names.</span></span>
- <span data-ttu-id="e1396-350">命名的实体属性`ID`或*classname* `ID`被识别为主键属性。</span><span class="sxs-lookup"><span data-stu-id="e1396-350">Entity properties that are named `ID` or *classname* `ID` are recognized as primary key properties.</span></span>

<span data-ttu-id="e1396-351">你已了解可以约定中重写 （例如，你指定不应表名变为复数形式），你将了解有关约定以及如何重写在[创建多个复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)教程稍后在此系列。</span><span class="sxs-lookup"><span data-stu-id="e1396-351">You've seen that conventions can be overridden (for example, you specified that table names shouldn't be pluralized), and you'll learn more about conventions and how to override them in the [Creating a More Complex Data Model](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) tutorial later in this series.</span></span> <span data-ttu-id="e1396-352">有关详细信息，请参阅[代码第一个约定](https://msdn.microsoft.com/data/jj679962)。</span><span class="sxs-lookup"><span data-stu-id="e1396-352">For more information, see [Code First Conventions](https://msdn.microsoft.com/data/jj679962).</span></span>

## <a name="summary"></a><span data-ttu-id="e1396-353">摘要</span><span class="sxs-lookup"><span data-stu-id="e1396-353">Summary</span></span>

<span data-ttu-id="e1396-354">你现在已创建的简单应用程序使用实体框架和 SQL Server Express 来存储和显示数据。</span><span class="sxs-lookup"><span data-stu-id="e1396-354">You've now created a simple application that uses the Entity Framework and SQL Server Express to store and display data.</span></span> <span data-ttu-id="e1396-355">在以下教程中，您将学习如何执行基本的 CRUD （创建、 读取、 更新、 删除） 操作。</span><span class="sxs-lookup"><span data-stu-id="e1396-355">In the following tutorial you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span> <span data-ttu-id="e1396-356">您可以离开此页底部的反馈。</span><span class="sxs-lookup"><span data-stu-id="e1396-356">You can leave feedback at the bottom of this page.</span></span> <span data-ttu-id="e1396-357">请让我们知道如何喜欢本教程的此部分的方式，我们可以如何改进它。</span><span class="sxs-lookup"><span data-stu-id="e1396-357">Please let us know how you liked this portion of the tutorial and how we could improve it.</span></span>

<span data-ttu-id="e1396-358">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="e1396-358">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="e1396-359">下一篇</span><span class="sxs-lookup"><span data-stu-id="e1396-359">Next</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
