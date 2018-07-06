---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署数据库更新-9 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5edb3cae785d578674f47f1aa3d5be7dfa6a8791
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822090"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="fcc7f-103">使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署数据库更新-9 12</span><span class="sxs-lookup"><span data-stu-id="fcc7f-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>
====================
<span data-ttu-id="fcc7f-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="fcc7f-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="fcc7f-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="fcc7f-106">本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="fcc7f-107">如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="fcc7f-108">该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="fcc7f-109">显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="fcc7f-110">概述</span><span class="sxs-lookup"><span data-stu-id="fcc7f-110">Overview</span></span>

<span data-ttu-id="fcc7f-111">在本教程中，将生成数据库更改和相关的代码的更改，在 Visual Studio 中，测试所做的更改，然后将更新部署到测试和生产环境。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="fcc7f-112">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="fcc7f-113">将新列添加到表</span><span class="sxs-lookup"><span data-stu-id="fcc7f-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="fcc7f-114">在本部分中，您将添加到的出生日期列`Person`的基类`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="fcc7f-115">然后更新，以便它将显示新的列显示讲师数据的页面。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="fcc7f-116">在中*ContosoUniversity.DAL*项目中，打开*Person.cs* ，并在末尾添加以下属性`Person`类 （应两个右大括号后面）：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="fcc7f-117">接下来，更新 Seed 方法，以便它向新列提供值。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="fcc7f-118">打开*migrations\ configuration.cs*并将代码块的开始为`var instructors = new List<Instructor>`与下面的代码块，其中包括出生日期信息：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="fcc7f-119">在 ContosoUniversity 项目中，打开*Instructors.aspx*并添加新的模板字段来显示出生日期。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="fcc7f-120">将其添加之间雇佣日期和 office 分配的：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="fcc7f-121">（如果代码缩进进行同步，你可以按 CTRL-K，然后选择 CTRL-D 以便自动重新格式化该文件。）</span><span class="sxs-lookup"><span data-stu-id="fcc7f-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="fcc7f-122">生成解决方案，然后打开**程序包管理器控制台**窗口。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="fcc7f-123">请确保 ContosoUniversity.DAL 仍处于选中状态作为**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="fcc7f-124">在中**程序包管理器控制台**窗口中，选择**ContosoUniversity.DAL**作为**默认项目**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="fcc7f-125">此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`类，然后在`Up`方法您可以看到创建的新列的代码。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="fcc7f-127">生成解决方案，并输入以下命令中的**程序包管理器控制台**窗口 （请确保 ContosoUniversity.DAL 项目仍处于选中状态）：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="fcc7f-128">此命令完成后，运行该应用程序，并选择讲师页。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="fcc7f-129">当页面加载时，您看到它有新的出生日期字段。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="fcc7f-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="fcc7f-131">数据库将更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="fcc7f-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="fcc7f-132">在中**解决方案资源管理器**选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="fcc7f-133">在中**Web 单键发布**工具栏中，选择**测试**发布配置文件，然后依次**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="fcc7f-134">(如果禁用工具栏，则选择中的 ContosoUniversity 项目**解决方案资源管理器**。)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="fcc7f-135">Visual Studio 将部署更新的应用程序，并在浏览器打开到主页页面。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="fcc7f-136">运行讲师页以验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="fcc7f-137">当应用程序尝试访问此页的数据库时，Code First，更新数据库架构，并运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="fcc7f-138">显示页时，您看到的预期**出生日期**中它的日期的列。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="fcc7f-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="fcc7f-140">数据库将更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="fcc7f-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="fcc7f-141">你现在可以部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-141">You can now deploy to production.</span></span> <span data-ttu-id="fcc7f-142">唯一的区别是，将使用*应用程序\_offline.htm*以防止用户访问站点并因此更新数据库时要部署的更改。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="fcc7f-143">对于生产部署中，执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="fcc7f-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="fcc7f-144">上传*应用程序\_offline.htm*到生产站点的文件。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="fcc7f-145">在 Visual Studio 中，选择中的生产配置文件**Web 单键发布**工具栏，然后单击**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="fcc7f-146">删除*应用程序\_offline.htm*生产站点中的文件。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc7f-147">在生产环境中使用你的应用程序时，应实施备份计划。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="fcc7f-148">也就是说，你应将定期复制*学校 Prod.sdf*并*aspnet Prod.sdf*文件从生产站点到安全存储位置，并应会保持此类的多个代备份。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="fcc7f-149">更新数据库时，应进行更改之前立即从备份副本。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="fcc7f-150">然后，如果您有误并部署到生产环境后不发现它之前，您将仍将能够将数据库恢复到其损坏之前的状态。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>


<span data-ttu-id="fcc7f-151">当 Visual Studio 在浏览器中打开主页 URL*应用程序\_offline.htm*显示页。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="fcc7f-152">删除后*应用程序\_offline.htm*文件中，您可以浏览到您的主页上，以验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="fcc7f-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="fcc7f-154">现在，你已部署包含对测试和生产的数据库更改的应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="fcc7f-155">下一步的教程演示如何从 SQL Server Compact 将数据库迁移到 SQL Server Express 和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="fcc7f-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fcc7f-156">[上一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="fcc7f-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
