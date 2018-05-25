---
title: 在 ASP.NET Core 依赖注入
author: ardalis
description: 了解 ASP.NET Core 如何实现依赖注入和如何使用它。
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/dependency-injection
ms.openlocfilehash: 067d9bd09f6d5e54bbafd953eea169d2df2be34e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="dependency-injection-in-aspnet-core"></a><span data-ttu-id="0fbf3-103">在 ASP.NET Core 依赖注入</span><span class="sxs-lookup"><span data-stu-id="0fbf3-103">Dependency injection in ASP.NET Core</span></span>

<a name="fundamentals-dependency-injection"></a>

<span data-ttu-id="0fbf3-104">作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="0fbf3-104">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="0fbf3-105">ASP.NET Core 的设计从头至尾以支持和利用依赖注入为目标。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-105">ASP.NET Core is designed from the ground up to support and leverage dependency injection.</span></span> <span data-ttu-id="0fbf3-106">ASP.NET Core 应用程序可以通过将内置框架服务注入 Startup 类的方法中来对其加以利用，应用程序服务也可以进行注入配置。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-106">ASP.NET Core applications can leverage built-in framework services by having them injected into methods in the Startup class, and application services can be configured for injection as well.</span></span> <span data-ttu-id="0fbf3-107">由 ASP.NET Core 提供的默认服务容器提供了一个最小功能集合，并非用于替换其他容器。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-107">The default services container provided by ASP.NET Core provides a minimal feature set and isn't intended to replace other containers.</span></span>

<span data-ttu-id="0fbf3-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0fbf3-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="0fbf3-109">什么是依赖注入？</span><span class="sxs-lookup"><span data-stu-id="0fbf3-109">What is dependency injection?</span></span>

<span data-ttu-id="0fbf3-110">依赖注入 (DI) 是一种用于在对象与其协作者或依赖项之间实现松散耦合的技术。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-110">Dependency injection (DI) is a technique for achieving loose coupling between objects and their collaborators, or dependencies.</span></span> <span data-ttu-id="0fbf3-111">该技术不是直接实例化协作者或使用静态引用，而是以某种方式向类提供该类执行其操作所需的对象。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-111">Rather than directly instantiating collaborators, or using static references, the objects a class needs in order to perform its actions are provided to the class in some fashion.</span></span> <span data-ttu-id="0fbf3-112">大多数情况下，类通过其构造函数声明它们的依赖项，从而允许它们遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-112">Most often, classes will declare their dependencies via their constructor, allowing them to follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span> <span data-ttu-id="0fbf3-113">此方法称为"构造函数注入"。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-113">This approach is known as "constructor injection".</span></span>

<span data-ttu-id="0fbf3-114">在遵循 DI 原则来设计类时，由于它们与其协作者没有直接的，硬编码的依赖关系，所以它们之间的耦合更为松散。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-114">When classes are designed with DI in mind, they're more loosely coupled because they don't have direct, hard-coded dependencies on their collaborators.</span></span> <span data-ttu-id="0fbf3-115">这遵循[依赖倒置原则](http://deviq.com/dependency-inversion-principle/)，其中指出 *"高级模块不应依赖于低级模块; 同时两者都应依赖于抽象"。*</span><span class="sxs-lookup"><span data-stu-id="0fbf3-115">This follows the [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/), which states that *"high level modules shouldn't depend on low level modules; both should depend on abstractions."*</span></span> <span data-ttu-id="0fbf3-116">类请求在该类被构造时提供给它们的抽象（通常是 `interfaces`），而不是引用特定的实现。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-116">Instead of referencing specific implementations, classes request abstractions (typically `interfaces`) which are provided to them when the class is constructed.</span></span> <span data-ttu-id="0fbf3-117">将依赖关系提取到接口中并将这些接口的实现作为参数提供也是[策略设计模式](http://deviq.com/strategy-design-pattern/) 的一个例子。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-117">Extracting dependencies into interfaces and providing implementations of these interfaces as parameters is also an example of the [Strategy design pattern](http://deviq.com/strategy-design-pattern/).</span></span>

<span data-ttu-id="0fbf3-118">当系统被设计为使用 DI 时，许多类通过其构造函数 （或属性）来请求它们的依赖项，所以有一个专门用来创建这些类以及它们相关的依赖项的类是很有帮助的。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-118">When a system is designed to use DI, with many classes requesting their dependencies via their constructor (or properties), it's helpful to have a class dedicated to creating these classes with their associated dependencies.</span></span> <span data-ttu-id="0fbf3-119">这些类统称为*容器*，或更具体地说，[控制反转 (IoC)](http://deviq.com/inversion-of-control/) 容器或依赖注入 (DI) 容器。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-119">These classes are referred to as *containers*, or more specifically, [Inversion of Control (IoC)](http://deviq.com/inversion-of-control/) containers or Dependency Injection (DI) containers.</span></span> <span data-ttu-id="0fbf3-120">容器本质上是一个工厂，它负责提供从中请求的类型的实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-120">A container is essentially a factory that's responsible for providing instances of types that are requested from it.</span></span> <span data-ttu-id="0fbf3-121">如果给定的类型已声明它具有依赖项，并且容器已经被配置为提供这些依赖类型，那么它将在创建请求实例时创建依赖项。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-121">If a given type has declared that it has dependencies, and the container has been configured to provide the dependency types, it will create the dependencies as part of creating the requested instance.</span></span> <span data-ttu-id="0fbf3-122">通过这种方式，可以为类提供复杂的依赖关系图，而无需任何硬编码对象构造。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-122">In this way, complex dependency graphs can be provided to classes without the need for any hard-coded object construction.</span></span> <span data-ttu-id="0fbf3-123">除了创建包含依赖项的对象外，容器通常还可以管理应用程序中的对象生命周期。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-123">In addition to creating objects with their dependencies, containers typically manage object lifetimes within the application.</span></span>

<span data-ttu-id="0fbf3-124">ASP.NET Core 包含一个简单的内置容器 (表示为 `IServiceProvider` 接口)，默认情况下，该容器支持构造函数注入，ASP.NET 可通过 DI 提供某些服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-124">ASP.NET Core includes a simple built-in container (represented by the `IServiceProvider` interface) that supports constructor injection by default, and ASP.NET makes certain services available through DI.</span></span> <span data-ttu-id="0fbf3-125">ASP.NET 的容器指其作为 *服务* 管理的类型。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-125">ASP.NET's container refers to the types it manages as *services*.</span></span> <span data-ttu-id="0fbf3-126">本文其余部分中，*服务* 指的是由 ASP.NET Core 的 IoC 容器管理的类型。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-126">Throughout the rest of this article, *services* will refer to types that are managed by ASP.NET Core's IoC container.</span></span> <span data-ttu-id="0fbf3-127">您可以在应用程序的 `Startup` 类中的 `ConfigureServices` 方法中配置内置容器的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-127">You configure the built-in container's services in the `ConfigureServices` method in your application's `Startup` class.</span></span>

> [!NOTE]
> <span data-ttu-id="0fbf3-128">Martin Fowler 写了另一篇全面介绍 [控制反转容器和依赖注入模式](https://www.martinfowler.com/articles/injection.html) 的文章。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-128">Martin Fowler has written an extensive article on [Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html).</span></span> <span data-ttu-id="0fbf3-129">Microsoft 模式和实践也对 [依赖关系注入](https://msdn.microsoft.com/library/hh323705.aspx) 进行了很好的描述。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-129">Microsoft Patterns and Practices also has a great description of [Dependency Injection](https://msdn.microsoft.com/library/hh323705.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0fbf3-130">本文介绍了适用于所有 ASP.NET 应用程序的依赖注入。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-130">This article covers Dependency Injection as it applies to all ASP.NET applications.</span></span> <span data-ttu-id="0fbf3-131">[依赖关系注入和控制器](../mvc/controllers/dependency-injection.md)中介绍了 MVC 控制器内的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-131">Dependency Injection within MVC controllers is covered in [Dependency Injection and Controllers](../mvc/controllers/dependency-injection.md).</span></span>

### <a name="constructor-injection-behavior"></a><span data-ttu-id="0fbf3-132">构造函数注入行为</span><span class="sxs-lookup"><span data-stu-id="0fbf3-132">Constructor injection behavior</span></span>

<span data-ttu-id="0fbf3-133">构造函数注入要求相关构造函数是公共的。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-133">Constructor injection requires that the constructor in question be *public*.</span></span> <span data-ttu-id="0fbf3-134">否则，应用程序会引发 `InvalidOperationException` 异常:</span><span class="sxs-lookup"><span data-stu-id="0fbf3-134">Otherwise, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="0fbf3-135">找不到适合类型 YourType 的构造函数。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-135">A suitable constructor for type 'YourType' couldn't be located.</span></span> <span data-ttu-id="0fbf3-136">请确保该类型是具体的，并为公共构造函数的所有参数注册服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-136">Ensure the type is concrete and services are registered for all parameters of a public constructor.</span></span>

<span data-ttu-id="0fbf3-137">构造函数注入要求只存在一个适用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-137">Constructor injection requires that only one applicable constructor exist.</span></span> <span data-ttu-id="0fbf3-138">支持构造函数重载，但其参数可以全部通过依赖注入来实现的重载只能存在一个。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-138">Constructor overloads are supported, but only one overload can exist whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="0fbf3-139">如果存在多个，应用程序将引发 `InvalidOperationException` 异常:</span><span class="sxs-lookup"><span data-stu-id="0fbf3-139">If more than one exists, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="0fbf3-140">已在类型 YourType 中找到多个接受所有给定的参数类型的构造函数。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-140">Multiple constructors accepting all given argument types have been found in type 'YourType'.</span></span> <span data-ttu-id="0fbf3-141">应该只有一个适用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-141">There should only be one applicable constructor.</span></span>

<span data-ttu-id="0fbf3-142">构造函数可以接受依赖注入没有提供的参数，但这些参数必须支持默认值。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-142">Constructors can accept arguments that are not provided by dependency injection, but these must support default values.</span></span> <span data-ttu-id="0fbf3-143">例如:</span><span class="sxs-lookup"><span data-stu-id="0fbf3-143">For example:</span></span>

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

## <a name="using-framework-provided-services"></a><span data-ttu-id="0fbf3-144">使用框架提供的服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-144">Using framework-provided services</span></span>

<span data-ttu-id="0fbf3-145">`Startup` 类中的 `ConfigureServices` 方法负责定义应用程序将使用的服务，包括 Entity Framework Core 和 ASP.NET Core MVC 之类的平台功能。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-145">The `ConfigureServices` method in the `Startup` class is responsible for defining the services the application will use, including platform features like Entity Framework Core and ASP.NET Core MVC.</span></span> <span data-ttu-id="0fbf3-146">最初，提供给 `ConfigureServices` 的 `IServiceCollection` 定义了以下服务（具体取决于[配置主机的方式](xref:fundamentals/host/index)）：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-146">Initially, the `IServiceCollection` provided to `ConfigureServices` has the following services defined (depending on [how the host was configured](xref:fundamentals/host/index)):</span></span>

| <span data-ttu-id="0fbf3-147">服务类型</span><span class="sxs-lookup"><span data-stu-id="0fbf3-147">Service Type</span></span> | <span data-ttu-id="0fbf3-148">生存期</span><span class="sxs-lookup"><span data-stu-id="0fbf3-148">Lifetime</span></span> |
| ----- | ------- |
| [<span data-ttu-id="0fbf3-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="0fbf3-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) | <span data-ttu-id="0fbf3-150">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-150">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-151">Microsoft.Extensions.Logging.ILoggerFactory</span><span class="sxs-lookup"><span data-stu-id="0fbf3-151">Microsoft.Extensions.Logging.ILoggerFactory</span></span>](/dotnet/api/microsoft.extensions.logging.iloggerfactory) | <span data-ttu-id="0fbf3-152">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-152">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="0fbf3-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.logging.ilogger) | <span data-ttu-id="0fbf3-154">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-154">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span><span class="sxs-lookup"><span data-stu-id="0fbf3-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | <span data-ttu-id="0fbf3-156">暂时</span><span class="sxs-lookup"><span data-stu-id="0fbf3-156">Transient</span></span> |
| [<span data-ttu-id="0fbf3-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span><span class="sxs-lookup"><span data-stu-id="0fbf3-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span></span>](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextfactory) | <span data-ttu-id="0fbf3-158">暂时</span><span class="sxs-lookup"><span data-stu-id="0fbf3-158">Transient</span></span> |
| [<span data-ttu-id="0fbf3-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="0fbf3-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.ioptions-1) | <span data-ttu-id="0fbf3-160">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-160">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-161">System.Diagnostics.DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="0fbf3-161">System.Diagnostics.DiagnosticSource</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | <span data-ttu-id="0fbf3-162">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-162">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-163">System.Diagnostics.DiagnosticListener</span><span class="sxs-lookup"><span data-stu-id="0fbf3-163">System.Diagnostics.DiagnosticListener</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | <span data-ttu-id="0fbf3-164">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-164">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span><span class="sxs-lookup"><span data-stu-id="0fbf3-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) | <span data-ttu-id="0fbf3-166">暂时</span><span class="sxs-lookup"><span data-stu-id="0fbf3-166">Transient</span></span> |
| [<span data-ttu-id="0fbf3-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span><span class="sxs-lookup"><span data-stu-id="0fbf3-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span></span>](/dotnet/api/microsoft.extensions.objectpool.objectpoolprovider) | <span data-ttu-id="0fbf3-168">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-168">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="0fbf3-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) | <span data-ttu-id="0fbf3-170">暂时</span><span class="sxs-lookup"><span data-stu-id="0fbf3-170">Transient</span></span> |
| [<span data-ttu-id="0fbf3-171">Microsoft.AspNetCore.Hosting.Server.IServer</span><span class="sxs-lookup"><span data-stu-id="0fbf3-171">Microsoft.AspNetCore.Hosting.Server.IServer</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) | <span data-ttu-id="0fbf3-172">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-172">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-173">Microsoft.AspNetCore.Hosting.IStartup</span><span class="sxs-lookup"><span data-stu-id="0fbf3-173">Microsoft.AspNetCore.Hosting.IStartup</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartup) | <span data-ttu-id="0fbf3-174">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-174">Singleton</span></span> |
| [<span data-ttu-id="0fbf3-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="0fbf3-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | <span data-ttu-id="0fbf3-176">单一实例</span><span class="sxs-lookup"><span data-stu-id="0fbf3-176">Singleton</span></span> |

<span data-ttu-id="0fbf3-177">下面的示例介绍了如何使用多个扩展方法（如 `AddDbContext`、`AddIdentity` 和 `AddMvc`）将附加服务添加到容器中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-177">Below is an example of how to add additional services to the container using a number of extension methods like `AddDbContext`, `AddIdentity`, and `AddMvc`.</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

<span data-ttu-id="0fbf3-178">ASP.NET 提供的功能和中间件（如 MVC），遵循使用单个 AddServiceName 扩展方法注册该功能请求的所有服务的约定。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-178">The features and middleware provided by ASP.NET, such as MVC, follow a convention of using a single Add*ServiceName* extension method to register all of the services required by that feature.</span></span>

> [!TIP]
> <span data-ttu-id="0fbf3-179">你可以通过其参数列表在 `Startup` 方法内请求某些框架提供的服务，请参阅[应用程序启动](startup.md)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-179">You can request certain framework-provided services within `Startup` methods through their parameter lists - see [Application Startup](startup.md) for more details.</span></span>

## <a name="registering-services"></a><span data-ttu-id="0fbf3-180">注册服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-180">Registering services</span></span>

<span data-ttu-id="0fbf3-181">可以按如下方式注册自己的应用程序服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-181">You can register your own application services as follows.</span></span> <span data-ttu-id="0fbf3-182">第一个泛型类型表示将从容器请求的类型（通常是一个接口）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-182">The first generic type represents the type (typically an interface) that will be requested from the container.</span></span> <span data-ttu-id="0fbf3-183">第二个泛型类型表示将由容器实例化并用于满足此类请求的具体类型。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-183">The second generic type represents the concrete type that will be instantiated by the container and used to fulfill such requests.</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> <span data-ttu-id="0fbf3-184">每个 `services.Add<ServiceName>` 扩展方法添加（并可能配置）服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-184">Each `services.Add<ServiceName>` extension method adds (and potentially configures) services.</span></span> <span data-ttu-id="0fbf3-185">例如，`services.AddMvc()` 添加 MVC 需要的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-185">For example, `services.AddMvc()` adds the services MVC requires.</span></span> <span data-ttu-id="0fbf3-186">建议遵循此约定，将扩展方法放置在 `Microsoft.Extensions.DependencyInjection` 命名空间中，以封装服务注册的组。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-186">It's recommended that you follow this convention, placing extension methods in the `Microsoft.Extensions.DependencyInjection` namespace, to encapsulate groups of service registrations.</span></span>

<span data-ttu-id="0fbf3-187">`AddTransient` 方法用于将抽象类型映射到为每个需要它的对象分别实例化的具体服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-187">The `AddTransient` method is used to map abstract types to concrete services that are instantiated separately for every object that requires it.</span></span> <span data-ttu-id="0fbf3-188">这称为服务的 *生存期*，其他生存期选项如下所述。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-188">This is known as the service's *lifetime*, and additional lifetime options are described below.</span></span> <span data-ttu-id="0fbf3-189">为注册的每个服务选择适当的生存期非常重要。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-189">It's important to choose an appropriate lifetime for each of the services you register.</span></span> <span data-ttu-id="0fbf3-190">是否应该向每个请求它的类提供一个新的服务实例？</span><span class="sxs-lookup"><span data-stu-id="0fbf3-190">Should a new instance of the service be provided to each class that requests it?</span></span> <span data-ttu-id="0fbf3-191">是否在整个给定的 Web 请求中使用一个实例？</span><span class="sxs-lookup"><span data-stu-id="0fbf3-191">Should one instance be used throughout a given web request?</span></span> <span data-ttu-id="0fbf3-192">或是否应该在应用程序生存期内使用单例？</span><span class="sxs-lookup"><span data-stu-id="0fbf3-192">Or should a single instance be used for the lifetime of the application?</span></span>

<span data-ttu-id="0fbf3-193">在本文示例中，有一个显示字符名称的简单控制器，名为 `CharactersController`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-193">In the sample for this article, there's a simple controller that displays character names, called `CharactersController`.</span></span> <span data-ttu-id="0fbf3-194">其 `Index` 方法会显示存储在应用程序中的当前字符列表，如果不存在，则使用少量字符初始化该集合。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-194">Its `Index` method displays the current list of characters that have been stored in the application, and initializes the collection with a handful of characters if none exist.</span></span> <span data-ttu-id="0fbf3-195">请注意，尽管此应用程序为其持久化使用Entity Framework Core和 `ApplicationDbContext`，但在控制器中没有任何明显的表现。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-195">Note that although this application uses Entity Framework Core and the `ApplicationDbContext` class for its persistence, none of that's apparent in the controller.</span></span> <span data-ttu-id="0fbf3-196">相反，特定的数据访问机制已经被抽象为一个接口，即 `ICharacterRepository`，它遵循 [仓储模式](http://deviq.com/repository-pattern/)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-196">Instead, the specific data access mechanism has been abstracted behind an interface, `ICharacterRepository`, which follows the [repository pattern](http://deviq.com/repository-pattern/).</span></span> <span data-ttu-id="0fbf3-197">通过构造函数请求 `ICharacterRepository` 实例，并将其分配给私有字段，然后根据需要使用它访问字符。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-197">An instance of `ICharacterRepository` is requested via the constructor and assigned to a private field, which is then used to access characters as necessary.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

<span data-ttu-id="0fbf3-198">`ICharacterRepository` 定义了控制器使用 `Character` 实例时需要的两种方法。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-198">The `ICharacterRepository` defines the two methods the controller needs to work with `Character` instances.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

<span data-ttu-id="0fbf3-199">此接口又由一个具体类型实现，即在运行时使用的 `CharacterRepository`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-199">This interface is in turn implemented by a concrete type, `CharacterRepository`, that's used at runtime.</span></span>

> [!NOTE]
> <span data-ttu-id="0fbf3-200">DI 与 `CharacterRepository` 类一起使用的方式是一个通用模型，您可以为所有应用程序服务遵循此模型，而不仅仅在“仓储库”或数据访问类中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-200">The way DI is used with the `CharacterRepository` class is a general model you can follow for all of your application services, not just in "repositories" or data access classes.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

<span data-ttu-id="0fbf3-201">请注意，`CharacterRepository` 在其构造函数中请求一个 `ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-201">Note that `CharacterRepository` requests an `ApplicationDbContext` in its constructor.</span></span> <span data-ttu-id="0fbf3-202">依赖注入以这种链式方式被使用并不罕见，（每个被请求的依赖进而请求它自己的依赖）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-202">It's not unusual for dependency injection to be used in a chained fashion like this, with each requested dependency in turn requesting its own dependencies.</span></span> <span data-ttu-id="0fbf3-203">容器将负责解决图中所有的依赖关系，并返回完全解析后的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-203">The container is responsible for resolving all of the dependencies in the graph and returning the fully resolved service.</span></span>

> [!NOTE]
> <span data-ttu-id="0fbf3-204">创建请求的对象，和它需要的所有对象，以及这些对象需要的所有对象，这有时被称为 *对象图*。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-204">Creating the requested object, and all of the objects it requires, and all of the objects those require, is sometimes referred to as an *object graph*.</span></span> <span data-ttu-id="0fbf3-205">同样，必须被解析的依赖关系的集合通常被称为*依赖关系树*或*依赖项关系图*。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-205">Likewise, the collective set of dependencies that must be resolved is typically referred to as a *dependency tree* or *dependency graph*.</span></span>

<span data-ttu-id="0fbf3-206">在这种情况下，`Startup` 和 `ApplicationDbContext` 必须在 `ICharacterRepository` 类的 `ConfigureServices` 中的服务容器中注册。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-206">In this case, both `ICharacterRepository` and in turn `ApplicationDbContext` must be registered with the services container in `ConfigureServices` in `Startup`.</span></span> <span data-ttu-id="0fbf3-207">`ApplicationDbContext` 通过调用扩展方法 `AddDbContext<T>` 进行配置。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-207">`ApplicationDbContext` is configured with the call to the extension method `AddDbContext<T>`.</span></span> <span data-ttu-id="0fbf3-208">下面的代码演示了 `CharacterRepository` 类型的注册。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-208">The following code shows the registration of the `CharacterRepository` type.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

<span data-ttu-id="0fbf3-209">应使用 `Scoped` 生命周期将实体框架上下文添加到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-209">Entity Framework contexts should be added to the services container using the `Scoped` lifetime.</span></span> <span data-ttu-id="0fbf3-210">如果您使用上面所示的帮助方法，则会自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-210">This is taken care of automatically if you use the helper methods as shown above.</span></span> <span data-ttu-id="0fbf3-211">使用实体框架的仓储库应使用相同的生命周期。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-211">Repositories that will make use of Entity Framework should use the same lifetime.</span></span>

> [!WARNING]
> <span data-ttu-id="0fbf3-212">需要注意的主要危险是从单例解析 `Scoped` 服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-212">The main danger to be wary of is resolving a `Scoped` service from a singleton.</span></span> <span data-ttu-id="0fbf3-213">在此类情况下，当处理后续请求时，服务可能会处于不正确的状态。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-213">It's likely in such a case that the service will have incorrect state when processing subsequent requests.</span></span>

<span data-ttu-id="0fbf3-214">具有依赖关系的服务应在容器中对它们进行注册。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-214">Services that have dependencies should register them in the container.</span></span> <span data-ttu-id="0fbf3-215">如果服务构造函数需要一个基元（如 `string`），可使用[配置](xref:fundamentals/configuration/index)和[选项模式](xref:fundamentals/configuration/options)将其注入。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-215">If a service's constructor requires a primitive, such as a `string`, this can be injected by using [configuration](xref:fundamentals/configuration/index) and the [options pattern](xref:fundamentals/configuration/options).</span></span>

## <a name="service-lifetimes-and-registration-options"></a><span data-ttu-id="0fbf3-216">服务生存期和注册选项</span><span class="sxs-lookup"><span data-stu-id="0fbf3-216">Service lifetimes and registration options</span></span>

<span data-ttu-id="0fbf3-217">可使用以下生存期配置 ASP.NET 服务：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-217">ASP.NET services can be configured with the following lifetimes:</span></span>

<span data-ttu-id="0fbf3-218">**暂时**</span><span class="sxs-lookup"><span data-stu-id="0fbf3-218">**Transient**</span></span>

<span data-ttu-id="0fbf3-219">暂时生存期服务是每次请求时创建的。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-219">Transient lifetime services are created each time they're requested.</span></span> <span data-ttu-id="0fbf3-220">这种生存期适合轻量级、 无状态的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-220">This lifetime works best for lightweight, stateless services.</span></span>

<span data-ttu-id="0fbf3-221">**作用域（Scoped）**</span><span class="sxs-lookup"><span data-stu-id="0fbf3-221">**Scoped**</span></span>

<span data-ttu-id="0fbf3-222">作用域生存期服务以每个请求一次的方式创建。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-222">Scoped lifetime services are created once per request.</span></span>

> [!WARNING]
> <span data-ttu-id="0fbf3-223">如果在中间件内使用有作用域的服务，请将该服务注入至 `Invoke` 或 `InvokeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-223">If you're using a scoped service in a middleware, inject the service into the `Invoke` or `InvokeAsync` method.</span></span> <span data-ttu-id="0fbf3-224">请不要通过构造函数注入进行注入，因为它会强制服务的行为与单一实例类似。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-224">Don't inject via constructor injection because it forces the service to behave like a singleton.</span></span>

<span data-ttu-id="0fbf3-225">**单例**</span><span class="sxs-lookup"><span data-stu-id="0fbf3-225">**Singleton**</span></span>

<span data-ttu-id="0fbf3-226">单例生存期服务在第一次被请求时或者 `ConfigureServices` 运行时（如果在其中指定实例）创建，然后每个后续请求使用同一实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-226">Singleton lifetime services are created the first time they're requested (or when `ConfigureServices` is run if you specify an instance there) and then every subsequent request will use the same instance.</span></span> <span data-ttu-id="0fbf3-227">如果应用程序需要单例行为，建议允许服务容器管理服务的生存期，而不是实现单例设计模式并在类中自行管理对象的生存期。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-227">If your application requires singleton behavior, allowing the services container to manage the service's lifetime is recommended instead of implementing the singleton design pattern and managing your object's lifetime in the class yourself.</span></span>

<span data-ttu-id="0fbf3-228">服务可以使用多种方式注册到容器中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-228">Services can be registered with the container in several ways.</span></span> <span data-ttu-id="0fbf3-229">我们已经看到了如何通过指定要使用的具体类型来注册一个给定类型的服务实现。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-229">We have already seen how to register a service implementation with a given type by specifying the concrete type to use.</span></span> <span data-ttu-id="0fbf3-230">此外，可以指定一个工厂，然后将其用于按需创建实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-230">In addition, a factory can be specified, which will then be used to create the instance on demand.</span></span> <span data-ttu-id="0fbf3-231">第三种方法是直接指定要使用的类型的实例，在这种情况下，容器将永远不会尝试创建实例（也不会释放实例）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-231">The third approach is to directly specify the instance of the type to use, in which case the container will never attempt to create an instance (nor will it dispose of the instance).</span></span>

<span data-ttu-id="0fbf3-232">为了演示这些生存期和注册选项之间的差异，请考虑一个简单的接口，将一个或多个任务表示为具有唯一标识符 `OperationId` 的*操作*。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-232">To demonstrate the difference between these lifetime and registration options, consider a simple interface that represents one or more tasks as an *operation* with a unique identifier, `OperationId`.</span></span> <span data-ttu-id="0fbf3-233">根据此服务的生存期配置方式，容器将向请求的类提供相同或不同的实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-233">Depending on how we configure the lifetime for this service, the container will provide either the same or different instances of the service to the requesting class.</span></span> <span data-ttu-id="0fbf3-234">为了明确正在请求哪个生存期，我们将为每个生命周期选项创建一个类型：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-234">To make it clear which lifetime is being requested, we will create one type per lifetime option:</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

<span data-ttu-id="0fbf3-235">我们使用单个类 `Operation` 来实现这些接口，它在构造函数中接受一个 `Guid`，如果没有提供，则使用一个新的 `Guid`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-235">We implement these interfaces using a single class, `Operation`, that accepts a `Guid` in its constructor, or uses a new `Guid` if none is provided.</span></span>

<span data-ttu-id="0fbf3-236">接下来，在 `ConfigureServices` 中，根据其命名的生存期，将每个类型添加到容器中：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-236">Next, in `ConfigureServices`, each type is added to the container according to its named lifetime:</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

<span data-ttu-id="0fbf3-237">请注意，`IOperationSingletonInstance` 服务正在使用一个具有已知 ID `Guid.Empty` 的特定实例，因此可以明确何时在使用此类型（其 Guid 将全部为零）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-237">Note that the `IOperationSingletonInstance` service is using a specific instance with a known ID of `Guid.Empty` so it will be clear when this type is in use (its Guid will be all zeroes).</span></span> <span data-ttu-id="0fbf3-238">我们已注册了依赖于每个其他 `Operation` 类型的 `OperationService`，因此对每个 Operation 类型来说，可以在请求中明确该服务是会获得与控制器相同的实例，还是获得一个新实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-238">We have also registered an `OperationService` that depends on each of the other `Operation` types, so that it will be clear within a request whether this service is getting the same instance as the controller, or a new one, for each operation type.</span></span> <span data-ttu-id="0fbf3-239">此服务的全部作用就是将其依赖项作为属性公开，以便它们可以显示在视图中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-239">All this service does is expose its dependencies as properties, so they can be displayed in the view.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

<span data-ttu-id="0fbf3-240">为了演示对应用程序的各个独立请求之内和之间的对象生存期，该示例包含一个`OperationsController`，它请求每种 `IOperation` 类型以及一个 `OperationService`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-240">To demonstrate the object lifetimes within and between separate individual requests to the application, the sample includes an `OperationsController` that requests each kind of `IOperation` type as well as an `OperationService`.</span></span> <span data-ttu-id="0fbf3-241">`Index` 操作随后显示所有控制器和服务的 `OperationId` 值。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-241">The `Index` action then displays all of the controller's and service's `OperationId` values.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

<span data-ttu-id="0fbf3-242">现在对该控制器操作发起了两个单独的请求：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-242">Now two separate requests are made to this controller action:</span></span>

![Microsoft Edge 中运行的依赖关系注入示例 Web 应用程序的操作视图对第一个请求显示暂时、限定、单一实例、实例控制器和操作服务操作的操作 ID 值 (GUID)。](dependency-injection/_static/lifetimes_request1.png)

![操作视图对第二个请求显示操作 ID 值。](dependency-injection/_static/lifetimes_request2.png)

<span data-ttu-id="0fbf3-245">观察请求内和请求之间哪些 `OperationId` 值不同。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-245">Observe which of the `OperationId` values vary within a request, and between requests.</span></span>

* <span data-ttu-id="0fbf3-246">暂时对象始终不同；向每个控制器和每项服务提供一个新的实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-246">*Transient* objects are always different; a new instance is provided to every controller and every service.</span></span>

* <span data-ttu-id="0fbf3-247">限定对象在请求内是相同的，但在不同的请求中是不同的</span><span class="sxs-lookup"><span data-stu-id="0fbf3-247">*Scoped* objects are the same within a request, but different across different requests</span></span>

* <span data-ttu-id="0fbf3-248">*单例* 对象对每个对象和每个请求都是相同的 (不管 `ConfigureServices` 是否提供了一个实例)</span><span class="sxs-lookup"><span data-stu-id="0fbf3-248">*Singleton* objects are the same for every object and every request (regardless of whether an instance is provided in `ConfigureServices`)</span></span>

## <a name="resolve-a-scoped-service-within-the-application-scope"></a><span data-ttu-id="0fbf3-249">解析应用程序作用域中有作用域的服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-249">Resolve a scoped service within the application scope</span></span>

<span data-ttu-id="0fbf3-250">采用 [IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope) 创建 [IServiceScope ](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope)，以解析应用作用域中有作用域的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-250">Create an [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope) with [IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope) to resolve a scoped service within the app's scope.</span></span> <span data-ttu-id="0fbf3-251">此方法可以用于在启动时访问有作用域的服务以便运行初始化任务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-251">This approach is useful to access a scoped service at startup to run initialization tasks.</span></span> <span data-ttu-id="0fbf3-252">以下示例演示如何在 `Program.Main` 中获取 `MyScopedService` 的上下文：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-252">The following example shows how to obtain a context for the `MyScopedService` in `Program.Main`:</span></span>

```csharp
public static void Main(string[] args)
{
    var host = BuildWebHost(args);

    using (var serviceScope = host.Services.CreateScope())
    {
        var services = serviceScope.ServiceProvider;

        try
        {
            var serviceContext = services.GetRequiredService<MyScopedService>();
            // Use the context here
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred.");
        }
    }

    host.Run();
}
```

## <a name="scope-validation"></a><span data-ttu-id="0fbf3-253">作用域验证</span><span class="sxs-lookup"><span data-stu-id="0fbf3-253">Scope validation</span></span>

<span data-ttu-id="0fbf3-254">如果在 ASP.NET Core 2.0 或更高版本上的开发环境中运行应用，默认的服务提供程序会执行检查，从而确认以下内容：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-254">When the app is running in the Development environment on ASP.NET Core 2.0 or later, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="0fbf3-255">没有从根服务提供程序直接或间接解析到有作用域的服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-255">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="0fbf3-256">未将有作用域的服务直接或间接注入到单一实例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-256">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="0fbf3-257">调用 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) 时，会创建根服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-257">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="0fbf3-258">在启动提供程序和应用时，根服务提供程序的生存期对应于应用/服务的生存期，并在关闭应用时释放。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-258">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="0fbf3-259">有作用域的服务由创建它们的容器释放。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-259">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="0fbf3-260">如果作用域创建于根容器，则该服务的生存会有效地提升至单一实例，因为根容器只会在应用/服务关闭时将其释放。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-260">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="0fbf3-261">验证服务作用域，将在调用 `BuildServiceProvider` 时收集这类情况。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-261">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="0fbf3-262">有关详细信息，请参阅 [Web 托管主题中的作用域验证](xref:fundamentals/host/web-host#scope-validation)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-262">For more information, see [Scope validation in the Web Host topic](xref:fundamentals/host/web-host#scope-validation).</span></span>

## <a name="request-services"></a><span data-ttu-id="0fbf3-263">请求服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-263">Request Services</span></span>

<span data-ttu-id="0fbf3-264">在 `HttpContext` 中的 ASP.NET 请求内可用的服务通过 `RequestServices` 集合进行公开。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-264">The services available within an ASP.NET request from `HttpContext` are exposed through the `RequestServices` collection.</span></span>

![HttpContext 请求服务 Intellisense 上下文对话框指出请求服务可获取或设置对请求的服务容器提供访问权限的 IServiceProvider。](dependency-injection/_static/request-services.png)

<span data-ttu-id="0fbf3-266">请求服务表示你作为应用程序的一部分配置的服务和请求。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-266">Request Services represent the services you configure and request as part of your application.</span></span> <span data-ttu-id="0fbf3-267">当对象指定依赖关系时，`RequestServices`（而不是 `ApplicationServices`）中的类型将满足这些要求。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-267">When your objects specify dependencies, these are satisfied by the types found in `RequestServices`, not `ApplicationServices`.</span></span>

<span data-ttu-id="0fbf3-268">通常情况下，不应直接使用这些属性，而应该通过类的构造函数来请求所需类的类型，并让框架注入这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-268">Generally, you shouldn't use these properties directly, preferring instead to request the types your classes you require via your class's constructor, and letting the framework inject these dependencies.</span></span> <span data-ttu-id="0fbf3-269">这将生成更易于测试且耦合更松散的类（请参阅[测试和调试](xref:testing/index)）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-269">This yields classes that are easier to test (see [Test and debug](xref:testing/index)) and are more loosely coupled.</span></span>

> [!NOTE]
> <span data-ttu-id="0fbf3-270">与访问 `RequestServices` 集合相比，以构造函数参数的形式请求依赖项是更优先的选择。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-270">Prefer requesting dependencies as constructor parameters to accessing the `RequestServices` collection.</span></span>

## <a name="designing-services-for-dependency-injection"></a><span data-ttu-id="0fbf3-271">设计能够进行依赖注入的服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-271">Designing services for dependency injection</span></span>

<span data-ttu-id="0fbf3-272">你应将自己的服务设计为可以使用依赖注入来获取其协作对象。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-272">You should design your services to use dependency injection to get their collaborators.</span></span> <span data-ttu-id="0fbf3-273">这意味着避免在服务中使用有状态的静态方法调用（这会导致称为[静态粘贴](http://deviq.com/static-cling/) 的代码异味）和依赖类的直接实例化。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-273">This means avoiding the use of stateful static method calls (which result in a code smell known as [static cling](http://deviq.com/static-cling/)) and the direct instantiation of dependent classes within your services.</span></span> <span data-ttu-id="0fbf3-274">在选择是实例化一个类型还是通过依赖注入来请求它时，记住这个短语可能会有所帮助：[新增即粘附](https://ardalis.com/new-is-glue)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-274">It may help to remember the phrase, [New is Glue](https://ardalis.com/new-is-glue), when choosing whether to instantiate a type or to request it via dependency injection.</span></span> <span data-ttu-id="0fbf3-275">遵循[面向对象设计的SOLID原则](http://deviq.com/solid/)，你往往会获得小型、良好分解和易于测试的类。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-275">By following the [SOLID Principles of Object Oriented Design](http://deviq.com/solid/), your classes will naturally tend to be small, well-factored, and easily tested.</span></span>

<span data-ttu-id="0fbf3-276">如果发现你的类往往具有太多的依赖项需要注入怎么办？</span><span class="sxs-lookup"><span data-stu-id="0fbf3-276">What if you find that your classes tend to have way too many dependencies being injected?</span></span> <span data-ttu-id="0fbf3-277">这通常表明你的类正试图做太多的事情，而且可能违反了 SRP-[单一责任原则](http://deviq.com/single-responsibility-principle/)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-277">This is generally a sign that your class is trying to do too much, and is probably violating SRP - the [Single Responsibility Principle](http://deviq.com/single-responsibility-principle/).</span></span> <span data-ttu-id="0fbf3-278">看看是否可以通过将某些职责移动到一个新类来重构类。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-278">See if you can refactor the class by moving some of its responsibilities into a new class.</span></span> <span data-ttu-id="0fbf3-279">请记住，你的 `Controller` 类应关注用户界面问题，因此业务规则和数据访问实现细节应保留在适用于这些[分离的关注点](http://deviq.com/separation-of-concerns/) 的类中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-279">Keep in mind that your `Controller` classes should be focused on UI concerns, so business rules and data access implementation details should be kept in classes appropriate to these [separate concerns](http://deviq.com/separation-of-concerns/).</span></span>

<span data-ttu-id="0fbf3-280">具体就数据访问而言，可以将 `DbContext` 注入到你的控制器（假设你已向 `ConfigureServices` 中的服务容器中添加了 EF）。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-280">With regards to data access specifically, you can inject the `DbContext` into your controllers (assuming you've added EF to the services container in `ConfigureServices`).</span></span> <span data-ttu-id="0fbf3-281">一些开发人员更愿意使用数据库的存储库接口而不是直接注入 `DbContext`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-281">Some developers prefer to use a repository interface to the database rather than injecting the `DbContext` directly.</span></span> <span data-ttu-id="0fbf3-282">使用接口将数据访问逻辑封装于一处可以最大程序减少数据更改时需要更改的位置数量。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-282">Using an interface to encapsulate the data access logic in one place can minimize how many places you will have to change when your database changes.</span></span>

### <a name="disposing-of-services"></a><span data-ttu-id="0fbf3-283">释放服务</span><span class="sxs-lookup"><span data-stu-id="0fbf3-283">Disposing of services</span></span>

<span data-ttu-id="0fbf3-284">容器将为其创建的 `IDisposable` 类型调用 `Dispose`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-284">The container will call `Dispose` for `IDisposable` types it creates.</span></span> <span data-ttu-id="0fbf3-285">但是，如果您自己将一个实例添加到容器，它将不会被释放。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-285">However, if you add an instance to the container yourself, it will not be disposed.</span></span>

<span data-ttu-id="0fbf3-286">示例:</span><span class="sxs-lookup"><span data-stu-id="0fbf3-286">Example:</span></span>

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
> <span data-ttu-id="0fbf3-287">在 1.0 版中，容器将对*所有* `IDisposable` 对象调用 dispose，包括那些并非由它创建的对象。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-287">In version 1.0, the container called dispose on *all* `IDisposable` objects, including those it didn't create.</span></span>

## <a name="replacing-the-default-services-container"></a><span data-ttu-id="0fbf3-288">替换默认服务容器</span><span class="sxs-lookup"><span data-stu-id="0fbf3-288">Replacing the default services container</span></span>

<span data-ttu-id="0fbf3-289">内置服务容器专门服务框架和基于其上生成的大多数应用程序的基本需求。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-289">The built-in services container is meant to serve the basic needs of the framework and most consumer applications built on it.</span></span> <span data-ttu-id="0fbf3-290">但是，开发人员可以使用自己喜欢的容器替换内置容器。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-290">However, developers can replace the built-in container with their preferred container.</span></span> <span data-ttu-id="0fbf3-291">`ConfigureServices` 方法通常返回 `void`，但是，如果更改其签名以返回 `IServiceProvider`，则可以配置和返回不同的容器。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-291">The `ConfigureServices` method typically returns `void`, but if its signature is changed to return `IServiceProvider`, a different container can be configured and returned.</span></span> <span data-ttu-id="0fbf3-292">有许多可用于 .NET 的 IOC 容器。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-292">There are many IOC containers available for .NET.</span></span> <span data-ttu-id="0fbf3-293">在此示例中，将使用 [Autofac](https://autofac.org/) 包。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-293">In this example, the [Autofac](https://autofac.org/) package is used.</span></span>

<span data-ttu-id="0fbf3-294">首先，安装适当的容器包：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-294">First, install the appropriate container package(s):</span></span>

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

<span data-ttu-id="0fbf3-295">接下来，在 `ConfigureServices` 中配置容器并返回 `IServiceProvider`：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-295">Next, configure the container in `ConfigureServices` and return an `IServiceProvider`:</span></span>

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
> <span data-ttu-id="0fbf3-296">使用第三方 DI 容器时，必须更改 `ConfigureServices`，以便其返回 `IServiceProvider`，而不是 `void`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-296">When using a third-party DI container, you must change `ConfigureServices` so that it returns `IServiceProvider` instead of `void`.</span></span>

<span data-ttu-id="0fbf3-297">最后，将 Autofac 在 `DefaultModule` 中配置为正常：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-297">Finally, configure Autofac as normal in `DefaultModule`:</span></span>

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

<span data-ttu-id="0fbf3-298">在运行时，将使用 Autofac 来解析类型，并注入依赖。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-298">At runtime, Autofac will be used to resolve types and inject dependencies.</span></span> <span data-ttu-id="0fbf3-299">[了解有关使用 Autofac 和 ASP.NET Core的更多信息](http://docs.autofac.org/en/latest/integration/aspnetcore.html)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-299">[Learn more about using Autofac and ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html).</span></span>

### <a name="thread-safety"></a><span data-ttu-id="0fbf3-300">线程安全</span><span class="sxs-lookup"><span data-stu-id="0fbf3-300">Thread safety</span></span>

<span data-ttu-id="0fbf3-301">单例服务需要是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-301">Singleton services need to be thread safe.</span></span> <span data-ttu-id="0fbf3-302">如果单例服务依赖于一个瞬时服务，那么瞬时服务可能也需要是线程安全的，具体取决于单例使用它的方式。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-302">If a singleton service has a dependency on a transient service, the transient service may also need to be thread safe depending how it's used by the singleton.</span></span>

## <a name="recommendations"></a><span data-ttu-id="0fbf3-303">建议</span><span class="sxs-lookup"><span data-stu-id="0fbf3-303">Recommendations</span></span>

<span data-ttu-id="0fbf3-304">使用依赖注入时，请记住以下建议：</span><span class="sxs-lookup"><span data-stu-id="0fbf3-304">When working with dependency injection, keep the following recommendations in mind:</span></span>

* <span data-ttu-id="0fbf3-305">DI 适用于具有复杂的依赖关系的对象。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-305">DI is for objects that have complex dependencies.</span></span> <span data-ttu-id="0fbf3-306">控制器、 服务、 适配器和仓储都是可能添加到 DI 中的对象示例。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-306">Controllers, services, adapters, and repositories are all examples of objects that might be added to DI.</span></span>

* <span data-ttu-id="0fbf3-307">避免在 DI 中直接存储数据和配置。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-307">Avoid storing data and configuration directly in DI.</span></span> <span data-ttu-id="0fbf3-308">例如，用户的购物车通常不应添加到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-308">For example, a user's shopping cart shouldn't typically be added to the services container.</span></span> <span data-ttu-id="0fbf3-309">配置应使用 [选项模型](xref:fundamentals/configuration/options)。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-309">Configuration should use the [options pattern](xref:fundamentals/configuration/options).</span></span> <span data-ttu-id="0fbf3-310">同样，避免"数据持有者"对象，也就是仅仅为实现对某些其他对象的访问而存在的对象。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-310">Similarly, avoid "data holder" objects that only exist to allow access to some other object.</span></span> <span data-ttu-id="0fbf3-311">如果可能，最好通过 DI 请求所需的实际项目。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-311">It's better to request the actual item needed via DI, if possible.</span></span>

* <span data-ttu-id="0fbf3-312">避免静态访问服务。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-312">Avoid static access to services.</span></span>

* <span data-ttu-id="0fbf3-313">应用程序代码中避免服务位置。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-313">Avoid service location in your application code.</span></span>

* <span data-ttu-id="0fbf3-314">避免静态访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-314">Avoid static access to `HttpContext`.</span></span>

<span data-ttu-id="0fbf3-315">如所有建议组合一样，你可能会遇到必须忽略一个的情况。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-315">Like all sets of recommendations, you may encounter situations where ignoring one is required.</span></span> <span data-ttu-id="0fbf3-316">我们发现例外情况很罕见 - 大多数是框架本身内部非常特殊的情况。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-316">We have found exceptions to be rare -- mostly very special cases within the framework itself.</span></span>

<span data-ttu-id="0fbf3-317">依赖注入是静态/全局对象访问模式的替代方法。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-317">Dependency injection is an *alternative* to static/global object access patterns.</span></span> <span data-ttu-id="0fbf3-318">如果将其与静态对象访问混合使用，则可能无法实现 DI 的优点。</span><span class="sxs-lookup"><span data-stu-id="0fbf3-318">You may not be able to realize the benefits of DI if you mix it with static object access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fbf3-319">其他资源</span><span class="sxs-lookup"><span data-stu-id="0fbf3-319">Additional resources</span></span>

* [<span data-ttu-id="0fbf3-320">视图中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="0fbf3-320">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
* [<span data-ttu-id="0fbf3-321">控制器中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="0fbf3-321">Dependency injection into controllers</span></span>](xref:mvc/controllers/dependency-injection)
* [<span data-ttu-id="0fbf3-322">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="0fbf3-322">Dependency injection in requirement handlers</span></span>](xref:security/authorization/dependencyinjection)
* [<span data-ttu-id="0fbf3-323">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="0fbf3-323">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="0fbf3-324">测试和调试</span><span class="sxs-lookup"><span data-stu-id="0fbf3-324">Test and debug</span></span>](xref:testing/index)
* [<span data-ttu-id="0fbf3-325">基于工厂的中间件激活</span><span class="sxs-lookup"><span data-stu-id="0fbf3-325">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
* [<span data-ttu-id="0fbf3-326">在 ASP.NET Core 中使用依赖关系注入编写干净代码 (MSDN) </span><span class="sxs-lookup"><span data-stu-id="0fbf3-326">Writing Clean Code in ASP.NET Core with Dependency Injection (MSDN)</span></span>](https://msdn.microsoft.com/magazine/mt703433.aspx)
* <span data-ttu-id="0fbf3-327">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)（容器托管的应用程序设计，序言：容器属于何处？）</span><span class="sxs-lookup"><span data-stu-id="0fbf3-327">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)</span></span>
* <span data-ttu-id="0fbf3-328">[Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显式依赖关系原则）</span><span class="sxs-lookup"><span data-stu-id="0fbf3-328">[Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)</span></span>
* <span data-ttu-id="0fbf3-329">[Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html)（控制反转容器和依赖关系注入模式）</span><span class="sxs-lookup"><span data-stu-id="0fbf3-329">[Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html) (Fowler)</span></span>
