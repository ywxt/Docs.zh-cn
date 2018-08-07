---
title: ASP.NET Core 中的选项模式
author: guardrex
description: 了解如何使用选项模式来表示 ASP.NET Core 应用中的相关设置组。
ms.author: riande
ms.custom: mvc
ms.date: 11/28/2017
uid: fundamentals/configuration/options
ms.openlocfilehash: fd3e55ec821be336501f523550f547f6049c9937
ms.sourcegitcommit: 4e34ce61e1e7f1317102b16012ce0742abf2cca6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2018
ms.locfileid: "39514747"
---
# <a name="options-pattern-in-aspnet-core"></a><span data-ttu-id="416a3-103">ASP.NET Core 中的选项模式</span><span class="sxs-lookup"><span data-stu-id="416a3-103">Options pattern in ASP.NET Core</span></span>

<span data-ttu-id="416a3-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="416a3-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="416a3-105">选项模式使用类来表示相关设置的组。</span><span class="sxs-lookup"><span data-stu-id="416a3-105">The options pattern uses classes to represent groups of related settings.</span></span> <span data-ttu-id="416a3-106">当配置设置由功能隔离到单独的类时，应用遵循两个重要软件工程原则：</span><span class="sxs-lookup"><span data-stu-id="416a3-106">When configuration settings are isolated by feature into separate classes, the app adheres to two important software engineering principles:</span></span>

* <span data-ttu-id="416a3-107">[接口分离原则 (ISP)](http://deviq.com/interface-segregation-principle/)：依赖于配置设置的功能（类）仅依赖于其使用的配置设置。</span><span class="sxs-lookup"><span data-stu-id="416a3-107">The [Interface Segregation Principle (ISP)](http://deviq.com/interface-segregation-principle/): Features (classes) that depend on configuration settings depend only on the configuration settings that they use.</span></span>
* <span data-ttu-id="416a3-108">[关注点分离](http://deviq.com/separation-of-concerns/)：应用的不同部件的设置不彼此依赖或相互耦合。</span><span class="sxs-lookup"><span data-stu-id="416a3-108">[Separation of Concerns](http://deviq.com/separation-of-concerns/): Settings for different parts of the app aren't dependent or coupled to one another.</span></span>

<span data-ttu-id="416a3-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）跟随示例应用可更轻松地理解本文。</span><span class="sxs-lookup"><span data-stu-id="416a3-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) This article is easier to follow with the sample app.</span></span>

## <a name="basic-options-configuration"></a><span data-ttu-id="416a3-110">基本选项配置</span><span class="sxs-lookup"><span data-stu-id="416a3-110">Basic options configuration</span></span>

<span data-ttu-id="416a3-111">基本选项配置已作为示例 &num;1 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-111">Basic options configuration is demonstrated as Example &num;1 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-112">选项类必须为包含公共无参数构造函数的非抽象类。</span><span class="sxs-lookup"><span data-stu-id="416a3-112">An options class must be non-abstract with a public parameterless constructor.</span></span> <span data-ttu-id="416a3-113">以下类 `MyOptions` 具有两种属性：`Option1` 和 `Option2`。</span><span class="sxs-lookup"><span data-stu-id="416a3-113">The following class, `MyOptions`, has two properties, `Option1` and `Option2`.</span></span> <span data-ttu-id="416a3-114">设置默认值为可选，但以下示例中的类构造函数设置了 `Option1` 的默认值。</span><span class="sxs-lookup"><span data-stu-id="416a3-114">Setting default values is optional, but the class constructor in the following example sets the default value of `Option1`.</span></span> <span data-ttu-id="416a3-115">`Option2` 具有通过直接初始化属性设置的默认值 (Models/MyOptions.cs)：</span><span class="sxs-lookup"><span data-stu-id="416a3-115">`Option2` has a default value set by initializing the property directly (*Models/MyOptions.cs*):</span></span>

[!code-csharp[](options/sample/Models/MyOptions.cs?name=snippet1)]

<span data-ttu-id="416a3-116">`MyOptions` 类通过 [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_) 添加到服务容器并绑定到配置：</span><span class="sxs-lookup"><span data-stu-id="416a3-116">The `MyOptions` class is added to the service container with [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_) and bound to configuration:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example1)]

<span data-ttu-id="416a3-117">以下页上的模型通过 [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) 使用[构造函数依赖关系注入](xref:mvc/controllers/dependency-injection)来访问设置 (Pages/Index.cshtml.cs)：</span><span class="sxs-lookup"><span data-stu-id="416a3-117">The following page model uses [constructor dependency injection](xref:mvc/controllers/dependency-injection) with [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) to access the settings (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

<span data-ttu-id="416a3-118">示例的 appsettings.json 文件指定 `option1` 和 `option2` 的值：</span><span class="sxs-lookup"><span data-stu-id="416a3-118">The sample's *appsettings.json* file specifies values for `option1` and `option2`:</span></span>

[!code-json[](options/sample/appsettings.json?highlight=2-3)]

<span data-ttu-id="416a3-119">运行应用时，页模型的 `OnGet` 方法返回显示选项类值的字符串：</span><span class="sxs-lookup"><span data-stu-id="416a3-119">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> <span data-ttu-id="416a3-120">使用自定义 [ConfigurationBuilder](/dotnet/api/system.configuration.configurationbuilder) 从设置文件加载选项配置时，请确认基路径设置正确：</span><span class="sxs-lookup"><span data-stu-id="416a3-120">When using a custom [ConfigurationBuilder](/dotnet/api/system.configuration.configurationbuilder) to load options configuration from a settings file, confirm that the base path is set correctly:</span></span>
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> <span data-ttu-id="416a3-121">通过 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 从设置文件加载选项配置时，不需要显式设置基路径。</span><span class="sxs-lookup"><span data-stu-id="416a3-121">Explicitly setting the base path isn't required when loading options configuration from the settings file via [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

## <a name="configure-simple-options-with-a-delegate"></a><span data-ttu-id="416a3-122">通过委托配置简单选项</span><span class="sxs-lookup"><span data-stu-id="416a3-122">Configure simple options with a delegate</span></span>

<span data-ttu-id="416a3-123">通过委托配置简单选项已作为示例 &num;2 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-123">Configuring simple options with a delegate is demonstrated as Example &num;2 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-124">使用委托设置选项值。</span><span class="sxs-lookup"><span data-stu-id="416a3-124">Use a delegate to set options values.</span></span> <span data-ttu-id="416a3-125">此示例应用使用 `MyOptionsWithDelegateConfig` 类 (Models/MyOptionsWithDelegateConfig.cs)：</span><span class="sxs-lookup"><span data-stu-id="416a3-125">The sample app uses the `MyOptionsWithDelegateConfig` class (*Models/MyOptionsWithDelegateConfig.cs*):</span></span>

[!code-csharp[](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

<span data-ttu-id="416a3-126">在以下代码中，已向服务容器添加第二个 `IConfigureOptions<TOptions>` 服务。</span><span class="sxs-lookup"><span data-stu-id="416a3-126">In the following code, a second `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="416a3-127">它通过 `MyOptionsWithDelegateConfig` 使用委托来配置绑定：</span><span class="sxs-lookup"><span data-stu-id="416a3-127">It uses a delegate to configure the binding with `MyOptionsWithDelegateConfig`:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example2)]

<span data-ttu-id="416a3-128">Index.cshtml.cs:</span><span class="sxs-lookup"><span data-stu-id="416a3-128">*Index.cshtml.cs*:</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

<span data-ttu-id="416a3-129">可添加多个配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="416a3-129">You can add multiple configuration providers.</span></span> <span data-ttu-id="416a3-130">配置提供程序在 NuGet 包中可用。</span><span class="sxs-lookup"><span data-stu-id="416a3-130">Configuration providers are available in NuGet packages.</span></span> <span data-ttu-id="416a3-131">应用此提供程序，以便将其注册。</span><span class="sxs-lookup"><span data-stu-id="416a3-131">They're applied in order that they're registered.</span></span>

<span data-ttu-id="416a3-132">每次调用 [Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) 都将添加 `IConfigureOptions<TOptions>` 服务到服务容器。</span><span class="sxs-lookup"><span data-stu-id="416a3-132">Each call to [Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) adds an `IConfigureOptions<TOptions>` service to the service container.</span></span> <span data-ttu-id="416a3-133">在前面的示例中，`Option1` 和 `Option2` 的值同时在 appsettings.json 中指定，但 `Option1` 和 `Option2` 的值被配置的委托替代。</span><span class="sxs-lookup"><span data-stu-id="416a3-133">In the preceding example, the values of `Option1` and `Option2` are both specified in *appsettings.json*, but the values of `Option1` and `Option2` are overridden by the configured delegate.</span></span>

<span data-ttu-id="416a3-134">当启用多个配置服务时，指定的最后一个配置源优于其他源，由其设置配置值。</span><span class="sxs-lookup"><span data-stu-id="416a3-134">When more than one configuration service is enabled, the last configuration source specified *wins* and sets the configuration value.</span></span> <span data-ttu-id="416a3-135">运行应用时，页模型的 `OnGet` 方法返回显示选项类值的字符串：</span><span class="sxs-lookup"><span data-stu-id="416a3-135">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a><span data-ttu-id="416a3-136">子选项配置</span><span class="sxs-lookup"><span data-stu-id="416a3-136">Suboptions configuration</span></span>

<span data-ttu-id="416a3-137">子选项配置已作为示例 &num;3 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-137">Suboptions configuration is demonstrated as Example &num;3 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-138">应用应创建适用于应用中特定功能组（类）的选项类。</span><span class="sxs-lookup"><span data-stu-id="416a3-138">Apps should create options classes that pertain to specific feature groups (classes) in the app.</span></span> <span data-ttu-id="416a3-139">需要配置值的部分应用应仅有权访问其使用的配置值。</span><span class="sxs-lookup"><span data-stu-id="416a3-139">Parts of the app that require configuration values should only have access to the configuration values that they use.</span></span>

<span data-ttu-id="416a3-140">将选项绑定到配置时，选项类型中的每个属性都将绑定到窗体 `property[:sub-property:]` 的配置键。</span><span class="sxs-lookup"><span data-stu-id="416a3-140">When binding options to configuration, each property in the options type is bound to a configuration key of the form `property[:sub-property:]`.</span></span> <span data-ttu-id="416a3-141">例如，`MyOptions.Option1` 属性将绑定到从 appsettings.json 中的 `option1` 属性读取的键 `Option1`。</span><span class="sxs-lookup"><span data-stu-id="416a3-141">For example, the `MyOptions.Option1` property is bound to the key `Option1`, which is read from the `option1` property in *appsettings.json*.</span></span>

<span data-ttu-id="416a3-142">在以下代码中，已向服务容器添加第三个 `IConfigureOptions<TOptions>` 服务。</span><span class="sxs-lookup"><span data-stu-id="416a3-142">In the following code, a third `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="416a3-143">它将 `MySubOptions` 绑定到 appsettings.json 文件的 `subsection` 部分：</span><span class="sxs-lookup"><span data-stu-id="416a3-143">It binds `MySubOptions` to the section `subsection` of the *appsettings.json* file:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example3)]

<span data-ttu-id="416a3-144">`GetSection` 扩展方法需要 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="416a3-144">The `GetSection` extension method requires the [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet package.</span></span> <span data-ttu-id="416a3-145">如果应用使用 [Microsoft.AspNetCore.App metapackage 元包](xref:fundamentals/metapackage-app)（ASP.NET Core 2.1 或更高版本），将自动包含此包。</span><span class="sxs-lookup"><span data-stu-id="416a3-145">If the app uses the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later), the package is automatically included.</span></span>

<span data-ttu-id="416a3-146">示例的 appsettings.json 文件定义具有 `suboption1` 和 `suboption2` 的键的 `subsection` 成员：</span><span class="sxs-lookup"><span data-stu-id="416a3-146">The sample's *appsettings.json* file defines a `subsection` member with keys for `suboption1` and `suboption2`:</span></span>

[!code-json[](options/sample/appsettings.json?highlight=4-7)]

<span data-ttu-id="416a3-147">`MySubOptions` 类定义属性 `SubOption1` 和 `SubOption2`，以保留子选项值 (Models/MySubOptions.cs)：</span><span class="sxs-lookup"><span data-stu-id="416a3-147">The `MySubOptions` class defines properties, `SubOption1` and `SubOption2`, to hold the sub-option values (*Models/MySubOptions.cs*):</span></span>

[!code-csharp[](options/sample/Models/MySubOptions.cs?name=snippet1)]

<span data-ttu-id="416a3-148">页模型的 `OnGet` 方法返回包含子选项值的字符串 (Pages/Index.cshtml.cs)：</span><span class="sxs-lookup"><span data-stu-id="416a3-148">The page model's `OnGet` method returns a string with the sub-option values (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

<span data-ttu-id="416a3-149">运行应用时，`OnGet` 方法返回显示子选项类值的字符串：</span><span class="sxs-lookup"><span data-stu-id="416a3-149">When the app is run, the `OnGet` method returns a string showing the sub-option class values:</span></span>

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a><span data-ttu-id="416a3-150">视图模型或通过直接视图注入提供的选项</span><span class="sxs-lookup"><span data-stu-id="416a3-150">Options provided by a view model or with direct view injection</span></span>

<span data-ttu-id="416a3-151">视图模型或通过直接视图注入提供的选项已作为示例 &num;4 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-151">Options provided by a view model or with direct view injection is demonstrated as Example &num;4 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-152">可在视图模型中或通过将 `IOptions<TOptions>` 直接注入到视图 (Pages/Index.cshtml.cs) 来提供选项：</span><span class="sxs-lookup"><span data-stu-id="416a3-152">Options can be supplied in a view model or by injecting `IOptions<TOptions>` directly into a view (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

<span data-ttu-id="416a3-153">对于直接注入，通过 `@inject` 指令注入 `IOptions<MyOptions>`：</span><span class="sxs-lookup"><span data-stu-id="416a3-153">For direct injection, inject `IOptions<MyOptions>` with an `@inject` directive:</span></span>

[!code-cshtml[](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

<span data-ttu-id="416a3-154">运行应用时，选项值显示在已呈现的页中：</span><span class="sxs-lookup"><span data-stu-id="416a3-154">When the app is run, the option values are shown in the rendered page:</span></span>

![选项值 Option1：value1_from_json 和 Option2：-1 从模型中加载并注入视图。](options/_static/view.png)

::: moniker range=">= aspnetcore-1.1"

## <a name="reload-configuration-data-with-ioptionssnapshot"></a><span data-ttu-id="416a3-156">通过 IOptionsSnapshot 重新加载配置数据</span><span class="sxs-lookup"><span data-stu-id="416a3-156">Reload configuration data with IOptionsSnapshot</span></span>

<span data-ttu-id="416a3-157">通过 `IOptionsSnapshot` 重新加载配置数据已作为示例 &num;5 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-157">Reloading configuration data with `IOptionsSnapshot` is demonstrated in Example &num;5 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-158">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) 支持包含最小处理开销的重新加载选项。</span><span class="sxs-lookup"><span data-stu-id="416a3-158">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) supports reloading options with minimal processing overhead.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="416a3-159">针对请求生存期访问和缓存选项时，每个请求只能计算一次选项。</span><span class="sxs-lookup"><span data-stu-id="416a3-159">Options are computed once per request when accessed and cached for the lifetime of the request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="416a3-160">`IOptionsSnapshot` 是 [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 的快照，每当监视器随数据源变化而触发更改时自动更新。</span><span class="sxs-lookup"><span data-stu-id="416a3-160">`IOptionsSnapshot` is a snapshot of [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) and updates automatically whenever the monitor triggers changes based on the data source changing.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="416a3-161">以下示例演示如何在更改 appsettings.json (Pages/Index.cshtml.cs) 后创建新的 `IOptionsSnapshot`。</span><span class="sxs-lookup"><span data-stu-id="416a3-161">The following example demonstrates how a new `IOptionsSnapshot` is created after *appsettings.json* changes (*Pages/Index.cshtml.cs*).</span></span> <span data-ttu-id="416a3-162">在更改文件和重新加载配置之前，针对服务器的多个请求返回 appsettings.json 文件提供的常数值。</span><span class="sxs-lookup"><span data-stu-id="416a3-162">Multiple requests to the server return constant values provided by the *appsettings.json* file until the file is changed and configuration reloads.</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

<span data-ttu-id="416a3-163">下图显示从 appsettings.json 文件加载的初始 `option1` 和 `option2` 值：</span><span class="sxs-lookup"><span data-stu-id="416a3-163">The following image shows the initial `option1` and `option2` values loaded from the *appsettings.json* file:</span></span>

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

<span data-ttu-id="416a3-164">将 appsettings.json 文件中的值更改为 `value1_from_json UPDATED` 和 `200`。</span><span class="sxs-lookup"><span data-stu-id="416a3-164">Change the values in the *appsettings.json* file to `value1_from_json UPDATED` and `200`.</span></span> <span data-ttu-id="416a3-165">保存 appsettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="416a3-165">Save the *appsettings.json* file.</span></span> <span data-ttu-id="416a3-166">刷新浏览器，查看更新的选项值：</span><span class="sxs-lookup"><span data-stu-id="416a3-166">Refresh the browser to see that the options values are updated:</span></span>

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

## <a name="named-options-support-with-iconfigurenamedoptions"></a><span data-ttu-id="416a3-167">包含 IConfigureNamedOptions 的命名选项支持</span><span class="sxs-lookup"><span data-stu-id="416a3-167">Named options support with IConfigureNamedOptions</span></span>

<span data-ttu-id="416a3-168">包含 [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) 的命名选项支持已作为示例 &num;6 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。</span><span class="sxs-lookup"><span data-stu-id="416a3-168">Named options support with [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) is demonstrated as Example &num;6 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="416a3-169">命名选项支持允许应用在命名选项配置之间进行区分。</span><span class="sxs-lookup"><span data-stu-id="416a3-169">*Named options* support allows the app to distinguish between named options configurations.</span></span> <span data-ttu-id="416a3-170">在示例应用中，通过 [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure) 声明命名的选项，其反过来又调用扩展方法 [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 方法：</span><span class="sxs-lookup"><span data-stu-id="416a3-170">In the sample app, named options are declared with the [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure) which in turn calls the extension method [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) method:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example6)]

<span data-ttu-id="416a3-171">示例应用通过 [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (Pages/Index.cshtml.cs) 访问命名选项：</span><span class="sxs-lookup"><span data-stu-id="416a3-171">The sample app accesses the named options with [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

<span data-ttu-id="416a3-172">运行示例应用，将返回命名选项：</span><span class="sxs-lookup"><span data-stu-id="416a3-172">Running the sample app, the named options are returned:</span></span>

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

<span data-ttu-id="416a3-173">从配置中提供从 appsettings.json 文件中加载的 `named_options_1` 值。</span><span class="sxs-lookup"><span data-stu-id="416a3-173">`named_options_1` values are provided from configuration, which are loaded from the *appsettings.json* file.</span></span> <span data-ttu-id="416a3-174">通过以下内容提供 `named_options_2` 值：</span><span class="sxs-lookup"><span data-stu-id="416a3-174">`named_options_2` values are provided by:</span></span>

* <span data-ttu-id="416a3-175">针对 `Option1` 的 `ConfigureServices` 中的 `named_options_2` 委托。</span><span class="sxs-lookup"><span data-stu-id="416a3-175">The `named_options_2` delegate in `ConfigureServices` for `Option1`.</span></span>
* <span data-ttu-id="416a3-176">`MyOptions` 类提供的 `Option2` 的默认值。</span><span class="sxs-lookup"><span data-stu-id="416a3-176">The default value for `Option2` provided by the `MyOptions` class.</span></span>

<span data-ttu-id="416a3-177">通过 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 方法配置所有命名选项实例。</span><span class="sxs-lookup"><span data-stu-id="416a3-177">Configure all named options instances with the [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) method.</span></span> <span data-ttu-id="416a3-178">以下代码将针对包含公共值的所有命名配置实例配置 `Option1`。</span><span class="sxs-lookup"><span data-stu-id="416a3-178">The following code configures `Option1` for all named configuration instances with a common value.</span></span> <span data-ttu-id="416a3-179">将以下代码手动添加到 `Configure` 方法：</span><span class="sxs-lookup"><span data-stu-id="416a3-179">Add the following code manually to the `Configure` method:</span></span>

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

<span data-ttu-id="416a3-180">添加代码后运行示例应用将产生以下结果：</span><span class="sxs-lookup"><span data-stu-id="416a3-180">Running the sample app after adding the code produces the following result:</span></span>

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> <span data-ttu-id="416a3-181">所有选项都是命名实例。</span><span class="sxs-lookup"><span data-stu-id="416a3-181">All options are named instances.</span></span> <span data-ttu-id="416a3-182">现有 `IConfigureOption` 实例将被视为面向为 `string.Empty` 的 `Options.DefaultName` 实例。</span><span class="sxs-lookup"><span data-stu-id="416a3-182">Existing `IConfigureOption` instances are treated as targeting the `Options.DefaultName` instance, which is `string.Empty`.</span></span> <span data-ttu-id="416a3-183">`IConfigureNamedOptions` 还可实现 `IConfigureOptions`。</span><span class="sxs-lookup"><span data-stu-id="416a3-183">`IConfigureNamedOptions` also implements `IConfigureOptions`.</span></span> <span data-ttu-id="416a3-184">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)（[引用源](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs)）的默认实现具有适当使用每个选项的逻辑。</span><span class="sxs-lookup"><span data-stu-id="416a3-184">The default implementation of the [IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) ([reference source](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs) has logic to use each appropriately.</span></span> <span data-ttu-id="416a3-185">`null` 命名选项用于面向所有命名实例而不是某一特定命名实例（[ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 和 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 使用此约定）。</span><span class="sxs-lookup"><span data-stu-id="416a3-185">The `null` named option is used to target all of the named instances instead of a specific named instance ([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) and [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) use this convention).</span></span>

## <a name="ipostconfigureoptions"></a><span data-ttu-id="416a3-186">IPostConfigureOptions</span><span class="sxs-lookup"><span data-stu-id="416a3-186">IPostConfigureOptions</span></span>

<span data-ttu-id="416a3-187">通过 [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1) 设置后期配置。</span><span class="sxs-lookup"><span data-stu-id="416a3-187">Set postconfiguration with [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1).</span></span> <span data-ttu-id="416a3-188">在发生所有 [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 配置后运行后期配置：</span><span class="sxs-lookup"><span data-stu-id="416a3-188">Postconfiguration runs after all [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) configuration occurs:</span></span>

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="416a3-189">[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) 可用于对命名选项进行后期配置：</span><span class="sxs-lookup"><span data-stu-id="416a3-189">[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) is available to post-configure named options:</span></span>

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="416a3-190">使用 [PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 对所有命名配置实例进行后期配置：</span><span class="sxs-lookup"><span data-stu-id="416a3-190">Use [PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) to post-configure all named configuration instances:</span></span>

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

::: moniker-end

## <a name="options-factory-monitoring-and-cache"></a><span data-ttu-id="416a3-191">选项工厂、监视和缓存</span><span class="sxs-lookup"><span data-stu-id="416a3-191">Options factory, monitoring, and cache</span></span>

<span data-ttu-id="416a3-192">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 用于在 `TOptions` 实例更改时进行通知。</span><span class="sxs-lookup"><span data-stu-id="416a3-192">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) is used for notifications when `TOptions` instances change.</span></span> <span data-ttu-id="416a3-193">`IOptionsMonitor` 支持可重载选项、更改通知和 `IPostConfigureOptions`。</span><span class="sxs-lookup"><span data-stu-id="416a3-193">`IOptionsMonitor` supports reloadable options, change notifications, and `IPostConfigureOptions`.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="416a3-194">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) 负责新建选项实例。</span><span class="sxs-lookup"><span data-stu-id="416a3-194">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) is responsible for creating new options instances.</span></span> <span data-ttu-id="416a3-195">它具有单个[创建](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create)方法。</span><span class="sxs-lookup"><span data-stu-id="416a3-195">It has a single [Create](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) method.</span></span> <span data-ttu-id="416a3-196">默认实现采用所有已注册 `IConfigureOptions` 和 `IPostConfigureOptions` 并首先运行所有配置，然后才进行后期配置。</span><span class="sxs-lookup"><span data-stu-id="416a3-196">The default implementation takes all registered `IConfigureOptions` and `IPostConfigureOptions` and runs all the configures first, followed by the post-configures.</span></span> <span data-ttu-id="416a3-197">它区分 `IConfigureNamedOptions` 和 `IConfigureOptions` 且仅调用适当的接口。</span><span class="sxs-lookup"><span data-stu-id="416a3-197">It distinguishes between `IConfigureNamedOptions` and `IConfigureOptions` and only calls the appropriate interface.</span></span>

<span data-ttu-id="416a3-198">`IOptionsMonitor` 使用 [IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) 缓存 `TOptions` 实例。</span><span class="sxs-lookup"><span data-stu-id="416a3-198">[IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) is used by `IOptionsMonitor` to cache `TOptions` instances.</span></span> <span data-ttu-id="416a3-199">`IOptionsMonitorCache` 可使监视器中的选项实例无效，以便重新计算值 ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove))。</span><span class="sxs-lookup"><span data-stu-id="416a3-199">The `IOptionsMonitorCache` invalidates options instances in the monitor so that the value is recomputed ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)).</span></span> <span data-ttu-id="416a3-200">还可通过 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd) 手动引入值。</span><span class="sxs-lookup"><span data-stu-id="416a3-200">Values can be manually introduced as well with [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd).</span></span> <span data-ttu-id="416a3-201">在应按需重新创建所有命名实例时使用[清除](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear)方法。</span><span class="sxs-lookup"><span data-stu-id="416a3-201">The [Clear](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) method is used when all named instances should be recreated on demand.</span></span>

::: moniker-end

## <a name="accessing-options-during-startup"></a><span data-ttu-id="416a3-202">在启动期间访问选项</span><span class="sxs-lookup"><span data-stu-id="416a3-202">Accessing options during startup</span></span>

<span data-ttu-id="416a3-203">`IOptions` 可用于 `Startup.Configure` 中，因为在 `Configure` 方法执行之前已生成服务。</span><span class="sxs-lookup"><span data-stu-id="416a3-203">`IOptions` can be used in `Startup.Configure`, since services are built before the `Configure` method executes.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IOptions<MyOptions> optionsAccessor)
{
    var option1 = optionsAccessor.Value.Option1;
}
```

<span data-ttu-id="416a3-204">`IOptions` 不应在 `Startup.ConfigureServices` 中使用。</span><span class="sxs-lookup"><span data-stu-id="416a3-204">`IOptions` shouldn't be used in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="416a3-205">由于服务注册的顺序，可能存在不一致的选项状态。</span><span class="sxs-lookup"><span data-stu-id="416a3-205">An inconsistent options state may exist due to the ordering of service registrations.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="416a3-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="416a3-206">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
