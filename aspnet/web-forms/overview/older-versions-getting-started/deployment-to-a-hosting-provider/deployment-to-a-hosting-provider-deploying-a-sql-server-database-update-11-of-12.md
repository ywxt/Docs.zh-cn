---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server 数据库更新-11 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 2018b58207365a0a3829f1f359d46d765aad0a77
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834561"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="271cf-103">使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server 数据库更新-11 12</span><span class="sxs-lookup"><span data-stu-id="271cf-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>
====================
<span data-ttu-id="271cf-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="271cf-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="271cf-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="271cf-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="271cf-106">本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="271cf-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="271cf-107">如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="271cf-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="271cf-108">该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="271cf-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="271cf-109">显示部署功能的 Visual Studio 2012 RC 发布后，显示了如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Windows Azure 网站的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="271cf-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="271cf-110">概述</span><span class="sxs-lookup"><span data-stu-id="271cf-110">Overview</span></span>

<span data-ttu-id="271cf-111">本教程演示如何将数据库更新部署到完整的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="271cf-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="271cf-112">因为 Code First 迁移更新数据库的所有工作，该过程是几乎与你为 SQL Server Compact 中所做[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="271cf-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="271cf-113">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="271cf-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="271cf-114">将新列添加到表</span><span class="sxs-lookup"><span data-stu-id="271cf-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="271cf-115">在本教程的此部分将使更改的数据库和相应的代码更改，然后将它们在准备部署到测试和生产环境中测试在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="271cf-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="271cf-116">更改涉及到添加`OfficeHours`列添加到`Instructor`实体并显示中的新信息**讲师**网页。</span><span class="sxs-lookup"><span data-stu-id="271cf-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="271cf-117">在 ContosoUniversity.DAL 项目中，打开*Instructor.cs* ，并添加以下属性之间`HireDate`和`Courses`属性：</span><span class="sxs-lookup"><span data-stu-id="271cf-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="271cf-118">更新初始值设定项类，使其使用测试数据的新列来设定种子。</span><span class="sxs-lookup"><span data-stu-id="271cf-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="271cf-119">打开*migrations\ configuration.cs*并将代码块的开始为`var instructors = new List<Instructor>`与下面的代码块，其中包括新列：</span><span class="sxs-lookup"><span data-stu-id="271cf-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="271cf-120">在 ContosoUniversity 项目中，打开*Instructors.aspx*并为工作时间结束之前添加新的模板字段`</Columns>`在第一个标记`GridView`控件：</span><span class="sxs-lookup"><span data-stu-id="271cf-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="271cf-121">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="271cf-121">Build the solution.</span></span>

<span data-ttu-id="271cf-122">打开**程序包管理器控制台**窗口中，并选择作为 ContosoUniversity.DAL**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="271cf-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="271cf-123">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="271cf-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="271cf-124">运行应用程序，并选择**讲师**页。</span><span class="sxs-lookup"><span data-stu-id="271cf-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="271cf-125">页面需要稍长的时间比平常要加载，因为实体框架将重新创建数据库并设定其种子使用测试数据。</span><span class="sxs-lookup"><span data-stu-id="271cf-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="271cf-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="271cf-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="271cf-127">数据库将更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="271cf-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="271cf-128">当您使用 Code First 迁移时，用于将数据库更改部署到 SQL Server 的方法是与 SQL Server Compact 相同。</span><span class="sxs-lookup"><span data-stu-id="271cf-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="271cf-129">但是，您必须更改测试发布配置文件，因为它仍设置为从 SQL Server Compact 迁移到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="271cf-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="271cf-130">第一步是删除在上一教程中创建的连接字符串转换。</span><span class="sxs-lookup"><span data-stu-id="271cf-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="271cf-131">不再需要使用这些操作因为你将发布配置文件中，指定连接字符串转换就像你在配置之前**打包/发布 SQL**迁移到 SQL Server 的选项卡。</span><span class="sxs-lookup"><span data-stu-id="271cf-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="271cf-132">打开*Web.Test.config*文件，移除`connectionStrings`元素。</span><span class="sxs-lookup"><span data-stu-id="271cf-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="271cf-133">中的唯一剩余转换*Web.Test.config*文件的用处`Environment`中的值`appSettings`元素。</span><span class="sxs-lookup"><span data-stu-id="271cf-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="271cf-134">现在你可以更新的发布配置文件和发布到测试环境。</span><span class="sxs-lookup"><span data-stu-id="271cf-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="271cf-135">打开**发布 Web**向导，然后再切换到**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="271cf-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="271cf-136">选择**测试**发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="271cf-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="271cf-137">选择**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="271cf-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="271cf-138">单击**启用新的数据库发布改进**。</span><span class="sxs-lookup"><span data-stu-id="271cf-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="271cf-139">在连接字符串中的**SchoolContext**，输入相同的值中使用*Web.Test.config*上一教程中的转换文件：</span><span class="sxs-lookup"><span data-stu-id="271cf-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="271cf-140">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="271cf-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="271cf-141">(在你的 Visual Studio 版本，可能会标记为复选框**应用 Code First 迁移**。)</span><span class="sxs-lookup"><span data-stu-id="271cf-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="271cf-142">在连接字符串中的**DefaultConnection**，输入相同的值中使用*Web.Test.config*上一教程中的转换文件：</span><span class="sxs-lookup"><span data-stu-id="271cf-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="271cf-143">将保留**更新数据库**清除。</span><span class="sxs-lookup"><span data-stu-id="271cf-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="271cf-144">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="271cf-144">Click **Publish**.</span></span>

<span data-ttu-id="271cf-145">Visual Studio 将代码更改部署到测试环境和 Contoso University 主页上的浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="271cf-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="271cf-146">选择讲师页。</span><span class="sxs-lookup"><span data-stu-id="271cf-146">Select the Instructors page.</span></span>

<span data-ttu-id="271cf-147">应用程序运行时此页，它尝试访问数据库。</span><span class="sxs-lookup"><span data-stu-id="271cf-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="271cf-148">Code First 迁移检查的数据库是最新，并查找有尚不已应用最新的迁移。</span><span class="sxs-lookup"><span data-stu-id="271cf-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="271cf-149">Code First 迁移应用最新的迁移，在运行`Seed`方法，然后页面会正常运行。</span><span class="sxs-lookup"><span data-stu-id="271cf-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="271cf-150">请参阅植入的数据的新工作时间列。</span><span class="sxs-lookup"><span data-stu-id="271cf-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="271cf-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="271cf-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="271cf-152">数据库将更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="271cf-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="271cf-153">您必须还更改生产环境的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="271cf-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="271cf-154">在这种情况下将删除现有配置文件，并创建一个新的导入更新后的.publishsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="271cf-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="271cf-155">更新后的文件将包括 Cytanium 上的 SQL Server 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="271cf-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="271cf-156">如您所见到测试环境部署时，不再需要连接字符串中的转换*Web.Production.config*转换文件。</span><span class="sxs-lookup"><span data-stu-id="271cf-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="271cf-157">打开的文件，移除`connectionStrings`元素。</span><span class="sxs-lookup"><span data-stu-id="271cf-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="271cf-158">剩余的转换适用于`Environment`中的值`appSettings`元素和`location`Elmah 错误报告中限制访问的元素。</span><span class="sxs-lookup"><span data-stu-id="271cf-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="271cf-159">在创建新的发布配置文件用于生产之前，下载更新后的.publishsettings 文件中较早像的一样[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="271cf-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="271cf-160">(在 Cytanium 控件面板中，单击**网站**，然后单击**contosouniversity.com**网站。</span><span class="sxs-lookup"><span data-stu-id="271cf-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="271cf-161">选择**Web 发布**选项卡，然后依次**下载发布配置文件添加为此网站**。)您这样做的原因是要选取的.publishsettings 文件中的数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="271cf-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="271cf-162">第一次下载该文件，因为还在使用 SQL Server Compact 和没有 SQL Server 数据库在 Cytanium 尚未创建，连接字符串不是可用。</span><span class="sxs-lookup"><span data-stu-id="271cf-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="271cf-163">现在你可以更新的发布配置文件和发布到生产环境。</span><span class="sxs-lookup"><span data-stu-id="271cf-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="271cf-164">打开**发布 Web**向导，然后再切换到**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="271cf-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="271cf-165">单击**管理配置文件**，然后删除生产配置文件。</span><span class="sxs-lookup"><span data-stu-id="271cf-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="271cf-166">关闭**发布 Web**向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="271cf-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="271cf-167">打开**发布 Web**同样，向导，然后单击**导入**。</span><span class="sxs-lookup"><span data-stu-id="271cf-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="271cf-168">上**连接**选项卡上，更改**目标 URL**为适当的值，如果您使用的临时的 URL。</span><span class="sxs-lookup"><span data-stu-id="271cf-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="271cf-169">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="271cf-169">Click **Next**.</span></span>

<span data-ttu-id="271cf-170">上**设置**选项卡上，单击**启用新的数据库发布改进**。</span><span class="sxs-lookup"><span data-stu-id="271cf-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="271cf-171">中的连接字符串下拉列表**SchoolContext**，选择 Cytanium 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="271cf-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="271cf-173">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="271cf-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="271cf-174">中的连接字符串下拉列表**DefaultConnection**，选择 Cytanium 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="271cf-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="271cf-175">选择**配置文件**选项卡上，单击**管理配置文件**，并将该配置文件重命名从"contosouniversity.com-Web 部署"，为"生产"。</span><span class="sxs-lookup"><span data-stu-id="271cf-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="271cf-176">关闭发布配置文件以保存更改，然后重新打开它。</span><span class="sxs-lookup"><span data-stu-id="271cf-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="271cf-177">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="271cf-177">Click **Publish**.</span></span> <span data-ttu-id="271cf-178">(对于实际的生产网站，会将复制*应用程序\_offline.htm*到生产环境并将置于前视情况下，项目文件夹中它然后将其删除部署完成后。)</span><span class="sxs-lookup"><span data-stu-id="271cf-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="271cf-179">Visual Studio 将代码更改部署到测试环境和 Contoso University 主页上的浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="271cf-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="271cf-180">选择讲师页。</span><span class="sxs-lookup"><span data-stu-id="271cf-180">Select the Instructors page.</span></span>

<span data-ttu-id="271cf-181">Code First 迁移更新数据库像在测试环境中的相同方法。</span><span class="sxs-lookup"><span data-stu-id="271cf-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="271cf-182">请参阅植入的数据的新工作时间列。</span><span class="sxs-lookup"><span data-stu-id="271cf-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="271cf-184">你现在已成功部署应用程序更新的包含数据库更改，使用 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="271cf-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="271cf-185">详细信息</span><span class="sxs-lookup"><span data-stu-id="271cf-185">More Information</span></span>

<span data-ttu-id="271cf-186">这样就完成这一系列的教程，介绍 ASP.NET web 应用程序部署到第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="271cf-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="271cf-187">任何在这些教程中所涉及的主题的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="271cf-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="271cf-188">致谢</span><span class="sxs-lookup"><span data-stu-id="271cf-188">Acknowledgements</span></span>

<span data-ttu-id="271cf-189">我想要感谢下列人员进行本系列教程的内容的重要贡献的人：</span><span class="sxs-lookup"><span data-stu-id="271cf-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="271cf-190">Alberto Poblacion、 MVP &amp; MCT、 西班牙</span><span class="sxs-lookup"><span data-stu-id="271cf-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="271cf-191">Jarod Ferguson，数据平台开发 MVP，美国</span><span class="sxs-lookup"><span data-stu-id="271cf-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="271cf-192">Harsh Mittal，Microsoft</span><span class="sxs-lookup"><span data-stu-id="271cf-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="271cf-193">Kristina Olson Microsoft</span><span class="sxs-lookup"><span data-stu-id="271cf-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="271cf-194">Mike 教皇 Microsoft</span><span class="sxs-lookup"><span data-stu-id="271cf-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="271cf-195">Mohit Srivastava Microsoft</span><span class="sxs-lookup"><span data-stu-id="271cf-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="271cf-196">Raffaele Rialdi，意大利</span><span class="sxs-lookup"><span data-stu-id="271cf-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="271cf-197">Rick Anderson Microsoft</span><span class="sxs-lookup"><span data-stu-id="271cf-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="271cf-198">[Sayed Hashimi、 Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="271cf-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="271cf-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="271cf-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="271cf-200">[Scott Hunter、 Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="271cf-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="271cf-201">Srđan Božović，塞尔维亚共和国</span><span class="sxs-lookup"><span data-stu-id="271cf-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="271cf-202">[Vishal Joshi、 Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="271cf-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="271cf-203">[上一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="271cf-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
