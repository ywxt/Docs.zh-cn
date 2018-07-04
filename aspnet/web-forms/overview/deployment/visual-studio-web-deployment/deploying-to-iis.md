---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署到测试 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 8c5034dd4948d96c5722e2dcc960cc0349241a1a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365680"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="749a9-103">使用 Visual Studio 的 ASP.NET Web 部署： 部署到测试</span><span class="sxs-lookup"><span data-stu-id="749a9-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>
====================
<span data-ttu-id="749a9-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="749a9-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="749a9-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="749a9-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="749a9-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="749a9-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="749a9-107">有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="749a9-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="749a9-108">概述</span><span class="sxs-lookup"><span data-stu-id="749a9-108">Overview</span></span>

<span data-ttu-id="749a9-109">本教程演示如何以 ASP.NET web 应用程序部署到 IIS 在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="749a9-109">This tutorial shows how to deploy an ASP.NET web application to IIS on the local computer.</span></span>

<span data-ttu-id="749a9-110">开发的应用程序，您通常进行测试的 Visual Studio 中运行。</span><span class="sxs-lookup"><span data-stu-id="749a9-110">When you develop an application, you generally test by running it in Visual Studio.</span></span> <span data-ttu-id="749a9-111">默认情况下，在 Visual Studio 2012 中的 web 应用程序项目使用 IIS Express 用作开发 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="749a9-111">By default, web application projects in Visual Studio 2012 use IIS Express as the development web server.</span></span> <span data-ttu-id="749a9-112">IIS Express 表现得更像与 Visual Studio 开发服务器 (也称为 Cassini)，默认情况下使用 Visual Studio 2010 的完整 IIS。</span><span class="sxs-lookup"><span data-stu-id="749a9-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2010 uses by default.</span></span> <span data-ttu-id="749a9-113">但既不开发 web 服务器的工作方式完全相同 IIS。</span><span class="sxs-lookup"><span data-stu-id="749a9-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="749a9-114">因此，就可以，当应用程序时对其进行测试在 Visual Studio 中，但失败部署到 IIS 时，将正确运行。</span><span class="sxs-lookup"><span data-stu-id="749a9-114">As a result, it's possible that an application will run correctly when you test it in Visual Studio, but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="749a9-115">你可以在以下方面更可靠地测试应用程序：</span><span class="sxs-lookup"><span data-stu-id="749a9-115">You can test your application more reliably in these ways:</span></span>

1. <span data-ttu-id="749a9-116">通过使用相同的过程的更高版本将使用它来将其部署到生产环境部署到 IIS 在开发计算机上的应用程序。</span><span class="sxs-lookup"><span data-stu-id="749a9-116">Deploy the application to IIS on your development computer by using the same process that you'll use later to deploy it to your production environment.</span></span> <span data-ttu-id="749a9-117">可以配置 Visual Studio 以使用 IIS 时运行 web 项目中，但执行该操作不会测试您的部署过程。</span><span class="sxs-lookup"><span data-stu-id="749a9-117">You can configure Visual Studio to use IIS when you run a web project, but doing that would not test your deployment process.</span></span> <span data-ttu-id="749a9-118">此方法验证部署过程除了验证你的应用程序将在 IIS 下正确运行。</span><span class="sxs-lookup"><span data-stu-id="749a9-118">This method validates your deployment process in addition to validating that your application will run correctly under IIS.</span></span>
2. <span data-ttu-id="749a9-119">应用程序部署到测试环境与生产环境几乎相同。</span><span class="sxs-lookup"><span data-stu-id="749a9-119">Deploy the application to a test environment that is nearly identical to your production environment.</span></span> <span data-ttu-id="749a9-120">由于这些教程在生产环境是 Azure 应用服务中的 Web 应用，因此非常适合测试环境是在 Azure 应用服务中创建的其他 web 应用。</span><span class="sxs-lookup"><span data-stu-id="749a9-120">Since the production environment for these tutorials is Web Apps in Azure App Service, the ideal test environment is an additional web app created in Azure App Service.</span></span> <span data-ttu-id="749a9-121">将此第二个 web 应用仅用于测试，但将设置为生产 web 应用的相同方法。</span><span class="sxs-lookup"><span data-stu-id="749a9-121">You would use this second web app only for testing, but it would be set up the same way as the production web app.</span></span>

<span data-ttu-id="749a9-122">选项 2 是最可靠的方法，若要测试，并且如果这样做，您不一定需要执行操作的选项 1。</span><span class="sxs-lookup"><span data-stu-id="749a9-122">Option 2 is the most reliable way to test, and if you do that, you don't necessarily have to do option 1.</span></span> <span data-ttu-id="749a9-123">但是，如果要部署到第三方托管提供程序选项 2 可能不可行，或可能开销很大，因此本系列教程演示这两种方法。</span><span class="sxs-lookup"><span data-stu-id="749a9-123">However, if you are deploying to a third-party hosting provider option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="749a9-124">在提供了选项 2 的指导[部署到生产环境](deploying-to-production.md)教程。</span><span class="sxs-lookup"><span data-stu-id="749a9-124">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="749a9-125">有关在 Visual Studio 中使用 web 服务器的详细信息，请参阅[对于 ASP.NET Web 项目的 Visual Studio 中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="749a9-125">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="749a9-126">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="749a9-126">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="install-iis"></a><span data-ttu-id="749a9-127">安装 IIS</span><span class="sxs-lookup"><span data-stu-id="749a9-127">Install IIS</span></span>

<span data-ttu-id="749a9-128">若要在开发计算机上部署到 IIS，必须具有 IIS 和 Web 部署安装。</span><span class="sxs-lookup"><span data-stu-id="749a9-128">To deploy to IIS on your development computer, you must have IIS and Web Deploy installed.</span></span> <span data-ttu-id="749a9-129">使用 Visual Studio 中，默认情况下安装 web 部署，但 IIS 未包含在默认 Windows 8 或 Windows 7 配置。</span><span class="sxs-lookup"><span data-stu-id="749a9-129">Web Deploy is installed by default with Visual Studio, but IIS is not included in the default Windows 8 or Windows 7 configuration.</span></span> <span data-ttu-id="749a9-130">如果已安装了 IIS 和默认应用程序池已设置为.NET 4，请跳到[下一步部分](#sqlexpress)。</span><span class="sxs-lookup"><span data-stu-id="749a9-130">If you have already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="749a9-131">使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是首选的方法来安装 IIS 和 Web 部署，因为 Web 平台安装程序为 IIS 安装建议的配置，并且它会自动安装 IIS 和 Web 的先决条件如有必要部署。</span><span class="sxs-lookup"><span data-stu-id="749a9-131">Using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) is the preferred way to install IIS and Web Deploy, because the Web Platform Installer installs a recommended configuration for IIS and it automatically installs the prerequisites for IIS and Web Deploy if necessary.</span></span>

    <span data-ttu-id="749a9-132">若要运行 Web 平台安装程序来安装 IIS 和 Web 部署，请使用以下链接。</span><span class="sxs-lookup"><span data-stu-id="749a9-132">To run Web Platform Installer to install IIS and Web Deploy, use the following link.</span></span> <span data-ttu-id="749a9-133">如果你已安装 IIS、 Web 部署或任何其所需的组件，Web 平台安装程序安装只缺少的内容。</span><span class="sxs-lookup"><span data-stu-id="749a9-133">If you already have installed IIS, Web Deploy or any of their required components, the Web Platform Installer installs only what is missing.</span></span>

   - [<span data-ttu-id="749a9-134">安装 IIS 和 Web 部署使用 WebPI</span><span class="sxs-lookup"><span data-stu-id="749a9-134">Install IIS and Web Deploy using WebPI</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

     <span data-ttu-id="749a9-135">可以看到，该值指示将安装 IIS 7 的消息。</span><span class="sxs-lookup"><span data-stu-id="749a9-135">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="749a9-136">链接的工作原理适用于 Windows 8 中的 IIS 8，但 Windows 8 确保 ASP.NET 4.5 安装，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="749a9-136">The link works for IIS 8 in Windows 8, but for Windows 8 make sure that ASP.NET 4.5 is installed by performing the following steps:</span></span>

   - <span data-ttu-id="749a9-137">打开**Control Panel**，**程序和功能**，**打开或关闭打开的 Windows 功能**。</span><span class="sxs-lookup"><span data-stu-id="749a9-137">Open **Control Panel**, **Programs and Features**, **Turn Windows features on or off**.</span></span>
   - <span data-ttu-id="749a9-138">展开**Internet 信息服务**，**万维网服务**，并**应用程序开发功能**。</span><span class="sxs-lookup"><span data-stu-id="749a9-138">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   - <span data-ttu-id="749a9-139">请确保**ASP.NET 4.5**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="749a9-139">Make sure that **ASP.NET 4.5** is selected.</span></span>

      ![选择 ASP.NET 4.5](deploying-to-iis/_static/image1.png)

<span data-ttu-id="749a9-141">安装 IIS 后，运行**IIS 管理器**以确保.NET Framework 版本 4 分配给默认应用程序池。</span><span class="sxs-lookup"><span data-stu-id="749a9-141">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="749a9-142">按 WINDOWS + R 打开**运行**对话框。</span><span class="sxs-lookup"><span data-stu-id="749a9-142">Press WINDOWS+R to open the **Run** dialog box.</span></span>

    <span data-ttu-id="749a9-143">(或在 Windows 8 中输入"运行"**启动**页上，或在 Windows 7 中选择**运行**从**启动**菜单。</span><span class="sxs-lookup"><span data-stu-id="749a9-143">(Or in Windows 8 enter "run" on the **Start** page, or in Windows 7 select **Run** from the **Start** menu.</span></span> <span data-ttu-id="749a9-144">如果**运行**不在**启动**菜单中，右键单击任务栏中，单击**属性**，选择 **「 开始 」 菜单**选项卡上，单击**自定义**，然后选择**运行命令**。)</span><span class="sxs-lookup"><span data-stu-id="749a9-144">If **Run** isn't in the **Start** menu, right-click the taskbar, click **Properties**, select the **Start Menu** tab, click **Customize**, and select **Run command**.)</span></span>
2. <span data-ttu-id="749a9-145">输入"inetmgr"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="749a9-145">Enter "inetmgr", and then click **OK**.</span></span>
3. <span data-ttu-id="749a9-146">在中**连接**窗格中，展开服务器节点，然后选择**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="749a9-146">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="749a9-147">在中**应用程序池**窗格中，如果**DefaultAppPool**是分配给.NET framework 版本 4 所示，跳到下一节。</span><span class="sxs-lookup"><span data-stu-id="749a9-147">In the **Application Pools** pane, if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

    <span data-ttu-id="749a9-148">[![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="749a9-148">[![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)</span></span>
4. <span data-ttu-id="749a9-149">如果您看到只有两个应用程序池，并且这两个值设置为.NET Framework 2.0，您必须在 IIS 中安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="749a9-149">If you see only two application pools and both of them are set to the .NET Framework 2.0, you have to install ASP.NET 4 in IIS.</span></span>

    <span data-ttu-id="749a9-150">有关 Windows 8 中，请参阅在前面的说明部分已安装并确保该 ASP.NET 4.5，或请参阅[此知识库文章](https://support.microsoft.com/kb/2736284)。</span><span class="sxs-lookup"><span data-stu-id="749a9-150">For Windows 8, see the instructions in the previous section for making sure that ASP.NET 4.5 is installed, or see [this KB article](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="749a9-151">对于 Windows 7 中，打开命令提示符窗口，请右键单击**命令提示符**在 Windows 中**启动**菜单并选择**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="749a9-151">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="749a9-152">然后运行[aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中，使用以下命令安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="749a9-152">Then run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS, using the following commands.</span></span> <span data-ttu-id="749a9-153">（在 32 位系统中，将为"Framework64"与"框架"。）</span><span class="sxs-lookup"><span data-stu-id="749a9-153">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

    <span data-ttu-id="749a9-154">此命令将为.NET Framework 4 中，创建新的应用程序池，但仍将被默认应用程序池设置为 2.0。</span><span class="sxs-lookup"><span data-stu-id="749a9-154">This command creates new application pools for the .NET Framework 4, but the default application pool will still be set to 2.0.</span></span> <span data-ttu-id="749a9-155">您要部署应用程序面向.NET 4 到该应用程序池，因此您必须将应用程序池更改为.NET 4。</span><span class="sxs-lookup"><span data-stu-id="749a9-155">You'll be deploying an application that targets .NET 4 to that application pool, so you have to change the application pool to .NET 4.</span></span>
5. <span data-ttu-id="749a9-156">如果您关闭**IIS 管理器**再次运行中，展开服务器节点，单击**应用程序池**以显示**应用程序池**再次窗格。</span><span class="sxs-lookup"><span data-stu-id="749a9-156">If you closed **IIS Manager**, run it again, expand the server node, and click **Application Pools** to display the **Application Pools** pane again.</span></span>
6. <span data-ttu-id="749a9-157">在中**应用程序池**窗格中，单击**DefaultAppPool**，然后在**操作**窗格中，单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="749a9-157">In the **Application Pools** pane, click **DefaultAppPool**, and then in the **Actions** pane click **Basic Settings**.</span></span>

    <span data-ttu-id="749a9-158">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="749a9-158">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)</span></span>
7. <span data-ttu-id="749a9-159">在中**编辑应用程序池**对话框中，更改 **.NET Framework 版本**到 **.NET Framework v4.0.30319**然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="749a9-159">In the **Edit Application Pool** dialog box, change **.NET Framework version** to **.NET Framework v4.0.30319** and click **OK**.</span></span>

    <span data-ttu-id="749a9-160">[![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="749a9-160">[![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)</span></span>

<span data-ttu-id="749a9-161">IIS 现在已准备就绪，发布 web 应用程序，但您可以执行的之前必须在测试环境中创建将使用的数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-161">IIS is now ready for you to publish a web application to it, but before you can do that you have to create the databases that you will use in the test environment.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="749a9-162">安装 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="749a9-162">Install SQL Server Express</span></span>

<span data-ttu-id="749a9-163">LocalDB 不设计用于处理在 IIS 中，因此对于你的测试环境需要已安装 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="749a9-163">LocalDB is not designed to work in IIS, so for your test environment you need to have SQL Server Express installed.</span></span> <span data-ttu-id="749a9-164">如果使用的 Visual Studio 2010 SQL Server Express 已安装默认情况下。</span><span class="sxs-lookup"><span data-stu-id="749a9-164">If you are using Visual Studio 2010 SQL Server Express is already installed by default.</span></span> <span data-ttu-id="749a9-165">如果正在使用 Visual Studio 2012，您必须安装它。</span><span class="sxs-lookup"><span data-stu-id="749a9-165">If you are using Visual Studio 2012, you have to install it.</span></span>

<span data-ttu-id="749a9-166">若要安装 SQL Server Express，请安装它从[Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062)通过单击[ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe)或[ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe)。</span><span class="sxs-lookup"><span data-stu-id="749a9-166">To install SQL Server Express, install it from [Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) by clicking [ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe) or [ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe).</span></span> <span data-ttu-id="749a9-167">如果选择了错误为您的系统，它将无法安装，并且您可以尝试另一个。</span><span class="sxs-lookup"><span data-stu-id="749a9-167">If you choose the wrong one for your system it will fail to install and you can try the other one.</span></span>

<span data-ttu-id="749a9-168">SQL Server 安装中心的第一页，单击**新的 SQL Server 独立安装或向现有安装添加功能**，并按照说明进行操作，接受默认选项。</span><span class="sxs-lookup"><span data-stu-id="749a9-168">On the first page of the SQL Server Installation Center, click **New SQL Server stand-alone installation or add features to an existing installation**, and follow the instructions, accepting the default choices.</span></span> <span data-ttu-id="749a9-169">在安装向导中，接受默认设置。</span><span class="sxs-lookup"><span data-stu-id="749a9-169">In the installation wizard accept the default settings.</span></span> <span data-ttu-id="749a9-170">有关安装选项的详细信息，请参阅[从安装向导 （安装程序） 中安装 SQL Server 2012](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="749a9-170">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="749a9-171">创建 SQL Server Express 数据库的测试环境</span><span class="sxs-lookup"><span data-stu-id="749a9-171">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="749a9-172">Contoso 大学应用程序有两个数据库： 成员资格数据库和应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-172">The Contoso University application has two databases: the membership database and the application database.</span></span> <span data-ttu-id="749a9-173">可以将这些数据库部署到两个独立数据库或单个数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-173">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="749a9-174">你可能想要将它们合并为了简化应用程序数据库和成员资格数据库之间的数据库联接。</span><span class="sxs-lookup"><span data-stu-id="749a9-174">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="749a9-175">如果要部署到第三方托管提供商，托管计划可能会提供的原因要将它们合并。</span><span class="sxs-lookup"><span data-stu-id="749a9-175">If you are deploying to a third-party hosting provider, your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="749a9-176">例如，托管提供商可能会收取多个数据库的详细信息，或可能甚至不允许多个数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-176">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="749a9-177">在本教程中，你将部署到测试环境中的两个数据库和过渡和生产环境中的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-177">In this tutorial, you'll deploy to two databases in the test environment, and to one database in the staging and production environments.</span></span>

<span data-ttu-id="749a9-178">从**视图**在 Visual Studio 中，选择菜单**服务器资源管理器**(**数据库资源管理器**在 Visual Web Developer)，然后右键单击**数据连接** ，然后选择**创建新的 SQL Server 数据库**。</span><span class="sxs-lookup"><span data-stu-id="749a9-178">From the **View** menu in Visual Studio select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="749a9-180">在中**创建新的 SQL Server 数据库**对话框框中，输入"。 \SQLExpress"在**服务器名称**框和"aspnet-ContosoUniversity"中**新的数据库名称**框，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="749a9-180">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box, then click **OK**.</span></span>

![创建 aspnet ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="749a9-182">请按照相同的过程来创建一个名为"ContosoUniversity"的新 SQL Server Express School 数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-182">Follow the same procedure to create a new SQL Server Express School database named "ContosoUniversity".</span></span>

<span data-ttu-id="749a9-183">**服务器资源管理器**现在将显示两个新数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-183">**Server Explorer** now shows the two new databases.</span></span>

![在服务器资源管理器中的新数据库](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="749a9-185">创建新的数据库授予脚本</span><span class="sxs-lookup"><span data-stu-id="749a9-185">Create a grant script for the new databases</span></span>

<span data-ttu-id="749a9-186">当在开发计算机上在 IIS 中运行的应用程序时，该应用程序使用的默认应用程序池的凭据访问数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-186">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="749a9-187">但是，默认情况下，应用程序池标识没有权限打开的数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-187">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="749a9-188">因此您必须运行一个脚本，以授予该权限。</span><span class="sxs-lookup"><span data-stu-id="749a9-188">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="749a9-189">在本部分中，您将创建将运行更高版本以确保在 IIS 中运行时，该应用程序可以打开数据库的脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-189">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="749a9-190">右键单击该解决方案 （而不是项目的），然后单击**添加新项**，然后创建一个新**SQL 文件**名为*Grant.sql*。</span><span class="sxs-lookup"><span data-stu-id="749a9-190">Right-click the solution (not one of the projects), and click **Add New Item**, and then create a new **SQL File** named *Grant.sql*.</span></span> <span data-ttu-id="749a9-191">将以下 SQL 命令复制到文件，然后保存并关闭文件：</span><span class="sxs-lookup"><span data-stu-id="749a9-191">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

> [!NOTE]
> <span data-ttu-id="749a9-192">此脚本用于处理与 SQL Server Express 2012 和 Windows 8 或 Windows 7 中的 IIS 设置，如在本教程中指定了。</span><span class="sxs-lookup"><span data-stu-id="749a9-192">This script is designed to work with SQL Server Express 2012 and with the IIS settings in Windows 8 or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="749a9-193">如果使用不同版本的 SQL Server 或 Windows，或您设置 IIS 计算机上以不同的方式，可能需要对此脚本的更改。</span><span class="sxs-lookup"><span data-stu-id="749a9-193">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="749a9-194">有关 SQL Server 脚本详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="749a9-194">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="749a9-195">**安全说明**此脚本将向提供 db\_所有者在运行时，这是您在生产环境中必须访问数据库的用户的权限。</span><span class="sxs-lookup"><span data-stu-id="749a9-195">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="749a9-196">在某些情况下您可能想要指定具有完整的数据库架构更新部署中，权限和指定的运行时具有的权限仅读取和写入数据的不同用户的用户。</span><span class="sxs-lookup"><span data-stu-id="749a9-196">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="749a9-197">有关详细信息，请参阅[评审 Code First 迁移自动 Web.config 更改](#reviewingmigrations)在本教程中更高版本。</span><span class="sxs-lookup"><span data-stu-id="749a9-197">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>


<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="749a9-198">运行应用程序数据库中授予脚本</span><span class="sxs-lookup"><span data-stu-id="749a9-198">Run the grant script in the application database</span></span>

<span data-ttu-id="749a9-199">你可以配置要运行授予脚本成员资格数据库中，在部署期间因为该数据库的部署使用 dbDacFx 提供程序的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-199">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the dbDacFx provider.</span></span> <span data-ttu-id="749a9-200">在 Code First 迁移部署，这是你要如何部署应用程序数据库期间，无法运行脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-200">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="749a9-201">因此，必须手动运行应用程序数据库中的部署前的脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-201">Therefore, you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="749a9-202">在 Visual Studio 中打开*Grant.sql*前面创建的文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-202">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>
2. <span data-ttu-id="749a9-203">单击“连接” 。</span><span class="sxs-lookup"><span data-stu-id="749a9-203">Click **Connect**.</span></span> 

    ![连接按钮](deploying-to-iis/_static/image11.png)
3. <span data-ttu-id="749a9-205">在中**连接到服务器**对话框框中，输入 *。 \SQLExpress*作为**服务器名称**，然后单击**Connect**。</span><span class="sxs-lookup"><span data-stu-id="749a9-205">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**, and then click **Connect**.</span></span>
4. <span data-ttu-id="749a9-206">在数据库下拉列表中选择**ContosoUniversity**，然后单击**Execute**。</span><span class="sxs-lookup"><span data-stu-id="749a9-206">In the database drop-down list select **ContosoUniversity**, and then click **Execute**.</span></span> 

    ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="749a9-207">现在，默认应用程序池标识代码优先迁移来创建数据库表，该应用程序运行时在应用程序数据库中具有足够的权限。</span><span class="sxs-lookup"><span data-stu-id="749a9-207">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="749a9-208">将发布到 IIS</span><span class="sxs-lookup"><span data-stu-id="749a9-208">Publish to IIS</span></span>

<span data-ttu-id="749a9-209">有几种方法可以将它们部署到 IIS，使用 Visual Studio 和 Web 部署：</span><span class="sxs-lookup"><span data-stu-id="749a9-209">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

- <span data-ttu-id="749a9-210">使用一键式发布的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="749a9-210">Use Visual Studio one-click publish.</span></span>
- <span data-ttu-id="749a9-211">从命令行发布。</span><span class="sxs-lookup"><span data-stu-id="749a9-211">Publish from the command line.</span></span>
- <span data-ttu-id="749a9-212">创建*部署包*和使用 IIS 管理器 UI 安装它。</span><span class="sxs-lookup"><span data-stu-id="749a9-212">Create a *deployment package* and install it using the IIS Manager UI.</span></span> <span data-ttu-id="749a9-213">部署包组成 *.zip*文件，其中包含所有文件和在 IIS 中安装站点所需的元数据。</span><span class="sxs-lookup"><span data-stu-id="749a9-213">The deployment package consists of a *.zip* file that contains all the files and metadata needed to install a site in IIS.</span></span>
- <span data-ttu-id="749a9-214">创建部署包并将其使用命令行安装。</span><span class="sxs-lookup"><span data-stu-id="749a9-214">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="749a9-215">已在前面的教程，要将 Visual Studio 设置为自动执行部署任务适用于所有这些方法的过程。</span><span class="sxs-lookup"><span data-stu-id="749a9-215">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="749a9-216">在这些教程将使用这些方法的前两个。</span><span class="sxs-lookup"><span data-stu-id="749a9-216">In these tutorials you'll use the first two of these methods.</span></span> <span data-ttu-id="749a9-217">有关使用部署包的信息，请参阅[web 应用程序部署通过创建和安装 web 部署包](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)for Visual Studio 和 ASP.NET Web 部署内容映射中。</span><span class="sxs-lookup"><span data-stu-id="749a9-217">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="749a9-218">发布前，请确保在管理员模式下运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="749a9-218">Before publishing, make sure that you are running Visual Studio in administrator mode.</span></span> <span data-ttu-id="749a9-219">如果没有看到 **（管理员）** 在标题栏中，关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="749a9-219">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="749a9-220">在 Windows 8**启动**页上或 Windows 7**启动**菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="749a9-220">In the Windows 8 **Start** page or the Windows 7 **Start** menu, right-click the icon for the version of Visual Studio you're using and select **Run as Administrator**.</span></span> <span data-ttu-id="749a9-221">管理员模式下是发布仅当您要发布到 IIS 在本地计算机上所必需的。</span><span class="sxs-lookup"><span data-stu-id="749a9-221">Administrator mode is required for publishing only when you are publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="749a9-222">创建发布配置文件</span><span class="sxs-lookup"><span data-stu-id="749a9-222">Create the publish profile</span></span>

1. <span data-ttu-id="749a9-223">在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目 （而不是 ContosoUniversity.DAL 项目），然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="749a9-223">In **Solution Explorer**, right-click the ContosoUniversity project (not the ContosoUniversity.DAL project) and select **Publish**.</span></span>

    <span data-ttu-id="749a9-224">**发布 Web**向导显示。</span><span class="sxs-lookup"><span data-stu-id="749a9-224">The **Publish Web** wizard appears.</span></span>

    ![发布 Web 向导配置文件选项卡](deploying-to-iis/_static/image13.png)
2. <span data-ttu-id="749a9-226">在下拉列表中，选择**&lt;新建...&gt;**.</span><span class="sxs-lookup"><span data-stu-id="749a9-226">In the drop-down list, select **&lt;New...&gt;**.</span></span> <span data-ttu-id="749a9-227">(安装了最新 Visual Studio 更新，没有任何下拉列表中，而且单击以从头开始创建新的配置文件按钮**自定义**。)</span><span class="sxs-lookup"><span data-stu-id="749a9-227">(With the latest Visual Studio update installed, there is no drop-down list, and the button to click in order to create a new profile from scratch is **Custom**.)</span></span>
3. <span data-ttu-id="749a9-228">在中**新的配置文件**对话框中，输入"Test"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="749a9-228">In the **New Profile** dialog box, enter "Test", and then click **OK**.</span></span>

    <span data-ttu-id="749a9-229">该向导将自动前进到**连接**选项卡。</span><span class="sxs-lookup"><span data-stu-id="749a9-229">The wizard automatically advances to the **Connection** tab.</span></span>
4. <span data-ttu-id="749a9-230">在中**服务 URL**框中，输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="749a9-230">In the **Service URL** box, enter *localhost*.</span></span>
5. <span data-ttu-id="749a9-231">在中**站点/应用程序**框中，输入*默认 Web 站点/ContosoUniversity*</span><span class="sxs-lookup"><span data-stu-id="749a9-231">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*</span></span>
6. <span data-ttu-id="749a9-232">在中**目标 URL**框中，输入 `http://localhost/ContosoUniversity`</span><span class="sxs-lookup"><span data-stu-id="749a9-232">In the **Destination URL** box, enter `http://localhost/ContosoUniversity`</span></span>

    <span data-ttu-id="749a9-233">**目标 URL**设置不需要。</span><span class="sxs-lookup"><span data-stu-id="749a9-233">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="749a9-234">完成 Visual Studio 部署应用程序后，它会自动打开默认浏览器访问此 URL。</span><span class="sxs-lookup"><span data-stu-id="749a9-234">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="749a9-235">如果不想要在部署后自动打开浏览器，将此框留空。</span><span class="sxs-lookup"><span data-stu-id="749a9-235">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>
7. <span data-ttu-id="749a9-236">单击**验证连接**以验证是否设置正确无误，并可以在本地计算机上连接到 IIS。</span><span class="sxs-lookup"><span data-stu-id="749a9-236">Click **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

    <span data-ttu-id="749a9-237">绿色复选标记验证连接成功。</span><span class="sxs-lookup"><span data-stu-id="749a9-237">A green check mark verifies that the connection is successful.</span></span>

    ![发布 Web 向导连接选项卡](deploying-to-iis/_static/image14.png)
8. <span data-ttu-id="749a9-239">单击**下一步**转到**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="749a9-239">Click **Next** to advance to the **Settings** tab.</span></span>
9. <span data-ttu-id="749a9-240">**配置**下拉列表框指定要部署的生成配置。</span><span class="sxs-lookup"><span data-stu-id="749a9-240">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="749a9-241">将其设置为发布的默认值。</span><span class="sxs-lookup"><span data-stu-id="749a9-241">Leave it set to the default value of Release.</span></span> <span data-ttu-id="749a9-242">不会将在本教程中部署了调试版本。</span><span class="sxs-lookup"><span data-stu-id="749a9-242">You won't be deploying Debug builds in this tutorial.</span></span>
10. <span data-ttu-id="749a9-243">展开**文件发布选项**，然后选择**排除将应用程序中的文件\_Data 文件夹**。</span><span class="sxs-lookup"><span data-stu-id="749a9-243">Expand **File Publish Options**, and then select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="749a9-244">在测试环境中应用程序将访问本地 SQL Server Express 实例中创建的数据库，不.mdf 文件中*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="749a9-244">In the test environment the application will access the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>
11. <span data-ttu-id="749a9-245">将保留**在发布期间预编译**并**删除目标处的其他文件**清除复选框。</span><span class="sxs-lookup"><span data-stu-id="749a9-245">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![设置选项卡中的文件发布选项](deploying-to-iis/_static/image15.png)

    <span data-ttu-id="749a9-247">预编译是主要用于非常大的站点; 一个选项它可以减少页面第一次请求页面时，将站点发布后的启动时间。</span><span class="sxs-lookup"><span data-stu-id="749a9-247">Precompiling is an option that is useful mainly for very large sites; it can reduce page startup time for the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="749a9-248">不需要由于这是你第一次部署，也不会有任何文件的目标文件夹中尚未删除的其他文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-248">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > 
    > [!CAUTION]
    > <span data-ttu-id="749a9-249">如果选择**删除的其他文件**对于到相同站点的后续部署，请确保你使用的预览功能，以便你提前看到在部署之前，将删除哪些文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-249">If you select **Remove additional files** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="749a9-250">预期的行为是，Web 部署会删除已在项目中删除目标服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-250">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="749a9-251">但是，在源和目标文件夹下的整个文件夹结构进行比较，并在某些情况下 Web 部署可能会删除不想要删除的文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-251">However, the entire folder structure under the source and destination folders is compared, and in some scenarios Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="749a9-252">例如，如果在服务器上的子文件夹中没有的 web 应用程序项目部署到的根文件夹时，将删除子文件夹。</span><span class="sxs-lookup"><span data-stu-id="749a9-252">For example, if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="749a9-253">你可能在 contoso.com 的主站点的一个项目，并在 contoso.com/blog 博客的另一个项目。</span><span class="sxs-lookup"><span data-stu-id="749a9-253">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="749a9-254">博客应用程序是一个子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="749a9-254">The blog application is in a subfolder.</span></span> <span data-ttu-id="749a9-255">如果您选择删除目标位置的其他文件，在将主站点时，将删除博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="749a9-255">If you select Remove additional files at destination when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="749a9-256">有关其他示例，您的应用程序\_数据文件夹可能会意外删除。</span><span class="sxs-lookup"><span data-stu-id="749a9-256">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="749a9-257">某些数据库，例如 SQL Server Compact 数据库文件存储在应用\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="749a9-257">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="749a9-258">在初始部署之后不想要保留将数据库文件复制在后续部署中，因此选择排除应用\_打包/发布 Web 选项卡上的数据。在执行操作，如果你已删除所选目标位置的其他文件、 数据库文件和应用程序之后\_的下次发布时都将删除数据文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="749a9-258">After the initial deployment you don't want to keep copying the database files in subsequent deployments so you select  Exclude App\_Data on the Package/Publish Web tab. After you do that, if you have Remove additional files at destination selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="749a9-259">配置成员资格数据库部署</span><span class="sxs-lookup"><span data-stu-id="749a9-259">Configure deployment for the membership database</span></span>

<span data-ttu-id="749a9-260">以下步骤适用于**DefaultConnection**数据库中**数据库**对话框的一节。</span><span class="sxs-lookup"><span data-stu-id="749a9-260">The following steps apply to the **DefaultConnection** database in the **Databases** section of the dialog box.</span></span>

1. <span data-ttu-id="749a9-261">在中**远程连接字符串**框中，输入以下指向新的 SQL Server Express 成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="749a9-261">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

    <span data-ttu-id="749a9-262">由于部署过程会将此连接字符串放在已部署的 Web.config 文件中**在运行时使用此连接字符串**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="749a9-262">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="749a9-263">此外可以获取的连接字符串**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="749a9-263">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="749a9-264">在中**服务器资源管理器**，展开**数据连接**，然后选择 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**数据库，然后从**属性**窗口中复制**连接字符串**值。</span><span class="sxs-lookup"><span data-stu-id="749a9-264">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="749a9-265">连接字符串将具有一个可以删除的其他设置： `Pooling=False`。</span><span class="sxs-lookup"><span data-stu-id="749a9-265">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>
2. <span data-ttu-id="749a9-266">选择**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="749a9-266">Select **Update database**.</span></span>

    <span data-ttu-id="749a9-267">这会导致要在部署过程中创建目标数据库中的数据库架构。</span><span class="sxs-lookup"><span data-stu-id="749a9-267">This will cause the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="749a9-268">以下步骤中指定您需要运行其他脚本： 一个用于授予对默认应用程序池，一个用于部署数据的数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="749a9-268">In the following steps you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>
3. <span data-ttu-id="749a9-269">单击**配置数据库更新**。</span><span class="sxs-lookup"><span data-stu-id="749a9-269">Click **Configure database updates**.</span></span>
4. <span data-ttu-id="749a9-270">在中**配置数据库更新**对话框中，单击**添加 SQL 脚本**，然后导航到*Grant.sql*之前保存在解决方案文件夹中的脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-270">In the **Configure Database Updates** dialog box, click **Add SQL Script** and then navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>
5. <span data-ttu-id="749a9-271">重复此过程以添加*aspnet 数据 dev.sql*脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-271">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

    ![为成员资格数据库配置数据库更新](deploying-to-iis/_static/image16.png)
6. <span data-ttu-id="749a9-273">单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="749a9-273">Click **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="749a9-274">配置应用程序数据库的部署</span><span class="sxs-lookup"><span data-stu-id="749a9-274">Configure deployment for the application database</span></span>

<span data-ttu-id="749a9-275">当 Visual Studio 检测到实体框架`DbContext`类，它创建中的条目**数据库**节，其中包含**执行 Code First 迁移**复选框，而不是**更新数据库**复选框。</span><span class="sxs-lookup"><span data-stu-id="749a9-275">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="749a9-276">对于本教程将使用该复选框来指定 Code First 迁移部署。</span><span class="sxs-lookup"><span data-stu-id="749a9-276">For this tutorial you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="749a9-277">在某些情况下，你可能使用`DbContext`数据库，但想要使用 dbDacFx 提供程序而不是迁移部署数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-277">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="749a9-278">在这种情况下，请参阅[如何将 Code First 数据库而无需迁移的部署？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) MSDN 上的 ASP.NET Web 部署常见问题解答中。</span><span class="sxs-lookup"><span data-stu-id="749a9-278">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="749a9-279">以下步骤适用于**SchoolContext**数据库中**数据库**对话框的一节。</span><span class="sxs-lookup"><span data-stu-id="749a9-279">The following steps apply to the **SchoolContext** database in the **Databases** section of the dialog box.</span></span>

1. <span data-ttu-id="749a9-280">在中**远程连接字符串**框中，输入以下指向新的 SQL Server Express 应用程序数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="749a9-280">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

    <span data-ttu-id="749a9-281">由于部署过程会将此连接字符串放在已部署的 Web.config 文件中**在运行时使用此连接字符串**处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="749a9-281">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="749a9-282">此外可以获取的应用程序数据库连接字符串**服务器资源管理器**相同的方式获得成员身份数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="749a9-282">You can also get the application database connection string from **Server Explorer** the same way you got the membership database connection string.</span></span>
2. <span data-ttu-id="749a9-283">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="749a9-283">Select **Execute Code First Migrations (runs on application start)**.</span></span>

    <span data-ttu-id="749a9-284">此选项将导致部署过程，配置已部署的 Web.config 文件，以指定`MigrateDatabaseToLatestVersion`初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="749a9-284">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="749a9-285">此初始值设定项自动更新数据库的最新版本时该应用程序部署后首次访问数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-285">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="749a9-286">配置发布配置文件转换</span><span class="sxs-lookup"><span data-stu-id="749a9-286">Configure publish profile transforms</span></span>

1. <span data-ttu-id="749a9-287">单击**关闭**，然后单击**是**当系统询问你是否要保存更改。</span><span class="sxs-lookup"><span data-stu-id="749a9-287">Click **Close**, and then click **Yes** when you are asked if you want to save changes.</span></span>
2. <span data-ttu-id="749a9-288">在中**解决方案资源管理器**，展开**属性**，展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="749a9-288">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>
3. <span data-ttu-id="749a9-289">Rright 键单击*Test.pubxml，* ，然后单击**添加配置转换**。</span><span class="sxs-lookup"><span data-stu-id="749a9-289">Rright-click *Test.pubxml,* and then click **Add Config Transform**.</span></span>

    ![添加配置转换菜单](deploying-to-iis/_static/image17.png)

    <span data-ttu-id="749a9-291">Visual Studio 将创建*Web.Test.config*转换文件并将其打开。</span><span class="sxs-lookup"><span data-stu-id="749a9-291">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>
4. <span data-ttu-id="749a9-292">在中*Web.Test.config*转换文件中，打开后立即插入以下代码配置标记。</span><span class="sxs-lookup"><span data-stu-id="749a9-292">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

    [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="749a9-293">当使用测试发布配置文件时，此转换设置为"Test"的环境指示器。</span><span class="sxs-lookup"><span data-stu-id="749a9-293">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="749a9-294">在已部署的站点将在"Contoso University"H1 标题后看到"（测试）"。</span><span class="sxs-lookup"><span data-stu-id="749a9-294">In the deployed site you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>
5. <span data-ttu-id="749a9-295">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="749a9-295">Save and close the file.</span></span>
6. <span data-ttu-id="749a9-296">右键单击*Web.Test.config*文件，并单击**预览版转换**以确保您编码的转换生成预期的更改。</span><span class="sxs-lookup"><span data-stu-id="749a9-296">Right-click the *Web.Test.config* file and click **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="749a9-297">**Web.config 预览版**窗口中显示结果应用同时*Web.Release.config*转换并*Web.Test.config*转换。</span><span class="sxs-lookup"><span data-stu-id="749a9-297">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="749a9-298">预览的部署更新</span><span class="sxs-lookup"><span data-stu-id="749a9-298">Preview the deployment updates</span></span>

1. <span data-ttu-id="749a9-299">打开**发布 Web**再次向导 (右键单击 ContosoUniversity 项目，然后单击**发布**)。</span><span class="sxs-lookup"><span data-stu-id="749a9-299">Open the **Publish Web** wizard again (right-click the ContosoUniversity project and click **Publish**).</span></span>
2. <span data-ttu-id="749a9-300">在中**预览版**选项卡上，请确保**测试**配置文件，并且仍然选择，然后单击**开始预览**以查看将复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="749a9-300">In the **Preview** tab, make sure that the **Test** profile is still selected, and then click **Start Preview** to see a list of the files that will be copied.</span></span>

    ![预览按钮](deploying-to-iis/_static/image18.png)

    ![发布预览](deploying-to-iis/_static/image19.png)

    <span data-ttu-id="749a9-303">此外可以单击**预览版数据库**链接可查看将在成员资格数据库中运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="749a9-303">You can also click the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="749a9-304">（没有运行脚本对于 Code First 迁移部署，因此没有要预览的应用程序数据库。）</span><span class="sxs-lookup"><span data-stu-id="749a9-304">(No scripts are run for Code First Migrations deployment, so there is nothing to preview for the application database.)</span></span>
3. <span data-ttu-id="749a9-305">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="749a9-305">Click **Publish**.</span></span>

    <span data-ttu-id="749a9-306">如果 Visual Studio 不是在管理员模式下，可能会收到一个错误消息，指示权限错误。</span><span class="sxs-lookup"><span data-stu-id="749a9-306">If Visual Studio is not in administrator mode, you might get an error message that indicates a permissions error.</span></span> <span data-ttu-id="749a9-307">在这种情况下，关闭 Visual Studio，在管理员模式下打开并尝试再次发布。</span><span class="sxs-lookup"><span data-stu-id="749a9-307">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

    <span data-ttu-id="749a9-308">在管理员模式下，Visual Studio 是否**输出**窗口报告成功生成和发布。</span><span class="sxs-lookup"><span data-stu-id="749a9-308">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

    ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

    <span data-ttu-id="749a9-310">如果输入中的 URL**目标 URL**上的发布配置文件框**连接**选项卡上，浏览器会自动打开指向本地计算机上在 IIS 中运行 Contoso University 主页上。</span><span class="sxs-lookup"><span data-stu-id="749a9-310">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on the local computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="749a9-311">在测试环境中测试</span><span class="sxs-lookup"><span data-stu-id="749a9-311">Test in the test environment</span></span>

<span data-ttu-id="749a9-312">请注意，环境指示器，显示"（测试）"而不是"（开发）"，其中显示*Web.config*环境指示器的转换是否成功。</span><span class="sxs-lookup"><span data-stu-id="749a9-312">Notice that the environment indicator shows "(Test)" instead of "(Dev)", which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="749a9-313">运行**讲师**页以验证 Code First 种子讲师数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-313">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="749a9-314">当选中此页时，可能需要几分钟才能加载，因为 Code First 创建数据库并运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="749a9-314">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="749a9-315">（它没有这样做时，因为该应用程序不尝试尚未访问的数据库都在主页上。）</span><span class="sxs-lookup"><span data-stu-id="749a9-315">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="749a9-316">单击**学生**选项卡以验证是否已部署的数据库具有任何学生。</span><span class="sxs-lookup"><span data-stu-id="749a9-316">Click the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="749a9-317">选择**添加学生**从**学生**菜单中，添加一名学生，，然后查看中的新学生**学生**页以验证是否可以成功写入到数据库.</span><span class="sxs-lookup"><span data-stu-id="749a9-317">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database.</span></span>

<span data-ttu-id="749a9-318">从**课程**菜单中，选择**更新信用额度**。</span><span class="sxs-lookup"><span data-stu-id="749a9-318">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="749a9-319">**更新信用额度**页面需要管理员权限，因此**Log In**显示页。</span><span class="sxs-lookup"><span data-stu-id="749a9-319">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="749a9-320">输入创建早期 （"admin"和"devpwd"） 的管理员帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="749a9-320">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="749a9-321">**更新信用额度**显示页面时，用于验证在上一教程中创建的管理员帐户已正确部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="749a9-321">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="749a9-322">确认*Elmah*文件夹中存在*c:\inetpub\wwwroot\ContosoUniversity*的占位符文件将在其中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="749a9-322">Verify that an *Elmah* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="749a9-323">查看自动 Web.config 更改的 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="749a9-323">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="749a9-324">打开*Web.config*文件中的已部署应用程序*C:\inetpub\wwwroot\ContosoUniversity* ，可以看到部署过程会自动配置 Code First 迁移到其中更新到最新版本的数据库。</span><span class="sxs-lookup"><span data-stu-id="749a9-324">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="749a9-325">部署过程还创建新的连接字符串的代码优先迁移来更新数据库架构的以独占方式使用：</span><span class="sxs-lookup"><span data-stu-id="749a9-325">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 连接字符串](deploying-to-iis/_static/image22.png)

<span data-ttu-id="749a9-327">通过此附加的连接字符串，您可以指定一个用户帐户对数据库架构更新，以及用于数据访问应用程序的不同用户帐户。</span><span class="sxs-lookup"><span data-stu-id="749a9-327">This additional connection string enables you to specify one user account for database schema updates, and a different user account for application data access.</span></span> <span data-ttu-id="749a9-328">例如，可将分配**db\_所有者**到 Code First 迁移角色和**db\_datareader**并**db\_datawriter**向应用程序角色。</span><span class="sxs-lookup"><span data-stu-id="749a9-328">For example, you could assign the **db\_owner** role to Code First Migrations, and **db\_datareader** and **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="749a9-329">这是一种常用的深度防御模式阻止潜在的恶意代码应用程序更改数据库架构。</span><span class="sxs-lookup"><span data-stu-id="749a9-329">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="749a9-330">（例如，可能发生此错误在成功的 SQL 注入式攻击。）这些教程不使用此模式。</span><span class="sxs-lookup"><span data-stu-id="749a9-330">(For example, this might happen in a successful SQL injection attack.) This pattern is not used by these tutorials.</span></span> <span data-ttu-id="749a9-331">如果你想要在你的方案中实现此模式，可以通过执行以下步骤操作即可：</span><span class="sxs-lookup"><span data-stu-id="749a9-331">If you want to implement this pattern in your scenario, you can do it by performing the following steps:</span></span>

1. <span data-ttu-id="749a9-332">在中**设置**选项卡**发布 Web**向导中，输入具有完整的数据库架构更新权限，指定的用户的连接字符串，并清除**使用此连接字符串在运行时**复选框。</span><span class="sxs-lookup"><span data-stu-id="749a9-332">In the **Settings** tab of the **Publish Web** wizard, enter the connection string that specifies a user with full database schema update permissions, and clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="749a9-333">在已部署的 Web.config 文件中，这将成为`DatabasePublish`连接字符串。</span><span class="sxs-lookup"><span data-stu-id="749a9-333">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>
2. <span data-ttu-id="749a9-334">创建 Web.config 文件转换为你想要在运行时使用的应用程序的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="749a9-334">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="749a9-335">总结</span><span class="sxs-lookup"><span data-stu-id="749a9-335">Summary</span></span>

<span data-ttu-id="749a9-336">现在已在开发计算机上部署到 IIS 应用程序，并对其进行存在测试。</span><span class="sxs-lookup"><span data-stu-id="749a9-336">You have now deployed your application to IIS on your development computer and tested it there.</span></span>

![在测试中的主页](deploying-to-iis/_static/image23.png)

<span data-ttu-id="749a9-338">这将验证部署过程将应用程序的内容复制到正确的位置 （不包括不想部署的文件），并还该 Web 部署 IIS 正确配置在部署过程。</span><span class="sxs-lookup"><span data-stu-id="749a9-338">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy), and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="749a9-339">在下一步的教程中，你将运行一个测试，以发现尚未完成的部署任务： 上设置文件夹权限*Elmah*文件夹。</span><span class="sxs-lookup"><span data-stu-id="749a9-339">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elmah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="749a9-340">详细信息</span><span class="sxs-lookup"><span data-stu-id="749a9-340">More information</span></span>

<span data-ttu-id="749a9-341">在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="749a9-341">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="749a9-342">[IIS Express 概述](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)IIS.net 站点上。</span><span class="sxs-lookup"><span data-stu-id="749a9-342">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="749a9-343">[引入了 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的博客上。</span><span class="sxs-lookup"><span data-stu-id="749a9-343">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="749a9-344">[Web 服务器在 Visual Studio 中的，对 ASP.NET Web 项目](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="749a9-344">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="749a9-345">[核心区别之间 IIS 和 ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 站点上。</span><span class="sxs-lookup"><span data-stu-id="749a9-345">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="749a9-346">在中等信任环境中运行应用程序时，可能出现什么问题的信息，请参阅[承载 ASP.NET 应用程序在中等信任](http://www.4guysfromrolla.com/articles/100307-1.aspx)上 Rolla 站点中的 4 个专家。</span><span class="sxs-lookup"><span data-stu-id="749a9-346">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the 4 Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="749a9-347">[上一页](project-properties.md)
> [下一页](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="749a9-347">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
