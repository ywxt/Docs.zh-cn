---
title: "Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持"
author: shirhatti
description: "发现对调试 ASP.NET Core 应用程序的支持（在 Windows Server 上以 IIS 为背景运行时）。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: a5f727dd21ac0c6702691df2215c42f4adc0ec27
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="a4672-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="a4672-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="a4672-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="a4672-104">By: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="a4672-105">本文介绍了对调试（在 Windows Server 上以 IIS 为背景运行的）ASP.NET Core 应用程序的 [Visual Studio](https://www.visualstudio.com/vs/) 支持。</span><span class="sxs-lookup"><span data-stu-id="a4672-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core applications running behind IIS on Windows Server.</span></span> <span data-ttu-id="a4672-106">本主题将指导完成启用此功能，并设置项目。</span><span class="sxs-lookup"><span data-stu-id="a4672-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4672-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="a4672-107">Prerequisites</span></span>

* <span data-ttu-id="a4672-108">Visual Studio（2017/版本 15.3 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="a4672-108">Visual Studio (2017/version 15.3 or later)</span></span>
* <span data-ttu-id="a4672-109">ASP.NET 和 Web 开发工作负荷或 .NET Core 跨平台开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="a4672-109">ASP.NET and web development workload *OR* the .NET Core cross-platform development workload</span></span>

## <a name="enable-iis"></a><span data-ttu-id="a4672-110">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="a4672-110">Enable IIS</span></span>

<span data-ttu-id="a4672-111">启用 IIS。</span><span class="sxs-lookup"><span data-stu-id="a4672-111">Enable IIS.</span></span> <span data-ttu-id="a4672-112">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="a4672-112">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="a4672-113">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="a4672-113">Select the **Internet Information Services** checkbox.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="a4672-115">如果 IIS 安装需要重新启动，重新启动系统。</span><span class="sxs-lookup"><span data-stu-id="a4672-115">If the IIS installation requires a reboot, reboot the system.</span></span>

## <a name="enable-development-time-iis-support"></a><span data-ttu-id="a4672-116">启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="a4672-116">Enable development-time IIS support</span></span>

<span data-ttu-id="a4672-117">安装 IIS 后，启动 Visual Studio 安装程序要修改现有的 Visual Studio 安装。</span><span class="sxs-lookup"><span data-stu-id="a4672-117">Once IIS is installed, launch the Visual Studio installer to modify the existing Visual Studio installation.</span></span> <span data-ttu-id="a4672-118">在安装程序中，选择“开发时 IIS 支持”组件。</span><span class="sxs-lookup"><span data-stu-id="a4672-118">In the installer, select the **Development time IIS support** component.</span></span> <span data-ttu-id="a4672-119">该组件在“ASP.NET 和 Web 开发”工作负荷的“摘要”面板中列为可选组件。</span><span class="sxs-lookup"><span data-stu-id="a4672-119">The component is listed as an optional component in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="a4672-120">此组件将安装 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，该模块是运行 ASP.NET Core 应用程序所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="a4672-120">This installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core applications.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="a4672-124">配置项目</span><span class="sxs-lookup"><span data-stu-id="a4672-124">Configure the project</span></span>

<span data-ttu-id="a4672-125">创建新的启动配置文件以添加开发时 IIS 支持。</span><span class="sxs-lookup"><span data-stu-id="a4672-125">Create a new launch profile to add development-time IIS support.</span></span> <span data-ttu-id="a4672-126">在 Visual Studio 的“解决方案资源管理器”中，右键单击项目，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="a4672-126">In Visual Studio's **Solution Explorer**, right-click the project and select **Properties**.</span></span> <span data-ttu-id="a4672-127">选择“调试”选项卡。从“启动”下拉列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="a4672-127">Select the **Debug** tab. Select **IIS** from the **Launch** dropdown.</span></span> <span data-ttu-id="a4672-128">确认已为“启动浏览器”功能配置了正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="a4672-128">Confirm that the **Launch browser** feature is enabled with the correct URL.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="a4672-133">或者，手动添加到的启动配置文件[launchSettings.json](http://json.schemastore.org/launchsettings)应用程序中的文件：</span><span class="sxs-lookup"><span data-stu-id="a4672-133">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

```json
{
    "iisSettings": {
        "windowsAuthentication": false,
        "anonymousAuthentication": true,
        "iis": {
            "applicationUrl": "http://localhost/WebApplication2",
            "sslPort": 0
        }
    },
    "profiles": {
        "IIS": {
            "commandName": "IIS",
            "launchBrowser": "true",
            "launchUrl": "http://localhost/WebApplication2",
            "environmentVariables": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    }
}
```

<span data-ttu-id="a4672-134">如果未以管理员身份运行 visual Studio 可能会提示重新启动。</span><span class="sxs-lookup"><span data-stu-id="a4672-134">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="a4672-135">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a4672-135">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="a4672-136">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="a4672-136">Congratulations!</span></span> <span data-ttu-id="a4672-137">此时，该项目已配置了开发时间 IIS 支持。</span><span class="sxs-lookup"><span data-stu-id="a4672-137">At this point, the project is configured for development-time IIS support.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a4672-138">其他资源</span><span class="sxs-lookup"><span data-stu-id="a4672-138">Additional resources</span></span>

* [<span data-ttu-id="a4672-139">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a4672-139">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="a4672-140">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="a4672-140">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="a4672-141">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="a4672-141">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
