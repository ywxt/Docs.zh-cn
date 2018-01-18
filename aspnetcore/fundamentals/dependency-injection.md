---
title: "在 ASP.NET 核心中的依赖关系注入"
author: ardalis
description: "了解如何 ASP.NET Core 实现依赖关系注入和如何使用它。"
keywords: "ASP.NET 核心，依赖关系注入、 di"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: fccd69be-7ad1-47fb-b203-b3633b6b9a9b
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/dependency-injection
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d12960708f9d9bf2bc7c5997f82096d93087d13
ms.sourcegitcommit: 8f42ab93402c1b8044815e1e48d0bb84c81f8b59
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2017
---
# <a name="introduction-to-dependency-injection-in-aspnet-core"></a>在 ASP.NET Core 中的依赖关系注入简介

<a name="fundamentals-dependency-injection"></a>

通过[Steve Smith](https://ardalis.com/)和[Scott Addie](https://scottaddie.com)

ASP.NET Core 的设计从头至尾以支持和利用依赖注入为目标。ASP.NET Core 应用程序可以通过将内置框架服务注入 Startup 类的方法中来对其加以利用，应用程序服务也可以进行注入配置。 由 ASP.NET Core 提供的默认服务容器提供了一个最小功能集合，并非用于替换其他容器。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-is-dependency-injection"></a>什么是依赖关系注入？

依赖注入 (DI) 是一种用于在对象与其协作者或依赖项之间实现松散耦合的技术。该技术不是直接实例化协作者或使用静态引用，而是以某种方式向类提供该类执行其操作所需的对象。大多数情况下，类通过其构造函数声明它们的依赖项，从而允许它们遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。 此方法称为"构造函数注入"。

在遵循 DI 原则来设计类时，由于它们与其协作者没有直接的，硬编码的依赖关系，所以它们之间的耦合更为松散。 这遵循[依赖倒置原则](http://deviq.com/dependency-inversion-principle/)，其中指出*"高级模块不应依赖于低级模块; 同时两者都应依赖于抽象"。* 类请求在该类被构造时提供给它们的抽象（通常是`interfaces`），而不是引用特定的实现。将依赖关系提取到接口中并将这些接口的实现作为参数提供也是[策略设计模式](http://deviq.com/strategy-design-pattern/)的一个例子。

当系统被设计为使用 DI 时，许多类通过其构造函数 （或属性）来请求它们的依赖项，所以有一个专门用来创建这些类以及它们相关的依赖项的类是很有帮助的。 这些类统称为*容器*，或更具体地说，[控制反转 (IoC)](http://deviq.com/inversion-of-control/)容器或依赖注入 (DI) 容器。 容器本质上是一个工厂，它负责提供从中请求的类型的实例。 如果给定的类型已声明它具有依赖项，并且容器已经被配置为提供这些依赖类型，那么它将在创建请求实例时创建依赖项。通过这种方式，可以为类提供复杂的依赖关系图，而无需任何硬编码对象构造。 除了创建包含依赖项的对象外，容器通常还可以管理应用程序中的对象生命周期。

ASP.NET Core 包含一个简单的内置容器 (表示为`IServiceProvider`接口)，默认情况下，该容器支持构造函数注入，ASP.NET 可通过 DI 提供某些服务。 ASP.NET 的容器指其作为*服务*管理的类型。 本文其余部分中，*服务*指的是由 ASP.NET Core 的 IoC 容器管理的类型。 您可以在应用程序的`Startup`类中的`ConfigureServices`方法中配置内置容器的服务。

> [!NOTE]
> Martin Fowler 写了另一篇全面介绍[控制反转容器和依赖注入模式](https://www.martinfowler.com/articles/injection.html)的文章。 Microsoft 模式和实践也对[依赖关系注入](https://msdn.microsoft.com/library/hh323705.aspx)进行了很好的描述。

> [!NOTE]
> 本文介绍了适用于所有 ASP.NET 应用程序的依赖注入。 MVC 控制器中的依赖注入在[依赖注入和控制器](../mvc/controllers/dependency-injection.md)中进行介绍。

### <a name="constructor-injection-behavior"></a>构造函数注入行为

构造函数注入要求使用的构造函数为*公共*函数。 否则，应用程序会引发`InvalidOperationException`异常:

> 找不到类型 YourType 合适的构造函数。 请确保该类型是具体的服务注册的所有参数的公共构造函数。


构造函数注入要求只存在一个适用的构造函数。 支持构造函数重载，但其参数可以全部通过依赖注入来实现的重载只能存在一个。如果存在多个，应用程序将引发 `InvalidOperationException` 异常:

> 已在类型 YourType 中找到多个构造函数接受所有给定的自变量类型。 只应为一个适用的构造函数。

构造函数可以接受没有提供的依赖关系注入的参数，但它们必须支持默认值。 例如: 

```csharp
// throws InvalidOperationException: Unable to resolve service for type 'System.String'...
public CharactersController(ICharacterRepository characterRepository, string title)
{
    _characterRepository = characterRepository;
    _title = title;
}

// runs without error
public CharactersController(ICharacterRepository characterRepository, string title = "Characters")
{
    _characterRepository = characterRepository;
    _title = title;
}
```

## <a name="using-framework-provided-services"></a>使用框架提供的服务

`Startup` 类中的 `ConfigureServices` 方法负责定义应用程序将使用的服务，包括 Entity Framework Core 和 ASP.NET Core MVC 这样的平台特性。 最初，提供给 `ConfigureServices` 的 `IServiceCollection` 定义了以下服务（具体取决于[配置主机的方式](xref:fundamentals/hosting)）：

| 服务类型 | 生存期 |
| ----- | ------- |
| [Microsoft.AspNetCore.Hosting.IHostingEnvironment](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) | 单一实例 |
| [Microsoft.Extensions.Logging.ILoggerFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.iloggerfactory) | 单一实例 |
| [Microsoft.Extensions.Logging.ILogger&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | 暂时性故障 |
| [Microsoft.AspNetCore.Http.IHttpContextFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.ihttpcontextfactory) | 暂时性故障 |
| [Microsoft.Extensions.Options.IOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.ioptions-1) | 单一实例 |
| [System.Diagnostics.DiagnosticSource](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | 单一实例 |
| [System.Diagnostics.DiagnosticListener](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IStartupFilter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartupfilter) | 暂时性故障 |
| [Microsoft.Extensions.ObjectPool.ObjectPoolProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.objectpool.objectpoolprovider) | 单一实例 |
| [Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.iconfigureoptions-1) | 暂时性故障 |
| [Microsoft.AspNetCore.Hosting.Server.IServer](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.server.iserver) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IStartup](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartup) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IApplicationLifetime](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | 单一实例 |

下面是如何使用数等扩展方法的容器中添加其他服务的一个示例`AddDbContext`， `AddIdentity`，和`AddMvc`。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

ASP.NET 提供的功能和中间件（如 MVC）遵循使用单个 *AddServiceName* 扩展方法的约定来注册该功能所需的所有服务。

>[!TIP]
> 你可以请求中某些框架提供的服务`Startup`通过其参数列表的方法请参阅[应用程序启动](startup.md)有关详细信息。

## <a name="registering-your-own-services"></a>注册你自己的服务

可按如下方式注册自己的应用程序服务。 第一个泛型类型表示将从容器请求的类型（通常是一个接口）。 第二个泛型类型表示将由容器实例化并用于满足此类请求的具体类型。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> 每个 `services.Add<ServiceName>` 扩展方法添加（并可能配置）服务。 例如，`services.AddMvc()` 添加 MVC 需要的服务。 建议遵循此约定，将扩展方法放置在 `Microsoft.Extensions.DependencyInjection` 命名空间中，以封装服务注册的组。

`AddTransient` 方法用于将抽象类型映射到为每个需要它的对象分别实例化的具体服务。 这称为服务的*生存期*，其他生存期选项如下所述。 为注册的每个服务选择适当的生存期非常重要。 是否应该向每个请求它的类提供一个新的服务实例？是否在整个给定的 Web 请求中使用一个实例？或是否应该在应用程序生存期内使用单例？

在本文示例中，有一个显示字符名称的简单控制器，名为 `CharactersController`。 其 `Index` 方法会显示存储在应用程序中的当前字符列表，如果不存在，则使用少量字符初始化该集合。请注意，尽管此应用程序为其持久化使用Entity Framework Core和 `ApplicationDbContext`，但在控制器中没有任何明显的表现。 相反，特定的数据访问机制已经被抽象为一个接口，即 `ICharacterRepository`，它遵循[仓储模式](http://deviq.com/repository-pattern/)。通过构造函数请求 `ICharacterRepository` 实例，并将其分配给私有字段，然后根据需要使用它访问字符。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

`ICharacterRepository` 定义了控制器使用 `Character` 实例时需要的两种方法。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

此接口又由一个具体类型实现，即在运行时使用的 `CharacterRepository`。

> [!NOTE]
> DI 与 `CharacterRepository` 类一起使用的方式是一个通用模型，您可以为所有应用程序服务遵循此模型，而不仅仅在“仓储库”或数据访问类中。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

请注意，`CharacterRepository` 在其构造函数中请求一个 `ApplicationDbContext`。依赖注入以这种链式方式被使用并不罕见，（每个被请求的依赖进而请求它自己的依赖）。容器将负责解决图中所有的依赖关系，并返回完全解析后的服务。

> [!NOTE]
> 创建请求的对象，和它需要的所有对象，以及这些对象需要的所有对象，这有时被称为*对象图*。 同样，必须被解析的依赖关系的集合通常被称为*依赖关系树*或*依赖项关系图*。

在这种情况下，`ICharacterRepository`和`ApplicationDbContext` 必须在 `Startup` 类的 `ConfigureServices` 中的服务容器中注册。 `ApplicationDbContext` 通过调用扩展方法 `AddDbContext<T>` 进行配置。 下面的代码演示了 `CharacterRepository` 类型的注册。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

应使用 `Scoped` 生命周期将实体框架上下文添加到服务容器中。如果您使用上面所示的帮助方法，则会自动执行此操作。使用实体框架的仓储库应使用相同的生命周期。

>[!WARNING]
> 需要注意的主要危险是从单例解析 `Scoped` 服务。 在此类情况下，当处理后续请求时，服务可能会处于不正确的状态。

具有依赖的服务应将其注册到容器中。 如果服务的构造函数需要一个基元，例如 `string`，可以通过使用[选项模式和配置](configuration.md)来注入。

## <a name="service-lifetimes-and-registration-options"></a>服务生命周期和注册选项

可以使用以下生存期配置 ASP.NET 服务：

**暂时性故障**

瞬时生存期服务在每次请求时都会创建。 这种生存期适合轻量级、 无状态的服务。

**作用域**

作用域生存期服务以每个请求一次的方式创建。

**单例**

单例生存期服务在第一次被请求时或者 `ConfigureServices` 运行时（如果在其中指定实例）创建，然后每个后续请求使用同一实例。如果应用程序需要单例行为，建议允许服务容器管理服务的生存期，而不是实现单例设计模式并在类中自行管理对象的生存期。

可以使用多种方式容器注册服务。 我们已经看到了如何通过指定要使用的具体类型使用给定类型注册服务实现。 此外，可以指定工厂，然后将用于按需创建实例。 第三种方法是类型的直接指定要使用的实例，在其中用例容器将永远不会尝试创建实例 （也不会释放的实例）。

为了演示这些生存期和注册选项之间的差异，请考虑一个简单的接口，将一个或多个任务表示为具有唯一标识符 `OperationId` 的*操作*。根据此服务的生存期配置方式，容器将向请求的类提供相同或不同的实例。为了明确正在请求哪个生存期，我们将为每个生命周期选项创建一个类型：

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

我们使用单个类 `Operation` 来实现这些接口，它在构造函数中接受一个 `Guid`，如果没有提供，则使用一个新的 `Guid`。

接下来，在 `ConfigureServices` 中，根据其命名的生存期，将每个类型添加到容器中：

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

请注意，`IOperationSingletonInstance` 服务正在使用一个具有已知 ID `Guid.Empty` 的特定实例，因此可以明确何时在使用此类型（其 Guid 将全部为零）。我们已注册了依赖于每个其他 `Operation` 类型的 `OperationService`，因此对每个 Operation 类型来说，可以在请求中明确该服务是会获得与控制器相同的实例，还是获得一个新实例。此服务的全部作用就是将其依赖项作为属性公开，以便它们可以显示在视图中。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

为了演示对应用程序的各个独立请求之内和之间的对象生存期，该示例包含一个`OperationsController`，它请求每种 `IOperation` 类型以及一个 `OperationService`。`Index` 操作随后显示所有控制器和服务的 `OperationId` 值。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

现在两个单独的请求都对此控制器操作：

![显示暂时性、 作用域、 转变成 Singleton，和实例控制器和操作的第一个请求上的服务操作的操作 ID 值 (GUID) 的 Microsoft Edge 中运行的依赖关系注入示例 web 应用程序操作视图中。](dependency-injection/_static/lifetimes_request1.png)

![操作查看显示第二个请求的操作 ID 值。](dependency-injection/_static/lifetimes_request2.png)

观察哪个 `OperationId` 值会在一个请求之内和不同请求之间变化。

* *暂时性*对象始终是不同的; 为每个控制器和每个服务提供的新实例。

* *作用域*对象是否相同请求，但具有不同跨不同请求中

* *单例*对象对每个对象和每个请求都是相同的 (不管 `ConfigureServices` 是否提供了一个实例)

## <a name="request-services"></a>请求服务

来自 `HttpContext` 的 ASP.NET 请求中可用的服务通过 `RequestServices` 集合公开。

![HttpContext 请求服务 Intellisense 上下文对话框指出请求服务获取或设置 IServiceProvider 提供请求的服务容器的访问权限。](dependency-injection/_static/request-services.png)

请求服务表示在应用程序中配置和请求的服务。当对象指定依赖关系时，`RequestServices`（而不是 `ApplicationServices`）中的类型将满足这些要求。

通常情况下，不应直接使用这些属性，而应该通过类的构造函数来请求所需类的类型，并让框架注入这些依赖关系。 这将生成更易于测试且耦合更松散的类（请参阅[测试](../testing/index.md)）。

> [!NOTE]
> 与访问 `RequestServices` 集合相比，以构造函数参数的形式请求依赖项是更优先的选择。

## <a name="designing-your-services-for-dependency-injection"></a>设计能够进行依赖注入的服务

你应将自己的服务设计为可以使用依赖注入来获取其协作对象。这意味着避免在服务中使用有状态的静态方法调用（这会导致称为[静态粘贴](http://deviq.com/static-cling/)的代码异味）和依赖类的直接实例化。在选择是实例化一个类型还是通过依赖注入来请求它时，记住这个短语可能会有所帮助：[新增即粘附](https://ardalis.com/new-is-glue)。遵循[面向对象设计的SOLID原则](http://deviq.com/solid/)，你往往会获得小型、良好分解和易于测试的类。

如果发现你的类往往具有太多的依赖项需要注入怎么办？这通常表明你的类正试图做太多的事情，而且可能违反了 SRP-[单一责任原则](http://deviq.com/single-responsibility-principle/)。 看看是否可以通过将某些职责移动到一个新类来重构类。 请记住，你的 `Controller` 类应关注用户界面问题，因此业务规则和数据访问实现细节应保留在适用于这些[分离的关注点](http://deviq.com/separation-of-concerns/)的类中。

具体就数据访问而言，可以将 `DbContext` 注入到你的控制器（假设你已向`ConfigureServices` 中的服务容器中添加了 EF）。一些开发人员更愿意使用数据库的存储库接口而不是直接注入 `DbContext`。使用接口将数据访问逻辑封装在一个地方，可以最大程度减少数据库更改时需要更改的地方的数量。

### <a name="disposing-of-services"></a>释放服务

容器将为它创建的 `IDisposable` 类型调用 `Dispose`。但是，如果您自己将一个实例添加到容器，它将不会被释放。

示例:

```csharp
// Services implement IDisposable:
public class Service1 : IDisposable {}
public class Service2 : IDisposable {}
public class Service3 : IDisposable {}

public interface ISomeService {}
public class SomeServiceImplementation : ISomeService, IDisposable {}


public void ConfigureServices(IServiceCollection services)
{
    // container will create the instance(s) of these types and will dispose them
    services.AddScoped<Service1>();
    services.AddSingleton<Service2>();
    services.AddSingleton<ISomeService>(sp => new SomeServiceImplementation());

    // container did not create instance so it will NOT dispose it
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

> [!NOTE]
> 在 1.0 版中，容器将对*所有* `IDisposable` 对象调用 dispose，包括那些并非由它创建的对象。

## <a name="replacing-the-default-services-container"></a>替换默认服务容器

内置的服务容器旨在满足框架和在其上生成的大多数消费者应用程序的基本需求。 但是，开发人员可以使用自己喜欢的容器替换内置容器。 `ConfigureServices` 方法通常返回 `void`，但是，如果更改其签名以返回 `IServiceProvider`，则可以配置和返回不同的容器。有许多可用于 .NET 的 IOC 容器。在此示例中，使用 [Autofac](https://autofac.org/) 包。

首先，安装适当的容器程序包：

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

接下来，在 `ConfigureServices` 中配置容器并返回 `IServiceProvider`：

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // Add other framework services

    // Add Autofac
    var containerBuilder = new ContainerBuilder();
    containerBuilder.RegisterModule<DefaultModule>();
    containerBuilder.Populate(services);
    var container = containerBuilder.Build();
    return new AutofacServiceProvider(container);
}
```

> [!NOTE]
> 在使用第三方 DI 容器时，必须更改`ConfigureServices`，以便它返回`IServiceProvider`而不是`void`。

最后，在 `DefaultModule` 中正常配置 Autofac：

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

在运行时，将使用 Autofac 来解决类型，并将依赖关系注入。 [了解有关使用 Autofac 和 ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html)。

### <a name="thread-safety"></a>线程安全

需要是线程安全的单一实例服务。 如果单一实例服务暂时服务有依赖项，可能还需要暂时服务是线程安全具体取决于使用单一实例的方式。

## <a name="recommendations"></a>建议

在使用依赖关系注入，请记住以下建议：

* DI 是的具有复杂的依赖关系的对象。 控制器、 服务、 适配器和存储库是的可能添加到 DI 的对象的所有示例。

* 避免在 DI 中直接存储数据和配置。 例如，用户的购物车通常不应添加到服务容器。 配置应使用[选项模式](xref:fundamentals/configuration/options)。 同样，避免仅存在以允许访问某些其他对象的"数据持有者"对象。 它是更好的做法请求通过 DI，如有可能需要的实际项目。

* 避免静态访问服务。

* 避免在应用程序代码中使用服务定位。。

* 避免静态访问`HttpContext`。

> [!NOTE]
> 像任何一组建议一样，您可能会遇到需要忽略其中某一条的情况。我们发现例外情况很罕见 - 大多数是框架本身内部非常特殊的情况。

请记住，依赖注入是静态/全局对象访问模式的*替代*方法。如果将其与静态对象访问混合使用，则无法实现 DI 的优点。

## <a name="additional-resources"></a>其他资源

* [应用程序启动](startup.md)

* [测试](../testing/index.md)

* [在 ASP.NET Core 中使用依赖关系注入编写干净代码 (MSDN) ](https://msdn.microsoft.com/magazine/mt703433.aspx)

* [容器管理应用程序设计，作： 其中？ 容器属于](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)

* [显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)

* [反向的控件容器和依赖关系注入模式](https://www.martinfowler.com/articles/injection.html)(Fowler)
