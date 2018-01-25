---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: "部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 作为测试环境-5 12，将部署到 IIS |Microsoft 文档"
author: tdykstra
description: "这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Stu 包含 SQL Server Compact 数据库..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: a7995844ee6ed19efa130c4f6c019214d6652ea7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a><span data-ttu-id="644e9-103">部署具有 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 的 ASP.NET Web 应用程序： 作为测试环境-5 12，将部署到 IIS</span><span class="sxs-lookup"><span data-stu-id="644e9-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying to IIS as a Test Environment - 5 of 12</span></span>
====================
<span data-ttu-id="644e9-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="644e9-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="644e9-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="644e9-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="644e9-106">这一系列的教程演示如何部署 （发布） ASP.NET web 应用程序项目，它通过使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 中包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="644e9-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="644e9-107">如果你安装 Web 发布更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="644e9-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="644e9-108">有关序列的简介，请参阅[序列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="644e9-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="644e9-109">显示部署功能后，将 Visual Studio 2012 RC 版本中推出，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Azure App Service Web Apps 的教程，请参阅[的 ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="644e9-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="644e9-110">概述</span><span class="sxs-lookup"><span data-stu-id="644e9-110">Overview</span></span>

<span data-ttu-id="644e9-111">本教程演示如何部署到 IIS 在本地计算机上的 ASP.NET web 应用。</span><span class="sxs-lookup"><span data-stu-id="644e9-111">This tutorial shows how to deploy an ASP.NET web application to IIS on the local computer.</span></span>

<span data-ttu-id="644e9-112">当你开发应用程序时，你通常测试通过在 Visual Studio 中运行它。</span><span class="sxs-lookup"><span data-stu-id="644e9-112">When you develop an application, you generally test by running it in Visual Studio.</span></span> <span data-ttu-id="644e9-113">默认情况下，这意味着你要使用 Visual Studio 开发服务器 (也称为 Cassini)。</span><span class="sxs-lookup"><span data-stu-id="644e9-113">By default, this means you're using the Visual Studio Development Server (also known as Cassini).</span></span> <span data-ttu-id="644e9-114">Visual Studio 开发服务器，可以轻松地在 Visual Studio 中开发期间测试，但它不与 IIS 的完全一样工作。</span><span class="sxs-lookup"><span data-stu-id="644e9-114">The Visual Studio Development Server makes it easy to test during development in Visual Studio, but it doesn't work exactly like IIS.</span></span> <span data-ttu-id="644e9-115">因此，很可能，当应用程序在 Visual Studio 中，对其进行测试，但在到 IIS 部署在托管环境中时失败时，将正确运行。</span><span class="sxs-lookup"><span data-stu-id="644e9-115">As a result, it's possible that an application will run correctly when you test it in Visual Studio, but fail when it's deployed to IIS in a hosting environment.</span></span>

<span data-ttu-id="644e9-116">你可以通过以下方式更可靠地测试你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="644e9-116">You can test your application more reliably in these ways:</span></span>

1. <span data-ttu-id="644e9-117">使用 IIS Express 或完整 IIS 而不是 Visual Studio 开发服务器时在 Visual Studio 中测试在开发过程。</span><span class="sxs-lookup"><span data-stu-id="644e9-117">Use IIS Express or full IIS instead of the Visual Studio Development Server when you test in Visual Studio during development.</span></span> <span data-ttu-id="644e9-118">此方法通常会模拟更准确地在 IIS 下运行你的站点将如何。</span><span class="sxs-lookup"><span data-stu-id="644e9-118">This method generally emulates more accurately how your site will run under IIS.</span></span> <span data-ttu-id="644e9-119">但是，此方法不测试您的部署过程或验证部署过程的结果都会正常运行。</span><span class="sxs-lookup"><span data-stu-id="644e9-119">However, this method does not test your deployment process or validate that the result of the deployment process will run correctly.</span></span>
2. <span data-ttu-id="644e9-120">通过使用相同的过程，你将使用更高版本来将其部署到生产环境部署到 IIS 开发计算机上的应用程序。</span><span class="sxs-lookup"><span data-stu-id="644e9-120">Deploy the application to IIS on your development computer by using the same process that you'll use later to deploy it to your production environment.</span></span> <span data-ttu-id="644e9-121">此方法验证除了验证你在 IIS 下将正确运行你的应用程序的部署过程。</span><span class="sxs-lookup"><span data-stu-id="644e9-121">This method validates your deployment process in addition to validating that your application will run correctly under IIS.</span></span>
3. <span data-ttu-id="644e9-122">将应用部署到尽可能接近于生产环境的测试环境。</span><span class="sxs-lookup"><span data-stu-id="644e9-122">Deploy the application to a test environment that is as close as possible to your production environment.</span></span> <span data-ttu-id="644e9-123">由于这些教程的生产环境是第三方托管提供商，理想的测试环境将具有托管提供商的第二个帐户。</span><span class="sxs-lookup"><span data-stu-id="644e9-123">Since the production environment for these tutorials is a third-party hosting provider, the ideal test environment would be a second account with the hosting provider.</span></span> <span data-ttu-id="644e9-124">你将此第二个帐户仅用于测试，但将其设置与生产帐户相同的方式。</span><span class="sxs-lookup"><span data-stu-id="644e9-124">You would use this second account only for testing, but it would be set up the same way as the production account.</span></span>

<span data-ttu-id="644e9-125">本教程演示选项 2 的步骤。</span><span class="sxs-lookup"><span data-stu-id="644e9-125">This tutorial shows the steps for option 2.</span></span> <span data-ttu-id="644e9-126">选项 3 指南提供在末尾[将部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中，并且在本教程末尾有用于选项 1 的资源链接。</span><span class="sxs-lookup"><span data-stu-id="644e9-126">Guidance for option 3 is provided at the end of the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, and at the end of this tutorial there are links to resources for option 1.</span></span>

<span data-ttu-id="644e9-127">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="644e9-127">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="configuring-the-application-to-run-in-medium-trust"></a><span data-ttu-id="644e9-128">在中等信任配置为运行该应用程序</span><span class="sxs-lookup"><span data-stu-id="644e9-128">Configuring the Application to Run in Medium Trust</span></span>

<span data-ttu-id="644e9-129">在安装 IIS 并部署到它之前, 将以便站点运行更像它在典型的共享宿主环境中将更改 Web.config 文件设置。</span><span class="sxs-lookup"><span data-stu-id="644e9-129">Before installing IIS and deploying to it, you'll change a Web.config file setting in order to make the site run more like it will in a typical shared hosting environment.</span></span>

<span data-ttu-id="644e9-130">托管提供商通常在运行您的网站*中等信任*，这意味着它不允许执行几项内容。</span><span class="sxs-lookup"><span data-stu-id="644e9-130">Hosting providers typically run your web site in *medium trust*, which means there are some things it is not allowed to do.</span></span> <span data-ttu-id="644e9-131">例如，应用程序代码不能访问 Windows 注册表和无法读取或写入应用程序的文件夹层次结构之外的文件。</span><span class="sxs-lookup"><span data-stu-id="644e9-131">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="644e9-132">默认情况下你的应用程序运行*高度信任*在本地计算机，这意味着应用程序可能能够执行时将其部署到生产环境将失败的操作。</span><span class="sxs-lookup"><span data-stu-id="644e9-132">By default your application runs in *high trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span> <span data-ttu-id="644e9-133">因此，若要使测试环境的详细信息准确地反映生产环境，你将配置要在中等信任中运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="644e9-133">Therefore, to make the test environment more accurately reflect the production environment, you'll configure the application to run in medium trust.</span></span>

<span data-ttu-id="644e9-134">在应用程序 Web.config 文件中，添加**信任**中的元素**system.web**元素，如本示例中所示。</span><span class="sxs-lookup"><span data-stu-id="644e9-134">In the application Web.config file, add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

<span data-ttu-id="644e9-135">即使在本地计算机上，现在在 IIS 中的中级信任应用程序将运行。</span><span class="sxs-lookup"><span data-stu-id="644e9-135">The application will now run in medium trust in IIS even on your local computer.</span></span> <span data-ttu-id="644e9-136">此设置可由应用程序代码以执行其他操作会导致生产失败尽早捕获任何尝试。</span><span class="sxs-lookup"><span data-stu-id="644e9-136">This setting enables you to catch as early as possible any attempts by application code to do something that would fail in production.</span></span>

> [!NOTE]
> <span data-ttu-id="644e9-137">如果使用 Entity Framework Code First 迁移，请确保您拥有版本 5.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="644e9-137">If you are using Entity Framework Code First Migrations, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="644e9-138">在实体框架版本 4.3，迁移以更新数据库架构需要完全信任。</span><span class="sxs-lookup"><span data-stu-id="644e9-138">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>


## <a name="installing-iis-and-web-deploy"></a><span data-ttu-id="644e9-139">安装 IIS 和 Web 部署</span><span class="sxs-lookup"><span data-stu-id="644e9-139">Installing IIS and Web Deploy</span></span>

<span data-ttu-id="644e9-140">若要将部署到 IIS 在开发计算机上，你必须 IIS 和 Web 部署安装。</span><span class="sxs-lookup"><span data-stu-id="644e9-140">To deploy to IIS on your development computer, you must have IIS and Web Deploy installed.</span></span> <span data-ttu-id="644e9-141">此外，默认 Windows 7 配置中不会包含这些信息。</span><span class="sxs-lookup"><span data-stu-id="644e9-141">These are not included in the default Windows 7 configuration.</span></span> <span data-ttu-id="644e9-142">如果你已经安装了 IIS 和 Web 部署，请跳至下一节。</span><span class="sxs-lookup"><span data-stu-id="644e9-142">If you have already installed both IIS and Web Deploy, skip to the next section.</span></span>

<span data-ttu-id="644e9-143">使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是首选的方法来安装 IIS 和 Web 部署，因为 Web 平台安装程序的 IIS 安装推荐的配置，并自动安装 IIS 和 Web 的先决条件如有必要部署。</span><span class="sxs-lookup"><span data-stu-id="644e9-143">Using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) is the preferred way to install IIS and Web Deploy, because the Web Platform Installer installs a recommended configuration for IIS and it automatically installs the prerequisites for IIS and Web Deploy if necessary.</span></span>

<span data-ttu-id="644e9-144">若要运行 Web 平台安装程序安装 IIS 和 Web 部署，请使用以下链接。</span><span class="sxs-lookup"><span data-stu-id="644e9-144">To run Web Platform Installer to install IIS and Web Deploy, use the following link.</span></span> <span data-ttu-id="644e9-145">如果你已安装 IIS、 Web 部署或任何其所需的组件，Web 平台安装程序仅安装功能丢失。</span><span class="sxs-lookup"><span data-stu-id="644e9-145">If you already have installed IIS, Web Deploy or any of their required components, the Web Platform Installer installs only what is missing.</span></span>

- [<span data-ttu-id="644e9-146">安装 IIS 和 Web 部署使用 WebPI</span><span class="sxs-lookup"><span data-stu-id="644e9-146">Install IIS and Web Deploy using WebPI</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a><span data-ttu-id="644e9-147">将默认应用程序池设置为.NET 4</span><span class="sxs-lookup"><span data-stu-id="644e9-147">Setting the Default Application Pool to .NET 4</span></span>

<span data-ttu-id="644e9-148">安装 IIS 后，运行**IIS 管理器**若要确保.NET Framework 版本 4 分配给默认应用程序池。</span><span class="sxs-lookup"><span data-stu-id="644e9-148">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

<span data-ttu-id="644e9-149">从 Windows**启动**菜单上，选择**运行**，输入"inetmgr"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="644e9-149">From the Windows **Start** menu, select **Run**, enter "inetmgr", and then click **OK**.</span></span> <span data-ttu-id="644e9-150">(如果**运行**命令将不在你**启动**菜单上，你可以按 Windows 键和 R，以将其打开。</span><span class="sxs-lookup"><span data-stu-id="644e9-150">(If the **Run** command is not in your **Start** menu, you can press the Windows Key and R to open it.</span></span> <span data-ttu-id="644e9-151">或右键单击任务栏中，单击**属性**，选择**开始菜单**选项卡上，单击**自定义**，然后选择**运行命令**。)</span><span class="sxs-lookup"><span data-stu-id="644e9-151">Or right-click the taskbar, click **Properties**, select the **Start Menu** tab, click **Customize**, and select **Run command**.)</span></span>

<span data-ttu-id="644e9-152">在**连接**窗格中，展开服务器节点，然后选择**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="644e9-152">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="644e9-153">在**应用程序池**窗格中，如果**DefaultAppPool**是分配给.NET framework 版本 4，如下图所示，跳到下一节。</span><span class="sxs-lookup"><span data-stu-id="644e9-153">In the **Application Pools** pane, if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

<span data-ttu-id="644e9-154">[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-154">[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)</span></span>

<span data-ttu-id="644e9-155">如果你看到只有两个应用程序池，并且这两个设置为.NET Framework 2.0，你必须安装在 IIS 中的 ASP.NET 4:</span><span class="sxs-lookup"><span data-stu-id="644e9-155">If you see only two application pools and both of them are set to the .NET Framework 2.0, you have to install ASP.NET 4 in IIS:</span></span>

- <span data-ttu-id="644e9-156">通过右键单击打开命令提示符窗口**命令提示符**中 Windows**启动**菜单并选择**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="644e9-156">Open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="644e9-157">然后运行[aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中，使用以下命令安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="644e9-157">Then run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS, using the following commands.</span></span> <span data-ttu-id="644e9-158">（在 64 位系统中，替换与"Framework64"的"Framework"。）</span><span class="sxs-lookup"><span data-stu-id="644e9-158">(In 64-bit systems, replace "Framework" with "Framework64".)</span></span>

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    <span data-ttu-id="644e9-159">[![aspnet_regiis_installing_ASP.NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-159">[![aspnet_regiis_installing_ASP.NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)</span></span>

    <span data-ttu-id="644e9-160">此命令为.NET Framework 4 中，创建新的应用程序池，但默认应用程序池将仍设置为 2.0。</span><span class="sxs-lookup"><span data-stu-id="644e9-160">This command creates new application pools for the .NET Framework 4, but the default application pool will still be set to 2.0.</span></span> <span data-ttu-id="644e9-161">您要部署应用程序面向.NET 4 到该应用程序池，因此你需要为.NET 4 中更改应用程序池。</span><span class="sxs-lookup"><span data-stu-id="644e9-161">You'll be deploying an application that targets .NET 4 to that application pool, so you have to change the application pool to .NET 4.</span></span>

<span data-ttu-id="644e9-162">如果您关闭**IIS 管理器**，再次运行，展开服务器节点中，，再单击**应用程序池**以显示**应用程序池**再次窗格。</span><span class="sxs-lookup"><span data-stu-id="644e9-162">If you closed **IIS Manager**, run it again, expand the server node, and click **Application Pools** to display the **Application Pools** pane again.</span></span>

<span data-ttu-id="644e9-163">在**应用程序池**窗格中，单击**DefaultAppPool**，然后在**操作**窗格中，单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="644e9-163">In the **Application Pools** pane, click **DefaultAppPool**, and then in the **Actions** pane click **Basic Settings**.</span></span>

<span data-ttu-id="644e9-164">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-164">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)</span></span>

<span data-ttu-id="644e9-165">在**编辑应用程序池**对话框中，更改**.NET Framework 版本**到**.NET Framework v4.0.30319**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="644e9-165">In the **Edit Application Pool** dialog box, change **.NET Framework version** to **.NET Framework v4.0.30319** and click **OK**.</span></span>

<span data-ttu-id="644e9-166">[![Selecting_.NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-166">[![Selecting_.NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)</span></span>

<span data-ttu-id="644e9-167">现在你就可以将发布到 IIS。</span><span class="sxs-lookup"><span data-stu-id="644e9-167">You are now ready to publish to IIS.</span></span>

## <a name="publishing-to-iis"></a><span data-ttu-id="644e9-168">发布到 IIS</span><span class="sxs-lookup"><span data-stu-id="644e9-168">Publishing to IIS</span></span>

<span data-ttu-id="644e9-169">有多种方法可以部署使用 Visual Studio 2010 和 Web 部署：</span><span class="sxs-lookup"><span data-stu-id="644e9-169">There are several ways you can deploy using Visual Studio 2010 and Web Deploy:</span></span>

- <span data-ttu-id="644e9-170">使用一键式发布的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="644e9-170">Use Visual Studio one-click publish.</span></span>
- <span data-ttu-id="644e9-171">创建*部署包*和使用 IIS 管理器 UI 安装它。</span><span class="sxs-lookup"><span data-stu-id="644e9-171">Create a *deployment package* and install it using the IIS Manager UI.</span></span> <span data-ttu-id="644e9-172">部署包所包含的*.zip*包含的所有文件和在 IIS 中安装站点所需的元数据的文件。</span><span class="sxs-lookup"><span data-stu-id="644e9-172">The deployment package consists of a *.zip* file that contains all the files and metadata needed to install a site in IIS.</span></span>
- <span data-ttu-id="644e9-173">创建部署包并将其使用命令行安装。</span><span class="sxs-lookup"><span data-stu-id="644e9-173">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="644e9-174">你已完成在前面的教程，若要将 Visual Studio 设置来自动执行部署任务适用于所有这三种方法的过程。</span><span class="sxs-lookup"><span data-stu-id="644e9-174">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these three methods.</span></span> <span data-ttu-id="644e9-175">这些教程中，你将使用第一种方法。</span><span class="sxs-lookup"><span data-stu-id="644e9-175">In these tutorials you'll use the first of these methods.</span></span> <span data-ttu-id="644e9-176">有关使用部署包的信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。</span><span class="sxs-lookup"><span data-stu-id="644e9-176">For information about using deployment packages, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx).</span></span>

<span data-ttu-id="644e9-177">在发布前，请确保在管理员模式下运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="644e9-177">Before publishing, make sure that you are running Visual Studio in administrator mode.</span></span> <span data-ttu-id="644e9-178">(在 Windows 7**启动**菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择**以管理员身份运行**。)管理员模式下是发布仅当你准备向 IIS 发布在本地计算机上所必需的。</span><span class="sxs-lookup"><span data-stu-id="644e9-178">(In the Windows 7 **Start** menu, right-click the icon for the version of Visual Studio you're using and select **Run as Administrator**.) Administrator mode is required for publishing only when you are publishing to IIS on the local computer.</span></span>

<span data-ttu-id="644e9-179">在**解决方案资源管理器**，右键单击 ContosoUniversity 项目 （而不是 ContosoUniversity.DAL 项目） 并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="644e9-179">In **Solution Explorer**, right-click the ContosoUniversity project (not the ContosoUniversity.DAL project) and select **Publish**.</span></span>

<span data-ttu-id="644e9-180">**发布 Web**向导显示。</span><span class="sxs-lookup"><span data-stu-id="644e9-180">The **Publish Web** wizard appears.</span></span>

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

<span data-ttu-id="644e9-182">在下拉列表中，选择**&lt;新建...&gt;**.</span><span class="sxs-lookup"><span data-stu-id="644e9-182">In the drop-down list, select **&lt;New...&gt;**.</span></span>

<span data-ttu-id="644e9-183">在**新的配置文件**对话框中，输入"Test"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="644e9-183">In the **New Profile** dialog box, enter "Test", and then click **OK**.</span></span>

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

<span data-ttu-id="644e9-185">此名称是与 Web.Test.config 中间节点相同转换之前创建的文件。</span><span class="sxs-lookup"><span data-stu-id="644e9-185">This name is the same as the middle node of the Web.Test.config transform file that you created earlier.</span></span> <span data-ttu-id="644e9-186">这种对应关系是什么因素会导致在发布使用此配置文件时要应用的 Web.Test.config 转换。</span><span class="sxs-lookup"><span data-stu-id="644e9-186">This correspondence is what causes the Web.Test.config transformations to be applied when you publish by using this profile.</span></span>

<span data-ttu-id="644e9-187">该向导将自动前进到**连接**选项卡。</span><span class="sxs-lookup"><span data-stu-id="644e9-187">The wizard automatically advances to the **Connection** tab.</span></span>

<span data-ttu-id="644e9-188">在**服务 URL**框中，输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="644e9-188">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="644e9-189">在**站点/应用程序**框中，输入*默认网站/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="644e9-189">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="644e9-190">在**目标 URL**框中，输入`http://localhost/ContosoUniversity`。</span><span class="sxs-lookup"><span data-stu-id="644e9-190">In the **Destination URL** box, enter `http://localhost/ContosoUniversity`.</span></span>

<span data-ttu-id="644e9-191">**目标 URL**设置不是必需的。</span><span class="sxs-lookup"><span data-stu-id="644e9-191">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="644e9-192">Visual Studio 完成部署应用程序，它将自动打开默认浏览器到此 URL。</span><span class="sxs-lookup"><span data-stu-id="644e9-192">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="644e9-193">如果你不想要在部署后自动打开浏览器，请将此框留空。</span><span class="sxs-lookup"><span data-stu-id="644e9-193">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

<span data-ttu-id="644e9-195">单击**验证连接**以验证设置是否正确，并可以在本地计算机上连接到 IIS。</span><span class="sxs-lookup"><span data-stu-id="644e9-195">Click **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

<span data-ttu-id="644e9-196">绿色的复选标记验证连接成功。</span><span class="sxs-lookup"><span data-stu-id="644e9-196">A green check mark verifies that the connection is successful.</span></span>

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

<span data-ttu-id="644e9-198">单击**下一步**以转到**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="644e9-198">Click **Next** to advance to the **Settings** tab.</span></span>

<span data-ttu-id="644e9-199">**配置**下拉框指定要部署的生成配置。</span><span class="sxs-lookup"><span data-stu-id="644e9-199">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="644e9-200">默认值为版本中，这是你希望。</span><span class="sxs-lookup"><span data-stu-id="644e9-200">The default value is Release, which is what you want.</span></span>

<span data-ttu-id="644e9-201">保留**删除目标位置的其他文件**清除复选框。</span><span class="sxs-lookup"><span data-stu-id="644e9-201">Leave the **Remove additional files at destination** check box cleared.</span></span> <span data-ttu-id="644e9-202">由于这是你第一次部署时，不会有任何文件在目标文件夹中尚未。</span><span class="sxs-lookup"><span data-stu-id="644e9-202">Since this is your first deployment, there won't be any files in the destination folder yet.</span></span>

<span data-ttu-id="644e9-203">在**数据库**部分中，在连接字符串框中输入以下值**SchoolContext**:</span><span class="sxs-lookup"><span data-stu-id="644e9-203">In the **Databases** section, enter the following value in the connection string box for **SchoolContext**:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

<span data-ttu-id="644e9-204">在部署过程会将此连接字符串置于部署的 Web.config 文件因为**在运行时使用此连接字符串**选择。</span><span class="sxs-lookup"><span data-stu-id="644e9-204">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

<span data-ttu-id="644e9-205">此外，在**SchoolContext**，选择**应用 Code First 迁移**。</span><span class="sxs-lookup"><span data-stu-id="644e9-205">Also under **SchoolContext**, select **Apply Code First Migrations**.</span></span> <span data-ttu-id="644e9-206">此选项将导致配置已部署的 Web.config 文件，以指定部署过程`MigrateDatabaseToLatestVersion`初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="644e9-206">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="644e9-207">此初始值设定项应用程序部署后首次访问数据库时，自动将数据库更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="644e9-207">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

<span data-ttu-id="644e9-208">中的连接字符串框**DefaultConnection**，输入以下值：</span><span class="sxs-lookup"><span data-stu-id="644e9-208">In the connection string box for **DefaultConnection**, enter the following value:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

<span data-ttu-id="644e9-209">保留**更新数据库**清除。</span><span class="sxs-lookup"><span data-stu-id="644e9-209">Leave **Update database** cleared.</span></span> <span data-ttu-id="644e9-210">将通过在应用程序中复制的.sdf 文件部署成员资格数据库\_数据，而您不希望部署过程以执行任何其他与此数据库操作。</span><span class="sxs-lookup"><span data-stu-id="644e9-210">The membership database will be deployed by copying the .sdf file in App\_Data, and you don't want the deployment process to do anything else with this database.</span></span>

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

<span data-ttu-id="644e9-212">单击**下一步**以转到**预览**选项卡。</span><span class="sxs-lookup"><span data-stu-id="644e9-212">Click **Next** to advance to the **Preview** tab.</span></span>

<span data-ttu-id="644e9-213">在**预览**选项卡上，单击**开始预览**以查看将复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="644e9-213">In the **Preview** tab, click **Start Preview** to see a list of the files that will be copied.</span></span>

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

<span data-ttu-id="644e9-216">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="644e9-216">Click **Publish**.</span></span>

<span data-ttu-id="644e9-217">如果在管理员模式下，Visual Studio 不是，你可能会指示权限错误的错误消息。</span><span class="sxs-lookup"><span data-stu-id="644e9-217">If Visual Studio is not in administrator mode, you might get an error message that indicates a permissions error.</span></span> <span data-ttu-id="644e9-218">在这种情况下，关闭 Visual Studio，在管理员模式下打开它并尝试再次发布。</span><span class="sxs-lookup"><span data-stu-id="644e9-218">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

<span data-ttu-id="644e9-219">在管理员模式下，Visual Studio 是否**输出**窗口报表成功生成和发布。</span><span class="sxs-lookup"><span data-stu-id="644e9-219">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

<span data-ttu-id="644e9-221">浏览器将自动打开到 Contoso 大学主页在 IIS 中在本地计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="644e9-221">The browser automatically opens to the Contoso University Home page running in IIS on the local computer.</span></span>

<span data-ttu-id="644e9-222">[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-222">[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)</span></span>

## <a name="testing-in-the-test-environment"></a><span data-ttu-id="644e9-223">在测试环境中测试</span><span class="sxs-lookup"><span data-stu-id="644e9-223">Testing in the Test Environment</span></span>

<span data-ttu-id="644e9-224">请注意环境指示器，显示"（测试）"而不是"（开发）"，其中显示*Web.config*环境指示器的转换是否成功。</span><span class="sxs-lookup"><span data-stu-id="644e9-224">Notice that the environment indicator shows "(Test)" instead of "(Dev)", which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="644e9-225">[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-225">[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)</span></span>

<span data-ttu-id="644e9-226">运行**学生**页后，可以验证是否已部署的数据库具有任何学生。</span><span class="sxs-lookup"><span data-stu-id="644e9-226">Run the **Students** page to verify that the deployed database has no students.</span></span> <span data-ttu-id="644e9-227">当选择此页可能需要几分钟才能加载，因为 Code First 创建数据库，然后运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="644e9-227">When you select this page it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="644e9-228">（它未执行操作，因为应用程序未尝试访问数据库尚未年在主页上。）</span><span class="sxs-lookup"><span data-stu-id="644e9-228">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="644e9-229">[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-229">[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)</span></span>

<span data-ttu-id="644e9-230">运行**教师**页以验证 Code First 种子教师数据的数据库：</span><span class="sxs-lookup"><span data-stu-id="644e9-230">Run the **Instructors** page to verify that Code First seeded the database with instructor data:</span></span>

<span data-ttu-id="644e9-231">[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-231">[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)</span></span>

<span data-ttu-id="644e9-232">选择**添加学生**从**学生**菜单上，添加一名学生，，然后查看在新的学生**学生**页以验证是否可以成功写入到数据库:</span><span class="sxs-lookup"><span data-stu-id="644e9-232">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database:</span></span>

<span data-ttu-id="644e9-233">[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-233">[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)</span></span>

<span data-ttu-id="644e9-234">[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-234">[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)</span></span>

<span data-ttu-id="644e9-235">从**课程**菜单上，选择**更新信用额度**。</span><span class="sxs-lookup"><span data-stu-id="644e9-235">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="644e9-236">**更新信用额度**页需要管理员权限，因此**Log In**显示页。</span><span class="sxs-lookup"><span data-stu-id="644e9-236">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="644e9-237">输入你创建更早版本 （"admin"和"Pa$ w0rd"） 的管理员帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="644e9-237">Enter the administrator account credentials that you created earlier ("admin" and "Pas$w0rd").</span></span> <span data-ttu-id="644e9-238">**更新信用额度**页面显示时，该验证你在前面的教程中创建的管理员帐户已正确部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="644e9-238">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="644e9-239">[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-239">[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)</span></span>

<span data-ttu-id="644e9-240">[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-240">[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)</span></span>

<span data-ttu-id="644e9-241">验证*Elmah*文件夹存在与仅中它的占位符文件。</span><span class="sxs-lookup"><span data-stu-id="644e9-241">Verify that an *Elmah* folder exists with only the placeholder file in it.</span></span>

<span data-ttu-id="644e9-242">[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="644e9-242">[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)</span></span>

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="644e9-243">对于 Code First 迁移查看自动 Web.config 更改</span><span class="sxs-lookup"><span data-stu-id="644e9-243">Reviewing the Automatic Web.config Changes for Code First Migrations</span></span>

<span data-ttu-id="644e9-244">打开*Web.config*在已部署的应用程序中的文件*C:\inetpub\wwwroot\ContosoUniversity* ，你可以看到部署过程自动配置 Code First 迁移到其中将数据库更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="644e9-244">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

<span data-ttu-id="644e9-245">在部署过程还创建新的连接字符串的代码优先迁移来更新数据库架构的以独占方式使用：</span><span class="sxs-lookup"><span data-stu-id="644e9-245">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

<span data-ttu-id="644e9-247">此额外的连接字符串，可指定一个用户帐户对数据库架构更新和应用程序数据访问的其他用户帐户。</span><span class="sxs-lookup"><span data-stu-id="644e9-247">This additional connection string enables you to specify one user account for database schema updates, and a different user account for application data access.</span></span> <span data-ttu-id="644e9-248">例如，您无法将数据库\_到 Code First 迁移和 db 所有者角色\_datareader 和 db\_datawriter 角色添加至应用程序。</span><span class="sxs-lookup"><span data-stu-id="644e9-248">For example, you could assign the db\_owner role to Code First Migrations, and db\_datareader and db\_datawriter roles to the application.</span></span> <span data-ttu-id="644e9-249">这是一种常见的深层防御模式，可防止在应用程序不能更改数据库架构中的潜在恶意代码。</span><span class="sxs-lookup"><span data-stu-id="644e9-249">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="644e9-250">（例如，这可能会发生在成功的 SQL 注入式攻击。）这些教程不使用此模式。</span><span class="sxs-lookup"><span data-stu-id="644e9-250">(For example, this might happen in a successful SQL injection attack.) This pattern is not used by these tutorials.</span></span> <span data-ttu-id="644e9-251">它不适用于 SQL Server Compact 和在本系列后面的教程中迁移到 SQL Server 时不适用。</span><span class="sxs-lookup"><span data-stu-id="644e9-251">It does not apply to SQL Server Compact, and it does not apply when you migrate to SQL Server in a later tutorial in this series.</span></span> <span data-ttu-id="644e9-252">Cytanium 站点提供了一个访问在 Cytanium 创建的 SQL Server 数据库的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="644e9-252">The Cytanium site offers just one user account for accessing the SQL Server database that you create at Cytanium.</span></span> <span data-ttu-id="644e9-253">如果你将能够在你的方案中实现此模式，可以通过执行以下步骤来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="644e9-253">If you are able to implement this pattern in your scenario, you can do it by performing the following steps:</span></span>

1. <span data-ttu-id="644e9-254">在**设置**选项卡**发布 Web**向导中，输入完整的数据库架构更新权限，使用指定的用户的连接字符串，然后清除**使用此连接字符串在运行时**复选框。</span><span class="sxs-lookup"><span data-stu-id="644e9-254">In the **Settings** tab of the **Publish Web** wizard, enter the connection string that specifies a user with full database schema update permissions, and clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="644e9-255">在已部署的 Web.config 文件中，这将成为`DatabasePublish`连接字符串。</span><span class="sxs-lookup"><span data-stu-id="644e9-255">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>
2. <span data-ttu-id="644e9-256">创建 Web.config 文件转换为你想要在运行时使用的应用程序的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="644e9-256">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

<span data-ttu-id="644e9-257">你现在已在开发计算机上部署到 IIS 应用程序，并且存在测试。</span><span class="sxs-lookup"><span data-stu-id="644e9-257">You have now deployed your application to IIS on your development computer and tested it there.</span></span> <span data-ttu-id="644e9-258">这将验证部署过程将应用程序的内容复制到正确的位置 （不包括你确实不想要部署的文件），并还该 Web 部署已配置的 IIS 正确在部署过程。</span><span class="sxs-lookup"><span data-stu-id="644e9-258">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy), and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="644e9-259">在下一步的教程中，你将运行一个查找尚未完成的部署任务的详细测试： 上设置文件夹权限*Elmah*文件夹。</span><span class="sxs-lookup"><span data-stu-id="644e9-259">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elmah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="644e9-260">详细信息</span><span class="sxs-lookup"><span data-stu-id="644e9-260">More Information</span></span>

<span data-ttu-id="644e9-261">在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="644e9-261">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="644e9-262">[IIS Express 概述](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="644e9-262">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="644e9-263">[引入了 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的博客上。</span><span class="sxs-lookup"><span data-stu-id="644e9-263">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="644e9-264">[如何： 为 Visual Studio 中的 Web 项目指定 Web 服务器](https://msdn.microsoft.com/library/ms178108.aspx)。</span><span class="sxs-lookup"><span data-stu-id="644e9-264">[How to: Specify the Web Server for Web Projects in Visual Studio](https://msdn.microsoft.com/library/ms178108.aspx).</span></span>
- <span data-ttu-id="644e9-265">[核心差异之间 IIS 和 ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 站点上。</span><span class="sxs-lookup"><span data-stu-id="644e9-265">[Core Differences Between IIS and the ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>
- <span data-ttu-id="644e9-266">[在 30 秒内测试你的 ASP.NET MVC 或 Web 窗体应用程序在 IIS 7 上](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx)Rick Anderson 博客上。</span><span class="sxs-lookup"><span data-stu-id="644e9-266">[Test your ASP.NET MVC or Web Forms Application on IIS 7 in 30 seconds](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) on Rick Anderson's blog.</span></span> <span data-ttu-id="644e9-267">此条目提供使用 Visual Studio 开发服务器 (用于 Cassini) 来测试为何不不如在 IIS Express 中，测试可靠和在 IIS Express 测试为何不不如在 IIS 中测试可靠的示例。</span><span class="sxs-lookup"><span data-stu-id="644e9-267">This entry provides examples of why testing with the Visual Studio Development Server (Cassini) is not as reliable as testing in IIS Express, and why testing in IIS Express is not as reliable as testing in IIS.</span></span>

<span data-ttu-id="644e9-268">在中等信任中运行你的应用程序时，可能出现哪些问题有关的信息，请参阅[在中等信任环境中承载 ASP.NET 应用程序](http://www.4guysfromrolla.com/articles/100307-1.aspx)上从 Rolla 站点 4 专家。</span><span class="sxs-lookup"><span data-stu-id="644e9-268">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the 4 Guys from Rolla site.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="644e9-269">[上一页](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
[下一页](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="644e9-269">[Previous](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
[Next](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)</span></span>
