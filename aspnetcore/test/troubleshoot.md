---
title: 解决 ASP.NET Core 项目
author: Rick-Anderson
description: 理解 ASP.NET Core 项目的警告和错误，并对其进行故障排除。
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: test/troubleshoot
ms.openlocfilehash: 150f2192bb4b6dd0d330fd678d9c5fa0bf31673e
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090106"
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="9d9ff-103">解决 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="9d9ff-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="9d9ff-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9d9ff-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9d9ff-105">以下链接提供的故障排除指南：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-105">The following links provide troubleshooting guidance:</span></span>

* <xref:host-and-deploy/azure-apps/troubleshoot>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-iis-errors-reference>
* [<span data-ttu-id="9d9ff-106">ASP.NET Core 应用程序中 （ndc） 会议 （伦敦，2018年）： 诊断问题</span><span class="sxs-lookup"><span data-stu-id="9d9ff-106">NDC Conference (London, 2018): Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [<span data-ttu-id="9d9ff-107">ASP.NET 博客： 解决 ASP.NET Core 性能问题</span><span class="sxs-lookup"><span data-stu-id="9d9ff-107">ASP.NET Blog: Troubleshooting ASP.NET Core Performance Problems</span></span>](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a><span data-ttu-id="9d9ff-108">.NET Core SDK 警告</span><span class="sxs-lookup"><span data-stu-id="9d9ff-108">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="9d9ff-109">安装的 32 位和 64 位版本的.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="9d9ff-109">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>

<span data-ttu-id="9d9ff-110">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-110">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="9d9ff-111">安装了.NET Core SDK 32 和 64 位版本。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-111">Both 32 and 64 bit versions of the .NET Core SDK are installed.</span></span> <span data-ttu-id="9d9ff-112">仅从安装在 64 位版本的模板 c:\\Program Files\\dotnet\\sdk\\将显示。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-112">Only templates from the 64 bit version(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="9d9ff-114">时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET Core SDK](https://www.microsoft.com/net/download/all)安装。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="9d9ff-115">可能安装这两个版本的常见原因包括：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-115">Common reasons both versions may be installed include:</span></span>

* <span data-ttu-id="9d9ff-116">你最初下载.NET Core SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine but then copied it across and installed it on a 64-bit machine.</span></span>
* <span data-ttu-id="9d9ff-117">由另一个应用程序安装了 32 位.NET Core SDK。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="9d9ff-118">下载并安装了错误的版本。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="9d9ff-119">卸载 32 位.NET Core SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="9d9ff-120">从卸载**Control Panel** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="9d9ff-121">如果您了解为何会出现的警告和其影响，则可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="9d9ff-122">.NET Core SDK 的安装在多个位置</span><span class="sxs-lookup"><span data-stu-id="9d9ff-122">The .NET Core SDK is installed in multiple locations</span></span>

<span data-ttu-id="9d9ff-123">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-123">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="9d9ff-124">.NET Core SDK 安装在多个位置中。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="9d9ff-125">仅安装在上 SDK 的模板 c:\\Program Files\\dotnet\\sdk\\将显示。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-125">Only templates from the SDK(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="9d9ff-127">外部的一个目录中有至少一个安装的.NET Core SDK 时，将显示此消息*c:\\Program Files\\dotnet\\sdk\\*。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-127">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\\Program Files\\dotnet\\sdk\\*.</span></span> <span data-ttu-id="9d9ff-128">这通常发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET Core SDK 时。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-128">Usually this happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="9d9ff-129">卸载 32 位.NET Core SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="9d9ff-130">从卸载**Control Panel** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="9d9ff-131">如果您了解为何会出现的警告和其影响，则可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="9d9ff-132">检测到没有.NET Core Sdk</span><span class="sxs-lookup"><span data-stu-id="9d9ff-132">No .NET Core SDKs were detected</span></span>

<span data-ttu-id="9d9ff-133">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-133">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="9d9ff-134">检测到没有.NET Core Sdk，请确保将它们包括在环境变量 PATH。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-134">No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'.</span></span>

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="9d9ff-136">时，此警告会出现的环境变量`PATH`没有指向计算机上任何.NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-136">This warning appears when the environment variable `PATH` doesn't point to any .NET Core SDKs on the machine.</span></span> <span data-ttu-id="9d9ff-137">若要解决此问题：</span><span class="sxs-lookup"><span data-stu-id="9d9ff-137">To resolve this problem:</span></span>

* <span data-ttu-id="9d9ff-138">安装或验证.NET Core SDK 的安装。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-138">Install or verify the .NET Core SDK is installed.</span></span>
* <span data-ttu-id="9d9ff-139">验证`PATH`环境变量指向在其中安装了 SDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-139">Verify that the `PATH` environment variable points to the location in which the SDK is installed.</span></span> <span data-ttu-id="9d9ff-140">安装程序通常设置`PATH`。</span><span class="sxs-lookup"><span data-stu-id="9d9ff-140">The installer normally sets the `PATH`.</span></span>
