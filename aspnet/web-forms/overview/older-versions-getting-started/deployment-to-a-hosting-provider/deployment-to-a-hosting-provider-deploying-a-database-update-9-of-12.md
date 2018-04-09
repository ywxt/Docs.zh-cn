---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 部署某一数据库更新-9 12 |Microsoft 文档
author: tdykstra
description: 这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Stu 包含 SQL Server Compact 数据库...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0a00f9d3ed284ebbc1d83c1b5696436e5ba00f4b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="ed0c8-103">部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 部署某一数据库更新-9 12</span><span class="sxs-lookup"><span data-stu-id="ed0c8-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>
====================
<span data-ttu-id="ed0c8-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="ed0c8-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="ed0c8-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="ed0c8-106">这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 中包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="ed0c8-107">如果你安装 Web 发布更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="ed0c8-108">有关序列的简介，请参阅[序列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="ed0c8-109">显示部署功能后，将 Visual Studio 2012 RC 版本中推出，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Azure App Service Web Apps 的教程，请参阅[的 ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="ed0c8-110">概述</span><span class="sxs-lookup"><span data-stu-id="ed0c8-110">Overview</span></span>

<span data-ttu-id="ed0c8-111">在本教程中，使数据库更改和相关的代码的更改，在 Visual Studio 中，测试所做的更改，然后将更新部署到测试和生产环境。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="ed0c8-112">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="ed0c8-113">将新列添加到表</span><span class="sxs-lookup"><span data-stu-id="ed0c8-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="ed0c8-114">在本部分中，你添加的出生日期列`Person`基类`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="ed0c8-115">然后你将更新，使其显示新的列显示教师数据的页。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="ed0c8-116">在*ContosoUniversity.DAL*项目中，打开*Person.cs* ，并在末尾添加以下属性`Person`（应两个关闭跟在它后面的大括号） 的类：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="ed0c8-117">接下来，更新的 Seed 方法，以便其提供了值的新列。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="ed0c8-118">打开*Migrations\Configuration.cs* ，并将开始的代码块`var instructors = new List<Instructor>`与下面的代码块，其中包括出生日期信息：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="ed0c8-119">在 ContosoUniversity 项目中，打开*Instructors.aspx*并添加一个新的模板字段来显示出生日期。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="ed0c8-120">将其添加之间对雇佣日期和 office 分配：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="ed0c8-121">（如果代码缩进获取同步的你可以按 CTRL K，然后选择 CTRL D 自动重新设置格式的文件。）</span><span class="sxs-lookup"><span data-stu-id="ed0c8-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="ed0c8-122">生成解决方案，，然后打开**程序包管理器控制台**窗口。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="ed0c8-123">请确保 ContosoUniversity.DAL 仍处于选中状态作为**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="ed0c8-124">在**程序包管理器控制台**窗口中，选择**ContosoUniversity.DAL**作为**默认项目**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="ed0c8-125">此命令完成时，Visual Studio 将打开定义新的类文件`DbMIgration`类，然后在`Up`方法你可以看到创建的新列的代码。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="ed0c8-127">生成解决方案，，然后输入以下命令包含在**程序包管理器控制台**窗口 （请确保 ContosoUniversity.DAL 项目仍处于选中状态）：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="ed0c8-128">完成该命令后，运行应用程序并选择教师页。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="ed0c8-129">在页面加载后，你看到它具有新出生日期字段。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="ed0c8-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="ed0c8-131">将数据库更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="ed0c8-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="ed0c8-132">在**解决方案资源管理器**选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="ed0c8-133">在**Web 单键发布**工具栏上，选择**测试**发布配置文件，并依次**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="ed0c8-134">(如果禁用了工具栏上，选择中的 ContosoUniversity 项目**解决方案资源管理器**。)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="ed0c8-135">Visual Studio 将部署更新的应用程序，并浏览器打开到主页。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="ed0c8-136">运行教师页后，可以验证更新成功部署。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="ed0c8-137">当应用程序尝试访问此页的数据库时，Code First，更新数据库架构，并运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="ed0c8-138">显示页时，你看到预期**出生日期**与在其中的日期的列。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="ed0c8-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="ed0c8-140">将数据库更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="ed0c8-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="ed0c8-141">你现在可以部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-141">You can now deploy to production.</span></span> <span data-ttu-id="ed0c8-142">唯一的区别是，你将使用*应用\_offline.htm*来防止用户访问该站点并因此更新数据库，而你要部署的更改。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="ed0c8-143">对于生产部署执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ed0c8-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="ed0c8-144">上载*应用\_offline.htm*到生产站点的文件。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="ed0c8-145">在 Visual Studio 中，选择中的生产配置文件**Web 单键发布**工具栏，然后单击**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="ed0c8-146">删除*应用\_offline.htm*生产站点中的文件。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="ed0c8-147">在生产环境中使用你的应用程序时你应实施备份计划。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="ed0c8-148">也就是说，你应将定期复制*学校 Prod.sdf*和*aspnet Prod.sdf*文件从生产站点到一个安全存储位置，并且您应保留多个代如备份。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="ed0c8-149">在更新数据库时，你应在更改之前立即从的备份副本。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="ed0c8-150">然后，如果犯错，进而不发现它之前，部署到生产环境之后，你仍将能够将数据库恢复到它损坏之前的状态。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>


<span data-ttu-id="ed0c8-151">当 Visual Studio 中浏览器中，打开主页 URL 时*应用\_offline.htm*显示页。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="ed0c8-152">删除后*应用\_offline.htm*文件，你可以浏览到您的主页上，以验证更新是否成功部署。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="ed0c8-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="ed0c8-154">现在，你已部署应用程序更新包含对测试和生产的数据库更改。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="ed0c8-155">下一教程演示如何将数据库从 SQL Server Compact 迁移到 SQL Server Express 和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ed0c8-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ed0c8-156">[上一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="ed0c8-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
