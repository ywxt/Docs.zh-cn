---
title: "Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持"
author: shirhatti
description: "发现的用于调试 ASP.NET Core 应用时在 Windows Server 上运行之后 IIS 的支持。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: a8bdf4c0c0399c62666e6e61e70c0298a42c2c12
ms.sourcegitcommit: 9f758b1550fcae88ab1eb284798a89e6320548a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="ca41b-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="ca41b-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="ca41b-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="ca41b-104">By: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="ca41b-105">本指南介绍了[Visual Studio](https://www.visualstudio.com/vs/)支持的用于调试在 IIS 后面运行 Windows Server 上的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="ca41b-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="ca41b-106">本主题将指导完成启用此功能，并设置项目。</span><span class="sxs-lookup"><span data-stu-id="ca41b-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca41b-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="ca41b-107">Prerequisites</span></span>

* <span data-ttu-id="ca41b-108">Visual Studio（2017/版本 15.3 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="ca41b-108">Visual Studio (2017/version 15.3 or later)</span></span>
* <span data-ttu-id="ca41b-109">ASP.NET 和 Web 开发工作负荷或 .NET Core 跨平台开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="ca41b-109">ASP.NET and web development workload *OR* the .NET Core cross-platform development workload</span></span>

## <a name="enable-iis"></a><span data-ttu-id="ca41b-110">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="ca41b-110">Enable IIS</span></span>

<span data-ttu-id="ca41b-111">启用 IIS。</span><span class="sxs-lookup"><span data-stu-id="ca41b-111">Enable IIS.</span></span> <span data-ttu-id="ca41b-112">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="ca41b-112">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="ca41b-113">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="ca41b-113">Select the **Internet Information Services** checkbox.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="ca41b-115">如果 IIS 安装需要重新启动，重新启动系统。</span><span class="sxs-lookup"><span data-stu-id="ca41b-115">If the IIS installation requires a restart, restart the system.</span></span>

## <a name="enable-development-time-iis-support"></a><span data-ttu-id="ca41b-116">启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="ca41b-116">Enable development-time IIS support</span></span>

<span data-ttu-id="ca41b-117">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="ca41b-117">Launch the Visual Studio installer.</span></span> <span data-ttu-id="ca41b-118">选择**IIS 支持的开发时间**组件。</span><span class="sxs-lookup"><span data-stu-id="ca41b-118">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="ca41b-119">列出为可选中了该组件**摘要**面板**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="ca41b-119">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="ca41b-120">这将安装[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)，即运行 ASP.NET Core 应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="ca41b-120">This installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="ca41b-124">配置项目</span><span class="sxs-lookup"><span data-stu-id="ca41b-124">Configure the project</span></span>

<span data-ttu-id="ca41b-125">创建新的启动配置文件以添加开发时 IIS 支持。</span><span class="sxs-lookup"><span data-stu-id="ca41b-125">Create a new launch profile to add development-time IIS support.</span></span> <span data-ttu-id="ca41b-126">在 Visual Studio 的“解决方案资源管理器”中，右键单击项目，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="ca41b-126">In Visual Studio's **Solution Explorer**, right-click the project and select **Properties**.</span></span> <span data-ttu-id="ca41b-127">选择“调试”选项卡。从“启动”下拉列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="ca41b-127">Select the **Debug** tab. Select **IIS** from the **Launch** dropdown.</span></span> <span data-ttu-id="ca41b-128">确认已为“启动浏览器”功能配置了正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="ca41b-128">Confirm that the **Launch browser** feature is enabled with the correct URL.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="ca41b-133">或者，手动添加到的启动配置文件[launchSettings.json](http://json.schemastore.org/launchsettings)应用程序中的文件：</span><span class="sxs-lookup"><span data-stu-id="ca41b-133">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

<span data-ttu-id="ca41b-134">如果未以管理员身份运行 visual Studio 可能会提示重新启动。</span><span class="sxs-lookup"><span data-stu-id="ca41b-134">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="ca41b-135">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ca41b-135">If prompted, restart Visual Studio.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca41b-136">其他资源</span><span class="sxs-lookup"><span data-stu-id="ca41b-136">Additional resources</span></span>

* [<span data-ttu-id="ca41b-137">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca41b-137">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="ca41b-138">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="ca41b-138">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="ca41b-139">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="ca41b-139">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
