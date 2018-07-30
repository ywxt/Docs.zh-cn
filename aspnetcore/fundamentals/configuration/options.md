---
title: ASP.NET Core 中的选项模式
author: guardrex
description: 了解如何使用选项模式来表示 ASP.NET Core 应用中的相关设置组。
ms.author: riande
ms.custom: mvc
ms.date: 11/28/2017
uid: fundamentals/configuration/options
ms.openlocfilehash: aa9c490aff873d12c9417e7b611991617207c0d3
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342440"
---
# <a name="options-pattern-in-aspnet-core"></a>ASP.NET Core 中的选项模式

作者：[Luke Latham](https://github.com/guardrex)

选项模式使用类来表示相关设置的组。 当配置设置由功能隔离到单独的类时，应用遵循两个重要软件工程原则：

* [接口分离原则 (ISP)](http://deviq.com/interface-segregation-principle/)：依赖于配置设置的功能（类）仅依赖于其使用的配置设置。
* [关注点分离](http://deviq.com/separation-of-concerns/)：应用的不同部件的设置不彼此依赖或相互耦合。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）跟随示例应用可更轻松地理解本文。

## <a name="basic-options-configuration"></a>基本选项配置

基本选项配置已作为示例 &num;1 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

选项类必须为包含公共无参数构造函数的非抽象类。 以下类 `MyOptions` 具有两种属性：`Option1` 和 `Option2`。 设置默认值为可选，但以下示例中的类构造函数设置了 `Option1` 的默认值。 `Option2` 具有通过直接初始化属性设置的默认值 (Models/MyOptions.cs)：

[!code-csharp[](options/sample/Models/MyOptions.cs?name=snippet1)]

`MyOptions` 类通过 [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_) 添加到服务容器并绑定到配置：

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example1)]

以下页上的模型通过 [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) 使用[构造函数依赖关系注入](xref:mvc/controllers/dependency-injection)来访问设置 (Pages/Index.cshtml.cs)：

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

示例的 appsettings.json 文件指定 `option1` 和 `option2` 的值：

[!code-json[](options/sample/appsettings.json?highlight=2-3)]

运行应用时，页模型的 `OnGet` 方法返回显示选项类值的字符串：

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> 使用自定义 [ConfigurationBuilder](/dotnet/api/system.configuration.configurationbuilder) 从设置文件加载选项配置时，请确认基路径设置正确：
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
> 通过 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 从设置文件加载选项配置时，不需要显式设置基路径。

## <a name="configure-simple-options-with-a-delegate"></a>通过委托配置简单选项

通过委托配置简单选项已作为示例 &num;2 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

使用委托设置选项值。 此示例应用使用 `MyOptionsWithDelegateConfig` 类 (Models/MyOptionsWithDelegateConfig.cs)：

[!code-csharp[](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

在以下代码中，已向服务容器添加第二个 `IConfigureOptions<TOptions>` 服务。 它通过 `MyOptionsWithDelegateConfig` 使用委托来配置绑定：

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example2)]

Index.cshtml.cs:

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

可添加多个配置提供程序。 配置提供程序在 NuGet 包中可用。 应用此提供程序，以便将其注册。

每次调用 [Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) 都将添加 `IConfigureOptions<TOptions>` 服务到服务容器。 在前面的示例中，`Option1` 和 `Option2` 的值同时在 appsettings.json 中指定，但 `Option1` 和 `Option2` 的值被配置的委托替代。

当启用多个配置服务时，指定的最后一个配置源优于其他源，由其设置配置值。 运行应用时，页模型的 `OnGet` 方法返回显示选项类值的字符串：

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>子选项配置

子选项配置已作为示例 &num;3 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

应用应创建适用于应用中特定功能组（类）的选项类。 需要配置值的部分应用应仅有权访问其使用的配置值。

将选项绑定到配置时，选项类型中的每个属性都将绑定到窗体 `property[:sub-property:]` 的配置键。 例如，`MyOptions.Option1` 属性将绑定到从 appsettings.json 中的 `option1` 属性读取的键 `Option1`。

在以下代码中，已向服务容器添加第三个 `IConfigureOptions<TOptions>` 服务。 它将 `MySubOptions` 绑定到 appsettings.json 文件的 `subsection` 部分：

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example3)]

`GetSection` 扩展方法需要 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 包。 如果应用使用 [Microsoft.AspNetCore.App metapackage 元包](xref:fundamentals/metapackage-app)（ASP.NET Core 2.1 或更高版本），将自动包含此包。

示例的 appsettings.json 文件定义具有 `suboption1` 和 `suboption2` 的键的 `subsection` 成员：

[!code-json[](options/sample/appsettings.json?highlight=4-7)]

`MySubOptions` 类定义属性 `SubOption1` 和 `SubOption2`，以保留子选项值 (Models/MySubOptions.cs)：

[!code-csharp[](options/sample/Models/MySubOptions.cs?name=snippet1)]

页模型的 `OnGet` 方法返回包含子选项值的字符串 (Pages/Index.cshtml.cs)：

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

运行应用时，`OnGet` 方法返回显示子选项类值的字符串：

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>视图模型或通过直接视图注入提供的选项

视图模型或通过直接视图注入提供的选项已作为示例 &num;4 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

可在视图模型中或通过将 `IOptions<TOptions>` 直接注入到视图 (Pages/Index.cshtml.cs) 来提供选项：

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

对于直接注入，通过 `@inject` 指令注入 `IOptions<MyOptions>`：

[!code-cshtml[](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

运行应用时，选项值显示在已呈现的页中：

![选项值 Option1：value1_from_json 和 Option2：-1 从模型中加载并注入视图。](options/_static/view.png)

::: moniker range=">= aspnetcore-1.1"

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>通过 IOptionsSnapshot 重新加载配置数据

通过 `IOptionsSnapshot` 重新加载配置数据已作为示例 &num;5 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) 支持包含最小处理开销的重新加载选项。

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

针对请求生存期访问和缓存选项时，每个请求只能计算一次选项。

::: moniker-end

::: moniker range="< aspnetcore-2.0"

`IOptionsSnapshot` 是 [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 的快照，每当监视器随数据源变化而触发更改时自动更新。

::: moniker-end

::: moniker range=">= aspnetcore-1.1"

以下示例演示如何在更改 appsettings.json (Pages/Index.cshtml.cs) 后创建新的 `IOptionsSnapshot`。 在更改文件和重新加载配置之前，针对服务器的多个请求返回 appsettings.json 文件提供的常数值。

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

下图显示从 appsettings.json 文件加载的初始 `option1` 和 `option2` 值：

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

将 appsettings.json 文件中的值更改为 `value1_from_json UPDATED` 和 `200`。 保存 appsettings.json 文件。 刷新浏览器，查看更新的选项值：

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

## <a name="named-options-support-with-iconfigurenamedoptions"></a>包含 IConfigureNamedOptions 的命名选项支持

包含 [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) 的命名选项支持已作为示例 &num;6 在[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)中进行了演示。

命名选项支持允许应用在命名选项配置之间进行区分。 在示例应用中，通过 [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure) 声明命名的选项，其反过来又调用扩展方法 [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 方法：

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example6)]

示例应用通过 [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (Pages/Index.cshtml.cs) 访问命名选项：

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

运行示例应用，将返回命名选项：

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

从配置中提供从 appsettings.json 文件中加载的 `named_options_1` 值。 通过以下内容提供 `named_options_2` 值：

* 针对 `Option1` 的 `ConfigureServices` 中的 `named_options_2` 委托。
* `MyOptions` 类提供的 `Option2` 的默认值。

通过 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 方法配置所有命名选项实例。 以下代码将针对包含公共值的所有命名配置实例配置 `Option1`。 将以下代码手动添加到 `Configure` 方法：

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

添加代码后运行示例应用将产生以下结果：

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> 所有选项都是命名实例。 现有 `IConfigureOption` 实例将被视为面向为 `string.Empty` 的 `Options.DefaultName` 实例。 `IConfigureNamedOptions` 还可实现 `IConfigureOptions`。 [IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)（[引用源](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs)）的默认实现具有适当使用每个选项的逻辑。 `null` 命名选项用于面向所有命名实例而不是某一特定命名实例（[ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 和 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 使用此约定）。

## <a name="ipostconfigureoptions"></a>IPostConfigureOptions

通过 [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1) 设置后期配置。 在发生所有 [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 配置后运行后期配置：

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) 可用于对命名选项进行后期配置：

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

使用 [PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 对所有命名配置实例进行后期配置：

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

::: moniker-end

## <a name="options-factory-monitoring-and-cache"></a>选项工厂、监视和缓存

[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 用于在 `TOptions` 实例更改时进行通知。 `IOptionsMonitor` 支持可重载选项、更改通知和 `IPostConfigureOptions`。

::: moniker range=">= aspnetcore-2.0"

[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) 负责新建选项实例。 它具有单个[创建](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create)方法。 默认实现采用所有已注册 `IConfigureOptions` 和 `IPostConfigureOptions` 并首先运行所有配置，然后才进行后期配置。 它区分 `IConfigureNamedOptions` 和 `IConfigureOptions` 且仅调用适当的接口。

`IOptionsMonitor` 使用 [IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) 缓存 `TOptions` 实例。 `IOptionsMonitorCache` 可使监视器中的选项实例无效，以便重新计算值 ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove))。 还可通过 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd) 手动引入值。 在应按需重新创建所有命名实例时使用[清除](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear)方法。

::: moniker-end

## <a name="accessing-options-during-startup"></a>在启动期间访问选项

`IOptions` 可用于 `Configure` 中，因为在 `Configure` 方法执行之前已生成服务。 如果在 `ConfigureServices` 中生成服务提供程序以访问选项，则它不应包含生成服务提供程序后所提供的任何选项配置。 因此，由于服务注册的顺序，可能存在不一致的选项状态。

由于选项通常从配置中加载，因此，可在 `Configure` 和 `ConfigureServices` 中的启动中使用配置。 有关在启动期间使用配置的示例，请参阅[应用程序启动](xref:fundamentals/startup)主题。

## <a name="see-also"></a>请参阅

* [配置](xref:fundamentals/configuration/index)
