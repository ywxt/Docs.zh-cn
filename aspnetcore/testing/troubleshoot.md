---
title: 有关 ASP.NET 核心故障排除
author: Rick-Anderson
description: 了解和解决警告和错误与 ASP.NET 核心项目。
manager: wpickett
ms.author: riande
ms.date: 04/05/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: testing/troubleshoot
ms.openlocfilehash: f2c785bfe27ddd67db0313b8ee1c077a8cc06e05
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="4fdfb-103">解决 ASP.NET 核心项目</span><span class="sxs-lookup"><span data-stu-id="4fdfb-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="4fdfb-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4fdfb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4fdfb-105">以下链接提供了故障排除指导：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="4fdfb-106">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="4fdfb-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="4fdfb-107">对 IIS 上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="4fdfb-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="4fdfb-108">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="4fdfb-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="4fdfb-109">YouTube：诊断 ASP.NET Core 应用程序中的问题</span><span class="sxs-lookup"><span data-stu-id="4fdfb-109">YouTube: Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)

<a name="sdk"></a>
## <a name="net-core-sdk-warnings"></a><span data-ttu-id="4fdfb-110">.NET 核心 SDK 警告</span><span class="sxs-lookup"><span data-stu-id="4fdfb-110">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="4fdfb-111">安装的 32 位和 64 位版本的.NET 核心 SDK</span><span class="sxs-lookup"><span data-stu-id="4fdfb-111">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>
<span data-ttu-id="4fdfb-112">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-112">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span> 

    Both 32 and 64 bit versions of the .NET Core SDK are installed. Only templates from the 64 bit version(s) installed at C:\Program Files\dotnet\sdk\" will be displayed.

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="4fdfb-114">时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET 核心 SDK](https://www.microsoft.com/net/download/all)安装。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="4fdfb-115">可以安装两个版本的常见原因包括：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-115">Common reasons both versions can be installed include:</span></span>

* <span data-ttu-id="4fdfb-116">你最初下载.NET 核心 SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine, but then copied it across and installed it on a 64-bit machine.</span></span> 
* <span data-ttu-id="4fdfb-117">由另一个应用程序安装了 32 位.NET 核心 SDK。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="4fdfb-118">下载并安装了错误版本。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="4fdfb-119">卸载 32 位.NET 核心 SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="4fdfb-120">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="4fdfb-121">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="4fdfb-122">.NET 核心 SDK 的安装在多个位置</span><span class="sxs-lookup"><span data-stu-id="4fdfb-122">The .NET Core SDK is installed in multiple locations</span></span>
<span data-ttu-id="4fdfb-123">在**新项目**对话框为 ASP.NET Core 可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-123">In the **New Project** dialog for ASP.NET Core you may see the following warning:</span></span> 

 <span data-ttu-id="4fdfb-124">.NET 核心 SDK 安装在多个位置中。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="4fdfb-125">从安装在 SDK(s) 的模板 C:\Program Files\dotnet\sdk\'将显示。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-125">Only templates from the SDK(s) installed at 'C:\Program Files\dotnet\sdk\' will be displayed.</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="4fdfb-127">外部的一个目录中有至少一个安装的.NET 核心 SDK 时，将显示此消息 * C:\Program Files\dotnet\sdk\*。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-127">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\Program Files\dotnet\sdk\*.</span></span> <span data-ttu-id="4fdfb-128">通常，这发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET 核心 SDK 时。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-128">Usually that happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="4fdfb-129">卸载 32 位.NET 核心 SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="4fdfb-130">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="4fdfb-131">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="4fdfb-132">检测到没有.NET 核心 Sdk</span><span class="sxs-lookup"><span data-stu-id="4fdfb-132">No .NET Core SDKs were detected</span></span>
<span data-ttu-id="4fdfb-133">在**新项目**对话框为 ASP.NET Core 可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-133">In the **New Project** dialog for ASP.NET Core you may see the following warning:</span></span> 

<span data-ttu-id="4fdfb-134">**检测到没有.NET 核心 Sdk，请确保将它们包括在环境变量 PATH**</span><span class="sxs-lookup"><span data-stu-id="4fdfb-134">**No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'**</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="4fdfb-136">时，此警告会出现的环境变量`PATH`没有指向计算机上任何.NET 核心 Sdk。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-136">This warning appears when the environment variable `PATH` doesn’t point to any .NET Core SDKs on the machine.</span></span> <span data-ttu-id="4fdfb-137">若要解决此问题：</span><span class="sxs-lookup"><span data-stu-id="4fdfb-137">To resolve this problem:</span></span>

* <span data-ttu-id="4fdfb-138">安装或验证.NET 核心 SDK 的安装。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-138">Install or verify the .NET Core SDK is installed.</span></span>
* <span data-ttu-id="4fdfb-139">验证`PATH`环境变量指向 SDK 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-139">Verify the `PATH` environment variable points to the location the SDK is installed.</span></span> <span data-ttu-id="4fdfb-140">安装程序通常设置`PATH`。</span><span class="sxs-lookup"><span data-stu-id="4fdfb-140">The installer normally sets the `PATH`.</span></span>