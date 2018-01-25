---
title: "在 ASP.NET Core 检测与更改令牌更改"
author: guardrex
description: "了解如何使用更改令牌来跟踪更改。"
manager: wpickett
ms.author: riande
ms.date: 11/10/2017
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/primitives/change-tokens
ms.openlocfilehash: 94bf356fcbfab3930804485c1b65e4a0f4c52b8e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="detect-changes-with-change-tokens-in-aspnet-core"></a><span data-ttu-id="1c292-103">在 ASP.NET Core 检测与更改令牌更改</span><span class="sxs-lookup"><span data-stu-id="1c292-103">Detect changes with change tokens in ASP.NET Core</span></span>

<span data-ttu-id="1c292-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="1c292-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="1c292-105">A*更改令牌*是用于跟踪更改的通用、 低级别构造块。</span><span class="sxs-lookup"><span data-stu-id="1c292-105">A *change token* is a general-purpose, low-level building block used to track changes.</span></span>

<span data-ttu-id="1c292-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/primitives/change-tokens/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="1c292-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/primitives/change-tokens/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="ichangetoken-interface"></a><span data-ttu-id="1c292-107">IChangeToken 接口</span><span class="sxs-lookup"><span data-stu-id="1c292-107">IChangeToken interface</span></span>

<span data-ttu-id="1c292-108">[IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken)传播已发生更改的通知。</span><span class="sxs-lookup"><span data-stu-id="1c292-108">[IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken) propagates notifications that a change has occurred.</span></span> <span data-ttu-id="1c292-109">`IChangeToken`驻留在[Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives)命名空间。</span><span class="sxs-lookup"><span data-stu-id="1c292-109">`IChangeToken` resides in the [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) namespace.</span></span> <span data-ttu-id="1c292-110">不使用的应用程序[Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage，引用[Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/)项目文件中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c292-110">For apps that don't use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, reference the [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) NuGet package in the project file.</span></span>

<span data-ttu-id="1c292-111">`IChangeToken`具有两个属性：</span><span class="sxs-lookup"><span data-stu-id="1c292-111">`IChangeToken` has two properties:</span></span>

* <span data-ttu-id="1c292-112">[ActiveChangedCallbacks](/dotnet/api/microsoft.extensions.primitives.ichangetoken.activechangecallbacks)指示是否令牌主动引发回调。</span><span class="sxs-lookup"><span data-stu-id="1c292-112">[ActiveChangedCallbacks](/dotnet/api/microsoft.extensions.primitives.ichangetoken.activechangecallbacks) indicate if the token proactively raises callbacks.</span></span> <span data-ttu-id="1c292-113">如果`ActiveChangedCallbacks`设置为`false`，永远不会调用的回调，并且应用程序必须轮询`HasChanged`的更改。</span><span class="sxs-lookup"><span data-stu-id="1c292-113">If `ActiveChangedCallbacks` is set to `false`, a callback is never called, and the app must poll `HasChanged` for changes.</span></span> <span data-ttu-id="1c292-114">还有可能适用于令牌，如果未发生任何更改或释放或禁用基础的更改侦听器永远不会取消。</span><span class="sxs-lookup"><span data-stu-id="1c292-114">It's also possible for a token to never be cancelled if no changes occur or the underlying change listener is disposed or disabled.</span></span>
* <span data-ttu-id="1c292-115">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged)获取一个值，该值指示是否发生了更改。</span><span class="sxs-lookup"><span data-stu-id="1c292-115">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged) gets a value that indicates if a change has occurred.</span></span>

<span data-ttu-id="1c292-116">此接口具有一个方法， [RegisterChangeCallback (操作&lt;对象&gt;，对象)](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback)，这会注册令牌已发生更改时调用的回调。</span><span class="sxs-lookup"><span data-stu-id="1c292-116">The interface has one method, [RegisterChangeCallback(Action&lt;Object&gt;, Object)](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback), which registers a callback that's invoked when the token has changed.</span></span> <span data-ttu-id="1c292-117">`HasChanged`调用回调之前，必须先设置。</span><span class="sxs-lookup"><span data-stu-id="1c292-117">`HasChanged` must be set before the callback is invoked.</span></span>

## <a name="changetoken-class"></a><span data-ttu-id="1c292-118">ChangeToken 类</span><span class="sxs-lookup"><span data-stu-id="1c292-118">ChangeToken class</span></span>

<span data-ttu-id="1c292-119">`ChangeToken`是静态的类，用于传播通知已发生更改。</span><span class="sxs-lookup"><span data-stu-id="1c292-119">`ChangeToken` is a static class used to propagate notifications that a change has occurred.</span></span> <span data-ttu-id="1c292-120">`ChangeToken`驻留在[Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives)命名空间。</span><span class="sxs-lookup"><span data-stu-id="1c292-120">`ChangeToken` resides in the [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) namespace.</span></span> <span data-ttu-id="1c292-121">不使用的应用程序[Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage，引用[Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/)项目文件中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c292-121">For apps that don't use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, reference the [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) NuGet package in the project file.</span></span>

<span data-ttu-id="1c292-122">`ChangeToken` [OnChange (Func&lt;IChangeToken&gt;，操作)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action_)方法寄存器`Action`调用令牌发生更改时：</span><span class="sxs-lookup"><span data-stu-id="1c292-122">The `ChangeToken` [OnChange(Func&lt;IChangeToken&gt;, Action)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action_) method registers an `Action` to call whenever the token changes:</span></span>
* <span data-ttu-id="1c292-123">`Func<IChangeToken>`生成令牌。</span><span class="sxs-lookup"><span data-stu-id="1c292-123">`Func<IChangeToken>` produces the token.</span></span>
* <span data-ttu-id="1c292-124">`Action`令牌更改时调用。</span><span class="sxs-lookup"><span data-stu-id="1c292-124">`Action` is called when the token changes.</span></span>

<span data-ttu-id="1c292-125">`ChangeToken`具有[OnChange&lt;TState&gt;(Func&lt;IChangeToken&gt;，操作&lt;TState&gt;，TState)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange__1_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action___0____0_)重载采用额外`TState`参数传递到令牌使用者`Action`。</span><span class="sxs-lookup"><span data-stu-id="1c292-125">`ChangeToken` has an [OnChange&lt;TState&gt;(Func&lt;IChangeToken&gt;, Action&lt;TState&gt;, TState)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange__1_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action___0____0_) overload that takes an additional `TState` parameter that's passed into the token consumer `Action`.</span></span>

<span data-ttu-id="1c292-126">`OnChange`返回[IDisposable](/dotnet/api/system.idisposable)。</span><span class="sxs-lookup"><span data-stu-id="1c292-126">`OnChange` returns an [IDisposable](/dotnet/api/system.idisposable).</span></span> <span data-ttu-id="1c292-127">调用[释放](/dotnet/api/system.idisposable.dispose)停止侦听做进一步更改中的令牌，释放标记的资源。</span><span class="sxs-lookup"><span data-stu-id="1c292-127">Calling [Dispose](/dotnet/api/system.idisposable.dispose) stops the token from listening for further changes and releases the token's resources.</span></span>

## <a name="example-uses-of-change-tokens-in-aspnet-core"></a><span data-ttu-id="1c292-128">ASP.NET 核心中的更改标记的示例使用</span><span class="sxs-lookup"><span data-stu-id="1c292-128">Example uses of change tokens in ASP.NET Core</span></span>

<span data-ttu-id="1c292-129">更改令牌使用 ASP.NET 核心监视对对象的更改的突出方面：</span><span class="sxs-lookup"><span data-stu-id="1c292-129">Change tokens are used in prominent areas of ASP.NET Core monitoring changes to objects:</span></span>

* <span data-ttu-id="1c292-130">用于监视更改的文件， [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)的[监视](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch)方法创建`IChangeToken`指定的文件或要监视的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c292-130">For monitoring changes to files, [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)'s [Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) method creates an `IChangeToken` for the specified files or folder to watch.</span></span>
* <span data-ttu-id="1c292-131">`IChangeToken`令牌可以添加到要触发更改的缓存逐出缓存项。</span><span class="sxs-lookup"><span data-stu-id="1c292-131">`IChangeToken` tokens can be added to cache entries to trigger cache evictions on change.</span></span>
* <span data-ttu-id="1c292-132">有关`TOptions`将默认值更改[OptionsMonitor](/dotnet/api/microsoft.extensions.options.optionsmonitor-1)实现[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1)具有一个接受一个或多个重载[IOptionsChangeTokenSource](/dotnet/api/microsoft.extensions.options.ioptionschangetokensource-1)实例。</span><span class="sxs-lookup"><span data-stu-id="1c292-132">For `TOptions` changes, the default [OptionsMonitor](/dotnet/api/microsoft.extensions.options.optionsmonitor-1) implementation of [IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) has an overload that accepts one or more [IOptionsChangeTokenSource](/dotnet/api/microsoft.extensions.options.ioptionschangetokensource-1) instances.</span></span> <span data-ttu-id="1c292-133">每个实例返回`IChangeToken`跟踪选项更改用于注册更改通知回调。</span><span class="sxs-lookup"><span data-stu-id="1c292-133">Each instance returns an `IChangeToken` to register a change notification callback for tracking options changes.</span></span>

## <a name="monitoring-for-configuration-changes"></a><span data-ttu-id="1c292-134">监视配置更改</span><span class="sxs-lookup"><span data-stu-id="1c292-134">Monitoring for configuration changes</span></span>

<span data-ttu-id="1c292-135">默认情况下，使用 ASP.NET Core 模板[JSON 配置文件](xref:fundamentals/configuration/index#json-configuration)(*appsettings.json*， *appsettings。Development.json*，和*appsettings。Production.json*) 来加载应用程序配置设置。</span><span class="sxs-lookup"><span data-stu-id="1c292-135">By default, ASP.NET Core templates use [JSON configuration files](xref:fundamentals/configuration/index#json-configuration) (*appsettings.json*, *appsettings.Development.json*, and *appsettings.Production.json*) to load app configuration settings.</span></span>

<span data-ttu-id="1c292-136">这些文件被配置使用[AddJsonFile （IConfigurationBuilder、 字符串、 布尔值、 布尔值）](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions.addjsonfile?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_JsonConfigurationExtensions_AddJsonFile_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_System_Boolean_System_Boolean_)上的扩展方法[ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder)接受`reloadOnChange`参数 (ASP.NET核心 1.1 和更高版本）。</span><span class="sxs-lookup"><span data-stu-id="1c292-136">These files are configured using the [AddJsonFile(IConfigurationBuilder, String, Boolean, Boolean)](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions.addjsonfile?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_JsonConfigurationExtensions_AddJsonFile_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_System_Boolean_System_Boolean_) extension method on [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder) that accepts a `reloadOnChange` parameter (ASP.NET Core 1.1 and later).</span></span> <span data-ttu-id="1c292-137">`reloadOnChange`指示是否在文件更改，应重新加载配置。</span><span class="sxs-lookup"><span data-stu-id="1c292-137">`reloadOnChange` indicates if configuration should be reloaded on file changes.</span></span> <span data-ttu-id="1c292-138">请参阅此设置在[WebHost](/dotnet/api/microsoft.aspnetcore.webhost)便捷方法[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) ([引用源](https://github.com/aspnet/MetaPackages/blob/rel/2.0.3/src/Microsoft.AspNetCore/WebHost.cs#L152-L193)):</span><span class="sxs-lookup"><span data-stu-id="1c292-138">See this setting in the [WebHost](/dotnet/api/microsoft.aspnetcore.webhost) convenience method [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) ([reference source](https://github.com/aspnet/MetaPackages/blob/rel/2.0.3/src/Microsoft.AspNetCore/WebHost.cs#L152-L193)):</span></span>

```csharp
config.AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
      .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, reloadOnChange: true);
```

<span data-ttu-id="1c292-139">基于文件的配置由[FileConfigurationSource](/dotnet/api/microsoft.extensions.configuration.fileconfigurationsource)。</span><span class="sxs-lookup"><span data-stu-id="1c292-139">File-based configuration is represented by [FileConfigurationSource](/dotnet/api/microsoft.extensions.configuration.fileconfigurationsource).</span></span> <span data-ttu-id="1c292-140">`FileConfigurationSource`使用[IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) ([引用源](https://github.com/aspnet/FileSystem/blob/patch/2.0.1/src/Microsoft.Extensions.FileProviders.Abstractions/IFileProvider.cs)) 若要监视的文件。</span><span class="sxs-lookup"><span data-stu-id="1c292-140">`FileConfigurationSource` uses [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) ([reference source](https://github.com/aspnet/FileSystem/blob/patch/2.0.1/src/Microsoft.Extensions.FileProviders.Abstractions/IFileProvider.cs)) to monitor files.</span></span>

<span data-ttu-id="1c292-141">默认情况下，`IFileMonitor`由[PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) ([引用源](https://github.com/aspnet/Configuration/blob/patch/2.0.1/src/Microsoft.Extensions.Configuration.FileExtensions/FileConfigurationSource.cs#L82))，它使用[FileSystemWatcher](/dotnet/api/system.io.filesystemwatcher)监视配置文件更改。</span><span class="sxs-lookup"><span data-stu-id="1c292-141">By default, the `IFileMonitor` is provided by a [PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) ([reference source](https://github.com/aspnet/Configuration/blob/patch/2.0.1/src/Microsoft.Extensions.Configuration.FileExtensions/FileConfigurationSource.cs#L82)), which uses [FileSystemWatcher](/dotnet/api/system.io.filesystemwatcher) to monitor for configuration file changes.</span></span>

<span data-ttu-id="1c292-142">示例应用程序演示了用于监视配置更改的两个实现。</span><span class="sxs-lookup"><span data-stu-id="1c292-142">The sample app demonstrates two implementations for monitoring configuration changes.</span></span> <span data-ttu-id="1c292-143">如果任一*appsettings.json*环境版本的文件或文件更改，每个实现将执行自定义代码。</span><span class="sxs-lookup"><span data-stu-id="1c292-143">If either the *appsettings.json* file changes or the Environment version of the file changes, each implementation executes custom code.</span></span> <span data-ttu-id="1c292-144">示例应用程序将消息写入控制台。</span><span class="sxs-lookup"><span data-stu-id="1c292-144">The sample app writes a message to the console.</span></span>

<span data-ttu-id="1c292-145">配置文件的`FileSystemWatcher`可以触发单个配置文件更改的多个令牌回调。</span><span class="sxs-lookup"><span data-stu-id="1c292-145">A configuration file's `FileSystemWatcher` can trigger multiple token callbacks for a single configuration file change.</span></span> <span data-ttu-id="1c292-146">示例的实现防止此问题，通过检查配置文件上的文件哈希值。</span><span class="sxs-lookup"><span data-stu-id="1c292-146">The sample's implementation guards against this problem by checking file hashes on the configuration files.</span></span> <span data-ttu-id="1c292-147">检查文件哈希值可确保在运行的自定义代码之前至少一个配置文件已更改。</span><span class="sxs-lookup"><span data-stu-id="1c292-147">Checking file hashes ensures that at least one of the configuration files has changed before running the custom code.</span></span> <span data-ttu-id="1c292-148">此示例使用 SHA1 哈希文件 (*Utilities/Utilities.cs*):</span><span class="sxs-lookup"><span data-stu-id="1c292-148">The sample uses SHA1 file hashing (*Utilities/Utilities.cs*):</span></span>

   [!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet1)]

   <span data-ttu-id="1c292-149">重试使用指数退让实现。</span><span class="sxs-lookup"><span data-stu-id="1c292-149">A retry is implemented with an exponential back-off.</span></span> <span data-ttu-id="1c292-150">重试不存在，因为文件锁定可能会发生，暂时禁止计算一个新的哈希上的文件之一。</span><span class="sxs-lookup"><span data-stu-id="1c292-150">The re-try is present because file locking may occur that temporarily prevents computing a new hash on one of the files.</span></span>

### <a name="simple-startup-change-token"></a><span data-ttu-id="1c292-151">简单启动更改令牌</span><span class="sxs-lookup"><span data-stu-id="1c292-151">Simple startup change token</span></span>

<span data-ttu-id="1c292-152">注册令牌使用者`Action`回调到配置重新加载令牌更改通知 (*Startup.cs*):</span><span class="sxs-lookup"><span data-stu-id="1c292-152">Register a token consumer `Action` callback for change notifications to the configuration reload token (*Startup.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="1c292-153">`config.GetReloadToken()`提供了令牌。</span><span class="sxs-lookup"><span data-stu-id="1c292-153">`config.GetReloadToken()` provides the token.</span></span> <span data-ttu-id="1c292-154">是回调`InvokeChanged`方法：</span><span class="sxs-lookup"><span data-stu-id="1c292-154">The callback is the `InvokeChanged` method:</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet3)]

<span data-ttu-id="1c292-155">`state`的回调用来中传递`IHostingEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="1c292-155">The `state` of the callback is used to pass in the `IHostingEnvironment`.</span></span> <span data-ttu-id="1c292-156">这可用于确定正确*appsettings* JSON 配置文件若要监视， *appsettings。&lt;环境&gt;.json*。</span><span class="sxs-lookup"><span data-stu-id="1c292-156">This is useful to determine the correct *appsettings* configuration JSON file to monitor, *appsettings.&lt;Environment&gt;.json*.</span></span> <span data-ttu-id="1c292-157">文件哈希值用于防止`WriteConsole`多次由于多个令牌的回调配置文件仅一次更改时才运行的语句。</span><span class="sxs-lookup"><span data-stu-id="1c292-157">File hashes are used to prevent the `WriteConsole` statement from running multiple times due to multiple token callbacks when the configuration file has only changed once.</span></span>

<span data-ttu-id="1c292-158">此系统在运行，只要该应用程序正在运行并且无法由用户禁用。</span><span class="sxs-lookup"><span data-stu-id="1c292-158">This system runs as long as the app is running and can't be disabled by the user.</span></span>

### <a name="monitoring-configuration-changes-as-a-service"></a><span data-ttu-id="1c292-159">作为一项服务的监视配置更改</span><span class="sxs-lookup"><span data-stu-id="1c292-159">Monitoring configuration changes as a service</span></span>

<span data-ttu-id="1c292-160">此示例实现：</span><span class="sxs-lookup"><span data-stu-id="1c292-160">The sample implements:</span></span>

* <span data-ttu-id="1c292-161">基本启动令牌监视。</span><span class="sxs-lookup"><span data-stu-id="1c292-161">Basic startup token monitoring.</span></span>
* <span data-ttu-id="1c292-162">监视作为一项服务。</span><span class="sxs-lookup"><span data-stu-id="1c292-162">Monitoring as a service.</span></span>
* <span data-ttu-id="1c292-163">一种机制来启用和禁用监视。</span><span class="sxs-lookup"><span data-stu-id="1c292-163">A mechanism to enable and disable monitoring.</span></span>

<span data-ttu-id="1c292-164">此示例建立`IConfigurationMonitor`接口 (*Extensions/ConfigurationMonitor.cs*):</span><span class="sxs-lookup"><span data-stu-id="1c292-164">The sample establishes an `IConfigurationMonitor` interface (*Extensions/ConfigurationMonitor.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet1)]

<span data-ttu-id="1c292-165">实现的类，构造函数`ConfigurationMonitor`，为更改通知注册回调：</span><span class="sxs-lookup"><span data-stu-id="1c292-165">The constructor of the implemented class, `ConfigurationMonitor`, registers a callback for change notifications:</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet2)]

<span data-ttu-id="1c292-166">`config.GetReloadToken()`提供该令牌。</span><span class="sxs-lookup"><span data-stu-id="1c292-166">`config.GetReloadToken()` supplies the token.</span></span> <span data-ttu-id="1c292-167">`InvokeChanged`是一个回调方法。</span><span class="sxs-lookup"><span data-stu-id="1c292-167">`InvokeChanged` is the callback method.</span></span> <span data-ttu-id="1c292-168">`state`此实例中是一个字符串，描述的监视状态。</span><span class="sxs-lookup"><span data-stu-id="1c292-168">The `state` in this instance is a string that describes the monitoring state.</span></span> <span data-ttu-id="1c292-169">使用两个属性：</span><span class="sxs-lookup"><span data-stu-id="1c292-169">Two properties are used:</span></span>

* <span data-ttu-id="1c292-170">`MonitoringEnabled`指示回调是否应运行其自定义代码。</span><span class="sxs-lookup"><span data-stu-id="1c292-170">`MonitoringEnabled` indicates if the callback should run its custom code.</span></span>
* <span data-ttu-id="1c292-171">`CurrentState`描述在 UI 中使用的当前监视状态。</span><span class="sxs-lookup"><span data-stu-id="1c292-171">`CurrentState` describes the current monitoring state for use in the UI.</span></span>

<span data-ttu-id="1c292-172">`InvokeChanged`方法类似于前面方法中，但它是：</span><span class="sxs-lookup"><span data-stu-id="1c292-172">The `InvokeChanged` method is similar to the earlier approach, except that it:</span></span>

* <span data-ttu-id="1c292-173">不运行其代码，除非`MonitoringEnabled`是`true`。</span><span class="sxs-lookup"><span data-stu-id="1c292-173">Doesn't run its code unless `MonitoringEnabled` is `true`.</span></span>
* <span data-ttu-id="1c292-174">集`CurrentState`属性字符串与记录代码运行时间的描述性消息。</span><span class="sxs-lookup"><span data-stu-id="1c292-174">Sets the `CurrentState` property string to a descriptive message that records the time that the code ran.</span></span>
* <span data-ttu-id="1c292-175">说明当前`state`中其`WriteConsole`输出。</span><span class="sxs-lookup"><span data-stu-id="1c292-175">Notes the current `state` in its `WriteConsole` output.</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet3)]

<span data-ttu-id="1c292-176">实例`ConfigurationMonitor`注册中的服务为`ConfigureServices`的*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="1c292-176">An instance `ConfigurationMonitor` is registered as a service in `ConfigureServices` of *Startup.cs*:</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="1c292-177">索引页提供对配置监视的用户控制。</span><span class="sxs-lookup"><span data-stu-id="1c292-177">The Index page offers the user control over configuration monitoring.</span></span> <span data-ttu-id="1c292-178">实例`IConfigurationMonitor`注入到`IndexModel`:</span><span class="sxs-lookup"><span data-stu-id="1c292-178">The instance of `IConfigurationMonitor` is injected into the `IndexModel`:</span></span>

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="1c292-179">按钮启用和禁用监视：</span><span class="sxs-lookup"><span data-stu-id="1c292-179">A button enables and disables monitoring:</span></span>

[!code-cshtml[Main](change-tokens/sample/Pages/Index.cshtml?range=35)]

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet2)]

<span data-ttu-id="1c292-180">当`OnPostStartMonitoring`是触发，启用了监视，并且会清除当前状态。</span><span class="sxs-lookup"><span data-stu-id="1c292-180">When `OnPostStartMonitoring` is triggered, monitoring is enabled, and the current state is cleared.</span></span> <span data-ttu-id="1c292-181">当`OnPostStopMonitoring`是触发，监视处于禁用状态，并且状态将设置以反映指出未进行监视。</span><span class="sxs-lookup"><span data-stu-id="1c292-181">When `OnPostStopMonitoring` is triggered, monitoring is disabled, and the state is set to reflect that monitoring isn't occurring.</span></span>

## <a name="monitoring-cached-file-changes"></a><span data-ttu-id="1c292-182">监视缓存的文件更改</span><span class="sxs-lookup"><span data-stu-id="1c292-182">Monitoring cached file changes</span></span>

<span data-ttu-id="1c292-183">文件内容可以是缓存内存中使用[IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)。</span><span class="sxs-lookup"><span data-stu-id="1c292-183">File content can be cached in-memory using [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache).</span></span> <span data-ttu-id="1c292-184">内存中缓存所述[内存中缓存](xref:performance/caching/memory)主题。</span><span class="sxs-lookup"><span data-stu-id="1c292-184">In-memory caching is described in the [In-memory caching](xref:performance/caching/memory) topic.</span></span> <span data-ttu-id="1c292-185">而无需采取其他步骤，如下面所述，实现*陈旧*如果源数据更改 （过时） 的数据从缓存返回。</span><span class="sxs-lookup"><span data-stu-id="1c292-185">Without taking additional steps, such as the implementation described below, *stale* (outdated) data is returned from a cache if the source data changes.</span></span>

<span data-ttu-id="1c292-186">不考虑缓存的源文件的状态时续订[相对过期机制](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration)段会导致过时的缓存数据。</span><span class="sxs-lookup"><span data-stu-id="1c292-186">Not taking into account the status of a cached source file when renewing a [sliding expiration](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) period leads to stale cache data.</span></span> <span data-ttu-id="1c292-187">数据的每个请求续订滑动过期时间，但该文件永远不会重新加载到缓存。</span><span class="sxs-lookup"><span data-stu-id="1c292-187">Each request for the data renews the sliding expiration period, but the file is never reloaded into the cache.</span></span> <span data-ttu-id="1c292-188">可能接收过时的内容受到使用该文件的缓存的内容的任何应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="1c292-188">Any app features that use the file's cached content are subject to possibly receiving stale content.</span></span>

<span data-ttu-id="1c292-189">在文件缓存方案中使用更改令牌可防止缓存中的陈旧文件内容。</span><span class="sxs-lookup"><span data-stu-id="1c292-189">Using change tokens in a file caching scenario prevents stale file content in the cache.</span></span> <span data-ttu-id="1c292-190">示例应用演示如何方法的实现。</span><span class="sxs-lookup"><span data-stu-id="1c292-190">The sample app demonstrates an implementation of the approach.</span></span>

<span data-ttu-id="1c292-191">此示例使用`GetFileContent`到：</span><span class="sxs-lookup"><span data-stu-id="1c292-191">The sample uses `GetFileContent` to:</span></span>

* <span data-ttu-id="1c292-192">返回文件内容。</span><span class="sxs-lookup"><span data-stu-id="1c292-192">Return file content.</span></span>
* <span data-ttu-id="1c292-193">实现使用指数退让到其中的文件锁定暂时防止文件被读取的封面情况下重试算法。</span><span class="sxs-lookup"><span data-stu-id="1c292-193">Implement a retry algorithm with exponential back-off to cover cases where a file lock is temporarily preventing a file from being read.</span></span>

<span data-ttu-id="1c292-194">*Utilities/Utilities.cs*:</span><span class="sxs-lookup"><span data-stu-id="1c292-194">*Utilities/Utilities.cs*:</span></span>

[!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet2)]

<span data-ttu-id="1c292-195">A`FileService`创建以处理查找缓存的文件。</span><span class="sxs-lookup"><span data-stu-id="1c292-195">A `FileService` is created to handle cached file lookups.</span></span> <span data-ttu-id="1c292-196">`GetFileContent`方法调用的服务将尝试从内存中缓存中获取文件内容并将其返回给调用方 (*Services/FileService.cs*)。</span><span class="sxs-lookup"><span data-stu-id="1c292-196">The `GetFileContent` method call of the service attempts to obtain file content from the in-memory cache and return it to the caller (*Services/FileService.cs*).</span></span>

<span data-ttu-id="1c292-197">如果没有找到缓存的内容，使用的缓存密钥，会采取以下操作：</span><span class="sxs-lookup"><span data-stu-id="1c292-197">If cached content isn't found using the cache key, the following actions are taken:</span></span>

1. <span data-ttu-id="1c292-198">使用获取文件内容`GetFileContent`。</span><span class="sxs-lookup"><span data-stu-id="1c292-198">The file content is obtained using `GetFileContent`.</span></span>
1. <span data-ttu-id="1c292-199">从使用文件提供程序获取更改令牌[IFileProviders.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch)。</span><span class="sxs-lookup"><span data-stu-id="1c292-199">A change token is obtained from the file provider with [IFileProviders.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch).</span></span> <span data-ttu-id="1c292-200">修改该文件时，会触发令牌的回调。</span><span class="sxs-lookup"><span data-stu-id="1c292-200">The token's callback is triggered when the file is modified.</span></span>
1. <span data-ttu-id="1c292-201">文件内容进行缓存[相对过期机制](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration)段。</span><span class="sxs-lookup"><span data-stu-id="1c292-201">The file content is cached with a [sliding expiration](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) period.</span></span> <span data-ttu-id="1c292-202">与连接的更改令牌[MemoryCacheEntryExtensions.AddExpirationToken](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryextensions.addexpirationtoken)逐出缓存项，如果文件发生更改时进行缓存。</span><span class="sxs-lookup"><span data-stu-id="1c292-202">The change token is attached with [MemoryCacheEntryExtensions.AddExpirationToken](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryextensions.addexpirationtoken) to evict the cache entry if the file changes while it's cached.</span></span>

[!code-csharp[Main](change-tokens/sample/Services/FileService.cs?name=snippet1)]

<span data-ttu-id="1c292-203">`FileService`在以及内存中缓存服务的服务容器中注册 (*Startup.cs*):</span><span class="sxs-lookup"><span data-stu-id="1c292-203">The `FileService` is registered in the service container along with the memory caching service (*Startup.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet4)]

<span data-ttu-id="1c292-204">页模型加载该文件的内容使用服务 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="1c292-204">The page model loads the file's content using the service (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet3)]

## <a name="compositechangetoken-class"></a><span data-ttu-id="1c292-205">CompositeChangeToken 类</span><span class="sxs-lookup"><span data-stu-id="1c292-205">CompositeChangeToken class</span></span>

<span data-ttu-id="1c292-206">用于表示一个或多个`IChangeToken`中单个对象的实例使用[CompositeChangeToken](/dotnet/api/microsoft.extensions.primitives.compositechangetoken)类 ([引用源](https://github.com/aspnet/Common/blob/patch/2.0.1/src/Microsoft.Extensions.Primitives/CompositeChangeToken.cs))。</span><span class="sxs-lookup"><span data-stu-id="1c292-206">For representing one or more `IChangeToken` instances in a single object, use the [CompositeChangeToken](/dotnet/api/microsoft.extensions.primitives.compositechangetoken) class ([reference source](https://github.com/aspnet/Common/blob/patch/2.0.1/src/Microsoft.Extensions.Primitives/CompositeChangeToken.cs)).</span></span>

```csharp
var firstCancellationTokenSource = new CancellationTokenSource();
var secondCancellationTokenSource = new CancellationTokenSource();

var firstCancellationToken = firstCancellationTokenSource.Token;
var secondCancellationToken = secondCancellationTokenSource.Token;

var firstCancellationChangeToken = new CancellationChangeToken(firstCancellationToken);
var secondCancellationChangeToken = new CancellationChangeToken(secondCancellationToken);

var compositeChangeToken = 
    new CompositeChangeToken(
        new List<IChangeToken> 
        { 
            firstCancellationChangeToken, 
            secondCancellationChangeToken
        });
```

<span data-ttu-id="1c292-207">`HasChanged`在复合令牌报告`true`如果任何表示令牌`HasChanged`是`true`。</span><span class="sxs-lookup"><span data-stu-id="1c292-207">`HasChanged` on the composite token reports `true` if any represented token `HasChanged` is `true`.</span></span> <span data-ttu-id="1c292-208">`ActiveChangeCallbacks`在复合令牌报告`true`如果任何表示令牌`ActiveChangeCallbacks`是`true`。</span><span class="sxs-lookup"><span data-stu-id="1c292-208">`ActiveChangeCallbacks` on the composite token reports `true` if any represented token `ActiveChangeCallbacks` is `true`.</span></span> <span data-ttu-id="1c292-209">如果多个并发更改事件发生，复合更改回调调用恰好一次。</span><span class="sxs-lookup"><span data-stu-id="1c292-209">If multiple concurrent change events occur, the composite change callback is invoked exactly one time.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c292-210">请参阅</span><span class="sxs-lookup"><span data-stu-id="1c292-210">See also</span></span>

* [<span data-ttu-id="1c292-211">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="1c292-211">In-memory caching</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="1c292-212">使用分布式缓存</span><span class="sxs-lookup"><span data-stu-id="1c292-212">Working with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="1c292-213">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="1c292-213">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="1c292-214">响应缓存</span><span class="sxs-lookup"><span data-stu-id="1c292-214">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="1c292-215">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="1c292-215">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="1c292-216">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="1c292-216">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="1c292-217">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="1c292-217">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
