---
title: .NET 通用主机
author: guardrex
description: 了解有关 .NET 中负责应用启动和生存期管理的通用主机。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/generic-host
ms.openlocfilehash: 15f4a689b2756d2bfb6320ab31f2e8d63af51a09
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="net-generic-host"></a>.NET 通用主机

作者：[Luke Latham](https://github.com/guardrex)

.NET 应用配置和启动主机。 主机负责应用程序启动和生存期管理。 本主题介绍 ASP.NET Core 通用主机 ([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder))，该主机对于托管不处理 HTTP 请求的应用非常有用。 有关 Web 主机 ([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)) 的介绍，请参阅 [Web 主机](xref:fundamentals/host/web-host)主题。

通用主机的目标是将 HTTP 管道从 Web 主机 API 中分离出来，从而启用更多的主机方案。 基于通用主机的消息、后台任务和其他非 HTTP 工作负载可从横切功能（如配置、依赖关系注入 [DI] 和日志记录）中受益。

通用主机是 ASP.NET Core 2.1 中的新增功能，不适用于 Web 承载方案。 对于 Web 承载方案，请使用 [Web 主机](xref:fundamentals/host/web-host)。 通用主机正处于开发阶段，用于在未来版本中替换 Web 主机，并在 HTTP 和非 HTTP 方案中充当主要的主机 API。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

在 [Visual Studio Code](https://code.visualstudio.com/) 中运行示例应用时，请使用外部或集成终端。 请勿在 `internalConsole` 中运行示例。

在 Visual Studio Code 中设置控制台：

1. 打开 .vscode/launch.json 文件。
1. 在 .NET Core 启动（控制台）配置中，找到控制台条目。 将值设置为 `externalTerminal` 或 `integratedTerminal`。

## <a name="introduction"></a>介绍

通用主机库位于 [Microsoft.Extensions.Hosting 命名空间](/dotnet/api/microsoft.extensions.hosting)中，由 [Microsoft.Extensions.Hosting NuGet 包](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/)提供。 [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) 元包中包括 `Microsoft.Extensions.Hosting` 包。

[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 是执行代码的入口点。 每个 `IHostedService` 实现都按照 [ConfigureServices 中服务注册](#configureservices)的顺序执行。 主机启动时，每个 `IHostedService` 上都会调用 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync)主机正常关闭时，以反向注册顺序调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync)。

## <a name="set-up-a-host"></a>设置主机

[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 是供库和应用初始化、生成和运行主机的主要组件：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="host-configuration"></a>主机配置

[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) 依赖于以下方法来设置主机配置值：

* 配置生成器
* 扩展方法配置

### <a name="configuration-builder"></a>配置生成器

通过在 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 实现上调用 [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration) 来创建主机生成器配置。 `ConfigureHostConfiguration` 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 为主机创建 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)。 配置生成器初始化 [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)，以在应用程序的生成过程中使用。 可以利用相加结果多次调用 `ConfigureHostConfiguration`。 主机使用任何一个选项设置上一个值。

hostsettings.json：

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

示例 `HostBuilder` 配置使用 `ConfigureHostConfiguration`：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

> [!NOTE]
> [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 扩展方法当前不能分析由 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) 返回的配置部分（例如 `.AddConfiguration(Configuration.GetSection("section"))`）。 `GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:environment`）。 `AddConfiguration` 方法需要键来匹配 `HostBuilder` 键（例如 `environment`）。 键上存在的节名称阻止节的值配置主机。 将在即将发布的版本中解决此问题。 有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。

### <a name="extension-method-configuration"></a>扩展方法配置

在 `IHostBuilder` 实现上调用扩展方法，用于配置内容根和环境。

#### <a name="content-root"></a>内容根

此设置确定主机从哪里开始搜索内容文件。

**键**：contentRoot  
**类型**：string  
**默认值**：默认为应用程序集所在的文件夹。  
**设置使用**：`UseContentRoot`  
**环境变量**：`ASPNETCORE_CONTENTROOT`

如果路径不存在，主机将无法启动。

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

#### <a name="environment"></a>环境

设置应用的[环境](xref:fundamentals/environments)。

**键**：环境  
**类型**：string  
**默认值**：生产  
**设置使用**：`UseEnvironment`  
**环境变量**：`ASPNETCORE_ENVIRONMENT`

环境可以设置为任何值。 框架定义的值包括 `Development``Staging` 和 `Production`。 值不区分大小写。 默认情况下，从 `ASPNETCORE_ENVIRONMENT` 环境变量读取环境。 使用 [Visual Studio](https://www.visualstudio.com/) 时，可能会在 launchSettings.json 文件中设置环境变量。 有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

## <a name="configureappconfiguration"></a>ConfigureAppConfiguration

通过在 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 实现上调用 [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration) 来创建应用生成器配置。 `ConfigureAppConfiguration` 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 为应用创建 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)。 可多次调用 `ConfigureAppConfiguration`，并得到累计结果。 应用会使用最后设置值的选项。 用于进行后续操作和 [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services) 中的 [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration) 中可以使用由 `ConfigureAppConfiguration` 创建的配置。

示例应用配置使用 `ConfigureAppConfiguration`：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

appsettings.json：

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

appsettings.Development.json：

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

appsettings.Production.json：

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

> [!NOTE]
> [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 扩展方法当前不能分析由 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) 返回的配置部分（例如 `.AddConfiguration(Configuration.GetSection("section"))`）。 `GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:Logging:LogLevel:Default`）。 `AddConfiguration` 方法预期得到配置键（例如 `Logging:LogLevel:Default`）的完全匹配项。 键上存在的节名称阻止节的值配置应用。 将在即将发布的版本中解决此问题。 有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。

## <a name="configureservices"></a>ConfigureServices

[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices) 将服务添加到应用的[依赖关系注入](xref:fundamentals/dependency-injection)容器。 可以利用相加结果多次调用 `ConfigureServices`。

托管服务是一个类，具有实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口的后台任务逻辑。 有关详细信息，请参阅[使用托管服务的后台任务](xref:fundamentals/host/hosted-services)主题。

[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)使用 `AddHostedService` 扩展方法向应用添加生存期事件 `LifetimeEventsHostedService` 和定时后台任务 `TimedHostedService` 服务：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a>ConfigureLogging

[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging) 添加一个委托，用于配置提供的 [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder)。 可以利用相加结果多次调用 `ConfigureLogging`。

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a>UseConsoleLifetime

[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime) 侦听 `Ctrl+C`/SIGINT 或 SIGTERM 并调用 [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) 来启动关闭进程。 `UseConsoleLifetime` 解除阻止 [ RunAsync](#runasync) 和 [WaitForShutdownAsync](#waitforshutdownasync) 等扩展。 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) 预注册为默认生存期实现。 使用注册的最后一个生存期。

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a>容器配置

为支持插入其他容器中，主机可以接受 [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1)。 提供工厂不属于 DI 容器注册，而是用于创建具体 DI 容器的主机内部函数。 [UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory) 重写用于创建应用的服务提供程序的默认工厂。

[ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) 方法托管自定义容器配置。 `ConfigureContainer` 提供在基础主机 API 的基础之上配置容器的强类型体验。 可以利用相加结果多次调用 `ConfigureContainer`。

为应用创建服务容器：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

提供服务容器工厂：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

使用该工厂并为应用配置自定义服务容器：

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a>扩展性

在 `IHostBuilder` 上使用扩展方法实现主机扩展性。 以下示例介绍扩展方法如何使用 [RabbitMQ](https://www.rabbitmq.com/) 扩展 `IHostBuilder` 实现。 该扩展方法（在应用中的其他位置）注册 RabbitMQ `IHostedService`：

```csharp
// UseRabbitMq is an extension method that sets up RabbitMQ to handle incoming
// messages.
var host = new HostBuilder()
    .UseRabbitMq<MyMessageHandler>()
    .Build();

await host.StartAsync();
```

## <a name="manage-the-host"></a>管理主机

[IHost](/dotnet/api/microsoft.extensions.hosting.ihost) 实现负责启动和停止服务容器中注册的 `IHostedService` 实现。

### <a name="run"></a>运行

[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run) 运行应用并阻止调用线程，直到关闭主机：

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        host.Run();
    }
}
```

### <a name="runasync"></a>RunAsync

[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync) 运行应用并返回在触发取消令牌或关闭时完成的 `Task`：

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        await host.RunAsync();
    }
}
```

### <a name="runconsoleasync"></a>RunConsoleAsync

[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync) 启用控制台、生成和启动主机，以及等待 `Ctrl+C`/SIGINT 或 SIGTERM 关闭。

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        await host.RunConsoleAsync();
    }
}
```

### <a name="start-and-stopasync"></a>Start 和 StopAsync

[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start) 同步启动主机。

[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync) 尝试在提供的超时时间内停止主机。

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            await host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

### <a name="startasync-and-stopasync"></a>StartAsync 和 StopAsync

[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 启动应用。

[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) 停止应用。

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.StopAsync();
        }
    }
}
```

### <a name="waitforshutdown"></a>WaitForShutdown

通过 [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime)，如 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)（侦听 `Ctrl+C`/SIGINT 或 SIGTERM）来触发 [WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown)。 `WaitForShutdown` 调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)。

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            host.WaitForShutdown();
        }
    }
}
```

### <a name="waitforshutdownasync"></a>WaitForShutdownAsync

[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync) 返回在通过给定的定牌和调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) 来触发关闭时完成的 `Task`。

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.WaitForShutdownAsync();
        }

    }
}
```

### <a name="external-control"></a>外部控件

使用可从外部调用的方法，能够实现主机的外部控件：

```csharp
public class Program
{
    private IHost _host;

    public Program()
    {
        _host = new HostBuilder()
            .Build();
    }

    public async Task StartAsync()
    {
        _host.StartAsync();
    }

    public async Task StopAsync()
    {
        using (_host)
        {
            await _host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

在 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 开始时调用 [IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync)，在继续之前，会一直等待该操作完成。 它可用于延迟启动，直到外部事件发出信号。

## <a name="ihostingenvironment-interface"></a>IHostingEnvironment 接口

[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) 提供有关应用托管环境的信息。 使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：

```csharp
public class MyClass
{
    private readonly IHostingEnvironment _env;

    public MyClass(IHostingEnvironment env)
    {
        _env = env;
    }

    public void DoSomething()
    {
        var environmentName = _env.EnvironmentName;
    }
}
```

有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。

## <a name="iapplicationlifetime-interface"></a>IApplicationLifetime 接口

[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime) 允许启动后和关闭活动，包括正常关闭请求。 接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。

| 取消标记 | 触发条件 |
| ------------------ | --------------------- |
| [ApplicationStarted](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | 主机已完全启动。 |
| [ApplicationStopped](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | 主机正在完成正常关闭。 应处理所有请求。 关闭受到阻止，直到完成此事件。 |
| [ApplicationStopping](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | 主机正在执行正常关闭。 仍在处理请求。 关闭受到阻止，直到完成此事件。 |

构造函数将 `IApplicationLifetime` 服务注入到任何类中。 [示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)将构造函数注入到 `LifetimeEventsHostedService` 类（一个 `IHostedService` 实现）中，用于注册事件。

LifetimeEventsHostedService.cs：

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) 请求应用终止。 以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：

```csharp
public class MyClass
{
    private readonly IApplicationLifetime _appLifetime;

    public MyClass(IApplicationLifetime appLifetime)
    {
        _appLifetime = appLifetime;
    }

    public void Shutdown()
    {
        _appLifetime.StopApplication();
    }
}
```

## <a name="additional-resources"></a>其他资源

* [使用托管服务的后台任务](xref:fundamentals/host/hosted-services)
* [GitHub 上托管的存储库示例](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
