---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: "开始使用 Entity Framework 6 Code First 使用 MVC 5 |Microsoft 文档"
author: tdykstra
description: "提供了本系列教程的较新版本： 开始使用 ASP.NET Core 和使用 Visual Studio 2015 的实体框架核心。 Contoso Universi 中..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/22/2015
ms.topic: article
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 46f53279e2e6daa4266c06feb4ba544e14b68a03
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-entity-framework-6-code-first-using-mvc-5"></a><span data-ttu-id="db756-104">首先通过 MVC 5 使用 Entity Framework 6 Code First</span><span class="sxs-lookup"><span data-stu-id="db756-104">Getting Started with Entity Framework 6 Code First using MVC 5</span></span>
====================
<span data-ttu-id="db756-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="db756-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="db756-106">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="db756-106">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> > [!NOTE] 
> > 
> > <span data-ttu-id="db756-107">提供了本系列教程的较新版本：[开始使用 ASP.NET Core 和使用 Visual Studio 2015 的实体框架核心](https://docs.asp.net/en/latest/data/ef-mvc/intro.html)。</span><span class="sxs-lookup"><span data-stu-id="db756-107">A newer version of this tutorial series is available: [Get started with ASP.NET Core and Entity Framework Core using Visual Studio 2015](https://docs.asp.net/en/latest/data/ef-mvc/intro.html).</span></span>
> 
> 
> <span data-ttu-id="db756-108">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="db756-108">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 and Visual Studio 2013.</span></span> <span data-ttu-id="db756-109">本教程使用 Code First 的工作流。</span><span class="sxs-lookup"><span data-stu-id="db756-109">This tutorial uses the Code First workflow.</span></span> <span data-ttu-id="db756-110">有关如何选择 Code First、 数据库第一个和第一个模型之间的信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。</span><span class="sxs-lookup"><span data-stu-id="db756-110">For information about how to choose between Code First, Database First, and Model First, see [Entity Framework Development Workflows](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>
> 
> <span data-ttu-id="db756-111">示例应用程序是一个用于 fictional Contoso 大学网站。</span><span class="sxs-lookup"><span data-stu-id="db756-111">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="db756-112">它包括诸如学生许可、 过程创建和教师分配等功能。</span><span class="sxs-lookup"><span data-stu-id="db756-112">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="db756-113">本系列教程说明如何生成 Contoso 大学示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="db756-113">This tutorial series explains how to build the Contoso University sample application.</span></span> <span data-ttu-id="db756-114">你可以[下载已完成的应用程序](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)。</span><span class="sxs-lookup"><span data-stu-id="db756-114">You can [download the completed application](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8).</span></span>
> 
> <span data-ttu-id="db756-115">提供了由 Mike Brind 翻译的 Visual Basic 版本：[与在 Visual Basic 中的 EF 6 的 MVC 5](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) Mikesdotnetting 站点上。</span><span class="sxs-lookup"><span data-stu-id="db756-115">A Visual Basic version translated by Mike Brind is available: [MVC 5 with EF 6 in Visual Basic](http://www.mikesdotnetting.com/Article/241/MVC-5-with-EF-6-in-Visual-Basic-Creating-an-Entity-Framework-Data-Model) on the Mikesdotnetting site.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="db756-116">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="db756-116">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="db756-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="db756-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="db756-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="db756-118">.NET 4.5</span></span>
> - <span data-ttu-id="db756-119">实体框架 6 （EntityFramework 6.1.0 NuGet 包）</span><span class="sxs-lookup"><span data-stu-id="db756-119">Entity Framework 6 (EntityFramework 6.1.0 NuGet package)</span></span>
> - <span data-ttu-id="db756-120">[Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) （可选）</span><span class="sxs-lookup"><span data-stu-id="db756-120">[Windows Azure SDK 2.2](https://go.microsoft.com/fwlink/p/?linkid=323510) (optional)</span></span>
>   
> 
> <span data-ttu-id="db756-121">本教程还应使用[Visual Studio 2013 Express for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)或 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="db756-121">The tutorial should also work with [Visual Studio 2013 Express for Web](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express) or Visual Studio 2012.</span></span> <span data-ttu-id="db756-122">[VS 2012 版本的 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323511)是使用 Visual Studio 2012 的 Windows Azure 部署所必需的。</span><span class="sxs-lookup"><span data-stu-id="db756-122">The [VS 2012 version of the Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323511) is required for Windows Azure deployment with Visual Studio 2012.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="db756-123">教程版本</span><span class="sxs-lookup"><span data-stu-id="db756-123">Tutorial versions</span></span>
> 
> <span data-ttu-id="db756-124">对于本教程的早期版本，请参阅[EF 4.1 / MVC 3 电子书](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)和[Getting Started with EF 5 使用 MVC 4](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="db756-124">For previous versions of this tutorial, see [the EF 4.1 / MVC 3 e-book](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC) and [Getting Started with EF 5 using MVC 4](../../older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="db756-125">问题和意见</span><span class="sxs-lookup"><span data-stu-id="db756-125">Questions and comments</span></span>
> 
> <span data-ttu-id="db756-126">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="db756-126">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="db756-127">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)、[实体框架和 LINQ to Entities 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="db756-127">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx), the [Entity Framework and LINQ to Entities forum](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/), or [StackOverflow.com](http://stackoverflow.com/).</span></span>
> 
> <span data-ttu-id="db756-128">如果你遇到无法解决的问题，你通常可以通过比较已完成的项目，你可以下载你的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="db756-128">If you run into a problem you can't resolve, you can generally find the solution to the problem by comparing your code to the completed project that you can download.</span></span> <span data-ttu-id="db756-129">一些常见的错误和如何解决它们，请参阅[常见错误，以及解决方案或解决办法它们。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="db756-129">For some common errors and how to solve them, see [Common errors, and solutions or workarounds for them.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


## <a name="the-contoso-university-web-application"></a><span data-ttu-id="db756-130">Contoso 大学 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="db756-130">The Contoso University Web Application</span></span>

<span data-ttu-id="db756-131">你将在这些教程中构建的应用程序是简单大学网站。</span><span class="sxs-lookup"><span data-stu-id="db756-131">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="db756-132">用户可以查看和更新学生、 课程中和教师信息。</span><span class="sxs-lookup"><span data-stu-id="db756-132">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="db756-133">以下是一些你将创建的屏幕。</span><span class="sxs-lookup"><span data-stu-id="db756-133">Here are a few of the screens you'll create.</span></span>

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![编辑学生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="db756-136">此站点的用户界面样式而保留接近什么由运行内置的任何模板，以便在本教程主要关注如何使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="db756-136">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db756-137">系统必备</span><span class="sxs-lookup"><span data-stu-id="db756-137">Prerequisites</span></span>

<span data-ttu-id="db756-138">请参阅**软件版本**页顶部。</span><span class="sxs-lookup"><span data-stu-id="db756-138">See **Software Versions** at the top of the page.</span></span> <span data-ttu-id="db756-139">实体框架 6 不是先决条件，因为本教程的一部分安装 EF NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="db756-139">Entity Framework 6 is not a prerequisite because you install the EF NuGet package as part of the tutorial.</span></span>

## <a name="create-an-mvc-web-application"></a><span data-ttu-id="db756-140">创建 MVC Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="db756-140">Create an MVC Web Application</span></span>

<span data-ttu-id="db756-141">打开 Visual Studio 并创建一个名为"ContosoUniversity"的新 C# Web 项目。</span><span class="sxs-lookup"><span data-stu-id="db756-141">Open Visual Studio and create a new C# Web project named "ContosoUniversity".</span></span>

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="db756-143">在**新建 ASP.NET 项目**对话框框中，选择**MVC**模板。</span><span class="sxs-lookup"><span data-stu-id="db756-143">In the **New ASP.NET Project** dialog box select the **MVC** template.</span></span>

<span data-ttu-id="db756-144">如果**在云中托管**中的复选框**Microsoft Azure**选择部分后，清除它。</span><span class="sxs-lookup"><span data-stu-id="db756-144">If the **Host in the cloud** check box in the **Microsoft Azure** section is selected, clear it.</span></span>

<span data-ttu-id="db756-145">单击**更改身份验证**。</span><span class="sxs-lookup"><span data-stu-id="db756-145">Click **Change Authentication**.</span></span>

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="db756-147">在**更改身份验证**对话框中，选择**无身份验证**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="db756-147">In the **Change Authentication** dialog box, select **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="db756-148">对于本教程中你不会是要求用户登录，也限制基于登录的用户访问。</span><span class="sxs-lookup"><span data-stu-id="db756-148">For this tutorial you won't be requiring users to log on or restricting access based on who's logged on.</span></span>

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="db756-150">返回在新建 ASP.NET 项目对话框中，单击**确定**以创建该项目。</span><span class="sxs-lookup"><span data-stu-id="db756-150">Back in the New ASP.NET Project dialog box, click **OK** to create the project.</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="db756-151">设置站点样式</span><span class="sxs-lookup"><span data-stu-id="db756-151">Set Up the Site Style</span></span>

<span data-ttu-id="db756-152">几个简单的更改将设置站点菜单、 布局和主页。</span><span class="sxs-lookup"><span data-stu-id="db756-152">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="db756-153">打开*views/shared\\_Layout.cshtml*，并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="db756-153">Open *Views\Shared\\_Layout.cshtml*, and make the following changes:</span></span>

- <span data-ttu-id="db756-154">将每个匹配项的"My ASP.NET Application"和"应用程序名称"更改为"Contoso 大学"。</span><span class="sxs-lookup"><span data-stu-id="db756-154">Change each occurrence of "My ASP.NET Application" and "Application name" to "Contoso University".</span></span>
- <span data-ttu-id="db756-155">学生、 课程，教师和部门，添加菜单项和删除联系人条目。</span><span class="sxs-lookup"><span data-stu-id="db756-155">Add menu entries for Students, Courses, Instructors, and Departments, and delete the Contact entry.</span></span>

<span data-ttu-id="db756-156">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="db756-156">The changes are highlighted.</span></span>

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

<span data-ttu-id="db756-157">在*Views\Home\Index.cshtml*，将文件的内容替换为以下代码以将有关 ASP.NET 和 MVC 的文本替换为有关此应用程序的文本：</span><span class="sxs-lookup"><span data-stu-id="db756-157">In *Views\Home\Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

<span data-ttu-id="db756-158">按 CTRL + F5 以运行该站点。</span><span class="sxs-lookup"><span data-stu-id="db756-158">Press CTRL+F5 to run the site.</span></span> <span data-ttu-id="db756-159">你看到与主菜单的主页。</span><span class="sxs-lookup"><span data-stu-id="db756-159">You see the home page with the main menu.</span></span>

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

## <a name="install-entity-framework-6"></a><span data-ttu-id="db756-161">安装的 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="db756-161">Install Entity Framework 6</span></span>

<span data-ttu-id="db756-162">从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="db756-162">From the **Tools** menu click **NuGet Package Manager** and then click **Package Manager Console**.</span></span>

<span data-ttu-id="db756-163">在**程序包管理器控制台**窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="db756-163">In the **Package Manager Console** window enter the following command:</span></span>

`Install-Package EntityFramework`

![EF 安装](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="db756-165">图显示正在安装的 6.0.0 但 NuGet 将安装最新版本 （不包括预发行版本），实体框架的截至本教程的最新更新即 6.1.1。</span><span class="sxs-lookup"><span data-stu-id="db756-165">The image shows 6.0.0 being installed, but NuGet will install the latest version of Entity Framework (excluding pre-release versions), which as of the most recent update to the tutorial is 6.1.1.</span></span>

<span data-ttu-id="db756-166">此步骤是几个步骤，本教程将使你在手动执行此，但其无法完成操作自动通过 ASP.NET MVC 基架功能之一。</span><span class="sxs-lookup"><span data-stu-id="db756-166">This step is one of a few steps that this tutorial has you do manually, but which could have been done automatically by the ASP.NET MVC scaffolding feature.</span></span> <span data-ttu-id="db756-167">这样您可以看到使用实体框架所需的步骤，你在从手动执行它们。</span><span class="sxs-lookup"><span data-stu-id="db756-167">You're doing them manually so that you can see the steps required to use the Entity Framework.</span></span> <span data-ttu-id="db756-168">你将更高版本使用基架创建 MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="db756-168">You'll use scaffolding later to create the MVC controller and views.</span></span> <span data-ttu-id="db756-169">一种替代方法是让基架自动安装 EF NuGet 包，创建数据库上下文类，并创建连接字符串。</span><span class="sxs-lookup"><span data-stu-id="db756-169">An alternative is to let scaffolding automatically install the EF NuGet package, create the database context class, and create the connection string.</span></span> <span data-ttu-id="db756-170">你已准备好执行此操作通过这种方式，你所要做时，跳过这些步骤并在创建实体类后，你的 MVC 控制器搭建基架。</span><span class="sxs-lookup"><span data-stu-id="db756-170">When you're ready to do it that way, all you have to do is skip those steps and scaffold your MVC controller after you create your entity classes.</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="db756-171">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="db756-171">Create the Data Model</span></span>

<span data-ttu-id="db756-172">接下来你将创建 Contoso 大学应用程序的实体类。</span><span class="sxs-lookup"><span data-stu-id="db756-172">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="db756-173">你将从开始以下三个实体：</span><span class="sxs-lookup"><span data-stu-id="db756-173">You'll start with the following three entities:</span></span>

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="db756-175">之间的一对多关系`Student`和`Enrollment`实体，并且没有之间的一个对多关系`Course`和`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-175">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="db756-176">换而言之，一名学生可以在任意数量的课程中, 注册，并且某一课程可以具有任意数量的学生在其中注册。</span><span class="sxs-lookup"><span data-stu-id="db756-176">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="db756-177">下列部分中，你将创建每个这些实体的类。</span><span class="sxs-lookup"><span data-stu-id="db756-177">In the following sections you'll create a class for each one of these entities.</span></span>

> [!NOTE]
> <span data-ttu-id="db756-178">如果你尝试编译项目，然后完成创建所有这些实体类，将收到编译器错误。</span><span class="sxs-lookup"><span data-stu-id="db756-178">If you try to compile the project before you finish creating all of these entity classes, you'll get compiler errors.</span></span>


### <a name="the-student-entity"></a><span data-ttu-id="db756-179">学生实体</span><span class="sxs-lookup"><span data-stu-id="db756-179">The Student Entity</span></span>

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="db756-181">在*模型*文件夹中，创建一个名为的类文件*Student.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="db756-181">In the *Models* folder, create a class file named *Student.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="db756-182">`ID`属性将成为对应于此类数据库表的主键列。</span><span class="sxs-lookup"><span data-stu-id="db756-182">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="db756-183">默认情况下，实体框架将解释一个属性，名为`ID`或*classname* `ID`为主键。</span><span class="sxs-lookup"><span data-stu-id="db756-183">By default, the Entity Framework interprets a property that's named `ID` or *classname* `ID` as the primary key.</span></span>

<span data-ttu-id="db756-184">`Enrollments`属性是*导航属性*。</span><span class="sxs-lookup"><span data-stu-id="db756-184">The `Enrollments` property is a *navigation property*.</span></span> <span data-ttu-id="db756-185">导航属性将分别包含与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="db756-185">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="db756-186">在这种情况下，`Enrollments`属性`Student`实体将保留所有`Enrollment`与该订阅相关的实体`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-186">In this case, the `Enrollments` property of a `Student` entity will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="db756-187">换而言之，如果给定`Student`数据库中的行具有两个相关`Enrollment`行 (包含该学生的主键的行值在其`StudentID`外键列)，则该`Student`实体的`Enrollments`导航属性将包含这两个`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-187">In other words, if a given `Student` row in the database has two related `Enrollment` rows (rows that contain that student's primary key value in their `StudentID` foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="db756-188">导航属性通常定义为`virtual`，以便它们可以充分利用某些实体框架功能，如*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="db756-188">Navigation properties are typically defined as `virtual` so that they can take advantage of certain Entity Framework functionality such as *lazy loading*.</span></span> <span data-ttu-id="db756-189">(将解释延迟加载更高版本，在[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)更高版本中这一系列教程。)</span><span class="sxs-lookup"><span data-stu-id="db756-189">(Lazy loading will be explained later, in the [Reading Related Data](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series.)</span></span>

<span data-ttu-id="db756-190">如果导航属性可以具有多个实体 （如多对多或一对多关系），其类型必须是的列表中的条目可以是添加、 删除和更新，如`ICollection`。</span><span class="sxs-lookup"><span data-stu-id="db756-190">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection`.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="db756-191">注册实体</span><span class="sxs-lookup"><span data-stu-id="db756-191">The Enrollment Entity</span></span>

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="db756-193">在*模型*文件夹中，创建*Enrollment.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="db756-193">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="db756-194">`EnrollmentID`属性将是主键; 此实体使用*classname* `ID`模式而不是`ID`本身作为你在中看到`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-194">The `EnrollmentID` property will be the primary key; this entity uses the *classname* `ID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="db756-195">通常，你将选择一个模式，并使用它在你的数据模型。</span><span class="sxs-lookup"><span data-stu-id="db756-195">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="db756-196">在这里，变体说明了你可以使用任一模式。</span><span class="sxs-lookup"><span data-stu-id="db756-196">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="db756-197">在更高版本的教程中，你将看到如何使用`ID`而无需`classname`轻松地在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="db756-197">In a later tutorial, you'll see how using `ID` without `classname` makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="db756-198">`Grade`属性是[枚举](https://msdn.microsoft.com/data/hh859576.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db756-198">The `Grade` property is an [enum](https://msdn.microsoft.com/data/hh859576.aspx).</span></span> <span data-ttu-id="db756-199">后问号`Grade`类型声明指示`Grade`属性是[可以为 null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db756-199">The question mark after the `Grade` type declaration indicates that the `Grade` property is [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx).</span></span> <span data-ttu-id="db756-200">为 null 的等级是不同于零年级-null 意味着一个等级而言未知的或未尚未分配。</span><span class="sxs-lookup"><span data-stu-id="db756-200">A grade that's null is different from a zero grade — null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="db756-201">`StudentID`属性是一个外键，且相应的导航属性为`Student`。</span><span class="sxs-lookup"><span data-stu-id="db756-201">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="db756-202">`Enrollment`实体是与一个相关联`Student`实体，因此该属性只包含单个`Student`实体 (与不同`Student.Enrollments`导航属性前面所看到的后者可以容纳多个`Enrollment`实体)。</span><span class="sxs-lookup"><span data-stu-id="db756-202">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="db756-203">`CourseID`属性是一个外键，且相应的导航属性为`Course`。</span><span class="sxs-lookup"><span data-stu-id="db756-203">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="db756-204">`Enrollment`实体是与一个相关联`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-204">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="db756-205">实体框架： 将属性解释为外键属性，如果它名为*&lt;的导航属性名称&gt;&lt;主键属性名称&gt;* (例如， `StudentID`为`Student`以来的导航属性`Student`实体的主键是`ID`)。</span><span class="sxs-lookup"><span data-stu-id="db756-205">Entity Framework interprets a property as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="db756-206">外键属性还可以进行命名相同只需*&lt;主键属性名称&gt;* (例如，`CourseID`由于`Course`实体的主键是`CourseID`)。</span><span class="sxs-lookup"><span data-stu-id="db756-206">Foreign key properties can also be named the same simply *&lt;primary key property name&gt;* (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="db756-207">课程实体</span><span class="sxs-lookup"><span data-stu-id="db756-207">The Course Entity</span></span>

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

<span data-ttu-id="db756-209">在*模型*文件夹中，创建*Course.cs*，模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="db756-209">In the *Models* folder, create *Course.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="db756-210">`Enrollments`属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="db756-210">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="db756-211">A`Course`可以与任意数量的相关实体`Enrollment`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-211">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="db756-212">我们举例更多有关[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)本系列后面的教程中的属性。</span><span class="sxs-lookup"><span data-stu-id="db756-212">We'll say more about the [DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx) attribute in a later tutorial in this series.</span></span> <span data-ttu-id="db756-213">基本上，此属性允许您输入的过程，而不是让生成它的数据库的主键。</span><span class="sxs-lookup"><span data-stu-id="db756-213">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="db756-214">创建的数据库上下文</span><span class="sxs-lookup"><span data-stu-id="db756-214">Create the Database Context</span></span>

<span data-ttu-id="db756-215">协调为给定的数据模型的实体框架功能的主类是*数据库上下文*类。</span><span class="sxs-lookup"><span data-stu-id="db756-215">The main class that coordinates Entity Framework functionality for a given data model is the *database context* class.</span></span> <span data-ttu-id="db756-216">通过派生自创建此类[System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)类。</span><span class="sxs-lookup"><span data-stu-id="db756-216">You create this class by deriving from the [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) class.</span></span> <span data-ttu-id="db756-217">在代码中你指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="db756-217">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="db756-218">你还可以自定义某些实体框架行为。</span><span class="sxs-lookup"><span data-stu-id="db756-218">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="db756-219">在此项目中类命名为`SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="db756-219">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="db756-220">ContosoUniversity 项目中创建文件夹，右键单击中的项目**解决方案资源管理器**单击**添加**，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="db756-220">To create a folder in the ContosoUniversity project, right-click the project in **Solution Explorer** and click **Add**, and then click **New Folder**.</span></span> <span data-ttu-id="db756-221">将新文件夹命名*DAL* （适用于数据访问层）。</span><span class="sxs-lookup"><span data-stu-id="db756-221">Name the new folder *DAL* (for Data Access Layer).</span></span> <span data-ttu-id="db756-222">在该文件夹中创建名为的新类文件*SchoolContext.cs*，并将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="db756-222">In that folder create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specifying-entity-sets"></a><span data-ttu-id="db756-223">指定的实体集</span><span class="sxs-lookup"><span data-stu-id="db756-223">Specifying entity sets</span></span>

<span data-ttu-id="db756-224">此代码将创建[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)每个实体集的属性。</span><span class="sxs-lookup"><span data-stu-id="db756-224">This code creates a [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) property for each entity set.</span></span> <span data-ttu-id="db756-225">在实体框架术语中，*实体集*通常对应于一个数据库表，和*实体*对应于表中的行。</span><span class="sxs-lookup"><span data-stu-id="db756-225">In Entity Framework terminology, an *entity set* typically corresponds to a database table, and an *entity* corresponds to a row in the table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="db756-226">可以省略`DbSet<Enrollment>`和`DbSet<Course>`语句和其效果相同。</span><span class="sxs-lookup"><span data-stu-id="db756-226">You could have omitted the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="db756-227">实体框架会将其包含隐式因为`Student`实体引用`Enrollment`实体和`Enrollment`实体引用`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="db756-227">The Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>


### <a name="specifying-the-connection-string"></a><span data-ttu-id="db756-228">指定的连接字符串</span><span class="sxs-lookup"><span data-stu-id="db756-228">Specifying the connection string</span></span>

<span data-ttu-id="db756-229">连接字符串的 （稍后将添加到 Web.config 文件） 的名称被传递给构造函数。</span><span class="sxs-lookup"><span data-stu-id="db756-229">The name of the connection string (which you'll add to the Web.config file later) is passed in to the constructor.</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

<span data-ttu-id="db756-230">您还无法传入的连接字符串本身而不是一个存储在 Web.config 文件的名称。</span><span class="sxs-lookup"><span data-stu-id="db756-230">You could also pass in the connection string itself instead of the name of one that is stored in the Web.config file.</span></span> <span data-ttu-id="db756-231">有关将数据库指定要使用的选项的详细信息，请参阅[实体框架的连接和模型](https://msdn.microsoft.com/data/jj592674)。</span><span class="sxs-lookup"><span data-stu-id="db756-231">For more information about options for specifying the database to use, see [Entity Framework - Connections and Models](https://msdn.microsoft.com/data/jj592674).</span></span>

<span data-ttu-id="db756-232">如果不显式指定连接字符串或其中一个的名称，实体框架将假定该连接字符串名称是否与类名称相同。</span><span class="sxs-lookup"><span data-stu-id="db756-232">If you don't specify a connection string or the name of one explicitly, Entity Framework assumes that the connection string name is the same as the class name.</span></span> <span data-ttu-id="db756-233">在此示例中的默认连接字符串名称将为`SchoolContext`，与你在指定的显式相同。</span><span class="sxs-lookup"><span data-stu-id="db756-233">The default connection string name in this example would then be `SchoolContext`, the same as what you're specifying explicitly.</span></span>

### <a name="specifying-singular-table-names"></a><span data-ttu-id="db756-234">指定采用单数形式的表名称</span><span class="sxs-lookup"><span data-stu-id="db756-234">Specifying singular table names</span></span>

<span data-ttu-id="db756-235">`modelBuilder.Conventions.Remove`中的语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)的方法阻止从正在变为复数形式的表名称。</span><span class="sxs-lookup"><span data-stu-id="db756-235">The `modelBuilder.Conventions.Remove` statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method prevents table names from being pluralized.</span></span> <span data-ttu-id="db756-236">如果你未执行此操作，数据库中生成的表将被命名为`Students`， `Courses`，和`Enrollments`。</span><span class="sxs-lookup"><span data-stu-id="db756-236">If you didn't do this, the generated tables in the database would be named `Students`, `Courses`, and `Enrollments`.</span></span> <span data-ttu-id="db756-237">相反，则表名将为`Student`， `Course`，和`Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="db756-237">Instead, the table names will be `Student`, `Course`, and `Enrollment`.</span></span> <span data-ttu-id="db756-238">开发者对表名称是否应为复数意见不一。</span><span class="sxs-lookup"><span data-stu-id="db756-238">Developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="db756-239">本教程使用单数形式，但重要的一点是，可以选择你的首选，通过包括或忽略这行代码的任何一个窗体。</span><span class="sxs-lookup"><span data-stu-id="db756-239">This tutorial uses the singular form, but the important point is that you can select whichever form you prefer by including or omitting this line of code.</span></span>

## <a name="set-up-ef-to-initialize-the-database-with-test-data"></a><span data-ttu-id="db756-240">设置 EF 初始化测试数据的数据库</span><span class="sxs-lookup"><span data-stu-id="db756-240">Set up EF to initialize the database with test data</span></span>

<span data-ttu-id="db756-241">实体框架可以自动创建 （或除去并重新创建） 为你的应用程序运行时的数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-241">The Entity Framework can automatically create (or drop and re-create) a database for you when the application runs.</span></span> <span data-ttu-id="db756-242">你可以指定，这应进行每次运行应用程序或仅时模型不同步的与现有数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-242">You can specify that this should be done every time your application runs or only when the model is out of sync with the existing database.</span></span> <span data-ttu-id="db756-243">你还可以编写`Seed`实体框架自动填充测试数据以创建数据库后调用的方法。</span><span class="sxs-lookup"><span data-stu-id="db756-243">You can also write a `Seed` method that the Entity Framework automatically calls after creating the database in order to populate it with test data.</span></span>

<span data-ttu-id="db756-244">默认行为是创建数据库，仅当它不存在 （和引发异常，如果该模型已更改，并且数据库已存在）。</span><span class="sxs-lookup"><span data-stu-id="db756-244">The default behavior is to create a database only if it doesn't exist (and throw an exception if the model has changed and the database already exists).</span></span> <span data-ttu-id="db756-245">在本部分中，你将指定应删除并重新创建该模型发生更改时数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-245">In this section you'll specify that the database should be dropped and re-created whenever the model changes.</span></span> <span data-ttu-id="db756-246">删除数据库导致所有数据的丢失。</span><span class="sxs-lookup"><span data-stu-id="db756-246">Dropping the database causes the loss of all your data.</span></span> <span data-ttu-id="db756-247">这通常是确定在开发期间，因为`Seed`方法将在数据库重新创建，并将重新创建测试数据时运行。</span><span class="sxs-lookup"><span data-stu-id="db756-247">This is generally OK during development, because the `Seed` method will run when the database is re-created and will re-create your test data.</span></span> <span data-ttu-id="db756-248">但在生产环境中你通常不希望每次需要更改数据库架构时，会丢失所有数据。</span><span class="sxs-lookup"><span data-stu-id="db756-248">But in production you generally don't want to lose all your data every time you need to change the database schema.</span></span> <span data-ttu-id="db756-249">更高版本，你将了解如何通过使用 Code First 迁移以更改而不是删除并重新创建数据库的数据库架构处理模型更改。</span><span class="sxs-lookup"><span data-stu-id="db756-249">Later you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

<span data-ttu-id="db756-250">在 DAL 文件夹中，创建名为的新类文件*SchoolInitializer.cs*并使用该模板代码替换</span><span class="sxs-lookup"><span data-stu-id="db756-250">In the DAL folder, create a new class file named *SchoolInitializer.cs* and replace the template code with the</span></span>  
<span data-ttu-id="db756-251">下面的代码，这会导致数据库创建时需要并将测试数据加载到新的数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-251">following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="db756-252">`Seed`方法采用数据库上下文对象作为输入参数，并在方法中的代码使用</span><span class="sxs-lookup"><span data-stu-id="db756-252">The `Seed` method takes the database context object as an input parameter, and the code in the method uses</span></span>  
<span data-ttu-id="db756-253">要向数据库添加新实体该对象。</span><span class="sxs-lookup"><span data-stu-id="db756-253">that object to add new entities to the database.</span></span> <span data-ttu-id="db756-254">对于每个实体类型，该代码创建的集合新</span><span class="sxs-lookup"><span data-stu-id="db756-254">For each entity type, the code creates a collection of new</span></span>  
 <span data-ttu-id="db756-255">实体，将它们添加到相应`DbSet`属性，然后将保存到数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="db756-255">entities, adds them to the appropriate `DbSet` property, and then saves the changes to the database.</span></span> <span data-ttu-id="db756-256">它不</span><span class="sxs-lookup"><span data-stu-id="db756-256">It isn't</span></span>  
<span data-ttu-id="db756-257">不必调用`SaveChanges`方法之后每个组的实体，如上文所述，但这样做，可帮助</span><span class="sxs-lookup"><span data-stu-id="db756-257">necessary to call the `SaveChanges` method after each group of entities, as is done here, but doing that helps</span></span>  
<span data-ttu-id="db756-258">如果向数据库写入代码时出现异常，你可以找到问题的根源。</span><span class="sxs-lookup"><span data-stu-id="db756-258">you locate the source of a problem if an exception occurs while the code is writing to the database.</span></span>

<span data-ttu-id="db756-259">若要指示实体框架可以使用初始值设定项类，将元素添加到`entityFramework`应用程序中的元素*Web.config*文件 （文件的根项目文件夹中），如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="db756-259">To tell Entity Framework to use your initializer class, add an element to the `entityFramework` element in the application *Web.config* file (the one in the root project folder), as shown in the following example:</span></span>

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

<span data-ttu-id="db756-260">`context type`指定完全限定的上下文类名称和在中，它是程序集和`databaseinitializer type`指定初始值设定项类和在程序集的完全限定的名称。</span><span class="sxs-lookup"><span data-stu-id="db756-260">The `context type` specifies the fully qualified context class name and the assembly it's in, and the `databaseinitializer type` specifies the fully qualified name of the initializer class and the assembly it's in.</span></span> <span data-ttu-id="db756-261">(如果你不想使用初始值设定项的 EF，您可以对设置属性`context`元素： `disableDatabaseInitialization="true"`。)有关详细信息，请参阅[实体框架的配置文件设置](https://msdn.microsoft.com/data/jj556606)。</span><span class="sxs-lookup"><span data-stu-id="db756-261">(When you don't want EF to use the initializer, you can set an attribute on the `context` element: `disableDatabaseInitialization="true"`.) For more information, see [Entity Framework - Config File Settings](https://msdn.microsoft.com/data/jj556606).</span></span>

<span data-ttu-id="db756-262">作为设置初始值设定项的替代方法*Web.config*文件是代码以执行此操作通过添加`Database.SetInitializer`语句`Application_Start`中的方法*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="db756-262">As an alternative to setting the initializer in the *Web.config* file is to do it in code by adding a `Database.SetInitializer` statement to the `Application_Start` method in the *Global.asax.cs* file.</span></span> <span data-ttu-id="db756-263">有关详细信息，请参阅[了解数据库初始值设定项中 Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。</span><span class="sxs-lookup"><span data-stu-id="db756-263">For more information, see [Understanding Database Initializers in Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).</span></span>

<span data-ttu-id="db756-264">应用程序现在已设置最多，以便在某给定运行过程的第一次访问数据库时</span><span class="sxs-lookup"><span data-stu-id="db756-264">The application is now set up so that when you access the database for the first time in a given run of the</span></span>  
<span data-ttu-id="db756-265">应用程序，实体框架比较对模型数据库 (你`SchoolContext`和实体类)。</span><span class="sxs-lookup"><span data-stu-id="db756-265">application, the Entity Framework compares the database to the model (your `SchoolContext` and entity classes).</span></span> <span data-ttu-id="db756-266">如果差异，应用程序将删除并重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-266">If there's a difference, the application drops and re-creates the database.</span></span>

> [!NOTE]
> <span data-ttu-id="db756-267">在部署到生产 web 服务器应用程序时，你必须删除或禁用将删除并重新创建数据库的代码。</span><span class="sxs-lookup"><span data-stu-id="db756-267">When you deploy an application to a production web server, you must remove or disable code that drops and re-creates the database.</span></span> <span data-ttu-id="db756-268">在本系列后面的教程中，将执行该操作。</span><span class="sxs-lookup"><span data-stu-id="db756-268">You'll do that in a later tutorial in this series.</span></span>


## <a name="set-up-ef-to-use-a-sql-server-express-localdb-database"></a><span data-ttu-id="db756-269">设置为使用 SQL Server Express LocalDB 数据库的 EF</span><span class="sxs-lookup"><span data-stu-id="db756-269">Set up EF to use a SQL Server Express LocalDB database</span></span>

<span data-ttu-id="db756-270">[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)是 SQL Server Express 数据库引擎的轻量版本。</span><span class="sxs-lookup"><span data-stu-id="db756-270">[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) is a lightweight version of the SQL Server Express Database Engine.</span></span> <span data-ttu-id="db756-271">它很容易安装和配置、 启动点播情况下，并在用户模式下运行。</span><span class="sxs-lookup"><span data-stu-id="db756-271">It's easy to install and configure, starts on demand, and runs in user mode.</span></span> <span data-ttu-id="db756-272">LocalDB 运行中的 SQL Server Express，可用于处理数据库作为一种特殊的执行模式*.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="db756-272">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="db756-273">你可以将 LocalDB 数据库文件放入*应用\_数据*的 web 项目中，如果你想要能够复制数据库与项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="db756-273">You can put LocalDB database files in the *App\_Data* folder of a web project if you want to be able to copy the database with the project.</span></span> <span data-ttu-id="db756-274">在 SQL Server Express 用户实例功能还可以使您能够使用*.mdf*文件，但用户实例功能已弃用; 因此，使用建议 LocalDB *.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="db756-274">The user instance feature in SQL Server Express also enables you to work with *.mdf* files, but the user instance feature is deprecated; therefore, LocalDB is recommended for working with *.mdf* files.</span></span> <span data-ttu-id="db756-275">在 Visual Studio 2012 和更高版本中，默认情况下，使用 Visual Studio 安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="db756-275">In Visual Studio 2012 and later versions, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="db756-276">通常 SQL Server Express 不用于生产 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="db756-276">Typically SQL Server Express is not used for production web applications.</span></span> <span data-ttu-id="db756-277">LocalDB 具体而言不是建议生产使用与 web 应用程序由于它不是使用 IIS。</span><span class="sxs-lookup"><span data-stu-id="db756-277">LocalDB in particular is not recommended for production use with a web application because it is not designed to work with IIS.</span></span>

<span data-ttu-id="db756-278">在本教程中，您将可以使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="db756-278">In this tutorial you'll work with LocalDB.</span></span> <span data-ttu-id="db756-279">打开应用程序*Web.config*文件并添加`connectionStrings`元素前面`appSettings`元素，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="db756-279">Open the application *Web.config* file and add a `connectionStrings` element preceding the `appSettings` element, as shown in the following example.</span></span> <span data-ttu-id="db756-280">(请确保你更新*Web.config*根项目文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="db756-280">(Make sure you update the *Web.config* file in the root project folder.</span></span> <span data-ttu-id="db756-281">此外，还有*Web.config*文件位于*视图*无需更新的子文件夹。)</span><span class="sxs-lookup"><span data-stu-id="db756-281">There's also a *Web.config* file is in the *Views* subfolder that you don't need to update.)</span></span>

<span data-ttu-id="db756-282">如果你使用的 Visual Studio 2015，替换连接字符串中的"v11.0""MSSQLLocalDB"，因为默认 SQL Server 实例名称已更改。</span><span class="sxs-lookup"><span data-stu-id="db756-282">If you are using Visual Studio 2015, replace "v11.0" in the connection string with "MSSQLLocalDB", as the default SQL Server instance name has changed.</span></span>

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

<span data-ttu-id="db756-283">你已添加的连接字符串指定实体框架将使用名为的 LocalDB 数据库*ContosoUniversity1.mdf*。</span><span class="sxs-lookup"><span data-stu-id="db756-283">The connection string you've added specifies that Entity Framework will use a LocalDB database named *ContosoUniversity1.mdf*.</span></span> <span data-ttu-id="db756-284">（数据库尚不存在;EF 将创建它。）如果你想要在中创建的数据库你*应用\_数据*文件夹中，你可以添加`AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf`到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="db756-284">(The database doesn't exist yet; EF will create it.) If you wanted the database to be created in your *App\_Data* folder, you could add `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` to the connection string.</span></span> <span data-ttu-id="db756-285">有关连接字符串的详细信息，请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db756-285">For more information about connection strings, see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="db756-286">你实际上不必中有一个连接字符串*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="db756-286">You don't actually have to have a connection string in the *Web.config* file.</span></span> <span data-ttu-id="db756-287">如果你不提供的连接字符串，实体框架将使用的默认的基于上下文类。</span><span class="sxs-lookup"><span data-stu-id="db756-287">If you don't supply a connection string, Entity Framework will use a default one based on your context class.</span></span> <span data-ttu-id="db756-288">有关详细信息，请参阅[到新数据库 Code First](https://msdn.microsoft.com/data/jj193542)。</span><span class="sxs-lookup"><span data-stu-id="db756-288">For more information, see [Code First to a New Database](https://msdn.microsoft.com/data/jj193542).</span></span>

## <a name="creating-a-student-controller-and-views"></a><span data-ttu-id="db756-289">正在创建学生控制器和视图</span><span class="sxs-lookup"><span data-stu-id="db756-289">Creating a Student Controller and Views</span></span>

<span data-ttu-id="db756-290">现在，你将要创建网页上显示数据，并请求数据的过程将自动触发</span><span class="sxs-lookup"><span data-stu-id="db756-290">Now you'll create a web page to display data, and the process of requesting the data will automatically trigger</span></span>  
<span data-ttu-id="db756-291">创建数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-291">the creation of the database.</span></span> <span data-ttu-id="db756-292">你将首先创建新的控制器。</span><span class="sxs-lookup"><span data-stu-id="db756-292">You'll begin by creating a new controller.</span></span> <span data-ttu-id="db756-293">但执行此操作之前，生成项目后，要提供给 MVC 控制器基架的模型和上下文类。</span><span class="sxs-lookup"><span data-stu-id="db756-293">But before you do that, build the project to make the model and context classes available to MVC controller scaffolding.</span></span>

1. <span data-ttu-id="db756-294">右键单击**控制器**文件夹中的**解决方案资源管理器**，选择**添加**，然后单击**新建基架项**。</span><span class="sxs-lookup"><span data-stu-id="db756-294">Right-click the **Controllers** folder in **Solution Explorer**, select **Add**, and then click **New Scaffolded Item**.</span></span>
- <span data-ttu-id="db756-295">在**添加基架**对话框中，选择**数据与视图，MVC 5 控制器使用 Entity Framework**。</span><span class="sxs-lookup"><span data-stu-id="db756-295">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework**.</span></span>

    ![添加基架](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)
- <span data-ttu-id="db756-297">在添加控制器对话框中，进行以下选择，然后单击**添加**:</span><span class="sxs-lookup"><span data-stu-id="db756-297">In the Add Controller dialog box, make the following selections and then click **Add**:</span></span>

    - <span data-ttu-id="db756-298">模型类：**学生 (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="db756-298">Model class: **Student (ContosoUniversity.Models)**.</span></span> <span data-ttu-id="db756-299">（如果你没有看见此选项在下拉列表中的，生成项目并重试。）</span><span class="sxs-lookup"><span data-stu-id="db756-299">(If you don't see this option in the drop-down list, build the project and try again.)</span></span>
    - <span data-ttu-id="db756-300">数据上下文类： **SchoolContext (ContosoUniversity.DAL)**。</span><span class="sxs-lookup"><span data-stu-id="db756-300">Data context class: **SchoolContext (ContosoUniversity.DAL)**.</span></span>
    - <span data-ttu-id="db756-301">控制器名称： **StudentController** (不 StudentsController)。</span><span class="sxs-lookup"><span data-stu-id="db756-301">Controller name: **StudentController** (not StudentsController).</span></span>
    - <span data-ttu-id="db756-302">保留其他字段的默认值。</span><span class="sxs-lookup"><span data-stu-id="db756-302">Leave the default values for the other fields.</span></span>

    ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    <span data-ttu-id="db756-304">当你单击**添加**，基架创建 StudentController.cs 文件和一组工作与控制器的视图 （.cshtml 文件）。</span><span class="sxs-lookup"><span data-stu-id="db756-304">When you click **Add**, the scaffolder creates a StudentController.cs file and a set of views (.cshtml files) that work with the controller.</span></span> <span data-ttu-id="db756-305">将来当你创建使用实体框架的项目，你还可以利用的基架一些附加功能： 只需创建第一个模型类，无需创建一个连接字符串，然后在**添加控制器**框中指定新的上下文类。</span><span class="sxs-lookup"><span data-stu-id="db756-305">In the future when you create projects that use Entity Framework you can also take advantage of some additional functionality of the scaffolder: just create your first model class, don't create a connection string, and then in the **Add Controller** box specify new context class.</span></span> <span data-ttu-id="db756-306">基架将创建你`DbContext`类和你的连接字符串以及控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="db756-306">The scaffolder will create your `DbContext` class and your connection string as well as the controller and views.</span></span>
- <span data-ttu-id="db756-307">Visual Studio 将打开*Controllers\StudentController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="db756-307">Visual Studio opens the *Controllers\StudentController.cs* file.</span></span> <span data-ttu-id="db756-308">你看到类变量具有已创建可实例化数据库上下文对象：</span><span class="sxs-lookup"><span data-stu-id="db756-308">You see a class variable has been created that instantiates a database context object:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    <span data-ttu-id="db756-309">`Index`操作方法获取从学生列表*学生*实体集通过阅读`Students`数据库上下文实例属性：</span><span class="sxs-lookup"><span data-stu-id="db756-309">The `Index` action method gets a list of students from the *Students* entity set by reading the `Students` property of the database context instance:</span></span>

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    <span data-ttu-id="db756-310">*Student\Index.cshtml*视图在表中显示此列表：</span><span class="sxs-lookup"><span data-stu-id="db756-310">The *Student\Index.cshtml* view displays this list in a table:</span></span>

    [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
- <span data-ttu-id="db756-311">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="db756-311">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="db756-312">（如果收到"无法创建卷影副本"错误时，关闭浏览器并重试。）</span><span class="sxs-lookup"><span data-stu-id="db756-312">(If you get a "Cannot create Shadow Copy" error, close the browser and try again.)</span></span>

    <span data-ttu-id="db756-313">单击**学生**选项卡以查看测试数据，`Seed`插入的方法。</span><span class="sxs-lookup"><span data-stu-id="db756-313">Click the **Students** tab to see the test data that the `Seed` method inserted.</span></span> <span data-ttu-id="db756-314">具体取决于如何窄浏览器窗口，你将看到在顶部的地址栏中的学生选项卡链接或你将需要单击右上角才能看到该链接。</span><span class="sxs-lookup"><span data-stu-id="db756-314">Depending on how narrow your browser window is, you'll see the Student tab link in the top address bar or you'll have to click the upper right corner to see the link.</span></span>

    ![菜单按钮](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    ![学生索引页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="view-the-database"></a><span data-ttu-id="db756-317">查看数据库</span><span class="sxs-lookup"><span data-stu-id="db756-317">View the Database</span></span>

<span data-ttu-id="db756-318">当你运行学生页和应用程序尝试访问数据库时，EF 会看到没有任何数据库，所以创建了一个，然后它运行 seed 方法，可使用数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-318">When you ran the Students page and the application tried to access the database, EF saw that there was no database and so it created one, then it ran the seed method to populate the database with data.</span></span>

<span data-ttu-id="db756-319">你可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**(SSOX) 若要查看 Visual Studio 中的数据库。</span><span class="sxs-lookup"><span data-stu-id="db756-319">You can use either **Server Explorer** or **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span> <span data-ttu-id="db756-320">对于本教程将使用**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="db756-320">For this tutorial you'll use **Server Explorer**.</span></span> <span data-ttu-id="db756-321">(在 Visual Studio Express 版本早于 2013，**服务器资源管理器**称为**数据库资源管理器**。)</span><span class="sxs-lookup"><span data-stu-id="db756-321">(In Visual Studio Express editions earlier than 2013, **Server Explorer** is called **Database Explorer**.)</span></span>

1. <span data-ttu-id="db756-322">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="db756-322">Close the browser.</span></span>
2. <span data-ttu-id="db756-323">在**服务器资源管理器**，展开**数据连接**，展开**学校上下文 (ContosoUniversity)**，然后展开**表**若要查看新的数据库中的表。</span><span class="sxs-lookup"><span data-stu-id="db756-323">In **Server Explorer**, expand **Data Connections**, expand **School Context (ContosoUniversity)**, and then expand **Tables** to see the tables in your new database.</span></span>

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
3. <span data-ttu-id="db756-324">右键单击**学生**表，然后单击**显示表数据**若要查看已创建的列和已插入到表的行。</span><span class="sxs-lookup"><span data-stu-id="db756-324">Right-click the **Student** table and click **Show Table Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

    ![学生表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
4. <span data-ttu-id="db756-326">关闭**服务器资源管理器**连接。</span><span class="sxs-lookup"><span data-stu-id="db756-326">Close the **Server Explorer** connection.</span></span>

<span data-ttu-id="db756-327">*ContosoUniversity1.mdf*和*.ldf*数据库文件位于`C:\Users\<yourusername>`文件夹。</span><span class="sxs-lookup"><span data-stu-id="db756-327">The *ContosoUniversity1.mdf* and *.ldf* database files are in the `C:\Users\<yourusername>` folder.</span></span>

<span data-ttu-id="db756-328">因为您正在使用`DropCreateDatabaseIfModelChanges`初始值设定项，你可以现在进行的更改`Student`类，再次运行应用程序，并且数据库将自动为重新创建，以匹配所做的更改。</span><span class="sxs-lookup"><span data-stu-id="db756-328">Because you're using the `DropCreateDatabaseIfModelChanges` initializer, you could now make a change to the `Student` class, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="db756-329">例如，如果你添加`EmailAddress`属性`Student`类，请再次运行学生页面，然后查看表再次，你将看到管理新`EmailAddress`列。</span><span class="sxs-lookup"><span data-stu-id="db756-329">For example, if you add an `EmailAddress` property to the `Student` class, run the Students page again, and then look at the table again, you will see a new `EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="db756-330">约定</span><span class="sxs-lookup"><span data-stu-id="db756-330">Conventions</span></span>

<span data-ttu-id="db756-331">你必须编写实体框架能够为你创建完整的数据库中的代码量很短的因为使用了*约定*，或使实体框架的假设。</span><span class="sxs-lookup"><span data-stu-id="db756-331">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of *conventions*, or assumptions that the Entity Framework makes.</span></span> <span data-ttu-id="db756-332">其中一些已记录或已使用不带你不知道的：</span><span class="sxs-lookup"><span data-stu-id="db756-332">Some of them have already been noted or were used without your being aware of them:</span></span>

- <span data-ttu-id="db756-333">实体类名称 pluralized 窗体用作表名称。</span><span class="sxs-lookup"><span data-stu-id="db756-333">The pluralized forms of entity class names are used as table names.</span></span>
- <span data-ttu-id="db756-334">实体属性名称用于列名称。</span><span class="sxs-lookup"><span data-stu-id="db756-334">Entity property names are used for column names.</span></span>
- <span data-ttu-id="db756-335">命名的实体属性`ID`或*classname* `ID`被识别为主键属性。</span><span class="sxs-lookup"><span data-stu-id="db756-335">Entity properties that are named `ID` or *classname* `ID` are recognized as primary key properties.</span></span>
- <span data-ttu-id="db756-336">如果它名为属性将被解释为外键属性*&lt;的导航属性名称&gt;&lt;主键属性名称&gt;* (例如，`StudentID`为`Student`以来的导航属性`Student`实体的主键是`ID`)。</span><span class="sxs-lookup"><span data-stu-id="db756-336">A property is interpreted as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="db756-337">外键属性还可以进行命名相同只需&lt;主键属性名称&gt;(例如，`EnrollmentID`由于`Enrollment`实体的主键是`EnrollmentID`)。</span><span class="sxs-lookup"><span data-stu-id="db756-337">Foreign key properties can also be named the same simply &lt;primary key property name&gt; (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="db756-338">你已了解可以约定中重写。</span><span class="sxs-lookup"><span data-stu-id="db756-338">You've seen that conventions can be overridden.</span></span> <span data-ttu-id="db756-339">例如，指定表名称不应变为复数形式，并稍后你将看到如何显式标记为外键属性的属性。</span><span class="sxs-lookup"><span data-stu-id="db756-339">For example, you specified that table names shouldn't be pluralized, and you'll see later how to explicitly mark a property as a foreign key property.</span></span> <span data-ttu-id="db756-340">你将了解有关约定和如何重写在[创建多个复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)更高版本中这一系列教程。</span><span class="sxs-lookup"><span data-stu-id="db756-340">You'll learn more about conventions and how to override them in the [Creating a More Complex Data Model](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) tutorial later in this series.</span></span> <span data-ttu-id="db756-341">有关约定的详细信息，请参阅[代码第一个约定](https://msdn.microsoft.com/data/jj679962)。</span><span class="sxs-lookup"><span data-stu-id="db756-341">For more information about conventions, see [Code First Conventions](https://msdn.microsoft.com/data/jj679962).</span></span>

## <a name="summary"></a><span data-ttu-id="db756-342">摘要</span><span class="sxs-lookup"><span data-stu-id="db756-342">Summary</span></span>

<span data-ttu-id="db756-343">你现在已创建的简单应用程序使用的实体框架和 SQL Server Express LocalDB 来存储和显示数据。</span><span class="sxs-lookup"><span data-stu-id="db756-343">You've now created a simple application that uses the Entity Framework and SQL Server Express LocalDB to store and display data.</span></span> <span data-ttu-id="db756-344">在以下教程中，您将学习如何执行基本的 CRUD （创建、 读取、 更新、 删除） 操作。</span><span class="sxs-lookup"><span data-stu-id="db756-344">In the following tutorial you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>

<span data-ttu-id="db756-345">请在如何喜欢本教程的方式，我们可以提高上，留下反馈。</span><span class="sxs-lookup"><span data-stu-id="db756-345">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="db756-346">你还可以请求新主题[教我编写代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="db756-346">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="db756-347">在找不到其他实体框架资源的链接[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="db756-347">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="db756-348">下一篇</span><span class="sxs-lookup"><span data-stu-id="db756-348">Next</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
