---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 检索和显示与数据模型绑定和 web 窗体 |Microsoft 文档
author: tfitzmac
description: 本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互详细直接-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 26873efa5dbfdbdab39a52cfb9cfd5a65c8231a3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889090"
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="12534-104">检索和显示使用模型的绑定和 web 窗体的数据</span><span class="sxs-lookup"><span data-stu-id="12534-104">Retrieving and displaying data with model binding and web forms</span></span>
====================
<span data-ttu-id="12534-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="12534-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="12534-106">本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="12534-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="12534-107">模型绑定使数据交互更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource）。</span><span class="sxs-lookup"><span data-stu-id="12534-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="12534-108">这一系列开头介绍性材料，更高版本的教程中移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="12534-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="12534-109">与任何数据访问技术配合使用模型绑定模式。</span><span class="sxs-lookup"><span data-stu-id="12534-109">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="12534-110">在本教程中，你将使用实体框架中，但你无法使用最熟悉的数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="12534-110">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="12534-111">通过数据绑定服务器控件，如 GridView、 ListView、 说明或 FormView 控件，你可以指定要用于选择、 更新、 删除和创建数据的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="12534-111">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="12534-112">在本教程中，你将为 SelectMethod 指定值。</span><span class="sxs-lookup"><span data-stu-id="12534-112">In this tutorial, you will specify a value for the SelectMethod.</span></span>
> 
> <span data-ttu-id="12534-113">在该方法中，用于检索数据提供的逻辑。</span><span class="sxs-lookup"><span data-stu-id="12534-113">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="12534-114">在下一步的教程中，你将为 UpdateMethod、 delete 方法和 InsertMethod 设置值。</span><span class="sxs-lookup"><span data-stu-id="12534-114">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
> 
> <span data-ttu-id="12534-115">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)在 C# 或 VB.完整项目</span><span class="sxs-lookup"><span data-stu-id="12534-115">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="12534-116">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="12534-116">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="12534-117">它使用 Visual Studio 2012 模板，这是本教程中所示的 Visual Studio 2013 模板过程稍有不同。</span><span class="sxs-lookup"><span data-stu-id="12534-117">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="12534-118">本教程中 Visual Studio 中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="12534-118">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="12534-119">你还可以让应用程序访问 Internet 上通过将其部署到托管提供商。</span><span class="sxs-lookup"><span data-stu-id="12534-119">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="12534-120">Microsoft 提供的最多 10 个网站中免费的 web 承载</span><span class="sxs-lookup"><span data-stu-id="12534-120">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
>  <span data-ttu-id="12534-121">[免费 Azure 试用帐户](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="12534-121">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="12534-122">有关如何将 Visual Studio web 项目部署到 Azure App Service Web Apps 的信息，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)系列。</span><span class="sxs-lookup"><span data-stu-id="12534-122">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="12534-123">该教程还演示如何使用 Entity Framework Code First 迁移将您的 SQL Server 数据库部署到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="12534-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="12534-124">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="12534-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="12534-125">Microsoft Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="12534-125">Microsoft Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web</span></span>
>   
> 
> <span data-ttu-id="12534-126">本教程还适用于 Visual Studio 2012，但将有一些差异的用户界面和项目模板。</span><span class="sxs-lookup"><span data-stu-id="12534-126">This tutorial also works with Visual Studio 2012 but there will be some differences in the user interface and project template.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="12534-127">你将生成</span><span class="sxs-lookup"><span data-stu-id="12534-127">What you'll build</span></span>

<span data-ttu-id="12534-128">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="12534-128">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="12534-129">生成与学生课程中注册反映一所大学的数据对象</span><span class="sxs-lookup"><span data-stu-id="12534-129">Build data objects that reflect a university with students enrolled in courses</span></span>
2. <span data-ttu-id="12534-130">生成从对象的数据库表</span><span class="sxs-lookup"><span data-stu-id="12534-130">Build database tables from the objects</span></span>
3. <span data-ttu-id="12534-131">使用测试数据填充数据库</span><span class="sxs-lookup"><span data-stu-id="12534-131">Populate the database with test data</span></span>
4. <span data-ttu-id="12534-132">在 web 窗体中显示数据</span><span class="sxs-lookup"><span data-stu-id="12534-132">Display data in a web form</span></span>

## <a name="set-up-project"></a><span data-ttu-id="12534-133">设置项目</span><span class="sxs-lookup"><span data-stu-id="12534-133">Set up project</span></span>

<span data-ttu-id="12534-134">在 Visual Studio 2013 中，创建一个新**ASP.NET Web 应用程序**调用**ContosoUniversityModelBinding**。</span><span class="sxs-lookup"><span data-stu-id="12534-134">In Visual Studio 2013, create a new **ASP.NET Web Application** called **ContosoUniversityModelBinding**.</span></span>

![创建项目](retrieving-data/_static/image2.png)

<span data-ttu-id="12534-136">选择 Web 窗体模板，并将其他默认选项。</span><span class="sxs-lookup"><span data-stu-id="12534-136">Select the Web Forms template, and leave the other default options.</span></span> <span data-ttu-id="12534-137">单击确定以安装项目。</span><span class="sxs-lookup"><span data-stu-id="12534-137">Click OK to setup the project.</span></span>

![选择 web 窗体](retrieving-data/_static/image3.png)

<span data-ttu-id="12534-139">首先，将进行一些小更改自定义网站的外观。</span><span class="sxs-lookup"><span data-stu-id="12534-139">First, you will make a couple of small changes to customize the appearance of the site.</span></span> <span data-ttu-id="12534-140">打开**Site.Master**文件，并将更改要包括 Contoso 大学，而不是我的 ASP.NET 应用程序的标题。</span><span class="sxs-lookup"><span data-stu-id="12534-140">Open the **Site.Master** file, and change the title to include Contoso University instead of My ASP.NET Application.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

<span data-ttu-id="12534-141">然后，将更改中的标头文本**应用程序名称**到**Contoso 大学**。</span><span class="sxs-lookup"><span data-stu-id="12534-141">Then, change the header text from **Application name** to **Contoso University**.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

<span data-ttu-id="12534-142">此外在 Site.Master，更改以反映此站点相关的页面的标头中显示的导航链接。</span><span class="sxs-lookup"><span data-stu-id="12534-142">Also in Site.Master, change the navigation links that appear in the header to reflect the pages that are relevant to this site.</span></span> <span data-ttu-id="12534-143">将不需要以下两者之一**有关**页或**联系人**页，以便可以删除这些链接。</span><span class="sxs-lookup"><span data-stu-id="12534-143">You will not need either the **About** page or the **Contact** page so those links can be removed.</span></span> <span data-ttu-id="12534-144">相反，您将需要调用的页链接**学生**。</span><span class="sxs-lookup"><span data-stu-id="12534-144">Instead, you will need a link to a page called **Students**.</span></span> <span data-ttu-id="12534-145">此页尚未创建。</span><span class="sxs-lookup"><span data-stu-id="12534-145">This page has not been created yet.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample3.aspx)]

<span data-ttu-id="12534-146">保存并关闭 Site.Master。</span><span class="sxs-lookup"><span data-stu-id="12534-146">Save and close Site.Master.</span></span>

<span data-ttu-id="12534-147">现在，你将创建显示学生数据的 web 窗体。</span><span class="sxs-lookup"><span data-stu-id="12534-147">Now, you'll create the web form for displaying student data.</span></span> <span data-ttu-id="12534-148">右键单击你的项目，并**添加****新项**。</span><span class="sxs-lookup"><span data-stu-id="12534-148">Right-click your project, and **Add** a **New Item**.</span></span> <span data-ttu-id="12534-149">选择**包含母版页的 Web 窗体**模板，并将其命名**Students.aspx**。</span><span class="sxs-lookup"><span data-stu-id="12534-149">Select the **Web Form with Master Page** template, and name it **Students.aspx**.</span></span>

![创建页](retrieving-data/_static/image5.png)

<span data-ttu-id="12534-151">选择**Site.Master**作为新的 web 窗体母版页。</span><span class="sxs-lookup"><span data-stu-id="12534-151">Select **Site.Master** as the master page for the new web form.</span></span>

## <a name="create-the-data-models-and-database"></a><span data-ttu-id="12534-152">创建数据模型和数据库</span><span class="sxs-lookup"><span data-stu-id="12534-152">Create the data models and database</span></span>

<span data-ttu-id="12534-153">Code First 迁移将用于创建对象和相应的数据库表。</span><span class="sxs-lookup"><span data-stu-id="12534-153">You will use Code First Migrations to create objects and the corresponding database tables.</span></span> <span data-ttu-id="12534-154">这些表将存储有关学生和他们的课程的信息。</span><span class="sxs-lookup"><span data-stu-id="12534-154">These tables will store information about the students and their courses.</span></span>

<span data-ttu-id="12534-155">在 Models 文件夹中，添加一个名为的新类**UniversityModels.cs**。</span><span class="sxs-lookup"><span data-stu-id="12534-155">In the Models folder, add a new class named **UniversityModels.cs**.</span></span>

![创建模型类](retrieving-data/_static/image7.png)

<span data-ttu-id="12534-157">在此文件中，定义 SchoolContext、 学生、 注册、 和课程类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="12534-157">In this file, define the SchoolContext, Student, Enrollment, and Course classes as follows:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample4.cs)]

<span data-ttu-id="12534-158">SchoolContext 类派生自 DbContext，它管理的数据库连接和数据中的更改。</span><span class="sxs-lookup"><span data-stu-id="12534-158">The SchoolContext class derives from DbContext, which manages the database connection and changes in the data.</span></span>

<span data-ttu-id="12534-159">在学生类中，请注意已应用于属性**FirstName**， **LastName**，和**年**属性。</span><span class="sxs-lookup"><span data-stu-id="12534-159">In the Student class, notice the attributes that have been applied to the **FirstName**, **LastName**, and **Year** properties.</span></span> <span data-ttu-id="12534-160">这些属性将用于在本教程中的数据验证。</span><span class="sxs-lookup"><span data-stu-id="12534-160">These attributes will be used for data validation in this tutorial.</span></span> <span data-ttu-id="12534-161">若要简化此演示项目的代码，只有这些属性都是使用数据验证特性标记。</span><span class="sxs-lookup"><span data-stu-id="12534-161">To simplify the code for this demonstration project, only these properties were marked with data-validation attributes.</span></span> <span data-ttu-id="12534-162">在实际项目中，则将应用对需要验证的数据，例如注册和课程类中的属性的所有属性的验证特性。</span><span class="sxs-lookup"><span data-stu-id="12534-162">In a real project, you would apply validation attributes to all properties that need validated data, such as properties in the Enrollment and Course classes.</span></span>

<span data-ttu-id="12534-163">保存 UniversityModels.cs。</span><span class="sxs-lookup"><span data-stu-id="12534-163">Save UniversityModels.cs.</span></span>

<span data-ttu-id="12534-164">对于 Code First 迁移工具将用于将基于这些类数据库设置。</span><span class="sxs-lookup"><span data-stu-id="12534-164">You will use the tools for Code First Migrations to set up a database based on these classes.</span></span>

<span data-ttu-id="12534-165">在**程序包管理器控制台**，运行命令：</span><span class="sxs-lookup"><span data-stu-id="12534-165">In **Package Manager Console**, run the command:</span></span>  
`enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

<span data-ttu-id="12534-166">如果命令成功完成，则你将收到一条消息已启用迁移，</span><span class="sxs-lookup"><span data-stu-id="12534-166">If the command completes successfully you will receive a message stating migrations have been enabled,</span></span>

![启用迁移](retrieving-data/_static/image8.png)

<span data-ttu-id="12534-168">请注意，新文件命名为**Configuration.cs**已创建。</span><span class="sxs-lookup"><span data-stu-id="12534-168">Notice that a new file named **Configuration.cs** has been created.</span></span> <span data-ttu-id="12534-169">在 Visual Studio 中，将在创建后将自动打开此文件。</span><span class="sxs-lookup"><span data-stu-id="12534-169">In Visual Studio, this file is automatically opened after it is created.</span></span> <span data-ttu-id="12534-170">配置类包含**种子**方法使你以预填充使用测试数据的数据库表。</span><span class="sxs-lookup"><span data-stu-id="12534-170">The Configuration class contains a **Seed** method which enables you to pre-populate the database tables with test data.</span></span>

<span data-ttu-id="12534-171">将以下代码添加到 Seed 方法。</span><span class="sxs-lookup"><span data-stu-id="12534-171">Add the following code to the Seed method.</span></span> <span data-ttu-id="12534-172">你将需要添加**使用**语句**ContosoUniversityModelBinding.Models**命名空间。</span><span class="sxs-lookup"><span data-stu-id="12534-172">You'll need to add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample5.cs)]

<span data-ttu-id="12534-173">保存 Configuration.cs。</span><span class="sxs-lookup"><span data-stu-id="12534-173">Save Configuration.cs.</span></span>

<span data-ttu-id="12534-174">在程序包管理器控制台中，运行命令`add-migration initial`。</span><span class="sxs-lookup"><span data-stu-id="12534-174">In the Package Manager Console, run the command `add-migration initial`.</span></span>

<span data-ttu-id="12534-175">然后，运行命令`update-database`。</span><span class="sxs-lookup"><span data-stu-id="12534-175">Then, run the command `update-database`.</span></span>

<span data-ttu-id="12534-176">如果运行此命令时，你会收到异常，，则可能 StudentID 和 CourseID 的值具有不同的 Seed 方法中的值。</span><span class="sxs-lookup"><span data-stu-id="12534-176">If you receive an exception when running this command, it is possible that the values for StudentID and CourseID have varied from the values in the Seed method.</span></span> <span data-ttu-id="12534-177">在数据库中打开这些表，并查找 StudentID 和 CourseID 现有值。</span><span class="sxs-lookup"><span data-stu-id="12534-177">Open those tables in the database and find existing values for StudentID and CourseID.</span></span> <span data-ttu-id="12534-178">在种子设定注册表的代码中添加这些值。</span><span class="sxs-lookup"><span data-stu-id="12534-178">Add those values in the code for seeding the Enrollments table.</span></span>

<span data-ttu-id="12534-179">已添加的数据库文件，但它当前隐藏项目中。</span><span class="sxs-lookup"><span data-stu-id="12534-179">The database file has been added, but it is currently hidden in the project.</span></span> <span data-ttu-id="12534-180">单击**显示所有文件**若要显示的文件。</span><span class="sxs-lookup"><span data-stu-id="12534-180">Click **Show All Files** to display the file.</span></span>

![显示所有文件](retrieving-data/_static/image10.png)

<span data-ttu-id="12534-182">请注意.mdf 文件现在将出现在应用程序中\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="12534-182">Notice the .mdf file now appears in the App\_Data folder.</span></span>

![数据库文件](retrieving-data/_static/image12.png)

<span data-ttu-id="12534-184">双击.mdf 文件，打开服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="12534-184">Double-click the .mdf file and open the Server Explorer.</span></span> <span data-ttu-id="12534-185">现在，表存在，且使用数据填充。</span><span class="sxs-lookup"><span data-stu-id="12534-185">The tables now exist and are populated with data.</span></span>

![数据库表](retrieving-data/_static/image14.png)

## <a name="display-data-from-students-and-related-tables"></a><span data-ttu-id="12534-187">显示学生和相关的表中的数据</span><span class="sxs-lookup"><span data-stu-id="12534-187">Display data from Students and related tables</span></span>

<span data-ttu-id="12534-188">数据库中的数据，你就现在可以检索该数据并将其显示在网页中。</span><span class="sxs-lookup"><span data-stu-id="12534-188">With data in the database, you are now ready to retrieve that data and display it in a web page.</span></span> <span data-ttu-id="12534-189">你将使用**GridView**控件以显示行和列中的数据。</span><span class="sxs-lookup"><span data-stu-id="12534-189">You will use a **GridView** control to display the data in columns and rows.</span></span>

<span data-ttu-id="12534-190">打开 Students.aspx，并找到**主内容**占位符。</span><span class="sxs-lookup"><span data-stu-id="12534-190">Open Students.aspx, and locate the **MainContent** placeholder.</span></span> <span data-ttu-id="12534-191">在该占位符，添加**GridView**包括下面的代码的控件。</span><span class="sxs-lookup"><span data-stu-id="12534-191">Within that placeholder, add a **GridView** control that includes the following code.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample6.aspx)]

<span data-ttu-id="12534-192">有几个在此标记代码中为你需要注意的重要概念。</span><span class="sxs-lookup"><span data-stu-id="12534-192">There are a couple of important concepts in this markup code for you to notice.</span></span> <span data-ttu-id="12534-193">首先，请注意，为设置一个值**SelectMethod** GridView 元素中的属性。</span><span class="sxs-lookup"><span data-stu-id="12534-193">First, notice that a value is set for the **SelectMethod** property in the GridView element.</span></span> <span data-ttu-id="12534-194">此值指定用于检索数据的 GridView 方法的名称。</span><span class="sxs-lookup"><span data-stu-id="12534-194">This value specifies the name of the method that is used for retrieving data for the GridView.</span></span> <span data-ttu-id="12534-195">你将在下一步中创建此方法。</span><span class="sxs-lookup"><span data-stu-id="12534-195">You will create this method in the next step.</span></span> <span data-ttu-id="12534-196">其次，请注意， **ItemType**属性设置为前面创建的学生类。</span><span class="sxs-lookup"><span data-stu-id="12534-196">Second, notice that the **ItemType** property is set to the Student class that you created earlier.</span></span> <span data-ttu-id="12534-197">通过设置此值，你可以引用该类中的标记代码的属性。</span><span class="sxs-lookup"><span data-stu-id="12534-197">By setting this value, you can refer to properties of that class in the markup code.</span></span> <span data-ttu-id="12534-198">例如，学生类包含名为注册的集合。</span><span class="sxs-lookup"><span data-stu-id="12534-198">For example, the Student class contains a collection named Enrollments.</span></span> <span data-ttu-id="12534-199">你可以使用**Item.Enrollments**来检索该集合，然后使用 LINQ 语法来检索每个学生的已注册的信用额度的总和。</span><span class="sxs-lookup"><span data-stu-id="12534-199">You can use **Item.Enrollments** to retrieve that collection and then use LINQ syntax to retrieve the sum of enrolled credits for each student.</span></span>

<span data-ttu-id="12534-200">在代码隐藏文件中，你需要添加为指定的方法**SelectMethod**值。</span><span class="sxs-lookup"><span data-stu-id="12534-200">In the code-behind file, you need to add the method that is specified for the **SelectMethod** value.</span></span> <span data-ttu-id="12534-201">打开**Students.aspx.cs**，并添加**使用**语句**ContosoUniversityModelBinding.Models**和**System.Data.Entity**命名空间。</span><span class="sxs-lookup"><span data-stu-id="12534-201">Open **Students.aspx.cs**, and add **using** statements for the **ContosoUniversityModelBinding.Models** and **System.Data.Entity** namespaces.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample7.cs)]

<span data-ttu-id="12534-202">然后，添加以下方法。</span><span class="sxs-lookup"><span data-stu-id="12534-202">Then, add the following method.</span></span> <span data-ttu-id="12534-203">请注意，此方法的名称与为 SelectMethod 提供的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="12534-203">Notice that the name of this method matches the name you provided for SelectMethod.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample8.cs)]

<span data-ttu-id="12534-204">**包括**子句提高了此查询的性能，但不是必需的工作的查询。</span><span class="sxs-lookup"><span data-stu-id="12534-204">The **Include** clause improves the performance of this query but is not essential for the query to work.</span></span> <span data-ttu-id="12534-205">不带 Include 子句中，将使用延迟加载，涉及发送到数据库的单独查询每个时间相关检索数据检索的数据。</span><span class="sxs-lookup"><span data-stu-id="12534-205">Without the Include clause, the data would be retrieved using lazy loading, which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="12534-206">通过提供 Include 子句，使用预先加载，这意味着通过数据库的单个查询检索的所有相关的数据检索的数据。</span><span class="sxs-lookup"><span data-stu-id="12534-206">By providing the Include clause, the data is retrieved using eager loading, which means all of the related data is retrieved through a single query of the database.</span></span> <span data-ttu-id="12534-207">在其中的大多数相关的数据是不能的情况下使用过的、 预先加载可能会效率较低，因为检索更多的数据。</span><span class="sxs-lookup"><span data-stu-id="12534-207">In cases where most of the related data is not be used, eager loading can be less efficient because more data is retrieved.</span></span> <span data-ttu-id="12534-208">但是，在这种情况下，预先加载提供最佳性能因为相关的数据显示为每个记录。</span><span class="sxs-lookup"><span data-stu-id="12534-208">However, in this case, eager loading provides the best performance because the related data is displayed for each record.</span></span>

<span data-ttu-id="12534-209">有关加载时的性能注意事项的详细信息与相关的数据，请参阅节**Lazy、 Eager 和显式加载的相关数据**中[读取与 ASP 在实体框架的相关数据.NET MVC 应用程序](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)主题。</span><span class="sxs-lookup"><span data-stu-id="12534-209">For more information about performance consideration when loading related data, see the section titled **Lazy, Eager, and Explicit Loading of Related Data** in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) topic.</span></span>

<span data-ttu-id="12534-210">默认情况下，数据按标记为键属性的值。</span><span class="sxs-lookup"><span data-stu-id="12534-210">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="12534-211">你可以添加一个 OrderBy 子句，以指定不同的值进行排序。</span><span class="sxs-lookup"><span data-stu-id="12534-211">You can add an OrderBy clause to specify a different value for sorting.</span></span> <span data-ttu-id="12534-212">在此示例中，默认 StudentID 属性用于排序。</span><span class="sxs-lookup"><span data-stu-id="12534-212">In this example, the default StudentID property is used for sorting.</span></span> <span data-ttu-id="12534-213">在[排序、 分页和筛选数据](sorting-paging-and-filtering-data.md)主题中，将使用户能够选择列进行排序。</span><span class="sxs-lookup"><span data-stu-id="12534-213">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) topic, you will enable the user to select a column for sorting.</span></span>

<span data-ttu-id="12534-214">运行 web 应用程序，并导航到学生页。</span><span class="sxs-lookup"><span data-stu-id="12534-214">Run your web application, and navigate to the Students page.</span></span> <span data-ttu-id="12534-215">学生页显示以下学生信息。</span><span class="sxs-lookup"><span data-stu-id="12534-215">The Students page displays the following student information.</span></span>

![显示数据](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="12534-217">自动生成的模型绑定方法</span><span class="sxs-lookup"><span data-stu-id="12534-217">Automatic generation of model binding methods</span></span>

<span data-ttu-id="12534-218">当学习本教程系列中，你可以只需复制的代码从本教程到你的项目。</span><span class="sxs-lookup"><span data-stu-id="12534-218">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="12534-219">但是，此方法的一个缺点是功能的，你可能不会变得感知的 Visual Studio 自动生成模型绑定方法的代码提供。</span><span class="sxs-lookup"><span data-stu-id="12534-219">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="12534-220">处理的您自己的项目时，自动代码生成可为你节省时间并帮助你了解如何实现一个操作。</span><span class="sxs-lookup"><span data-stu-id="12534-220">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="12534-221">本部分介绍的自动代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="12534-221">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="12534-222">本部分仅供参考，并不包含任何需要在你的项目中实现的代码。</span><span class="sxs-lookup"><span data-stu-id="12534-222">This section is only informational and does not contain any code you need to implement in your project.</span></span>

<span data-ttu-id="12534-223">设置的值时**SelectMethod**， **UpdateMethod**， **InsertMethod**，或**delete 方法**在标记代码中，属性你可以选择**创建新方法**选项。</span><span class="sxs-lookup"><span data-stu-id="12534-223">When setting a value for the **SelectMethod**, **UpdateMethod**, **InsertMethod**, or **DeleteMethod** properties in the markup code, you can select the **Create New Method** option.</span></span>

![创建新的方法](retrieving-data/_static/image18.png)

<span data-ttu-id="12534-225">Visual Studio 不仅具有正确签名的代码隐藏文件中创建一个方法，而且还会生成实现代码，以帮助您执行该操作。</span><span class="sxs-lookup"><span data-stu-id="12534-225">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to assist you with performing the operation.</span></span> <span data-ttu-id="12534-226">如果第一次设置**ItemType**之前使用自动代码生成功能，生成的代码的属性将使用该类型的操作。</span><span class="sxs-lookup"><span data-stu-id="12534-226">If you first set the **ItemType** property before using the automatic code generation feature, the generated code will use that type for the operations.</span></span> <span data-ttu-id="12534-227">例如，设置 UpdateMethod 属性时，会自动会生成以下代码：</span><span class="sxs-lookup"><span data-stu-id="12534-227">For example, when setting the UpdateMethod property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="12534-228">同样，上面的代码不必添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="12534-228">Again, the above code does not need to be added to your project.</span></span> <span data-ttu-id="12534-229">在下一步的教程中，你将实现用于更新、 删除和添加新数据的方法。</span><span class="sxs-lookup"><span data-stu-id="12534-229">In the next tutorial, you will implement methods for updating, deleting and adding new data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="12534-230">结束语</span><span class="sxs-lookup"><span data-stu-id="12534-230">Conclusion</span></span>

<span data-ttu-id="12534-231">在本教程中，你将创建数据模型类，并从这些类生成数据库。</span><span class="sxs-lookup"><span data-stu-id="12534-231">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="12534-232">使用测试数据填充数据库表。</span><span class="sxs-lookup"><span data-stu-id="12534-232">You filled the database tables with test data.</span></span> <span data-ttu-id="12534-233">模型绑定用于从数据库中检索数据并在一个 GridView 中显示数据。</span><span class="sxs-lookup"><span data-stu-id="12534-233">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="12534-234">在下一个[教程](updating-deleting-and-creating-data.md)在此系列中，将启用更新、 删除和创建的数据。</span><span class="sxs-lookup"><span data-stu-id="12534-234">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you will enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="12534-235">下一篇</span><span class="sxs-lookup"><span data-stu-id="12534-235">Next</span></span>](updating-deleting-and-creating-data.md)
