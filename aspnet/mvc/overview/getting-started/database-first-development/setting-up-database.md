---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 开始使用 Entity Framework 6 Database First 通过 MVC 5 |Microsoft Docs
author: Rick-Anderson
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: riande
ms.date: 10/01/2014
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: 7fcb2b82dfa27ae192e1890c0c771d68658760a4
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021139"
---
<a name="getting-started-with-entity-framework-6-database-first-using-mvc-5"></a><span data-ttu-id="824c8-104">使用 Entity Framework 6 Database First 通过 MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="824c8-104">Getting Started with Entity Framework 6 Database First using MVC 5</span></span>
====================
<span data-ttu-id="824c8-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="824c8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="824c8-106">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="824c8-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="824c8-107">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="824c8-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="824c8-108">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="824c8-108">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="824c8-109">在本系列的最后部分，会将站点和数据库部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="824c8-109">In the last part of the series, you will deploy the site and database to Azure.</span></span>
> 
> <span data-ttu-id="824c8-110">本系列的此部分主要介绍在创建数据库和使用数据填充。</span><span class="sxs-lookup"><span data-stu-id="824c8-110">This part of the series focuses on creating a database and populating it with data.</span></span>
> 
> <span data-ttu-id="824c8-111">这一系列已用的发布内容写入 Tom Dykstra 和 Rick Anderson。</span><span class="sxs-lookup"><span data-stu-id="824c8-111">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="824c8-112">它改进了基于注释部分中的用户的反馈。</span><span class="sxs-lookup"><span data-stu-id="824c8-112">It was improved based on feedback from users in the comments section.</span></span>


## <a name="introduction"></a><span data-ttu-id="824c8-113">介绍</span><span class="sxs-lookup"><span data-stu-id="824c8-113">Introduction</span></span>

<span data-ttu-id="824c8-114">本主题说明如何开始使用现有数据库并快速创建 web 应用程序，使用户能够与数据交互。</span><span class="sxs-lookup"><span data-stu-id="824c8-114">This topic shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="824c8-115">它使用 Entity Framework 6 和 MVC 5 构建 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="824c8-115">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="824c8-116">ASP.NET 基架功能可以自动生成用于显示、 更新、 创建和删除数据的代码。</span><span class="sxs-lookup"><span data-stu-id="824c8-116">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="824c8-117">使用 Visual Studio 中的发布工具，你可以轻松部署站点和数据库到 Azure。</span><span class="sxs-lookup"><span data-stu-id="824c8-117">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="824c8-118">本主题介绍这种情况，如果有数据库并且想要为 web 应用程序根据该数据库的字段生成代码。</span><span class="sxs-lookup"><span data-stu-id="824c8-118">This topic addresses the situation where you have a database and want to generate code for a web application based on the fields of that database.</span></span> <span data-ttu-id="824c8-119">这种方法称为数据库优先开发。</span><span class="sxs-lookup"><span data-stu-id="824c8-119">This approach is called Database First development.</span></span> <span data-ttu-id="824c8-120">如果你还没有现有数据库，则可以改用方法称作 Code First 开发这涉及到定义数据类和类属性从生成数据库。</span><span class="sxs-lookup"><span data-stu-id="824c8-120">If you do not already have an existing database, you can instead use an approach called Code First development which involves defining data classes and generating the database from the class properties.</span></span>

<span data-ttu-id="824c8-121">Code First 开发的介绍性示例，请参阅[Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="824c8-121">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="824c8-122">有关更高级的示例，请参阅[为 ASP.NET MVC 4 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="824c8-122">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="824c8-123">选择要使用的实体框架方法的指导，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。</span><span class="sxs-lookup"><span data-stu-id="824c8-123">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="824c8-124">系统必备</span><span class="sxs-lookup"><span data-stu-id="824c8-124">Prerequisites</span></span>

<span data-ttu-id="824c8-125">Visual Studio 2013 或 Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="824c8-125">Visual Studio 2013 or Visual Studio Express 2013 for Web</span></span>

## <a name="set-up-the-database"></a><span data-ttu-id="824c8-126">将数据库设置</span><span class="sxs-lookup"><span data-stu-id="824c8-126">Set up the database</span></span>

<span data-ttu-id="824c8-127">以模拟拥有现有的数据库的环境，你将首先使用一些预填充的数据，创建一个数据库，然后创建 web 应用程序连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="824c8-127">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="824c8-128">本教程是使用 LocalDB 与 Visual Studio 2013 或 Visual Studio Express 2013 for Web 开发的。</span><span class="sxs-lookup"><span data-stu-id="824c8-128">This tutorial was developed using LocalDB with either Visual Studio 2013 or Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="824c8-129">您可以使用现有的数据库服务器，而不是 LocalDB，但具体取决于版本的 Visual Studio 和您的数据库的类型，所有 Visual Studio 中的数据工具可能不受支持。</span><span class="sxs-lookup"><span data-stu-id="824c8-129">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="824c8-130">如果这些工具不可用于你的数据库，您可能需要执行某些管理套件中的特定于数据库的步骤为你的数据库。</span><span class="sxs-lookup"><span data-stu-id="824c8-130">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="824c8-131">如果你的 Visual Studio 版本中有数据库工具的问题，请确保已安装的数据库工具的最新版本。</span><span class="sxs-lookup"><span data-stu-id="824c8-131">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="824c8-132">有关更新或安装数据库工具的信息，请参阅[Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)。</span><span class="sxs-lookup"><span data-stu-id="824c8-132">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="824c8-133">启动 Visual Studio 并创建**SQL Server 数据库项目**。</span><span class="sxs-lookup"><span data-stu-id="824c8-133">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="824c8-134">将项目命名**ContosoUniversityData**。</span><span class="sxs-lookup"><span data-stu-id="824c8-134">Name the project **ContosoUniversityData**.</span></span>

![创建数据库项目](setting-up-database/_static/image1.png)

<span data-ttu-id="824c8-136">您现在有一个空数据库项目。</span><span class="sxs-lookup"><span data-stu-id="824c8-136">You now have an empty database project.</span></span> <span data-ttu-id="824c8-137">您将此数据库在部署到 Azure 以后本教程中，因此将需要将 Azure SQL Database 设置为项目的目标平台。</span><span class="sxs-lookup"><span data-stu-id="824c8-137">You will deploy this database to Azure later in this tutorial, so you'll need to set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="824c8-138">设置目标平台不实际部署该数据库。它只意味着数据库项目将验证数据库设计为与目标平台兼容。</span><span class="sxs-lookup"><span data-stu-id="824c8-138">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="824c8-139">若要设置目标平台，打开**属性**项目并选择**Microsoft Azure SQL 数据库**为目标平台。</span><span class="sxs-lookup"><span data-stu-id="824c8-139">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

![将目标平台设置](setting-up-database/_static/image2.png)

<span data-ttu-id="824c8-141">可以创建本教程中添加的定义的表的 SQL 脚本所需的表。</span><span class="sxs-lookup"><span data-stu-id="824c8-141">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="824c8-142">右键单击项目并添加新项。</span><span class="sxs-lookup"><span data-stu-id="824c8-142">Right-click your project and add a new item.</span></span>

![添加新项](setting-up-database/_static/image3.png)

<span data-ttu-id="824c8-144">添加名为学生的新表。</span><span class="sxs-lookup"><span data-stu-id="824c8-144">Add a new table named Student.</span></span>

![添加 student 表](setting-up-database/_static/image4.png)

<span data-ttu-id="824c8-146">表文件中替换以下代码以创建表的 T-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="824c8-146">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="824c8-147">请注意，设计窗口会自动同步的代码。</span><span class="sxs-lookup"><span data-stu-id="824c8-147">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="824c8-148">您可以使用代码或设计器。</span><span class="sxs-lookup"><span data-stu-id="824c8-148">You can work with either the code or designer.</span></span>

![显示代码和设计](setting-up-database/_static/image5.png)

<span data-ttu-id="824c8-150">添加另一个表。</span><span class="sxs-lookup"><span data-stu-id="824c8-150">Add another table.</span></span> <span data-ttu-id="824c8-151">这一次课程将其命名，并使用以下 T-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="824c8-151">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="824c8-152">然后，重复一次，以创建名为注册的表。</span><span class="sxs-lookup"><span data-stu-id="824c8-152">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="824c8-153">您可以在用数据填充数据库通过部署数据库后运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="824c8-153">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="824c8-154">向项目添加后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="824c8-154">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="824c8-155">可以使用默认名称。</span><span class="sxs-lookup"><span data-stu-id="824c8-155">You can use the default name.</span></span>

![添加后期部署脚本](setting-up-database/_static/image6.png)

<span data-ttu-id="824c8-157">将以下 T-SQL 代码添加到后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="824c8-157">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="824c8-158">此脚本只需将数据添加到数据库时找到没有匹配的记录。</span><span class="sxs-lookup"><span data-stu-id="824c8-158">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="824c8-159">不覆盖或删除您可能会输入到数据库的任何数据。</span><span class="sxs-lookup"><span data-stu-id="824c8-159">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="824c8-160">请务必注意每次部署您的数据库项目时，运行后期部署脚本。</span><span class="sxs-lookup"><span data-stu-id="824c8-160">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="824c8-161">因此，您需要编写此脚本时请仔细考虑您的要求。</span><span class="sxs-lookup"><span data-stu-id="824c8-161">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="824c8-162">在某些情况下，你可能想要从一组已知的数据开始，每次部署该项目。</span><span class="sxs-lookup"><span data-stu-id="824c8-162">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="824c8-163">在其他情况下，您可能不想要更改的现有数据以任何方式。</span><span class="sxs-lookup"><span data-stu-id="824c8-163">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="824c8-164">根据您的要求，可以决定是否需要后期部署脚本或需要在脚本中包括。</span><span class="sxs-lookup"><span data-stu-id="824c8-164">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="824c8-165">有关填充使用后期部署脚本在数据库的详细信息，请参阅[SQL Server 数据库项目中包括数据](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。</span><span class="sxs-lookup"><span data-stu-id="824c8-165">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="824c8-166">现在，您有 4 个 SQL 脚本文件不存在实际的表。</span><span class="sxs-lookup"><span data-stu-id="824c8-166">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="824c8-167">已准备好将您的数据库项目部署到 localdb。</span><span class="sxs-lookup"><span data-stu-id="824c8-167">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="824c8-168">在 Visual Studio 中，单击开始按钮 （或 F5） 以生成和部署数据库项目。</span><span class="sxs-lookup"><span data-stu-id="824c8-168">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="824c8-169">检查输出选项卡以验证成功的生成和部署。</span><span class="sxs-lookup"><span data-stu-id="824c8-169">Check the Output tab to verify that the build and deployment succeeded.</span></span>

![显示输出](setting-up-database/_static/image7.png)

<span data-ttu-id="824c8-171">若要查看已创建新数据库，请打开**SQL Server 对象资源管理器**并查找正确的本地数据库服务器中的项目的名称 (在这种情况下 **(localdb) \ProjectsV12**)。</span><span class="sxs-lookup"><span data-stu-id="824c8-171">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV12**).</span></span>

![显示新的数据库](setting-up-database/_static/image8.png)

<span data-ttu-id="824c8-173">若要查看表中填充了数据，请右键单击某个表，并选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="824c8-173">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![显示表数据](setting-up-database/_static/image9.png)

<span data-ttu-id="824c8-175">显示表数据的可编辑视图。</span><span class="sxs-lookup"><span data-stu-id="824c8-175">An editable view of the table data is displayed.</span></span>

![显示表数据的结果](setting-up-database/_static/image10.png)

<span data-ttu-id="824c8-177">现在设置和使用数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="824c8-177">Your database is now set up and populated with data.</span></span> <span data-ttu-id="824c8-178">在下一步的教程中，将创建数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="824c8-178">In the next tutorial, you will create a web application for the database.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="824c8-179">下一篇</span><span class="sxs-lookup"><span data-stu-id="824c8-179">Next</span></span>](creating-the-web-application.md)
