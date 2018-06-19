---
uid: whitepapers/side-by-side-with-10
title: .NET framework 1.0 和 1.1 的 ASP.NET 并行执行 |Microsoft 文档
author: rick-anderson
description: 该白皮书介绍了如何在您允许 ASP.NET Web 应用程序框架的任一版本上运行的计算机上安装.NET 1.0 和.NET 1.1...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: 939b04d440955b184bf5f4c40a2ef8175641edfa
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530176"
---
<a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="82b5c-103">.NET framework 1.0 和 1.1 的 ASP.NET 并行执行</span><span class="sxs-lookup"><span data-stu-id="82b5c-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>
====================
> <span data-ttu-id="82b5c-104">该白皮书介绍了如何在您允许 ASP.NET Web 应用程序框架的任一版本上运行的计算机上安装.NET 1.0 和.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="82b5c-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="82b5c-105">适用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="82b5c-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>


<span data-ttu-id="82b5c-106">在 ASP.NET 中，应用程序被认为时它们安装在同一台计算机，但使用不同版本的.NET Framework 并行运行。</span><span class="sxs-lookup"><span data-stu-id="82b5c-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="82b5c-107">以下主题介绍如何配置 ASP.NET 应用程序的并行执行，并提供详细的步骤：</span><span class="sxs-lookup"><span data-stu-id="82b5c-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="82b5c-108">维护到.NET Framework 1.0 版在安装过程中的 Web 应用程序的映射</span><span class="sxs-lookup"><span data-stu-id="82b5c-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="82b5c-109">映射到.NET Framework 的特定版本的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="82b5c-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="82b5c-110">查找使用网站的.NET framework 版本</span><span class="sxs-lookup"><span data-stu-id="82b5c-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="82b5c-111">传统上，当更新的计算机上的组件或应用程序后，较旧版本删除和替换为较新版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="82b5c-112">如果新的版本不兼容的以前版本，这通常会中断其他应用程序使用的组件或应用程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="82b5c-113">.NET Framework 支持的并行执行，从而允许多个版本的程序集或应用程序在同一台计算机上安装在同一时间。</span><span class="sxs-lookup"><span data-stu-id="82b5c-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="82b5c-114">可以同时安装多个版本，因为托管应用程序可以选择要使用而不会影响使用不同版本的应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="82b5c-115">默认情况下，在.NET Framework 1.1 版中，安装过程中所有现有的 ASP.NET 应用程序自动重新配置为使用.NET Framework 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="82b5c-116">如果您不希望你的 ASP.NET 应用程序，默认为.NET Framework 1.1，请单击[此处](#1)若要了解如何防止这种情况在安装过程。</span><span class="sxs-lookup"><span data-stu-id="82b5c-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="82b5c-117">如果你更新到.NET Framework 1.1 的 Web 服务器，并希望一个或多个 Web 应用程序运行.NET Framework 1.0，你需要更新 Internet 信息服务 (IIS) 的脚本映射。</span><span class="sxs-lookup"><span data-stu-id="82b5c-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="82b5c-118">脚本映射是映射到.NET Framework 的版本特定的 Web 应用程序的.aspx 文件扩展名的机制。</span><span class="sxs-lookup"><span data-stu-id="82b5c-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="82b5c-119">单击[此处](#2)若要了解如何将映射到.NET Framework 的特定版本的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="82b5c-120">你可以使用 Internet 信息管理器或 ASP.NET IIS 注册工具 (Aspnet\_regiis.exe) 若要了解哪些.NET Framework 版本运行特定 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="82b5c-121">单击[此处](#3)若要了解如何查找网站正在使用的.NET framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="82b5c-122">导入其中时迁移到.NET Framework 1.1 之一是每个版本的.NET Framework 使用其自己的 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="82b5c-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="82b5c-123">因此，如果 Web 管理员具有对 Machine.config 文件中进行了更改，这些更改必须迁移到.NET Framework 1.1 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="82b5c-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="82b5c-124">维护.NET Framework 1.0 到在安装过程中的 Web 应用程序的映射</span><span class="sxs-lookup"><span data-stu-id="82b5c-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="82b5c-125">默认情况下，所有现有的 ASP.NET 应用程序自动重新配置在安装过程中使用.NET Framework 的较新版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="82b5c-126">使用.NET Framework 的较新版本，应用程序可以充分利用的改进和新功能包含在新版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="82b5c-127">同时，可能希望精确地控制哪些应用程序的 Web 管理员，均已更新，可能会阻止自动重新映射的所有现有的 ASP.NET 应用程序在.NET framework 安装过程。</span><span class="sxs-lookup"><span data-stu-id="82b5c-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="82b5c-128">若要防止自动重新映射到较新版本的.NET framework 的整个 ASP.NET 应用程序，Web 管理员可以与 Dotnetfx.exe 安装程序使用 /noaspupgrade 命令行选项。</span><span class="sxs-lookup"><span data-stu-id="82b5c-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="82b5c-129">**若要防止总重新映射到较新版本的 ASP.NET 应用程序**</span><span class="sxs-lookup"><span data-stu-id="82b5c-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="82b5c-130">转到**启动**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-130">Go to **Start**.</span></span>
2. <span data-ttu-id="82b5c-131">单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-131">Click on **run**.</span></span>
3. <span data-ttu-id="82b5c-132">键入“cmd”。</span><span class="sxs-lookup"><span data-stu-id="82b5c-132">Type **cmd**.</span></span>
4. <span data-ttu-id="82b5c-133">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="82b5c-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="82b5c-134">从命令提示符处，键入要启动的.NET framework 安装的以下行： **Dotnetfx.exe 无"安装 /noaspupgrade？**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="82b5c-135">单击**是**中 Microsoft.NET Framework 1.1 安装程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="82b5c-136">这将启动.NET Framework 1.1 的安装过程。</span><span class="sxs-lookup"><span data-stu-id="82b5c-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="82b5c-137">映射到.NET Framework 的特定版本的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="82b5c-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="82b5c-138">每个版本的.NET Framework 包括 ASP.NET IIS 注册工具的版本 (Aspnet\_regiis.exe)。</span><span class="sxs-lookup"><span data-stu-id="82b5c-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="82b5c-139">此工具使管理员能够指定.NET Framework 的特定版本下运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="82b5c-140">这被称为映射到.NET Framework 的版本的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="82b5c-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="82b5c-141">管理员必须选择 Aspnet\_regiis.exe 对应于将与 Web 应用程序相关联的.NET framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="82b5c-142">例如，想要指定网站使用.NET Framework 1.1 的管理员必须使用 Aspnet\_regiis.exe 随附.NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="82b5c-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="82b5c-143">Aspnet\_版本 1.0 regiis.exe 位于：</span><span class="sxs-lookup"><span data-stu-id="82b5c-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="82b5c-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705** \aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="82b5c-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="82b5c-145">Aspnet\_regiis.exe 版本 1，1 位于：</span><span class="sxs-lookup"><span data-stu-id="82b5c-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="82b5c-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322-** \aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="82b5c-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="82b5c-147">Aspnet\_regiis.exe 提供脚本映射 Web 应用程序的两个选项：</span><span class="sxs-lookup"><span data-stu-id="82b5c-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="82b5c-148">**-s**设置脚本映射和其子级中路径目录。</span><span class="sxs-lookup"><span data-stu-id="82b5c-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="82b5c-149">**-sn**路径仅中设置的脚本映射。</span><span class="sxs-lookup"><span data-stu-id="82b5c-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="82b5c-150">该路径定义的 Web 应用程序 IIS 元数据路径，定义形式 W3SVC/ROOT / {WebSiteNumber} / {应用程序\_名称}。</span><span class="sxs-lookup"><span data-stu-id="82b5c-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="82b5c-151">例如，对于称为门户位于默认网站下的 Web 应用程序，元数据库路径是 W3SVC/1/根/门户。</span><span class="sxs-lookup"><span data-stu-id="82b5c-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="82b5c-152">请注意你可以使用一个称为元数据库编辑器的工具来获取的元数据库路径。</span><span class="sxs-lookup"><span data-stu-id="82b5c-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="82b5c-153">你可以从 Microsoft 支持网站下载此工具[https://support.microsoft.com/default.aspx?scid=kb;en-us;232068。](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="82b5c-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="82b5c-154">运行 Aspnet\_regiis.exe-s W3SVC/1/根/门户更新门户 IIS 脚本映射和其 subapplication。</span><span class="sxs-lookup"><span data-stu-id="82b5c-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="82b5c-155">运行 Aspnet\_regiis.exe-sn W3SVC/1/根/门户可更新的门户的 IIS 脚本映射，而不会影响门户中的应用程序？ s 子目录。</span><span class="sxs-lookup"><span data-stu-id="82b5c-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="82b5c-156">查找 Web 应用程序使用的.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="82b5c-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="82b5c-157">管理员可以使用 Internet 服务管理器来查找.NET Framework 的版本运行网站。</span><span class="sxs-lookup"><span data-stu-id="82b5c-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="82b5c-158">不同的操作系统版本以不同方式启动 Internet 服务管理器。</span><span class="sxs-lookup"><span data-stu-id="82b5c-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="82b5c-159">若要启动服务管理器，请按照下面列出的步骤。</span><span class="sxs-lookup"><span data-stu-id="82b5c-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="82b5c-160">**启动 Internet 服务管理器**</span><span class="sxs-lookup"><span data-stu-id="82b5c-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="82b5c-161">转到**启动**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-161">Go to **Start**.</span></span>
2. <span data-ttu-id="82b5c-162">单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-162">Click on **run**.</span></span>
3. <span data-ttu-id="82b5c-163">类型**inetmgr**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="82b5c-164">从 Internet 服务管理器中，选择 Web 应用程序想要知道的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="82b5c-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="82b5c-165">Web 应用程序中，右键单击，然后单击**属性。**</span><span class="sxs-lookup"><span data-stu-id="82b5c-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="82b5c-166">从属性窗口中，选择**配置。**</span><span class="sxs-lookup"><span data-stu-id="82b5c-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="82b5c-167">从应用程序映射表中，选择 **.aspx**，然后单击**编辑**。</span><span class="sxs-lookup"><span data-stu-id="82b5c-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="82b5c-168">从**可执行文件**文本框中，查看滚动的版本目录。</span><span class="sxs-lookup"><span data-stu-id="82b5c-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="82b5c-169">如果版本目录为 v.1.1.4322，应用程序映射到.NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="82b5c-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="82b5c-170">相反，如果版本目录为 v1.0.3705，应用程序将映射到.NET Framework 1.0。</span><span class="sxs-lookup"><span data-stu-id="82b5c-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
