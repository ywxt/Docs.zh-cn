---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现的用于调试 ASP.NET Core 应用时在 Windows Server 上运行之后 IIS 的支持。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 218bb2653b92cd7b1cf2c6726b2d4bedbf307a62
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="7097c-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="7097c-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="7097c-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="7097c-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="7097c-105">本指南介绍了[Visual Studio](https://www.visualstudio.com/vs/)支持的用于调试在 IIS 后面运行 Windows Server 上的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="7097c-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="7097c-106">本主题将指导完成启用此功能，并设置项目。</span><span class="sxs-lookup"><span data-stu-id="7097c-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7097c-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="7097c-107">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="7097c-108">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="7097c-108">Enable IIS</span></span>

<span data-ttu-id="7097c-109">启用 IIS。</span><span class="sxs-lookup"><span data-stu-id="7097c-109">Enable IIS.</span></span> <span data-ttu-id="7097c-110">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="7097c-110">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="7097c-111">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="7097c-111">Select the **Internet Information Services** checkbox.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="7097c-113">如果 IIS 安装需要重新启动，则重新启动系统。</span><span class="sxs-lookup"><span data-stu-id="7097c-113">If the IIS installation requires a restart, restart the system.</span></span>

## <a name="enable-development-time-iis-support"></a><span data-ttu-id="7097c-114">启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="7097c-114">Enable development-time IIS support</span></span>

<span data-ttu-id="7097c-115">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="7097c-115">Launch the Visual Studio installer.</span></span> <span data-ttu-id="7097c-116">选择**IIS 支持的开发时间**组件。</span><span class="sxs-lookup"><span data-stu-id="7097c-116">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="7097c-117">列出为可选中了该组件**摘要**面板**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="7097c-117">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="7097c-118">这将安装[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)，即运行 ASP.NET Core 应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="7097c-118">This installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="7097c-122">配置项目</span><span class="sxs-lookup"><span data-stu-id="7097c-122">Configure the project</span></span>

<span data-ttu-id="7097c-123">创建新的启动配置文件以添加开发时 IIS 支持。</span><span class="sxs-lookup"><span data-stu-id="7097c-123">Create a new launch profile to add development-time IIS support.</span></span> <span data-ttu-id="7097c-124">在 Visual Studio 的“解决方案资源管理器”中，右键单击项目，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="7097c-124">In Visual Studio's **Solution Explorer**, right-click the project and select **Properties**.</span></span> <span data-ttu-id="7097c-125">选择“调试”选项卡。从“启动”下拉列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="7097c-125">Select the **Debug** tab. Select **IIS** from the **Launch** dropdown.</span></span> <span data-ttu-id="7097c-126">确认已为“启动浏览器”功能配置了正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="7097c-126">Confirm that the **Launch browser** feature is enabled with the correct URL.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="7097c-131">或者，手动添加到的启动配置文件[launchSettings.json](http://json.schemastore.org/launchsettings)应用程序中的文件：</span><span class="sxs-lookup"><span data-stu-id="7097c-131">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

<span data-ttu-id="7097c-132">如果未以管理员身份运行 visual Studio 可能会提示重新启动。</span><span class="sxs-lookup"><span data-stu-id="7097c-132">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="7097c-133">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7097c-133">If prompted, restart Visual Studio.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7097c-134">其他资源</span><span class="sxs-lookup"><span data-stu-id="7097c-134">Additional resources</span></span>

* [<span data-ttu-id="7097c-135">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7097c-135">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="7097c-136">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="7097c-136">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="7097c-137">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="7097c-137">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
