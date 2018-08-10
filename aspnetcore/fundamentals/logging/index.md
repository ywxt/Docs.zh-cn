---
title: ASP.NET Core 中的日志记录
author: ardalis
description: 了解 ASP.NET Core 中的记录框架。 发现内置日志记录提供程序，并详细了解常见第三方提供程序。
ms.author: tdykstra
ms.date: 07/24/2018
uid: fundamentals/logging/index
ms.openlocfilehash: 35bb7fa51db541f825a79151fb7fbe85d48e1998
ms.sourcegitcommit: 028ad28c546de706ace98066c76774de33e4ad20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/08/2018
ms.locfileid: "39655354"
---
# <a name="logging-in-aspnet-core"></a><span data-ttu-id="0078d-104">ASP.NET Core 中的日志记录</span><span class="sxs-lookup"><span data-stu-id="0078d-104">Logging in ASP.NET Core</span></span>

<span data-ttu-id="0078d-105">作者：[Steve Smith](https://ardalis.com/) 和 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0078d-105">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0078d-106">ASP.NET Core 支持适用于各种日志记录提供程序的日志记录 API。</span><span class="sxs-lookup"><span data-stu-id="0078d-106">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="0078d-107">通过内置提供程序，可向一个或多个目标发送日志，还可插入第三方记录框架。</span><span class="sxs-lookup"><span data-stu-id="0078d-107">Built-in providers let you send logs to one or more destinations, and you can plug in a third-party logging framework.</span></span> <span data-ttu-id="0078d-108">本文介绍如何在代码中使用内置日志记录 API 和提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-108">This article shows how to use the built-in logging API and providers in your code.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="0078d-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0078d-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="0078d-110">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0078d-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker-end

<span data-ttu-id="0078d-111">有关使用 IIS 进行托管时的 stdout 日志记录的信息，请参阅 <xref:host-and-deploy/iis/troubleshoot#aspnet-core-module-stdout-log>。</span><span class="sxs-lookup"><span data-stu-id="0078d-111">For information on stdout logging when hosting with IIS, see <xref:host-and-deploy/iis/troubleshoot#aspnet-core-module-stdout-log>.</span></span> <span data-ttu-id="0078d-112">有关使用 Azure 应用服务进行 stdout 日志记录的信息，请参阅 <xref:host-and-deploy/azure-apps/troubleshoot#aspnet-core-module-stdout-log>。</span><span class="sxs-lookup"><span data-stu-id="0078d-112">For information on stdout logging with Azure App Service, see <xref:host-and-deploy/azure-apps/troubleshoot#aspnet-core-module-stdout-log>.</span></span>

## <a name="how-to-create-logs"></a><span data-ttu-id="0078d-113">如何创建日志</span><span class="sxs-lookup"><span data-stu-id="0078d-113">How to create logs</span></span>

<span data-ttu-id="0078d-114">要创建日志，请从[依赖关系注入](xref:fundamentals/dependency-injection)容器实现 [ILogger&lt;TCategoryName&gt;](/dotnet/api/microsoft.extensions.logging.ilogger-1) 对象：</span><span class="sxs-lookup"><span data-stu-id="0078d-114">To create logs, implement an [ILogger&lt;TCategoryName&gt;](/dotnet/api/microsoft.extensions.logging.ilogger-1) object from the [dependency injection](xref:fundamentals/dependency-injection) container:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="0078d-115">然后在该记录器对象上调用日志记录方法：</span><span class="sxs-lookup"><span data-stu-id="0078d-115">Then call logging methods on that logger object:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="0078d-116">此示例使用 `TodoController` 类创建日志作为类别。</span><span class="sxs-lookup"><span data-stu-id="0078d-116">This example creates logs with the `TodoController` class as the *category*.</span></span> <span data-ttu-id="0078d-117">[本文的稍后部分](#log-category)对这些类别进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="0078d-117">Categories are explained [later in this article](#log-category).</span></span>

<span data-ttu-id="0078d-118">ASP.NET Core 不提供异步记录器方法，因为日志记录的速度应非常快，使用异步的代价是不值得的。</span><span class="sxs-lookup"><span data-stu-id="0078d-118">ASP.NET Core doesn't provide async logger methods because logging should be so fast that it isn't worth the cost of using async.</span></span> <span data-ttu-id="0078d-119">如果发现自己的实际情况与上述不同，请考虑更改记录方式。</span><span class="sxs-lookup"><span data-stu-id="0078d-119">If you're in a situation where that's not true, consider changing the way you log.</span></span> <span data-ttu-id="0078d-120">如果数据存储速度较慢，请先将日志消息写入快速存储，稍后再将其转移至低速存储。</span><span class="sxs-lookup"><span data-stu-id="0078d-120">If your data store is slow, write the log messages to a fast store first, then move them to a slow store later.</span></span> <span data-ttu-id="0078d-121">例如，记录到由另一进程读取和暂留以减缓存储的消息队列。</span><span class="sxs-lookup"><span data-stu-id="0078d-121">For example, log to a message queue that's read and persisted to slow storage by another process.</span></span>

## <a name="how-to-add-providers"></a><span data-ttu-id="0078d-122">如何添加提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-122">How to add providers</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="0078d-123">日志记录提供程序通过 `ILogger` 对象获取所创建的消息，并显示或存储它们。</span><span class="sxs-lookup"><span data-stu-id="0078d-123">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="0078d-124">例如，控制台提供程序在控制台上显示消息，Azure App Service 提供程序可将消息存储在 Azure blob 存储中。</span><span class="sxs-lookup"><span data-stu-id="0078d-124">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="0078d-125">要使用提供程序，请在 Program.cs 中调用提供程序的 `Add<ProviderName>` 扩展方法：</span><span class="sxs-lookup"><span data-stu-id="0078d-125">To use a provider, call the provider's `Add<ProviderName>` extension method in *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=16,17)]

<span data-ttu-id="0078d-126">借助默认项目模板，可以在 Program.cs 中调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 扩展方法，从而启用控制台和调试日志记录提供程序：</span><span class="sxs-lookup"><span data-stu-id="0078d-126">The default project template enables the Console and Debug logging providers with a call to the [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) extension method in *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_TemplateCode&highlight=7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="0078d-127">日志记录提供程序通过 `ILogger` 对象获取所创建的消息，并显示或存储它们。</span><span class="sxs-lookup"><span data-stu-id="0078d-127">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="0078d-128">例如，控制台提供程序在控制台上显示消息，Azure App Service 提供程序可将消息存储在 Azure blob 存储中。</span><span class="sxs-lookup"><span data-stu-id="0078d-128">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="0078d-129">要使用提供程序，请安装其 NuGet 包，并在 [ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory) 的实例上调用提供程序的扩展方法，如下方示例所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-129">To use a provider, install its NuGet package and call the provider's extension method on an instance of [ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory), as shown in the following example:</span></span>

[!code-csharp[](index/sample//Startup.cs?name=snippet_AddConsoleAndDebug&highlight=3,5-7)]

<span data-ttu-id="0078d-130">ASP.NET Core [依赖关系注入](xref:fundamentals/dependency-injection) (DI) 将提供 `ILoggerFactory` 实例。</span><span class="sxs-lookup"><span data-stu-id="0078d-130">ASP.NET Core [dependency injection](xref:fundamentals/dependency-injection) (DI) provides the `ILoggerFactory` instance.</span></span> <span data-ttu-id="0078d-131">在 [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) 和 [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) 包中定义了 `AddConsole` 和 `AddDebug` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="0078d-131">The `AddConsole` and `AddDebug` extension methods are defined in the [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) and [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) packages.</span></span> <span data-ttu-id="0078d-132">每个扩展方法都调用 `ILoggerFactory.AddProvider` 方法，传入提供程序的一个实例。</span><span class="sxs-lookup"><span data-stu-id="0078d-132">Each extension method calls the `ILoggerFactory.AddProvider` method, passing in an instance of the provider.</span></span>

> [!NOTE]
> <span data-ttu-id="0078d-133">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample)在 `Startup.Configure` 方法中添加了日志提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-133">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) adds logging providers in the `Startup.Configure` method.</span></span> <span data-ttu-id="0078d-134">要从先前执行的代码获取日志输出，请在 `Startup` 类构造函数中添加日志提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-134">If you want to obtain log output from code that executes earlier, add logging providers in the `Startup` class constructor.</span></span>

::: moniker-end

<span data-ttu-id="0078d-135">详细了解[内置日志记录提供程序](#built-in-logging-providers)，并查找本文稍后部分介绍的[第三方日志记录提供程序](#third-party-logging-providers)的链接。</span><span class="sxs-lookup"><span data-stu-id="0078d-135">Learn more about the [built-in logging providers](#built-in-logging-providers) and find links to [third-party logging providers](#third-party-logging-providers) later in the article.</span></span>

## <a name="configuration"></a><span data-ttu-id="0078d-136">配置</span><span class="sxs-lookup"><span data-stu-id="0078d-136">Configuration</span></span>

<span data-ttu-id="0078d-137">日志记录提供程序配置由一个或多个配置提供程序提供：</span><span class="sxs-lookup"><span data-stu-id="0078d-137">Logging provider configuration is provided by one or more configuration providers:</span></span>

* <span data-ttu-id="0078d-138">文件格式（INI、JSON 和 XML）。</span><span class="sxs-lookup"><span data-stu-id="0078d-138">File formats (INI, JSON, and XML).</span></span>
* <span data-ttu-id="0078d-139">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="0078d-139">Command-line arguments.</span></span>
* <span data-ttu-id="0078d-140">环境变量。</span><span class="sxs-lookup"><span data-stu-id="0078d-140">Environment variables.</span></span>
* <span data-ttu-id="0078d-141">内存中的 .NET 对象。</span><span class="sxs-lookup"><span data-stu-id="0078d-141">In-memory .NET objects.</span></span>
* <span data-ttu-id="0078d-142">未加密的[机密管理器](xref:security/app-secrets)存储。</span><span class="sxs-lookup"><span data-stu-id="0078d-142">The unencrypted [Secret Manager](xref:security/app-secrets) storage.</span></span>
* <span data-ttu-id="0078d-143">加密的用户存储，如 [Azure Key Vault](xref:security/key-vault-configuration)。</span><span class="sxs-lookup"><span data-stu-id="0078d-143">An encrypted user store, such as [Azure Key Vault](xref:security/key-vault-configuration).</span></span>
* <span data-ttu-id="0078d-144">（已安装或已创建的）自定义提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-144">Custom providers (installed or created).</span></span>

<span data-ttu-id="0078d-145">例如，日志记录配置通常由应用设置文件的 `Logging` 部分提供。</span><span class="sxs-lookup"><span data-stu-id="0078d-145">For example, logging configuration is commonly provided by the `Logging` section of app settings files.</span></span> <span data-ttu-id="0078d-146">以下示例显示了典型 *appsettings.Development.json* 文件的内容：</span><span class="sxs-lookup"><span data-stu-id="0078d-146">The following example shows the contents of a typical *appsettings.Development.json* file:</span></span>

::: moniker range=">= aspnetcore-2.1"

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    },
    "Console":
    {
      "IncludeScopes": "true"
    }
  }
}
```

<span data-ttu-id="0078d-147">`LogLevel` 项表示日志名称。</span><span class="sxs-lookup"><span data-stu-id="0078d-147">`LogLevel` keys represent log names.</span></span> <span data-ttu-id="0078d-148">`Default` 项适用于未显式列出的日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-148">The `Default` key applies to logs not explicitly listed.</span></span> <span data-ttu-id="0078d-149">其值表示应用于给定日志的[日志级别](#log-level)。</span><span class="sxs-lookup"><span data-stu-id="0078d-149">The value represents the [log level](#log-level) applied to the given log.</span></span> <span data-ttu-id="0078d-150">设置 `IncludeScopes`（示例中的 `Console`）的日志项指定是否为相关日志启用了[日志作用域](#log-scopes)。</span><span class="sxs-lookup"><span data-stu-id="0078d-150">Log keys that set `IncludeScopes` (`Console` in the example), specify if [log scopes](#log-scopes) are enabled for the indicated log.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    }
  }
}
```

<span data-ttu-id="0078d-151">`LogLevel` 项表示日志名称。</span><span class="sxs-lookup"><span data-stu-id="0078d-151">`LogLevel` keys represent log names.</span></span> <span data-ttu-id="0078d-152">`Default` 项适用于未显式列出的日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-152">The `Default` key applies to logs not explicitly listed.</span></span> <span data-ttu-id="0078d-153">其值表示应用于给定日志的[日志级别](#log-level)。</span><span class="sxs-lookup"><span data-stu-id="0078d-153">The value represents the [log level](#log-level) applied to the given log.</span></span>

::: moniker-end

<span data-ttu-id="0078d-154">若要了解如何实现配置提供程序，请参阅 <xref:fundamentals/configuration/index>。</span><span class="sxs-lookup"><span data-stu-id="0078d-154">For information on implementing configuration providers, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="sample-logging-output"></a><span data-ttu-id="0078d-155">日志记录输出示例</span><span class="sxs-lookup"><span data-stu-id="0078d-155">Sample logging output</span></span>

<span data-ttu-id="0078d-156">从命令行运行上一部分所示的示例代码时，将在控制台中看到日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-156">With the sample code shown in the preceding section, you'll see logs in the console when you run from the command line.</span></span> <span data-ttu-id="0078d-157">以下是控制台输出示例：</span><span class="sxs-lookup"><span data-stu-id="0078d-157">Here's an example of console output:</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:5000/api/todo/0
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 42.9286ms
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 148.889ms 404
```

<span data-ttu-id="0078d-158">转到 `http://localhost:5000/api/todo/0`，触发上一部分所示的两个 `ILogger` 调用的执行，创建了以上日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-158">These logs were created by going to `http://localhost:5000/api/todo/0`, which triggers execution of both `ILogger` calls shown in the preceding section.</span></span>

<span data-ttu-id="0078d-159">在 Visual Studio 中运行示例应用程序时，“调试”窗口中将显示如下日志：</span><span class="sxs-lookup"><span data-stu-id="0078d-159">Here's an example of the same logs as they appear in the Debug window when you run the sample application in Visual Studio:</span></span>

```console
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request starting HTTP/1.1 GET http://localhost:53104/api/todo/0  
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
TodoApi.Controllers.TodoController:Information: Getting item 0
TodoApi.Controllers.TodoController:Warning: GetById(0) NOT FOUND
Microsoft.AspNetCore.Mvc.StatusCodeResult:Information: Executing HttpStatusCodeResult, setting HTTP status code 404
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 152.5657ms
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request finished in 316.3195ms 404
```

<span data-ttu-id="0078d-160">由上一部分所示的 `ILogger` 调用创建的日志以“TodoApi.Controllers.TodoController”开头的。</span><span class="sxs-lookup"><span data-stu-id="0078d-160">The logs that were created by the `ILogger` calls shown in the preceding section begin with "TodoApi.Controllers.TodoController".</span></span> <span data-ttu-id="0078d-161">以“Microsoft”类别开头的日志来自 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="0078d-161">The logs that begin with "Microsoft" categories are from ASP.NET Core.</span></span> <span data-ttu-id="0078d-162">ASP.NET Core 本身和应用程序代码使用相同的日志记录 API 和日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-162">ASP.NET Core itself and your application code are using the same logging API and the same logging providers.</span></span>

<span data-ttu-id="0078d-163">本文余下部分将介绍有关日志记录的某些详细信息及选项。</span><span class="sxs-lookup"><span data-stu-id="0078d-163">The remainder of this article explains some details and options for logging.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="0078d-164">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="0078d-164">NuGet packages</span></span>

<span data-ttu-id="0078d-165">`ILogger` 和 `ILoggerFactory` 接口位于 [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/) 中，其默认实现位于 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/) 中。</span><span class="sxs-lookup"><span data-stu-id="0078d-165">The `ILogger` and `ILoggerFactory` interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), and default implementations for them are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/).</span></span>

## <a name="log-category"></a><span data-ttu-id="0078d-166">日志类别</span><span class="sxs-lookup"><span data-stu-id="0078d-166">Log category</span></span>

<span data-ttu-id="0078d-167">所创建的每个日志都包含一个类别。</span><span class="sxs-lookup"><span data-stu-id="0078d-167">A *category* is included with each log that you create.</span></span> <span data-ttu-id="0078d-168">在创建 `ILogger` 对象时指定类别。</span><span class="sxs-lookup"><span data-stu-id="0078d-168">You specify the category when you create an `ILogger` object.</span></span> <span data-ttu-id="0078d-169">类别可以是任意字符串，但约定使用写入日志的类的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="0078d-169">The category may be any string, but a convention is to use the fully qualified name of the class from which the logs are written.</span></span> <span data-ttu-id="0078d-170">例如“TodoApi.Controllers.TodoController”。</span><span class="sxs-lookup"><span data-stu-id="0078d-170">For example: "TodoApi.Controllers.TodoController".</span></span>

<span data-ttu-id="0078d-171">可以将类别指定为字符串，或使用从类型派生类别的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="0078d-171">You can specify the category as a string or use an extension method that derives the category from the type.</span></span> <span data-ttu-id="0078d-172">要将类别指定为字符串，请在 `ILoggerFactory` 实例上调用 `CreateLogger`，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0078d-172">To specify the category as a string, call `CreateLogger` on an `ILoggerFactory` instance, as shown below.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

<span data-ttu-id="0078d-173">如下方示例所示，在大多数情况下使用 `ILogger<T>` 更简单。</span><span class="sxs-lookup"><span data-stu-id="0078d-173">Most of the time, it will be easier to use `ILogger<T>`, as in the following example.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="0078d-174">这相当于使用 `T` 的完全限定类型名称来调用 `CreateLogger`。</span><span class="sxs-lookup"><span data-stu-id="0078d-174">This is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="0078d-175">日志级别</span><span class="sxs-lookup"><span data-stu-id="0078d-175">Log level</span></span>

<span data-ttu-id="0078d-176">每次写入日志时都需指定其 [LogLevel](/dotnet/api/microsoft.extensions.logging.logLevel)。</span><span class="sxs-lookup"><span data-stu-id="0078d-176">Each time you write a log, you specify its [LogLevel](/dotnet/api/microsoft.extensions.logging.logLevel).</span></span> <span data-ttu-id="0078d-177">日志级别指示严重性或重要程度。</span><span class="sxs-lookup"><span data-stu-id="0078d-177">The log level indicates the degree of severity or importance.</span></span> <span data-ttu-id="0078d-178">例如，如果方法正常结束则写入 `Information` 日志，如果方法返回 404 返回代码则写入 `Warning` 日志，如果捕获未知异常则写入 `Error` 日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-178">For example, you might write an `Information` log when a method ends normally, a `Warning` log when a method returns a 404 return code, and an `Error` log when you catch an unexpected exception.</span></span>

<span data-ttu-id="0078d-179">在下列代码示例中，由方法的名称（如 `LogWarning`）指定日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-179">In the following code example, the names of the methods (for example, `LogWarning`) specify the log level.</span></span> <span data-ttu-id="0078d-180">第一个参数是[日志事件 ID](#log-event-id)。</span><span class="sxs-lookup"><span data-stu-id="0078d-180">The first parameter is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="0078d-181">第二个形参是[消息模板](#log-message-template)，包含由剩余方法形参提供的实参值的占位符。</span><span class="sxs-lookup"><span data-stu-id="0078d-181">The second parameter is a [message template](#log-message-template) with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="0078d-182">本文稍后部分更详细地介绍了方法参数。</span><span class="sxs-lookup"><span data-stu-id="0078d-182">The method parameters are explained in more detail later in this article.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="0078d-183">在方法名称中包含级别的日志方法是 [ILogger 的扩展方法](/dotnet/api/microsoft.extensions.logging.loggerextensions)。</span><span class="sxs-lookup"><span data-stu-id="0078d-183">Log methods that include the level in the method name are [extension methods for ILogger](/dotnet/api/microsoft.extensions.logging.loggerextensions).</span></span> <span data-ttu-id="0078d-184">在后台，这些方法调用可接受 `LogLevel` 参数的 `Log` 方法。</span><span class="sxs-lookup"><span data-stu-id="0078d-184">Behind the scenes, these methods call a `Log` method that takes a `LogLevel` parameter.</span></span> <span data-ttu-id="0078d-185">可直接调用 `Log` 方法而不调用其中某个扩展方法，但语法相对复杂。</span><span class="sxs-lookup"><span data-stu-id="0078d-185">You can call the `Log` method directly rather than one of these extension methods, but the syntax is relatively complicated.</span></span> <span data-ttu-id="0078d-186">有关详细信息，请参阅 [ILogger 接口](/dotnet/api/microsoft.extensions.logging.ilogger)和[记录器扩展源代码](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs)。</span><span class="sxs-lookup"><span data-stu-id="0078d-186">For more information, see the [ILogger interface](/dotnet/api/microsoft.extensions.logging.ilogger) and the [logger extensions source code](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span></span>

<span data-ttu-id="0078d-187">ASP.NET Core 定义了以下[日志级别](/dotnet/api/microsoft.extensions.logging.loglevel)（按严重性从低到高排列）。</span><span class="sxs-lookup"><span data-stu-id="0078d-187">ASP.NET Core defines the following [log levels](/dotnet/api/microsoft.extensions.logging.loglevel), ordered here from least to highest severity.</span></span>

* <span data-ttu-id="0078d-188">跟踪 = 0</span><span class="sxs-lookup"><span data-stu-id="0078d-188">Trace = 0</span></span>

  <span data-ttu-id="0078d-189">表示仅对于开发人员调试问题有价值的信息。</span><span class="sxs-lookup"><span data-stu-id="0078d-189">For information that's valuable only to a developer debugging an issue.</span></span> <span data-ttu-id="0078d-190">这些消息可能包含敏感应用程序数据，因此不得在生产环境中启用它们。</span><span class="sxs-lookup"><span data-stu-id="0078d-190">These messages may contain sensitive application data and so shouldn't be enabled in a production environment.</span></span> <span data-ttu-id="0078d-191">默认情况下禁用。</span><span class="sxs-lookup"><span data-stu-id="0078d-191">*Disabled by default.*</span></span> <span data-ttu-id="0078d-192">示例：`Credentials: {"User":"someuser", "Password":"P@ssword"}`</span><span class="sxs-lookup"><span data-stu-id="0078d-192">Example: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span></span>

* <span data-ttu-id="0078d-193">调试 = 1</span><span class="sxs-lookup"><span data-stu-id="0078d-193">Debug = 1</span></span>

  <span data-ttu-id="0078d-194">表示在开发和调试过程中短期有用的信息。</span><span class="sxs-lookup"><span data-stu-id="0078d-194">For information that has short-term usefulness during development and debugging.</span></span> <span data-ttu-id="0078d-195">示例：`Entering method Configure with flag set to true.`。除非要排查问题，否则通常不会在生产中启用 `Debug` 级别日志，因为日志数量过多。</span><span class="sxs-lookup"><span data-stu-id="0078d-195">Example: `Entering method Configure with flag set to true.` You typically wouldn't enable `Debug` level logs in production unless you are troubleshooting, due to the high volume of logs.</span></span>

* <span data-ttu-id="0078d-196">信息 = 2</span><span class="sxs-lookup"><span data-stu-id="0078d-196">Information = 2</span></span>

  <span data-ttu-id="0078d-197">用于跟踪应用程序的常规流。</span><span class="sxs-lookup"><span data-stu-id="0078d-197">For tracking the general flow of the application.</span></span> <span data-ttu-id="0078d-198">这些日志通常有长期价值。</span><span class="sxs-lookup"><span data-stu-id="0078d-198">These logs typically have some long-term value.</span></span> <span data-ttu-id="0078d-199">示例：`Request received for path /api/todo`</span><span class="sxs-lookup"><span data-stu-id="0078d-199">Example: `Request received for path /api/todo`</span></span>

* <span data-ttu-id="0078d-200">警告 = 3</span><span class="sxs-lookup"><span data-stu-id="0078d-200">Warning = 3</span></span>

  <span data-ttu-id="0078d-201">表示应用程序流中的异常或意外事件。</span><span class="sxs-lookup"><span data-stu-id="0078d-201">For abnormal or unexpected events in the application flow.</span></span> <span data-ttu-id="0078d-202">可能包括不会中断应用程序运行但仍需调查的错误或其他条件。</span><span class="sxs-lookup"><span data-stu-id="0078d-202">These may include errors or other conditions that don't cause the application to stop, but which may need to be investigated.</span></span> <span data-ttu-id="0078d-203">`Warning` 日志级别常用于已处理的异常。</span><span class="sxs-lookup"><span data-stu-id="0078d-203">Handled exceptions are a common place to use the `Warning` log level.</span></span> <span data-ttu-id="0078d-204">示例：`FileNotFoundException for file quotes.txt.`</span><span class="sxs-lookup"><span data-stu-id="0078d-204">Example: `FileNotFoundException for file quotes.txt.`</span></span>

* <span data-ttu-id="0078d-205">错误 = 4</span><span class="sxs-lookup"><span data-stu-id="0078d-205">Error = 4</span></span>

  <span data-ttu-id="0078d-206">表示无法处理的错误和异常。</span><span class="sxs-lookup"><span data-stu-id="0078d-206">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="0078d-207">这些消息指示的是当前活动或操作（如当前 HTTP 请求）中的失败，而不是应用程序范围的失败。</span><span class="sxs-lookup"><span data-stu-id="0078d-207">These messages indicate a failure in the current activity or operation (such as the current HTTP request), not an application-wide failure.</span></span> <span data-ttu-id="0078d-208">日志消息示例：`Cannot insert record due to duplicate key violation.`</span><span class="sxs-lookup"><span data-stu-id="0078d-208">Example log message: `Cannot insert record due to duplicate key violation.`</span></span>

* <span data-ttu-id="0078d-209">严重 = 5</span><span class="sxs-lookup"><span data-stu-id="0078d-209">Critical = 5</span></span>

  <span data-ttu-id="0078d-210">需要立即关注的失败。</span><span class="sxs-lookup"><span data-stu-id="0078d-210">For failures that require immediate attention.</span></span> <span data-ttu-id="0078d-211">例如数据丢失、磁盘空间不足。</span><span class="sxs-lookup"><span data-stu-id="0078d-211">Examples: data loss scenarios, out of disk space.</span></span>

<span data-ttu-id="0078d-212">可以使用日志级别控制写入到特定存储介质或显示窗口的日志输出量。</span><span class="sxs-lookup"><span data-stu-id="0078d-212">You can use the log level to control how much log output is written to a particular storage medium or display window.</span></span> <span data-ttu-id="0078d-213">例如在生产中，可将所有 `Information` 及以下级别的日志放在卷数据存储，将所有 `Warning` 及以上级别的日志放在值数据存储。</span><span class="sxs-lookup"><span data-stu-id="0078d-213">For example, in production you might want all logs of `Information` level and lower to go to a volume data store, and all logs of `Warning` level and higher to go to a value data store.</span></span> <span data-ttu-id="0078d-214">在开发期间，通常要将严重性为 `Warning` 或以上级别的日志发送到控制台。</span><span class="sxs-lookup"><span data-stu-id="0078d-214">During development, you might normally send logs of `Warning` or higher severity to the console.</span></span> <span data-ttu-id="0078d-215">需要进行故障排除时，可添加 `Debug` 级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-215">Then when you need to troubleshoot, you can add `Debug` level.</span></span> <span data-ttu-id="0078d-216">本文稍后的[日志筛选](#log-filtering)部分介绍如何控制提供程序处理的日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-216">The [Log filtering](#log-filtering) section later in this article explains how to control which log levels a provider handles.</span></span>

<span data-ttu-id="0078d-217">ASP.NET Core 框架为框架事件写入 `Debug` 级别日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-217">The ASP.NET Core framework writes `Debug` level logs for framework events.</span></span> <span data-ttu-id="0078d-218">本文前面部分提供的日志示例排除了低于 `Information` 级别的日志，因此未显示 `Debug` 级别日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-218">The log examples earlier in this article excluded logs below `Information` level, so no `Debug` level logs were shown.</span></span> <span data-ttu-id="0078d-219">如果运行配置为显示控制台提供程序 `Debug` 及以上级别的日志的示例应用程序，则控制台日志示例如下所示。</span><span class="sxs-lookup"><span data-stu-id="0078d-219">Here's an example of console logs if you run the sample application configured to show `Debug` and higher logs for the console provider.</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:62555/api/todo/0
dbug: Microsoft.AspNetCore.Routing.Tree.TreeRouter[1]
      Request successfully matched the route with name 'GetTodo' and template 'api/Todo/{id}'.
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Update (TodoApi)' with id '089d59b6-92ec-472d-b552-cc613dfd625d' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Delete (TodoApi)' with id 'f3476abe-4bd9-4ad3-9261-3ead09607366' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action TodoApi.Controllers.TodoController.GetById (TodoApi)
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action method TodoApi.Controllers.TodoController.GetById (TodoApi), returned result Microsoft.AspNetCore.Mvc.NotFoundResult.
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 0.8788ms
dbug: Microsoft.AspNetCore.Server.Kestrel[9]
      Connection id "0HL6L7NEFF2QD" completed keep alive response.
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 2.7286ms 404
```

## <a name="log-event-id"></a><span data-ttu-id="0078d-220">日志事件 ID</span><span class="sxs-lookup"><span data-stu-id="0078d-220">Log event ID</span></span>

<span data-ttu-id="0078d-221">每次写入日志时都可指定一个事件 ID。</span><span class="sxs-lookup"><span data-stu-id="0078d-221">Each time you write a log, you can specify an *event ID*.</span></span> <span data-ttu-id="0078d-222">该示例应用通过使用本地定义的 `LoggingEvents` 类来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="0078d-222">The sample app does this by using a locally-defined `LoggingEvents` class:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/sample//Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

<span data-ttu-id="0078d-223">事件 ID 是一个整数值，可用于关联多组已记录事件。</span><span class="sxs-lookup"><span data-stu-id="0078d-223">An event ID is an integer value that you can use to associate a set of logged events with one another.</span></span> <span data-ttu-id="0078d-224">例如，向购物车添加项的日志可以是事件 ID 1000，完成购买的日志可以是事件 ID 1001。</span><span class="sxs-lookup"><span data-stu-id="0078d-224">For instance, a log for adding an item to a shopping cart could be event ID 1000 and a log for completing a purchase could be event ID 1001.</span></span>

<span data-ttu-id="0078d-225">在日志记录输出中，事件 ID 既可存储在字段里，也可包含在文本消息内，这由提供程序来决定。</span><span class="sxs-lookup"><span data-stu-id="0078d-225">In logging output, the event ID may be stored in a field or included in the text message, depending on the provider.</span></span> <span data-ttu-id="0078d-226">调试提供程序不显示事件 ID，但控制台提供程序会将其显示在类别后的括号里：</span><span class="sxs-lookup"><span data-stu-id="0078d-226">The Debug provider doesn't show event IDs, but the console provider shows them in brackets after the category:</span></span>

```console
info: TodoApi.Controllers.TodoController[1002]
      Getting item invalidid
warn: TodoApi.Controllers.TodoController[4000]
      GetById(invalidid) NOT FOUND
```

## <a name="log-message-template"></a><span data-ttu-id="0078d-227">日志消息模板</span><span class="sxs-lookup"><span data-stu-id="0078d-227">Log message template</span></span>

<span data-ttu-id="0078d-228">每次写入日志消息都会提供一个消息模板。</span><span class="sxs-lookup"><span data-stu-id="0078d-228">Each time you write a log message, you provide a message template.</span></span> <span data-ttu-id="0078d-229">消息模板可以是字符串，也可以包含放置参数值的命名占位符。</span><span class="sxs-lookup"><span data-stu-id="0078d-229">The message template can be a string or it can contain named placeholders into which argument values are placed.</span></span> <span data-ttu-id="0078d-230">该模板不是格式字符串，应对占位符进行命名而不是编号。</span><span class="sxs-lookup"><span data-stu-id="0078d-230">The template isn't a format string, and placeholders should be named, not numbered.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="0078d-231">占位符的顺序（而非其名称）决定了为其提供值的参数。</span><span class="sxs-lookup"><span data-stu-id="0078d-231">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="0078d-232">如果你有以下代码：</span><span class="sxs-lookup"><span data-stu-id="0078d-232">If you have the following code:</span></span>

```csharp
string p1 = "parm1";
string p2 = "parm2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="0078d-233">生成的日志消息如下所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-233">The resulting log message looks like this:</span></span>

```
Parameter values: parm1, parm2
```

<span data-ttu-id="0078d-234">记录框架以这种方式对消息进行格式化，以便日志记录提供程序能实现[语义日志记录（又称结构化日志记录）](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)。</span><span class="sxs-lookup"><span data-stu-id="0078d-234">The logging framework does message formatting in this way to make it possible for logging providers to implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span> <span data-ttu-id="0078d-235">由于传递到日志记录系统的是参数本身（而不仅仅是格式化的消息模板），因此除消息模板外，日志记录提供程序还可将参数值存储为字段。</span><span class="sxs-lookup"><span data-stu-id="0078d-235">Because the arguments themselves are passed to the logging system, not just the formatted message template, logging providers can store the parameter values as fields in addition to the message template.</span></span> <span data-ttu-id="0078d-236">如果将日志输出定向到 Azure 表存储，则记录器方法调用将如下所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-236">If you're directing your log output to Azure Table Storage and your logger method call looks like this:</span></span>

```csharp
_logger.LogInformation("Getting item {ID} at {RequestTime}", id, DateTime.Now);
```

<span data-ttu-id="0078d-237">每个 Azure 表实体都具有 `ID` 和 `RequestTime` 属性，简化了对日志数据的查询。</span><span class="sxs-lookup"><span data-stu-id="0078d-237">Each Azure Table entity can have `ID` and `RequestTime` properties, which simplifies queries on log data.</span></span> <span data-ttu-id="0078d-238">无需分析文本消息的超时，即可找到特定 `RequestTime` 范围内的全部日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-238">You can find all logs within a particular `RequestTime` range without the need to parse the time out of the text message.</span></span>

## <a name="logging-exceptions"></a><span data-ttu-id="0078d-239">日志记录异常</span><span class="sxs-lookup"><span data-stu-id="0078d-239">Logging exceptions</span></span>

<span data-ttu-id="0078d-240">记录器方法有可传入异常的重载，如下方示例所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-240">The logger methods have overloads that let you pass in an exception, as in the following example:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

<span data-ttu-id="0078d-241">不同的提供程序处理异常信息的方式不同。</span><span class="sxs-lookup"><span data-stu-id="0078d-241">Different providers handle the exception information in different ways.</span></span> <span data-ttu-id="0078d-242">以下是上示代码的调试提供程序输出示例。</span><span class="sxs-lookup"><span data-stu-id="0078d-242">Here's an example of Debug provider output from the code shown above.</span></span>

```
TodoApi.Controllers.TodoController:Warning: GetById(036dd898-fb01-47e8-9a65-f92eb73cf924) NOT FOUND

System.Exception: Item not found exception.
 at TodoApi.Controllers.TodoController.GetById(String id) in C:\logging\sample\src\TodoApi\Controllers\TodoController.cs:line 226
```

## <a name="log-filtering"></a><span data-ttu-id="0078d-243">日志筛选</span><span class="sxs-lookup"><span data-stu-id="0078d-243">Log filtering</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="0078d-244">可为特定或所有提供程序和类别指定最低日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-244">You can specify a minimum log level for a specific provider and category or for all providers or all categories.</span></span> <span data-ttu-id="0078d-245">最低级别以下的日志不会传递给该提供程序，因此不会显示或存储它们。</span><span class="sxs-lookup"><span data-stu-id="0078d-245">Any logs below the minimum level aren't passed to that provider, so they don't get displayed or stored.</span></span>

<span data-ttu-id="0078d-246">要禁止显示所有日志，可将 `LogLevel.None` 指定为最低日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-246">If you want to suppress all logs, you can specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="0078d-247">`LogLevel.None` 的整数值为 6，它大于 `LogLevel.Critical` (5)。</span><span class="sxs-lookup"><span data-stu-id="0078d-247">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

### <a name="create-filter-rules-in-configuration"></a><span data-ttu-id="0078d-248">在配置中创建筛选规则</span><span class="sxs-lookup"><span data-stu-id="0078d-248">Create filter rules in configuration</span></span>

<span data-ttu-id="0078d-249">项目模板创建调用 `CreateDefaultBuilder` 的代码，以便为控制台和调试提供程序设置日志记录。</span><span class="sxs-lookup"><span data-stu-id="0078d-249">The project templates create code that calls `CreateDefaultBuilder` to set up logging for the Console and Debug providers.</span></span> <span data-ttu-id="0078d-250">`CreateDefaultBuilder` 方法还使用如下所示的代码，设置日志记录以查找 `Logging` 部分的配置：</span><span class="sxs-lookup"><span data-stu-id="0078d-250">The `CreateDefaultBuilder` method also sets up logging to look for configuration in a `Logging` section, using code like the following:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=15)]

<span data-ttu-id="0078d-251">配置数据按提供程序和类别指定最低日志级别，如下方示例所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-251">The configuration data specifies minimum log levels by provider and category, as in the following example:</span></span>

[!code-json[](index/sample2/appsettings.json)]

<span data-ttu-id="0078d-252">此 JSON 将创建六条筛选规则，一条用于调试提供程序，四条用于控制台提供程序，一条用于所有提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-252">This JSON creates six filter rules, one for the Debug provider, four for the Console provider, and one that applies to all providers.</span></span> <span data-ttu-id="0078d-253">稍后你将了解在创建 `ILogger` 对象后，如何为每个提供程序从上述规则中选择其一。</span><span class="sxs-lookup"><span data-stu-id="0078d-253">You'll see later how just one of these rules is chosen for each provider when an `ILogger` object is created.</span></span>

### <a name="filter-rules-in-code"></a><span data-ttu-id="0078d-254">代码中的筛选规则</span><span class="sxs-lookup"><span data-stu-id="0078d-254">Filter rules in code</span></span>

<span data-ttu-id="0078d-255">可在代码中注册筛选规则，如下方示例所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-255">You can register filter rules in code, as shown in the following example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterInCode&highlight=4-5)]

<span data-ttu-id="0078d-256">第二个 `AddFilter` 使用类型名称来指定调试提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-256">The second `AddFilter` specifies the Debug provider by using its type name.</span></span> <span data-ttu-id="0078d-257">第一个 `AddFilter` 应用于全部提供程序，因为它未指定提供程序类型。</span><span class="sxs-lookup"><span data-stu-id="0078d-257">The first `AddFilter` applies to all providers because it doesn't specify a provider type.</span></span>

### <a name="how-filtering-rules-are-applied"></a><span data-ttu-id="0078d-258">如何应用筛选规则</span><span class="sxs-lookup"><span data-stu-id="0078d-258">How filtering rules are applied</span></span>

<span data-ttu-id="0078d-259">先前示例中显示的配置数据和 `AddFilter` 代码会创建下表所示的规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-259">The configuration data and the `AddFilter` code shown in the preceding examples create the rules shown in the following table.</span></span> <span data-ttu-id="0078d-260">前六条由配置示例创建，后两条由代码示例创建。</span><span class="sxs-lookup"><span data-stu-id="0078d-260">The first six come from the configuration example and the last two come from the code example.</span></span>

| <span data-ttu-id="0078d-261">数字</span><span class="sxs-lookup"><span data-stu-id="0078d-261">Number</span></span> | <span data-ttu-id="0078d-262">提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-262">Provider</span></span>      | <span data-ttu-id="0078d-263">类别的开头为...</span><span class="sxs-lookup"><span data-stu-id="0078d-263">Categories that begin with ...</span></span>          | <span data-ttu-id="0078d-264">最低日志级别</span><span class="sxs-lookup"><span data-stu-id="0078d-264">Minimum log level</span></span> |
| :----: | ------------- | --------------------------------------- | ----------------- |
| <span data-ttu-id="0078d-265">1</span><span class="sxs-lookup"><span data-stu-id="0078d-265">1</span></span>      | <span data-ttu-id="0078d-266">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-266">Debug</span></span>         | <span data-ttu-id="0078d-267">全部类别</span><span class="sxs-lookup"><span data-stu-id="0078d-267">All categories</span></span>                          | <span data-ttu-id="0078d-268">信息</span><span class="sxs-lookup"><span data-stu-id="0078d-268">Information</span></span>       |
| <span data-ttu-id="0078d-269">2</span><span class="sxs-lookup"><span data-stu-id="0078d-269">2</span></span>      | <span data-ttu-id="0078d-270">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-270">Console</span></span>       | <span data-ttu-id="0078d-271">Microsoft.AspNetCore.Mvc.Razor.Internal</span><span class="sxs-lookup"><span data-stu-id="0078d-271">Microsoft.AspNetCore.Mvc.Razor.Internal</span></span> | <span data-ttu-id="0078d-272">警告</span><span class="sxs-lookup"><span data-stu-id="0078d-272">Warning</span></span>           |
| <span data-ttu-id="0078d-273">3</span><span class="sxs-lookup"><span data-stu-id="0078d-273">3</span></span>      | <span data-ttu-id="0078d-274">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-274">Console</span></span>       | <span data-ttu-id="0078d-275">Microsoft.AspNetCore.Mvc.Razor.Razor</span><span class="sxs-lookup"><span data-stu-id="0078d-275">Microsoft.AspNetCore.Mvc.Razor.Razor</span></span>    | <span data-ttu-id="0078d-276">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-276">Debug</span></span>             |
| <span data-ttu-id="0078d-277">4</span><span class="sxs-lookup"><span data-stu-id="0078d-277">4</span></span>      | <span data-ttu-id="0078d-278">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-278">Console</span></span>       | <span data-ttu-id="0078d-279">Microsoft.AspNetCore.Mvc.Razor</span><span class="sxs-lookup"><span data-stu-id="0078d-279">Microsoft.AspNetCore.Mvc.Razor</span></span>          | <span data-ttu-id="0078d-280">Error</span><span class="sxs-lookup"><span data-stu-id="0078d-280">Error</span></span>             |
| <span data-ttu-id="0078d-281">5</span><span class="sxs-lookup"><span data-stu-id="0078d-281">5</span></span>      | <span data-ttu-id="0078d-282">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-282">Console</span></span>       | <span data-ttu-id="0078d-283">全部类别</span><span class="sxs-lookup"><span data-stu-id="0078d-283">All categories</span></span>                          | <span data-ttu-id="0078d-284">信息</span><span class="sxs-lookup"><span data-stu-id="0078d-284">Information</span></span>       |
| <span data-ttu-id="0078d-285">6</span><span class="sxs-lookup"><span data-stu-id="0078d-285">6</span></span>      | <span data-ttu-id="0078d-286">全部提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-286">All providers</span></span> | <span data-ttu-id="0078d-287">全部类别</span><span class="sxs-lookup"><span data-stu-id="0078d-287">All categories</span></span>                          | <span data-ttu-id="0078d-288">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-288">Debug</span></span>             |
| <span data-ttu-id="0078d-289">7</span><span class="sxs-lookup"><span data-stu-id="0078d-289">7</span></span>      | <span data-ttu-id="0078d-290">全部提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-290">All providers</span></span> | <span data-ttu-id="0078d-291">系统</span><span class="sxs-lookup"><span data-stu-id="0078d-291">System</span></span>                                  | <span data-ttu-id="0078d-292">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-292">Debug</span></span>             |
| <span data-ttu-id="0078d-293">8</span><span class="sxs-lookup"><span data-stu-id="0078d-293">8</span></span>      | <span data-ttu-id="0078d-294">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-294">Debug</span></span>         | <span data-ttu-id="0078d-295">Microsoft</span><span class="sxs-lookup"><span data-stu-id="0078d-295">Microsoft</span></span>                               | <span data-ttu-id="0078d-296">跟踪</span><span class="sxs-lookup"><span data-stu-id="0078d-296">Trace</span></span>             |

<span data-ttu-id="0078d-297">创建 `ILogger` 对象来写入日志时，`ILoggerFactory` 对象将从根据提供程序选择一条规则，将其应用于该记录器。</span><span class="sxs-lookup"><span data-stu-id="0078d-297">When you create an `ILogger` object to write logs with, the `ILoggerFactory` object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="0078d-298">将按所选规则筛选该 `ILogger` 对象写入的所有消息。</span><span class="sxs-lookup"><span data-stu-id="0078d-298">All messages written by that `ILogger` object are filtered based on the selected rules.</span></span> <span data-ttu-id="0078d-299">从可用规则中为每个提供程序和类别对选择最具体的规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-299">The most specific rule possible for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="0078d-300">在为给定的类别创建 `ILogger` 时，以下算法将用于每个提供程序：</span><span class="sxs-lookup"><span data-stu-id="0078d-300">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

* <span data-ttu-id="0078d-301">选择匹配提供程序或其别名的所有规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-301">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="0078d-302">如果找不到，则选择具有空提供程序的所有规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-302">If none are found, select all rules with an empty provider.</span></span>
* <span data-ttu-id="0078d-303">根据上一步的结果，选择具有最长匹配类别前缀的规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-303">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="0078d-304">如果找不到，则选择未指定类别的所有规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-304">If none are found, select all rules that don't specify a category.</span></span>
* <span data-ttu-id="0078d-305">如果选择了多条规则，则采用最后一条。</span><span class="sxs-lookup"><span data-stu-id="0078d-305">If multiple rules are selected take the **last** one.</span></span>
* <span data-ttu-id="0078d-306">如果未选择任何规则，则使用 `MinimumLevel`。</span><span class="sxs-lookup"><span data-stu-id="0078d-306">If no rules are selected, use `MinimumLevel`.</span></span>

<span data-ttu-id="0078d-307">例如，假设你拥有上述规则列表，并为类别“Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine”创建了 `ILogger` 对象：</span><span class="sxs-lookup"><span data-stu-id="0078d-307">For example, suppose you have the preceding list of rules and you create an `ILogger` object for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span></span>

* <span data-ttu-id="0078d-308">对于调试提供程序，规则 1、6 和 8 适用。</span><span class="sxs-lookup"><span data-stu-id="0078d-308">For the Debug provider, rules 1, 6, and 8 apply.</span></span> <span data-ttu-id="0078d-309">规则 8 最为具体，因此选择了它。</span><span class="sxs-lookup"><span data-stu-id="0078d-309">Rule 8 is most specific, so that's the one selected.</span></span>
* <span data-ttu-id="0078d-310">对于控制台提供程序，符合的有规则 3、规则 4、规则 5 和规则 6。</span><span class="sxs-lookup"><span data-stu-id="0078d-310">For the Console provider, rules 3, 4, 5, and 6 apply.</span></span> <span data-ttu-id="0078d-311">规则 3 最为具体。</span><span class="sxs-lookup"><span data-stu-id="0078d-311">Rule 3 is most specific.</span></span>

<span data-ttu-id="0078d-312">在使用 `ILogger` 为类别“Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine”创建日志时，`Trace` 及以上级别的日志将发送到调试提供程序，`Debug` 及以上级别的日志将发送到控制台提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-312">When you create logs with an `ILogger` for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine", logs of `Trace` level and above will go to the Debug provider, and logs of `Debug` level and above will go to the Console provider.</span></span>

### <a name="provider-aliases"></a><span data-ttu-id="0078d-313">提供程序别名</span><span class="sxs-lookup"><span data-stu-id="0078d-313">Provider aliases</span></span>

<span data-ttu-id="0078d-314">虽然可以使用类型名称在配置中指定提供程序，但每个提供程序都定义了更短且更易于使用的别名。</span><span class="sxs-lookup"><span data-stu-id="0078d-314">You can use the type name to specify a provider in configuration, but each provider defines a shorter *alias* that's easier to use.</span></span> <span data-ttu-id="0078d-315">对于内置提供程序，请使用以下别名：</span><span class="sxs-lookup"><span data-stu-id="0078d-315">For the built-in providers, use the following aliases:</span></span>

* <span data-ttu-id="0078d-316">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-316">Console</span></span>
* <span data-ttu-id="0078d-317">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-317">Debug</span></span>
* <span data-ttu-id="0078d-318">EventLog</span><span class="sxs-lookup"><span data-stu-id="0078d-318">EventLog</span></span>
* <span data-ttu-id="0078d-319">AzureAppServices</span><span class="sxs-lookup"><span data-stu-id="0078d-319">AzureAppServices</span></span>
* <span data-ttu-id="0078d-320">TraceSource</span><span class="sxs-lookup"><span data-stu-id="0078d-320">TraceSource</span></span>
* <span data-ttu-id="0078d-321">EventSource</span><span class="sxs-lookup"><span data-stu-id="0078d-321">EventSource</span></span>

### <a name="default-minimum-level"></a><span data-ttu-id="0078d-322">默认最低级别</span><span class="sxs-lookup"><span data-stu-id="0078d-322">Default minimum level</span></span>

<span data-ttu-id="0078d-323">仅当配置或代码中的规则对给定提供程序和类别都不适用时，最低级别设置才会生效。</span><span class="sxs-lookup"><span data-stu-id="0078d-323">There's a minimum level setting that takes effect only if no rules from configuration or code apply for a given provider and category.</span></span> <span data-ttu-id="0078d-324">下面的示例演示如何设置最低级别：</span><span class="sxs-lookup"><span data-stu-id="0078d-324">The following example shows how to set the minimum level:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_MinLevel&highlight=3)]

<span data-ttu-id="0078d-325">如果没有明确设置最低级别，则默认值为 `Information`，它表示 `Trace` 和 `Debug` 日志将被忽略。</span><span class="sxs-lookup"><span data-stu-id="0078d-325">If you don't explicitly set the minimum level, the default value is `Information`, which means that `Trace` and `Debug` logs are ignored.</span></span>

### <a name="filter-functions"></a><span data-ttu-id="0078d-326">筛选器函数</span><span class="sxs-lookup"><span data-stu-id="0078d-326">Filter functions</span></span>

<span data-ttu-id="0078d-327">可向筛选器函数写入代码以应用筛选规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-327">You can write code in a filter function to apply filtering rules.</span></span> <span data-ttu-id="0078d-328">对配置或代码没有向其分配规则的所有提供程序和类别调用筛选器函数。</span><span class="sxs-lookup"><span data-stu-id="0078d-328">A filter function is invoked for all providers and categories that don't have rules assigned to them by configuration or code.</span></span> <span data-ttu-id="0078d-329">函数中的代码有权访问提供程序类型、类别和日志级别，以决定是否记录某条消息。</span><span class="sxs-lookup"><span data-stu-id="0078d-329">Code in the function has access to the provider type, category, and log level to decide whether or not a message should be logged.</span></span> <span data-ttu-id="0078d-330">例如:</span><span class="sxs-lookup"><span data-stu-id="0078d-330">For example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterFunction&highlight=5-13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="0078d-331">通过某些日志记录提供程序，可根据日志级别和类别指定何时向存储介质写入日志、何时忽略日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-331">Some logging providers let you specify when logs should be written to a storage medium or ignored based on log level and category.</span></span>

<span data-ttu-id="0078d-332">`AddConsole` 和 `AddDebug` 扩展方法提供允许传入筛选条件的重载。</span><span class="sxs-lookup"><span data-stu-id="0078d-332">The `AddConsole` and `AddDebug` extension methods provide overloads that let you pass in filtering criteria.</span></span> <span data-ttu-id="0078d-333">下列示例代码将使控制台提供程序忽略低于 `Warning` 级别的日志，而使调试提供程序忽略由框架创建的日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-333">The following sample code causes the console provider to ignore logs below `Warning` level, while the Debug provider ignores logs that the framework creates.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_AddConsoleAndDebugWithFilter&highlight=6-7)]

<span data-ttu-id="0078d-334">`AddEventLog` 方法拥有接受 `EventLogSettings` 实例的重载，该实例的 `Filter` 属性中可能包含筛选函数。</span><span class="sxs-lookup"><span data-stu-id="0078d-334">The `AddEventLog` method has an overload that takes an `EventLogSettings` instance, which may contain a filtering function in its `Filter` property.</span></span> <span data-ttu-id="0078d-335">TraceSource 提供程序不提供以上任何重载，因为其日志记录级别和其他参数都以它使用的 `SourceSwitch` 和 `TraceListener` 为依据。</span><span class="sxs-lookup"><span data-stu-id="0078d-335">The TraceSource provider doesn't provide any of those overloads, since its logging level and other parameters are based on the `SourceSwitch` and `TraceListener` it uses.</span></span>

<span data-ttu-id="0078d-336">可以使用 `WithFilter` 扩展方法为所有通过 `ILoggerFactory` 实例注册的提供程序设置筛选规则。</span><span class="sxs-lookup"><span data-stu-id="0078d-336">You can set filtering rules for all providers that are registered with an `ILoggerFactory` instance by using the `WithFilter` extension method.</span></span> <span data-ttu-id="0078d-337">以下示例将（类别以“Microsoft”或“System”开头的）框架日志限制为警告，并在调试级别记录应用日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-337">The example below limits framework logs (category begins with "Microsoft" or "System") to warnings while letting the app log at debug level.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_FactoryFilter&highlight=6-11)]

<span data-ttu-id="0078d-338">要通过筛选来防止写入某个特定类别的所有日志，可将 `LogLevel.None` 指定为该类别的最低日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-338">If you want to use filtering to prevent all logs from being written for a particular category, you can specify `LogLevel.None` as the minimum log level for that category.</span></span> <span data-ttu-id="0078d-339">`LogLevel.None` 的整数值为 6，它大于 `LogLevel.Critical` (5)。</span><span class="sxs-lookup"><span data-stu-id="0078d-339">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="0078d-340">`WithFilter` 扩展方法由 [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet 包提供。</span><span class="sxs-lookup"><span data-stu-id="0078d-340">The `WithFilter` extension method is provided by the [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet package.</span></span> <span data-ttu-id="0078d-341">该方法返回一个新的 `ILoggerFactory` 实例，该实例将筛选传递给注册的所有记录器提供程序的日志消息。</span><span class="sxs-lookup"><span data-stu-id="0078d-341">The method returns a new `ILoggerFactory` instance that will filter the log messages passed to all logger providers registered with it.</span></span> <span data-ttu-id="0078d-342">它不会影响其他任何 `ILoggerFactory` 实例，包括原始 `ILoggerFactory` 实例。</span><span class="sxs-lookup"><span data-stu-id="0078d-342">It doesn't affect any other `ILoggerFactory` instances, including the original `ILoggerFactory` instance.</span></span>

::: moniker-end

## <a name="log-scopes"></a><span data-ttu-id="0078d-343">日志作用域</span><span class="sxs-lookup"><span data-stu-id="0078d-343">Log scopes</span></span>

<span data-ttu-id="0078d-344">可以将逻辑操作集划入范围，从而将相同的数据附加到在此集中创建的每个日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-344">You can group a set of logical operations within a *scope* in order to attach the same data to each log that's created as part of that set.</span></span> <span data-ttu-id="0078d-345">例如，可让处理事务时创建的每个日志都包含事务 ID。</span><span class="sxs-lookup"><span data-stu-id="0078d-345">For example, you might want every log created as part of processing a transaction to include the transaction ID.</span></span>

<span data-ttu-id="0078d-346">范围是由 [ILogger.BeginScope&lt;TState&gt;](/dotnet/api/microsoft.extensions.logging.ilogger.beginscope) 方法返回的 `IDisposable` 类型，持续至释放为止。</span><span class="sxs-lookup"><span data-stu-id="0078d-346">A scope is an `IDisposable` type that's returned by the [ILogger.BeginScope&lt;TState&gt;](/dotnet/api/microsoft.extensions.logging.ilogger.beginscope) method and lasts until it's disposed.</span></span> <span data-ttu-id="0078d-347">要使用作用域，请在 `using` 块中包装记录器调用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-347">You use a scope by wrapping your logger calls in a `using` block, as shown here:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_Scopes&highlight=4-5,13)]

<span data-ttu-id="0078d-348">下列代码为控制台提供程序启用作用域：</span><span class="sxs-lookup"><span data-stu-id="0078d-348">The following code enables scopes for the console provider:</span></span>

::: moniker range="> aspnetcore-2.0"

<span data-ttu-id="0078d-349">Program.cs:</span><span class="sxs-lookup"><span data-stu-id="0078d-349">*Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="0078d-350">要启用基于作用域的日志记录，必须先配置 `IncludeScopes` 控制台记录器选项。</span><span class="sxs-lookup"><span data-stu-id="0078d-350">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span>
>
> <span data-ttu-id="0078d-351">若要了解关配置，请参阅[配置](#configuration)部分。</span><span class="sxs-lookup"><span data-stu-id="0078d-351">For information on configuration, see the [Configuration](#configuration) section.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0078d-352">Program.cs:</span><span class="sxs-lookup"><span data-stu-id="0078d-352">*Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="0078d-353">要启用基于作用域的日志记录，必须先配置 `IncludeScopes` 控制台记录器选项。</span><span class="sxs-lookup"><span data-stu-id="0078d-353">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="0078d-354">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="0078d-354">*Startup.cs*:</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_Scopes&highlight=6)]

::: moniker-end

<span data-ttu-id="0078d-355">每条日志消息都包含作用域内的信息：</span><span class="sxs-lookup"><span data-stu-id="0078d-355">Each log message includes the scoped information:</span></span>

```
info: TodoApi.Controllers.TodoController[1002]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      GetById(0) NOT FOUND
```

## <a name="built-in-logging-providers"></a><span data-ttu-id="0078d-356">内置日志记录提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-356">Built-in logging providers</span></span>

<span data-ttu-id="0078d-357">ASP.NET Core 提供以下提供程序：</span><span class="sxs-lookup"><span data-stu-id="0078d-357">ASP.NET Core ships the following providers:</span></span>

* [<span data-ttu-id="0078d-358">控制台</span><span class="sxs-lookup"><span data-stu-id="0078d-358">Console</span></span>](#console-provider)
* [<span data-ttu-id="0078d-359">调试</span><span class="sxs-lookup"><span data-stu-id="0078d-359">Debug</span></span>](#debug-provider)
* [<span data-ttu-id="0078d-360">EventSource</span><span class="sxs-lookup"><span data-stu-id="0078d-360">EventSource</span></span>](#eventsource-provider)
* [<span data-ttu-id="0078d-361">EventLog</span><span class="sxs-lookup"><span data-stu-id="0078d-361">EventLog</span></span>](#windows-eventlog-provider)
* [<span data-ttu-id="0078d-362">TraceSource</span><span class="sxs-lookup"><span data-stu-id="0078d-362">TraceSource</span></span>](#tracesource-provider)
* [<span data-ttu-id="0078d-363">Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="0078d-363">Azure App Service</span></span>](#azure-app-service-provider)

### <a name="console-provider"></a><span data-ttu-id="0078d-364">控制台提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-364">Console provider</span></span>

<span data-ttu-id="0078d-365">[Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) 提供程序包向控制台发送日志输出。</span><span class="sxs-lookup"><span data-stu-id="0078d-365">The [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) provider package sends log output to the console.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddConsole();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddConsole();
```

<span data-ttu-id="0078d-366">[AddConsole 重载](/dotnet/api/microsoft.extensions.logging.consoleloggerextensions)允许传入一个最低日志级别、一个筛选器函数，以及一个用于指示作用域是否受支持的布尔值。</span><span class="sxs-lookup"><span data-stu-id="0078d-366">[AddConsole overloads](/dotnet/api/microsoft.extensions.logging.consoleloggerextensions) let you pass in an a minimum log level, a filter function, and a boolean that indicates whether scopes are supported.</span></span> <span data-ttu-id="0078d-367">另一个选项是传递 `IConfiguration` 对象，可通过它来指定支持的作用域及日志记录级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-367">Another option is to pass in an `IConfiguration` object, which can specify scopes support and logging levels.</span></span>

<span data-ttu-id="0078d-368">在为生产环境选择控制台提供程序时，请考虑到它将对性能产生重大影响。</span><span class="sxs-lookup"><span data-stu-id="0078d-368">If you are considering the console provider for use in production, be aware that it has a significant impact on performance.</span></span>

<span data-ttu-id="0078d-369">在 Visual Studio 中创建新项目时，`AddConsole` 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="0078d-369">When you create a new project in Visual Studio, the `AddConsole` method looks like this:</span></span>

```csharp
loggerFactory.AddConsole(Configuration.GetSection("Logging"));
```

<span data-ttu-id="0078d-370">此代码引用 appSettings.json 文件的 `Logging` 部分：</span><span class="sxs-lookup"><span data-stu-id="0078d-370">This code refers to the `Logging` section of the *appSettings.json* file:</span></span>

[!code-json[](index/sample//appsettings.json)]

<span data-ttu-id="0078d-371">所显示的设置将框架日志限制为警告，并允许在调试级别记录应用日志，如[日志筛选](#log-filtering)部分所述。</span><span class="sxs-lookup"><span data-stu-id="0078d-371">The settings shown limit framework logs to warnings while allowing the app to log at debug level, as explained in the [Log filtering](#log-filtering) section.</span></span> <span data-ttu-id="0078d-372">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="0078d-372">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

::: moniker-end

### <a name="debug-provider"></a><span data-ttu-id="0078d-373">调试提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-373">Debug provider</span></span>

<span data-ttu-id="0078d-374">[Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) 提供程序包使用 [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) 类（`Debug.WriteLine` 方法调用）来写入日志输出。</span><span class="sxs-lookup"><span data-stu-id="0078d-374">The [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) provider package writes log output by using the [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) class (`Debug.WriteLine` method calls).</span></span>

<span data-ttu-id="0078d-375">在 Linux 中，此提供程序将日志写入 /var/log/message。</span><span class="sxs-lookup"><span data-stu-id="0078d-375">On Linux, this provider writes logs to */var/log/message*.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddDebug();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddDebug();
```

<span data-ttu-id="0078d-376">[AddDebug 重载](/dotnet/api/microsoft.extensions.logging.debugloggerfactoryextensions)允许传入最低日志级别或筛选器函数。</span><span class="sxs-lookup"><span data-stu-id="0078d-376">[AddDebug overloads](/dotnet/api/microsoft.extensions.logging.debugloggerfactoryextensions) let you pass in a minimum log level or a filter function.</span></span>

::: moniker-end

### <a name="eventsource-provider"></a><span data-ttu-id="0078d-377">EventSource 提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-377">EventSource provider</span></span>

<span data-ttu-id="0078d-378">对于面向 ASP.NET Core 1.1.0 或更高版本的应用，[Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) 提供程序包可实现事件跟踪。</span><span class="sxs-lookup"><span data-stu-id="0078d-378">For apps that target ASP.NET Core 1.1.0 or later, the [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) provider package can implement event tracing.</span></span> <span data-ttu-id="0078d-379">在 Windows 中，它使用 [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803)。</span><span class="sxs-lookup"><span data-stu-id="0078d-379">On Windows, it uses [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span></span> <span data-ttu-id="0078d-380">提供程序可跨平台使用，但尚无支持 Linux 或 macOS 的事件集合和显示工具。</span><span class="sxs-lookup"><span data-stu-id="0078d-380">The provider is cross-platform, but there are no event collection and display tools yet for Linux or macOS.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddEventSourceLogger();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddEventSourceLogger();
```

::: moniker-end

<span data-ttu-id="0078d-381">可使用 [PerfView 实用工具](https://github.com/Microsoft/perfview)收集和查看日志。</span><span class="sxs-lookup"><span data-stu-id="0078d-381">A good way to collect and view logs is to use the [PerfView utility](https://github.com/Microsoft/perfview).</span></span> <span data-ttu-id="0078d-382">虽然其他工具也可以查看 ETW 日志，但在处理由 ASP.NET 发出的 ETW 事件时，使用 PerfView 能获得最佳体验。</span><span class="sxs-lookup"><span data-stu-id="0078d-382">There are other tools for viewing ETW logs, but PerfView provides the best experience for working with the ETW events emitted by ASP.NET.</span></span>

<span data-ttu-id="0078d-383">要将 PerfView 配置为收集此提供程序记录的事件，请向 Additional Providers 列表添加字符串 `*Microsoft-Extensions-Logging`。</span><span class="sxs-lookup"><span data-stu-id="0078d-383">To configure PerfView for collecting events logged by this provider, add the string `*Microsoft-Extensions-Logging` to the **Additional Providers** list.</span></span> <span data-ttu-id="0078d-384">（请勿遗漏字符串起始处的星号。）</span><span class="sxs-lookup"><span data-stu-id="0078d-384">(Don't miss the asterisk at the start of the string.)</span></span>

![其他 Perfview 提供程序](index/_static/perfview-additional-providers.png)

### <a name="windows-eventlog-provider"></a><span data-ttu-id="0078d-386">Windows EventLog 提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-386">Windows EventLog provider</span></span>

<span data-ttu-id="0078d-387">[Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) 提供程序包向 Windows 事件日志发送日志输出。</span><span class="sxs-lookup"><span data-stu-id="0078d-387">The [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) provider package sends log output to the Windows Event Log.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddEventLog();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddEventLog();
```

<span data-ttu-id="0078d-388">[AddEventLog 重载](/dotnet/api/microsoft.extensions.logging.eventloggerfactoryextensions)允许传入 `EventLogSettings` 或最低日志级别。</span><span class="sxs-lookup"><span data-stu-id="0078d-388">[AddEventLog overloads](/dotnet/api/microsoft.extensions.logging.eventloggerfactoryextensions) let you pass in `EventLogSettings` or a minimum log level.</span></span>

::: moniker-end

### <a name="tracesource-provider"></a><span data-ttu-id="0078d-389">TraceSource 提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-389">TraceSource provider</span></span>

<span data-ttu-id="0078d-390">[Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) 提供程序包使用 [System.Diagnostics.TraceSource](/dotnet/api/system.diagnostics.tracesource) 库和提供程序。</span><span class="sxs-lookup"><span data-stu-id="0078d-390">The [Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) provider package uses the [System.Diagnostics.TraceSource](/dotnet/api/system.diagnostics.tracesource) libraries and providers.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddTraceSource(sourceSwitchName);
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddTraceSource(sourceSwitchName);
```

::: moniker-end

<span data-ttu-id="0078d-391">[AddTraceSource 重载](/dotnet/api/microsoft.extensions.logging.tracesourcefactoryextensions) 允许传入资源开关和跟踪侦听器。</span><span class="sxs-lookup"><span data-stu-id="0078d-391">[AddTraceSource overloads](/dotnet/api/microsoft.extensions.logging.tracesourcefactoryextensions) let you pass in a source switch and a trace listener.</span></span>

<span data-ttu-id="0078d-392">要使用此提供程序，应用程序必须在 .NET Framework（而非 .NET Core）上运行。</span><span class="sxs-lookup"><span data-stu-id="0078d-392">To use this provider, an application has to run on the .NET Framework (rather than .NET Core).</span></span> <span data-ttu-id="0078d-393">使用提供程序，可以将消息路由到多个[侦听器](/dotnet/framework/debug-trace-profile/trace-listeners)，例如示例应用程序中使用的 [TextWriterTraceListener](/dotnet/api/system.diagnostics.textwritertracelistenerr)。</span><span class="sxs-lookup"><span data-stu-id="0078d-393">The provider lets you route messages to a variety of [listeners](/dotnet/framework/debug-trace-profile/trace-listeners), such as the [TextWriterTraceListener](/dotnet/api/system.diagnostics.textwritertracelistenerr) used in the sample application.</span></span>

<span data-ttu-id="0078d-394">以下示例配置了 `TraceSource` 提供程序，用于向控制台窗口记录 `Warning` 和更高级别的消息。</span><span class="sxs-lookup"><span data-stu-id="0078d-394">The following example configures a `TraceSource` provider that logs `Warning` and higher messages to the console window.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_TraceSource&highlight=9-12)]

### <a name="azure-app-service-provider"></a><span data-ttu-id="0078d-395">Azure 应用服务提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-395">Azure App Service provider</span></span>

<span data-ttu-id="0078d-396">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) 提供程序包将日志写入 Azure App Service 应用的文件系统，以及 Azure 存储帐户中的 [blob 存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage)。</span><span class="sxs-lookup"><span data-stu-id="0078d-396">The [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) provider package writes logs to text files in an Azure App Service app's file system and to [blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) in an Azure Storage account.</span></span> <span data-ttu-id="0078d-397">面向 .NET Core 1.1 或更高版本的应用可使用该提供程序包。</span><span class="sxs-lookup"><span data-stu-id="0078d-397">The provider package is available for apps targeting .NET Core 1.1 or later.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="0078d-398">如果面向 .NET Core，请注意以下几点：</span><span class="sxs-lookup"><span data-stu-id="0078d-398">If targeting .NET Core, note the following points:</span></span>

* <span data-ttu-id="0078d-399">提供程序包包括在 ASP.NET Core [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage) 中，但不包括在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中。</span><span class="sxs-lookup"><span data-stu-id="0078d-399">The provider package is included in the ASP.NET Core [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) but not in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>
* <span data-ttu-id="0078d-400">请勿显示调用 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)</span><span class="sxs-lookup"><span data-stu-id="0078d-400">Don't explicitly call [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics).</span></span> <span data-ttu-id="0078d-401">将应用部署到 Azure 应用服务时，会自动使提供程序对应用可用。</span><span class="sxs-lookup"><span data-stu-id="0078d-401">The provider is automatically made available to the app when the app is deployed to Azure App Service.</span></span>

<span data-ttu-id="0078d-402">如果面向 .NET Framework 或引用 `Microsoft.AspNetCore.App` 元包，请向项目添加提供程序包。</span><span class="sxs-lookup"><span data-stu-id="0078d-402">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, add the provider package to the project.</span></span> <span data-ttu-id="0078d-403">在 [ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory) 实例上调用 `AddAzureWebAppDiagnostics`：</span><span class="sxs-lookup"><span data-stu-id="0078d-403">Invoke `AddAzureWebAppDiagnostics` on an [ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory) instance:</span></span>

```csharp
logging.AddAzureWebAppDiagnostics();
```

::: moniker-end

::: moniker range="= aspnetcore-1.1"

```csharp
loggerFactory.AddAzureWebAppDiagnostics();
```

::: moniker-end

<span data-ttu-id="0078d-404">[AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) 重载允许传入 [AzureAppServicesDiagnosticsSettings](/dotnet/api/microsoft.extensions.logging.azureappservices.azureappservicesdiagnosticssettings)，可用它替代默认设置，例如日志记录输出模板、blob 名称和文件大小限制等。</span><span class="sxs-lookup"><span data-stu-id="0078d-404">An [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) overload lets you pass in [AzureAppServicesDiagnosticsSettings](/dotnet/api/microsoft.extensions.logging.azureappservices.azureappservicesdiagnosticssettings) with which you can override default settings, such as the logging output template, blob name, and file size limit.</span></span> <span data-ttu-id="0078d-405">（输出模板是应用于所有日志的消息模板，其优先级高于调用 `ILogger` 方法时提供的模板。）</span><span class="sxs-lookup"><span data-stu-id="0078d-405">(*Output template* is a message template that's applied to all logs on top of the one that you provide when you call an `ILogger` method.)</span></span>

<span data-ttu-id="0078d-406">在部署 App Service 应用时，应用将遵循 Azure 门户中 App Service 页下[诊断日志](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag)部分的设置。</span><span class="sxs-lookup"><span data-stu-id="0078d-406">When you deploy to an App Service app, the app honors the settings in the [Diagnostic Logs](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) section of the **App Service** page of the Azure portal.</span></span> <span data-ttu-id="0078d-407">更新这些设置后，更改会立即生效，无需重新启动或重新部署应用。</span><span class="sxs-lookup"><span data-stu-id="0078d-407">When these settings are updated, the changes take effect immediately without requiring a restart or redeployment of the app.</span></span>

![Azure 日志记录设置](index/_static/azure-logging-settings.png)

<span data-ttu-id="0078d-409">日志文件的默认位置是 D:\\home\\LogFiles\\Application 文件夹，默认文件名为 diagnostics-yyyymmdd.txt。</span><span class="sxs-lookup"><span data-stu-id="0078d-409">The default location for log files is in the *D:\\home\\LogFiles\\Application* folder, and the default file name is *diagnostics-yyyymmdd.txt*.</span></span> <span data-ttu-id="0078d-410">默认文件大小上限为 10 MB，默认最大保留文件数为 2。</span><span class="sxs-lookup"><span data-stu-id="0078d-410">The default file size limit is 10 MB, and the default maximum number of files retained is 2.</span></span> <span data-ttu-id="0078d-411">默认 blob 名为 {app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt。</span><span class="sxs-lookup"><span data-stu-id="0078d-411">The default blob name is *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span></span> <span data-ttu-id="0078d-412">有关默认行为的详细信息，请参阅 [AzureAppServicesDiagnosticsSettings](/dotnet/api/microsoft.extensions.logging.azureappservices.azureappservicesdiagnosticssettings)。</span><span class="sxs-lookup"><span data-stu-id="0078d-412">For more information about default behavior, see [AzureAppServicesDiagnosticsSettings](/dotnet/api/microsoft.extensions.logging.azureappservices.azureappservicesdiagnosticssettings).</span></span>

<span data-ttu-id="0078d-413">该提供程序仅当项目在 Azure 环境中运行时有效。</span><span class="sxs-lookup"><span data-stu-id="0078d-413">The provider only works when the project runs in the Azure environment.</span></span> <span data-ttu-id="0078d-414">项目在本地运行时，该提供程序无效 &mdash; 它不会写入本地文件或 blob 的本地开发存储。</span><span class="sxs-lookup"><span data-stu-id="0078d-414">It has no effect when the project is run locally&mdash;it doesn't write to local files or local development storage for blobs.</span></span>

## <a name="third-party-logging-providers"></a><span data-ttu-id="0078d-415">第三方日志记录提供程序</span><span class="sxs-lookup"><span data-stu-id="0078d-415">Third-party logging providers</span></span>

<span data-ttu-id="0078d-416">适用于 ASP.NET Core 的第三方日志记录框架：</span><span class="sxs-lookup"><span data-stu-id="0078d-416">Third-party logging frameworks that work with ASP.NET Core:</span></span>

* <span data-ttu-id="0078d-417">[elmah.io](https://elmah.io/)（[GitHub 存储库](https://github.com/elmahio/Elmah.Io.Extensions.Logging)）</span><span class="sxs-lookup"><span data-stu-id="0078d-417">[elmah.io](https://elmah.io/) ([GitHub repo](https://github.com/elmahio/Elmah.Io.Extensions.Logging))</span></span>
* <span data-ttu-id="0078d-418">[Gelf](http://docs.graylog.org/en/2.3/pages/gelf.html)（[GitHub 存储库](https://github.com/mattwcole/gelf-extensions-logging)）</span><span class="sxs-lookup"><span data-stu-id="0078d-418">[Gelf](http://docs.graylog.org/en/2.3/pages/gelf.html) ([GitHub repo](https://github.com/mattwcole/gelf-extensions-logging))</span></span>
* <span data-ttu-id="0078d-419">[JSNLog](http://jsnlog.com/)（[GitHub 存储库](https://github.com/mperdeck/jsnlog)）</span><span class="sxs-lookup"><span data-stu-id="0078d-419">[JSNLog](http://jsnlog.com/) ([GitHub repo](https://github.com/mperdeck/jsnlog))</span></span>
* <span data-ttu-id="0078d-420">[Loggr](http://loggr.net/)（[GitHub 存储库](https://github.com/imobile3/Loggr.Extensions.Logging)）</span><span class="sxs-lookup"><span data-stu-id="0078d-420">[Loggr](http://loggr.net/) ([GitHub repo](https://github.com/imobile3/Loggr.Extensions.Logging))</span></span>
* <span data-ttu-id="0078d-421">[NLog](http://nlog-project.org/)（[GitHub 存储库](https://github.com/NLog/NLog.Extensions.Logging)）</span><span class="sxs-lookup"><span data-stu-id="0078d-421">[NLog](http://nlog-project.org/) ([GitHub repo](https://github.com/NLog/NLog.Extensions.Logging))</span></span>
* <span data-ttu-id="0078d-422">[Serilog](https://serilog.net/)（[GitHub 存储库](https://github.com/serilog/serilog-extensions-logging)）</span><span class="sxs-lookup"><span data-stu-id="0078d-422">[Serilog](https://serilog.net/) ([GitHub repo](https://github.com/serilog/serilog-extensions-logging))</span></span>

<span data-ttu-id="0078d-423">某些第三方框架可以执行[语义日志记录（又称结构化日志记录）](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)。</span><span class="sxs-lookup"><span data-stu-id="0078d-423">Some third-party frameworks can perform [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="0078d-424">使用第三方框架类似于使用以下内置提供程序之一：</span><span class="sxs-lookup"><span data-stu-id="0078d-424">Using a third-party framework is similar to using one of the built-in providers:</span></span>

1. <span data-ttu-id="0078d-425">将 NuGet 包添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="0078d-425">Add a NuGet package to your project.</span></span>
1. <span data-ttu-id="0078d-426">在 `ILoggerFactory` 上调用扩展方法。</span><span class="sxs-lookup"><span data-stu-id="0078d-426">Call an extension method on `ILoggerFactory`.</span></span>

<span data-ttu-id="0078d-427">有关详细信息，请参阅各框架的相关文档。</span><span class="sxs-lookup"><span data-stu-id="0078d-427">For more information, see each framework's documentation.</span></span>

## <a name="azure-log-streaming"></a><span data-ttu-id="0078d-428">Azure 日志流式处理</span><span class="sxs-lookup"><span data-stu-id="0078d-428">Azure log streaming</span></span>

<span data-ttu-id="0078d-429">通过 Azure 日志流式处理，可从以下位置实时查看日志活动：</span><span class="sxs-lookup"><span data-stu-id="0078d-429">Azure log streaming enables you to view log activity in real time from:</span></span>

* <span data-ttu-id="0078d-430">应用程序服务器</span><span class="sxs-lookup"><span data-stu-id="0078d-430">The application server</span></span>
* <span data-ttu-id="0078d-431">Web 服务器</span><span class="sxs-lookup"><span data-stu-id="0078d-431">The web server</span></span>
* <span data-ttu-id="0078d-432">请求跟踪失败</span><span class="sxs-lookup"><span data-stu-id="0078d-432">Failed request tracing</span></span>

<span data-ttu-id="0078d-433">要配置 Azure 日志流式处理，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0078d-433">To configure Azure log streaming:</span></span>

* <span data-ttu-id="0078d-434">从应用程序的门户页导航到“诊断日志”页</span><span class="sxs-lookup"><span data-stu-id="0078d-434">Navigate to the **Diagnostics Logs** page from your application's portal page</span></span>
* <span data-ttu-id="0078d-435">将“应用程序日志记录 (Filesystem)”设置为启用。</span><span class="sxs-lookup"><span data-stu-id="0078d-435">Set **Application Logging (Filesystem)** to on.</span></span>

![Azure 门户诊断日志页](index/_static/azure-diagnostic-logs.png)

<span data-ttu-id="0078d-437">导航到“日志流式处理”页，查看应用程序消息。</span><span class="sxs-lookup"><span data-stu-id="0078d-437">Navigate to the **Log Streaming** page to view application messages.</span></span> <span data-ttu-id="0078d-438">它们由应用程序通过 `ILogger` 接口记录。</span><span class="sxs-lookup"><span data-stu-id="0078d-438">They're logged by application through the `ILogger` interface.</span></span>

![Azure 门户应用程序日志流式处理](index/_static/azure-log-streaming.png)

## <a name="azure-application-insights-trace-logging"></a><span data-ttu-id="0078d-440">Azure Application Insights 跟踪日志记录</span><span class="sxs-lookup"><span data-stu-id="0078d-440">Azure Application Insights trace logging</span></span>

<span data-ttu-id="0078d-441">[Application Insights](https://azure.microsoft.com/services/application-insights/) SDK 可从通过 ASP.NET Core日志记录基础结构生成的日志中收集跟踪遥测数据。</span><span class="sxs-lookup"><span data-stu-id="0078d-441">The [Application Insights](https://azure.microsoft.com/services/application-insights/) SDK is capable of collecting trace telemetry from logs generated via the ASP.NET Core logging infrastructure.</span></span> <span data-ttu-id="0078d-442">有关详细信息，请参阅 [Application Insights for ASP.NET Core](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-core) 和 [Microsoft/ApplicationInsights-aspnetcore Wiki：日志记录](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Logging)。</span><span class="sxs-lookup"><span data-stu-id="0078d-442">For more information, see [Application Insights for ASP.NET Core](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-core) and [Microsoft/ApplicationInsights-aspnetcore Wiki: Logging](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Logging).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0078d-443">其他资源</span><span class="sxs-lookup"><span data-stu-id="0078d-443">Additional resources</span></span>

* <xref:fundamentals/logging/loggermessage>
