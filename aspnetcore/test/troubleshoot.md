---
title: 解决 ASP.NET Core项目
author: Rick-Anderson
description: 理解 ASP.NET Core 项目的警告和错误，并对其进行故障排除。
ms.author: riande
ms.date: 04/05/2018
uid: test/troubleshoot
ms.openlocfilehash: ae4e6f191d8f856de60ecf21cb882b5ee9b02064
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274588"
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="ba13e-103">解决 ASP.NET Core项目</span><span class="sxs-lookup"><span data-stu-id="ba13e-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="ba13e-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ba13e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ba13e-105">以下链接提供了故障排除指导：</span><span class="sxs-lookup"><span data-stu-id="ba13e-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="ba13e-106">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="ba13e-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="ba13e-107">对 IIS 上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="ba13e-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="ba13e-108">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="ba13e-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="ba13e-109">ASP.NET Core应用程序中 （ndc） 会议 （伦敦，2018年）： 诊断问题</span><span class="sxs-lookup"><span data-stu-id="ba13e-109">NDC Conference (London, 2018): Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [<span data-ttu-id="ba13e-110">ASP.NET 博客： 解决 ASP.NET Core 性能问题</span><span class="sxs-lookup"><span data-stu-id="ba13e-110">ASP.NET Blog: Troubleshooting ASP.NET Core Performance Problems</span></span>](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a><span data-ttu-id="ba13e-111">.NET Core SDK 警告</span><span class="sxs-lookup"><span data-stu-id="ba13e-111">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="ba13e-112">安装的 32 位和 64 位版本的.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ba13e-112">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>

<span data-ttu-id="ba13e-113">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="ba13e-113">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="ba13e-114">安装了.NET Core SDK 32 和 64 位版本。</span><span class="sxs-lookup"><span data-stu-id="ba13e-114">Both 32 and 64 bit versions of the .NET Core SDK are installed.</span></span> <span data-ttu-id="ba13e-115">仅从安装在 64 位版本的模板 c:\\Program Files\\dotnet\\sdk\\将显示。</span><span class="sxs-lookup"><span data-stu-id="ba13e-115">Only templates from the 64 bit version(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="ba13e-117">时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET Core SDK](https://www.microsoft.com/net/download/all)安装。</span><span class="sxs-lookup"><span data-stu-id="ba13e-117">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="ba13e-118">可能安装这两个版本的常见原因包括：</span><span class="sxs-lookup"><span data-stu-id="ba13e-118">Common reasons both versions may be installed include:</span></span>

* <span data-ttu-id="ba13e-119">你最初下载.NET Core SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。</span><span class="sxs-lookup"><span data-stu-id="ba13e-119">You originally downloaded the .NET Core SDK installer using a 32-bit machine but then copied it across and installed it on a 64-bit machine.</span></span>
* <span data-ttu-id="ba13e-120">由另一个应用程序安装了 32 位.NET Core SDK。</span><span class="sxs-lookup"><span data-stu-id="ba13e-120">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="ba13e-121">下载并安装了错误版本。</span><span class="sxs-lookup"><span data-stu-id="ba13e-121">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="ba13e-122">卸载 32 位.NET Core SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="ba13e-122">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="ba13e-123">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="ba13e-123">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="ba13e-124">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="ba13e-124">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="ba13e-125">.NET Core SDK 的安装在多个位置</span><span class="sxs-lookup"><span data-stu-id="ba13e-125">The .NET Core SDK is installed in multiple locations</span></span>

<span data-ttu-id="ba13e-126">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="ba13e-126">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="ba13e-127">.NET Core SDK 安装在多个位置中。</span><span class="sxs-lookup"><span data-stu-id="ba13e-127">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="ba13e-128">仅从安装在 SDK(s) 的模板 c:\\Program Files\\dotnet\\sdk\\将显示。</span><span class="sxs-lookup"><span data-stu-id="ba13e-128">Only templates from the SDK(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="ba13e-130">外部的一个目录中有至少一个安装的.NET Core SDK 时，将显示此消息*c:\\Program Files\\dotnet\\sdk\\*。</span><span class="sxs-lookup"><span data-stu-id="ba13e-130">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\\Program Files\\dotnet\\sdk\\*.</span></span> <span data-ttu-id="ba13e-131">这通常发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET Core SDK 时。</span><span class="sxs-lookup"><span data-stu-id="ba13e-131">Usually this happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="ba13e-132">卸载 32 位.NET Core SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="ba13e-132">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="ba13e-133">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="ba13e-133">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="ba13e-134">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="ba13e-134">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="ba13e-135">检测到没有.NET Core Sdk</span><span class="sxs-lookup"><span data-stu-id="ba13e-135">No .NET Core SDKs were detected</span></span>

<span data-ttu-id="ba13e-136">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="ba13e-136">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="ba13e-137">检测到没有.NET Core Sdk，请确保将它们包括在环境变量 PATH。</span><span class="sxs-lookup"><span data-stu-id="ba13e-137">No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'.</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="ba13e-139">时，此警告会出现的环境变量`PATH`没有指向计算机上任何.NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="ba13e-139">This warning appears when the environment variable `PATH` doesn't point to any .NET Core SDKs on the machine.</span></span> <span data-ttu-id="ba13e-140">若要解决此问题：</span><span class="sxs-lookup"><span data-stu-id="ba13e-140">To resolve this problem:</span></span>

* <span data-ttu-id="ba13e-141">安装或验证.NET Core SDK 的安装。</span><span class="sxs-lookup"><span data-stu-id="ba13e-141">Install or verify the .NET Core SDK is installed.</span></span>
* <span data-ttu-id="ba13e-142">验证`PATH`环境变量指向 SDK 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="ba13e-142">Verify the `PATH` environment variable points to the location the SDK is installed.</span></span> <span data-ttu-id="ba13e-143">安装程序通常设置`PATH`。</span><span class="sxs-lookup"><span data-stu-id="ba13e-143">The installer normally sets the `PATH`.</span></span>

::: moniker range=">= aspnetcore-2.1"

### <a name="use-of-ihtmlhelperpartial-may-result-in-app-deadlocks"></a><span data-ttu-id="ba13e-144">利用 IHtmlHelper.Partial 可能会导致应用程序死锁</span><span class="sxs-lookup"><span data-stu-id="ba13e-144">Use of IHtmlHelper.Partial may result in app deadlocks</span></span>

<span data-ttu-id="ba13e-145">在 ASP.NET Core 2.1 及更高版本，则调用`Html.Partial`导致死锁的可能性由于分析器警告。</span><span class="sxs-lookup"><span data-stu-id="ba13e-145">In ASP.NET Core 2.1 and later, calling `Html.Partial` results in an analyzer warning due to the potential for deadlocks.</span></span> <span data-ttu-id="ba13e-146">警告消息为：</span><span class="sxs-lookup"><span data-stu-id="ba13e-146">The warning message is:</span></span>

> <span data-ttu-id="ba13e-147">利用 IHtmlHelper.Partial 可能会导致应用程序死锁。</span><span class="sxs-lookup"><span data-stu-id="ba13e-147">Use of IHtmlHelper.Partial may result in application deadlocks.</span></span> <span data-ttu-id="ba13e-148">请考虑使用`<partial>`标记帮助器或`IHtmlHelper.PartialAsync`。</span><span class="sxs-lookup"><span data-stu-id="ba13e-148">Consider using `<partial>` Tag Helper or `IHtmlHelper.PartialAsync`.</span></span>

<span data-ttu-id="ba13e-149">调用`@Html.Partial`应替换为`@await Html.PartialAsync`或部分标记帮助器`<partial name="_Partial" />`。</span><span class="sxs-lookup"><span data-stu-id="ba13e-149">Calls to `@Html.Partial` should be replaced by `@await Html.PartialAsync` or the partial tag helper `<partial name="_Partial" />`.</span></span>

::: moniker-end
