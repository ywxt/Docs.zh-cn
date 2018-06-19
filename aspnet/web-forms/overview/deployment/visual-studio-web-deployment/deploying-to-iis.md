---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio 的 ASP.NET Web 部署： 将部署到测试 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: dc11072e053cbddd089e5df4bcea6d2a7af864fc
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890861"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="25a13-103">使用 Visual Studio 的 ASP.NET Web 部署： 将部署到测试</span><span class="sxs-lookup"><span data-stu-id="25a13-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>
====================
<span data-ttu-id="25a13-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="25a13-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="25a13-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="25a13-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="25a13-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="25a13-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="25a13-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="25a13-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="25a13-108">概述</span><span class="sxs-lookup"><span data-stu-id="25a13-108">Overview</span></span>

<span data-ttu-id="25a13-109">本教程演示如何部署到 IIS 在本地计算机上的 ASP.NET web 应用。</span><span class="sxs-lookup"><span data-stu-id="25a13-109">This tutorial shows how to deploy an ASP.NET web application to IIS on the local computer.</span></span>

<span data-ttu-id="25a13-110">当你开发应用程序时，你通常测试通过在 Visual Studio 中运行它。</span><span class="sxs-lookup"><span data-stu-id="25a13-110">When you develop an application, you generally test by running it in Visual Studio.</span></span> <span data-ttu-id="25a13-111">默认情况下，在 Visual Studio 2012 中的 web 应用程序项目使用 IIS Express 作为开发 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="25a13-111">By default, web application projects in Visual Studio 2012 use IIS Express as the development web server.</span></span> <span data-ttu-id="25a13-112">IIS Express 表现得更像与 Visual Studio 开发服务器 (也称为 Cassini)，默认情况下使用 Visual Studio 2010 的完整 IIS。</span><span class="sxs-lookup"><span data-stu-id="25a13-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2010 uses by default.</span></span> <span data-ttu-id="25a13-113">但既不开发 web 服务器的工作原理完全类似 IIS。</span><span class="sxs-lookup"><span data-stu-id="25a13-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="25a13-114">因此，很可能，当应用程序时对其进行测试在 Visual Studio 中，但在部署到 IIS 时失败，将正确运行。</span><span class="sxs-lookup"><span data-stu-id="25a13-114">As a result, it's possible that an application will run correctly when you test it in Visual Studio, but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="25a13-115">你可以通过以下方式更可靠地测试你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="25a13-115">You can test your application more reliably in these ways:</span></span>

1. <span data-ttu-id="25a13-116">通过使用相同的过程，你将使用更高版本来将其部署到生产环境部署到 IIS 开发计算机上的应用程序。</span><span class="sxs-lookup"><span data-stu-id="25a13-116">Deploy the application to IIS on your development computer by using the same process that you'll use later to deploy it to your production environment.</span></span> <span data-ttu-id="25a13-117">你可以配置 Visual Studio 以使用 IIS 时运行 web 项目中，但执行该操作将不会测试你的部署过程。</span><span class="sxs-lookup"><span data-stu-id="25a13-117">You can configure Visual Studio to use IIS when you run a web project, but doing that would not test your deployment process.</span></span> <span data-ttu-id="25a13-118">此方法验证除了验证你在 IIS 下将正确运行你的应用程序的部署过程。</span><span class="sxs-lookup"><span data-stu-id="25a13-118">This method validates your deployment process in addition to validating that your application will run correctly under IIS.</span></span>
2. <span data-ttu-id="25a13-119">将应用部署到生产环境到几乎完全相同的测试环境。</span><span class="sxs-lookup"><span data-stu-id="25a13-119">Deploy the application to a test environment that is nearly identical to your production environment.</span></span> <span data-ttu-id="25a13-120">由于这些教程的生产环境是在 Azure App Service Web Apps，理想的测试环境是在 Azure App Service 中创建的其他 web 应用。</span><span class="sxs-lookup"><span data-stu-id="25a13-120">Since the production environment for these tutorials is Web Apps in Azure App Service, the ideal test environment is an additional web app created in Azure App Service.</span></span> <span data-ttu-id="25a13-121">仅对于测试，你可以使用此第二个 web 应用，但将其设置与生产 web 应用相同的方式。</span><span class="sxs-lookup"><span data-stu-id="25a13-121">You would use this second web app only for testing, but it would be set up the same way as the production web app.</span></span>

<span data-ttu-id="25a13-122">选项 2 是最可靠的方法，若要测试，并且如果你这样做，你不一定不要选项 1。</span><span class="sxs-lookup"><span data-stu-id="25a13-122">Option 2 is the most reliable way to test, and if you do that, you don't necessarily have to do option 1.</span></span> <span data-ttu-id="25a13-123">但是，如果您要部署到第三方宿主提供程序选项 2 可能不可行，或可能占用大量资源，因此此教程系列将演示这两种方法。</span><span class="sxs-lookup"><span data-stu-id="25a13-123">However, if you are deploying to a third-party hosting provider option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="25a13-124">选项 2 指南提供在[将部署到生产环境](deploying-to-production.md)教程。</span><span class="sxs-lookup"><span data-stu-id="25a13-124">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="25a13-125">有关使用 Visual Studio 中的 web 服务器的详细信息，请参阅[用于 ASP.NET Web 项目的 Visual Studio 中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25a13-125">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="25a13-126">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="25a13-126">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="install-iis"></a><span data-ttu-id="25a13-127">安装 IIS</span><span class="sxs-lookup"><span data-stu-id="25a13-127">Install IIS</span></span>

<span data-ttu-id="25a13-128">若要将部署到 IIS 在开发计算机上，你必须 IIS 和 Web 部署安装。</span><span class="sxs-lookup"><span data-stu-id="25a13-128">To deploy to IIS on your development computer, you must have IIS and Web Deploy installed.</span></span> <span data-ttu-id="25a13-129">默认情况下，使用 Visual Studio，安装 web 部署，但是 IIS 不包含在默认 Windows 8 或 Windows 7 配置。</span><span class="sxs-lookup"><span data-stu-id="25a13-129">Web Deploy is installed by default with Visual Studio, but IIS is not included in the default Windows 8 or Windows 7 configuration.</span></span> <span data-ttu-id="25a13-130">如果已安装了 IIS，并且默认应用程序池已设置为.NET 4，请跳到[下一节](#sqlexpress)。</span><span class="sxs-lookup"><span data-stu-id="25a13-130">If you have already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="25a13-131">使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是首选的方法来安装 IIS 和 Web 部署，因为 Web 平台安装程序的 IIS 安装推荐的配置，并自动安装 IIS 和 Web 的先决条件如有必要部署。</span><span class="sxs-lookup"><span data-stu-id="25a13-131">Using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) is the preferred way to install IIS and Web Deploy, because the Web Platform Installer installs a recommended configuration for IIS and it automatically installs the prerequisites for IIS and Web Deploy if necessary.</span></span>

    <span data-ttu-id="25a13-132">若要运行 Web 平台安装程序安装 IIS 和 Web 部署，请使用以下链接。</span><span class="sxs-lookup"><span data-stu-id="25a13-132">To run Web Platform Installer to install IIS and Web Deploy, use the following link.</span></span> <span data-ttu-id="25a13-133">如果你已安装 IIS、 Web 部署或任何其所需的组件，Web 平台安装程序仅安装功能丢失。</span><span class="sxs-lookup"><span data-stu-id="25a13-133">If you already have installed IIS, Web Deploy or any of their required components, the Web Platform Installer installs only what is missing.</span></span>

   - [<span data-ttu-id="25a13-134">安装 IIS 和 Web 部署使用 WebPI</span><span class="sxs-lookup"><span data-stu-id="25a13-134">Install IIS and Web Deploy using WebPI</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

     <span data-ttu-id="25a13-135">你将看到，该值指示将安装 IIS 7 的消息。</span><span class="sxs-lookup"><span data-stu-id="25a13-135">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="25a13-136">链接适用于 Windows 8 中 IIS 8 但适用于 Windows 8 确保执行以下步骤安装 ASP.NET 4.5:</span><span class="sxs-lookup"><span data-stu-id="25a13-136">The link works for IIS 8 in Windows 8, but for Windows 8 make sure that ASP.NET 4.5 is installed by performing the following steps:</span></span>

   - <span data-ttu-id="25a13-137">打开**控制面板**，**程序和功能**，**打开或关闭 Windows 功能**。</span><span class="sxs-lookup"><span data-stu-id="25a13-137">Open **Control Panel**, **Programs and Features**, **Turn Windows features on or off**.</span></span>
   - <span data-ttu-id="25a13-138">展开**Internet Information Services**， **World Wide Web 服务**，和**应用程序开发功能**。</span><span class="sxs-lookup"><span data-stu-id="25a13-138">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   - <span data-ttu-id="25a13-139">请确保**ASP.NET 4.5**选择。</span><span class="sxs-lookup"><span data-stu-id="25a13-139">Make sure that **ASP.NET 4.5** is selected.</span></span>

      ![选择 ASP.NET 4.5](deploying-to-iis/_static/image1.png)

<span data-ttu-id="25a13-141">安装 IIS 后，运行**IIS 管理器**若要确保.NET Framework 版本 4 分配给默认应用程序池。</span><span class="sxs-lookup"><span data-stu-id="25a13-141">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="25a13-142">按 WINDOWS + R，打开**运行**对话框。</span><span class="sxs-lookup"><span data-stu-id="25a13-142">Press WINDOWS+R to open the **Run** dialog box.</span></span>

    <span data-ttu-id="25a13-143">(或在 Windows 8 中输入"运行"**启动**页上，或在 Windows 7 中选择**运行**从**启动**菜单。</span><span class="sxs-lookup"><span data-stu-id="25a13-143">(Or in Windows 8 enter "run" on the **Start** page, or in Windows 7 select **Run** from the **Start** menu.</span></span> <span data-ttu-id="25a13-144">如果**运行**不在**启动**菜单上，右键单击任务栏中，单击**属性**，选择**开始菜单**选项卡上，单击**自定义**，然后选择**运行命令**。)</span><span class="sxs-lookup"><span data-stu-id="25a13-144">If **Run** isn't in the **Start** menu, right-click the taskbar, click **Properties**, select the **Start Menu** tab, click **Customize**, and select **Run command**.)</span></span>
2. <span data-ttu-id="25a13-145">输入"inetmgr"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="25a13-145">Enter "inetmgr", and then click **OK**.</span></span>
3. <span data-ttu-id="25a13-146">在**连接**窗格中，展开服务器节点，然后选择**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="25a13-146">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="25a13-147">在**应用程序池**窗格中，如果**DefaultAppPool**是分配给.NET framework 版本 4，如下图所示，跳到下一节。</span><span class="sxs-lookup"><span data-stu-id="25a13-147">In the **Application Pools** pane, if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

    <span data-ttu-id="25a13-148">[![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="25a13-148">[![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)</span></span>
4. <span data-ttu-id="25a13-149">如果你看到只有两个应用程序池，并且这两个设置为.NET Framework 2.0，你必须安装在 IIS 中的 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="25a13-149">If you see only two application pools and both of them are set to the .NET Framework 2.0, you have to install ASP.NET 4 in IIS.</span></span>

    <span data-ttu-id="25a13-150">有关 Windows 8，请参阅部分安装适用于确保该 ASP.NET 4.5 的或请参阅在前面说明[此知识库文章](https://support.microsoft.com/kb/2736284)。</span><span class="sxs-lookup"><span data-stu-id="25a13-150">For Windows 8, see the instructions in the previous section for making sure that ASP.NET 4.5 is installed, or see [this KB article](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="25a13-151">对于 Windows 7 中打开命令提示符窗口，通过右键单击**命令提示符**中 Windows**启动**菜单并选择**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="25a13-151">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="25a13-152">然后运行[aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中，使用以下命令安装 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="25a13-152">Then run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS, using the following commands.</span></span> <span data-ttu-id="25a13-153">（在 32 位系统中，替换"Framework64"与"Framework"。）</span><span class="sxs-lookup"><span data-stu-id="25a13-153">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

    <span data-ttu-id="25a13-154">此命令为.NET Framework 4 中，创建新的应用程序池，但默认应用程序池将仍设置为 2.0。</span><span class="sxs-lookup"><span data-stu-id="25a13-154">This command creates new application pools for the .NET Framework 4, but the default application pool will still be set to 2.0.</span></span> <span data-ttu-id="25a13-155">您要部署应用程序面向.NET 4 到该应用程序池，因此你需要为.NET 4 中更改应用程序池。</span><span class="sxs-lookup"><span data-stu-id="25a13-155">You'll be deploying an application that targets .NET 4 to that application pool, so you have to change the application pool to .NET 4.</span></span>
5. <span data-ttu-id="25a13-156">如果您关闭**IIS 管理器**，再次运行，展开服务器节点中，，再单击**应用程序池**以显示**应用程序池**再次窗格。</span><span class="sxs-lookup"><span data-stu-id="25a13-156">If you closed **IIS Manager**, run it again, expand the server node, and click **Application Pools** to display the **Application Pools** pane again.</span></span>
6. <span data-ttu-id="25a13-157">在**应用程序池**窗格中，单击**DefaultAppPool**，然后在**操作**窗格中，单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="25a13-157">In the **Application Pools** pane, click **DefaultAppPool**, and then in the **Actions** pane click **Basic Settings**.</span></span>

    <span data-ttu-id="25a13-158">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="25a13-158">[![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)</span></span>
7. <span data-ttu-id="25a13-159">在**编辑应用程序池**对话框中，更改 **.NET Framework 版本**到 **.NET Framework v4.0.30319**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="25a13-159">In the **Edit Application Pool** dialog box, change **.NET Framework version** to **.NET Framework v4.0.30319** and click **OK**.</span></span>

    <span data-ttu-id="25a13-160">[![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="25a13-160">[![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)</span></span>

<span data-ttu-id="25a13-161">IIS 现在已准备好为你发布到其中，web 应用程序，但是可以执行此操作之前必须先在测试环境中创建将使用的数据库的。</span><span class="sxs-lookup"><span data-stu-id="25a13-161">IIS is now ready for you to publish a web application to it, but before you can do that you have to create the databases that you will use in the test environment.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="25a13-162">安装 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="25a13-162">Install SQL Server Express</span></span>

<span data-ttu-id="25a13-163">LocalDB 不是用于处理在 IIS 中，因此对于你的测试环境需要已安装 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="25a13-163">LocalDB is not designed to work in IIS, so for your test environment you need to have SQL Server Express installed.</span></span> <span data-ttu-id="25a13-164">如果你使用 Visual Studio 2010 SQL Server Express 已安装默认情况下。</span><span class="sxs-lookup"><span data-stu-id="25a13-164">If you are using Visual Studio 2010 SQL Server Express is already installed by default.</span></span> <span data-ttu-id="25a13-165">如果你正在使用 Visual Studio 2012，你必须安装它。</span><span class="sxs-lookup"><span data-stu-id="25a13-165">If you are using Visual Studio 2012, you have to install it.</span></span>

<span data-ttu-id="25a13-166">若要安装 SQL Server Express，将其从安装[下载中心： Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062)通过单击[ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe)或[ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe)。</span><span class="sxs-lookup"><span data-stu-id="25a13-166">To install SQL Server Express, install it from [Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) by clicking [ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe) or [ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe).</span></span> <span data-ttu-id="25a13-167">如果选择了错误对于你的系统，它将无法安装，并且您可以尝试另一个。</span><span class="sxs-lookup"><span data-stu-id="25a13-167">If you choose the wrong one for your system it will fail to install and you can try the other one.</span></span>

<span data-ttu-id="25a13-168">在 SQL Server 安装中心的第一页，单击**新的 SQL Server 独立安装或向现有安装添加功能**，并按照说明操作，接受默认选项。</span><span class="sxs-lookup"><span data-stu-id="25a13-168">On the first page of the SQL Server Installation Center, click **New SQL Server stand-alone installation or add features to an existing installation**, and follow the instructions, accepting the default choices.</span></span> <span data-ttu-id="25a13-169">在安装向导中，接受默认设置。</span><span class="sxs-lookup"><span data-stu-id="25a13-169">In the installation wizard accept the default settings.</span></span> <span data-ttu-id="25a13-170">有关安装选项的详细信息，请参阅[从安装向导 （安装程序） 中安装 SQL Server 2012](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25a13-170">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="25a13-171">创建 SQL Server Express 数据库的测试环境</span><span class="sxs-lookup"><span data-stu-id="25a13-171">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="25a13-172">Contoso 大学应用程序具有两个数据库： 成员资格数据库和应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-172">The Contoso University application has two databases: the membership database and the application database.</span></span> <span data-ttu-id="25a13-173">你可以将这些数据库部署到两个单独的数据库或单个数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-173">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="25a13-174">你可能想要将它们合并为了简化你的应用程序数据库和成员资格数据库之间的数据库联接。</span><span class="sxs-lookup"><span data-stu-id="25a13-174">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="25a13-175">如果将部署到第三方托管提供商，托管计划可能还会提供相应原因，才能将它们合并。</span><span class="sxs-lookup"><span data-stu-id="25a13-175">If you are deploying to a third-party hosting provider, your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="25a13-176">例如，托管提供商可能会收费多个数据库的详细信息，或可能不甚至允许多个数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-176">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="25a13-177">在本教程中，你将部署到两个数据库在测试环境中，和过渡和生产环境中的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-177">In this tutorial, you'll deploy to two databases in the test environment, and to one database in the staging and production environments.</span></span>

<span data-ttu-id="25a13-178">从**视图**菜单在 Visual Studio 中，选择**服务器资源管理器**(**数据库资源管理器**在 Visual Web Developer)，然后右键单击**数据连接**和选择**创建新的 SQL Server 数据库**。</span><span class="sxs-lookup"><span data-stu-id="25a13-178">From the **View** menu in Visual Studio select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="25a13-180">在**创建新的 SQL Server 数据库**对话框框中，输入"。 \SQLExpress"中**服务器名称**框和"aspnet-ContosoUniversity"中**新的数据库名称**框中，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="25a13-180">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box, then click **OK**.</span></span>

![创建 aspnet ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="25a13-182">请按照相同的过程来创建名为"ContosoUniversity"的新 SQL Server Express School 数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-182">Follow the same procedure to create a new SQL Server Express School database named "ContosoUniversity".</span></span>

<span data-ttu-id="25a13-183">**服务器资源管理器**现在将显示两个新数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-183">**Server Explorer** now shows the two new databases.</span></span>

![在服务器资源管理器中的新数据库](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="25a13-185">创建新的数据库授予脚本</span><span class="sxs-lookup"><span data-stu-id="25a13-185">Create a grant script for the new databases</span></span>

<span data-ttu-id="25a13-186">当在 IIS 中在开发计算机上运行应用程序时，应用程序使用默认应用程序池的凭据访问数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-186">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="25a13-187">但是，默认情况下，应用程序池标识没有打开数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="25a13-187">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="25a13-188">因此，你需要运行一个脚本来授予该权限。</span><span class="sxs-lookup"><span data-stu-id="25a13-188">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="25a13-189">在本部分中，你将创建你将运行更高版本，以确保它在 IIS 中运行时，该应用程序可以打开数据库的脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-189">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="25a13-190">右键单击该解决方案 （不是一种项目），然后单击**添加新项**，然后创建一个新**SQL 文件**名为*Grant.sql*。</span><span class="sxs-lookup"><span data-stu-id="25a13-190">Right-click the solution (not one of the projects), and click **Add New Item**, and then create a new **SQL File** named *Grant.sql*.</span></span> <span data-ttu-id="25a13-191">将以下 SQL 命令复制到文件，然后保存并关闭文件：</span><span class="sxs-lookup"><span data-stu-id="25a13-191">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

> [!NOTE]
> <span data-ttu-id="25a13-192">此脚本用于处理与 SQL Server Express 2012 和 Windows 8 或 Windows 7 中的 IIS 设置，因为它们在本教程中指定。</span><span class="sxs-lookup"><span data-stu-id="25a13-192">This script is designed to work with SQL Server Express 2012 and with the IIS settings in Windows 8 or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="25a13-193">如果在使用不同版本的 SQL Server 或的 Windows 中，或者如果你设置 IIS 在你的计算机上以不同的方式，可能需要对此脚本的更改。</span><span class="sxs-lookup"><span data-stu-id="25a13-193">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="25a13-194">有关 SQL Server 脚本的详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="25a13-194">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="25a13-195">**安全说明**此脚本将向提供 db\_程序在运行时，这是必须在生产环境中访问数据库的用户的所有者权限。</span><span class="sxs-lookup"><span data-stu-id="25a13-195">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="25a13-196">在某些情况下你可能想要指定具有完整的数据库架构更新权限仅对于部署，并指定运行时具有的权限仅读取和写入数据的不同用户的用户。</span><span class="sxs-lookup"><span data-stu-id="25a13-196">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="25a13-197">有关详细信息，请参阅[为 Code First 迁移查看自动 Web.config 更改](#reviewingmigrations)本教程后面。</span><span class="sxs-lookup"><span data-stu-id="25a13-197">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>


<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="25a13-198">运行应用程序数据库中授予脚本</span><span class="sxs-lookup"><span data-stu-id="25a13-198">Run the grant script in the application database</span></span>

<span data-ttu-id="25a13-199">你可以配置要运行授予脚本成员资格数据库中，在部署过程因为该数据库部署使用 dbDacFx 提供程序的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-199">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the dbDacFx provider.</span></span> <span data-ttu-id="25a13-200">在 Code First 迁移部署，也就是如何在部署应用程序数据库期间，无法运行脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-200">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="25a13-201">因此，你必须手动运行应用程序数据库中的部署之前，该脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-201">Therefore, you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="25a13-202">在 Visual Studio 中，打开*Grant.sql*前面创建的文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-202">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>
2. <span data-ttu-id="25a13-203">单击“连接” 。</span><span class="sxs-lookup"><span data-stu-id="25a13-203">Click **Connect**.</span></span> 

    ![连接按钮](deploying-to-iis/_static/image11.png)
3. <span data-ttu-id="25a13-205">在**连接到服务器**对话框框中，输入 *。 \SQLExpress*作为**服务器名称**，然后单击**连接**。</span><span class="sxs-lookup"><span data-stu-id="25a13-205">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**, and then click **Connect**.</span></span>
4. <span data-ttu-id="25a13-206">在数据库下拉列表选择**ContosoUniversity**，然后单击**执行**。</span><span class="sxs-lookup"><span data-stu-id="25a13-206">In the database drop-down list select **ContosoUniversity**, and then click **Execute**.</span></span> 

    ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="25a13-207">现在，默认应用程序池标识代码优先迁移来创建数据库表，应用程序运行时的应用程序数据库中具有足够的权限。</span><span class="sxs-lookup"><span data-stu-id="25a13-207">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="25a13-208">将发布到 IIS</span><span class="sxs-lookup"><span data-stu-id="25a13-208">Publish to IIS</span></span>

<span data-ttu-id="25a13-209">有多种方法可以将它们部署到 IIS 使用 Visual Studio 和 Web 部署：</span><span class="sxs-lookup"><span data-stu-id="25a13-209">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

- <span data-ttu-id="25a13-210">使用一键式发布的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25a13-210">Use Visual Studio one-click publish.</span></span>
- <span data-ttu-id="25a13-211">从命令行发布。</span><span class="sxs-lookup"><span data-stu-id="25a13-211">Publish from the command line.</span></span>
- <span data-ttu-id="25a13-212">创建*部署包*和使用 IIS 管理器 UI 安装它。</span><span class="sxs-lookup"><span data-stu-id="25a13-212">Create a *deployment package* and install it using the IIS Manager UI.</span></span> <span data-ttu-id="25a13-213">部署包所包含的 *.zip*包含的所有文件和在 IIS 中安装站点所需的元数据的文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-213">The deployment package consists of a *.zip* file that contains all the files and metadata needed to install a site in IIS.</span></span>
- <span data-ttu-id="25a13-214">创建部署包并将其使用命令行安装。</span><span class="sxs-lookup"><span data-stu-id="25a13-214">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="25a13-215">你已完成在前面的教程，若要将 Visual Studio 设置来自动执行部署任务适用于所有这些方法的过程。</span><span class="sxs-lookup"><span data-stu-id="25a13-215">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="25a13-216">这些教程中，你将使用这些方法在前的两个。</span><span class="sxs-lookup"><span data-stu-id="25a13-216">In these tutorials you'll use the first two of these methods.</span></span> <span data-ttu-id="25a13-217">有关使用部署包的信息，请参阅[部署 web 应用程序创建和安装 web 部署包](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)for Visual Studio 和 ASP.NET Web 部署内容映射中。</span><span class="sxs-lookup"><span data-stu-id="25a13-217">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="25a13-218">在发布前，请确保在管理员模式下运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25a13-218">Before publishing, make sure that you are running Visual Studio in administrator mode.</span></span> <span data-ttu-id="25a13-219">如果看不到 **（管理员）** 在标题栏中，关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25a13-219">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="25a13-220">Windows 8 中**启动**页或 Windows 7**启动**菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="25a13-220">In the Windows 8 **Start** page or the Windows 7 **Start** menu, right-click the icon for the version of Visual Studio you're using and select **Run as Administrator**.</span></span> <span data-ttu-id="25a13-221">管理员模式下是发布仅当你准备向 IIS 发布在本地计算机上所必需的。</span><span class="sxs-lookup"><span data-stu-id="25a13-221">Administrator mode is required for publishing only when you are publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="25a13-222">创建发布配置文件</span><span class="sxs-lookup"><span data-stu-id="25a13-222">Create the publish profile</span></span>

1. <span data-ttu-id="25a13-223">在**解决方案资源管理器**，右键单击 ContosoUniversity 项目 （而不是 ContosoUniversity.DAL 项目） 并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="25a13-223">In **Solution Explorer**, right-click the ContosoUniversity project (not the ContosoUniversity.DAL project) and select **Publish**.</span></span>

    <span data-ttu-id="25a13-224">**发布 Web**向导显示。</span><span class="sxs-lookup"><span data-stu-id="25a13-224">The **Publish Web** wizard appears.</span></span>

    ![发布 Web 向导配置文件选项卡](deploying-to-iis/_static/image13.png)
2. <span data-ttu-id="25a13-226">在下拉列表中，选择**&lt;新建...&gt;**.</span><span class="sxs-lookup"><span data-stu-id="25a13-226">In the drop-down list, select **&lt;New...&gt;**.</span></span> <span data-ttu-id="25a13-227">(利用最新的 Visual Studio 更新安装，没有任何下拉列表中，并且要从头开始创建新的配置文件以便单击的按钮是**自定义**。)</span><span class="sxs-lookup"><span data-stu-id="25a13-227">(With the latest Visual Studio update installed, there is no drop-down list, and the button to click in order to create a new profile from scratch is **Custom**.)</span></span>
3. <span data-ttu-id="25a13-228">在**新的配置文件**对话框中，输入"Test"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="25a13-228">In the **New Profile** dialog box, enter "Test", and then click **OK**.</span></span>

    <span data-ttu-id="25a13-229">该向导将自动前进到**连接**选项卡。</span><span class="sxs-lookup"><span data-stu-id="25a13-229">The wizard automatically advances to the **Connection** tab.</span></span>
4. <span data-ttu-id="25a13-230">在**服务 URL**框中，输入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="25a13-230">In the **Service URL** box, enter *localhost*.</span></span>
5. <span data-ttu-id="25a13-231">在**站点/应用程序**框中，输入*默认网站/ContosoUniversity*</span><span class="sxs-lookup"><span data-stu-id="25a13-231">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*</span></span>
6. <span data-ttu-id="25a13-232">在**目标 URL**框中，输入 `http://localhost/ContosoUniversity`</span><span class="sxs-lookup"><span data-stu-id="25a13-232">In the **Destination URL** box, enter `http://localhost/ContosoUniversity`</span></span>

    <span data-ttu-id="25a13-233">**目标 URL**设置不是必需的。</span><span class="sxs-lookup"><span data-stu-id="25a13-233">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="25a13-234">Visual Studio 完成部署应用程序，它将自动打开默认浏览器到此 URL。</span><span class="sxs-lookup"><span data-stu-id="25a13-234">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="25a13-235">如果你不想要在部署后自动打开浏览器，请将此框留空。</span><span class="sxs-lookup"><span data-stu-id="25a13-235">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>
7. <span data-ttu-id="25a13-236">单击**验证连接**以验证设置是否正确，并可以在本地计算机上连接到 IIS。</span><span class="sxs-lookup"><span data-stu-id="25a13-236">Click **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

    <span data-ttu-id="25a13-237">绿色的复选标记验证连接成功。</span><span class="sxs-lookup"><span data-stu-id="25a13-237">A green check mark verifies that the connection is successful.</span></span>

    ![发布 Web 向导连接选项卡](deploying-to-iis/_static/image14.png)
8. <span data-ttu-id="25a13-239">单击**下一步**以转到**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="25a13-239">Click **Next** to advance to the **Settings** tab.</span></span>
9. <span data-ttu-id="25a13-240">**配置**下拉框指定要部署的生成配置。</span><span class="sxs-lookup"><span data-stu-id="25a13-240">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="25a13-241">请将其设置为发布的默认值。</span><span class="sxs-lookup"><span data-stu-id="25a13-241">Leave it set to the default value of Release.</span></span> <span data-ttu-id="25a13-242">不会同时在本教程中部署了调试版本。</span><span class="sxs-lookup"><span data-stu-id="25a13-242">You won't be deploying Debug builds in this tutorial.</span></span>
10. <span data-ttu-id="25a13-243">展开**文件发布选项**，然后选择**将应用程序中排除文件\_数据文件夹**。</span><span class="sxs-lookup"><span data-stu-id="25a13-243">Expand **File Publish Options**, and then select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="25a13-244">在测试环境中应用程序将访问本地 SQL Server Express 实例中创建的数据库，不.mdf 文件中*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="25a13-244">In the test environment the application will access the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>
11. <span data-ttu-id="25a13-245">保留**在发布过程 Precompile**和**删除目标位置的其他文件**清除复选框。</span><span class="sxs-lookup"><span data-stu-id="25a13-245">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![设置选项卡中的文件发布选项](deploying-to-iis/_static/image15.png)

    <span data-ttu-id="25a13-247">预编译是选项，主要用于非常大的站点。它可以减少首次将站点发布后，请求页的页启动时间。</span><span class="sxs-lookup"><span data-stu-id="25a13-247">Precompiling is an option that is useful mainly for very large sites; it can reduce page startup time for the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="25a13-248">你不需要由于这是你第一次部署，不会有任何文件在目标文件夹中尚未删除的其他文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-248">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > 
    > [!CAUTION]
    > <span data-ttu-id="25a13-249">如果你选择**删除其他文件**对于后续部署到相同的站点，请确保你使用预览功能，以便你提前看到在部署之前，将删除哪些文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-249">If you select **Remove additional files** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="25a13-250">预期的行为是，Web 部署将会删除已删除项目中的目标服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-250">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="25a13-251">但是，在源和目标文件夹的整个文件夹结构进行比较，并且在某些情况下 Web 部署可能会删除你不想要删除的文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-251">However, the entire folder structure under the source and destination folders is compared, and in some scenarios Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="25a13-252">例如，如果你有 web 应用程序服务器上的子文件夹中为项目部署到的根文件夹时，将删除子文件夹。</span><span class="sxs-lookup"><span data-stu-id="25a13-252">For example, if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="25a13-253">你可能必须在 contoso.com 的主站点的一个项目并在 contoso.com/blog 的博客的另一个项目。</span><span class="sxs-lookup"><span data-stu-id="25a13-253">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="25a13-254">博客应用程序是子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="25a13-254">The blog application is in a subfolder.</span></span> <span data-ttu-id="25a13-255">如果你选择删除目标位置的其他文件部署主站点时，将删除博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="25a13-255">If you select Remove additional files at destination when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="25a13-256">有关其他示例，你的应用程序\_数据文件夹可能会意外删除。</span><span class="sxs-lookup"><span data-stu-id="25a13-256">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="25a13-257">某些数据库，例如 SQL Server Compact 数据库文件存储在应用程序\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="25a13-257">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="25a13-258">在初始部署之后你不想保留选择排除的应用程序以便在后续的部署中复制数据库文件\_打包/发布 Web 选项卡上的数据。在执行操作，如果你已删除所选目标位置的其他文件、 数据库文件和应用程序之后\_数据文件夹本身将删除的下次发布。</span><span class="sxs-lookup"><span data-stu-id="25a13-258">After the initial deployment you don't want to keep copying the database files in subsequent deployments so you select  Exclude App\_Data on the Package/Publish Web tab. After you do that, if you have Remove additional files at destination selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="25a13-259">配置成员资格数据库的部署</span><span class="sxs-lookup"><span data-stu-id="25a13-259">Configure deployment for the membership database</span></span>

<span data-ttu-id="25a13-260">以下步骤适用于**DefaultConnection**数据库中**数据库**的对话框中的部分。</span><span class="sxs-lookup"><span data-stu-id="25a13-260">The following steps apply to the **DefaultConnection** database in the **Databases** section of the dialog box.</span></span>

1. <span data-ttu-id="25a13-261">在**远程连接字符串**框中，输入以下指向新的 SQL Server Express 的成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25a13-261">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

    <span data-ttu-id="25a13-262">在部署过程会将此连接字符串置于部署的 Web.config 文件因为**在运行时使用此连接字符串**选择。</span><span class="sxs-lookup"><span data-stu-id="25a13-262">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="25a13-263">你还可以获得的连接字符串来**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="25a13-263">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="25a13-264">在**服务器资源管理器**，展开**数据连接**和选择 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**数据库，然后从**属性**窗口复制**连接字符串**值。</span><span class="sxs-lookup"><span data-stu-id="25a13-264">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="25a13-265">连接字符串，将具有一个可以删除的其他设置： `Pooling=False`。</span><span class="sxs-lookup"><span data-stu-id="25a13-265">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>
2. <span data-ttu-id="25a13-266">选择**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="25a13-266">Select **Update database**.</span></span>

    <span data-ttu-id="25a13-267">这将导致在部署过程在目标数据库中创建的数据库架构。</span><span class="sxs-lookup"><span data-stu-id="25a13-267">This will cause the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="25a13-268">在以下步骤中指定你需要运行其他脚本： 一个用于授予到默认应用程序池，另一个用于部署数据的数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="25a13-268">In the following steps you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>
3. <span data-ttu-id="25a13-269">单击**配置数据库更新**。</span><span class="sxs-lookup"><span data-stu-id="25a13-269">Click **Configure database updates**.</span></span>
4. <span data-ttu-id="25a13-270">在**配置数据库更新**对话框中，单击**添加 SQL 脚本**然后导航到*Grant.sql*你前面保存在解决方案文件夹中的脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-270">In the **Configure Database Updates** dialog box, click **Add SQL Script** and then navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>
5. <span data-ttu-id="25a13-271">重复此过程以添加*aspnet 数据 dev.sql*脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-271">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

    ![为成员资格数据库配置数据库更新](deploying-to-iis/_static/image16.png)
6. <span data-ttu-id="25a13-273">单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="25a13-273">Click **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="25a13-274">配置应用程序数据库的部署</span><span class="sxs-lookup"><span data-stu-id="25a13-274">Configure deployment for the application database</span></span>

<span data-ttu-id="25a13-275">当 Visual Studio 检测到实体框架`DbContext`类，它创建中的条目**数据库**部分**执行 Code First 迁移**复选框，而不是**更新数据库**复选框。</span><span class="sxs-lookup"><span data-stu-id="25a13-275">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="25a13-276">对于本教程将使用该复选框以指定 Code First 迁移部署。</span><span class="sxs-lookup"><span data-stu-id="25a13-276">For this tutorial you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="25a13-277">在某些情况下，你可能使用`DbContext`数据库，但你想要使用 dbDacFx 提供程序而不是迁移部署数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-277">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="25a13-278">在这种情况下，请参阅[如何部署没有迁移的 Code First 数据库？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) MSDN 上的 ASP.NET Web 部署常见问题中。</span><span class="sxs-lookup"><span data-stu-id="25a13-278">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="25a13-279">以下步骤适用于**SchoolContext**数据库中**数据库**的对话框中的部分。</span><span class="sxs-lookup"><span data-stu-id="25a13-279">The following steps apply to the **SchoolContext** database in the **Databases** section of the dialog box.</span></span>

1. <span data-ttu-id="25a13-280">在**远程连接字符串**框中，输入以下指向新的 SQL Server Express 应用程序数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25a13-280">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

    [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

    <span data-ttu-id="25a13-281">在部署过程会将此连接字符串置于部署的 Web.config 文件因为**在运行时使用此连接字符串**选择。</span><span class="sxs-lookup"><span data-stu-id="25a13-281">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="25a13-282">你还可以获得从应用程序数据库连接字符串**服务器资源管理器**相同的方式获取成员资格数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25a13-282">You can also get the application database connection string from **Server Explorer** the same way you got the membership database connection string.</span></span>
2. <span data-ttu-id="25a13-283">选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="25a13-283">Select **Execute Code First Migrations (runs on application start)**.</span></span>

    <span data-ttu-id="25a13-284">此选项将导致配置已部署的 Web.config 文件，以指定部署过程`MigrateDatabaseToLatestVersion`初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="25a13-284">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="25a13-285">此初始值设定项应用程序部署后首次访问数据库时，自动将数据库更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="25a13-285">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="25a13-286">配置发布配置文件转换</span><span class="sxs-lookup"><span data-stu-id="25a13-286">Configure publish profile transforms</span></span>

1. <span data-ttu-id="25a13-287">单击**关闭**，然后单击**是**当系统询问你是否要保存更改。</span><span class="sxs-lookup"><span data-stu-id="25a13-287">Click **Close**, and then click **Yes** when you are asked if you want to save changes.</span></span>
2. <span data-ttu-id="25a13-288">在**解决方案资源管理器**，展开**属性**，展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="25a13-288">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>
3. <span data-ttu-id="25a13-289">Rright 单击*Test.pubxml，* ，然后单击**添加配置转换**。</span><span class="sxs-lookup"><span data-stu-id="25a13-289">Rright-click *Test.pubxml,* and then click **Add Config Transform**.</span></span>

    ![添加配置转换菜单](deploying-to-iis/_static/image17.png)

    <span data-ttu-id="25a13-291">Visual Studio 将创建*Web.Test.config*转换文件并将其打开。</span><span class="sxs-lookup"><span data-stu-id="25a13-291">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>
4. <span data-ttu-id="25a13-292">在*Web.Test.config*转换文件中，插入以下代码打开后立即配置标记。</span><span class="sxs-lookup"><span data-stu-id="25a13-292">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

    [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="25a13-293">当使用测试发布配置文件时，此转换设置为"Test"的环境指示器。</span><span class="sxs-lookup"><span data-stu-id="25a13-293">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="25a13-294">在已部署的站点将在"Contoso 大学"H1 标题后看到"（测试）"。</span><span class="sxs-lookup"><span data-stu-id="25a13-294">In the deployed site you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>
5. <span data-ttu-id="25a13-295">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="25a13-295">Save and close the file.</span></span>
6. <span data-ttu-id="25a13-296">右键单击*Web.Test.config*文件并单击**预览转换**以确保的转换编码时产生预期的更改。</span><span class="sxs-lookup"><span data-stu-id="25a13-296">Right-click the *Web.Test.config* file and click **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="25a13-297">**Web.config 预览**窗口中显示的应用同时结果*Web.Release.config*转换和*Web.Test.config*转换。</span><span class="sxs-lookup"><span data-stu-id="25a13-297">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="25a13-298">预览部署更新</span><span class="sxs-lookup"><span data-stu-id="25a13-298">Preview the deployment updates</span></span>

1. <span data-ttu-id="25a13-299">打开**发布 Web**向导重新 (右键单击 ContosoUniversity 项目并单击**发布**)。</span><span class="sxs-lookup"><span data-stu-id="25a13-299">Open the **Publish Web** wizard again (right-click the ContosoUniversity project and click **Publish**).</span></span>
2. <span data-ttu-id="25a13-300">在**预览**选项卡上，请确保**测试**配置文件为仍然选择，然后单击**开始预览**以查看将复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="25a13-300">In the **Preview** tab, make sure that the **Test** profile is still selected, and then click **Start Preview** to see a list of the files that will be copied.</span></span>

    ![预览按钮](deploying-to-iis/_static/image18.png)

    ![发布预览](deploying-to-iis/_static/image19.png)

    <span data-ttu-id="25a13-303">您也可以单击**预览版数据库**链接以查看将在成员资格数据库中运行的脚本。</span><span class="sxs-lookup"><span data-stu-id="25a13-303">You can also click the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="25a13-304">（任何脚本为不运行 Code First 迁移部署，因此无需进行任何应用程序数据库预览。）</span><span class="sxs-lookup"><span data-stu-id="25a13-304">(No scripts are run for Code First Migrations deployment, so there is nothing to preview for the application database.)</span></span>
3. <span data-ttu-id="25a13-305">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="25a13-305">Click **Publish**.</span></span>

    <span data-ttu-id="25a13-306">如果在管理员模式下，Visual Studio 不是，你可能会指示权限错误的错误消息。</span><span class="sxs-lookup"><span data-stu-id="25a13-306">If Visual Studio is not in administrator mode, you might get an error message that indicates a permissions error.</span></span> <span data-ttu-id="25a13-307">在这种情况下，关闭 Visual Studio，在管理员模式下打开它并尝试再次发布。</span><span class="sxs-lookup"><span data-stu-id="25a13-307">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

    <span data-ttu-id="25a13-308">在管理员模式下，Visual Studio 是否**输出**窗口报表成功生成和发布。</span><span class="sxs-lookup"><span data-stu-id="25a13-308">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

    ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

    <span data-ttu-id="25a13-310">如果你输入中的 URL**目标 URL**发布配置文件上的框**连接**选项卡上，浏览器将自动打开到 Contoso 大学主页在 IIS 中在本地计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="25a13-310">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on the local computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="25a13-311">在测试环境中测试</span><span class="sxs-lookup"><span data-stu-id="25a13-311">Test in the test environment</span></span>

<span data-ttu-id="25a13-312">请注意环境指示器，显示"（测试）"而不是"（开发）"，其中显示*Web.config*环境指示器的转换是否成功。</span><span class="sxs-lookup"><span data-stu-id="25a13-312">Notice that the environment indicator shows "(Test)" instead of "(Dev)", which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="25a13-313">运行**教师**页以验证 Code First 种子教师数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="25a13-313">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="25a13-314">当选中此页时，可能需要几分钟才能加载，因为 Code First 创建数据库，然后运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="25a13-314">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="25a13-315">（它未执行操作，因为应用程序未尝试访问数据库尚未年在主页上。）</span><span class="sxs-lookup"><span data-stu-id="25a13-315">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="25a13-316">单击**学生**选项卡以验证是否已部署的数据库具有任何学生。</span><span class="sxs-lookup"><span data-stu-id="25a13-316">Click the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="25a13-317">选择**添加学生**从**学生**菜单上，添加一名学生，，然后查看在新的学生**学生**页以验证是否可以成功写入到数据库.</span><span class="sxs-lookup"><span data-stu-id="25a13-317">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database.</span></span>

<span data-ttu-id="25a13-318">从**课程**菜单上，选择**更新信用额度**。</span><span class="sxs-lookup"><span data-stu-id="25a13-318">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="25a13-319">**更新信用额度**页需要管理员权限，因此**Log In**显示页。</span><span class="sxs-lookup"><span data-stu-id="25a13-319">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="25a13-320">输入你创建更早版本 （"admin"和"devpwd"） 的管理员帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="25a13-320">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="25a13-321">**更新信用额度**页面显示时，该验证你在前面的教程中创建的管理员帐户已正确部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="25a13-321">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="25a13-322">验证*Elmah*文件夹中存在*c:\inetpub\wwwroot\ContosoUniversity*与只会在其中将占位符文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="25a13-322">Verify that an *Elmah* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="25a13-323">对于 Code First 迁移查看自动 Web.config 更改</span><span class="sxs-lookup"><span data-stu-id="25a13-323">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="25a13-324">打开*Web.config*在已部署的应用程序中的文件*C:\inetpub\wwwroot\ContosoUniversity* ，你可以看到部署过程自动配置 Code First 迁移到其中将数据库更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="25a13-324">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="25a13-325">在部署过程还创建新的连接字符串的代码优先迁移来更新数据库架构的以独占方式使用：</span><span class="sxs-lookup"><span data-stu-id="25a13-325">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 连接字符串](deploying-to-iis/_static/image22.png)

<span data-ttu-id="25a13-327">此额外的连接字符串，可指定一个用户帐户对数据库架构更新和应用程序数据访问的其他用户帐户。</span><span class="sxs-lookup"><span data-stu-id="25a13-327">This additional connection string enables you to specify one user account for database schema updates, and a different user account for application data access.</span></span> <span data-ttu-id="25a13-328">例如，你可能会分配**db\_所有者**Code First 迁移角色和**db\_datareader**和**db\_datawriter**到应用程序的角色。</span><span class="sxs-lookup"><span data-stu-id="25a13-328">For example, you could assign the **db\_owner** role to Code First Migrations, and **db\_datareader** and **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="25a13-329">这是一种常见的深层防御模式，可防止在应用程序不能更改数据库架构中的潜在恶意代码。</span><span class="sxs-lookup"><span data-stu-id="25a13-329">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="25a13-330">（例如，这可能会发生在成功的 SQL 注入式攻击。）这些教程不使用此模式。</span><span class="sxs-lookup"><span data-stu-id="25a13-330">(For example, this might happen in a successful SQL injection attack.) This pattern is not used by these tutorials.</span></span> <span data-ttu-id="25a13-331">如果你想要在你的方案中实现此模式，可以通过执行以下步骤来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="25a13-331">If you want to implement this pattern in your scenario, you can do it by performing the following steps:</span></span>

1. <span data-ttu-id="25a13-332">在**设置**选项卡**发布 Web**向导中，输入完整的数据库架构更新权限，使用指定的用户的连接字符串，然后清除**使用此连接字符串在运行时**复选框。</span><span class="sxs-lookup"><span data-stu-id="25a13-332">In the **Settings** tab of the **Publish Web** wizard, enter the connection string that specifies a user with full database schema update permissions, and clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="25a13-333">在已部署的 Web.config 文件中，这将成为`DatabasePublish`连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25a13-333">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>
2. <span data-ttu-id="25a13-334">创建 Web.config 文件转换为你想要在运行时使用的应用程序的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25a13-334">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="25a13-335">总结</span><span class="sxs-lookup"><span data-stu-id="25a13-335">Summary</span></span>

<span data-ttu-id="25a13-336">你现在已在开发计算机上部署到 IIS 应用程序，并且存在测试。</span><span class="sxs-lookup"><span data-stu-id="25a13-336">You have now deployed your application to IIS on your development computer and tested it there.</span></span>

![在测试中的主页](deploying-to-iis/_static/image23.png)

<span data-ttu-id="25a13-338">这将验证部署过程将应用程序的内容复制到正确的位置 （不包括你确实不想要部署的文件），并还该 Web 部署已配置的 IIS 正确在部署过程。</span><span class="sxs-lookup"><span data-stu-id="25a13-338">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy), and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="25a13-339">在下一步的教程中，你将运行一个查找尚未完成的部署任务的详细测试： 上设置文件夹权限*Elmah*文件夹。</span><span class="sxs-lookup"><span data-stu-id="25a13-339">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elmah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="25a13-340">详细信息</span><span class="sxs-lookup"><span data-stu-id="25a13-340">More information</span></span>

<span data-ttu-id="25a13-341">在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="25a13-341">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="25a13-342">[IIS Express 概述](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="25a13-342">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="25a13-343">[引入了 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的博客上。</span><span class="sxs-lookup"><span data-stu-id="25a13-343">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="25a13-344">[Web 服务器在 Visual Studio 中的，对于 ASP.NET Web 项目](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25a13-344">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="25a13-345">[核心差异之间 IIS 和 ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 站点上。</span><span class="sxs-lookup"><span data-stu-id="25a13-345">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="25a13-346">在中等信任中运行你的应用程序时，可能出现哪些问题有关的信息，请参阅[在中等信任环境中承载 ASP.NET 应用程序](http://www.4guysfromrolla.com/articles/100307-1.aspx)上从 Rolla 站点 4 专家。</span><span class="sxs-lookup"><span data-stu-id="25a13-346">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the 4 Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="25a13-347">[上一页](project-properties.md)
> [下一页](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="25a13-347">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
