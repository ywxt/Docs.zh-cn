---
title: 在 ASP.NET Core 中使用托管服务实现后台任务
author: guardrex
description: 了解如何在 ASP.NET Core 中使用托管服务实现后台任务。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
uid: fundamentals/host/hosted-services
ms.openlocfilehash: 92905d86cb963d01f1806f08d07b270a7f6d8563
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207402"
---
# <a name="background-tasks-with-hosted-services-in-aspnet-core"></a>在 ASP.NET Core 中使用托管服务实现后台任务

作者：[Luke Latham](https://github.com/guardrex)

在 ASP.NET Core 中，后台任务作为托管服务实现。 托管服务是一个类，具有实现 <xref:Microsoft.Extensions.Hosting.IHostedService> 接口的后台任务逻辑。 本主题提供了三个托管服务示例：

* 在计时器上运行的后台任务。
* 激活有作用域的服务的托管服务。 有作用域的服务可使用依赖项注入。
* 按顺序运行的已排队后台任务。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/hosted-services/samples/)（[如何下载](xref:index#how-to-download-a-sample)）

此示例应用分为两个版本：

* Web 主机 &ndash; Web 主机可用于托管 Web 应用。 本主题中所示的示例代码来自示例的 Web 主机版本。 有关详细信息，请参阅 [Web 主机](xref:fundamentals/host/web-host)主题。
* 通用主机 &ndash; 通用主机是 ASP.NET Core 2.1 中的新增功能。 有关详细信息，请参阅[通用主机](xref:fundamentals/host/generic-host)主题。

## <a name="package"></a>Package

引用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)或将包引用添加到 [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) 包。

## <a name="ihostedservice-interface"></a>IHostedService 接口

托管服务实现 <xref:Microsoft.Extensions.Hosting.IHostedService> 接口。 该接口为主机托管的对象定义了两种方法：

* [StartAsync(CancellationToken)](xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*) - `StartAsync` 包含启动后台任务的逻辑。 当使用 [Web 主机](xref:fundamentals/host/web-host)时，会在启动服务器并触发 [IApplicationLifetime.ApplicationStarted](xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime.ApplicationStarted*) 后调用 `StartAsync`。 当使用[通用主机](xref:fundamentals/host/generic-host)时，会在触发 `ApplicationStarted` 之前调用 `StartAsync`。

* [StopAsync(CancellationToken)](xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*) - 主机正常关闭时触发。 `StopAsync` 包含结束后台任务和处理任何非托管资源的逻辑。 如果应用意外关闭（例如，应用的进程失败），则可能不会调用 `StopAsync`。

托管服务在应用启动时激活一次，在应用关闭时正常关闭。 实现 <xref:System.IDisposable> 后，可在处置服务容器时处理资源。 如果在执行后台任务期间引发错误，即使未调用 `StopAsync`，也应调用 `Dispose`。

## <a name="timed-background-tasks"></a>计时的后台任务

定时后台任务使用 [System.Threading.Timer](xref:System.Threading.Timer) 类。 计时器触发任务的 `DoWork` 方法。 在 `StopAsync` 上禁用计时器，并在 `Dispose` 上处置服务容器时处置计时器：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/TimedHostedService.cs?name=snippet1&highlight=15-16,30,37)]

已使用 `AddHostedService` 扩展方法在 `Startup.ConfigureServices` 中注册该服务：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet1)]

## <a name="consuming-a-scoped-service-in-a-background-task"></a>在后台任务中使用有作用域的服务

要在 `IHostedService` 中使用有作用域的服务，请创建一个作用域。 默认情况下，不会为托管服务创建作用域。

作用域后台任务服务包含后台任务的逻辑。 在以下示例中，将 <xref:Microsoft.Extensions.Logging.ILogger> 注入到服务中：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ScopedProcessingService.cs?name=snippet1)]

托管服务创建一个作用域来解决作用域后台任务服务以调用其 `DoWork` 方法：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/ConsumeScopedServiceHostedService.cs?name=snippet1&highlight=29-36)]

已在 `Startup.ConfigureServices` 中注册这些服务。 已使用 `AddHostedService` 扩展方法注册 `IHostedService` 实现：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet2)]

## <a name="queued-background-tasks"></a>排队的后台任务

后台任务队列基于 .NET 4.x <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem*>（[暂定为 ASP.NET Core 3.0 内置版本](https://github.com/aspnet/Hosting/issues/1280)）：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/BackgroundTaskQueue.cs?name=snippet1)]

在 `QueueHostedService` 中，队列中的后台任务会取消排队，并作为 <xref:Microsoft.Extensions.Hosting.BackgroundService> 执行，此类是用于实现长时间运行 `IHostedService` 的基类：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Services/QueuedHostedService.cs?name=snippet1&highlight=21,25)]

已在 `Startup.ConfigureServices` 中注册这些服务。 已使用 `AddHostedService` 扩展方法注册 `IHostedService` 实现：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Startup.cs?name=snippet3)]

在索引页模型类中，将 `IBackgroundTaskQueue` 注入构造函数并分配给 `Queue`：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet1)]

在索引页上选择“添加任务”按钮时，会执行 `OnPostAddTask` 方法。 调用 `QueueBackgroundWorkItem` 来将工作项排入队列：

[!code-csharp[](hosted-services/samples/2.x/BackgroundTasksSample-WebHost/Pages/Index.cshtml.cs?name=snippet2)]

## <a name="additional-resources"></a>其他资源

* [使用 IHostedService 和 BackgroundService 类在微服务中实现后台任务](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)
* [System.Threading.Timer](xref:System.Threading.Timer)
