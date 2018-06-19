---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署某一数据库更新 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 3020cfa19bf12f21c6d42a77ed257595431b4e86
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892616"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="6a4f7-103">使用 Visual Studio 的 ASP.NET Web 部署： 部署某一数据库更新</span><span class="sxs-lookup"><span data-stu-id="6a4f7-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>
====================
<span data-ttu-id="6a4f7-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6a4f7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="6a4f7-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="6a4f7-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="6a4f7-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="6a4f7-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="6a4f7-108">概述</span><span class="sxs-lookup"><span data-stu-id="6a4f7-108">Overview</span></span>

<span data-ttu-id="6a4f7-109">在本教程中，使数据库更改和相关的代码的更改，在 Visual Studio 中，测试所做的更改，然后将更新部署到测试、 过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="6a4f7-110">本教程首先演示如何更新管理的 Code First 迁移的数据库，然后更高版本显示如何通过使用 dbDacFx 提供程序更新数据库。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="6a4f7-111">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="6a4f7-112">将数据库更新部署通过使用 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="6a4f7-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="6a4f7-113">在本部分中，你添加的出生日期列`Person`基类`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="6a4f7-114">然后你将更新，使其显示新的列显示教师数据的页。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="6a4f7-115">最后，将所做的更改部署到测试、 过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="6a4f7-116">向应用程序数据库的表中添加列</span><span class="sxs-lookup"><span data-stu-id="6a4f7-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="6a4f7-117">在*ContosoUniversity.DAL*项目中，打开*Person.cs* ，并在末尾添加以下属性`Person`（应两个关闭跟在它后面的大括号） 的类：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="6a4f7-118">接下来，更新`Seed`方法，以便它提供的新列的值。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="6a4f7-119">打开*Migrations\Configuration.cs* ，并将开始的代码块`var instructors = new List<Instructor>`与下面的代码块，其中包括出生日期信息：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="6a4f7-120">生成解决方案，，然后打开**程序包管理器控制台**窗口。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="6a4f7-121">请确保 ContosoUniversity.DAL 仍处于选中状态作为**默认项目**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="6a4f7-122">在**程序包管理器控制台**窗口中，选择**ContosoUniversity.DAL**作为**默认项目**，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="6a4f7-123">此命令完成时，Visual Studio 将打开定义新的类文件`DbMIgration`类，然后在`Up`方法你可以看到创建的新列的代码。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="6a4f7-124">`Up`方法实现此更改，请时创建列和`Down`方法删除列时您正在回滚更改。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="6a4f7-126">生成解决方案，，然后输入以下命令包含在**程序包管理器控制台**窗口 （请确保 ContosoUniversity.DAL 项目仍处于选中状态）：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="6a4f7-127">实体框架运行`Up`方法，然后运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="6a4f7-128">在教师页中显示新的列</span><span class="sxs-lookup"><span data-stu-id="6a4f7-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="6a4f7-129">在 ContosoUniversity 项目中，打开*Instructors.aspx*并添加一个新的模板字段来显示出生日期。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="6a4f7-130">将其添加之间对雇佣日期和 office 分配：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="6a4f7-131">（如果代码缩进获取同步的你可以按 CTRL K，然后选择 CTRL D 自动重新设置格式的文件。）</span><span class="sxs-lookup"><span data-stu-id="6a4f7-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="6a4f7-132">运行应用程序，然后单击**教师**链接。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="6a4f7-133">在页面加载后，你看到它具有新出生日期字段。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![出生日期教师页](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="6a4f7-135">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="6a4f7-136">将数据库更新部署</span><span class="sxs-lookup"><span data-stu-id="6a4f7-136">Deploy the database update</span></span>

1. <span data-ttu-id="6a4f7-137">在**解决方案资源管理器**选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="6a4f7-138">在**Web 单键发布**工具栏上，单击**测试**发布配置文件，并依次**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="6a4f7-139">(如果禁用了工具栏上，选择中的 ContosoUniversity 项目**解决方案资源管理器**。)</span><span class="sxs-lookup"><span data-stu-id="6a4f7-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="6a4f7-140">Visual Studio 将部署更新的应用程序，并浏览器打开到主页。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="6a4f7-141">运行**教师**页后，可以验证更新是否成功部署。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="6a4f7-142">当应用程序尝试访问此页的数据库时，Code First，更新数据库架构，并运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="6a4f7-143">显示页时，你看到预期**出生日期**与在其中的日期的列。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="6a4f7-144">在**Web 单键发布**工具栏上，单击**过渡**发布配置文件，并依次**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="6a4f7-145">运行**教师**中将临时以验证更新是否成功部署中的页。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="6a4f7-146">在**Web 单键发布**工具栏上，单击**生产**发布配置文件，并依次**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="6a4f7-147">运行**教师**在生产环境以验证更新是否成功部署中的页。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="6a4f7-148">对于包括数据库更改的实际生产应用程序更新你通过使用通常还需要在部署过程中，脱机应用*应用\_offline.htm*，如你在前面的教程中看到。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="6a4f7-149">将数据库更新部署使用 dbDacFx 提供程序</span><span class="sxs-lookup"><span data-stu-id="6a4f7-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="6a4f7-150">在本部分中，你添加*注释*列*用户*表中成员资格数据库并创建一个页，可以显示并编辑每个用户的注释。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="6a4f7-151">然后将所做的更改部署到测试、 过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="6a4f7-152">向成员资格数据库中的表中添加列</span><span class="sxs-lookup"><span data-stu-id="6a4f7-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="6a4f7-153">在 Visual Studio 中，打开**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="6a4f7-154">展开 **(localdb) \v11.0**，展开**数据库**，展开**aspnet ContosoUniversity** (不**aspnet ContosoUniversity Prod**)然后展开**表**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="6a4f7-155">如果看不到 **(localdb) \v11.0**下**SQL Server**节点，右键单击**SQL Server**节点，然后单击**添加 SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="6a4f7-156">在**连接到服务器**对话框中，输入 *(localdb) \v11.0*作为**服务器名称**，然后单击**连接**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="6a4f7-157">如果看不到**aspnet ContosoUniversity**、 运行该项目并使用登录*管理员*凭据 (密码*devpwd*)，然后刷新**SQL Server 对象资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="6a4f7-158">右键单击**用户**表，并依次**视图设计器**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX 视图设计器](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="6a4f7-160">在设计器中，添加*注释*列并使其*nvarchar （128)* 和可以为 null，然后单击**更新**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![添加注释列](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="6a4f7-162">在**预览数据库更新**框中，单击**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![预览数据库更新](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="6a4f7-164">创建页，以显示和编辑新的列</span><span class="sxs-lookup"><span data-stu-id="6a4f7-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="6a4f7-165">在**解决方案资源管理器**，右键单击**帐户**ContosoUniversity 项目中的文件夹，请单击**添加**，然后单击**新项**.</span><span class="sxs-lookup"><span data-stu-id="6a4f7-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="6a4f7-166">创建一个新**Web 窗体使用母版页**并将其命名*UserInfo.aspx*。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="6a4f7-167">接受默认值*Site.Master*作为主控页文件。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="6a4f7-168">将复制到以下标记`MainContent``Content`元素 (3 的最后一个`Content`元素):</span><span class="sxs-lookup"><span data-stu-id="6a4f7-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="6a4f7-169">右键单击*UserInfo.aspx*页上，单击**用浏览器查看**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="6a4f7-170">登录你*管理员*用户凭据 (密码*devpwd*) 并将注释添加到用户以验证页是否工作正常。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![UserInfo 页](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="6a4f7-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="6a4f7-173">将数据库更新部署</span><span class="sxs-lookup"><span data-stu-id="6a4f7-173">Deploy the database update</span></span>

<span data-ttu-id="6a4f7-174">若要部署使用 dbDacFx 提供程序，只需选择**更新数据库**发布配置文件中的选项。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="6a4f7-175">但是，对于初始部署使用此选项时你还配置一些其他的 SQL 脚本，运行： 这种仍在配置文件和你需要防止其再次运行。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="6a4f7-176">打开**发布 Web**向导通过右键单击 ContosoUniversity 项目并单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="6a4f7-177">选择**测试**配置文件。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="6a4f7-178">单击**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="6a4f7-179">下**DefaultConnection**，选择**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="6a4f7-180">禁用配置为用于初始部署运行其他脚本：</span><span class="sxs-lookup"><span data-stu-id="6a4f7-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="6a4f7-181">单击**配置数据库更新**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="6a4f7-182">在**配置数据库更新**对话框中，清除的复选框旁边*Grant.sql*和*aspnet 数据 dev.sql*。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="6a4f7-183">单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-183">Click **Close**.</span></span>
6. <span data-ttu-id="6a4f7-184">单击**预览**选项卡。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="6a4f7-185">下**数据库**和右侧的**DefaultConnection**，单击**预览版数据库**链接。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![数据库预览](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="6a4f7-187">预览窗口显示将在要使该数据库架构与源数据库的架构匹配的目标数据库中运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="6a4f7-188">该脚本包含的 ALTER TABLE 命令时，添加新列。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="6a4f7-189">关闭**Database 预览版**对话框中，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="6a4f7-190">Visual Studio 将部署更新的应用程序，并浏览器打开到主页。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="6a4f7-191">运行 UserInfo 页 (添加*Account/UserInfo.aspx*到主页 URL) 以验证更新是否成功部署。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="6a4f7-192">你将需要输入登录*管理员*和*devpwd*。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="6a4f7-193">默认情况下，不部署表中的数据和未配置数据部署脚本来运行，因此，您不会发现你在开发中添加注释。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="6a4f7-194">你可以在暂存以验证已部署到数据库中更改，而该页运行正确现在添加新的注释。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="6a4f7-195">请按照相同的过程来将部署到过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="6a4f7-196">不要忘记禁用额外的脚本。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="6a4f7-197">相比测试配置文件的唯一区别是，将禁用只有一个脚本在过渡和生产配置文件，因为它们已配置为仅运行*aspnet prod data.sql*。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="6a4f7-198">过渡和生产的凭据是管理员和 prodpwd。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="6a4f7-199">包括数据库更改的实际生产应用程序更新为您通常也将进行应用程序脱机在部署过程中通过上载*应用\_offline.htm*之前发布，将其删除此后，正如你在看到[以前一教程](deploying-a-code-update.md)。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="6a4f7-200">总结</span><span class="sxs-lookup"><span data-stu-id="6a4f7-200">Summary</span></span>

<span data-ttu-id="6a4f7-201">现在，你已部署包含使用 Code First 迁移和 dbDacFx 提供程序的数据库更改的应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![出生日期教师页](deploying-a-database-update/_static/image8.png)

![UserInfo 页](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="6a4f7-204">下一教程演示如何通过使用命令行执行部署。</span><span class="sxs-lookup"><span data-stu-id="6a4f7-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6a4f7-205">[上一页](deploying-a-code-update.md)
> [下一页](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="6a4f7-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
