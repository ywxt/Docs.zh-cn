---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 设置 Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何下载和配置 Contact Manager 解决方案开发人员工作站上本地运行。
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 479dbb8d2edbe9fb953ea9e1312ffb8fdbd3e2fe
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802126"
---
<a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="41311-103">设置 Contact Manager 解决方案</span><span class="sxs-lookup"><span data-stu-id="41311-103">Setting Up the Contact Manager Solution</span></span>
====================
<span data-ttu-id="41311-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="41311-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="41311-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="41311-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="41311-106">本主题介绍如何下载和配置 Contact Manager 解决方案开发人员工作站上本地运行。</span><span class="sxs-lookup"><span data-stu-id="41311-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>


## <a name="system-requirements"></a><span data-ttu-id="41311-107">系统要求</span><span class="sxs-lookup"><span data-stu-id="41311-107">System Requirements</span></span>

<span data-ttu-id="41311-108">若要在本地运行 Contact Manager 解决方案并执行其他任务在本教程中所述，你将需要开发人员工作站上安装此软件：</span><span class="sxs-lookup"><span data-stu-id="41311-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="41311-109">Visual Studio 2010 Service Pack 1、 Premium 或 Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="41311-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="41311-110">Internet 信息服务 (IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="41311-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="41311-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="41311-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="41311-112">IIS Web 部署工具 （Web 部署） 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="41311-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="41311-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="41311-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="41311-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="41311-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="41311-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="41311-115">.NET Framework 4</span></span>
- <span data-ttu-id="41311-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="41311-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="41311-117">除了 Visual Studio 2010 中，您可以下载并安装最新版本的所有这些产品和组件[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="41311-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="41311-118">下载并提取解决方案</span><span class="sxs-lookup"><span data-stu-id="41311-118">Download and Extract the Solution</span></span>

<span data-ttu-id="41311-119">您可以从 MSDN 代码库下载联系人管理器示例应用程序[此处](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)。</span><span class="sxs-lookup"><span data-stu-id="41311-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="41311-120">配置和运行解决方案</span><span class="sxs-lookup"><span data-stu-id="41311-120">Configure and Run the Solution</span></span>

<span data-ttu-id="41311-121">若要配置并在本地计算机上运行 Contact Manager 解决方案，你将需要执行以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="41311-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="41311-122">如果你还没有，请使用启用的成员资格和角色管理功能创建本地 ASP.NET 应用程序服务数据库。</span><span class="sxs-lookup"><span data-stu-id="41311-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="41311-123">编辑中的连接字符串*web.config*文件以指向本地 SQL Server Express 实例。</span><span class="sxs-lookup"><span data-stu-id="41311-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="41311-124">从 Visual Studio 2010 运行解决方案。</span><span class="sxs-lookup"><span data-stu-id="41311-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="41311-125">本部分的其余部分提供有关如何完成这些任务的更多指导。</span><span class="sxs-lookup"><span data-stu-id="41311-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="41311-126">**若要创建应用程序服务数据库**</span><span class="sxs-lookup"><span data-stu-id="41311-126">**To create the application services database**</span></span>

1. <span data-ttu-id="41311-127">打开 Visual Studio 2010 命令提示符。</span><span class="sxs-lookup"><span data-stu-id="41311-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="41311-128">为此，请在**启动**菜单，依次指向**所有程序**，单击**Microsoft Visual Studio 2010**，单击**Visual Studio Tools**，，然后单击**Visual Studio 命令提示符 (2010)**。</span><span class="sxs-lookup"><span data-stu-id="41311-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="41311-129">在命令提示符下，键入以下命令，并按 Enter:</span><span class="sxs-lookup"><span data-stu-id="41311-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="41311-130">使用 **– C**开关来指定你的数据库服务器的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="41311-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="41311-131">使用 **– A**开关来指定应用程序服务想要向数据库添加的功能。</span><span class="sxs-lookup"><span data-stu-id="41311-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="41311-132">在这种情况下， **m**指示你想要添加的成员资格提供程序支持并**r**指示你想要添加对角色管理器的支持。</span><span class="sxs-lookup"><span data-stu-id="41311-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="41311-133">使用 **– d**开关来指定你的应用程序服务数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="41311-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="41311-134">如果省略此开关，该实用工具将使用的默认名称创建数据库**aspnetdb**。</span><span class="sxs-lookup"><span data-stu-id="41311-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="41311-135">已成功创建数据库，命令提示符会显示一条确认消息。</span><span class="sxs-lookup"><span data-stu-id="41311-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="41311-136">有关详细信息 aspnet\_regsql 实用程序，请参阅[ASP.NET SQL Server 注册工具 (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="41311-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>


<span data-ttu-id="41311-137">下一步是确保 Contact Manager 解决方案中的连接字符串指向 SQL Server Express 的本地实例。</span><span class="sxs-lookup"><span data-stu-id="41311-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="41311-138">**若要更新连接字符串**</span><span class="sxs-lookup"><span data-stu-id="41311-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="41311-139">在 Visual Studio 2010 中打开 Contact Manager 解决方案。</span><span class="sxs-lookup"><span data-stu-id="41311-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="41311-140">在中**解决方案资源管理器**窗口中，展开**ContactManager.Mvc**项目，然后再双击**Web.config**节点。</span><span class="sxs-lookup"><span data-stu-id="41311-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41311-141">ContactManager.Mvc 项目包含两个*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="41311-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="41311-142">您需要编辑项目级文件。</span><span class="sxs-lookup"><span data-stu-id="41311-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="41311-143">在中**connectionStrings**元素中，验证连接字符串指定**ApplicationServices**指向您的本地 ASP.NET 应用程序服务数据库。</span><span class="sxs-lookup"><span data-stu-id="41311-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="41311-144">在中**解决方案资源管理器**窗口中，展开**ContactManager.Service**项目，然后再双击**Web.config**节点。</span><span class="sxs-lookup"><span data-stu-id="41311-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="41311-145">在**connectionStrings**元素，在名为的连接字符串**ContactManagerContext**，验证**数据源**属性设置为本地的 SQL 实例Server Express。</span><span class="sxs-lookup"><span data-stu-id="41311-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="41311-146">不需要更改连接字符串中的其他部分。</span><span class="sxs-lookup"><span data-stu-id="41311-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="41311-147">保存所有打开的文件。</span><span class="sxs-lookup"><span data-stu-id="41311-147">Save all open files.</span></span>

<span data-ttu-id="41311-148">现在，应准备好在本地计算机上运行 Contact Manager 解决方案。</span><span class="sxs-lookup"><span data-stu-id="41311-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="41311-149">如果按照这些步骤操作无需首先创建应用程序服务数据库，ASP.NET 将尝试创建一个用户首次创建数据库。</span><span class="sxs-lookup"><span data-stu-id="41311-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="41311-150">但是，手动创建数据库用户可更多地掌控你想要支持的应用程序服务功能集。</span><span class="sxs-lookup"><span data-stu-id="41311-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>


<span data-ttu-id="41311-151">**若要运行 Contact Manager 解决方案**</span><span class="sxs-lookup"><span data-stu-id="41311-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="41311-152">在 Visual Studio 2010 中，按 F5。</span><span class="sxs-lookup"><span data-stu-id="41311-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="41311-153">Internet Explorer 启动，并请求联系人管理器 ASP.NET MVC 3 应用程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="41311-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="41311-154">默认情况下，应用程序将显示**所有联系人**页。</span><span class="sxs-lookup"><span data-stu-id="41311-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="41311-155">添加几个联系人，并验证该应用程序按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="41311-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="41311-156">浏览到`http://localhost:50114/Account/Register`（如果您正在托管不同的端口上的应用程序，则调整 URL）。</span><span class="sxs-lookup"><span data-stu-id="41311-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="41311-157">添加用户名、 电子邮件地址和密码，并验证您能够成功注册一个帐户。</span><span class="sxs-lookup"><span data-stu-id="41311-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="41311-158">浏览到`http://localhost:50114/Account/LogOn`（如果您正在托管不同的端口上的应用程序，则调整 URL）。</span><span class="sxs-lookup"><span data-stu-id="41311-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="41311-159">验证您可以使用刚刚创建的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="41311-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="41311-160">关闭 Internet Explorer 以停止调试。</span><span class="sxs-lookup"><span data-stu-id="41311-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="41311-161">结束语</span><span class="sxs-lookup"><span data-stu-id="41311-161">Conclusion</span></span>

<span data-ttu-id="41311-162">此时，应完全配置 Contact Manager 解决方案为在本地计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="41311-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="41311-163">在本教程中处理通过其他主题时，可以使用该解决方案作为参考。</span><span class="sxs-lookup"><span data-stu-id="41311-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="41311-164">下一主题[了解项目文件](understanding-the-project-file.md)，介绍了如何使用 Contact Manager 解决方案中的自定义 Microsoft Build Engine (MSBuild) 项目文件来控制部署过程。</span><span class="sxs-lookup"><span data-stu-id="41311-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="41311-165">[上一页](the-contact-manager-solution.md)
> [下一页](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="41311-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
