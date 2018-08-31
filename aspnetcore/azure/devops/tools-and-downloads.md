---
title: 使用 ASP.NET Core 和 Azure DevOps |工具和下载
author: CamSoper
description: 提供有关为托管在 Azure 中的 ASP.NET Core 应用构建 DevOps 管道的端到端指导的指南。
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/tools-and-downloads
ms.openlocfilehash: a63e97d9ab9eb0ed2fbd30e8c2e033f0c048d33e
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312296"
---
# <a name="tools-and-downloads"></a><span data-ttu-id="e810b-103">工具和下载</span><span class="sxs-lookup"><span data-stu-id="e810b-103">Tools and downloads</span></span>

<span data-ttu-id="e810b-104">Azure 具有用于预配和管理资源，如多个接口[Azure 门户](https://portal.azure.com)， [Azure CLI](https://docs.microsoft.com/cli/azure/)， [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)， [Azure 云Shell](https://shell.azure.com/bash)，和 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e810b-104">Azure has several interfaces for provisioning and managing resources, such as the [Azure portal](https://portal.azure.com), [Azure CLI](https://docs.microsoft.com/cli/azure/), [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Cloud Shell](https://shell.azure.com/bash), and Visual Studio.</span></span> <span data-ttu-id="e810b-105">本指南将最低要求方法，并使用 Azure Cloud Shell 中，只要有可能以减少所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="e810b-105">This guide takes a minimalist approach and uses the Azure Cloud Shell whenever possible to reduce the steps required.</span></span> <span data-ttu-id="e810b-106">但是，对于某些部分都必须使用 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="e810b-106">However, the Azure portal must be used for some portions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e810b-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="e810b-107">Prerequisites</span></span>

<span data-ttu-id="e810b-108">以下订阅是必需的：</span><span class="sxs-lookup"><span data-stu-id="e810b-108">The following subscriptions are required:</span></span>

* <span data-ttu-id="e810b-109">Azure&mdash;如果还没有帐户，[获取免费试用版](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="e810b-109">Azure &mdash; If you don't have an account, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="e810b-110">Visual Studio Team Services (VSTS)&mdash;第 4 章中创建此帐户。</span><span class="sxs-lookup"><span data-stu-id="e810b-110">Visual Studio Team Services (VSTS) &mdash; This account is created in Chapter 4.</span></span>
* <span data-ttu-id="e810b-111">GitHub&mdash;如果还没有帐户，[免费注册](https://github.com/join)。</span><span class="sxs-lookup"><span data-stu-id="e810b-111">GitHub &mdash; If you don't have an account, [sign up for free](https://github.com/join).</span></span>

<span data-ttu-id="e810b-112">以下工具是必需的：</span><span class="sxs-lookup"><span data-stu-id="e810b-112">The following tools are required:</span></span>

* <span data-ttu-id="e810b-113">[Git](https://git-scm.com/downloads) &mdash;本指南中建议的 Git 基本的了解。</span><span class="sxs-lookup"><span data-stu-id="e810b-113">[Git](https://git-scm.com/downloads) &mdash; A fundamental understanding of Git is recommended for this guide.</span></span> <span data-ttu-id="e810b-114">审阅[Git 文档](https://git-scm.com/doc)，具体而言[的 git remote](https://git-scm.com/docs/git-remote)并[git 推送](https://git-scm.com/docs/git-push)。</span><span class="sxs-lookup"><span data-stu-id="e810b-114">Review the [Git documentation](https://git-scm.com/doc), specifically [git remote](https://git-scm.com/docs/git-remote) and [git push](https://git-scm.com/docs/git-push).</span></span>
* <span data-ttu-id="e810b-115">[.NET core SDK](https://www.microsoft.com/net/download/) &mdash; 2.1.300 版本或更高版本需要生成并运行示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="e810b-115">[.NET Core SDK](https://www.microsoft.com/net/download/) &mdash; Version 2.1.300 or later is required to build and run the sample app.</span></span> <span data-ttu-id="e810b-116">如果使用安装了 Visual Studio **.NET Core 跨平台开发**已安装工作负荷中，.NET Core SDK。</span><span class="sxs-lookup"><span data-stu-id="e810b-116">If Visual Studio is installed with the **.NET Core cross-platform development** workload, the .NET Core SDK is already installed.</span></span>

    <span data-ttu-id="e810b-117">验证您的.NET Core SDK 安装。</span><span class="sxs-lookup"><span data-stu-id="e810b-117">Verify your .NET Core SDK installation.</span></span> <span data-ttu-id="e810b-118">打开命令外壳中，并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e810b-118">Open a command shell, and run the following command:</span></span>

    ```console
    dotnet --version
    ```

## <a name="recommended-tools-windows-only"></a><span data-ttu-id="e810b-119">建议的工具 (仅 Windows)</span><span class="sxs-lookup"><span data-stu-id="e810b-119">Recommended tools (Windows only)</span></span>

* <span data-ttu-id="e810b-120">[Visual Studio](https://www.visualstudio.com/)的可靠的 Azure 工具提供了 GUI 的大部分在本指南中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="e810b-120">[Visual Studio](https://www.visualstudio.com/)'s robust Azure tools provide a GUI for most of the functionality described in this guide.</span></span> <span data-ttu-id="e810b-121">任何版本的 Visual Studio 将起作用，包括免费的 Visual Studio Community Edition。</span><span class="sxs-lookup"><span data-stu-id="e810b-121">Any edition of Visual Studio will work, including the free Visual Studio Community Edition.</span></span> <span data-ttu-id="e810b-122">教程旨在演示开发、 部署和 DevOps 与和不使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e810b-122">The tutorials are written to demonstrate development, deployment, and DevOps both with and without Visual Studio.</span></span>

  <span data-ttu-id="e810b-123">确认 Visual Studio 具有以下[工作负荷](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)安装：</span><span class="sxs-lookup"><span data-stu-id="e810b-123">Confirm that Visual Studio has the following [workloads](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) installed:</span></span>

  * <span data-ttu-id="e810b-124">ASP.NET 和 Web 开发</span><span class="sxs-lookup"><span data-stu-id="e810b-124">ASP.NET and web development</span></span>
  * <span data-ttu-id="e810b-125">Azure 开发</span><span class="sxs-lookup"><span data-stu-id="e810b-125">Azure development</span></span>
  * <span data-ttu-id="e810b-126">.NET Core 跨平台开发</span><span class="sxs-lookup"><span data-stu-id="e810b-126">.NET Core cross-platform development</span></span>
