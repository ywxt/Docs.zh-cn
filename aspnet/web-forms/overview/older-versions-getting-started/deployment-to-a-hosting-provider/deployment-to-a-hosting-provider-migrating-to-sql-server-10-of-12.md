---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 迁移到 SQL Server-10 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: bc0bca18d2f6e4cdbb527ab75952e9a50eb49b20
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827350"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="f85fa-103">使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 迁移到 SQL Server-10 12</span><span class="sxs-lookup"><span data-stu-id="f85fa-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>
====================
<span data-ttu-id="f85fa-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f85fa-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f85fa-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="f85fa-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="f85fa-106">本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="f85fa-107">如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="f85fa-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="f85fa-108">该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="f85fa-109">显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="f85fa-110">概述</span><span class="sxs-lookup"><span data-stu-id="f85fa-110">Overview</span></span>

<span data-ttu-id="f85fa-111">本教程演示如何从 SQL Server Compact 迁移到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f85fa-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="f85fa-112">你可能想要执行此操作的原因之一是利用 SQL Server Compact 不支持，如存储的过程、 触发器、 视图或复制的 SQL Server 功能。</span><span class="sxs-lookup"><span data-stu-id="f85fa-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="f85fa-113">有关 SQL Server Compact 和 SQL Server 之间的差异的详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="f85fa-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="f85fa-114">SQL Server Express，而不是完整的 SQL Server 进行开发</span><span class="sxs-lookup"><span data-stu-id="f85fa-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="f85fa-115">一旦您已决定升级到 SQL Server，你可能想要在开发和测试环境中使用 SQL Server 或 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="f85fa-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="f85fa-116">工具支持在和中的数据库引擎功能的差异，除了有提供程序实现中 SQL Server Compact 与其他版本的 SQL Server 之间的差异。</span><span class="sxs-lookup"><span data-stu-id="f85fa-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="f85fa-117">这些差异可能会导致相同的代码生成不同的结果。</span><span class="sxs-lookup"><span data-stu-id="f85fa-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="f85fa-118">因此，如果您决定要保留 SQL Server Compact 与开发数据库，，应全面测试您的站点在 SQL Server 或 SQL Server Express 中每个部署到生产环境之前测试环境中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="f85fa-119">与 SQL Server Compact 不同 SQL Server Express 是实质上是相同的数据库引擎和作为完整的 SQL Server 使用相同的.NET 提供程序。</span><span class="sxs-lookup"><span data-stu-id="f85fa-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="f85fa-120">当测试与 SQL Server Express 时，您可以确信的获得相同的结果也将与 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f85fa-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="f85fa-121">可以使用 SQL Server Express 的 SQL Server 可以使用使用大部分相同的数据库工具 (值得注意的例外正在[SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx))，并支持的 SQL Server 存储的过程、 视图、 触发器等其他功能和复制。</span><span class="sxs-lookup"><span data-stu-id="f85fa-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="f85fa-122">（您通常需要在生产网站中，但是使用完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f85fa-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="f85fa-123">SQL Server Express 可以在共享宿主环境中运行，但它不是为此，请和很多宿主提供程序不支持它。）</span><span class="sxs-lookup"><span data-stu-id="f85fa-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="f85fa-124">如果正在使用 Visual Studio 2012，则通常选择 SQL Server Express LocalDB 在开发环境因为这是默认情况下使用 Visual Studio 安装的内容。</span><span class="sxs-lookup"><span data-stu-id="f85fa-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="f85fa-125">但是，在 IIS 中，因此您必须使用 SQL Server 或 SQL Server Express 为您的测试环境时，不会将 LocalDB 起作用。</span><span class="sxs-lookup"><span data-stu-id="f85fa-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="f85fa-126">而不保留它们单独存放数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="f85fa-127">Contoso 大学应用程序有两个 SQL Server Compact 数据库： 成员资格数据库 (*aspnet.sdf*) 和应用程序数据库 (*School.sdf*)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="f85fa-128">迁移时，您可以将这些数据库迁移到两个独立数据库或单个数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="f85fa-129">你可能想要将它们合并为了简化应用程序数据库和成员资格数据库之间的数据库联接。</span><span class="sxs-lookup"><span data-stu-id="f85fa-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="f85fa-130">托管计划还可能提供的原因要将它们合并。</span><span class="sxs-lookup"><span data-stu-id="f85fa-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="f85fa-131">例如，托管提供商可能会收取多个数据库的详细信息，或可能甚至不允许多个数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="f85fa-132">这是与 Cytanium Lite 承载用于本教程中，这样只有一个 SQL Server 数据库的帐户的情况。</span><span class="sxs-lookup"><span data-stu-id="f85fa-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="f85fa-133">在本教程中，你会将两个数据库迁移这种方式：</span><span class="sxs-lookup"><span data-stu-id="f85fa-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="f85fa-134">迁移到开发环境中的两个 LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="f85fa-135">迁移到测试环境中的两个 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="f85fa-136">迁移到一个组合完整 SQL Server 数据库在生产环境中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="f85fa-137">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="f85fa-138">安装 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="f85fa-138">Installing SQL Server Express</span></span>

<span data-ttu-id="f85fa-139">Visual Studio 2010 中，默认情况下会自动安装 SQL Server Express，但默认情况下它不随一起安装 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="f85fa-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="f85fa-140">若要安装 SQL Server 2012 Express，请单击以下链接</span><span class="sxs-lookup"><span data-stu-id="f85fa-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="f85fa-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="f85fa-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="f85fa-142">选择*简体中文/x64/SQLEXPR\_x64\_ENU.exe*或*简体中文/x86/SQLEXPR\_x86\_ENU.exe*，并在安装向导中，接受默认值设置。</span><span class="sxs-lookup"><span data-stu-id="f85fa-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="f85fa-143">有关安装选项的详细信息，请参阅[从安装向导 （安装程序） 中安装 SQL Server 2012](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="f85fa-144">对于测试环境中创建 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="f85fa-145">下一步是创建的 ASP.NET 成员资格和 School 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="f85fa-146">从**视图**菜单中选择**服务器资源管理器**(**数据库资源管理器**在 Visual Web Developer)，然后右键单击**数据连接**，然后选择**创建新的 SQL Server 数据库**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="f85fa-148">在中**创建新的 SQL Server 数据库**对话框框中，输入"。 \SQLExpress"在**服务器名称**框和"aspnet-测试"中**新的数据库名称**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="f85fa-150">请按照相同的过程来创建一个名为"学校-Test"的新 SQL Server Express School 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="f85fa-151">（要追加"Test"到这些数据库名因为稍后需要创建开发环境中，每个数据库的其他实例，并且需要能够以区分两个组数据库。）</span><span class="sxs-lookup"><span data-stu-id="f85fa-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="f85fa-152">**服务器资源管理器**现在将显示两个新数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="f85fa-154">创建新的数据库授予脚本</span><span class="sxs-lookup"><span data-stu-id="f85fa-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="f85fa-155">当在开发计算机上在 IIS 中运行的应用程序时，该应用程序使用的默认应用程序池的凭据访问数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="f85fa-156">但是，默认情况下，应用程序池标识没有权限打开的数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="f85fa-157">因此您必须运行一个脚本，以授予该权限。</span><span class="sxs-lookup"><span data-stu-id="f85fa-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="f85fa-158">在本部分中，您将创建将运行更高版本以确保在 IIS 中运行时，该应用程序可以打开数据库的脚本。</span><span class="sxs-lookup"><span data-stu-id="f85fa-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="f85fa-159">在解决方案中*SolutionFiles*中创建的文件夹[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中，创建名为的新 SQL 文件*Grant.sql*。</span><span class="sxs-lookup"><span data-stu-id="f85fa-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="f85fa-160">将以下 SQL 命令复制到文件，然后保存并关闭文件：</span><span class="sxs-lookup"><span data-stu-id="f85fa-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="f85fa-161">此脚本用于处理与 SQL Server 2008 和 Windows 7 中的 IIS 设置，如在本教程中指定了。</span><span class="sxs-lookup"><span data-stu-id="f85fa-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="f85fa-162">如果使用不同版本的 SQL Server 或 Windows，或您设置 IIS 计算机上以不同的方式，可能需要对此脚本的更改。</span><span class="sxs-lookup"><span data-stu-id="f85fa-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="f85fa-163">有关 SQL Server 脚本详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="f85fa-164">**安全说明**此脚本将向提供 db\_所有者在运行时，这是您在生产环境中必须访问数据库的用户的权限。</span><span class="sxs-lookup"><span data-stu-id="f85fa-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="f85fa-165">在某些情况下您可能想要指定具有完整的数据库架构更新部署中，权限和指定的运行时具有的权限仅读取和写入数据的不同用户的用户。</span><span class="sxs-lookup"><span data-stu-id="f85fa-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="f85fa-166">有关详细信息，请参阅**评审 Code First 迁移自动 Web.config 更改**中[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>


## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="f85fa-167">配置测试环境的数据库部署</span><span class="sxs-lookup"><span data-stu-id="f85fa-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="f85fa-168">接下来，您将配置 Visual Studio，以便它将执行以下任务，以便每个数据库：</span><span class="sxs-lookup"><span data-stu-id="f85fa-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="f85fa-169">生成 SQL 脚本，在目标数据库中创建源数据库的结构 （表、 列、 约束等）。</span><span class="sxs-lookup"><span data-stu-id="f85fa-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="f85fa-170">生成 SQL 脚本，将源数据库的数据插入到目标数据库中的表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="f85fa-171">运行生成的脚本，并创建目标数据库中授予脚本。</span><span class="sxs-lookup"><span data-stu-id="f85fa-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="f85fa-172">打开**项目属性**窗口，然后选择**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f85fa-173">请确保**处于活动状态 （发布）** 或**发行**中选择**配置**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="f85fa-174">单击**启用此页**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="f85fa-176">**打包/发布 SQL**因为它指定旧部署方法，通常会禁用选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="f85fa-177">大多数情况下，应配置中的数据库部署**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="f85fa-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="f85fa-178">从 SQL Server Compact 迁移到 SQL Server 或 SQL Server Express 是一种特殊情况，此方法是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="f85fa-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="f85fa-179">单击**从 Web.config 导入**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="f85fa-181">Visual Studio 将查找连接字符串*Web.config*文件中，查找另一个用于成员资格数据库，一个用于 School 数据库，并将行对应于每个连接字符串中添加**数据库条目**表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="f85fa-182">对于现有的 SQL Server Compact 数据库，是它找到的连接字符串和下一步就是要配置方式和位置来部署这些数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="f85fa-183">输入中的数据库部署设置**数据库项详细信息**以下部分**数据库条目**表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="f85fa-184">中所示的设置**数据库项详细信息**部分适用于二者中的一行**数据库条目**选择表，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="f85fa-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="f85fa-186">配置部署设置的成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="f85fa-187">选择**DefaultConnection 部署**中的一行**数据库条目**表中以配置应用于成员资格数据库的设置。</span><span class="sxs-lookup"><span data-stu-id="f85fa-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="f85fa-188">在中**目标数据库的连接字符串**，输入指向新的 SQL Server Express 成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f85fa-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="f85fa-189">可以获取从所需的连接字符串**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="f85fa-190">在中**服务器资源管理器**，展开**数据连接**，然后选择**aspnetTest**数据库，然后从**属性**窗口复制**连接字符串**值。</span><span class="sxs-lookup"><span data-stu-id="f85fa-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="f85fa-192">此处重现相同的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="f85fa-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="f85fa-193">复制并粘贴到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f85fa-194">请确保**抽取数据和/或从现有数据库架构**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="f85fa-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="f85fa-195">这是哪些因素会导致 SQL 脚本来自动生成并运行目标数据库中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="f85fa-196">**源数据库的连接字符串**从提取值*Web.config*文件，指向开发 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="f85fa-197">这是将用于生成将在目标数据库中更高版本运行的脚本的源数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="f85fa-198">由于你想要部署生产版本的数据库，更改"aspnet Dev.sdf"为"aspnet Prod.sdf"。</span><span class="sxs-lookup"><span data-stu-id="f85fa-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="f85fa-199">更改**数据库脚本选项**从**仅限架构**到**架构和数据**，因为要从中复制数据 （用户帐户和角色） 以及数据库结构。</span><span class="sxs-lookup"><span data-stu-id="f85fa-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="f85fa-200">若要配置部署运行之前创建的授予脚本，必须将其添加到**数据库脚本**部分。</span><span class="sxs-lookup"><span data-stu-id="f85fa-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="f85fa-201">单击**添加脚本**，然后在**添加 SQL 脚本**对话框框中，导航到你在其中存储授予脚本的文件夹 （这是包含您的解决方案文件的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="f85fa-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="f85fa-202">选择名为的文件*Grant.sql*，然后单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="f85fa-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="f85fa-204">设置**DefaultConnection 部署**中的一行**数据库条目**现在如以下插图所示：</span><span class="sxs-lookup"><span data-stu-id="f85fa-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="f85fa-206">配置部署设置的 School 数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="f85fa-207">接下来，选择**SchoolContext 部署**中的一行**数据库条目**若要配置的 School 数据库部署设置的表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="f85fa-208">可以使用你之前用来获取新的 SQL Server Express 数据库的连接字符串的相同方法。</span><span class="sxs-lookup"><span data-stu-id="f85fa-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="f85fa-209">将复制到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="f85fa-210">请确保**抽取数据和/或从现有数据库架构**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="f85fa-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="f85fa-211">**源数据库的连接字符串**从提取值*Web.config*文件，指向开发 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="f85fa-212">将"学校 Dev.sdf"更改为"学校-Prod.sdf"若要部署生产版本的数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="f85fa-213">(在应用中永远不会创建学校 Prod.sdf 文件\_Data 文件夹中，因此会将该文件从测试环境复制到应用\_ContosoUniversity 项目文件夹更高版本中的数据文件夹。)</span><span class="sxs-lookup"><span data-stu-id="f85fa-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="f85fa-214">更改**数据库脚本选项**到**架构和数据**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="f85fa-215">您还想要运行脚本，以授予读取和写入应用程序池标识此数据库的权限，因此添加*Grant.sql*之前用于成员资格数据库的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="f85fa-216">完成后，设置**SchoolContext 部署**中的一行**数据库条目**如以下插图所示：</span><span class="sxs-lookup"><span data-stu-id="f85fa-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="f85fa-218">保存对更改**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f85fa-219">复制*学校 Prod.sdf*文件从*c:\inetpub\wwwroot\ContosoUniversity\App\_数据*文件夹*应用\_数据*文件夹中在 ContosoUniversity 项目中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="f85fa-220">为授予脚本指定事务的模式</span><span class="sxs-lookup"><span data-stu-id="f85fa-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="f85fa-221">部署过程生成脚本来部署数据库架构和数据。</span><span class="sxs-lookup"><span data-stu-id="f85fa-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="f85fa-222">默认情况下，这些脚本在事务中运行。</span><span class="sxs-lookup"><span data-stu-id="f85fa-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="f85fa-223">但是，默认情况下 （如 grant 脚本中） 的自定义脚本不能在事务中运行。</span><span class="sxs-lookup"><span data-stu-id="f85fa-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="f85fa-224">如果部署过程包含事务模式，在部署期间运行的脚本时可能遇到超时错误。</span><span class="sxs-lookup"><span data-stu-id="f85fa-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="f85fa-225">在本部分中，若要配置自定义脚本来运行在事务中编辑项目文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="f85fa-226">在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，然后选择**卸载项目**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="f85fa-228">然后再次右键单击项目并选择**编辑 ContosoUniversity.csproj**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="f85fa-230">Visual Studio 编辑器中显示项目文件的 XML 的内容。</span><span class="sxs-lookup"><span data-stu-id="f85fa-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="f85fa-231">请注意，有几条`PropertyGroup`元素。</span><span class="sxs-lookup"><span data-stu-id="f85fa-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="f85fa-232">(在图中的内容，`PropertyGroup`省略了元素。)</span><span class="sxs-lookup"><span data-stu-id="f85fa-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![项目文件编辑器窗口](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="f85fa-234">第一个，不具有`Condition`属性，而不考虑应用的设置生成配置的。</span><span class="sxs-lookup"><span data-stu-id="f85fa-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="f85fa-235">一个`PropertyGroup`元素仅适用于调试生成配置 (请注意`Condition`属性)、 一个仅适用于发布生成配置，并且其中一个仅适用于测试生成配置。</span><span class="sxs-lookup"><span data-stu-id="f85fa-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="f85fa-236">内`PropertyGroup`元素中的为发布生成配置，你将看到`PublishDatabaseSettings`上输入的包含设置元素**打包/发布 SQL**选项卡。没有`Object`对应于每个授权脚本的元素的指定的 （请注意，这两个实例"Grant.sql"）。</span><span class="sxs-lookup"><span data-stu-id="f85fa-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="f85fa-237">默认情况下`Transacted`的属性`Source`元素为每个授予脚本`False`。</span><span class="sxs-lookup"><span data-stu-id="f85fa-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="f85fa-239">更改的值`Transacted`的属性`Source`元素`True`。</span><span class="sxs-lookup"><span data-stu-id="f85fa-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="f85fa-241">保存并关闭项目文件中，并右键单击项目中的**解决方案资源管理器**，然后选择**重新加载项目**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="f85fa-243">设置连接字符串的 Web.Config 转换</span><span class="sxs-lookup"><span data-stu-id="f85fa-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="f85fa-244">连接字符串的新的 SQL Express 数据库输入**打包/发布 SQL**选项卡上通过 Web 部署仅用于在部署期间更新目标数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="f85fa-245">您仍必须设置*Web.config*转换，以便在已部署中的连接字符串*Web.config*文件指向新的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="f85fa-246">(当你使用**打包/发布 SQL**选项卡上，无法在发布配置文件中配置连接字符串。)</span><span class="sxs-lookup"><span data-stu-id="f85fa-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="f85fa-247">打开*Web.Test.config*和替换`connectionStrings`具有元素`connectionStrings`下面的示例中的元素。</span><span class="sxs-lookup"><span data-stu-id="f85fa-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="f85fa-248">（请确保你仅将复制 connectionStrings 元素，而不是如下所示提供上下文的周围的代码。）</span><span class="sxs-lookup"><span data-stu-id="f85fa-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="f85fa-249">此代码会导致`connectionString`并`providerName`每个属性`add`要被替换元素中已部署*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="f85fa-250">这些连接字符串不是你在中输入相同**打包/发布 SQL**选项卡。设置"MultipleActiveResultSets = True"具有已添加到它们，因为它具有所需的实体框架和通用提供程序。</span><span class="sxs-lookup"><span data-stu-id="f85fa-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="f85fa-251">安装 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f85fa-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="f85fa-252">SqlServerCompact NuGet 包提供 SQL Server Compact 数据库引擎的 Contoso 大学应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="f85fa-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="f85fa-253">但现在它不是应用程序，但 Web 部署，必须能够读取 SQL Server Compact 数据库中，若要创建在 SQL Server 数据库中运行脚本。</span><span class="sxs-lookup"><span data-stu-id="f85fa-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="f85fa-254">若要启用 Web 部署可以读取 SQL Server Compact 数据库，请安装 SQL Server Compact 在开发计算机上使用以下链接： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="f85fa-255">部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="f85fa-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="f85fa-256">若要发布到测试环境，您必须创建配置为使用的发布配置文件**打包/发布 SQL**数据库发布而不发布配置文件数据库设置的选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="f85fa-257">首先，删除现有的测试配置文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="f85fa-258">在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f85fa-259">选择**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="f85fa-260">单击**管理配置文件**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="f85fa-261">选择**测试**，单击**删除**，然后单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="f85fa-262">关闭**发布 Web**向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="f85fa-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="f85fa-263">接下来，创建新的测试配置文件，并使用它来发布该项目。</span><span class="sxs-lookup"><span data-stu-id="f85fa-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="f85fa-264">在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f85fa-265">选择**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="f85fa-266">选择**&lt;新...&gt;** 从下拉列表中，并输入"Test"作为配置文件名称。</span><span class="sxs-lookup"><span data-stu-id="f85fa-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="f85fa-267">在中**服务 URL**框中，输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="f85fa-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="f85fa-268">在中**站点/应用程序**框中，输入*默认 Web 站点/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="f85fa-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="f85fa-269">在中**目标 URL**框中，输入 `http://localhost/ContosoUniversity/` 。</span><span class="sxs-lookup"><span data-stu-id="f85fa-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="f85fa-270">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-270">Click **Next**.</span></span>

<span data-ttu-id="f85fa-271">**设置**选项卡会发出警告，**打包/发布 SQL**已经配置了选项卡上，并且它使你有机会来覆盖它们通过单击启用新的数据库发布的改进。</span><span class="sxs-lookup"><span data-stu-id="f85fa-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="f85fa-272">为此部署，不想要重写**打包/发布 SQL**选项卡上设置，因此只需单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="f85fa-274">中的消息**预览版**选项卡指示**没有数据库选择发布**，但这只意味着未在发布配置文件中配置数据库发布。</span><span class="sxs-lookup"><span data-stu-id="f85fa-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="f85fa-275">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="f85fa-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="f85fa-277">Visual Studio 部署应用程序，并在测试环境中的站点的主页上浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="f85fa-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="f85fa-278">运行讲师页以查看它显示您在前面看到的相同数据。</span><span class="sxs-lookup"><span data-stu-id="f85fa-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="f85fa-279">运行**添加学生**页上，添加新学生，然后查看中的新学生**学生**页。</span><span class="sxs-lookup"><span data-stu-id="f85fa-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="f85fa-280">这将验证你可以更新数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="f85fa-281">选择**更新信用额度**（需要登录） 的页以验证是否已部署成员资格数据库并有权访问它。</span><span class="sxs-lookup"><span data-stu-id="f85fa-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="f85fa-282">对于生产环境中创建 SQL Server 数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="f85fa-283">现在，已部署到测试环境，你准备好设置部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="f85fa-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="f85fa-284">在开始之前用于测试环境中，通过创建要部署到的数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="f85fa-285">您还记得概述，Cytanium Lite 托管计划将仅允许单个 SQL Server 数据库，因此将只有一个数据库，不是两个设置。</span><span class="sxs-lookup"><span data-stu-id="f85fa-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="f85fa-286">所有表和成员身份和学校 SQL Server Compact 数据库中的数据将部署到生产环境中的一个 SQL Server 数据库中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="f85fa-287">转到 Cytanium 控件面板[ http://panel.cytanium.com ](http://panel.cytanium.com)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="f85fa-288">将鼠标悬停**数据库**，然后单击**SQL Server 2008**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="f85fa-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="f85fa-290">在中**SQL Server 2008**页上，单击**Create Database**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="f85fa-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="f85fa-292">命名数据库"学校"，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="f85fa-293">（页上会自动添加前缀"contosou"，因此有效的名称将是"contosouSchool"。）</span><span class="sxs-lookup"><span data-stu-id="f85fa-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="f85fa-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="f85fa-295">在同一页上，单击**Create User**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="f85fa-296">在 Cytanium 的服务器，而不是使用集成的 Windows 安全性，并让应用程序池标识，打开你的数据库，你将创建有权打开你的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="f85fa-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="f85fa-297">你将转到生产环境中的连接字符串添加用户的凭据*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="f85fa-298">在此步骤中创建这些凭据。</span><span class="sxs-lookup"><span data-stu-id="f85fa-298">In this step you create those credentials.</span></span>

<span data-ttu-id="f85fa-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="f85fa-300">填写必填字段**SQL 用户属性**页：</span><span class="sxs-lookup"><span data-stu-id="f85fa-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="f85fa-301">输入"ContosoUniversityUser"作为名称。</span><span class="sxs-lookup"><span data-stu-id="f85fa-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="f85fa-302">输入密码。</span><span class="sxs-lookup"><span data-stu-id="f85fa-302">Enter a password.</span></span>
- <span data-ttu-id="f85fa-303">选择**contosouSchool**作为默认数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="f85fa-304">选择**contosouSchool**复选框。</span><span class="sxs-lookup"><span data-stu-id="f85fa-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="f85fa-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="f85fa-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="f85fa-306">在生产环境的配置数据库部署</span><span class="sxs-lookup"><span data-stu-id="f85fa-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="f85fa-307">现在您已准备好设置中的数据库部署设置**打包/发布 SQL**选项卡，如之前在测试环境。</span><span class="sxs-lookup"><span data-stu-id="f85fa-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="f85fa-308">打开**项目属性**窗口中，选择**打包/发布 SQL**选项卡，并确保选中**处于活动状态 （发布）** 或者**版本**是在所选**配置**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="f85fa-309">在配置部署设置为每个数据库时，你的生产和测试环境所执行的操作的主要区别是如何配置连接字符串中。</span><span class="sxs-lookup"><span data-stu-id="f85fa-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="f85fa-310">对于测试环境中输入不同的目标数据库连接字符串，但是对于生产环境目标连接字符串将是相同的两个数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="f85fa-311">这是因为这两个数据库部署到生产环境中的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="f85fa-312">配置部署设置的成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="f85fa-313">若要配置将应用于成员资格数据库的设置，请选择**DefaultConnection 部署**中的一行**数据库条目**表。</span><span class="sxs-lookup"><span data-stu-id="f85fa-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="f85fa-314">在中**目标数据库的连接字符串**，输入指向刚创建的新生产 SQL Server 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f85fa-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="f85fa-315">可以从欢迎使用电子邮件来获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f85fa-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="f85fa-316">电子邮件的相关部分包含以下示例连接字符串：</span><span class="sxs-lookup"><span data-stu-id="f85fa-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="f85fa-317">替换为三个变量后，您需要的连接字符串看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="f85fa-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="f85fa-318">复制并粘贴到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="f85fa-319">请确保**抽取数据和/或从现有数据库架构**仍然选择，且**数据库脚本选项**仍**架构和数据**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="f85fa-320">在中**数据库脚本**框中，清除 Grant.sql 脚本旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="f85fa-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="f85fa-322">配置部署设置的 School 数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="f85fa-323">接下来，选择**SchoolContext 部署**中的一行**数据库条目**表中以配置 School 数据库设置。</span><span class="sxs-lookup"><span data-stu-id="f85fa-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="f85fa-324">将复制到相同的连接字符串**目标数据库的连接字符串**复制到此字段中的成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="f85fa-325">请确保**抽取数据和/或从现有数据库架构**仍然选择，且**数据库脚本选项**仍**架构和数据**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="f85fa-326">在中**数据库脚本**框中，清除 Grant.sql 脚本旁边的复选框。</span><span class="sxs-lookup"><span data-stu-id="f85fa-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="f85fa-327">保存对更改**打包/发布 SQL**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="f85fa-328">设置 Web.Config 转换为对生产数据库的连接字符串</span><span class="sxs-lookup"><span data-stu-id="f85fa-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="f85fa-329">接下来，你将设置*Web.config*转换，以便在已部署中的连接字符串*Web.config*文件以指向新的生产数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="f85fa-330">输入的连接字符串**打包/发布 SQL** Web 部署可以使用选项卡是与应用程序需要使用，除了添加一个相同`MultipleResultSets`选项。</span><span class="sxs-lookup"><span data-stu-id="f85fa-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="f85fa-331">打开*Web.Production.config*和替换`connectionStrings`具有元素`connectionStrings`元素，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="f85fa-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="f85fa-332">(仅复制`connectionStrings`元素中，不提供要显示的上下文的周围的标记。)</span><span class="sxs-lookup"><span data-stu-id="f85fa-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="f85fa-333">有时，您看到建议，告诉你始终加密中的连接字符串*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="f85fa-334">这可能是如果你已部署到你自己的公司网络上的服务器。</span><span class="sxs-lookup"><span data-stu-id="f85fa-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="f85fa-335">时要部署到共享宿主环境中，不过，将信任托管提供商的安全做法并不是必需的或实际加密连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f85fa-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="f85fa-336">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="f85fa-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="f85fa-337">现在你已准备好部署到生产。</span><span class="sxs-lookup"><span data-stu-id="f85fa-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="f85fa-338">Web 部署将在项目中的 SQL Server Compact 数据库中读取*应用程序\_数据*文件夹，然后重新创建其所有表和生产 SQL Server 数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="f85fa-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="f85fa-339">若要通过使用发布**打包/发布 Web**选项卡设置，则必须创建新的发布配置文件用于生产。</span><span class="sxs-lookup"><span data-stu-id="f85fa-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="f85fa-340">首先，删除现有的生产配置文件，如之前所做的测试配置文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="f85fa-341">在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f85fa-342">选择**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="f85fa-343">单击**管理配置文件**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="f85fa-344">选择**生产**，单击**删除**，然后单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="f85fa-345">关闭**发布 Web**向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="f85fa-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="f85fa-346">接下来，创建新的生产配置文件，并使用它来发布该项目。</span><span class="sxs-lookup"><span data-stu-id="f85fa-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="f85fa-347">在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="f85fa-348">选择**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="f85fa-349">单击**导入**，并选择前面下载的.publishsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="f85fa-350">上**连接**选项卡上，更改**目标 URL**到正确的临时 URL，在此示例是 http://contosouniversity.com.vserver01.cytanium.com 。</span><span class="sxs-lookup"><span data-stu-id="f85fa-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="f85fa-351">重命名到生产环境的配置文件。</span><span class="sxs-lookup"><span data-stu-id="f85fa-351">Rename the profile to Production.</span></span> <span data-ttu-id="f85fa-352">(选择**配置文件**选项卡，单击**管理配置文件**若要执行此操作)。</span><span class="sxs-lookup"><span data-stu-id="f85fa-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="f85fa-353">关闭**发布 Web**向导将保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f85fa-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="f85fa-354">在实际的应用程序在其中正在更新数据库在生产环境中，您将执行两个附加步骤现在在发布之前：</span><span class="sxs-lookup"><span data-stu-id="f85fa-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="f85fa-355">上传*应用程序\_offline.htm*，如下所示[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="f85fa-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="f85fa-356">使用**文件管理器**Cytanium 控件面板要复制的功能*aspnet Prod.sdf*并*学校 Prod.sdf*文件从生产站点复制到*应用程序\_数据*ContosoUniversity 项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="f85fa-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="f85fa-357">这可确保要部署到新的 SQL Server 数据库的数据包括最新的更新所做的生产网站。</span><span class="sxs-lookup"><span data-stu-id="f85fa-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="f85fa-358">在中**Web 单键发布**工具栏中，请确保**生产**配置文件已选中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="f85fa-359">如果上传<em>应用程序\_offline.htm</em>发布前，您必须使用<strong>文件管理器</strong>实用程序在要删除的 Cytanium 控件面板<em>应用\_脱机。</em>htm 然后再测试。</span><span class="sxs-lookup"><span data-stu-id="f85fa-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="f85fa-360">你还可以在同一时间删除<em>.sdf</em>文件从<em>应用\_数据</em>文件夹。</span><span class="sxs-lookup"><span data-stu-id="f85fa-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="f85fa-361">你现在可以打开浏览器并转到您的个人网站的 URL 以测试应用程序相同的方式部署到测试环境之后。</span><span class="sxs-lookup"><span data-stu-id="f85fa-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="f85fa-362">切换到开发中的 SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="f85fa-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="f85fa-363">如概述中所述，它是通常最好在测试和生产环境中使用的开发中使用相同的数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="f85fa-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="f85fa-364">（请记住在开发中使用 SQL Server Express 的优势是，数据库仍将可用开发、 测试和生产环境中）。在本部分中您将设置为 ContosoUniversity 项目从 Visual Studio 运行应用程序时使用 SQL Server Express LocalDB。</span><span class="sxs-lookup"><span data-stu-id="f85fa-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="f85fa-365">若要执行此迁移的最简单方法是让代码优先和成员资格系统为你创建这两个新的开发数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="f85fa-366">使用此方法将迁移需要三个步骤：</span><span class="sxs-lookup"><span data-stu-id="f85fa-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="f85fa-367">更改连接字符串以指定新的 SQL Express LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="f85fa-368">运行网站管理工具以创建管理员用户。</span><span class="sxs-lookup"><span data-stu-id="f85fa-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="f85fa-369">这将创建成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="f85fa-369">This creates the membership database.</span></span>
3. <span data-ttu-id="f85fa-370">使用 Code First 迁移更新数据库命令来创建和设置应用程序数据库的种子。</span><span class="sxs-lookup"><span data-stu-id="f85fa-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="f85fa-371">正在更新 Web.config 文件中的连接字符串</span><span class="sxs-lookup"><span data-stu-id="f85fa-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="f85fa-372">打开*Web.config*文件，然后替换`connectionStrings`元素使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="f85fa-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="f85fa-373">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-373">Creating the Membership Database</span></span>

<span data-ttu-id="f85fa-374">在中**解决方案资源管理器**，选择 ContosoUniversity 项目，然后单击**ASP.NET 配置**中**项目**菜单。</span><span class="sxs-lookup"><span data-stu-id="f85fa-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="f85fa-375">选择安全选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-375">Select the Security tab.</span></span>

<span data-ttu-id="f85fa-376">单击**创建或管理角色**，然后创建**管理员**角色。</span><span class="sxs-lookup"><span data-stu-id="f85fa-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="f85fa-377">返回到安全选项卡。</span><span class="sxs-lookup"><span data-stu-id="f85fa-377">Return to the Security tab.</span></span>

<span data-ttu-id="f85fa-378">单击**创建用户**，然后选择**管理员**复选框，并创建名为管理员的用户</span><span class="sxs-lookup"><span data-stu-id="f85fa-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="f85fa-379">关闭**网站管理工具**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="f85fa-380">创建 School 数据库</span><span class="sxs-lookup"><span data-stu-id="f85fa-380">Creating the School Database</span></span>

<span data-ttu-id="f85fa-381">打开包管理器控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="f85fa-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="f85fa-382">在中**默认项目**下拉列表中，选择 ContosoUniversity.DAL 项目。</span><span class="sxs-lookup"><span data-stu-id="f85fa-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="f85fa-383">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f85fa-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="f85fa-384">Code First 迁移应用的初始迁移创建数据库，然后应用 AddBirthDate 迁移，然后运行 Seed 方法。</span><span class="sxs-lookup"><span data-stu-id="f85fa-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="f85fa-385">通过按控件 F5 运行该站点。</span><span class="sxs-lookup"><span data-stu-id="f85fa-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="f85fa-386">与用于测试和生产环境一样，运行**添加学生**页上，添加新学生，然后查看中的新学生**学生**页。</span><span class="sxs-lookup"><span data-stu-id="f85fa-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="f85fa-387">这将验证 School 数据库已创建并初始化和你已阅读并向其中写入访问权限。</span><span class="sxs-lookup"><span data-stu-id="f85fa-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="f85fa-388">选择**更新信用额度**页上，然后登录以验证成员资格数据库已部署并且有权访问它。</span><span class="sxs-lookup"><span data-stu-id="f85fa-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="f85fa-389">如果未迁移的用户帐户，创建一个管理员帐户，然后选择**更新信用额度**页后，可以验证它是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="f85fa-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="f85fa-390">清除 SQL Server Compact 文件</span><span class="sxs-lookup"><span data-stu-id="f85fa-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="f85fa-391">您不再需要的文件和已包含在内以支持 SQL Server Compact 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f85fa-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="f85fa-392">如果你想 （此步骤不需要），你可以清理不需要的文件和引用。</span><span class="sxs-lookup"><span data-stu-id="f85fa-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="f85fa-393">在中**解决方案资源管理器**，删除 *.sdf*从文件*应用\_数据*文件夹和*amd64*和*x86*从文件夹*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="f85fa-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="f85fa-394">在中**解决方案资源管理器**，右键单击该解决方案 （而不是项目的），并单击**为解决方案管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="f85fa-395">在左窗格中**管理 NuGet 包**对话框中，选择**已安装的包**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="f85fa-396">选择**EntityFramework.SqlServerCompact**程序包，再单击**管理**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="f85fa-397">在中**选择项目**对话框中，选择这两个项目。</span><span class="sxs-lookup"><span data-stu-id="f85fa-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="f85fa-398">若要卸载这两个项目中的包，请清除这两个复选框，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="f85fa-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="f85fa-399">在询问您是否也卸载依赖的包的对话框中，单击不可以。</span><span class="sxs-lookup"><span data-stu-id="f85fa-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="f85fa-400">其中一种是您必须保留的实体框架包。</span><span class="sxs-lookup"><span data-stu-id="f85fa-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="f85fa-401">请按照相同的过程来卸载**SqlServerCompact**包。</span><span class="sxs-lookup"><span data-stu-id="f85fa-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="f85fa-402">(必须按以下顺序卸载包，因为**EntityFramework.SqlServerCompact**程序包依赖于**SqlServerCompact**包。)</span><span class="sxs-lookup"><span data-stu-id="f85fa-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="f85fa-403">你现在已成功迁移到 SQL Server Express 和完整的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="f85fa-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="f85fa-404">在下一个教程将使另一个数据库更改，并将了解如何测试和生产数据库使用 SQL Server Express 和完整的 SQL Server 时部署数据库更改。</span><span class="sxs-lookup"><span data-stu-id="f85fa-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f85fa-405">[上一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="f85fa-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
