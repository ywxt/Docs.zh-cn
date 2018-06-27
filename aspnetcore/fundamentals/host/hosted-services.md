---
title: 在 ASP.NET Core 中使用托管服务实现后台任务
author: guardrex
description: 了解如何在 ASP.NET Core 中使用托管服务实现后台任务。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/hosted-services
ms.openlocfilehash: 13ac7e266b657bc186188b2b6f40204cfd936fca
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341816"
---
# <a name="background-tasks-with-hosted-services-in-aspnet-core"></a><span data-ttu-id="dab48-103">在 ASP.NET Core 中使用托管服务实现后台任务</span><span class="sxs-lookup"><span data-stu-id="dab48-103">Background tasks with hosted services in ASP.NET Core</span></span>

<span data-ttu-id="dab48-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="dab48-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="dab48-105">在 ASP.NET Core 中，后台任务作为托管服务实现。</span><span class="sxs-lookup"><span data-stu-id="dab48-105">In ASP.NET Core, background tasks can be implemented as *hosted services*.</span></span> <span data-ttu-id="dab48-106">托管服务是一个类，具有实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="dab48-106">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="dab48-107">本主题提供了三个托管服务示例：</span><span class="sxs-lookup"><span data-stu-id="dab48-107">This topic provides three hosted service examples:</span></span>

* <span data-ttu-id="dab48-108">在计时器上运行的后台任务。</span><span class="sxs-lookup"><span data-stu-id="dab48-108">Background task that runs on a timer.</span></span>
* <span data-ttu-id="dab48-109">激活有作用域的服务的托管服务。</span><span class="sxs-lookup"><span data-stu-id="dab48-109">Hosted service that activates a scoped service.</span></span> <span data-ttu-id="dab48-110">有作用域的服务可使用依赖项注入。</span><span class="sxs-lookup"><span data-stu-id="dab48-110">The scoped service can use dependency injection.</span></span>
* <span data-ttu-id="dab48-111">按顺序运行的已排队后台任务。</span><span class="sxs-lookup"><span data-stu-id="dab48-111">Queued background tasks that run sequentially.</span></span>

<span data-ttu-id="dab48-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/hosted-services/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="dab48-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/hosted-services/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="dab48-113">此示例应用分为两个版本：</span><span class="sxs-lookup"><span data-stu-id="dab48-113">The sample app is provided in two versions:</span></span>

* <span data-ttu-id="dab48-114">Web 主机 &ndash; Web 主机可用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="dab48-114">Web Host &ndash; The Web Host is useful for hosting web apps.</span></span> <span data-ttu-id="dab48-115">本主题中所示的示例代码来自示例的 Web 主机版本。</span><span class="sxs-lookup"><span data-stu-id="dab48-115">The example code shown in this topic is from the Web Host version of the sample.</span></span> <span data-ttu-id="dab48-116">有关详细信息，请参阅 [Web 主机](xref:fundamentals/host/web-host)主题。</span><span class="sxs-lookup"><span data-stu-id="dab48-116">For more information, see the [Web Host](xref:fundamentals/host/web-host) topic.</span></span>
* <span data-ttu-id="dab48-117">通用主机 &ndash; 通用主机是 ASP.NET Core 2.1 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="dab48-117">Generic Host &ndash; The Generic Host is new in ASP.NET Core 2.1.</span></span> <span data-ttu-id="dab48-118">有关详细信息，请参阅[通用主机](xref:fundamentals/host/generic-host)主题。</span><span class="sxs-lookup"><span data-stu-id="dab48-118">For more information, see the [Generic Host](xref:fundamentals/host/generic-host) topic.</span></span>

::: moniker-end

## <a name="ihostedservice-interface"></a><span data-ttu-id="dab48-119">IHostedService 接口</span><span class="sxs-lookup"><span data-stu-id="dab48-119">IHostedService interface</span></span>

<span data-ttu-id="dab48-120">托管服务实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口。</span><span class="sxs-lookup"><span data-stu-id="dab48-120">Hosted services implement the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="dab48-121">该接口为主机托管的对象定义了两种方法：</span><span class="sxs-lookup"><span data-stu-id="dab48-121">The interface defines two methods for objects that are managed by the host:</span></span>

* <span data-ttu-id="dab48-122">[StartAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) - 启动服务器并触发 [IApplicationLifetime.ApplicationStarted](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstarted) 后调用。</span><span class="sxs-lookup"><span data-stu-id="dab48-122">[StartAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) - Called after the server has started and [IApplicationLifetime.ApplicationStarted](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstarted) is triggered.</span></span> <span data-ttu-id="dab48-123">`StartAsync` 包含启动后台任务的逻辑。</span><span class="sxs-lookup"><span data-stu-id="dab48-123">`StartAsync` contains the logic to start the background task.</span></span>

* <span data-ttu-id="dab48-124">[StopAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) - 主机正常关闭时触发。</span><span class="sxs-lookup"><span data-stu-id="dab48-124">[StopAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) - Triggered when the host is performing a graceful shutdown.</span></span> <span data-ttu-id="dab48-125">`StopAsync` 包含结束后台任务和处理任何非托管资源的逻辑。</span><span class="sxs-lookup"><span data-stu-id="dab48-125">`StopAsync` contains the logic to end the background task and dispose of any unmanaged resources.</span></span> <span data-ttu-id="dab48-126">如果应用意外关闭（例如，应用的进程失败），则可能不会调用 `StopAsync`。</span><span class="sxs-lookup"><span data-stu-id="dab48-126">If the app shuts down unexpectedly (for example, the app's process fails), `StopAsync` might not be called.</span></span>

<span data-ttu-id="dab48-127">托管服务在应用启动时激活一次，在应用关闭时正常关闭。</span><span class="sxs-lookup"><span data-stu-id="dab48-127">The hosted service is activated once at app startup and gracefully shutdown at app shutdown.</span></span> <span data-ttu-id="dab48-128">实现 [IDisposable](/dotnet/api/system.idisposable) 时，可在处置服务容器时处理资源。</span><span class="sxs-lookup"><span data-stu-id="dab48-128">When [IDisposable](/dotnet/api/system.idisposable) is implemented, resources can be disposed when the service container is disposed.</span></span> <span data-ttu-id="dab48-129">如果在执行后台任务期间引发错误，即使未调用 `StopAsync`，也应调用 `Dispose`。</span><span class="sxs-lookup"><span data-stu-id="dab48-129">If an error is thrown during background task execution, `Dispose` should be called even if `StopAsync` isn't called.</span></span>

## <a name="timed-background-tasks"></a><span data-ttu-id="dab48-130">计时的后台任务</span><span class="sxs-lookup"><span data-stu-id="dab48-130">Timed background tasks</span></span>

<span data-ttu-id="dab48-131">定时后台任务使用 [System.Threading.Timer](/dotnet/api/system.threading.timer) 类。</span><span class="sxs-lookup"><span data-stu-id="dab48-131">A timed background task makes use of the [System.Threading.Timer](/dotnet/api/system.threading.timer) class.</span></span> <span data-ttu-id="dab48-132">计时器触发任务的 `DoWork` 方法。</span><span class="sxs-lookup"><span data-stu-id="dab48-132">The timer triggers the task's `DoWork` method.</span></span> <span data-ttu-id="dab48-133">在 `StopAsync` 上禁用计时器，并在 `Dispose` 上处置服务容器时处置计时器：</span><span class="sxs-lookup"><span data-stu-id="dab48-133">The timer is disabled on `StopAsync` and disposed when the service container is disposed on `Dispose`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/TimedHostedService.cs?name=snippet1&highlight=15-16,30,37)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="dab48-134">已使用 `AddHostedService` 扩展方法在 `Startup.ConfigureServices` 中注册该服务：</span><span class="sxs-lookup"><span data-stu-id="dab48-134">The service is registered in `Startup.ConfigureServices` with the `AddHostedService` extension method:</span></span>

<span data-ttu-id="dab48-135">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="dab48-135">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="dab48-136">已在 `Startup.ConfigureServices` 中注册该服务：</span><span class="sxs-lookup"><span data-stu-id="dab48-136">The service is registered in `Startup.ConfigureServices`:</span></span>

<span data-ttu-id="dab48-137">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="dab48-137">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]</span></span>

::: moniker-end

## <a name="consuming-a-scoped-service-in-a-background-task"></a><span data-ttu-id="dab48-138">在后台任务中使用有作用域的服务</span><span class="sxs-lookup"><span data-stu-id="dab48-138">Consuming a scoped service in a background task</span></span>

<span data-ttu-id="dab48-139">要在 `IHostedService` 中使用有作用域的服务，请创建一个作用域。</span><span class="sxs-lookup"><span data-stu-id="dab48-139">To use scoped services within an `IHostedService`, create a scope.</span></span> <span data-ttu-id="dab48-140">默认情况下，不会为托管服务创建作用域。</span><span class="sxs-lookup"><span data-stu-id="dab48-140">No scope is created for a hosted service by default.</span></span>

<span data-ttu-id="dab48-141">作用域后台任务服务包含后台任务的逻辑。</span><span class="sxs-lookup"><span data-stu-id="dab48-141">The scoped background task service contains the background task's logic.</span></span> <span data-ttu-id="dab48-142">在以下示例中，将 [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger) 注入到服务中：</span><span class="sxs-lookup"><span data-stu-id="dab48-142">In the following example, [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger) is injected into the service:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ScopedProcessingService.cs?name=snippet1)]

<span data-ttu-id="dab48-143">托管服务创建一个作用域来解决作用域后台任务服务以调用其 `DoWork` 方法：</span><span class="sxs-lookup"><span data-stu-id="dab48-143">The hosted service creates a scope to resolve the scoped background task service to call its `DoWork` method:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ConsumeScopedServiceHostedService.cs?name=snippet1&highlight=29-36)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="dab48-144">已在 `Startup.ConfigureServices` 中注册这些服务。</span><span class="sxs-lookup"><span data-stu-id="dab48-144">The services are registered in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="dab48-145">已使用 `AddHostedService` 扩展方法注册 `IHostedService` 实现：</span><span class="sxs-lookup"><span data-stu-id="dab48-145">The `IHostedService` implementation is registered with the `AddHostedService` extension method:</span></span>

<span data-ttu-id="dab48-146">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]</span><span class="sxs-lookup"><span data-stu-id="dab48-146">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="dab48-147">已在 `Startup.ConfigureServices` 中注册这些服务：</span><span class="sxs-lookup"><span data-stu-id="dab48-147">The services are registered in `Startup.ConfigureServices`:</span></span>

<span data-ttu-id="dab48-148">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]</span><span class="sxs-lookup"><span data-stu-id="dab48-148">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]</span></span>

::: moniker-end

## <a name="queued-background-tasks"></a><span data-ttu-id="dab48-149">排队的后台任务</span><span class="sxs-lookup"><span data-stu-id="dab48-149">Queued background tasks</span></span>

<span data-ttu-id="dab48-150">后台任务队列基于 .NET 4.x [QueueBackgroundWorkItem](/dotnet/api/system.web.hosting.hostingenvironment.queuebackgroundworkitem)（[暂定为 ASP.NET Core 3.0 内置版本](https://github.com/aspnet/Hosting/issues/1280)）：</span><span class="sxs-lookup"><span data-stu-id="dab48-150">A background task queue is based on the .NET 4.x [QueueBackgroundWorkItem](/dotnet/api/system.web.hosting.hostingenvironment.queuebackgroundworkitem) ([tentatively scheduled to be built-in for ASP.NET Core 3.0](https://github.com/aspnet/Hosting/issues/1280)):</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/BackgroundTaskQueue.cs?name=snippet1)]

<span data-ttu-id="dab48-151">在 `QueueHostedService` 中，取消排队并执行队列中的后台任务 (`workItem`)：</span><span class="sxs-lookup"><span data-stu-id="dab48-151">In `QueueHostedService`, background tasks (`workItem`) in the queue are dequeued and executed:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/QueuedHostedService.cs?name=snippet1&highlight=30-31,35)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="dab48-152">已在 `Startup.ConfigureServices` 中注册这些服务。</span><span class="sxs-lookup"><span data-stu-id="dab48-152">The services are registered in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="dab48-153">已使用 `AddHostedService` 扩展方法注册 `IHostedService` 实现：</span><span class="sxs-lookup"><span data-stu-id="dab48-153">The `IHostedService` implementation is registered with the `AddHostedService` extension method:</span></span>

<span data-ttu-id="dab48-154">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]</span><span class="sxs-lookup"><span data-stu-id="dab48-154">[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="dab48-155">已在 `Startup.ConfigureServices` 中注册这些服务：</span><span class="sxs-lookup"><span data-stu-id="dab48-155">The services are registered in `Startup.ConfigureServices`:</span></span>

<span data-ttu-id="dab48-156">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]</span><span class="sxs-lookup"><span data-stu-id="dab48-156">[!code-csharp[](hosted-services/samples-snapshot/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]</span></span>

::: moniker-end

<span data-ttu-id="dab48-157">在索引页模型类中，将 `IBackgroundTaskQueue` 注入构造函数并分配给 `Queue`：</span><span class="sxs-lookup"><span data-stu-id="dab48-157">In the Index page model class, the `IBackgroundTaskQueue` is injected into the constructor and assigned to `Queue`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="dab48-158">在索引页上选择“添加任务”按钮时，会执行 `OnPostAddTask` 方法。</span><span class="sxs-lookup"><span data-stu-id="dab48-158">When the **Add Task** button is selected on the Index page, the `OnPostAddTask` method is executed.</span></span> <span data-ttu-id="dab48-159">调用 `QueueBackgroundWorkItem` 来将工作项排入队列：</span><span class="sxs-lookup"><span data-stu-id="dab48-159">`QueueBackgroundWorkItem` is called to enqueue the work item:</span></span>

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet2)]

## <a name="additional-resources"></a><span data-ttu-id="dab48-160">其他资源</span><span class="sxs-lookup"><span data-stu-id="dab48-160">Additional resources</span></span>

* [<span data-ttu-id="dab48-161">使用 IHostedService 和 BackgroundService 类在微服务中实现后台任务</span><span class="sxs-lookup"><span data-stu-id="dab48-161">Implement background tasks in microservices with IHostedService and the BackgroundService class</span></span>](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)
* [<span data-ttu-id="dab48-162">System.Threading.Timer</span><span class="sxs-lookup"><span data-stu-id="dab48-162">System.Threading.Timer</span></span>](/dotnet/api/system.threading.timer)
