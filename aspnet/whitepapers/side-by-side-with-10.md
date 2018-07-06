---
uid: whitepapers/side-by-side-with-10
title: .NET framework 1.0 和 1.1 的 ASP.NET 并行执行 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍了如何允许帧任一版本上运行的 ASP.NET Web 应用程序在计算机上安装.NET 1.0 和.NET 1.1...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: 1018845e3d2c6603732bfbbde78f4a9183e49d5d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808390"
---
<a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="51671-103">.NET framework 1.0 和 1.1 的 ASP.NET 并行执行</span><span class="sxs-lookup"><span data-stu-id="51671-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>
====================
> <span data-ttu-id="51671-104">本白皮书介绍了如何允许任一版本的 framework 上运行的 ASP.NET Web 应用程序在计算机上安装.NET 1.0 和.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="51671-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="51671-105">适用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="51671-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>


<span data-ttu-id="51671-106">在 ASP.NET 中，应用程序被称为时它们安装在同一台计算机上，但使用不同版本的.NET Framework 并行运行。</span><span class="sxs-lookup"><span data-stu-id="51671-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="51671-107">以下主题介绍如何配置 ASP.NET 应用程序通过并行执行，并提供详细的步骤：</span><span class="sxs-lookup"><span data-stu-id="51671-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="51671-108">维护在安装过程中的 Web 应用程序映射到.NET Framework 1.0 版</span><span class="sxs-lookup"><span data-stu-id="51671-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="51671-109">将映射到特定版本的.NET Framework 的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="51671-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="51671-110">查找使用网站上的.NET framework 版本</span><span class="sxs-lookup"><span data-stu-id="51671-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="51671-111">传统上，当更新的计算机上的组件或应用程序后，较旧版本删除并替换为较新版本。</span><span class="sxs-lookup"><span data-stu-id="51671-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="51671-112">如果新版本不是与以前的版本兼容的通常会中断其他应用程序使用的组件或应用程序。</span><span class="sxs-lookup"><span data-stu-id="51671-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="51671-113">.NET Framework 的并行执行，从而允许多个版本的程序集或在同一时间在同一台计算机上安装应用程序，用于提供支持。</span><span class="sxs-lookup"><span data-stu-id="51671-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="51671-114">可以同时安装多个版本，因为托管应用程序可以选择要使用而不会影响使用不同版本的应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="51671-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="51671-115">默认情况下，在.NET Framework 版本 1.1，安装过程中所有现有的 ASP.NET 应用程序会自动重新配置为使用.NET Framework 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="51671-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="51671-116">如果不希望使 ASP.NET 应用程序默认为.NET Framework 1.1，请单击[此处](#1)若要了解如何防止这种在安装过程。</span><span class="sxs-lookup"><span data-stu-id="51671-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="51671-117">如果你更新到.NET Framework 1.1 的 Web 服务器，并想一个或多个 Web 应用程序运行.NET Framework 1.0，您需要更新 Internet 信息服务 (IIS) 脚本映射。</span><span class="sxs-lookup"><span data-stu-id="51671-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="51671-118">脚本映射是映射到.NET Framework 的版本特定的 Web 应用程序的.aspx 文件扩展名的机制。</span><span class="sxs-lookup"><span data-stu-id="51671-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="51671-119">单击[此处](#2)若要了解如何将映射到特定版本的.NET Framework 的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="51671-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="51671-120">可以使用 Internet 信息管理器或 ASP.NET IIS 注册工具 (Aspnet\_regiis.exe) 若要查找特定的 Web 应用程序运行的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="51671-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="51671-121">单击[此处](#3)若要了解如何查找使用网站上的.NET framework 版本。</span><span class="sxs-lookup"><span data-stu-id="51671-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="51671-122">一个导入中不考虑迁移到.NET Framework 1.1 时是每个版本的.NET Framework 使用其自己的 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="51671-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="51671-123">因此，如果 Web 管理员已到 Machine.config 文件发生更改，这些更改必须迁移到.NET Framework 1.1 Machine.config 文件。</span><span class="sxs-lookup"><span data-stu-id="51671-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="51671-124">维护.NET Framework 1.0 到在安装过程中的 Web 应用程序的映射</span><span class="sxs-lookup"><span data-stu-id="51671-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="51671-125">默认情况下，所有现有的 ASP.NET 应用程序会自动重新配置为使用.NET Framework 的较新版本的安装过程。</span><span class="sxs-lookup"><span data-stu-id="51671-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="51671-126">使用.NET Framework 的较新版本，应用程序可以充分利用的改进和新版本中包括的新功能。</span><span class="sxs-lookup"><span data-stu-id="51671-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="51671-127">同时，Web 管理员，他可能希望精确地控制哪些应用程序均已更新，可能会阻止自动重新映射的所有现有的 ASP.NET 应用程序在安装.NET Framework 的过程。</span><span class="sxs-lookup"><span data-stu-id="51671-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="51671-128">若要防止自动重新映射到较新版本的.NET Framework 的整个 ASP.NET 应用程序，Web 管理员可以使用 Dotnetfx.exe 安装程序使用 /noaspupgrade 命令行选项。</span><span class="sxs-lookup"><span data-stu-id="51671-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="51671-129">**若要防止总重新映射到较新版本的 ASP.NET 应用程序**</span><span class="sxs-lookup"><span data-stu-id="51671-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="51671-130">转到**启动**。</span><span class="sxs-lookup"><span data-stu-id="51671-130">Go to **Start**.</span></span>
2. <span data-ttu-id="51671-131">单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="51671-131">Click on **run**.</span></span>
3. <span data-ttu-id="51671-132">键入“cmd”。</span><span class="sxs-lookup"><span data-stu-id="51671-132">Type **cmd**.</span></span>
4. <span data-ttu-id="51671-133">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="51671-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="51671-134">从命令提示符处，键入要开始的.NET framework 安装的以下行： **Dotnetfx.exe 无"安装 /noaspupgrade？**。</span><span class="sxs-lookup"><span data-stu-id="51671-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="51671-135">单击**是**中 Microsoft.NET Framework 1.1 安装程序。</span><span class="sxs-lookup"><span data-stu-id="51671-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="51671-136">这将启动.NET Framework 1.1 的安装过程。</span><span class="sxs-lookup"><span data-stu-id="51671-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="51671-137">将映射到特定版本的.NET Framework 的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="51671-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="51671-138">每个版本的.NET Framework 包括 ASP.NET IIS 注册工具的版本 (Aspnet\_regiis.exe)。</span><span class="sxs-lookup"><span data-stu-id="51671-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="51671-139">此工具使管理员可以指定特定版本的.NET Framework 下运行的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="51671-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="51671-140">这被称为映射到.NET framework 版本的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="51671-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="51671-141">管理员必须选择 Aspnet\_regiis.exe 将与 Web 应用程序相关联的.NET framework 的版本相对应。</span><span class="sxs-lookup"><span data-stu-id="51671-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="51671-142">例如，想要指定网站上使用.NET Framework 1.1 的管理员必须使用 Aspnet\_regiis.exe 随附.NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="51671-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="51671-143">Aspnet\_regiis.exe 对于 1.0 版位于：</span><span class="sxs-lookup"><span data-stu-id="51671-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="51671-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="51671-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="51671-145">Aspnet\_regiis.exe 版本 1，1 位于：</span><span class="sxs-lookup"><span data-stu-id="51671-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="51671-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="51671-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="51671-147">Aspnet\_regiis.exe 提供两个映射的 Web 应用程序的脚本选项：</span><span class="sxs-lookup"><span data-stu-id="51671-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="51671-148">**-s**设置的脚本映射和及其子路径中的目录。</span><span class="sxs-lookup"><span data-stu-id="51671-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="51671-149">**-sn**只能在路径中设置的脚本映射。</span><span class="sxs-lookup"><span data-stu-id="51671-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="51671-150">该路径定义 Web 应用程序 IIS 元数据路径，W3SVC/根的窗体中定义 / {WebSiteNumber} / {应用程序\_名称}。</span><span class="sxs-lookup"><span data-stu-id="51671-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="51671-151">例如，对于名为门户位于默认网站下的 Web 应用程序，元数据库路径是 W3SVC/1/根目录/门户。</span><span class="sxs-lookup"><span data-stu-id="51671-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="51671-152">请注意您可以使用一个称为配置数据库编辑器工具，若要获取的元数据库路径。</span><span class="sxs-lookup"><span data-stu-id="51671-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="51671-153">可以从 Microsoft 支持网站下载此工具[ https://support.microsoft.com/default.aspx?scid=kb; en-我们; 232068。](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="51671-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="51671-154">运行 Aspnet\_regiis.exe-s W3SVC/1/根目录/门户更新门户 IIS 脚本映射和其 subapplication。</span><span class="sxs-lookup"><span data-stu-id="51671-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="51671-155">运行 Aspnet\_regiis.exe-sn W3SVC/1/根目录/门户更新门户的 IIS 脚本映射，而不会影响在门户中的应用程序？ s 子目录。</span><span class="sxs-lookup"><span data-stu-id="51671-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="51671-156">查找 Web 应用程序使用的.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="51671-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="51671-157">管理员可以使用 Internet 服务管理器来查找 Web 站点运行的.NET framework 版本。</span><span class="sxs-lookup"><span data-stu-id="51671-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="51671-158">不同的操作系统版本以不同方式启动 Internet 服务管理器。</span><span class="sxs-lookup"><span data-stu-id="51671-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="51671-159">若要启动服务管理器，请执行下面列出的步骤。</span><span class="sxs-lookup"><span data-stu-id="51671-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="51671-160">**启动 Internet 服务管理器**</span><span class="sxs-lookup"><span data-stu-id="51671-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="51671-161">转到**启动**。</span><span class="sxs-lookup"><span data-stu-id="51671-161">Go to **Start**.</span></span>
2. <span data-ttu-id="51671-162">单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="51671-162">Click on **run**.</span></span>
3. <span data-ttu-id="51671-163">类型**inetmgr**。</span><span class="sxs-lookup"><span data-stu-id="51671-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="51671-164">从 Internet 服务管理器中，选择你想要知道的.NET Framework 版本的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="51671-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="51671-165">Web 应用程序中，右键单击，然后单击**属性。**</span><span class="sxs-lookup"><span data-stu-id="51671-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="51671-166">从属性窗口中，选择**配置。**</span><span class="sxs-lookup"><span data-stu-id="51671-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="51671-167">从应用程序映射表中，选择 **.aspx**，然后单击**编辑**。</span><span class="sxs-lookup"><span data-stu-id="51671-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="51671-168">从**可执行文件**文本框中，查看通过滚动版本目录。</span><span class="sxs-lookup"><span data-stu-id="51671-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="51671-169">如果版本目录 v.1.1.4322，应用程序映射到.NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="51671-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="51671-170">相反，如果版本目录 v1.0.3705，应用程序映射到.NET Framework 1.0。</span><span class="sxs-lookup"><span data-stu-id="51671-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
