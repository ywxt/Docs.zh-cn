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
ms.openlocfilehash: a75dc666621600e1e2fe36c29acbe7484bae9229
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="85d05-103">解决 ASP.NET 核心项目</span><span class="sxs-lookup"><span data-stu-id="85d05-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="85d05-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="85d05-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="85d05-105">以下链接提供了故障排除指导：</span><span class="sxs-lookup"><span data-stu-id="85d05-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="85d05-106">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="85d05-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="85d05-107">对 IIS 上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="85d05-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="85d05-108">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="85d05-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="85d05-109">YouTube： 诊断 ASP.NET 核心应用程序中的问题</span><span class="sxs-lookup"><span data-stu-id="85d05-109">YouTube: Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)

<a name="sdk"></a>
## <a name="net-core-sdk-warnings"></a><span data-ttu-id="85d05-110">.NET 核心 SDK 警告</span><span class="sxs-lookup"><span data-stu-id="85d05-110">.NET Core SDK warnings</span></span>

### <a name="both-the-32-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="85d05-111">安装这两个 32 和 64 位版本的.NET 核心 SDK</span><span class="sxs-lookup"><span data-stu-id="85d05-111">Both the 32 and 64 bit versions of the .NET Core SDK are installed</span></span>
<span data-ttu-id="85d05-112">在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告出现在的顶部：</span><span class="sxs-lookup"><span data-stu-id="85d05-112">In the **New Project** dialog for ASP.NET Core, you may see the following warning appear at the top:</span></span> 

    Both 32 and 64 bit versions of the .NET Core SDK are installed. Only templates from the 64 bit version(s) installed at C:\Program Files\dotnet\sdk\" will be displayed.

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="85d05-114">时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET 核心 SDK](https://www.microsoft.com/net/download/all)安装。</span><span class="sxs-lookup"><span data-stu-id="85d05-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="85d05-115">可以安装两个版本的常见原因包括：</span><span class="sxs-lookup"><span data-stu-id="85d05-115">Common reasons both versions can be installed include:</span></span>

* <span data-ttu-id="85d05-116">你最初下载.NET 核心 SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。</span><span class="sxs-lookup"><span data-stu-id="85d05-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine, but then copied it across and installed it on a 64-bit machine.</span></span> 
* <span data-ttu-id="85d05-117">由另一个应用程序安装了 32 位.NET 核心 SDK。</span><span class="sxs-lookup"><span data-stu-id="85d05-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="85d05-118">下载并安装了错误版本。</span><span class="sxs-lookup"><span data-stu-id="85d05-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="85d05-119">卸载 32 位.NET 核心 SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="85d05-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="85d05-120">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="85d05-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="85d05-121">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="85d05-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="85d05-122">.NET 核心 SDK 的安装在多个位置</span><span class="sxs-lookup"><span data-stu-id="85d05-122">The .NET Core SDK is installed in multiple locations</span></span>
<span data-ttu-id="85d05-123">在**新项目**ASP.NET Core 可能会看到以下警告顶部显示的对话框：</span><span class="sxs-lookup"><span data-stu-id="85d05-123">In the **New Project** dialog for ASP.NET Core you may see the following warning appear at the top:</span></span> 

 <span data-ttu-id="85d05-124">.NET 核心 SDK 安装在多个位置中。</span><span class="sxs-lookup"><span data-stu-id="85d05-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="85d05-125">从安装在 SDK(s) 的模板 C:\Program Files\dotnet\sdk\'将显示。</span><span class="sxs-lookup"><span data-stu-id="85d05-125">Only templates from the SDK(s) installed at 'C:\Program Files\dotnet\sdk\' will be displayed.</span></span>

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="85d05-127">你看到此消息因为之外的一个目录中有至少一个安装的.NET 核心 SDK * C:\Program Files\dotnet\sdk\*。</span><span class="sxs-lookup"><span data-stu-id="85d05-127">You are seeing this message because you have at least one installation of the .NET Core SDK in a directory outside of *C:\Program Files\dotnet\sdk\*.</span></span> <span data-ttu-id="85d05-128">通常，这发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET 核心 SDK 时。</span><span class="sxs-lookup"><span data-stu-id="85d05-128">Usually that happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="85d05-129">卸载 32 位.NET 核心 SDK，以防止出现此警告。</span><span class="sxs-lookup"><span data-stu-id="85d05-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="85d05-130">从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。</span><span class="sxs-lookup"><span data-stu-id="85d05-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="85d05-131">如果你了解为何会出现的警告和它的含义，你可以忽略该警告。</span><span class="sxs-lookup"><span data-stu-id="85d05-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>
