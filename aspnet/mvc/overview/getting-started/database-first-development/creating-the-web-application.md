---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 创建 Web 应用程序和数据模型 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: a1c4e3365d320ee54d378de33a77666558a854d2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398240"
---
<a name="ef-database-first-with-aspnet-mvc-creating-the-web-application-and-data-models"></a><span data-ttu-id="0bb99-104">第一种使用 ASP.NET MVC 的 EF 数据库： 创建 Web 应用程序和数据模型</span><span class="sxs-lookup"><span data-stu-id="0bb99-104">EF Database First with ASP.NET MVC: Creating the Web Application and Data Models</span></span>
====================
<span data-ttu-id="0bb99-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0bb99-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0bb99-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0bb99-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="0bb99-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="0bb99-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="0bb99-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="0bb99-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="0bb99-109">本系列的此部分重点介绍创建 web 应用程序，并生成基于数据库表的数据模型。</span><span class="sxs-lookup"><span data-stu-id="0bb99-109">This part of the series focuses on creating the web application, and generating the data models based on your database tables.</span></span>


## <a name="create-a-new-aspnet-web-application"></a><span data-ttu-id="0bb99-110">创建新的 ASP.NET Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="0bb99-110">Create a new ASP.NET Web Application</span></span>

<span data-ttu-id="0bb99-111">在新的解决方案或与数据库项目相同的解决方案中，创建 Visual Studio 中的新项目，然后选择**ASP.NET Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="0bb99-111">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="0bb99-112">将项目命名**ContosoSite**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-112">Name the project **ContosoSite**.</span></span>

![创建项目](creating-the-web-application/_static/image1.png)

<span data-ttu-id="0bb99-114">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-114">Click **OK**.</span></span>

<span data-ttu-id="0bb99-115">在新建 ASP.NET 项目窗口中，选择**MVC**模板。</span><span class="sxs-lookup"><span data-stu-id="0bb99-115">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="0bb99-116">您可以清除**在云中托管**现在选项，因为你将部署到云的应用程序更高版本。</span><span class="sxs-lookup"><span data-stu-id="0bb99-116">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="0bb99-117">单击**确定**创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="0bb99-117">Click **OK** to create the application.</span></span>

![选择 mvc 模板](creating-the-web-application/_static/image2.png)

<span data-ttu-id="0bb99-119">使用默认文件和文件夹创建项目。</span><span class="sxs-lookup"><span data-stu-id="0bb99-119">The project is created with the default files and folders.</span></span>

<span data-ttu-id="0bb99-120">在本教程中，将使用 Entity Framework 6。</span><span class="sxs-lookup"><span data-stu-id="0bb99-120">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="0bb99-121">可以通过管理 NuGet 包窗口在项目中，请仔细检查 Entity Framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="0bb99-121">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="0bb99-122">如果有必要，请更新你的实体框架版本。</span><span class="sxs-lookup"><span data-stu-id="0bb99-122">If necessary, update your version of Entity Framework.</span></span>

![显示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="0bb99-124">生成模型</span><span class="sxs-lookup"><span data-stu-id="0bb99-124">Generate the models</span></span>

<span data-ttu-id="0bb99-125">现在将从数据库表创建实体框架模型。</span><span class="sxs-lookup"><span data-stu-id="0bb99-125">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="0bb99-126">这些模型是将用于处理的数据的类。</span><span class="sxs-lookup"><span data-stu-id="0bb99-126">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="0bb99-127">每个模型反映数据库中的表，并包含对应于表中的列的属性。</span><span class="sxs-lookup"><span data-stu-id="0bb99-127">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="0bb99-128">右键单击**模型**文件夹，然后选择**添加**并**新项**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-128">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

![添加新项](creating-the-web-application/_static/image4.png)

<span data-ttu-id="0bb99-130">在添加新项窗口中，选择**数据**的左窗格中并**ADO.NET 实体数据模型**从中间窗格中的选项。</span><span class="sxs-lookup"><span data-stu-id="0bb99-130">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="0bb99-131">将新的模型文件**ContosoModel**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-131">Name the new model file **ContosoModel**.</span></span>

![创建模型](creating-the-web-application/_static/image5.png)

<span data-ttu-id="0bb99-133">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-133">Click **Add**.</span></span>

<span data-ttu-id="0bb99-134">在实体数据模型向导中，选择**EF 设计器从数据库**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

![从数据库生成](creating-the-web-application/_static/image6.png)

<span data-ttu-id="0bb99-136">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-136">Click **Next**.</span></span>

<span data-ttu-id="0bb99-137">如果必须在开发环境中定义的数据库连接，可能会看到其中一个预先选择这些连接。</span><span class="sxs-lookup"><span data-stu-id="0bb99-137">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="0bb99-138">但是，你想要创建新的连接到在本教程的第一部分创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="0bb99-138">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="0bb99-139">单击**新的连接**按钮。</span><span class="sxs-lookup"><span data-stu-id="0bb99-139">Click the **New Connection** button.</span></span>

![连接到数据库](creating-the-web-application/_static/image7.png)

<span data-ttu-id="0bb99-141">在连接属性窗口中，提供了创建数据库时所在的本地服务器的名称 (在这种情况下 **(localdb) \ProjectsV12**)。</span><span class="sxs-lookup"><span data-stu-id="0bb99-141">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV12**).</span></span> <span data-ttu-id="0bb99-142">提供服务器名称后, 从可用数据库中选择 ContosoUniversityData。</span><span class="sxs-lookup"><span data-stu-id="0bb99-142">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![设置连接属性](creating-the-web-application/_static/image8.png)

<span data-ttu-id="0bb99-144">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-144">Click **OK**.</span></span>

<span data-ttu-id="0bb99-145">此时将显示正确的连接属性。</span><span class="sxs-lookup"><span data-stu-id="0bb99-145">The correct connection properties are now displayed.</span></span> <span data-ttu-id="0bb99-146">可以在 Web.Config 文件中使用连接的默认名称</span><span class="sxs-lookup"><span data-stu-id="0bb99-146">You can use the default name for connection in the Web.Config file</span></span>

![连接设置](creating-the-web-application/_static/image9.png)

<span data-ttu-id="0bb99-148">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-148">Click **Next**.</span></span>

<span data-ttu-id="0bb99-149">选择**表**来生成模型的所有三个表。</span><span class="sxs-lookup"><span data-stu-id="0bb99-149">Select **Tables** to generate models for all three tables.</span></span>

![选择表](creating-the-web-application/_static/image10.png)

<span data-ttu-id="0bb99-151">单击 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="0bb99-151">Click **Finish**.</span></span>

<span data-ttu-id="0bb99-152">如果你收到一条安全警告，选择**确定**继续运行模板。</span><span class="sxs-lookup"><span data-stu-id="0bb99-152">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="0bb99-153">从数据库表生成模型和关系图显示，其中显示的属性和表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="0bb99-153">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![模型的关系图](creating-the-web-application/_static/image11.png)

<span data-ttu-id="0bb99-155">模型文件夹现在包括许多与从数据库生成的模型相关的新文件。</span><span class="sxs-lookup"><span data-stu-id="0bb99-155">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

![显示新的模型文件](creating-the-web-application/_static/image12.png)

<span data-ttu-id="0bb99-157">**ContosoModel.Context.cs**文件包含的类的派生自**DbContext**类，并提供了用于每个对应于数据库表的 model 类属性。</span><span class="sxs-lookup"><span data-stu-id="0bb99-157">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="0bb99-158">**Course.cs**， **Enrollment.cs**，并**Student.cs**文件包含表示数据库表的模型类。</span><span class="sxs-lookup"><span data-stu-id="0bb99-158">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="0bb99-159">使用基架时，将使用上下文类和模型类。</span><span class="sxs-lookup"><span data-stu-id="0bb99-159">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="0bb99-160">本教程前，生成项目。</span><span class="sxs-lookup"><span data-stu-id="0bb99-160">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="0bb99-161">在下一步部分中，将生成基于数据模型代码，但如果未生成项目，将无法工作部分。</span><span class="sxs-lookup"><span data-stu-id="0bb99-161">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0bb99-162">[上一页](setting-up-database.md)
> [下一页](generating-views.md)</span><span class="sxs-lookup"><span data-stu-id="0bb99-162">[Previous](setting-up-database.md)
[Next](generating-views.md)</span></span>
