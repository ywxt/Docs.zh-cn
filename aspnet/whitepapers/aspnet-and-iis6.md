---
uid: whitepapers/aspnet-and-iis6
title: 向 IIS 6.0 中运行 ASP.NET 1.1 |Microsoft 文档
author: rick-anderson
description: 虽然 Windows Server 2003 包含 IIS 6.0 和 ASP.NET 1.1，这些组件在默认情况下处于禁用状态。 该白皮书介绍了如何启用 IIS 6.0...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 1fcac7b8bc295ccf4e36189295b6bc2e4d328623
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530106"
---
<a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="dfb6b-104">向 IIS 6.0 中运行 ASP.NET 1.1</span><span class="sxs-lookup"><span data-stu-id="dfb6b-104">Running ASP.NET 1.1 with IIS 6.0</span></span>
====================
> <span data-ttu-id="dfb6b-105">虽然 Windows Server 2003 包含 IIS 6.0 和 ASP.NET 1.1，这些组件在默认情况下处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="dfb6b-106">本白皮书介绍如何启用 IIS 6.0 和 ASP.NET 1.1 版中，并建议多个配置设置以从 IIS 和 ASP.NET 中获取最佳性能。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="dfb6b-107">适用于 ASP.NET 1.1 和 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>


<span data-ttu-id="dfb6b-108">ASP.NET 1.1 附带还包括最新版本的 Internet 信息服务器 (IIS) 6.0 版的 Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="dfb6b-109">IIS 6.0 和 ASP.NET 1.1 旨在无缝集成，ASP.NET 现在默认值为新的 IIS 6.0 辅助进程模型。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="dfb6b-110">默认情况下不安装 ASP.NET 1.1</span><span class="sxs-lookup"><span data-stu-id="dfb6b-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="dfb6b-111">与以前版本的 Microsoft 的服务器操作系统，不同的是 Internet 信息服务器 (IIS) 未启用默认设置。也不是 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="dfb6b-112">有两个选项用于启用 IIS:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="dfb6b-113">启用 IIS，选项 #1-配置服务器向导</span><span class="sxs-lookup"><span data-stu-id="dfb6b-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="dfb6b-114">Windows Server 2003 附带新配置服务器向导来帮助你正确配置服务器所需模式。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="dfb6b-115">若要启动向导-请注意，若要运行的向导必须以管理员身份的身份登录，请转到： 启动 |程序 |管理工具和选择配置服务器。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="dfb6b-116">选择后，你应看到配置服务器向导开始屏幕：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="dfb6b-117">单击下一步&gt;:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="dfb6b-118">单击下一步&gt;</span><span class="sxs-lookup"><span data-stu-id="dfb6b-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="dfb6b-119">在此屏幕上，你将需要选择应用程序服务器 （IIS，ASP.NET） 作为配置的选项。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="dfb6b-120">单击下一步&gt;。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="dfb6b-121">选择后将服务器配置为应用程序服务器，此屏幕将显示提示应安装哪些其他功能。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="dfb6b-122">默认情况下选择任何选项。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-122">Neither option is selected by default.</span></span> <span data-ttu-id="dfb6b-123">若要自动启用 ASP.NET，你需要选择启用 ASP。NET。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="dfb6b-124">单击下一步&gt;。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="dfb6b-125">此屏幕显示要安装的选项。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="dfb6b-126">单击下一步&gt;。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="dfb6b-127">在安装你选择的选项时，你将看到此屏幕。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="dfb6b-128">它是正常的请参阅框显示为正在安装服务的其他对话框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="dfb6b-129">可能此外会提示你为 Windows 2003 Server 安装 CD 的位置。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="dfb6b-130">单击下一步&gt;完成时。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="dfb6b-131">单击完成-Windows Server 2003 现在已配置为支持 IIS 6.0 和 ASP.NET 1.1 版。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="dfb6b-132">启用 IIS，选项 #2-手动配置 IIS 和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dfb6b-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="dfb6b-133">如果不希望使用配置服务器向导您可以选择安装 IIS 6.0 和 ASP.NET 1.1 使用添加或删除程序从控制面板。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="dfb6b-134">首次打开控制面板:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="dfb6b-135">接下来，单击添加/删除 Windows 组件这将打开 Windows 组件向导:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="dfb6b-136">突出显示并检查应用程序服务器，然后单击详细信息？</span><span class="sxs-lookup"><span data-stu-id="dfb6b-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="dfb6b-137">按钮：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="dfb6b-138">若要安装 ASP.NET，请检查 ASP。NET。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="dfb6b-139">单击确定以返回到 Windows 组件向导。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="dfb6b-140">单击下一步&gt;从 Windows 组件向导以开始安装：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="dfb6b-141">它是正常的请参阅框显示为正在安装服务的其他对话框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="dfb6b-142">可能此外会提示你为 Windows 2003 Server 安装 CD 的位置。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="dfb6b-143">安装完成后你将看到 Windows 组件向导的最后一个屏幕：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="dfb6b-144">IIS 6.0 和 ASP.NET 1.1 现已配置并且可用。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="dfb6b-145">建议的设置</span><span class="sxs-lookup"><span data-stu-id="dfb6b-145">Recommended Settings</span></span>

<span data-ttu-id="dfb6b-146">使用 IIS 6.0 中运行 ASP.NET 1.1 时有多个配置设置，建议从 ASP.NET 获得最佳性能：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="dfb6b-147">配置辅助进程内存限制</span><span class="sxs-lookup"><span data-stu-id="dfb6b-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="dfb6b-148">配置辅助进程回收</span><span class="sxs-lookup"><span data-stu-id="dfb6b-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="dfb6b-149">配置辅助进程内存限制</span><span class="sxs-lookup"><span data-stu-id="dfb6b-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="dfb6b-150">默认情况下 IIS 6.0 不允许 IIS 使用的内存量设置限制。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="dfb6b-151">ASP。NET 的缓存功能依赖于内存的限制，以便从内存中缓存可以主动删除未使用的项。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="dfb6b-152">建议你配置的内存回收 IIS 6.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="dfb6b-153">若要配置此打开的 Internet Information Services 管理器 (开始 |程序 |管理工具 |Internet Information Services)。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="dfb6b-154">后打开，展开应用程序池文件夹：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="dfb6b-155">每个应用程序池：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="dfb6b-156">例如右键单击应用程序池DefaultAppPool 并选择属性:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="dfb6b-157">接下来，启用单击任何一个的内存回收最大内存使用 （以兆字节为单位）:。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="dfb6b-158">值不应为多个服务器上的物理 （不是虚拟的） 内存量，极佳近似值为 60%的物理内存，即对于具有 512 MB 的物理内存选择 310 的服务器。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="dfb6b-159">建议使用 2 GB 地址空间时，最大值将不超过 800 MB。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="dfb6b-160">如果服务器的内存地址空间为 3 GB，可以最高可达 1，800 MB 的工作进程的最大内存限制：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="dfb6b-161">单击应用和确定退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="dfb6b-162">对于所有可用的应用程序池重复此操作。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="dfb6b-163">配置辅助回收</span><span class="sxs-lookup"><span data-stu-id="dfb6b-163">Configuring worker recycling</span></span>

<span data-ttu-id="dfb6b-164">默认情况下 IIS 6.0 配置以回收其工作进程每 29 个小时。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="dfb6b-165">这是有点主动运行的 ASP.NET 应用程序，建议已禁用的自动工作进程回收。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="dfb6b-166">若要禁用自动工作进程回收，请先打开 Internet Information Services 管理器 (开始 |程序 |管理工具 |Internet Information Services)。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="dfb6b-167">后打开，展开应用程序池文件夹：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="dfb6b-168">每个应用程序池：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-168">For each application pool:</span></span>

1. <span data-ttu-id="dfb6b-169">例如右键单击应用程序池DefaultAppPool 并选择属性:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="dfb6b-170">取消选中回收工作进程 （以分钟为单位）::</span><span class="sxs-lookup"><span data-stu-id="dfb6b-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="dfb6b-171">单击应用和确定退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="dfb6b-172">对于所有可用的应用程序池重复此操作。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="dfb6b-173">授予对文件系统的写访问权限</span><span class="sxs-lookup"><span data-stu-id="dfb6b-173">Granting write access to the file system</span></span>

<span data-ttu-id="dfb6b-174">如果你的应用程序需要写到文件系统的访问权限，并且使用 NTFS 你将需要修改访问控制列表 (ACL) 上的文件夹或文件授予对 ASP.NET 访问权限。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="dfb6b-175">例如，若要授予 ASP.NET 写访问权限 c:\inetpub\wwwroot 首先打开资源管理器并导航到的目录：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="dfb6b-176">接下来，右键单击该目录，例如，wwwroot 并选择属性。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="dfb6b-177">属性对话框打开后，选择安全选项卡：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="dfb6b-178">C:\inetpub\wwwroot\ 目录是一个特殊目录中的特殊 IIS 6.0 组 IIS\_WPG 已授予读取&amp;执行、 列出文件夹内容和读取权限。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="dfb6b-179">但是，若要授予写入权限，您需要单击允许复选框以进行写入：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="dfb6b-180">IIS 6.0 现在对此文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="dfb6b-181">若要授予写权限的其他文件夹，请按照下列步骤-请注意，你可能需要添加 IIS\_WPG 组如果不存在。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="dfb6b-182">授予写权限 IIS\_WPG 将允许任何 ASP.NET 应用程序写入到该目录。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="dfb6b-183">支持与 SQL Server 的集成身份验证</span><span class="sxs-lookup"><span data-stu-id="dfb6b-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="dfb6b-184">集成身份验证允许 SQL Server 利用 Windows NT 身份验证来验证 SQL Server 登录帐户。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="dfb6b-185">这允许用户跳过在标准的 SQL Server 登录过程。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="dfb6b-186">使用此方法时，网络用户可以访问 SQL Server 数据库，而无需提供单独的登录标识或密码，因为 SQL Server 从 Windows NT 网络的安全过程获取的用户和密码信息。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="dfb6b-187">选择用于 ASP.NET 应用程序的集成身份验证是一个不错的选择，因为没有凭据曾经存储在你的应用程序连接字符串。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="dfb6b-188">而是用来连接到 SQL 连接字符串将如下所示：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="dfb6b-189">此连接字符串告知 SQL Server 以使用应用程序尝试访问 SQL Server 的 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="dfb6b-190">在 ASP.NET/IIS 6 的情况下，这将是在 IIS 中的帐户\_WPG 组。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="dfb6b-191">若要启用 SQL Server 和 ASP.NET 之间的集成身份验证，你将需要首先确保 SQL Server 是否配置为集成身份验证或混合模式身份验证-咨询 DBA 以确定这一点。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="dfb6b-192">如果这两种模式之一中有 SQL Server，你可以使用集成身份验证。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="dfb6b-193">打开 SQL Server 企业管理器 (开始 |程序 |Microsoft SQL Server |企业管理器），选择适当的服务器，然后展开安全性文件夹：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="dfb6b-194">如果 BUILTINT\IIS\_WPG 未列出组、 登录名右键单击并选择新建登录名:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="dfb6b-195">在名称: 文本框中输入 [服务器/域名] \IIS\_WPG 或单击省略号按钮以打开 Windows NT 用户/组选取器：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="dfb6b-196">选择在当前计算机的 IIS\_WPG 组，然后单击添加和确定以关闭选择器。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="dfb6b-197">然后，你需要设置为默认数据库和访问数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="dfb6b-198">若要设置的默认数据库选择从下拉列表中，选择以下 Northwind 例如：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="dfb6b-199">接下来，单击数据库访问选项卡：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="dfb6b-200">单击你想要允许访问每个数据库的允许复选框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="dfb6b-201">你还需要选择数据库角色检查 db\_所有者将确保你的登录名具有所有必要的权限管理，使用所选的数据库。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="dfb6b-202">单击确定退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="dfb6b-203">ASP.NET 应用程序现在已配置为支持集成的 SQL Server 身份验证。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="dfb6b-204">不在 IIS 6.0 纯模式下运行 ASP.NET 1.0</span><span class="sxs-lookup"><span data-stu-id="dfb6b-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="dfb6b-205">在 IIS 5 兼容性模式下仅支持 IIS 6.0 上的 ASP.NET 1.0。</span><span class="sxs-lookup"><span data-stu-id="dfb6b-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="dfb6b-206">若要配置在 IIS 5.0 兼容性模式下运行的 ASP.NET 1.0，打开 Internet 服务管理器，右键单击网站并选择属性：</span><span class="sxs-lookup"><span data-stu-id="dfb6b-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="dfb6b-207">切换到服务选项卡，并检查？以 IIS 5.0 隔离模式运行 WWW 服务？:</span><span class="sxs-lookup"><span data-stu-id="dfb6b-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
