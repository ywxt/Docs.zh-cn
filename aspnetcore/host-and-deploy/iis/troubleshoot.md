---
title: "解决在 IIS 上的 ASP.NET 核心"
author: guardrex
description: "了解如何使用 IIS 的 ASP.NET Core 应用的部署诊断问题。"
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 03/13/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 2e42d5904e2be8c031c5c6d4bbc104a251b699f2
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="bd974-103">解决在 IIS 上的 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="bd974-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="bd974-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="bd974-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="bd974-105">诊断问题 IIS 部署：</span><span class="sxs-lookup"><span data-stu-id="bd974-105">To diagnose issues with IIS deployments:</span></span>

* <span data-ttu-id="bd974-106">查看浏览器输出。</span><span class="sxs-lookup"><span data-stu-id="bd974-106">Study browser output.</span></span>
* <span data-ttu-id="bd974-107">通过“事件查看器”检查系统的“应用程序”日志。</span><span class="sxs-lookup"><span data-stu-id="bd974-107">Examine the system's **Application** log through **Event Viewer**.</span></span>
* <span data-ttu-id="bd974-108">启用 `stdout` 日志记录</span><span class="sxs-lookup"><span data-stu-id="bd974-108">Enable `stdout` logging.</span></span> <span data-ttu-id="bd974-109">ASP.NET Core 模块日志位于 web.config 中 `<aspNetCore>` 元素的 stdoutLogFile 属性提供的路径上。属性值中提供的路径上的任何文件夹都必须存在于部署中。</span><span class="sxs-lookup"><span data-stu-id="bd974-109">The **ASP.NET Core Module** log is found on the path provided in the *stdoutLogFile* attribute of the `<aspNetCore>` element in *web.config*. Any folders on the path provided in the attribute value must exist in the deployment.</span></span> <span data-ttu-id="bd974-110">设置*stdoutLogEnabled*到`true`。</span><span class="sxs-lookup"><span data-stu-id="bd974-110">Set *stdoutLogEnabled* to `true`.</span></span> <span data-ttu-id="bd974-111">应用程序使用`Microsoft.NET.Sdk.Web`SDK 创建*web.config*文件默认*stdoutLogEnabled*将设置为`false`，请手动提供*web.config*文件或修改文件，以便启用`stdout`日志记录。</span><span class="sxs-lookup"><span data-stu-id="bd974-111">Apps that use the the `Microsoft.NET.Sdk.Web` SDK to create the *web.config* file default the *stdoutLogEnabled* setting to `false`, so manually provide the *web.config* file or modify the file in order to enable `stdout` logging.</span></span>

<span data-ttu-id="bd974-112">使用来自与这些三个源信息[常见错误引用主题](xref:host-and-deploy/azure-iis-errors-reference)以确定问题。</span><span class="sxs-lookup"><span data-stu-id="bd974-112">Use information from those three sources with the [common errors reference topic](xref:host-and-deploy/azure-iis-errors-reference) to determine the problem.</span></span> <span data-ttu-id="bd974-113">请按照用于解决此问题的故障排除建议。</span><span class="sxs-lookup"><span data-stu-id="bd974-113">Follow the troubleshooting advice provided to resolve the issue.</span></span>

<span data-ttu-id="bd974-114">多种常见错误只有在经过模块的 startupTimeLimit（默认值：120 秒）和 startupRetryCount（默认值：2 次）后，才会在浏览器、应用程序日志和 ASP.NET Core 模块日志中显示。</span><span class="sxs-lookup"><span data-stu-id="bd974-114">Several of the common errors don't appear in the browser, Application Log, and ASP.NET Core Module Log until the module *startupTimeLimit* (default: 120 seconds) and *startupRetryCount* (default: 2) have passed.</span></span> <span data-ttu-id="bd974-115">因此，请先等足六分钟，然后再推断出模块无法为应用启动进程。</span><span class="sxs-lookup"><span data-stu-id="bd974-115">Therefore, wait a full six minutes before deducing that the module has failed to start a process for the app.</span></span>

<span data-ttu-id="bd974-116">一种快速确定应用是否正常工作的方法是直接在 Kestrel 上运行应用。</span><span class="sxs-lookup"><span data-stu-id="bd974-116">One quick way to determine if the app is working properly is to run the app directly on Kestrel.</span></span> <span data-ttu-id="bd974-117">如果应用程序作为发布[framework 相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，执行`dotnet <assembly_name>.dll`在部署文件夹中，这是 IIS 到应用的物理路径。</span><span class="sxs-lookup"><span data-stu-id="bd974-117">If the app was published as a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd), execute `dotnet <assembly_name>.dll` in the deployment folder, which is the IIS physical path to the app.</span></span> <span data-ttu-id="bd974-118">如果应用程序作为发布[独立的部署](/dotnet/core/deploying/#self-contained-deployments-scd)中运行应用程序的可执行文件直接从命令提示符处， `<assembly_name>.exe`，部署文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bd974-118">If the app was published as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd), run the app's executable directly from a command prompt, `<assembly_name>.exe`, in the deployment folder.</span></span> <span data-ttu-id="bd974-119">如果 Kestrel 正在侦听默认端口 5000，应用程序应该可以在获得`http://localhost:5000/`。</span><span class="sxs-lookup"><span data-stu-id="bd974-119">If Kestrel is listening on default port 5000, the app should be available at `http://localhost:5000/`.</span></span> <span data-ttu-id="bd974-120">如果应用程序通常响应 Kestrel 终结点地址，该问题更可能是相关的反向代理配置和不太可能在应用内。</span><span class="sxs-lookup"><span data-stu-id="bd974-120">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

<span data-ttu-id="bd974-121">若要确定反向代理是否正常工作的一种方法是针对样式表、 脚本或从应用程序的静态文件中的映像执行简单的静态文件请求*wwwroot*使用[静态文件中间件](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="bd974-121">One way to determine if the reverse proxy is working properly is to perform a simple static file request for a stylesheet, script, or image from the app's static files in *wwwroot* using [Static File Middleware](xref:fundamentals/static-files).</span></span> <span data-ttu-id="bd974-122">如果应用程序可以为静态文件提供服务，但失败 MVC 视图和其他终结点，该问题是不太可能相关的反向代理配置，并且更可能在应用程序 （如 MVC 路由或 500 内部服务器错误）。</span><span class="sxs-lookup"><span data-stu-id="bd974-122">If the app can serve static files but MVC Views and other endpoints are failing, the problem is less likely related to the reverse proxy configuration and more likely within the app (for example, MVC routing or 500 Internal Server Error).</span></span>

<span data-ttu-id="bd974-123">环境变量时 Kestrel 后面 IIS 正常启动，但应用程序不会在系统上运行本地成功运行后，可以临时添加到*web.config*设置`ASPNETCORE_ENVIRONMENT`到`Development`。</span><span class="sxs-lookup"><span data-stu-id="bd974-123">When Kestrel starts normally behind IIS but the app won't run on the system after successfully running locally, an environment variable can be temporarily added to *web.config* to set the `ASPNETCORE_ENVIRONMENT` to `Development`.</span></span> <span data-ttu-id="bd974-124">只要环境不重写应用程序启动时，设置环境变量允许[开发人员异常页](xref:fundamentals/error-handling)显示应用程序运行时。</span><span class="sxs-lookup"><span data-stu-id="bd974-124">As long as the environment isn't overridden in app startup, setting the environment variable allows the [developer exception page](xref:fundamentals/error-handling) to appear when the app is run.</span></span> <span data-ttu-id="bd974-125">设置环境变量中的`ASPNETCORE_ENVIRONMENT`以这种方式仅建议在测试过渡/服务器不公开到 Internet。</span><span class="sxs-lookup"><span data-stu-id="bd974-125">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` in this way is only recommended for staging/testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="bd974-126">请务必删除从该环境变量*web.config*文件完成。</span><span class="sxs-lookup"><span data-stu-id="bd974-126">Be sure to remove the environment variable from the *web.config* file when finished.</span></span> <span data-ttu-id="bd974-127">有关如何设置环境变量通过*web.config*，请参阅[environmentVariables 子元素的 aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="bd974-127">For information on setting environment variables via *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

<span data-ttu-id="bd974-128">在大多数情况下，启用应用程序日志记录有助于排查应用问题或反向代理问题。</span><span class="sxs-lookup"><span data-stu-id="bd974-128">In most cases, enabling application logging assists in troubleshooting problems with the app or the reverse proxy.</span></span> <span data-ttu-id="bd974-129">有关详细信息，请参阅[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="bd974-129">See [Logging](xref:fundamentals/logging/index) for more information.</span></span>

<span data-ttu-id="bd974-130">最后一项故障排除提示将在应用内的开发计算机或包版本上的.NET 核心 SDK 与无法升级或者后运行的应用。</span><span class="sxs-lookup"><span data-stu-id="bd974-130">The last troubleshooting tip pertains to apps that fail to run after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="bd974-131">在某些情况下，不同的包可能在执行主要升级时中断应用。</span><span class="sxs-lookup"><span data-stu-id="bd974-131">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="bd974-132">可通过解决这些问题的大多数：</span><span class="sxs-lookup"><span data-stu-id="bd974-132">Most of these issues can be fixed by:</span></span>

* <span data-ttu-id="bd974-133">删除`bin`和`obj`的项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="bd974-133">Deleting the `bin` and `obj` folders in the project.</span></span>
* <span data-ttu-id="bd974-134">清除包缓存在`%UserProfile%\.nuget\packages\`和`%LocalAppData%\Nuget\v3-cache`。</span><span class="sxs-lookup"><span data-stu-id="bd974-134">Clearing package caches at `%UserProfile%\.nuget\packages\` and `%LocalAppData%\Nuget\v3-cache`.</span></span>
* <span data-ttu-id="bd974-135">还原和重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="bd974-135">Restoring and rebuilding the project.</span></span>
* <span data-ttu-id="bd974-136">确认已完全重新部署应用程序之前删除以前部署到服务器上。</span><span class="sxs-lookup"><span data-stu-id="bd974-136">Confirming that the prior deployment on the server has been completely deleted prior to re-deploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="bd974-137">清除包缓存的简便方法是执行`dotnet nuget locals all --clear`从命令提示符。</span><span class="sxs-lookup"><span data-stu-id="bd974-137">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
> 
> <span data-ttu-id="bd974-138">清除包缓存还可通过使用[nuget.exe](https://www.nuget.org/downloads)工具并执行命令`nuget locals all -clear`。</span><span class="sxs-lookup"><span data-stu-id="bd974-138">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="bd974-139">*nuget.exe*不与 Windows 10 的捆绑的安装，并且必须单独获取从 NuGet 网站。</span><span class="sxs-lookup"><span data-stu-id="bd974-139">*nuget.exe* isn't a bundled install with Windows 10 and must be obtained separately from the NuGet website.</span></span>
<!--
> [!TIP]
> A convenient way to clear package caches is to:
>
> * Obtain the *NuGet.exe* tool from [NuGet.org](https://www.nuget.org/).
> * Add the path to *NuGet.exe* to the system PATH.
> * Execute `nuget locals all -clear` from a command prompt.
>
> Alternatively, execute `dotnet nuget locals all --clear` from a command prompt without obtaining *NuGet.exe*. -->

## <a name="additional-resources"></a><span data-ttu-id="bd974-140">其他资源</span><span class="sxs-lookup"><span data-stu-id="bd974-140">Additional resources</span></span>

* [<span data-ttu-id="bd974-141">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="bd974-141">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="bd974-142">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="bd974-142">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
