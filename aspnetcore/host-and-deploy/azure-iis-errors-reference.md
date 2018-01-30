---
title: "Azure App Service 和 ASP.NET Core 了 IIS 的常见错误参考"
author: guardrex
description: "承载 Azure 应用程序服务和 IIS 上的 ASP.NET Core 应用时，请区分常见错误。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 214f8c616aa65077690757e7805983a77ec4249e
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a><span data-ttu-id="e9059-103">Azure App Service 和 ASP.NET Core 了 IIS 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="e9059-103">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>

<span data-ttu-id="e9059-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="e9059-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="e9059-105">以下不是错误的完整列表。</span><span class="sxs-lookup"><span data-stu-id="e9059-105">The following isn't a complete list of errors.</span></span> <span data-ttu-id="e9059-106">如果你遇到此处未列出的错误[打开一个新问题](https://github.com/aspnet/Docs/issues/new)与再现错误的详细说明。</span><span class="sxs-lookup"><span data-stu-id="e9059-106">If you encounter an error not listed here, [open a new issue](https://github.com/aspnet/Docs/issues/new) with detailed instructions to reproduce the error.</span></span>

## <a name="installer-unable-to-obtain-vc-redistributable"></a><span data-ttu-id="e9059-107">安装程序无法获取 VC++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="e9059-107">Installer unable to obtain VC++ Redistributable</span></span>

* <span data-ttu-id="e9059-108">**安装程序异常：**0x80072efd 或 0x80072f76 - 未指定的错误</span><span class="sxs-lookup"><span data-stu-id="e9059-108">**Installer Exception:** 0x80072efd or 0x80072f76 - Unspecified error</span></span>

* <span data-ttu-id="e9059-109">**安装程序日志异常&#8224;：**0x80072efd 或 0x80072f76 错误：未能执行 EXE 包</span><span class="sxs-lookup"><span data-stu-id="e9059-109">**Installer Log Exception&#8224;:** Error 0x80072efd or 0x80072f76: Failed to execute EXE package</span></span>

  <span data-ttu-id="e9059-110">&#8224;此日志位于 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log。</span><span class="sxs-lookup"><span data-stu-id="e9059-110">&#8224;The log is located at C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log.</span></span>

<span data-ttu-id="e9059-111">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-111">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-112">如果在安装服务器托管捆绑包时系统无法访问 Internet，则在系统阻止安装程序获取 Microsoft Visual C++ 2015 Redistributable 时会出现此异常。</span><span class="sxs-lookup"><span data-stu-id="e9059-112">If the system doesn't have Internet access while installing the server hosting bundle, this exception occurs when the installer is prevented from obtaining the *Microsoft Visual C++ 2015 Redistributable*.</span></span> <span data-ttu-id="e9059-113">获取从安装[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840)。</span><span class="sxs-lookup"><span data-stu-id="e9059-113">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span> <span data-ttu-id="e9059-114">如果安装失败，服务器可能不会收到托管依赖于框架的部署 (FDD) 所需.NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="e9059-114">If the installer fails, the server may not receive the .NET Core runtime required to host a framework-dependent deployment (FDD).</span></span> <span data-ttu-id="e9059-115">如果托管 FDD，确认在程序中安装了运行时&amp;功能。</span><span class="sxs-lookup"><span data-stu-id="e9059-115">If hosting an FDD, confirm that the runtime is installed in Programs &amp; Features.</span></span> <span data-ttu-id="e9059-116">如果需要获取从运行时安装[.NET 下载](https://www.microsoft.com/net/download/core)。</span><span class="sxs-lookup"><span data-stu-id="e9059-116">If needed, obtain a runtime installer from [.NET Downloads](https://www.microsoft.com/net/download/core).</span></span> <span data-ttu-id="e9059-117">安装运行时后，重启系统，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS。</span><span class="sxs-lookup"><span data-stu-id="e9059-117">After installing the runtime, restart the system or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a><span data-ttu-id="e9059-118">OS 升级删除了 32 位 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="e9059-118">OS upgrade removed the 32-bit ASP.NET Core Module</span></span>

* <span data-ttu-id="e9059-119">**应用程序日志：**未能加载模块 DLL C:\WINDOWS\system32\inetsrv\aspnetcore.dll。</span><span class="sxs-lookup"><span data-stu-id="e9059-119">**Application Log:** The Module DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll** failed to load.</span></span> <span data-ttu-id="e9059-120">该数据是个错误。</span><span class="sxs-lookup"><span data-stu-id="e9059-120">The data is the error.</span></span>

<span data-ttu-id="e9059-121">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-121">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-122">OS 升级期间不会保留 C:\Windows\SysWOW64\inetsrv 目录中的非 OS 文件。</span><span class="sxs-lookup"><span data-stu-id="e9059-122">Non-OS files in the **C:\Windows\SysWOW64\inetsrv** directory aren't preserved during an OS upgrade.</span></span> <span data-ttu-id="e9059-123">如果之前安装 ASP.NET 核心模块操作系统升级，然后任何应用程序池运行时在 32 位模式下 OS 升级之后，遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="e9059-123">If the ASP.NET Core Module is installed prior to an OS upgrade and then any AppPool is run in 32-bit mode after an OS upgrade, this issue is encountered.</span></span> <span data-ttu-id="e9059-124">在 OS 升级后修复 ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="e9059-124">After an OS upgrade, repair the ASP.NET Core Module.</span></span> <span data-ttu-id="e9059-125">请参阅[安装 .NET Core Windows Server 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)。</span><span class="sxs-lookup"><span data-stu-id="e9059-125">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span> <span data-ttu-id="e9059-126">选择**修复**安装运行时。</span><span class="sxs-lookup"><span data-stu-id="e9059-126">Select **Repair** when the installer is run.</span></span>

## <a name="platform-conflicts-with-rid"></a><span data-ttu-id="e9059-127">平台与 RID 冲突</span><span class="sxs-lookup"><span data-stu-id="e9059-127">Platform conflicts with RID</span></span>

* <span data-ttu-id="e9059-128">**浏览器：**HTTP 错误 502.5 - 进程失败</span><span class="sxs-lookup"><span data-stu-id="e9059-128">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="e9059-129">**应用程序日志：**应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\{路径}\'无法使用命令行启动进程"c:\\{路径} {程序集}。 {exe | dll}"，错误代码 ="0x80004005: ff。</span><span class="sxs-lookup"><span data-stu-id="e9059-129">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"C:\\{PATH}{assembly}.{exe|dll}" ', ErrorCode = '0x80004005 : ff.</span></span>

* <span data-ttu-id="e9059-130">**ASP.NET 核心模块日志：**未经处理的异常： System.BadImageFormatException： 无法加载文件或程序集 {程序集}.dll。</span><span class="sxs-lookup"><span data-stu-id="e9059-130">**ASP.NET Core Module Log:** Unhandled Exception: System.BadImageFormatException: Could not load file or assembly '{assembly}.dll'.</span></span> <span data-ttu-id="e9059-131">试图加载的程序的格式不正确。</span><span class="sxs-lookup"><span data-stu-id="e9059-131">An attempt was made to load a program with an incorrect format.</span></span>

<span data-ttu-id="e9059-132">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-132">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-133">确认应用在 Kestrel 上本地运行。</span><span class="sxs-lookup"><span data-stu-id="e9059-133">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="e9059-134">进程失败可能是由应用的内部问题导致的。</span><span class="sxs-lookup"><span data-stu-id="e9059-134">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="e9059-135">有关详细信息，请参阅[故障排除](xref:host-and-deploy/iis/troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="e9059-135">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="e9059-136">确认`<PlatformTarget>`中*.csproj*不会与 RID 冲突。</span><span class="sxs-lookup"><span data-stu-id="e9059-136">Confirm that the `<PlatformTarget>` in the *.csproj* doesn't conflict with the RID.</span></span> <span data-ttu-id="e9059-137">例如，未指定`<PlatformTarget>`的`x86`和发布与的 RID `win10-x64`，通过使用*dotnet 发布-c 版本-r win10 x64*或通过设置`<RuntimeIdentifiers>`中*.csproj*到`win10-x64`。</span><span class="sxs-lookup"><span data-stu-id="e9059-137">For example, don't specify a `<PlatformTarget>` of `x86` and publish with an RID of `win10-x64`, either by using *dotnet publish -c Release -r win10-x64* or by setting the `<RuntimeIdentifiers>` in the *.csproj* to `win10-x64`.</span></span> <span data-ttu-id="e9059-138">项目在不显示任何警告或错误的情况下发布，但会失败，且系统上出现上述记录的异常。</span><span class="sxs-lookup"><span data-stu-id="e9059-138">The project publishes without warning or error but fails with the above logged exceptions on the system.</span></span>

* <span data-ttu-id="e9059-139">如果此异常发生的 Azure 应用程序部署升级应用程序时，以及手动部署更新的程序集，从以前的部署中删除所有文件。</span><span class="sxs-lookup"><span data-stu-id="e9059-139">If this exception occurs for an Azure Apps deployment when upgrading an app and deploying newer assemblies, manually delete all files from the prior deployment.</span></span> <span data-ttu-id="e9059-140">部署升级的应用时，延迟的不兼容程序集可能造成 `System.BadImageFormatException` 异常。</span><span class="sxs-lookup"><span data-stu-id="e9059-140">Lingering incompatible assemblies can result in a `System.BadImageFormatException` exception when deploying an upgraded app.</span></span>

## <a name="uri-endpoint-wrong-or-stopped-website"></a><span data-ttu-id="e9059-141">URI 终结点错误或网站已停止</span><span class="sxs-lookup"><span data-stu-id="e9059-141">URI endpoint wrong or stopped website</span></span>

* <span data-ttu-id="e9059-142">**浏览器：**ERR_CONNECTION_REFUSED</span><span class="sxs-lookup"><span data-stu-id="e9059-142">**Browser:** ERR_CONNECTION_REFUSED</span></span>

* <span data-ttu-id="e9059-143">**应用程序日志：**没有任何条目</span><span class="sxs-lookup"><span data-stu-id="e9059-143">**Application Log:** No entry</span></span>

* <span data-ttu-id="e9059-144">**ASP.NET Core 模块日志：**未创建日志文件</span><span class="sxs-lookup"><span data-stu-id="e9059-144">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="e9059-145">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-145">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-146">确认正在使用正确的 URI 终结点应用程序。</span><span class="sxs-lookup"><span data-stu-id="e9059-146">Confirm the correct URI endpoint for the app is being used.</span></span> <span data-ttu-id="e9059-147">请检查绑定中。</span><span class="sxs-lookup"><span data-stu-id="e9059-147">Check the bindings.</span></span>

* <span data-ttu-id="e9059-148">确认 IIS 网站不在*已停止*状态。</span><span class="sxs-lookup"><span data-stu-id="e9059-148">Confirm that the IIS website isn't in the *Stopped* state.</span></span>

## <a name="corewebengine-or-w3svc-server-features-disabled"></a><span data-ttu-id="e9059-149">已禁用 CoreWebEngine 或 W3SVC 服务器功能</span><span class="sxs-lookup"><span data-stu-id="e9059-149">CoreWebEngine or W3SVC server features disabled</span></span>

* <span data-ttu-id="e9059-150">**OS 异常：**必须安装 IIS 7.0 CoreWebEngine 和 W3SVC 功能，以便使用 ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="e9059-150">**OS Exception:** The IIS 7.0 CoreWebEngine and W3SVC features must be installed to use the ASP.NET Core Module.</span></span>

<span data-ttu-id="e9059-151">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-151">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-152">确认已启用适当的角色和功能。</span><span class="sxs-lookup"><span data-stu-id="e9059-152">Confirm that the proper role and features are enabled.</span></span> <span data-ttu-id="e9059-153">请参阅 [IIS 配置](xref:host-and-deploy/iis/index#iis-configuration)。</span><span class="sxs-lookup"><span data-stu-id="e9059-153">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

## <a name="incorrect-website-physical-path-or-app-missing"></a><span data-ttu-id="e9059-154">不正确的网站物理路径或缺少应用程序</span><span class="sxs-lookup"><span data-stu-id="e9059-154">Incorrect website physical path or app missing</span></span>

* <span data-ttu-id="e9059-155">**浏览器：**403 禁止访问 - 访问被拒绝 --或者-- 403.14 禁止访问 - Web 服务器被配置为不列出此目录的内容。</span><span class="sxs-lookup"><span data-stu-id="e9059-155">**Browser:** 403 Forbidden - Access is denied **--OR--** 403.14 Forbidden - The Web server is configured to not list the contents of this directory.</span></span>

* <span data-ttu-id="e9059-156">**应用程序日志：**没有任何条目</span><span class="sxs-lookup"><span data-stu-id="e9059-156">**Application Log:** No entry</span></span>

* <span data-ttu-id="e9059-157">**ASP.NET Core 模块日志：**未创建日志文件</span><span class="sxs-lookup"><span data-stu-id="e9059-157">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="e9059-158">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-158">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-159">检查 IIS 网站**基本设置**和物理应用文件夹。</span><span class="sxs-lookup"><span data-stu-id="e9059-159">Check the IIS website **Basic Settings** and the physical app folder.</span></span> <span data-ttu-id="e9059-160">确认应用程序是否在 IIS 网站的文件夹中**物理路径**。</span><span class="sxs-lookup"><span data-stu-id="e9059-160">Confirm that the app is in the folder at the IIS website **Physical path**.</span></span>

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a><span data-ttu-id="e9059-161">角色不正确、未安装模块或权限不正确</span><span class="sxs-lookup"><span data-stu-id="e9059-161">Incorrect role, module not installed, or incorrect permissions</span></span>

* <span data-ttu-id="e9059-162">**浏览器：**500.19 内部服务器错误 - 无法访问请求的页面，因为该页面的相关配置数据无效。</span><span class="sxs-lookup"><span data-stu-id="e9059-162">**Browser:** 500.19 Internal Server Error - The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

* <span data-ttu-id="e9059-163">**应用程序日志：**没有任何条目</span><span class="sxs-lookup"><span data-stu-id="e9059-163">**Application Log:** No entry</span></span>

* <span data-ttu-id="e9059-164">**ASP.NET Core 模块日志：**未创建日志文件</span><span class="sxs-lookup"><span data-stu-id="e9059-164">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="e9059-165">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-165">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-166">确认启用了适当的角色。</span><span class="sxs-lookup"><span data-stu-id="e9059-166">Confirm that the proper role is enabled.</span></span> <span data-ttu-id="e9059-167">请参阅 [IIS 配置](xref:host-and-deploy/iis/index#iis-configuration)。</span><span class="sxs-lookup"><span data-stu-id="e9059-167">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

* <span data-ttu-id="e9059-168">检查“程序和功能”，确认已安装Microsoft ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="e9059-168">Check **Programs &amp; Features** and confirm that the **Microsoft ASP.NET Core Module** has been installed.</span></span> <span data-ttu-id="e9059-169">如果已安装程序列表中没有 Microsoft ASP.NET Core 模块，请安装该模块。</span><span class="sxs-lookup"><span data-stu-id="e9059-169">If the **Microsoft ASP.NET Core Module** isn't present in the list of installed programs, install the module.</span></span> <span data-ttu-id="e9059-170">请参阅[安装 .NET Core Windows Server 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)。</span><span class="sxs-lookup"><span data-stu-id="e9059-170">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span>

* <span data-ttu-id="e9059-171">请确保**应用程序池** > **进程模型** > **标识**设置为**ApplicationPoolIdentity**或自定义标识具有访问应用程序的部署文件夹的正确权限。</span><span class="sxs-lookup"><span data-stu-id="e9059-171">Make sure that the **Application Pool** > **Process Model** > **Identity** is set to **ApplicationPoolIdentity** or the custom identity has the correct permissions to access the app's deployment folder.</span></span>

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a><span data-ttu-id="e9059-172">processPath 不正确、缺少 PATH 变量、未安装托管捆绑包、未重启系统/IIS、未安装 VC++ Redistributable 或 dotnet.exe 访问冲突</span><span class="sxs-lookup"><span data-stu-id="e9059-172">Incorrect processPath, missing PATH variable, hosting bundle not installed, system/IIS not restarted, VC++ Redistributable not installed, or dotnet.exe access violation</span></span>

* <span data-ttu-id="e9059-173">**浏览器：**HTTP 错误 502.5 - 进程失败</span><span class="sxs-lookup"><span data-stu-id="e9059-173">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="e9059-174">**应用程序日志：**应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\\{路径}\'无法使用命令行启动进程"。\{程序集}.exe"，错误代码 ="0x80070002: 0。</span><span class="sxs-lookup"><span data-stu-id="e9059-174">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '".\{assembly}.exe" ', ErrorCode = '0x80070002 : 0.</span></span>

* <span data-ttu-id="e9059-175">**ASP.NET Core 模块日志：**已创建日志文件，但该日志文件为空</span><span class="sxs-lookup"><span data-stu-id="e9059-175">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="e9059-176">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-176">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-177">确认应用在 Kestrel 上本地运行。</span><span class="sxs-lookup"><span data-stu-id="e9059-177">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="e9059-178">进程失败可能是由应用的内部问题导致的。</span><span class="sxs-lookup"><span data-stu-id="e9059-178">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="e9059-179">有关详细信息，请参阅[故障排除](xref:host-and-deploy/iis/troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="e9059-179">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="e9059-180">检查*processPath*属性`<aspNetCore>`中的元素*web.config*以确认它是*dotnet*为依赖于框架的部署 (FDD) 或*.\{程序集}.exe*自包含的部署 (SCD)。</span><span class="sxs-lookup"><span data-stu-id="e9059-180">Check the *processPath* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's *dotnet* for a framework-dependent deployment (FDD) or *.\{assembly}.exe* for a self-contained deployment (SCD).</span></span>

* <span data-ttu-id="e9059-181">对于 FDD，可能无法通过路径设置访问 dotnet.exe。</span><span class="sxs-lookup"><span data-stu-id="e9059-181">For an FDD, *dotnet.exe* might not be accessible via the PATH settings.</span></span> <span data-ttu-id="e9059-182">确认系统路径设置中存在 *C:\Program Files\dotnet\*。</span><span class="sxs-lookup"><span data-stu-id="e9059-182">Confirm that *C:\Program Files\dotnet\* exists in the System PATH settings.</span></span>

* <span data-ttu-id="e9059-183">对于 FDD，应用程序池的用户标识可能无法访问 dotnet.exe。</span><span class="sxs-lookup"><span data-stu-id="e9059-183">For an FDD, *dotnet.exe* might not be accessible for the user identity of the Application Pool.</span></span> <span data-ttu-id="e9059-184">确认应用程序池用户标识具有访问 C:\Program Files\dotnet 目录的权限。</span><span class="sxs-lookup"><span data-stu-id="e9059-184">Confirm that the AppPool user identity has access to the *C:\Program Files\dotnet* directory.</span></span> <span data-ttu-id="e9059-185">确认没有拒绝规则配置上的应用程序池用户标识*C:\Program Files\dotnet*和应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="e9059-185">Confirm that there are no deny rules configured for the AppPool user identity on the *C:\Program Files\dotnet* and app directories.</span></span>

* <span data-ttu-id="e9059-186">FDD 可能已部署，.NET 核心安装，无需重新启动 IIS。</span><span class="sxs-lookup"><span data-stu-id="e9059-186">An FDD may have been deployed and .NET Core installed without restarting IIS.</span></span> <span data-ttu-id="e9059-187">重启服务器，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS。</span><span class="sxs-lookup"><span data-stu-id="e9059-187">Either restart the server or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="e9059-188">FDD 可能已不在主机系统上安装.NET Core 运行时的情况下部署。</span><span class="sxs-lookup"><span data-stu-id="e9059-188">An FDD may have been deployed without installing the .NET Core runtime on the hosting system.</span></span> <span data-ttu-id="e9059-189">如果尚未安装.NET Core 运行时，运行**.NET 核心 Windows 服务器承载捆绑安装**系统上。</span><span class="sxs-lookup"><span data-stu-id="e9059-189">If the .NET Core runtime hasn't been installed, run the **.NET Core Windows Server Hosting bundle installer** on the system.</span></span> <span data-ttu-id="e9059-190">请参阅[安装 .NET Core Windows Server 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)。</span><span class="sxs-lookup"><span data-stu-id="e9059-190">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span> <span data-ttu-id="e9059-191">如果尝试在未连接到 Internet 的系统上安装.NET Core 运行时，获取从运行时[.NET 下载](https://www.microsoft.com/net/download/core)并运行托管的捆绑包安装，安装 ASP.NET 核心模块。</span><span class="sxs-lookup"><span data-stu-id="e9059-191">If attempting to install the .NET Core runtime on a system without an Internet connection, obtain the runtime from [.NET Downloads](https://www.microsoft.com/net/download/core) and run the hosting bundle installer to install the ASP.NET Core Module.</span></span> <span data-ttu-id="e9059-192">重启系统，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS，完成安装。</span><span class="sxs-lookup"><span data-stu-id="e9059-192">Complete the installation by restarting the system or restarting IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="e9059-193">FDD 可能已部署和*Microsoft Visual c + + 2015年可再发行组件 (x64)*系统上未安装。</span><span class="sxs-lookup"><span data-stu-id="e9059-193">An FDD may have been deployed and the *Microsoft Visual C++ 2015 Redistributable (x64)* isn't installed on the system.</span></span> <span data-ttu-id="e9059-194">获取从安装[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840)。</span><span class="sxs-lookup"><span data-stu-id="e9059-194">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span>

## <a name="incorrect-arguments-of-aspnetcore-element"></a><span data-ttu-id="e9059-195">\<aspNetCore\> 元素的参数不正确</span><span class="sxs-lookup"><span data-stu-id="e9059-195">Incorrect arguments of \<aspNetCore\> element</span></span>

* <span data-ttu-id="e9059-196">**浏览器：**HTTP 错误 502.5 - 进程失败</span><span class="sxs-lookup"><span data-stu-id="e9059-196">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="e9059-197">**应用程序日志：**应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\\{路径}\'无法使用命令行启动进程"dotnet"。\{程序集}.dll，错误代码 ="0x80004005: 80008081。</span><span class="sxs-lookup"><span data-stu-id="e9059-197">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="e9059-198">**ASP.NET 核心模块日志：**要执行的应用程序不存在: 路径\{程序集}.dll</span><span class="sxs-lookup"><span data-stu-id="e9059-198">**ASP.NET Core Module Log:** The application to execute does not exist: 'PATH\{assembly}.dll'</span></span>

<span data-ttu-id="e9059-199">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-199">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-200">确认应用在 Kestrel 上本地运行。</span><span class="sxs-lookup"><span data-stu-id="e9059-200">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="e9059-201">进程失败可能是由应用的内部问题导致的。</span><span class="sxs-lookup"><span data-stu-id="e9059-201">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="e9059-202">有关详细信息，请参阅[故障排除](xref:host-and-deploy/iis/troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="e9059-202">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="e9059-203">检查*参数*属性`<aspNetCore>`中的元素*web.config*要确认它是否是 (a) *。\{程序集}.dll*依赖于框架的部署 (FDD); 或 (b) 不存在空字符串 (*参数 =""*)，或应用程序的自变量列表 (*参数 ="arg1，arg2，..."*)为独立部署 (SCD)。</span><span class="sxs-lookup"><span data-stu-id="e9059-203">Examine the *arguments* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's either (a) *.\{assembly}.dll* for a framework-dependent deployment (FDD); or (b) not present, an empty string (*arguments=""*), or a list of the app's arguments (*arguments="arg1, arg2, ..."*) for a self-contained deployment (SCD).</span></span>

## <a name="missing-net-framework-version"></a><span data-ttu-id="e9059-204">缺少 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="e9059-204">Missing .NET Framework version</span></span>

* <span data-ttu-id="e9059-205">**浏览器：**502.3 错误网关 - 尝试路由请求时出现连接错误。</span><span class="sxs-lookup"><span data-stu-id="e9059-205">**Browser:** 502.3 Bad Gateway - There was a connection error while trying to route the request.</span></span>

* <span data-ttu-id="e9059-206">**应用程序日志：** ErrorCode = 应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\\{路径}\'无法使用命令行启动进程"dotnet"。\{程序集}.dll，错误代码 ="0x80004005: 80008081。</span><span class="sxs-lookup"><span data-stu-id="e9059-206">**Application Log:** ErrorCode = Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="e9059-207">**ASP.NET Core 模块日志：**缺少方法、文件或程序集异常。</span><span class="sxs-lookup"><span data-stu-id="e9059-207">**ASP.NET Core Module Log:** Missing method, file, or assembly exception.</span></span> <span data-ttu-id="e9059-208">在异常中指定的方法、文件或程序集是 .NET Framework 方法、文件或程序集。</span><span class="sxs-lookup"><span data-stu-id="e9059-208">The method, file, or assembly specified in the exception is a .NET Framework method, file, or assembly.</span></span>

<span data-ttu-id="e9059-209">疑难解答：</span><span class="sxs-lookup"><span data-stu-id="e9059-209">Troubleshooting:</span></span>

* <span data-ttu-id="e9059-210">安装系统缺少的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="e9059-210">Install the .NET Framework version missing from the system.</span></span>

* <span data-ttu-id="e9059-211">对于依赖于框架的部署 (FDD)，确认正确的运行时系统上安装。</span><span class="sxs-lookup"><span data-stu-id="e9059-211">For a framework-dependent deployment (FDD), confirm that the correct runtime installed on the system.</span></span> <span data-ttu-id="e9059-212">如果项目从 1.1 升级到 2.0，部署到主机系统，并且此异常结果，请确保 2.0 framework 是在主机系统。</span><span class="sxs-lookup"><span data-stu-id="e9059-212">If the project is upgraded from 1.1 to 2.0, deployed to the hosting system, and this exception results, ensure that the 2.0 framework is on the hosting system.</span></span>

## <a name="stopped-application-pool"></a><span data-ttu-id="e9059-213">应用程序池已停止</span><span class="sxs-lookup"><span data-stu-id="e9059-213">Stopped Application Pool</span></span>

* <span data-ttu-id="e9059-214">**浏览器：**503 服务不可用</span><span class="sxs-lookup"><span data-stu-id="e9059-214">**Browser:** 503 Service Unavailable</span></span>

* <span data-ttu-id="e9059-215">**应用程序日志：**没有任何条目</span><span class="sxs-lookup"><span data-stu-id="e9059-215">**Application Log:** No entry</span></span>

* <span data-ttu-id="e9059-216">**ASP.NET Core 模块日志：**未创建日志文件</span><span class="sxs-lookup"><span data-stu-id="e9059-216">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="e9059-217">疑难解答</span><span class="sxs-lookup"><span data-stu-id="e9059-217">Troubleshooting</span></span>

* <span data-ttu-id="e9059-218">确认应用程序池不在*已停止*状态。</span><span class="sxs-lookup"><span data-stu-id="e9059-218">Confirm that the Application Pool isn't in the *Stopped* state.</span></span>

## <a name="iis-integration-middleware-not-implemented"></a><span data-ttu-id="e9059-219">未实现 IIS 集成中间件</span><span class="sxs-lookup"><span data-stu-id="e9059-219">IIS Integration middleware not implemented</span></span>

* <span data-ttu-id="e9059-220">**浏览器：**HTTP 错误 502.5 - 进程失败</span><span class="sxs-lookup"><span data-stu-id="e9059-220">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="e9059-221">**应用程序日志：**应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\\{路径}\'使用命令行创建过程"c:\\{路径}\{程序集}。 {exe | dll}"但损坏或未不响应，或者没有侦听给定的端口 {PORT}，错误代码 ="0x800705b4"</span><span class="sxs-lookup"><span data-stu-id="e9059-221">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="e9059-222">**ASP.NET Core 模块日志：**已创建日志文件，且该日志文件显示正常操作。</span><span class="sxs-lookup"><span data-stu-id="e9059-222">**ASP.NET Core Module Log:** Log file created and shows normal operation.</span></span>

<span data-ttu-id="e9059-223">疑难解答</span><span class="sxs-lookup"><span data-stu-id="e9059-223">Troubleshooting</span></span>

* <span data-ttu-id="e9059-224">确认应用在 Kestrel 上本地运行。</span><span class="sxs-lookup"><span data-stu-id="e9059-224">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="e9059-225">进程失败可能是由应用的内部问题导致的。</span><span class="sxs-lookup"><span data-stu-id="e9059-225">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="e9059-226">有关详细信息，请参阅[故障排除](xref:host-and-deploy/iis/troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="e9059-226">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="e9059-227">请确认：</span><span class="sxs-lookup"><span data-stu-id="e9059-227">Confirm that either:</span></span>
  * <span data-ttu-id="e9059-228">IIS 集成中间件是 referencedby 调用`UseIISIntegration`上应用的方法`WebHostBuilder`(ASP.NET Core 1.x)</span><span class="sxs-lookup"><span data-stu-id="e9059-228">The IIS Integration middleware is referencedby calling the `UseIISIntegration` method on the app's `WebHostBuilder` (ASP.NET Core 1.x)</span></span>
  * <span data-ttu-id="e9059-229">应用程序使用`CreateDefaultBuilder`方法 (ASP.NET Core 2.x)。</span><span class="sxs-lookup"><span data-stu-id="e9059-229">The apps uses the `CreateDefaultBuilder` method (ASP.NET Core 2.x).</span></span>
  
  <span data-ttu-id="e9059-230">有关详细信息，请参阅 [ASP.NET Core 中的承载](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="e9059-230">See [Hosting in ASP.NET Core](xref:fundamentals/hosting) for details.</span></span>

## <a name="sub-application-includes-a-handlers-section"></a><span data-ttu-id="e9059-231">子应用程序包括 \<handlers\> 部分</span><span class="sxs-lookup"><span data-stu-id="e9059-231">Sub-application includes a \<handlers\> section</span></span>

* <span data-ttu-id="e9059-232">**浏览器：**HTTP 错误 500.19 - 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="e9059-232">**Browser:** HTTP Error 500.19 - Internal Server Error</span></span>

* <span data-ttu-id="e9059-233">**应用程序日志：**没有任何条目</span><span class="sxs-lookup"><span data-stu-id="e9059-233">**Application Log:** No entry</span></span>

* <span data-ttu-id="e9059-234">**ASP.NET 核心模块日志：**日志文件创建并显示有关根应用程序的正常操作。</span><span class="sxs-lookup"><span data-stu-id="e9059-234">**ASP.NET Core Module Log:** Log file created and shows normal operation for the root app.</span></span> <span data-ttu-id="e9059-235">不会为订阅应用程序创建的日志文件。</span><span class="sxs-lookup"><span data-stu-id="e9059-235">Log file not created for the sub-app.</span></span>

<span data-ttu-id="e9059-236">疑难解答</span><span class="sxs-lookup"><span data-stu-id="e9059-236">Troubleshooting</span></span>

* <span data-ttu-id="e9059-237">确认子应用的 web.config 文件不包括 `<handlers>` 部分。</span><span class="sxs-lookup"><span data-stu-id="e9059-237">Confirm that the sub-app's *web.config* file doesn't include a `<handlers>` section.</span></span>

## <a name="application-configuration-general-issue"></a><span data-ttu-id="e9059-238">应用程序配置常见问题</span><span class="sxs-lookup"><span data-stu-id="e9059-238">Application configuration general issue</span></span>

* <span data-ttu-id="e9059-239">**浏览器：**HTTP 错误 502.5 - 进程失败</span><span class="sxs-lookup"><span data-stu-id="e9059-239">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="e9059-240">**应用程序日志：**应用程序 ' MACHINE/WEBROOT/APPHOST / {程序集} 与物理根 c:\\{路径}\'使用命令行创建过程"c:\\{路径}\{程序集}。 {exe | dll}"但损坏或未不响应，或者没有侦听给定的端口 {PORT}，错误代码 ="0x800705b4"</span><span class="sxs-lookup"><span data-stu-id="e9059-240">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="e9059-241">**ASP.NET Core 模块日志：**已创建日志文件，但该日志文件为空</span><span class="sxs-lookup"><span data-stu-id="e9059-241">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="e9059-242">疑难解答</span><span class="sxs-lookup"><span data-stu-id="e9059-242">Troubleshooting</span></span>

* <span data-ttu-id="e9059-243">此常规异常指示进程无法启动，很可能由于应用程序配置问题。</span><span class="sxs-lookup"><span data-stu-id="e9059-243">This general exception indicates that the process failed to start, most likely due to an app configuration issue.</span></span> <span data-ttu-id="e9059-244">引用[目录结构](xref:host-and-deploy/directory-structure)，确认应用程序的部署文件和文件夹是适当和应用程序的配置文件是否存在并且包含正确的设置为应用程序和环境。</span><span class="sxs-lookup"><span data-stu-id="e9059-244">Referring to [Directory Structure](xref:host-and-deploy/directory-structure), confirm that the app's deployed files and folders are appropriate and that the app's configuration files are present and contain the correct settings for the app and environment.</span></span> <span data-ttu-id="e9059-245">有关详细信息，请参阅[故障排除](xref:host-and-deploy/iis/troubleshoot)。</span><span class="sxs-lookup"><span data-stu-id="e9059-245">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>
