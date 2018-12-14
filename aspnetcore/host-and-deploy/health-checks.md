---
title: ASP.NET Core 中的运行状况检查
author: guardrex
description: 了解如何为 ASP.NET Core 基础结构（如应用和数据库）设置运行状况检查。
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 12/03/2018
uid: host-and-deploy/health-checks
ms.openlocfilehash: d8fd43d9d689396cf30ca371763cdf7ac9423c77
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862575"
---
# <a name="health-checks-in-aspnet-core"></a><span data-ttu-id="3692f-103">ASP.NET Core 中的运行状况检查</span><span class="sxs-lookup"><span data-stu-id="3692f-103">Health checks in ASP.NET Core</span></span>

<span data-ttu-id="3692f-104">通过 [Luke Latham](https://github.com/guardrex) 和 [Glenn Condron](https://github.com/glennc)</span><span class="sxs-lookup"><span data-stu-id="3692f-104">By [Luke Latham](https://github.com/guardrex) and [Glenn Condron](https://github.com/glennc)</span></span>

<span data-ttu-id="3692f-105">ASP.NET Core 提供运行状况检查中间件和库，以用于报告应用基础结构组件的运行状况。</span><span class="sxs-lookup"><span data-stu-id="3692f-105">ASP.NET Core offers Health Check Middleware and libraries for reporting the health of app infrastructure components.</span></span>

<span data-ttu-id="3692f-106">运行状况检查由应用程序作为 HTTP 终结点公开。</span><span class="sxs-lookup"><span data-stu-id="3692f-106">Health checks are exposed by an app as HTTP endpoints.</span></span> <span data-ttu-id="3692f-107">可以为各种实时监视方案配置运行状况检查终结点：</span><span class="sxs-lookup"><span data-stu-id="3692f-107">Health check endpoints can be configured for a variety of real-time monitoring scenarios:</span></span>

* <span data-ttu-id="3692f-108">运行状况探测可以由容器业务流程协调程和负载均衡器用于检查应用的状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-108">Health probes can be used by container orchestrators and load balancers to check an app's status.</span></span> <span data-ttu-id="3692f-109">例如，容器业务流程协调程序可以通过停止滚动部署或重新启动容器来响应失败的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-109">For example, a container orchestrator may respond to a failing health check by halting a rolling deployment or restarting a container.</span></span> <span data-ttu-id="3692f-110">负载均衡器可以通过将流量从失败的实例路由到正常实例，来应对不正常的应用。</span><span class="sxs-lookup"><span data-stu-id="3692f-110">A load balancer might react to an unhealthy app by routing traffic away from the failing instance to a healthy instance.</span></span>
* <span data-ttu-id="3692f-111">可以监视内存、磁盘和其他物理服务器资源的使用情况来了解是否处于正常状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-111">Use of memory, disk, and other physical server resources can be monitored for healthy status.</span></span>
* <span data-ttu-id="3692f-112">运行状况检查可以测试应用的依赖项（如数据库和外部服务终结点）以确认是否可用和正常工作。</span><span class="sxs-lookup"><span data-stu-id="3692f-112">Health checks can test an app's dependencies, such as databases and external service endpoints, to confirm availability and normal functioning.</span></span>

<span data-ttu-id="3692f-113">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="3692f-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3692f-114">示例应用包含本主题中所述的方案示例。</span><span class="sxs-lookup"><span data-stu-id="3692f-114">The sample app includes examples of the scenarios described in this topic.</span></span> <span data-ttu-id="3692f-115">若要运行给定方案的示例应用，请在命令行界面中从项目文件夹中使用 [dotnet run](/dotnet/core/tools/dotnet-run) 命令。</span><span class="sxs-lookup"><span data-stu-id="3692f-115">To run the sample app for a given scenario, use the [dotnet run](/dotnet/core/tools/dotnet-run) command from the project's folder in a command shell.</span></span> <span data-ttu-id="3692f-116">请参阅示例应用的 README.md 文件和本主题中的方案说明，以了解有关如何使用示例应用的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3692f-116">See the sample app's *README.md* file and the scenario descriptions in this topic for details on how to use the sample app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3692f-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="3692f-117">Prerequisites</span></span>

<span data-ttu-id="3692f-118">运行状况检查通常与外部监视服务或容器业务流程协调程序一起用于检查应用的状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-118">Health checks are usually used with an external monitoring service or container orchestrator to check the status of an app.</span></span> <span data-ttu-id="3692f-119">向应用添加运行状况检查之前，需确定要使用的监视系统。</span><span class="sxs-lookup"><span data-stu-id="3692f-119">Before adding health checks to an app, decide on which monitoring system to use.</span></span> <span data-ttu-id="3692f-120">监视系统决定了要创建的运行状况检查类型以及配置其终结点的方式。</span><span class="sxs-lookup"><span data-stu-id="3692f-120">The monitoring system dictates what types of health checks to create and how to configure their endpoints.</span></span>

<span data-ttu-id="3692f-121">引用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)或将包引用添加到 [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) 包。</span><span class="sxs-lookup"><span data-stu-id="3692f-121">Reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) package.</span></span>

<span data-ttu-id="3692f-122">示例应用提供了启动代码来演示几个方案的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-122">The sample app provides start-up code to demonstrate health checks for several scenarios.</span></span> <span data-ttu-id="3692f-123">[数据库探测](#database-probe)方案使用 [BeatPulse](https://github.com/Xabaril/BeatPulse) 探测数据库连接的运行状况。</span><span class="sxs-lookup"><span data-stu-id="3692f-123">The [database probe](#database-probe) scenario probes the health of a database connection using [BeatPulse](https://github.com/Xabaril/BeatPulse).</span></span> <span data-ttu-id="3692f-124">[DbContext 探测](#entity-framework-core-dbcontext-probe)方案使用 EF Core `DbContext` 探测数据库。</span><span class="sxs-lookup"><span data-stu-id="3692f-124">The [DbContext probe](#entity-framework-core-dbcontext-probe) scenario probes a database using an EF Core `DbContext`.</span></span> <span data-ttu-id="3692f-125">使用示例应用探索数据库方案：</span><span class="sxs-lookup"><span data-stu-id="3692f-125">To explore the database scenarios using the sample app:</span></span>

* <span data-ttu-id="3692f-126">创建一个数据库，并在应用的 appsettings.json 文件中提供其连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3692f-126">Create a database and provide its connection string in the *appsettings.json* file of the app.</span></span>
* <span data-ttu-id="3692f-127">添加对 [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/) 的包引用。</span><span class="sxs-lookup"><span data-stu-id="3692f-127">Add a package reference to [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/).</span></span>

> [!NOTE]
> <span data-ttu-id="3692f-128">[BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。</span><span class="sxs-lookup"><span data-stu-id="3692f-128">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

<span data-ttu-id="3692f-129">另一个运行状况检查方案演示如何将运行状况检查筛选到某个管理端口。</span><span class="sxs-lookup"><span data-stu-id="3692f-129">Another health check scenario demonstrates how to filter health checks to a management port.</span></span> <span data-ttu-id="3692f-130">示例应用要求创建包含管理 URL 和管理端口的 Properties/launchSettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="3692f-130">The sample app requires you to create a *Properties/launchSettings.json* file that includes the management URL and management port.</span></span> <span data-ttu-id="3692f-131">有关详细信息，请参阅[按端口筛选](#filter-by-port)部分。</span><span class="sxs-lookup"><span data-stu-id="3692f-131">For more information, see the [Filter by port](#filter-by-port) section.</span></span>

## <a name="basic-health-probe"></a><span data-ttu-id="3692f-132">基本运行状况探测</span><span class="sxs-lookup"><span data-stu-id="3692f-132">Basic health probe</span></span>

<span data-ttu-id="3692f-133">对于许多应用，报告应用在处理请求方面的可用性（运行情况）的基本运行状况探测配置足以发现应用的状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-133">For many apps, a basic health probe configuration that reports the app's availability to process requests (*liveness*) is sufficient to discover the status of the app.</span></span>

<span data-ttu-id="3692f-134">基本配置会注册运行状况检查服务，并调用运行状况检查中间件以使用运行状况响应在 URL 终结点处进行响应。</span><span class="sxs-lookup"><span data-stu-id="3692f-134">The basic configuration registers health check services and calls the Health Check Middleware to respond at a URL endpoint with a health response.</span></span> <span data-ttu-id="3692f-135">默认情况下，不会注册任何特定运行状况检查来测试任何特定依赖项或子系统。</span><span class="sxs-lookup"><span data-stu-id="3692f-135">By default, no specific health checks are registered to test any particular dependency or subsystem.</span></span> <span data-ttu-id="3692f-136">如果能够在运行状况终结点 URL 处进行响应，则应用被视为正常。</span><span class="sxs-lookup"><span data-stu-id="3692f-136">The app is considered healthy if it's capable of responding at the health endpoint URL.</span></span> <span data-ttu-id="3692f-137">默认响应编写器会以纯文本响应形式将状态 (`HealthCheckStatus`) 写回到客户端，以便指示 `HealthCheckResult.Healthy` 或 `HealthCheckResult.Unhealthy` 状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-137">The default response writer writes the status (`HealthCheckStatus`) as a plaintext response back to the client, indicating either a `HealthCheckResult.Healthy` or `HealthCheckResult.Unhealthy` status.</span></span>

<span data-ttu-id="3692f-138">在 `Startup.ConfigureServices` 中使用 `AddHealthChecks` 注册运行状况检查服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-138">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="3692f-139">在 `Startup.Configure` 的请求处理管道中使用 `UseHealthChecks` 注册运行状况检查中间件。</span><span class="sxs-lookup"><span data-stu-id="3692f-139">Add Health Check Middleware with `UseHealthChecks` in the request processing pipeline of `Startup.Configure`.</span></span>

<span data-ttu-id="3692f-140">在示例应用中，在 `/health` 处创建运行状况检查终结点 (BasicStartup.cs)：</span><span class="sxs-lookup"><span data-stu-id="3692f-140">In the sample app, the health check endpoint is created at `/health` (*BasicStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/BasicStartup.cs?name=snippet1&highlight=5,10)]

<span data-ttu-id="3692f-141">若要使用示例应用运行基本配置方案，请在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-141">To run the basic configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario basic
```

### <a name="docker-example"></a><span data-ttu-id="3692f-142">Docker 示例</span><span class="sxs-lookup"><span data-stu-id="3692f-142">Docker example</span></span>

<span data-ttu-id="3692f-143">[Docker](xref:host-and-deploy/docker/index) 提供内置 `HEALTHCHECK` 指令，该指令可以用于检查使用基本运行状况检查配置的应用的状态：</span><span class="sxs-lookup"><span data-stu-id="3692f-143">[Docker](xref:host-and-deploy/docker/index) offers a built-in `HEALTHCHECK` directive that can be used to check the status of an app that uses the basic health check configuration:</span></span>

```
HEALTHCHECK CMD curl --fail http://localhost:5000/health || exit
```

## <a name="create-health-checks"></a><span data-ttu-id="3692f-144">创建运行状况检查</span><span class="sxs-lookup"><span data-stu-id="3692f-144">Create health checks</span></span>

<span data-ttu-id="3692f-145">运行状况检查通过实现 `IHealthCheck` 接口进行创建。</span><span class="sxs-lookup"><span data-stu-id="3692f-145">Health checks are created by implementing the `IHealthCheck` interface.</span></span> <span data-ttu-id="3692f-146">`IHealthCheck.CheckHealthAsync` 方法会返回 `Task<HealthCheckResult>`，它以 `Healthy`、`Degraded` 或 `Unhealthy` 的形式指示运行状况。</span><span class="sxs-lookup"><span data-stu-id="3692f-146">The `IHealthCheck.CheckHealthAsync` method returns a `Task<HealthCheckResult>` that indicates the health as `Healthy`, `Degraded`, or `Unhealthy`.</span></span> <span data-ttu-id="3692f-147">结果会使用可配置状态代码（配置在[运行状况检查选项](#health-check-options)部分中进行介绍）编写为纯文本响应。</span><span class="sxs-lookup"><span data-stu-id="3692f-147">The result is written as a plaintext response with a configurable status code (configuration is described in the [Health check options](#health-check-options) section).</span></span> <span data-ttu-id="3692f-148">`HealthCheckResult` 还可以返回可选的键值对。</span><span class="sxs-lookup"><span data-stu-id="3692f-148">`HealthCheckResult` can also return optional key-value pairs.</span></span>

### <a name="example-health-check"></a><span data-ttu-id="3692f-149">示例运行状况检查</span><span class="sxs-lookup"><span data-stu-id="3692f-149">Example health check</span></span>

<span data-ttu-id="3692f-150">下面的 `ExampleHealthCheck` 类演示运行状况检查的布局：</span><span class="sxs-lookup"><span data-stu-id="3692f-150">The following `ExampleHealthCheck` class demonstrates the layout of a health check:</span></span>

```csharp
public class ExampleHealthCheck : IHealthCheck
{
    public ExampleHealthCheck()
    {
        // Use dependency injection (DI) to supply any required services to the
        // health check.
    }

    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context, 
        CancellationToken cancellationToken = default(CancellationToken))
    {
        // Execute health check logic here. This example sets a dummy
        // variable to true.
        var healthCheckResultHealthy = true;

        if (healthCheckResultHealthy)
        {
            return Task.FromResult(
                HealthCheckResult.Healthy("The check indicates a healthy result."));
        }

        return Task.FromResult(
            HealthCheckResult.Unhealthy("The check indicates an unhealthy result."));
    }
}
```

### <a name="register-health-check-services"></a><span data-ttu-id="3692f-151">注册运行状况检查服务</span><span class="sxs-lookup"><span data-stu-id="3692f-151">Register health check services</span></span>

<span data-ttu-id="3692f-152">`ExampleHealthCheck` 类型使用 `AddCheck` 添加到运行状况检查服务：</span><span class="sxs-lookup"><span data-stu-id="3692f-152">The `ExampleHealthCheck` type is added to health check services with `AddCheck`:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck<ExampleHealthCheck>("example_health_check");
}
```

<span data-ttu-id="3692f-153">以下示例中显示的 `AddCheck` 重载会设置要在运行状况检查报告失败时报告的失败状态 (`HealthStatus`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-153">The `AddCheck` overload shown in the following example sets the failure status (`HealthStatus`) to report when the health check reports a failure.</span></span> <span data-ttu-id="3692f-154">如果失败状态设置为 `null`（默认值），则会报告 `HealthStatus.Unhealthy`。</span><span class="sxs-lookup"><span data-stu-id="3692f-154">If the failure status is set to `null` (default), `HealthStatus.Unhealthy` is reported.</span></span> <span data-ttu-id="3692f-155">此重载对于库创建者是一种十分有用的方案，在这种情况下，如果运行状况检查实现遵循该设置，则在发生运行状况检查失败时，应用会强制实施库所指示的失败状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-155">This overload is a useful scenario for library authors, where the failure status indicated by the library is enforced by the app when a health check failure occurs if the health check implementation honors the setting.</span></span>

<span data-ttu-id="3692f-156">标记用于筛选运行状况检查（在[筛选运行状况检查](#filter-health-checks)部分中进行了进一步介绍）。</span><span class="sxs-lookup"><span data-stu-id="3692f-156">*Tags* can be used to filter health checks (described further in the [Filter health checks](#filter-health-checks) section).</span></span>

```csharp
services.AddHealthChecks()
    .AddCheck<ExampleHealthCheck>(
        "example_health_check", 
        failureStatus: HealthStatus.Degraded, 
        tags: new[] { "example" });
```

<span data-ttu-id="3692f-157">`AddCheck` 还可以执行 lambda 函数。</span><span class="sxs-lookup"><span data-stu-id="3692f-157">`AddCheck` can also execute a lambda function.</span></span> <span data-ttu-id="3692f-158">在以下示例中，运行状况检查名称指定为 `Example`，并且检查始终返回正常状态：</span><span class="sxs-lookup"><span data-stu-id="3692f-158">In the following example, the health check name is specified as `Example` and the check always returns a healthy state:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Example", () => 
            HealthCheckResult.Healthy("Example is OK!"), tags: new[] { "example" })
}
```

### <a name="use-health-checks-middleware"></a><span data-ttu-id="3692f-159">使用运行状况检查中间件</span><span class="sxs-lookup"><span data-stu-id="3692f-159">Use Health Checks Middleware</span></span>

<span data-ttu-id="3692f-160">在 `Startup.Configure` 内，在处理管道中使用终结点 URL 或相对路径调用 `UseHealthChecks`：</span><span class="sxs-lookup"><span data-stu-id="3692f-160">In `Startup.Configure`, call `UseHealthChecks` in the processing pipeline with the endpoint URL or relative path:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health");
}
```

<span data-ttu-id="3692f-161">如果运行状况检查应侦听特定端口，则使用 `UseHealthChecks` 的重载设置端口（在[按端口筛选](#filter-by-port)部分中进行了进一步介绍）：</span><span class="sxs-lookup"><span data-stu-id="3692f-161">If the health checks should listen on a specific port, use an overload of `UseHealthChecks` to set the port (described further in the [Filter by port](#filter-by-port) section):</span></span>

```csharp
app.UseHealthChecks("/health", port: 8000);
```

<span data-ttu-id="3692f-162">运行状况检查中间件是应用请求处理管道中的*终端中间件*。</span><span class="sxs-lookup"><span data-stu-id="3692f-162">Health Checks Middleware is a *terminal middleware* in the app's request processing pipeline.</span></span> <span data-ttu-id="3692f-163">遇到的与请求 URL 完全匹配的第一个运行状况检查终结点会进行执行，并且使中间件管道的其余部分短路。</span><span class="sxs-lookup"><span data-stu-id="3692f-163">The first health check endpoint encountered that's an exact match to the request URL executes and short-circuits the rest of the middleware pipeline.</span></span> <span data-ttu-id="3692f-164">当短路发生时，不会执行匹配运行状况检查后面的任何中间件。</span><span class="sxs-lookup"><span data-stu-id="3692f-164">When short-circuiting occurs, no middleware following the matched health check executes.</span></span>

## <a name="health-check-options"></a><span data-ttu-id="3692f-165">运行状况检查选项</span><span class="sxs-lookup"><span data-stu-id="3692f-165">Health check options</span></span>

<span data-ttu-id="3692f-166">`HealthCheckOptions` 使你可以自定义运行状况检查行为：</span><span class="sxs-lookup"><span data-stu-id="3692f-166">`HealthCheckOptions` provide an opportunity to customize health check behavior:</span></span>

* [<span data-ttu-id="3692f-167">筛选运行状况检查</span><span class="sxs-lookup"><span data-stu-id="3692f-167">Filter health checks</span></span>](#filter-health-checks)
* [<span data-ttu-id="3692f-168">自定义 HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="3692f-168">Customize the HTTP status code</span></span>](#customize-the-http-status-code)
* [<span data-ttu-id="3692f-169">取消缓存标头</span><span class="sxs-lookup"><span data-stu-id="3692f-169">Suppress cache headers</span></span>](#suppress-cache-headers)
* [<span data-ttu-id="3692f-170">自定义输出</span><span class="sxs-lookup"><span data-stu-id="3692f-170">Customize output</span></span>](#customize-output)

### <a name="filter-health-checks"></a><span data-ttu-id="3692f-171">筛选运行状况检查</span><span class="sxs-lookup"><span data-stu-id="3692f-171">Filter health checks</span></span>

<span data-ttu-id="3692f-172">默认情况下，运行状况检查中间件会运行所有已注册的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-172">By default, Health Check Middleware runs all registered health checks.</span></span> <span data-ttu-id="3692f-173">若要运行运行状况检查的子集，请提供向 `Predicate` 选项返回布尔值的函数。</span><span class="sxs-lookup"><span data-stu-id="3692f-173">To run a subset of health checks, provide a function that returns a boolean to the `Predicate` option.</span></span> <span data-ttu-id="3692f-174">在以下示例中，`Bar` 运行状况检查在函数条件语句 中由于其标记 (`bar_tag`) 而被筛选掉，在条件语句中，仅当运行状况检查的 `Tag` 属性与 `foo_tag` 或 `baz_tag` 匹配时才返回 `true`：</span><span class="sxs-lookup"><span data-stu-id="3692f-174">In the following example, the `Bar` health check is filtered out by its tag (`bar_tag`) in the function's conditional statement, where `true` is only returned if the health check's `Tag` property matches `foo_tag` or `baz_tag`:</span></span>

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Foo", () => 
            HealthCheckResult.Healthy("Foo is OK!"), tags: new[] { "foo_tag" })
        .AddCheck("Bar", () => 
            HealthCheckResult.Unhealthy("Bar is unhealthy!"), tags: new[] { "bar_tag" })
        .AddCheck("Baz", () => 
            HealthCheckResult.Healthy("Baz is OK!"), tags: new[] { "baz_tag" });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // Filter out the 'Bar' health check. Only Foo and Baz execute.
        Predicate = (check) => check.Tags.Contains("foo_tag") || 
            check.Tags.Contains("baz_tag")
    });
}
```

### <a name="customize-the-http-status-code"></a><span data-ttu-id="3692f-175">自定义 HTTP 状态代码</span><span class="sxs-lookup"><span data-stu-id="3692f-175">Customize the HTTP status code</span></span>

<span data-ttu-id="3692f-176">使用 `ResultStatusCodes` 可自定义运行状况状态到 HTTP 状态代码的映射。</span><span class="sxs-lookup"><span data-stu-id="3692f-176">Use `ResultStatusCodes` to customize the mapping of health status to HTTP status codes.</span></span> <span data-ttu-id="3692f-177">以下 `StatusCode` 分配是中间件所使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="3692f-177">The following `StatusCode` assignments are the default values used by the middleware.</span></span> <span data-ttu-id="3692f-178">更改状态代码值以满足要求。</span><span class="sxs-lookup"><span data-stu-id="3692f-178">Change the status code values to meet your requirements.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The following StatusCodes are the default assignments for
        // the HealthCheckStatus properties.
        ResultStatusCodes =
        {
            [HealthCheckStatus.Healthy] = StatusCodes.Status200OK,
            [HealthCheckStatus.Degraded] = StatusCodes.Status200OK,
            [HealthCheckStatus.Unhealthy] = StatusCodes.Status503ServiceUnavailable
        }
    });
}
```

### <a name="suppress-cache-headers"></a><span data-ttu-id="3692f-179">取消缓存标头</span><span class="sxs-lookup"><span data-stu-id="3692f-179">Suppress cache headers</span></span>

<span data-ttu-id="3692f-180">`AllowCachingResponses` 控制运行状况检查中间件是否将 HTTP 标头添加到探测响应以防止响应缓存。</span><span class="sxs-lookup"><span data-stu-id="3692f-180">`AllowCachingResponses` controls whether the Health Check Middleware adds HTTP headers to a probe response to prevent response caching.</span></span> <span data-ttu-id="3692f-181">如果值为 `false`（默认值），则中间件会设置或替代 `Cache-Control`、`Expires` 和 `Pragma` 标头以防止响应缓存。</span><span class="sxs-lookup"><span data-stu-id="3692f-181">If the value is `false` (default), the middleware sets or overrides the `Cache-Control`, `Expires`, and `Pragma` headers to prevent response caching.</span></span> <span data-ttu-id="3692f-182">如果值为 `true`，则中间件不会修改响应的缓存标头。</span><span class="sxs-lookup"><span data-stu-id="3692f-182">If the value is `true`, the middleware doesn't modify the cache headers of the response.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The default value is false.
        AllowCachingResponses = false
    });
}
```

### <a name="customize-output"></a><span data-ttu-id="3692f-183">自定义输出</span><span class="sxs-lookup"><span data-stu-id="3692f-183">Customize output</span></span>

<span data-ttu-id="3692f-184">`ResponseWriter` 选项可获取或设置用于编写响应的委托。</span><span class="sxs-lookup"><span data-stu-id="3692f-184">The `ResponseWriter` option gets or sets a delegate used to write the response.</span></span> <span data-ttu-id="3692f-185">默认委托会使用 `HealthReport.Status` 字符串值编写最小的纯文本响应。</span><span class="sxs-lookup"><span data-stu-id="3692f-185">The default delegate writes a minimal plaintext response with the string value of `HealthReport.Status`.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // WriteResponse is a delegate used to write the response.
        ResponseWriter = WriteResponse
    });
}

private static Task WriteResponse(HttpContext httpContext, 
    HealthReport result)
{
    httpContext.Response.ContentType = "application/json";

    var json = new JObject(
        new JProperty("status", result.Status.ToString()),
        new JProperty("results", new JObject(result.Entries.Select(pair =>
            new JProperty(pair.Key, new JObject(
                new JProperty("status", pair.Value.Status.ToString()),
                new JProperty("description", pair.Value.Description),
                new JProperty("data", new JObject(pair.Value.Data.Select(
                    p => new JProperty(p.Key, p.Value))))))))));
    return httpContext.Response.WriteAsync(
        json.ToString(Formatting.Indented));
}
```

## <a name="database-probe"></a><span data-ttu-id="3692f-186">数据库探测</span><span class="sxs-lookup"><span data-stu-id="3692f-186">Database probe</span></span>

<span data-ttu-id="3692f-187">运行状况检查可以指定数据库查询作为布尔测试来运行，以指示数据库是否在正常响应。</span><span class="sxs-lookup"><span data-stu-id="3692f-187">A health check can specify a database query to run as a boolean test to indicate if the database is responding normally.</span></span>

<span data-ttu-id="3692f-188">示例应用使用 [BeatPulse](https://github.com/Xabaril/BeatPulse)（适用于 ASP.NET Core 应用的运行状况检查库）对 SQL Server 数据库执行运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-188">The sample app uses [BeatPulse](https://github.com/Xabaril/BeatPulse), a health check library for ASP.NET Core apps, to perform a health check on a SQL Server database.</span></span> <span data-ttu-id="3692f-189">BeatPulse 会对数据库执行 `SELECT 1` 查询以确认数据库连接是否处于正常状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-189">BeatPulse executes a `SELECT 1` query against the database to confirm the connection to the database is healthy.</span></span>

> [!WARNING]
> <span data-ttu-id="3692f-190">使用查询检查数据库连接时，请选择快速返回的查询。</span><span class="sxs-lookup"><span data-stu-id="3692f-190">When checking a database connection with a query, choose a query that returns quickly.</span></span> <span data-ttu-id="3692f-191">查询方法会面临使数据库过载和降低其性能的风险。</span><span class="sxs-lookup"><span data-stu-id="3692f-191">The query approach runs the risk of overloading the database and degrading its performance.</span></span> <span data-ttu-id="3692f-192">在大多数情况下，无需运行测试查询。</span><span class="sxs-lookup"><span data-stu-id="3692f-192">In most cases, running a test query isn't necessary.</span></span> <span data-ttu-id="3692f-193">只需建立成功的数据库连接便足矣。</span><span class="sxs-lookup"><span data-stu-id="3692f-193">Merely making a successful connection to the database is sufficient.</span></span> <span data-ttu-id="3692f-194">如果发现需要运行查询，请选择简单的 SELECT 查询，如 `SELECT 1`。</span><span class="sxs-lookup"><span data-stu-id="3692f-194">If you find it necessary to run a query, choose a simple SELECT query, such as `SELECT 1`.</span></span>

<span data-ttu-id="3692f-195">若要使用 BeatPulse 库，请包含对 [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/) 的包引用。</span><span class="sxs-lookup"><span data-stu-id="3692f-195">In order to use the BeatPulse library, include a package reference to [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/).</span></span>

<span data-ttu-id="3692f-196">在应用的 appsettings.json 文件中提供有效数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3692f-196">Supply a valid database connection string in the *appsettings.json* file of the sample app.</span></span> <span data-ttu-id="3692f-197">应用使用名为 `HealthCheckSample` 的 SQL Server 数据库：</span><span class="sxs-lookup"><span data-stu-id="3692f-197">The app uses a SQL Server database named `HealthCheckSample`:</span></span>

[!code-json[](health-checks/samples/2.x/HealthChecksSample/appsettings.json?highlight=3)]

<span data-ttu-id="3692f-198">在 `Startup.ConfigureServices` 中使用 `AddHealthChecks` 注册运行状况检查服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-198">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="3692f-199">示例应用使用数据库连接字符串 (DbHealthStartup.cs) 调用 BeatPulse 的 `AddSqlServer` 方法：</span><span class="sxs-lookup"><span data-stu-id="3692f-199">The sample app calls BeatPulse's `AddSqlServer` method with the database's connection string (*DbHealthStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="3692f-200">在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件：</span><span class="sxs-lookup"><span data-stu-id="3692f-200">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_Configure)]

<span data-ttu-id="3692f-201">若要使用示例应用运行数据库探测方案，请在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-201">To run the database probe scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario db
```

> [!NOTE]
> <span data-ttu-id="3692f-202">[BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。</span><span class="sxs-lookup"><span data-stu-id="3692f-202">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

## <a name="entity-framework-core-dbcontext-probe"></a><span data-ttu-id="3692f-203">Entity Framework Core DbContext 探测</span><span class="sxs-lookup"><span data-stu-id="3692f-203">Entity Framework Core DbContext probe</span></span>

<span data-ttu-id="3692f-204">在使用 [Entity Framework (EF) Core](/ef/core/) 的应用支持 `DbContext` 检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-204">The `DbContext` check is supported in apps that use [Entity Framework (EF) Core](/ef/core/).</span></span> <span data-ttu-id="3692f-205">此检查确认应用可以与为 EF Core `DbContext` 配置的数据库通信。</span><span class="sxs-lookup"><span data-stu-id="3692f-205">This check confirms that the app can communicate with the database configured for an EF Core `DbContext`.</span></span> <span data-ttu-id="3692f-206">默认情况下，`DbContextHealthCheck` 调用 EF Core 的 `CanConnectAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="3692f-206">By default, the `DbContextHealthCheck` calls EF Core's `CanConnectAsync` method.</span></span> <span data-ttu-id="3692f-207">可以自定义在使用 `AddDbContextCheck` 方法的重载检查运行状况时运行的操作。</span><span class="sxs-lookup"><span data-stu-id="3692f-207">You can customize what operation is run when checking health using overloads of the `AddDbContextCheck` method.</span></span>

<span data-ttu-id="3692f-208">`AddDbContextCheck<TContext>` 为 `DbContext` 注册运行状况检查 (`TContext`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-208">`AddDbContextCheck<TContext>` registers a health check for a `DbContext` (`TContext`).</span></span> <span data-ttu-id="3692f-209">默认情况下，运行状况检查的名称是 `TContext` 类型的名称。</span><span class="sxs-lookup"><span data-stu-id="3692f-209">By default, the name of the health check is the name of the `TContext` type.</span></span> <span data-ttu-id="3692f-210">重载可用于配置失败状态、标记和自定义测试查询。</span><span class="sxs-lookup"><span data-stu-id="3692f-210">An overload is available to configure the failure status, tags, and a custom test query.</span></span>

<span data-ttu-id="3692f-211">在示例应用中，`AppDbContext` 会提供给 `AddDbContextCheck`，并在 `Startup.ConfigureServices` 中注册为服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-211">In the sample app, `AppDbContext` is provided to `AddDbContextCheck` and registered as a service in `Startup.ConfigureServices`.</span></span>

<span data-ttu-id="3692f-212">*DbContextHealthStartup.cs*：</span><span class="sxs-lookup"><span data-stu-id="3692f-212">*DbContextHealthStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="3692f-213">在示例应用中，`UseHealthChecks` 在 `Startup.Configure` 中添加运行状况检查中间件。</span><span class="sxs-lookup"><span data-stu-id="3692f-213">In the sample app, `UseHealthChecks` adds the Health Check Middleware in `Startup.Configure`.</span></span>

<span data-ttu-id="3692f-214">*DbContextHealthStartup.cs*：</span><span class="sxs-lookup"><span data-stu-id="3692f-214">*DbContextHealthStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_Configure)]

<span data-ttu-id="3692f-215">若要使用示例应用运行 `DbContext` 探测方案，请确认连接字符串指定的数据库在 SQL Server 实例中不存在。</span><span class="sxs-lookup"><span data-stu-id="3692f-215">To run the `DbContext` probe scenario using the sample app, confirm that the database specified by the the connection string doesn't exist in the SQL Server instance.</span></span> <span data-ttu-id="3692f-216">如果该数据库存在，请删除它。</span><span class="sxs-lookup"><span data-stu-id="3692f-216">If the database exists, delete it.</span></span>

<span data-ttu-id="3692f-217">在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-217">Execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario dbcontext
```

<span data-ttu-id="3692f-218">在应用运行之后，在浏览器中对 `/health` 终结点发出请求，从而检查运行状况。</span><span class="sxs-lookup"><span data-stu-id="3692f-218">After the app is running, check the health status by making a request to the `/health` endpoint in a browser.</span></span> <span data-ttu-id="3692f-219">数据库和 `AppDbContext` 不存在，因此应用提供以下响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-219">The database and `AppDbContext` don't exist, so app provides the following response:</span></span>

```
Unhealthy
```

<span data-ttu-id="3692f-220">触发示例应用以创建数据库。</span><span class="sxs-lookup"><span data-stu-id="3692f-220">Trigger the sample app to create the database.</span></span> <span data-ttu-id="3692f-221">向 `/createdatabase` 发出请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-221">Make a request to `/createdatabase`.</span></span> <span data-ttu-id="3692f-222">应用会进行以下响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-222">The app responds:</span></span>

```
Creating the database...
Done!
Navigate to /health to see the health status.
```

<span data-ttu-id="3692f-223">向 `/health` 终结点发出请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-223">Make a request to the `/health` endpoint.</span></span> <span data-ttu-id="3692f-224">数据库和上下文存在，因此应用会进行以下响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-224">The database and context exist, so app responds:</span></span>

```
Healthy
```

<span data-ttu-id="3692f-225">触发示例应用以删除数据库。</span><span class="sxs-lookup"><span data-stu-id="3692f-225">Trigger the sample app to delete the database.</span></span> <span data-ttu-id="3692f-226">向 `/deletedatabase` 发出请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-226">Make a request to `/deletedatabase`.</span></span> <span data-ttu-id="3692f-227">应用会进行以下响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-227">The app responds:</span></span>

```
Deleting the database...
Done!
Navigate to /health to see the health status.
```

<span data-ttu-id="3692f-228">向 `/health` 终结点发出请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-228">Make a request to the `/health` endpoint.</span></span> <span data-ttu-id="3692f-229">应用提供不正常的响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-229">The app provides an unhealthy response:</span></span>

```
Unhealthy
```

## <a name="separate-readiness-and-liveness-probes"></a><span data-ttu-id="3692f-230">单独的就绪情况和运行情况探测</span><span class="sxs-lookup"><span data-stu-id="3692f-230">Separate readiness and liveness probes</span></span>

<span data-ttu-id="3692f-231">在某些托管方案中，会使用一对区分两种应用状态的运行状况检查：</span><span class="sxs-lookup"><span data-stu-id="3692f-231">In some hosting scenarios, a pair of health checks are used that distinguish two app states:</span></span>

* <span data-ttu-id="3692f-232">应用正常运行，但尚未准备好接收请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-232">The app is functioning but not yet ready to receive requests.</span></span> <span data-ttu-id="3692f-233">此状态是应用的就绪情况。</span><span class="sxs-lookup"><span data-stu-id="3692f-233">This state is the app's *readiness*.</span></span>
* <span data-ttu-id="3692f-234">应用正常运行并响应请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-234">The app is functioning and responding to requests.</span></span> <span data-ttu-id="3692f-235">此状态是应用的运行情况。</span><span class="sxs-lookup"><span data-stu-id="3692f-235">This state is the app's *liveness*.</span></span>

<span data-ttu-id="3692f-236">就绪情况检查通常执行更广泛和耗时的检查集，以确定应用的所有子系统和资源是否都可用。</span><span class="sxs-lookup"><span data-stu-id="3692f-236">The readiness check usually performs a more extensive and time-consuming set of checks to determine if all of the app's subsystems and resources are available.</span></span> <span data-ttu-id="3692f-237">运行情况检查只是执行一个快速检查，以确定应用是否可用于处理请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-237">A liveness check merely performs a quick check to determine if the app is available to process requests.</span></span> <span data-ttu-id="3692f-238">应用通过其就绪情况检查之后，无需使用成本高昂的就绪情况检查集来进一步增加应用负荷 &mdash; 后续检查只需检查运行情况。</span><span class="sxs-lookup"><span data-stu-id="3692f-238">After the app passes its readiness check, there's no need to burden the app further with the expensive set of readiness checks&mdash;further checks only require checking for liveness.</span></span>

<span data-ttu-id="3692f-239">示例应用包含运行状况检查，以报告[托管服务](xref:fundamentals/host/hosted-services)中长时间运行的启动任务的完成。</span><span class="sxs-lookup"><span data-stu-id="3692f-239">The sample app contains a health check to report the completion of long-running startup task in a [Hosted Service](xref:fundamentals/host/hosted-services).</span></span> <span data-ttu-id="3692f-240">`StartupHostedServiceHealthCheck` 公开了属性 `StartupTaskCompleted`，托管服务在其长时间运行的任务完成时可以将该属性设置为 `true` (StartupHostedServiceHealthCheck.cs)：</span><span class="sxs-lookup"><span data-stu-id="3692f-240">The `StartupHostedServiceHealthCheck` exposes a property, `StartupTaskCompleted`, that the hosted service can set to `true` when its long-running task is finished (*StartupHostedServiceHealthCheck.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/StartupHostedServiceHealthCheck.cs?name=snippet1&highlight=5)]

<span data-ttu-id="3692f-241">长时间运行的后台任务由[托管服务](xref:fundamentals/host/hosted-services) (Services/StartupHostedService) 启动。</span><span class="sxs-lookup"><span data-stu-id="3692f-241">The long-running background task is started by a [Hosted Service](xref:fundamentals/host/hosted-services) (*Services/StartupHostedService*).</span></span> <span data-ttu-id="3692f-242">在该任务结束时，`StartupHostedServiceHealthCheck.StartupTaskCompleted` 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="3692f-242">At the conclusion of the task, `StartupHostedServiceHealthCheck.StartupTaskCompleted` is set to `true`:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/Services/StartupHostedService.cs?name=snippet1&highlight=18-20)]

<span data-ttu-id="3692f-243">运行状况检查在 `Startup.ConfigureServices` 中使用 `AddCheck` 与托管服务一起注册。</span><span class="sxs-lookup"><span data-stu-id="3692f-243">The health check is registered with `AddCheck` in `Startup.ConfigureServices` along with the hosted service.</span></span> <span data-ttu-id="3692f-244">因为托管服务必须对运行状况检查设置该属性，所以运行状况检查也会在服务容器 (LivenessProbeStartup.cs) 中进行注册：</span><span class="sxs-lookup"><span data-stu-id="3692f-244">Because the hosted service must set the property on the health check, the health check is also registered in the service container (*LivenessProbeStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="3692f-245">在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件。</span><span class="sxs-lookup"><span data-stu-id="3692f-245">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`.</span></span> <span data-ttu-id="3692f-246">在示例应用中，在 `/health/ready` 处为就绪情况检查，并且在 `/health/live` 处为运行情况检查创建运行状况检查终结点。</span><span class="sxs-lookup"><span data-stu-id="3692f-246">In the sample app, the health check endpoints are created at `/health/ready` for the readiness check and `/health/live` for the liveness check.</span></span> <span data-ttu-id="3692f-247">就绪情况检查会将运行状况检查筛选到具有 `ready` 标记的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-247">The readiness check filters health checks to the health check with the `ready` tag.</span></span> <span data-ttu-id="3692f-248">运行情况检查通过在 `HealthCheckOptions.Predicate` 中返回 `false` 来筛选出 `StartupHostedServiceHealthCheck`（有关详细信息，请参阅[筛选运行状况检查](#filter-health-checks)）：</span><span class="sxs-lookup"><span data-stu-id="3692f-248">The liveness check filters out the `StartupHostedServiceHealthCheck` by returning `false` in the `HealthCheckOptions.Predicate` (for more information, see [Filter health checks](#filter-health-checks)):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_Configure)]

<span data-ttu-id="3692f-249">若要使用示例应用运行就绪情况/运行情况配置方案，请在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-249">To run the readiness/liveness configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario liveness
```

<span data-ttu-id="3692f-250">在浏览器中，访问 `/health/ready` 几次，直到过了 15 秒。</span><span class="sxs-lookup"><span data-stu-id="3692f-250">In a browser, visit `/health/ready` several times until 15 seconds have passed.</span></span> <span data-ttu-id="3692f-251">运行状况检查会在前 15 秒内报告 `Unhealthy`。</span><span class="sxs-lookup"><span data-stu-id="3692f-251">The health check reports `Unhealthy` for the first 15 seconds.</span></span> <span data-ttu-id="3692f-252">15 秒之后，终结点会报告 `Healthy`，这反映托管服务完成了长时间运行的任务。</span><span class="sxs-lookup"><span data-stu-id="3692f-252">After 15 seconds, the endpoint reports `Healthy`, which reflects the completion of the long-running task by the hosted service.</span></span>

### <a name="kubernetes-example"></a><span data-ttu-id="3692f-253">Kubernetes 示例</span><span class="sxs-lookup"><span data-stu-id="3692f-253">Kubernetes example</span></span>

<span data-ttu-id="3692f-254">在诸如 [Kubernetes](https://kubernetes.io/) 这类环境中，使用单独的就绪情况和运行情况检查会十分有用。</span><span class="sxs-lookup"><span data-stu-id="3692f-254">Using separate readiness and liveness checks is useful in an environment such as [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="3692f-255">在 Kubernetes 中，应用可能需要在接受请求之前执行耗时的启动工作，如基础数据库可用性测试。</span><span class="sxs-lookup"><span data-stu-id="3692f-255">In Kubernetes, an app might be required to perform time-consuming startup work before accepting requests, such as a test of the underlying database availability.</span></span> <span data-ttu-id="3692f-256">使用单独检查使业务流程协调程序可以区分应用是否正常运行但尚未准备就绪，或是应用程序是否未能启动。</span><span class="sxs-lookup"><span data-stu-id="3692f-256">Using separate checks allows the orchestrator to distinguish whether the app is functioning but not yet ready or if the app has failed to start.</span></span> <span data-ttu-id="3692f-257">有关 Kubernetes 中的就绪情况和运行情况探测的详细信息，请参阅 Kubernetes 文档中的[配置运行情况和就绪情况探测](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)。</span><span class="sxs-lookup"><span data-stu-id="3692f-257">For more information on readiness and liveness probes in Kubernetes, see [Configure Liveness and Readiness Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) in the Kubernetes documentation.</span></span>

<span data-ttu-id="3692f-258">以下示例演示如何使用 Kubernetes 就绪情况探测配置：</span><span class="sxs-lookup"><span data-stu-id="3692f-258">The following example demonstrates a Kubernetes readiness probe configuration:</span></span>

```
spec:
  template:
  spec:
    readinessProbe:
      # an http probe
      httpGet:
        path: /health/ready
        port: 80
      # length of time to wait for a pod to initialize
      # after pod startup, before applying health checking
      initialDelaySeconds: 30
      timeoutSeconds: 1
    ports:
      - containerPort: 80
```

## <a name="metric-based-probe-with-a-custom-response-writer"></a><span data-ttu-id="3692f-259">具有自定义响应编写器的基于指标的探测</span><span class="sxs-lookup"><span data-stu-id="3692f-259">Metric-based probe with a custom response writer</span></span>

<span data-ttu-id="3692f-260">示例应用演示具有自定义响应编写器的内存运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-260">The sample app demonstrates a memory health check with a custom response writer.</span></span>

<span data-ttu-id="3692f-261">如果应用使用的内存多于给定内存阈值（在示例应用中为 1 GB），则 `MemoryHealthCheck` 报告降级状态。</span><span class="sxs-lookup"><span data-stu-id="3692f-261">`MemoryHealthCheck` reports a degraded status if the app uses more than a given threshold of memory (1 GB in the sample app).</span></span> <span data-ttu-id="3692f-262">`HealthCheckResult` 包括应用的垃圾回收器 (GC) 信息 (MemoryHealthCheck.cs)：</span><span class="sxs-lookup"><span data-stu-id="3692f-262">The `HealthCheckResult` includes Garbage Collector (GC) information for the app (*MemoryHealthCheck.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/MemoryHealthCheck.cs?name=snippet1)]

<span data-ttu-id="3692f-263">在 `Startup.ConfigureServices` 中使用 `AddHealthChecks` 注册运行状况检查服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-263">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="3692f-264">`MemoryHealthCheck` 注册为服务，而不是通过将运行状况检查传递到 `AddCheck` 来启用它。</span><span class="sxs-lookup"><span data-stu-id="3692f-264">Instead of enabling the health check by passing it to `AddCheck`, the `MemoryHealthCheck` is registered as a service.</span></span> <span data-ttu-id="3692f-265">所有 `IHealthCheck` 注册服务都可供运行状况检查服务和中间件使用。</span><span class="sxs-lookup"><span data-stu-id="3692f-265">All `IHealthCheck` registered services are available to the health check services and middleware.</span></span> <span data-ttu-id="3692f-266">建议将运行状况检查服务注册为单一实例服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-266">We recommend registering health check services as Singleton services.</span></span>

<span data-ttu-id="3692f-267">CustomWriterStartup.cs：</span><span class="sxs-lookup"><span data-stu-id="3692f-267">*CustomWriterStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_ConfigureServices&highlight=4)]

<span data-ttu-id="3692f-268">在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件。</span><span class="sxs-lookup"><span data-stu-id="3692f-268">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`.</span></span> <span data-ttu-id="3692f-269">一个 `WriteResponse` 委托提供给 `ResponseWriter` 属性，以在执行运行状况检查时输出自定义 JSON 响应：</span><span class="sxs-lookup"><span data-stu-id="3692f-269">A `WriteResponse` delegate is provided to the `ResponseWriter` property to output a custom JSON response when the health check executes:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_Configure&highlight=6)]

<span data-ttu-id="3692f-270">`WriteResponse` 方法将 `CompositeHealthCheckResult` 格式化为 JSON 对象，并生成运行状况检查响应的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="3692f-270">The `WriteResponse` method formats the `CompositeHealthCheckResult` into a JSON object and yields JSON output for the health check response:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_WriteResponse)]

<span data-ttu-id="3692f-271">若要使用示例应用运行具有自定义响应编写器输出的基于指标的探测，请在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-271">To run the metric-based probe with custom response writer output using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario writer
```

> [!NOTE]
> <span data-ttu-id="3692f-272">[BeatPulse](https://github.com/Xabaril/BeatPulse) 包括基于指标的运行状况检查方案（包括磁盘存储和最大值运行情况检查）。</span><span class="sxs-lookup"><span data-stu-id="3692f-272">[BeatPulse](https://github.com/Xabaril/BeatPulse) includes metric-based health check scenarios, including disk storage and maximum value liveness checks.</span></span>
>
> <span data-ttu-id="3692f-273">[BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。</span><span class="sxs-lookup"><span data-stu-id="3692f-273">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

## <a name="filter-by-port"></a><span data-ttu-id="3692f-274">按端口筛选</span><span class="sxs-lookup"><span data-stu-id="3692f-274">Filter by port</span></span>

<span data-ttu-id="3692f-275">使用端口调用 `UseHealthChecks` 会将运行状况检查请求限制到指定端口。</span><span class="sxs-lookup"><span data-stu-id="3692f-275">Calling `UseHealthChecks` with a port restricts health check requests to the port specified.</span></span> <span data-ttu-id="3692f-276">这通常用于在容器环境中公开用于监视服务的端口。</span><span class="sxs-lookup"><span data-stu-id="3692f-276">This is typically used in a container environment to expose a port for monitoring services.</span></span>

<span data-ttu-id="3692f-277">示例应用使用[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)配置端口。</span><span class="sxs-lookup"><span data-stu-id="3692f-277">The sample app configures the port using the [Environment Variable Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span> <span data-ttu-id="3692f-278">端口在 launchSettings.json 文件设置，并通过环境变量传递到配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="3692f-278">The port is set in the *launchSettings.json* file and passed to the configuration provider via an environment variable.</span></span> <span data-ttu-id="3692f-279">还必须配置服务器以在管理端口上侦听请求。</span><span class="sxs-lookup"><span data-stu-id="3692f-279">You must also configure the server to listen to requests on the management port.</span></span>

<span data-ttu-id="3692f-280">若要使用示例应用演示管理端口配置，请在 Properties 文件夹中创建 launchSettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="3692f-280">To use the sample app to demonstrate management port configuration, create the *launchSettings.json* file in a *Properties* folder.</span></span>

<span data-ttu-id="3692f-281">以下 launchSettings.json 文件未包含在示例应用的项目文件中，必须手动创建。</span><span class="sxs-lookup"><span data-stu-id="3692f-281">The following *launchSettings.json* file isn't included in the sample app's project files and must be created manually.</span></span>

<span data-ttu-id="3692f-282">Properties/launchSettings.json：</span><span class="sxs-lookup"><span data-stu-id="3692f-282">*Properties/launchSettings.json*:</span></span>

```json
{
  "profiles": {
    "SampleApp": {
      "commandName": "Project",
      "commandLineArgs": "",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_URLS": "http://localhost:5000/;http://localhost:5001/",
        "ASPNETCORE_MANAGEMENTPORT": "5001"
      },
      "applicationUrl": "http://localhost:5000/"
    }
  }
}
```

<span data-ttu-id="3692f-283">在 `Startup.ConfigureServices` 中使用 `AddHealthChecks` 注册运行状况检查服务。</span><span class="sxs-lookup"><span data-stu-id="3692f-283">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="3692f-284">`UseHealthChecks` 调用指定管理端口 (ManagementPortStartup.cs)：</span><span class="sxs-lookup"><span data-stu-id="3692f-284">The call to `UseHealthChecks` specifies the management port (*ManagementPortStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ManagementPortStartup.cs?name=snippet1&highlight=12,18)]

> [!NOTE]
> <span data-ttu-id="3692f-285">可以通过在代码中显式设置 URL 和管理端口，来避免在示例应用中创建 launchSettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="3692f-285">You can avoid creating the *launchSettings.json* file in the sample app by setting the URLs and management port explicitly in code.</span></span> <span data-ttu-id="3692f-286">在创建 `WebHostBuilder` 的 Program.cs 中，添加 `UseUrls` 调用并提供应用的正常响应终结点和管理端口终结点。</span><span class="sxs-lookup"><span data-stu-id="3692f-286">In *Program.cs* where the `WebHostBuilder` is created, add a call to `UseUrls` and provide the app's normal response endpoint and the management port endpoint.</span></span> <span data-ttu-id="3692f-287">在调用 `UseHealthChecks` 的 ManagementPortStartup.cs 中，显式指定管理端口。</span><span class="sxs-lookup"><span data-stu-id="3692f-287">In *ManagementPortStartup.cs* where `UseHealthChecks` is called, specify the management port explicitly.</span></span>
>
> <span data-ttu-id="3692f-288">Program.cs:</span><span class="sxs-lookup"><span data-stu-id="3692f-288">*Program.cs*:</span></span>
>
> ```csharp
> return new WebHostBuilder()
>     .UseConfiguration(config)
>     .UseUrls("http://localhost:5000/;http://localhost:5001/")
>     .ConfigureLogging(builder =>
>     {
>         builder.SetMinimumLevel(LogLevel.Trace);
>         builder.AddConfiguration(config);
>         builder.AddConsole();
>     })
>     .UseKestrel()
>     .UseStartup(startupType)
>     .Build();
> ```
>
> <span data-ttu-id="3692f-289">ManagementPortStartup.cs：</span><span class="sxs-lookup"><span data-stu-id="3692f-289">*ManagementPortStartup.cs*:</span></span>
>
> ```csharp
> app.UseHealthChecks("/health", port: 5001);
> ```

<span data-ttu-id="3692f-290">若要使用示例应用运行管理端口配置方案，请在命令行界面中从项目文件夹执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3692f-290">To run the management port configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario port
```

## <a name="distribute-a-health-check-library"></a><span data-ttu-id="3692f-291">分发运行状况检查库</span><span class="sxs-lookup"><span data-stu-id="3692f-291">Distribute a health check library</span></span>

<span data-ttu-id="3692f-292">将运行状况检查作为库进行分发：</span><span class="sxs-lookup"><span data-stu-id="3692f-292">To distribute a health check as a library:</span></span>

1. <span data-ttu-id="3692f-293">编写将 `IHealthCheck` 接口作为独立类来实现的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="3692f-293">Write a health check that implements the `IHealthCheck` interface as a standalone class.</span></span> <span data-ttu-id="3692f-294">该类可以依赖于[依赖关系注入 (DI)](xref:fundamentals/dependency-injection)类型激活和[命名选项](xref:fundamentals/configuration/options)来访问配置数据。</span><span class="sxs-lookup"><span data-stu-id="3692f-294">The class can rely on [dependency injection (DI)](xref:fundamentals/dependency-injection), type activation, and [named options](xref:fundamentals/configuration/options) to access configuration data.</span></span>

   ```csharp
   using System;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   namespace SampleApp
   {
       public class ExampleHealthCheck : IHealthCheck
       {
           private readonly string _data1;
           private readonly int? _data2;

           public ExampleHealthCheck(string data1, int? data2)
           {
               _data1 = data1 ?? throw new ArgumentNullException(nameof(data1));
               _data2 = data2 ?? throw new ArgumentNullException(nameof(data2));
           }

           public async Task<HealthCheckResult> CheckHealthAsync(
               HealthCheckContext context, CancellationToken cancellationToken)
           {
               try
               {
                   // Health check logic
                   //
                   // data1 and data2 are used in the method to
                   // run the probe's health check logic.

                   // Assume that it's possible for this health check
                   // to throw an AccessViolationException.

                   return HealthCheckResult.Healthy();
               }
               catch (AccessViolationException ex)
               {
                   return new HealthCheckResult(
                       context.Registration.FailureStatus,
                       description: "An access violation occurred during the check.",
                       exception: ex,
                       data: null);
               }
           }
       }
   }
   ```

1. <span data-ttu-id="3692f-295">使用参数编写一个扩展方法，所使用的应用会在其 `Startup.Configure` 方法中调用它。</span><span class="sxs-lookup"><span data-stu-id="3692f-295">Write an extension method with parameters that the consuming app calls in its `Startup.Configure` method.</span></span> <span data-ttu-id="3692f-296">在以下示例中，假设以下运行状况检查方法签名：</span><span class="sxs-lookup"><span data-stu-id="3692f-296">In the following example, assume the following health check method signature:</span></span>

   ```csharp
   ExampleHealthCheck(string, string, int )
   ```

   <span data-ttu-id="3692f-297">前面的签名指示 `ExampleHealthCheck` 需要其他数据来处理运行状况检查探测逻辑。</span><span class="sxs-lookup"><span data-stu-id="3692f-297">The preceding signature indicates that the `ExampleHealthCheck` requires additional data to process the health check probe logic.</span></span> <span data-ttu-id="3692f-298">当运行状况检查向扩展方法注册时，数据会提供给用于创建运行状况检查实例的委托。</span><span class="sxs-lookup"><span data-stu-id="3692f-298">The data is provided to the delegate used to create the health check instance when the health check is registered with an extension method.</span></span> <span data-ttu-id="3692f-299">在以下示例中，调用方会指定可选的：</span><span class="sxs-lookup"><span data-stu-id="3692f-299">In the following example, the caller specifies optional:</span></span>

   * <span data-ttu-id="3692f-300">运行状况检查名称 (`name`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-300">health check name (`name`).</span></span> <span data-ttu-id="3692f-301">如果为 `null`，则使用 `example_health_check`。</span><span class="sxs-lookup"><span data-stu-id="3692f-301">If `null`, `example_health_check` is used.</span></span>
   * <span data-ttu-id="3692f-302">运行状况检查的字符串数据点 (`data1`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-302">string data point for the health check (`data1`).</span></span>
   * <span data-ttu-id="3692f-303">运行状况检查的整数数据点 (`data2`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-303">integer data point for the health check (`data2`).</span></span> <span data-ttu-id="3692f-304">如果为 `null`，则使用 `1`。</span><span class="sxs-lookup"><span data-stu-id="3692f-304">If `null`, `1` is used.</span></span>
   * <span data-ttu-id="3692f-305">失败状态 (`HealthStatus`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-305">failure status (`HealthStatus`).</span></span> <span data-ttu-id="3692f-306">默认值为 `null`。</span><span class="sxs-lookup"><span data-stu-id="3692f-306">The default is `null`.</span></span> <span data-ttu-id="3692f-307">如果为 `null`，则对失败状态报告 `HealthStatus.Unhealthy`。</span><span class="sxs-lookup"><span data-stu-id="3692f-307">If `null`, `HealthStatus.Unhealthy` is reported for a failure status.</span></span>
   * <span data-ttu-id="3692f-308">标记 (`IEnumerable<string>`)。</span><span class="sxs-lookup"><span data-stu-id="3692f-308">tags (`IEnumerable<string>`).</span></span>

   ```csharp
   using System.Collections.Generic;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   public static class ExampleHealthCheckBuilderExtensions
   {
       const string NAME = "example_health_check";

       public static IHealthChecksBuilder AddExampleHealthCheck(
           this IHealthChecksBuilder builder, 
           string name = default, 
           string data1, 
           int data2 = 1, 
           HealthStatus? failureStatus = default, 
           IEnumerable<string> tags = default)
       {
           return builder.Add(new HealthCheckRegistration(
               name ?? NAME,
               sp => new ExampleHealthCheck(data1, data2),
               failureStatus,
               tags));
       }
   }
   ```

## <a name="health-check-publisher"></a><span data-ttu-id="3692f-309">运行状况检查发布服务器</span><span class="sxs-lookup"><span data-stu-id="3692f-309">Health Check Publisher</span></span>

<span data-ttu-id="3692f-310">当 `IHealthCheckPublisher` 添加到服务容器时，运行状况检查系统，会定期执行运行状况检查并使用结果调用 `PublishAsync`。</span><span class="sxs-lookup"><span data-stu-id="3692f-310">When an `IHealthCheckPublisher` is added to the service container, the health check system periodically executes your health checks and calls `PublishAsync` with the result.</span></span> <span data-ttu-id="3692f-311">在期望每个进程定期调用监视系统以便确定运行状况的基于推送的运行状况监视系统方案中，这十分有用。</span><span class="sxs-lookup"><span data-stu-id="3692f-311">This is useful in a push-based health monitoring system scenario that expects each process to call the monitoring system periodically in order to determine health.</span></span>

<span data-ttu-id="3692f-312">`IHealthCheckPublisher` 接口具有单个方法：</span><span class="sxs-lookup"><span data-stu-id="3692f-312">The `IHealthCheckPublisher` interface has a single method:</span></span>

```csharp
Task PublishAsync(HealthReport report, CancellationToken cancellationToken);
```

> [!NOTE]
> <span data-ttu-id="3692f-313">[BeatPulse](https://github.com/Xabaril/BeatPulse) 包括多个系统的发布服务器（包括 [Application Insights](/azure/application-insights/app-insights-overview)）。</span><span class="sxs-lookup"><span data-stu-id="3692f-313">[BeatPulse](https://github.com/Xabaril/BeatPulse) includes publishers for several systems, including [Application Insights](/azure/application-insights/app-insights-overview).</span></span>
>
> <span data-ttu-id="3692f-314">[BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。</span><span class="sxs-lookup"><span data-stu-id="3692f-314">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>
