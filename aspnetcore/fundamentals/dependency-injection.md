---
title: "ASP.NET Core 中的依赖关系注入"
author: ardalis
description: "了解 ASP.NET Core 如何实现依赖关系注入，以及如何使用它。"
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/dependency-injection
ms.openlocfilehash: acbce5d139da0acc0870a9cf23a779bf27699a61
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="dependency-injection-in-aspnet-core"></a>ASP.NET Core 中的依赖关系注入

<a name="fundamentals-dependency-injection"></a>

作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)

ASP.NET Core 从头开始进行设计，以支持和利用依赖关系注入。 ASP.NET Core 应用程序可以通过将内置框架服务注入启动类的方法中来利用它，并且还可为注入配置应用程序服务。 ASP.NET Core 提供的默认服务容器可提供一个最小功能集，且并非用来替换其他容器。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-is-dependency-injection"></a>什么是依存关系注入？

依赖关系注入 (DI) 是一种用于实现对象及其协作者或依赖关系之间的松散耦合的技术。 不是直接实例化协作者或使用静态引用，而是以某种方式向类提供其执行操作所需的对象。 大多数情况下，类将通过其构造函数声明其依赖关系，使它们遵循 [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显示依赖关系原则）。 此方法称为“构造函数注入”。

记住，使用 DI 设计类时，它们以更加松散的方式进行耦合，因为它们对协作者没有直接的、硬编码依赖关系。 这遵循 [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/)（依赖关系反转原则），其中指出“高级别模块不应依赖低级别模块，它们都应依赖抽象”。 构建类时，类请求向它们提供抽象（通常是 `interfaces`），而不是引用特定实现。 将依赖关系提取到接口并提供这些接口的实现作为参数也是 [Strategy design pattern](http://deviq.com/strategy-design-pattern/)（策略设计模式）的一个示例。

当系统被设计为使用 DI 时，由于许多类通过其构造函数（或属性）请求依赖关系，具有一个专门使用其关联的依赖关系创建这些类的类非常有用。 这些类称为容器，或者更具体地说，称为 [Inversion of Control (IoC)](http://deviq.com/inversion-of-control/)（控制反转 (IoC)）容器或依赖关系注入 (DI) 容器。 容器本质上是一个工厂，负责提供从其中请求的类型的实例。 如果给定的类型已声明它具有依赖关系，并且配置了容器以提供依赖关系类型，它将在创建所请求实例的过程中创建创建赖关系。 通过这种方式，可以向类提供复杂的依赖关系图，而无需任何硬编码对象构造。 除使用其依赖关系创建对象，容器通常还可管理应用程序内的对象生存期。

ASP.NET 核心包括默认支持构造函数注入的简单内置容器（由 `IServiceProvider` 接口表示），并且 ASP.NET Core 通过 DI 使某些服务可用。 ASP.NET 的容器指的是它作为服务进行管理的类型。 在本文其余部分，服务指的是 ASP.NET Core 的 IoC 容器管理的类型。 你可在应用程序的 `Startup` 类的 `ConfigureServices` 方法中配置该内置容器服务。

> [!NOTE]
> Martin Fowler 写了一篇关于 [Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html)（控制反转容器和依赖关系注入模式）的文章。 Microsoft 模式和做法也很好地介绍了[依赖关系注入](https://msdn.microsoft.com/library/hh323705.aspx)。

> [!NOTE]
> 本文介绍依赖关系注入，因其适用于所有 ASP.NET 应用程序。 [依赖关系注入和控制器](../mvc/controllers/dependency-injection.md)中介绍了 MVC 控制器内的依赖关系注入。

### <a name="constructor-injection-behavior"></a>构造函数注入行为

构造函数注入要求相关构造函数是公共的。 否则，你的应用将引发 `InvalidOperationException`：

> 找不到适合“YourType”类型的构造函数。 请确保该类型是具体的，并且针对公共构造函数的所有参数注册了服务。


构造函数注入要求只存在一个适用的构造函数。 支持构造函数重载，但只能存在一个重载，其参数全部可以通过依赖关系注入来实现。 如果存在多个重载，应用将引发 `InvalidOperationException`：

> 类型“YourType”中找到多个接受所有给定参数类型的构造函数。 应该只有一个适用的构造函数。

构造函数可以接受依赖关系注入未提供的参数，但它们必须支持默认值。 例如:

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

`Startup` 类中的 `ConfigureServices` 方法负责定义应用程序将使用的服务，包括 Entity Framework Core 和 ASP.NET Core MVC 之类的平台功能。 最初，向 `ConfigureServices` 提供的 `IServiceCollection` 定义了以下服务（具体取决于[主机的配置方式](xref:fundamentals/hosting)）：

| 服务类型 | 生存期 |
| ----- | ------- |
| [Microsoft.AspNetCore.Hosting.IHostingEnvironment](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) | 单一实例 |
| [Microsoft.Extensions.Logging.ILoggerFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.iloggerfactory) | 单一实例 |
| [Microsoft.Extensions.Logging.ILogger&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | 暂时 |
| [Microsoft.AspNetCore.Http.IHttpContextFactory](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.ihttpcontextfactory) | 暂时 |
| [Microsoft.Extensions.Options.IOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.ioptions-1) | 单一实例 |
| [System.Diagnostics.DiagnosticSource](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | 单一实例 |
| [System.Diagnostics.DiagnosticListener](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IStartupFilter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartupfilter) | 暂时 |
| [Microsoft.Extensions.ObjectPool.ObjectPoolProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.objectpool.objectpoolprovider) | 单一实例 |
| [Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.iconfigureoptions-1) | 暂时 |
| [Microsoft.AspNetCore.Hosting.Server.IServer](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.server.iserver) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IStartup](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartup) | 单一实例 |
| [Microsoft.AspNetCore.Hosting.IApplicationLifetime](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | 单一实例 |

下面的示例介绍了如何使用多个扩展方法（如 `AddDbContext`、`AddIdentity` 和 `AddMvc`）将附加服务添加到容器中。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

ASP.NET 提供的功能和中间件（如 MVC），遵循使用单个 AddServiceName 扩展方法注册该功能请求的所有服务的约定。

>[!TIP]
> 你可以通过其参数列表在 `Startup` 方法内请求某些框架提供的服务，请参阅[应用程序启动](startup.md)了解详细信息。

## <a name="registering-services"></a>注册服务

可以按如下方式注册自己的应用程序服务。 第一种泛型类型表示将从容器请求的类型（通常指接口）。 第二种泛型类型表示将由容器实例化并用来满足此类请求的具体类型。

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> 每个 `services.Add<ServiceName>` 扩展方法都将添加（并可能配置）服务。 例如，`services.AddMvc()` 将添加 MVC 需要的服务。 建议你遵循此约定，将扩展方法放置于 `Microsoft.Extensions.DependencyInjection` 命名空间，以封装服务注册组。

`AddTransient` 方法用于将抽象类型映射到针对需要它的每个对象单独实例化的具体服务。 这称为服务的生存期，其他生存期选项如下所述。 针对注册的每项服务，请务必选择相应的生存期。 是否应该向请求新服务实例的每个类提供该实例？ 是否应该在给定的 Web 请求的整个过程使用实例？ 或者，是否应该对应用程序的生存期使用单个实例？

在本文示例中，有一个显示字符名称的简单控制器，名为 `CharactersController`。 如果不存在，其 `Index` 方法将显示已存储在应用程序中的字符的当前列表，并使用少量字符初始化集合。 注意：尽管此应用程序使用 Entity Framework Core 和 `ApplicationDbContext` 类用于其暂留，但在控制器中均不明显。 相反，已在接口 `ICharacterRepository` 后面将特定数据访问机制抽象化，这遵循[Repository Pattern](http://deviq.com/repository-pattern/)（存储库模式）。 通过构造函数请求 `ICharacterRepository` 的实例，并分配给私有字段，然后根据需要将其用于访问字符。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

`ICharacterRepository` 定义控制器处理 `Character` 实例所需的两个方法。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

此接口反过来由运行时所用的具体类型 `CharacterRepository` 实现。

> [!NOTE]
> `CharacterRepository` 类使用 DI 的方式是你可针对所有应用程序服务遵循的常规模型，而不仅仅在“存储库”或数据访问类中。

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

注意：`CharacterRepository` 的构造函数中请求一个 `ApplicationDbContext`。 以此链接方式使用依赖关系注入很常见，因此每个被请求的依赖关系反过来都会请求其自己的依赖关系。 容器负责解析关系图中的所有依赖关系，并返回完全解析后的服务。

> [!NOTE]
> 创建所请求对象、其需要的所有对象以及它们需要的所有对象，有时称为对象图。 同样，通常将必须解析的一组依赖关系统称为依赖关系树或依赖关系图。

在这种情况下，必须向 `Startup` 的 `ConfigureServices` 中的服务容器注册 `ICharacterRepository` 和反过来的 `ApplicationDbContext`。 通过调用扩展方法 `AddDbContext<T>` 配置 `ApplicationDbContext`。 下面的代码演示 `CharacterRepository` 类型的注册。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

必须使用 `Scoped` 生存期将 Entity Framework 上下文添加到服务容器。 如果如上所述使用帮助程序方法，将自动进行处理。 将使用 Entity Framework 的存储库应该使用相同的生存期。

>[!WARNING]
> 要谨慎的主要危险是从单一实例中解析 `Scoped` 服务。 此类情况下，处理后续请求时，很可能服务状态不正确。

具有依赖关系的服务应在容器中对它们进行注册。 如果服务构造函数需要一个基元（如 `string`），可使用[配置](xref:fundamentals/configuration/index)和[选项模式](xref:fundamentals/configuration/options)将其注入。

## <a name="service-lifetimes-and-registration-options"></a>服务生存期和注册选项

可使用以下生存期配置 ASP.NET 服务：

**暂时**

暂时生存期服务是每次请求时创建的。 此生存期最适合轻型、无状态服务。

**限定**

限定生存期服务每个请求创建一次。

**单一实例**

单一实例生存期服务在首次请求时（或者如果在其中指定实例，则为 `ConfigureServices` 运行时）进行创建，然后所有后续请求都将使用相同实例。 如果应用程序要求单一实例行为，建议允许服务容器管理服务的生存期，而不是实现单一实例设计模式和自行管理类中对象的生存期。

可通过多种方式向容器注册服务。 我们已经了解了如何通过指定要使用的具体类型向给定的类型注册服务实现。 此外，还可指定工厂，将用来按需创建实例。 第三种方法是直接指定要使用的类型的实例，在这种情况下，容器永远不会尝试创建实例（也不会释放该实例）。

若要演示这些生存期和注册选项之间的差异，请考虑将表示一个或多个任务的简单接口视为带唯一标识符`OperationId` 的操作。 容器将向请求类提供相同或不同的服务实例，具体取决于配置此服务的生存期的方式。 为弄清楚正在请求的是哪个生存期，将每个生存期选项创建一种类型：

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

我们使用单一类 `Operation`（其构造函数接受 `Guid`），或使用新的 `Guid`（如果未提供任何类）实现这些接口。

接下来，在 `ConfigureServices` 中，将根据其命名生存期向容器添加每种类型：

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

注意，`IOperationSingletonInstance` 服务使用的是已知 ID 为 `Guid.Empty` 的特定实例，因此当使用此类型时会很清楚（其 GUID 全部为零）。 我们还注册了依赖所有其他 `Operation` 类型的 `OperationService`，因此请求中将很清楚此服务是否为每种操作类型获取与控制器相同的实例或者新实例。 此服务只需将其依赖关系公开为属性，便可在视图中显示。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

若要演示应用程序的各个请求内和各个请求之间的对象生存期，示例将包括请求每种 `IOperation` 类型的 `OperationsController` 以及 `OperationService`。 然后，`Index` 操作将显示所有控制器及服务的 `OperationId` 值。

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

现在，向此控制器操作提了如下两个单独请求：

![Microsoft Edge 中运行的依赖关系注入示例 Web 应用程序的操作视图对第一个请求显示暂时、限定、单一实例、实例控制器和操作服务操作的操作 ID 值 (GUID)。](dependency-injection/_static/lifetimes_request1.png)

![操作视图对第二个请求显示操作 ID 值。](dependency-injection/_static/lifetimes_request2.png)

观察请求内和请求之间哪些 `OperationId` 值不同。

* 暂时对象始终不同；向每个控制器和每项服务提供一个新的实例。

* 限定对象在请求内是相同的，但在不同的请求中是不同的

* 单一实例对象对每个对象和每个请求都是相同的（无论实例是否在 `ConfigureServices` 中提供）

## <a name="request-services"></a>请求服务

在 `HttpContext` 中的 ASP.NET 请求内可用的服务通过 `RequestServices` 集合进行公开。

![HttpContext 请求服务 Intellisense 上下文对话框指出请求服务可获取或设置对请求的服务容器提供访问权限的 IServiceProvider。](dependency-injection/_static/request-services.png)

请求服务表示你作为应用程序的一部分配置的服务和请求。 对象指定依赖关系时，由 `RequestServices`（而不是 `ApplicationServices`）中找到的类型满足这些依赖关系。

通常情况下，不应直接使用这些属性，而应该先通过类的构造函数请求其所需的类型，并允许框架注入这些依赖关系。 这可生成易于测试（请参阅[测试](../testing/index.md)）并且耦合更加松散的类。

> [!NOTE]
> 优先请求依赖关系作为构造函数参数，用于访问 `RequestServices` 集合。

## <a name="designing-services-for-dependency-injection"></a>设计适用于依赖关系注入的服务

应将服务设计为使用依赖关系注入获取其协作者。 这意味着避免使用有状态静态方法调用（将生成代码告知，称为[静态粘贴](http://deviq.com/static-cling/)），以及服务中相关类的直接实例化。 选择是否实例化类型或通过依赖关系注入请求它时，记住短语 [New is Glue](https://ardalis.com/new-is-glue)（新增即是粘附）可能有用。 按照[面向对象的设计的 SOLID 原则](http://deviq.com/solid/)，你的类将自然倾向于小型、构造良好和易测试。

如果发现类有太多的依赖关系要注入时怎么办？ 这通常表示类尝试执行过多操作，并可能违反 SRP，即[Single Responsibility Principle](http://deviq.com/single-responsibility-principle/)（单一责任原则）。 确认是否可以通过将其部分职责移到新类来重构该类。 请记住，`Controller` 类应该关注 UI 问题，因此业务规则和数据访问实现详细信息应保存在这些[单独问题](http://deviq.com/separation-of-concerns/)相应的类中。

具体而言，对于数据访问，可以将 `DbContext` 注入控制器（假设已向 `ConfigureServices` 中的服务容器添加 EF）。 部分开发者宁愿使用数据库的存储库接口，而不是直接注入 `DbContext`。 使用接口将数据访问逻辑封装于一处可以最大程序减少数据更改时需要更改的位置数量。

### <a name="disposing-of-services"></a>释放服务

容器将为其创建的 `IDisposable` 类型调用 `Dispose`。 但是，如果自行向容器添加实例，容器不会释放。

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

    // container didn't create instance so it will NOT dispose it
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

> [!NOTE]
> 在 1.0 版中，容器对所有 `IDisposable` 对象调用了 dispose，包括未创建的对象。

## <a name="replacing-the-default-services-container"></a>替换默认服务容器

内置服务容器专门服务框架和基于其上生成的大多数应用程序的基本需求。 但是，开发者可将内置容器替换为其首选容器。 `ConfigureServices` 方法通常会返回 `void`，但如果其签名更改为返回 `IServiceProvider`，可配置和返回不同的容器。 具有适用于 .NET 的多个 IOC 容器。 在此示例中，将使用 [Autofac](https://autofac.org/) 包。

首先，安装适当的容器包：

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
> 使用第三方 DI 容器时，必须更改 `ConfigureServices`，以便其返回 `IServiceProvider`，而不是 `void`。

最后，将 Autofac 在 `DefaultModule` 中配置为正常：

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

运行时，Autofac 将用来解析类型和注入依赖关系。 [深入了解如何使用 Autofac 和 ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html)。

### <a name="thread-safety"></a>线程安全

单一实例服务需要处于线程安全。 如果单一实例服务与暂时服务存在依赖关系，暂时服务可能也需要线程安全，具体取决于使用单一实例的方式。

## <a name="recommendations"></a>建议

使用依赖关系注入时，请记住以下建议：

* DI 适用于具有复杂依赖关系的对象。 控制器、服务、适配器和存储库是可添加到 DI 的对象的所有示例。

* 避免在 DI 中直接存储和配置数据。 例如，用户的购物车通常不应添加到服务容器中。 配置应该使用[选项模式](xref:fundamentals/configuration/options)。 同样，避免仅存在允许访部分其他对象的“数据持有者”对象。 如果可能，最好通过 DI 请求所需的实际项目。

* 避免静态访问服务。

* 应用程序代码中避免服务位置。

* 避免静态访问 `HttpContext`。

> [!NOTE]
> 如所有建议组合一样，你可能会遇到必须忽略一个的情况。 我们发现异常很少见，大多数是框架本身中非常特殊的情况。

记住，依赖关系注入是静态/局部对象访问模式的备用方案。 如果将 DI 与静态对象访问混合，你将无法实现其好处。

## <a name="additional-resources"></a>其他资源

* [应用程序启动](xref:fundamentals/startup)
* [测试](xref:testing/index)
* [使用依赖关系注入在 ASP.NET Core 中编写干净代码 (MSDN)](https://msdn.microsoft.com/magazine/mt703433.aspx)
* [Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)（容器托管的应用程序设计，序言：容器属于何处？）
* [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显式依赖关系原则）
* [Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html)（控制反转容器和依赖关系注入模式）
