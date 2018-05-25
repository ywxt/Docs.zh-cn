---
title: 在 ASP.NET Core 中使用托管服务实现后台任务
author: guardrex
description: 了解如何在 ASP.NET Core 中使用托管服务实现后台任务。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/hosted-services
ms.openlocfilehash: ace7fc8622864099b7c0e36e4a914de340d4d4e9
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="background-tasks-with-hosted-services-in-aspnet-core"></a>在 ASP.NET Core 中使用托管服务实现后台任务

作者：[Luke Latham](https://github.com/guardrex)

在 ASP.NET Core 中，后台任务作为托管服务实现。 托管服务是一个类，具有实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口的后台任务逻辑。 本主题提供了三个托管服务示例：

* 在计时器上运行的后台任务。
* 激活有作用域的服务的托管服务。 有作用域的服务可使用依赖项注入。
* 按顺序运行的已排队后台任务。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/hosted-services/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="ihostedservice-interface"></a>IHostedService 接口

托管服务实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口。 该接口为主机托管的对象定义了两种方法：

* [StartAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) - 启动服务器并触发 [IApplicationLifetime.ApplicationStarted](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstarted) 后调用。 `StartAsync` 包含启动后台任务的逻辑。

* [StopAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) - 主机正常关闭时触发。 `StopAsync` 包含结束后台任务和处理任何非托管资源的逻辑。 如果应用意外关闭（例如，应用的进程失败），则可能不会调用 `StopAsync`。

托管服务是在应用启动时激活一次并在应用关闭时正常关闭的单一实例。 实现 [IDisposable](/dotnet/api/system.idisposable) 时，可在处置服务容器时处理资源。 如果在执行后台任务期间引发错误，即使未调用 `StopAsync`，也应调用 `Dispose`。

## <a name="timed-background-tasks"></a>计时的后台任务

定时后台任务使用 [System.Threading.Timer](/dotnet/api/system.threading.timer) 类。 计时器触发任务的 `DoWork` 方法。 在 `StopAsync` 上禁用计时器，并在 `Dispose` 上处置服务容器时处置计时器：

[!code-csharp[](hosted-services/samples/2.x/Services/TimedHostedService.cs?name=snippet1&highlight=15-16,30,37)]

已在 `Startup.ConfigureServices` 中注册该服务：

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet1)]

## <a name="consuming-a-scoped-service-in-a-background-task"></a>在后台任务中使用有作用域的服务

要在 `IHostedService` 中使用有作用域的服务，请创建一个作用域。 默认情况下，不会为托管服务创建作用域。

作用域后台任务服务包含后台任务的逻辑。 在以下示例中，将 [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger) 注入到服务中：

[!code-csharp[](hosted-services/samples/2.x/Services/ScopedProcessingService.cs?name=snippet1)]

托管服务创建一个作用域来解决作用域后台任务服务以调用其 `DoWork` 方法：

[!code-csharp[](hosted-services/samples/2.x/Services/ConsumeScopedServiceHostedService.cs?name=snippet1&highlight=29-36)]

已在 `Startup.ConfigureServices` 中注册这些服务：

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet2)]

## <a name="queued-background-tasks"></a>排队的后台任务

后台任务队列基于 .NET 4.x [QueueBackgroundWorkItem](/dotnet/api/system.web.hosting.hostingenvironment.queuebackgroundworkitem)（[暂定为 ASP.NET Core 2.2 内置版本](https://github.com/aspnet/Hosting/issues/1280)）：

[!code-csharp[](hosted-services/samples/2.x/Services/BackgroundTaskQueue.cs?name=snippet1)]

在 `QueueHostedService` 中，取消排队并执行队列中的后台任务 (`workItem`)：

[!code-csharp[](hosted-services/samples/2.x/Services/QueuedHostedService.cs?name=snippet1&highlight=30-31,35)]

已在 `Startup.ConfigureServices` 中注册这些服务：

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet3)]

在索引页模型类中，将 `IBackgroundTaskQueue` 注入构造函数并分配给 `Queue`：

[!code-csharp[](hosted-services/samples/2.x/Pages/Index.cshtml.cs?name=snippet1)]

在索引页上选择“添加任务”按钮时，会执行 `OnPostAddTask` 方法。 调用 `QueueBackgroundWorkItem` 来将工作项排入队列：

[!code-csharp[](hosted-services/samples/2.x/Pages/Index.cshtml.cs?name=snippet2)]

## <a name="additional-resources"></a>其他资源

* [使用 IHostedService 和 BackgroundService 类在微服务中实现后台任务](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)
* [System.Threading.Timer](/dotnet/api/system.threading.timer)
