---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 设置联系人管理器解决方案 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何下载和配置联系人管理器解决方案，以在开发工作站上本地运行。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: e8fb24f5b2d96d864d1aa6bc0f78644773de00ab
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30881807"
---
<a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="47aa7-103">设置联系人管理器解决方案</span><span class="sxs-lookup"><span data-stu-id="47aa7-103">Setting Up the Contact Manager Solution</span></span>
====================
<span data-ttu-id="47aa7-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="47aa7-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="47aa7-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="47aa7-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="47aa7-106">本主题介绍如何下载和配置联系人管理器解决方案，以在开发工作站上本地运行。</span><span class="sxs-lookup"><span data-stu-id="47aa7-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>


## <a name="system-requirements"></a><span data-ttu-id="47aa7-107">系统要求</span><span class="sxs-lookup"><span data-stu-id="47aa7-107">System Requirements</span></span>

<span data-ttu-id="47aa7-108">若要本地运行联系人管理器解决方案并执行其他任务在本教程中所述，你将需要在你开发人员的工作站上安装此软件：</span><span class="sxs-lookup"><span data-stu-id="47aa7-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="47aa7-109">Visual Studio 2010 Service Pack 1、 Premium 或 Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="47aa7-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="47aa7-110">Internet Information Services (IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="47aa7-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="47aa7-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="47aa7-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="47aa7-112">IIS Web 部署工具 （Web 部署） 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="47aa7-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="47aa7-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="47aa7-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="47aa7-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="47aa7-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="47aa7-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="47aa7-115">.NET Framework 4</span></span>
- <span data-ttu-id="47aa7-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="47aa7-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="47aa7-117">除了 Visual Studio 2010 中，你可以下载并安装最新版本的所有这些产品和组件通过[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="47aa7-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="47aa7-118">下载并提取解决方案</span><span class="sxs-lookup"><span data-stu-id="47aa7-118">Download and Extract the Solution</span></span>

<span data-ttu-id="47aa7-119">你可以从 MSDN 代码库下载联系人管理器示例应用程序[此处](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)。</span><span class="sxs-lookup"><span data-stu-id="47aa7-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="47aa7-120">配置和运行解决方案</span><span class="sxs-lookup"><span data-stu-id="47aa7-120">Configure and Run the Solution</span></span>

<span data-ttu-id="47aa7-121">若要配置并在本地计算机上运行联系人管理器解决方案，你将需要执行以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="47aa7-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="47aa7-122">如果你没有已，请使用启用的成员资格和角色管理功能创建的本地 ASP.NET 应用程序服务数据库。</span><span class="sxs-lookup"><span data-stu-id="47aa7-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="47aa7-123">编辑连接字符串中的*web.config*文件以指向您的本地 SQL Server Express 实例。</span><span class="sxs-lookup"><span data-stu-id="47aa7-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="47aa7-124">从 Visual Studio 2010 中运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="47aa7-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="47aa7-125">本部分的其余部分提供有关如何完成上述每个任务的更多指南。</span><span class="sxs-lookup"><span data-stu-id="47aa7-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="47aa7-126">**若要创建应用程序服务数据库**</span><span class="sxs-lookup"><span data-stu-id="47aa7-126">**To create the application services database**</span></span>

1. <span data-ttu-id="47aa7-127">打开 Visual Studio 2010 命令提示符。</span><span class="sxs-lookup"><span data-stu-id="47aa7-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="47aa7-128">若要执行此操作，在**启动**菜单上，指向**所有程序**，单击**Microsoft Visual Studio 2010**，单击**Visual Studio Tools**，，然后单击**Visual Studio 命令提示 (2010)**。</span><span class="sxs-lookup"><span data-stu-id="47aa7-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="47aa7-129">在命令提示符下键入以下命令，，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="47aa7-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="47aa7-130">使用 **– C**开关来指定你的数据库服务器的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="47aa7-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="47aa7-131">使用 **–** 开关来指定应用程序服务的功能，你想要添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="47aa7-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="47aa7-132">在这种情况下， **m**指示你想要添加为成员资格提供程序的支持和**r**指示你想要添加的角色管理器的支持。</span><span class="sxs-lookup"><span data-stu-id="47aa7-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="47aa7-133">使用 **– d**开关来指定你的应用程序服务数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="47aa7-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="47aa7-134">如果省略此开关，该实用程序将使用的默认名称创建数据库**aspnetdb**。</span><span class="sxs-lookup"><span data-stu-id="47aa7-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="47aa7-135">当数据库已成功创建时，命令提示符将显示一条确认消息。</span><span class="sxs-lookup"><span data-stu-id="47aa7-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="47aa7-136">有关详细信息 aspnet\_regsql 实用程序，请参阅[ASP.NET SQL 服务器注册工具 (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="47aa7-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>


<span data-ttu-id="47aa7-137">下一步是确保联系人管理器解决方案中的连接字符串指向您的 SQL Server Express 的本地实例。</span><span class="sxs-lookup"><span data-stu-id="47aa7-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="47aa7-138">**若要更新的连接字符串**</span><span class="sxs-lookup"><span data-stu-id="47aa7-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="47aa7-139">在 Visual Studio 2010 中打开联系人管理器解决方案。</span><span class="sxs-lookup"><span data-stu-id="47aa7-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="47aa7-140">在**解决方案资源管理器**窗口中，展开**ContactManager.Mvc**项目，，然后双击**Web.config**节点。</span><span class="sxs-lookup"><span data-stu-id="47aa7-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47aa7-141">ContactManager.Mvc 项目包括两个*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="47aa7-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="47aa7-142">你需要编辑项目级文件。</span><span class="sxs-lookup"><span data-stu-id="47aa7-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="47aa7-143">在**connectionStrings**元素，验证连接字符串名为**ApplicationServices**指向您的本地 ASP.NET 应用程序服务数据库。</span><span class="sxs-lookup"><span data-stu-id="47aa7-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="47aa7-144">在**解决方案资源管理器**窗口中，展开**ContactManager.Service**项目，，然后双击**Web.config**节点。</span><span class="sxs-lookup"><span data-stu-id="47aa7-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="47aa7-145">在**connectionStrings**名为的连接字符串中的元素， **ContactManagerContext**，验证**数据源**属性设置为您的本地实例的 SQLServer Express。</span><span class="sxs-lookup"><span data-stu-id="47aa7-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="47aa7-146">你不需要更改连接字符串中的其他部分。</span><span class="sxs-lookup"><span data-stu-id="47aa7-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="47aa7-147">保存所有打开的文件。</span><span class="sxs-lookup"><span data-stu-id="47aa7-147">Save all open files.</span></span>

<span data-ttu-id="47aa7-148">现在，你应该已准备好在你的本地计算机上运行联系人管理器解决方案。</span><span class="sxs-lookup"><span data-stu-id="47aa7-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="47aa7-149">如果你按照这些步骤而不必首先创建应用程序服务数据库时，ASP.NET 将尝试创建一个用户首次创建数据库。</span><span class="sxs-lookup"><span data-stu-id="47aa7-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="47aa7-150">但是，手动创建数据库为你提供大量更好地控制你想要支持的应用程序服务功能集。</span><span class="sxs-lookup"><span data-stu-id="47aa7-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>


<span data-ttu-id="47aa7-151">**运行该联系人管理器解决方案**</span><span class="sxs-lookup"><span data-stu-id="47aa7-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="47aa7-152">在 Visual Studio 2010 中，按 F5。</span><span class="sxs-lookup"><span data-stu-id="47aa7-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="47aa7-153">Internet Explorer 启动并请求联系人管理器 ASP.NET MVC 3 应用程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="47aa7-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="47aa7-154">默认情况下，应用程序将显示**所有联系人**页。</span><span class="sxs-lookup"><span data-stu-id="47aa7-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="47aa7-155">添加几个联系人，并验证应用程序按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="47aa7-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="47aa7-156">浏览到`http://localhost:50114/Account/Register`（如果您正在托管不同的端口上的应用程序，则调整 URL）。</span><span class="sxs-lookup"><span data-stu-id="47aa7-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="47aa7-157">添加用户名称、 电子邮件地址和密码，并验证你已能够成功注册一个帐户。</span><span class="sxs-lookup"><span data-stu-id="47aa7-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="47aa7-158">浏览到`http://localhost:50114/Account/LogOn`（如果您正在托管不同的端口上的应用程序，则调整 URL）。</span><span class="sxs-lookup"><span data-stu-id="47aa7-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="47aa7-159">会验证您能够使用你刚刚创建的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="47aa7-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="47aa7-160">关闭 Internet Explorer 来停止调试。</span><span class="sxs-lookup"><span data-stu-id="47aa7-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="47aa7-161">结束语</span><span class="sxs-lookup"><span data-stu-id="47aa7-161">Conclusion</span></span>

<span data-ttu-id="47aa7-162">此时，应完全配置联系人管理器解决方案为本地计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="47aa7-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="47aa7-163">在本教程中处理通过其他主题时，可用作参考解决方案。</span><span class="sxs-lookup"><span data-stu-id="47aa7-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="47aa7-164">下一主题[了解项目文件](understanding-the-project-file.md)，说明如何使用联系人管理器解决方案中的自定义 Microsoft Build Engine (MSBuild) 项目文件来控制部署过程。</span><span class="sxs-lookup"><span data-stu-id="47aa7-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="47aa7-165">[上一页](the-contact-manager-solution.md)
> [下一页](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="47aa7-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
