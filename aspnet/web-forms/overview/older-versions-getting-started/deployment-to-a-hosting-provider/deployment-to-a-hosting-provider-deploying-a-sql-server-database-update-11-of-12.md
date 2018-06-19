---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 部署 SQL Server 数据库更新-11 12 |Microsoft 文档
author: tdykstra
description: 这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Stu 包含 SQL Server Compact 数据库...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: d8cc072c631900937f31c8f2637869b53d46cf54
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887325"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="2f5a3-103">部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 部署 SQL Server 数据库更新-11 12</span><span class="sxs-lookup"><span data-stu-id="2f5a3-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>
====================
<span data-ttu-id="2f5a3-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="2f5a3-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="2f5a3-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="2f5a3-106">这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 中包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="2f5a3-107">如果你安装 Web 发布更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="2f5a3-108">有关序列的简介，请参阅[序列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="2f5a3-109">显示部署功能后，将 Visual Studio 2012 RC 版本中推出，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Windows Azure 网站的教程，请参阅[的 ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="2f5a3-110">概述</span><span class="sxs-lookup"><span data-stu-id="2f5a3-110">Overview</span></span>

<span data-ttu-id="2f5a3-111">本教程演示如何将数据库更新部署到完整的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="2f5a3-112">Code First 迁移进行的更新的数据库的所有工作，因为进程在几乎等同于为 SQL Server Compact 中未[部署某一数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="2f5a3-113">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="2f5a3-114">将新列添加到表</span><span class="sxs-lookup"><span data-stu-id="2f5a3-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="2f5a3-115">在本教程的本部分中，你将使数据库更改和相应的代码更改，然后将它们在准备将它们部署到测试和生产环境中测试 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="2f5a3-116">更改涉及添加`OfficeHours`列`Instructor`实体和显示中的新信息**教师**网页。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="2f5a3-117">在 ContosoUniversity.DAL 项目中，打开*Instructor.cs*并添加以下属性之间`HireDate`和`Courses`属性：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="2f5a3-118">更新初始值设定项类，以便它设定种子测试数据的新列。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="2f5a3-119">打开*Migrations\Configuration.cs* ，并将开始的代码块`var instructors = new List<Instructor>`与下面的代码块，其中包括新的列：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="2f5a3-120">在 ContosoUniversity 项目中，打开*Instructors.aspx*和为办公时间结束之前添加新的模板字段`</Columns>`中第一个标记`GridView`控件：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="2f5a3-121">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-121">Build the solution.</span></span>

<span data-ttu-id="2f5a3-122">打开**程序包管理器控制台**窗口中，并选择作为 ContosoUniversity.DAL**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="2f5a3-123">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="2f5a3-124">运行应用程序并选择**教师**页。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="2f5a3-125">页面需要花费比平常若要加载，因为实体框架将重新创建数据库并设定其种子使用测试数据需要更长时间。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="2f5a3-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="2f5a3-127">将数据库更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="2f5a3-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="2f5a3-128">当你使用 Code First 迁移时，则将数据库更改部署到 SQL Server 的方法是与 SQL Server Compact 相同。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="2f5a3-129">但是，你必须将测试更改发布配置文件，因为它仍设置以从 SQL Server Compact 迁移到 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="2f5a3-130">第一步是删除你在前面的教程中创建的连接字符串转换。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="2f5a3-131">不再需要这些因为你将在发布配置文件，指定连接字符串转换就像你配置之前**打包/发布 SQL**迁移到 SQL Server 的选项卡。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="2f5a3-132">打开*Web.Test.config*文件并删除`connectionStrings`元素。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="2f5a3-133">中的唯一剩余转换*Web.Test.config*文件可供`Environment`中的值`appSettings`元素。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="2f5a3-134">现在你可以更新的发布配置文件和发布到测试环境。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="2f5a3-135">打开**发布 Web**向导，并切换至**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="2f5a3-136">选择**测试**发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="2f5a3-137">选择**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="2f5a3-138">单击**启用新的数据库发布改进**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="2f5a3-139">中的连接字符串框**SchoolContext**，输入你在中使用的相同值*Web.Test.config*以前一教程中的转换文件：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="2f5a3-140">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="2f5a3-141">(在你的 Visual Studio 版本，可能标记为复选框**应用 Code First 迁移**。)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="2f5a3-142">中的连接字符串框**DefaultConnection**，输入你在中使用的相同值*Web.Test.config*以前一教程中的转换文件：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="2f5a3-143">保留**更新数据库**清除。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="2f5a3-144">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-144">Click **Publish**.</span></span>

<span data-ttu-id="2f5a3-145">Visual Studio 将代码更改部署到测试环境，并打开浏览器向 Contoso 大学主页上。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="2f5a3-146">选择教师页。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-146">Select the Instructors page.</span></span>

<span data-ttu-id="2f5a3-147">当应用程序运行时此页时，它将尝试访问数据库。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="2f5a3-148">Code First 迁移检查的数据库是最新状态，并查找不已尚未应用最新的迁移。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="2f5a3-149">Code First 迁移应用最新的迁移，运行`Seed`方法，，然后选择页会正常运行。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="2f5a3-150">你看到植入的数据的新办公时间列。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="2f5a3-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="2f5a3-152">将数据库更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="2f5a3-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="2f5a3-153">你必须还更改生产环境的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="2f5a3-154">在这种情况下将删除现有配置文件，并创建一个新通过导入更新的.publishsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="2f5a3-155">更新的文件将包括 Cytanium 上的 SQL Server 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="2f5a3-156">正如你看到时部署到测试环境，你不再需要在连接字符串转换*Web.Production.config*转换文件。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="2f5a3-157">打开文件并删除`connectionStrings`元素。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="2f5a3-158">剩余的转换适用于`Environment`中的值`appSettings`元素和`location`限制的访问权限 Elmah 错误报告的元素。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="2f5a3-159">在创建新的发布配置文件用于生产之前，下载更新的.publishsettings 文件相同的方式更早版本中未[将部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="2f5a3-160">(在 Cytanium 控制面板中，单击**网站**，然后单击**contosouniversity.com**网站。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="2f5a3-161">选择**Web 发布**选项卡上，并依次**下载发布配置文件添加为此网站**。)您这样做的原因是以拾取.publishsettings 文件中的数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="2f5a3-162">连接字符串不可用因为仍在使用 SQL Server Compact 和尚未创建 SQL Server 数据库在 Cytanium 尚未下载该文件，第一次。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="2f5a3-163">现在你可以更新的发布配置文件和发布到生产环境。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="2f5a3-164">打开**发布 Web**向导，并切换至**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="2f5a3-165">单击**管理配置文件**，然后删除生产配置文件。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="2f5a3-166">关闭**发布 Web**向导以保存此更改。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="2f5a3-167">打开**发布 Web**再次，向导，然后依次单击**导入**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="2f5a3-168">上**连接**选项卡上，更改**目标 URL**为适当的值，如果你使用的临时的 URL。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="2f5a3-169">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-169">Click **Next**.</span></span>

<span data-ttu-id="2f5a3-170">上**设置**选项卡上，单击**启用新的数据库发布改进**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="2f5a3-171">连接字符串下拉列表中**SchoolContext**，选择 Cytanium 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="2f5a3-173">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="2f5a3-174">连接字符串下拉列表中**DefaultConnection**，选择 Cytanium 连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="2f5a3-175">选择**配置文件**选项卡上，单击**管理配置文件**，将配置文件从"contosouniversity.com-Web 部署"重命名为"生产"。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="2f5a3-176">关闭发布配置文件以保存更改，然后再次打开它。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="2f5a3-177">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-177">Click **Publish**.</span></span> <span data-ttu-id="2f5a3-178">(对于实际生产网站，会将复制*应用\_offline.htm*到生产并将置于在你的项目文件夹之前发布，然后将其删除部署完成后。)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="2f5a3-179">Visual Studio 将代码更改部署到测试环境，并打开浏览器向 Contoso 大学主页上。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="2f5a3-180">选择教师页。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-180">Select the Instructors page.</span></span>

<span data-ttu-id="2f5a3-181">Code First 迁移更新数据库相同的方式在测试环境中做过它。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="2f5a3-182">你看到植入的数据的新办公时间列。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="2f5a3-184">你现在已成功部署包含数据库更改，应用程序更新使用 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="2f5a3-185">详细信息</span><span class="sxs-lookup"><span data-stu-id="2f5a3-185">More Information</span></span>

<span data-ttu-id="2f5a3-186">这将完成这一系列的 ASP.NET web 应用程序部署到第三方托管提供商的教程。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="2f5a3-187">有关任何这些教程中所涵盖的主题的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="2f5a3-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="2f5a3-188">致谢</span><span class="sxs-lookup"><span data-stu-id="2f5a3-188">Acknowledgements</span></span>

<span data-ttu-id="2f5a3-189">我要特别感谢以下人员执行了巨大的内容的本系列教程的贡献：</span><span class="sxs-lookup"><span data-stu-id="2f5a3-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="2f5a3-190">Alberto Poblacion、 MVP &amp; MCT、 西班牙</span><span class="sxs-lookup"><span data-stu-id="2f5a3-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="2f5a3-191">Jarod Ferguson，数据平台开发 MVP，美国</span><span class="sxs-lookup"><span data-stu-id="2f5a3-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="2f5a3-192">恶劣 Mittal，Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f5a3-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="2f5a3-193">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f5a3-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="2f5a3-194">Mike Pope Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f5a3-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="2f5a3-195">Mohit Srivastava Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f5a3-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="2f5a3-196">Raffaele Rialdi，意大利</span><span class="sxs-lookup"><span data-stu-id="2f5a3-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="2f5a3-197">Rick Anderson Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f5a3-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="2f5a3-198">[Sayed Hashimi、 Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="2f5a3-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="2f5a3-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="2f5a3-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="2f5a3-200">[Scott 搜寻、 Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="2f5a3-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="2f5a3-201">Srđan Božović、 塞尔维亚共和国</span><span class="sxs-lookup"><span data-stu-id="2f5a3-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="2f5a3-202">[Vishal Joshi、 Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="2f5a3-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2f5a3-203">[上一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="2f5a3-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
