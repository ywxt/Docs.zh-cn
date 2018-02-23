---
title: "在 ASP.NET Core 依赖注入"
author: ardalis
description: "了解 ASP.NET Core 如何实现依赖注入和如何使用它。"
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/dependency-injection
ms.openlocfilehash: 43c937ff9631be3edc1f95b3689650e4574abfbd
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="dependency-injection-in-aspnet-core"></a><span data-ttu-id="6b433-103">在 ASP.NET Core 依赖注入</span><span class="sxs-lookup"><span data-stu-id="6b433-103">Dependency injection in ASP.NET Core</span></span>

<a name="fundamentals-dependency-injection"></a>

<span data-ttu-id="6b433-104">作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="6b433-104">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="6b433-105">ASP.NET Core 的设计从头至尾以支持和利用依赖注入为目标。</span><span class="sxs-lookup"><span data-stu-id="6b433-105">ASP.NET Core is designed from the ground up to support and leverage dependency injection.</span></span> <span data-ttu-id="6b433-106">ASP.NET Core 应用程序可以通过将内置框架服务注入 Startup 类的方法中来对其加以利用，应用程序服务也可以进行注入配置。</span><span class="sxs-lookup"><span data-stu-id="6b433-106">ASP.NET Core applications can leverage built-in framework services by having them injected into methods in the Startup class, and application services can be configured for injection as well.</span></span> <span data-ttu-id="6b433-107">由 ASP.NET Core 提供的默认服务容器提供了一个最小功能集合，并非用于替换其他容器。</span><span class="sxs-lookup"><span data-stu-id="6b433-107">The default services container provided by ASP.NET Core provides a minimal feature set and isn't intended to replace other containers.</span></span>

<span data-ttu-id="6b433-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="6b433-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="6b433-109">什么是依赖注入？</span><span class="sxs-lookup"><span data-stu-id="6b433-109">What is dependency injection?</span></span>

<span data-ttu-id="6b433-110">依赖注入 (DI) 是一种用于在对象与其协作者或依赖项之间实现松散耦合的技术。</span><span class="sxs-lookup"><span data-stu-id="6b433-110">Dependency injection (DI) is a technique for achieving loose coupling between objects and their collaborators, or dependencies.</span></span> <span data-ttu-id="6b433-111">该技术不是直接实例化协作者或使用静态引用，而是以某种方式向类提供该类执行其操作所需的对象。</span><span class="sxs-lookup"><span data-stu-id="6b433-111">Rather than directly instantiating collaborators, or using static references, the objects a class needs in order to perform its actions are provided to the class in some fashion.</span></span> <span data-ttu-id="6b433-112">大多数情况下，类通过其构造函数声明它们的依赖项，从而允许它们遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。</span><span class="sxs-lookup"><span data-stu-id="6b433-112">Most often, classes will declare their dependencies via their constructor, allowing them to follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span> <span data-ttu-id="6b433-113">此方法称为"构造函数注入"。</span><span class="sxs-lookup"><span data-stu-id="6b433-113">This approach is known as "constructor injection".</span></span>

<span data-ttu-id="6b433-114">在遵循 DI 原则来设计类时，由于它们与其协作者没有直接的，硬编码的依赖关系，所以它们之间的耦合更为松散。</span><span class="sxs-lookup"><span data-stu-id="6b433-114">When classes are designed with DI in mind, they're more loosely coupled because they don't have direct, hard-coded dependencies on their collaborators.</span></span> <span data-ttu-id="6b433-115">这遵循[依赖倒置原则](http://deviq.com/dependency-inversion-principle/)，其中指出*"高级模块不应依赖于低级模块; 同时两者都应依赖于抽象"。*</span><span class="sxs-lookup"><span data-stu-id="6b433-115">This follows the [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/), which states that *"high level modules shouldn't depend on low level modules; both should depend on abstractions."*</span></span> <span data-ttu-id="6b433-116">类请求在该类被构造时提供给它们的抽象（通常是 `interfaces`），而不是引用特定的实现。</span><span class="sxs-lookup"><span data-stu-id="6b433-116">Instead of referencing specific implementations, classes request abstractions (typically `interfaces`) which are provided to them when the class is constructed.</span></span> <span data-ttu-id="6b433-117">将依赖关系提取到接口中并将这些接口的实现作为参数提供也是[策略设计模式](http://deviq.com/strategy-design-pattern/) 的一个例子。</span><span class="sxs-lookup"><span data-stu-id="6b433-117">Extracting dependencies into interfaces and providing implementations of these interfaces as parameters is also an example of the [Strategy design pattern](http://deviq.com/strategy-design-pattern/).</span></span>

<span data-ttu-id="6b433-118">当系统被设计为使用 DI 时，许多类通过其构造函数 （或属性）来请求它们的依赖项，所以有一个专门用来创建这些类以及它们相关的依赖项的类是很有帮助的。</span><span class="sxs-lookup"><span data-stu-id="6b433-118">When a system is designed to use DI, with many classes requesting their dependencies via their constructor (or properties), it's helpful to have a class dedicated to creating these classes with their associated dependencies.</span></span> <span data-ttu-id="6b433-119">这些类统称为*容器*，或更具体地说，[控制反转 (IoC)](http://deviq.com/inversion-of-control/) 容器或依赖注入 (DI) 容器。</span><span class="sxs-lookup"><span data-stu-id="6b433-119">These classes are referred to as *containers*, or more specifically, [Inversion of Control (IoC)](http://deviq.com/inversion-of-control/) containers or Dependency Injection (DI) containers.</span></span> <span data-ttu-id="6b433-120">容器本质上是一个工厂，它负责提供从中请求的类型的实例。</span><span class="sxs-lookup"><span data-stu-id="6b433-120">A container is essentially a factory that's responsible for providing instances of types that are requested from it.</span></span> <span data-ttu-id="6b433-121">如果给定的类型已声明它具有依赖项，并且容器已经被配置为提供这些依赖类型，那么它将在创建请求实例时创建依赖项。</span><span class="sxs-lookup"><span data-stu-id="6b433-121">If a given type has declared that it has dependencies, and the container has been configured to provide the dependency types, it will create the dependencies as part of creating the requested instance.</span></span> <span data-ttu-id="6b433-122">通过这种方式，可以为类提供复杂的依赖关系图，而无需任何硬编码对象构造。</span><span class="sxs-lookup"><span data-stu-id="6b433-122">In this way, complex dependency graphs can be provided to classes without the need for any hard-coded object construction.</span></span> <span data-ttu-id="6b433-123">除了创建包含依赖项的对象外，容器通常还可以管理应用程序中的对象生命周期。</span><span class="sxs-lookup"><span data-stu-id="6b433-123">In addition to creating objects with their dependencies, containers typically manage object lifetimes within the application.</span></span>

<span data-ttu-id="6b433-124">ASP.NET Core 包含一个简单的内置容器 (表示为 `IServiceProvider` 接口)，默认情况下，该容器支持构造函数注入，ASP.NET 可通过 DI 提供某些服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-124">ASP.NET Core includes a simple built-in container (represented by the `IServiceProvider` interface) that supports constructor injection by default, and ASP.NET makes certain services available through DI.</span></span> <span data-ttu-id="6b433-125">ASP.NET 的容器指其作为 *服务* 管理的类型。</span><span class="sxs-lookup"><span data-stu-id="6b433-125">ASP.NET's container refers to the types it manages as *services*.</span></span> <span data-ttu-id="6b433-126">本文其余部分中，*服务* 指的是由 ASP.NET Core 的 IoC 容器管理的类型。</span><span class="sxs-lookup"><span data-stu-id="6b433-126">Throughout the rest of this article, *services* will refer to types that are managed by ASP.NET Core's IoC container.</span></span> <span data-ttu-id="6b433-127">您可以在应用程序的 `Startup` 类中的 `ConfigureServices` 方法中配置内置容器的服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-127">You configure the built-in container's services in the `ConfigureServices` method in your application's `Startup` class.</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-128">Martin Fowler 写了另一篇全面介绍 [控制反转容器和依赖注入模式](https://www.martinfowler.com/articles/injection.html) 的文章。</span><span class="sxs-lookup"><span data-stu-id="6b433-128">Martin Fowler has written an extensive article on [Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html).</span></span> <span data-ttu-id="6b433-129">Microsoft 模式和实践也对 [依赖关系注入](https://msdn.microsoft.com/library/hh323705.aspx) 进行了很好的描述。</span><span class="sxs-lookup"><span data-stu-id="6b433-129">Microsoft Patterns and Practices also has a great description of [Dependency Injection](https://msdn.microsoft.com/library/hh323705.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-130">本文介绍了适用于所有 ASP.NET 应用程序的依赖注入。</span><span class="sxs-lookup"><span data-stu-id="6b433-130">This article covers Dependency Injection as it applies to all ASP.NET applications.</span></span> <span data-ttu-id="6b433-131">MVC 控制器中的依赖注入在 [依赖注入和控制器](../mvc/controllers/dependency-injection.md) 中进行介绍。</span><span class="sxs-lookup"><span data-stu-id="6b433-131">Dependency Injection within MVC controllers is covered in [Dependency Injection and Controllers](../mvc/controllers/dependency-injection.md).</span></span>

### <a name="constructor-injection-behavior"></a><span data-ttu-id="6b433-132">构造函数注入行为</span><span class="sxs-lookup"><span data-stu-id="6b433-132">Constructor injection behavior</span></span>

<span data-ttu-id="6b433-133">构造函数注入要求使用的构造函数为 *公共* 函数。</span><span class="sxs-lookup"><span data-stu-id="6b433-133">Constructor injection requires that the constructor in question be *public*.</span></span> <span data-ttu-id="6b433-134">否则，应用程序会引发 `InvalidOperationException` 异常:</span><span class="sxs-lookup"><span data-stu-id="6b433-134">Otherwise, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="6b433-135">找不到适合类型 YourType 的构造函数。</span><span class="sxs-lookup"><span data-stu-id="6b433-135">A suitable constructor for type 'YourType' couldn't be located.</span></span> <span data-ttu-id="6b433-136">请确保该类型是具体的，并为公共构造函数的所有参数注册服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-136">Ensure the type is concrete and services are registered for all parameters of a public constructor.</span></span>


<span data-ttu-id="6b433-137">构造函数注入要求只存在一个适用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="6b433-137">Constructor injection requires that only one applicable constructor exist.</span></span> <span data-ttu-id="6b433-138">支持构造函数重载，但其参数可以全部通过依赖注入来实现的重载只能存在一个。</span><span class="sxs-lookup"><span data-stu-id="6b433-138">Constructor overloads are supported, but only one overload can exist whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="6b433-139">如果存在多个，应用程序将引发 `InvalidOperationException` 异常:</span><span class="sxs-lookup"><span data-stu-id="6b433-139">If more than one exists, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="6b433-140">已在类型 YourType 中找到多个接受所有给定的参数类型的构造函数。</span><span class="sxs-lookup"><span data-stu-id="6b433-140">Multiple constructors accepting all given argument types have been found in type 'YourType'.</span></span> <span data-ttu-id="6b433-141">应该只有一个适用的构造函数。</span><span class="sxs-lookup"><span data-stu-id="6b433-141">There should only be one applicable constructor.</span></span>

<span data-ttu-id="6b433-142">构造函数可以接受依赖注入没有提供的参数，但这些参数必须支持默认值。</span><span class="sxs-lookup"><span data-stu-id="6b433-142">Constructors can accept arguments that are not provided by dependency injection, but these must support default values.</span></span> <span data-ttu-id="6b433-143">例如: </span><span class="sxs-lookup"><span data-stu-id="6b433-143">For example:</span></span>

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

## <a name="using-framework-provided-services"></a><span data-ttu-id="6b433-144">使用框架提供的服务</span><span class="sxs-lookup"><span data-stu-id="6b433-144">Using framework-provided services</span></span>

<span data-ttu-id="6b433-145">`Startup` 类中的 `ConfigureServices` 方法负责定义应用程序将使用的服务，包括 Entity Framework Core 和 ASP.NET Core MVC 这样的平台特性。</span><span class="sxs-lookup"><span data-stu-id="6b433-145">The `ConfigureServices` method in the `Startup` class is responsible for defining the services the application will use, including platform features like Entity Framework Core and ASP.NET Core MVC.</span></span> <span data-ttu-id="6b433-146">最初，提供给 `ConfigureServices` 的 `IServiceCollection` 定义了以下服务（具体取决于[配置主机的方式](xref:fundamentals/hosting)）：</span><span class="sxs-lookup"><span data-stu-id="6b433-146">Initially, the `IServiceCollection` provided to `ConfigureServices` has the following services defined (depending on [how the host was configured](xref:fundamentals/hosting)):</span></span>

| <span data-ttu-id="6b433-147">服务类型</span><span class="sxs-lookup"><span data-stu-id="6b433-147">Service Type</span></span> | <span data-ttu-id="6b433-148">生存期</span><span class="sxs-lookup"><span data-stu-id="6b433-148">Lifetime</span></span> |
| ----- | ------- |
| [<span data-ttu-id="6b433-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="6b433-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) | <span data-ttu-id="6b433-150">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-150">Singleton</span></span> |
| [<span data-ttu-id="6b433-151">Microsoft.Extensions.Logging.ILoggerFactory</span><span class="sxs-lookup"><span data-stu-id="6b433-151">Microsoft.Extensions.Logging.ILoggerFactory</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.iloggerfactory) | <span data-ttu-id="6b433-152">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-152">Singleton</span></span> |
| [<span data-ttu-id="6b433-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="6b433-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) | <span data-ttu-id="6b433-154">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-154">Singleton</span></span> |
| [<span data-ttu-id="6b433-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span><span class="sxs-lookup"><span data-stu-id="6b433-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | <span data-ttu-id="6b433-156">暂时</span><span class="sxs-lookup"><span data-stu-id="6b433-156">Transient</span></span> |
| [<span data-ttu-id="6b433-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span><span class="sxs-lookup"><span data-stu-id="6b433-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.ihttpcontextfactory) | <span data-ttu-id="6b433-158">暂时</span><span class="sxs-lookup"><span data-stu-id="6b433-158">Transient</span></span> |
| [<span data-ttu-id="6b433-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="6b433-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.ioptions-1) | <span data-ttu-id="6b433-160">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-160">Singleton</span></span> |
| [<span data-ttu-id="6b433-161">System.Diagnostics.DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="6b433-161">System.Diagnostics.DiagnosticSource</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | <span data-ttu-id="6b433-162">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-162">Singleton</span></span> |
| [<span data-ttu-id="6b433-163">System.Diagnostics.DiagnosticListener</span><span class="sxs-lookup"><span data-stu-id="6b433-163">System.Diagnostics.DiagnosticListener</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | <span data-ttu-id="6b433-164">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-164">Singleton</span></span> |
| [<span data-ttu-id="6b433-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span><span class="sxs-lookup"><span data-stu-id="6b433-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartupfilter) | <span data-ttu-id="6b433-166">暂时</span><span class="sxs-lookup"><span data-stu-id="6b433-166">Transient</span></span> |
| [<span data-ttu-id="6b433-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span><span class="sxs-lookup"><span data-stu-id="6b433-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.objectpool.objectpoolprovider) | <span data-ttu-id="6b433-168">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-168">Singleton</span></span> |
| [<span data-ttu-id="6b433-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="6b433-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.options.iconfigureoptions-1) | <span data-ttu-id="6b433-170">暂时</span><span class="sxs-lookup"><span data-stu-id="6b433-170">Transient</span></span> |
| [<span data-ttu-id="6b433-171">Microsoft.AspNetCore.Hosting.Server.IServer</span><span class="sxs-lookup"><span data-stu-id="6b433-171">Microsoft.AspNetCore.Hosting.Server.IServer</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.server.iserver) | <span data-ttu-id="6b433-172">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-172">Singleton</span></span> |
| [<span data-ttu-id="6b433-173">Microsoft.AspNetCore.Hosting.IStartup</span><span class="sxs-lookup"><span data-stu-id="6b433-173">Microsoft.AspNetCore.Hosting.IStartup</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.istartup) | <span data-ttu-id="6b433-174">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-174">Singleton</span></span> |
| [<span data-ttu-id="6b433-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="6b433-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span></span>](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | <span data-ttu-id="6b433-176">单一实例</span><span class="sxs-lookup"><span data-stu-id="6b433-176">Singleton</span></span> |

<span data-ttu-id="6b433-177">下面的示例介绍了如何使用多个扩展方法（如 `AddDbContext`、`AddIdentity` 和 `AddMvc`）将附加服务添加到容器中。</span><span class="sxs-lookup"><span data-stu-id="6b433-177">Below is an example of how to add additional services to the container using a number of extension methods like `AddDbContext`, `AddIdentity`, and `AddMvc`.</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

<span data-ttu-id="6b433-178">ASP.NET 提供的功能和中间件（如 MVC）遵循使用单个 *AddServiceName* 扩展方法的约定来注册该功能所需的所有服务.</span><span class="sxs-lookup"><span data-stu-id="6b433-178">The features and middleware provided by ASP.NET, such as MVC, follow a convention of using a single Add*ServiceName* extension method to register all of the services required by that feature.</span></span>

>[!TIP]
> <span data-ttu-id="6b433-179">你可以通过参数列表在 `Startup` 方法中请求某些框架提供的服务-请参阅 [应用程序启动](startup.md) 以获取更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="6b433-179">You can request certain framework-provided services within `Startup` methods through their parameter lists - see [Application Startup](startup.md) for more details.</span></span>

## <a name="registering-services"></a><span data-ttu-id="6b433-180">注册服务</span><span class="sxs-lookup"><span data-stu-id="6b433-180">Registering services</span></span>

<span data-ttu-id="6b433-181">可按如下方式注册自己的应用程序服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-181">You can register your own application services as follows.</span></span> <span data-ttu-id="6b433-182">第一个泛型类型表示将从容器请求的类型（通常是一个接口）。</span><span class="sxs-lookup"><span data-stu-id="6b433-182">The first generic type represents the type (typically an interface) that will be requested from the container.</span></span> <span data-ttu-id="6b433-183">第二个泛型类型表示将由容器实例化并用于满足此类请求的具体类型。</span><span class="sxs-lookup"><span data-stu-id="6b433-183">The second generic type represents the concrete type that will be instantiated by the container and used to fulfill such requests.</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> <span data-ttu-id="6b433-184">每个 `services.Add<ServiceName>` 扩展方法添加（并可能配置）服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-184">Each `services.Add<ServiceName>` extension method adds (and potentially configures) services.</span></span> <span data-ttu-id="6b433-185">例如，`services.AddMvc()` 添加 MVC 需要的服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-185">For example, `services.AddMvc()` adds the services MVC requires.</span></span> <span data-ttu-id="6b433-186">建议遵循此约定，将扩展方法放置在 `Microsoft.Extensions.DependencyInjection` 命名空间中，以封装服务注册的组。</span><span class="sxs-lookup"><span data-stu-id="6b433-186">It's recommended that you follow this convention, placing extension methods in the `Microsoft.Extensions.DependencyInjection` namespace, to encapsulate groups of service registrations.</span></span>

<span data-ttu-id="6b433-187">`AddTransient` 方法用于将抽象类型映射到为每个需要它的对象分别实例化的具体服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-187">The `AddTransient` method is used to map abstract types to concrete services that are instantiated separately for every object that requires it.</span></span> <span data-ttu-id="6b433-188">这称为服务的 *生存期*，其他生存期选项如下所述。</span><span class="sxs-lookup"><span data-stu-id="6b433-188">This is known as the service's *lifetime*, and additional lifetime options are described below.</span></span> <span data-ttu-id="6b433-189">为注册的每个服务选择适当的生存期非常重要。</span><span class="sxs-lookup"><span data-stu-id="6b433-189">It's important to choose an appropriate lifetime for each of the services you register.</span></span> <span data-ttu-id="6b433-190">是否应该向每个请求它的类提供一个新的服务实例？</span><span class="sxs-lookup"><span data-stu-id="6b433-190">Should a new instance of the service be provided to each class that requests it?</span></span> <span data-ttu-id="6b433-191">是否在整个给定的 Web 请求中使用一个实例？</span><span class="sxs-lookup"><span data-stu-id="6b433-191">Should one instance be used throughout a given web request?</span></span> <span data-ttu-id="6b433-192">或是否应该在应用程序生存期内使用单例？</span><span class="sxs-lookup"><span data-stu-id="6b433-192">Or should a single instance be used for the lifetime of the application?</span></span>

<span data-ttu-id="6b433-193">在本文示例中，有一个显示字符名称的简单控制器，名为 `CharactersController`。</span><span class="sxs-lookup"><span data-stu-id="6b433-193">In the sample for this article, there's a simple controller that displays character names, called `CharactersController`.</span></span> <span data-ttu-id="6b433-194">其 `Index` 方法会显示存储在应用程序中的当前字符列表，如果不存在，则使用少量字符初始化该集合。</span><span class="sxs-lookup"><span data-stu-id="6b433-194">Its `Index` method displays the current list of characters that have been stored in the application, and initializes the collection with a handful of characters if none exist.</span></span> <span data-ttu-id="6b433-195">请注意，尽管此应用程序为其持久化使用Entity Framework Core和 `ApplicationDbContext`，但在控制器中没有任何明显的表现。</span><span class="sxs-lookup"><span data-stu-id="6b433-195">Note that although this application uses Entity Framework Core and the `ApplicationDbContext` class for its persistence, none of that's apparent in the controller.</span></span> <span data-ttu-id="6b433-196">相反，特定的数据访问机制已经被抽象为一个接口，即 `ICharacterRepository`，它遵循 [仓储模式](http://deviq.com/repository-pattern/)。</span><span class="sxs-lookup"><span data-stu-id="6b433-196">Instead, the specific data access mechanism has been abstracted behind an interface, `ICharacterRepository`, which follows the [repository pattern](http://deviq.com/repository-pattern/).</span></span> <span data-ttu-id="6b433-197">通过构造函数请求 `ICharacterRepository` 实例，并将其分配给私有字段，然后根据需要使用它访问字符。</span><span class="sxs-lookup"><span data-stu-id="6b433-197">An instance of `ICharacterRepository` is requested via the constructor and assigned to a private field, which is then used to access characters as necessary.</span></span>

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

<span data-ttu-id="6b433-198">`ICharacterRepository` 定义了控制器使用 `Character` 实例时需要的两种方法。</span><span class="sxs-lookup"><span data-stu-id="6b433-198">The `ICharacterRepository` defines the two methods the controller needs to work with `Character` instances.</span></span>

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

<span data-ttu-id="6b433-199">此接口又由一个具体类型实现，即在运行时使用的 `CharacterRepository`。</span><span class="sxs-lookup"><span data-stu-id="6b433-199">This interface is in turn implemented by a concrete type, `CharacterRepository`, that's used at runtime.</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-200">DI 与 `CharacterRepository` 类一起使用的方式是一个通用模型，您可以为所有应用程序服务遵循此模型，而不仅仅在“仓储库”或数据访问类中。</span><span class="sxs-lookup"><span data-stu-id="6b433-200">The way DI is used with the `CharacterRepository` class is a general model you can follow for all of your application services, not just in "repositories" or data access classes.</span></span>

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

<span data-ttu-id="6b433-201">请注意，`CharacterRepository` 在其构造函数中请求一个 `ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="6b433-201">Note that `CharacterRepository` requests an `ApplicationDbContext` in its constructor.</span></span> <span data-ttu-id="6b433-202">依赖注入以这种链式方式被使用并不罕见，（每个被请求的依赖进而请求它自己的依赖）。</span><span class="sxs-lookup"><span data-stu-id="6b433-202">It's not unusual for dependency injection to be used in a chained fashion like this, with each requested dependency in turn requesting its own dependencies.</span></span> <span data-ttu-id="6b433-203">容器将负责解决图中所有的依赖关系，并返回完全解析后的服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-203">The container is responsible for resolving all of the dependencies in the graph and returning the fully resolved service.</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-204">创建请求的对象，和它需要的所有对象，以及这些对象需要的所有对象，这有时被称为 *对象图*。</span><span class="sxs-lookup"><span data-stu-id="6b433-204">Creating the requested object, and all of the objects it requires, and all of the objects those require, is sometimes referred to as an *object graph*.</span></span> <span data-ttu-id="6b433-205">同样，必须被解析的依赖关系的集合通常被称为*依赖关系树*或*依赖项关系图*。</span><span class="sxs-lookup"><span data-stu-id="6b433-205">Likewise, the collective set of dependencies that must be resolved is typically referred to as a *dependency tree* or *dependency graph*.</span></span>

<span data-ttu-id="6b433-206">在这种情况下，`Startup` 和 `ApplicationDbContext` 必须在 `ICharacterRepository` 类的 `ConfigureServices` 中的服务容器中注册。</span><span class="sxs-lookup"><span data-stu-id="6b433-206">In this case, both `ICharacterRepository` and in turn `ApplicationDbContext` must be registered with the services container in `ConfigureServices` in `Startup`.</span></span> <span data-ttu-id="6b433-207">`ApplicationDbContext` 通过调用扩展方法 `AddDbContext<T>` 进行配置。</span><span class="sxs-lookup"><span data-stu-id="6b433-207">`ApplicationDbContext` is configured with the call to the extension method `AddDbContext<T>`.</span></span> <span data-ttu-id="6b433-208">下面的代码演示了 `CharacterRepository` 类型的注册。</span><span class="sxs-lookup"><span data-stu-id="6b433-208">The following code shows the registration of the `CharacterRepository` type.</span></span>

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

<span data-ttu-id="6b433-209">应使用 `Scoped` 生命周期将实体框架上下文添加到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="6b433-209">Entity Framework contexts should be added to the services container using the `Scoped` lifetime.</span></span> <span data-ttu-id="6b433-210">如果您使用上面所示的帮助方法，则会自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6b433-210">This is taken care of automatically if you use the helper methods as shown above.</span></span> <span data-ttu-id="6b433-211">使用实体框架的仓储库应使用相同的生命周期。</span><span class="sxs-lookup"><span data-stu-id="6b433-211">Repositories that will make use of Entity Framework should use the same lifetime.</span></span>

>[!WARNING]
> <span data-ttu-id="6b433-212">需要注意的主要危险是从单例解析 `Scoped` 服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-212">The main danger to be wary of is resolving a `Scoped` service from a singleton.</span></span> <span data-ttu-id="6b433-213">在此类情况下，当处理后续请求时，服务可能会处于不正确的状态。</span><span class="sxs-lookup"><span data-stu-id="6b433-213">It's likely in such a case that the service will have incorrect state when processing subsequent requests.</span></span>

<span data-ttu-id="6b433-214">具有依赖的服务应将其注册到容器中。</span><span class="sxs-lookup"><span data-stu-id="6b433-214">Services that have dependencies should register them in the container.</span></span> <span data-ttu-id="6b433-215">如果服务构造函数需要一个基元（如 `string`），可使用[配置](xref:fundamentals/configuration/index)和[选项模式](xref:fundamentals/configuration/options)将其注入。</span><span class="sxs-lookup"><span data-stu-id="6b433-215">If a service's constructor requires a primitive, such as a `string`, this can be injected by using [configuration](xref:fundamentals/configuration/index) and the [options pattern](xref:fundamentals/configuration/options).</span></span>

## <a name="service-lifetimes-and-registration-options"></a><span data-ttu-id="6b433-216">服务生存期和注册选项</span><span class="sxs-lookup"><span data-stu-id="6b433-216">Service lifetimes and registration options</span></span>

<span data-ttu-id="6b433-217">可以使用以下生存期配置 ASP.NET 服务：</span><span class="sxs-lookup"><span data-stu-id="6b433-217">ASP.NET services can be configured with the following lifetimes:</span></span>

<span data-ttu-id="6b433-218">**暂时**</span><span class="sxs-lookup"><span data-stu-id="6b433-218">**Transient**</span></span>

<span data-ttu-id="6b433-219">瞬时生存期服务在每次请求时都会创建。</span><span class="sxs-lookup"><span data-stu-id="6b433-219">Transient lifetime services are created each time they're requested.</span></span> <span data-ttu-id="6b433-220">这种生存期适合轻量级、 无状态的服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-220">This lifetime works best for lightweight, stateless services.</span></span>

<span data-ttu-id="6b433-221">**作用域（Scoped）**</span><span class="sxs-lookup"><span data-stu-id="6b433-221">**Scoped**</span></span>

<span data-ttu-id="6b433-222">限定生存期服务每个请求创建一次。</span><span class="sxs-lookup"><span data-stu-id="6b433-222">Scoped lifetime services are created once per request.</span></span>

<span data-ttu-id="6b433-223">**单一实例**</span><span class="sxs-lookup"><span data-stu-id="6b433-223">**Singleton**</span></span>

<span data-ttu-id="6b433-224">单一实例生存期服务在首次请求时（或者如果在其中指定实例，则为 `ConfigureServices` 运行时）进行创建，然后所有后续请求都将使用相同实例。</span><span class="sxs-lookup"><span data-stu-id="6b433-224">Singleton lifetime services are created the first time they're requested (or when `ConfigureServices` is run if you specify an instance there) and then every subsequent request will use the same instance.</span></span> <span data-ttu-id="6b433-225">如果应用程序要求单一实例行为，建议允许服务容器管理服务的生存期，而不是实现单一实例设计模式和自行管理类中对象的生存期。</span><span class="sxs-lookup"><span data-stu-id="6b433-225">If your application requires singleton behavior, allowing the services container to manage the service's lifetime is recommended instead of implementing the singleton design pattern and managing your object's lifetime in the class yourself.</span></span>

<span data-ttu-id="6b433-226">可通过多种方式向容器注册服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-226">Services can be registered with the container in several ways.</span></span> <span data-ttu-id="6b433-227">我们已经了解了如何通过指定要使用的具体类型向给定的类型注册服务实现。</span><span class="sxs-lookup"><span data-stu-id="6b433-227">We have already seen how to register a service implementation with a given type by specifying the concrete type to use.</span></span> <span data-ttu-id="6b433-228">此外，还可指定工厂，将用来按需创建实例。</span><span class="sxs-lookup"><span data-stu-id="6b433-228">In addition, a factory can be specified, which will then be used to create the instance on demand.</span></span> <span data-ttu-id="6b433-229">第三种方法是直接指定要使用的类型的实例，在这种情况下，容器永远不会尝试创建实例（也不会释放该实例）。</span><span class="sxs-lookup"><span data-stu-id="6b433-229">The third approach is to directly specify the instance of the type to use, in which case the container will never attempt to create an instance (nor will it dispose of the instance).</span></span>

<span data-ttu-id="6b433-230">若要演示这些生存期和注册选项之间的差异，请考虑将表示一个或多个任务的简单接口视为带唯一标识符`OperationId` 的操作。</span><span class="sxs-lookup"><span data-stu-id="6b433-230">To demonstrate the difference between these lifetime and registration options, consider a simple interface that represents one or more tasks as an *operation* with a unique identifier, `OperationId`.</span></span> <span data-ttu-id="6b433-231">容器将向请求类提供相同或不同的服务实例，具体取决于配置此服务的生存期的方式。</span><span class="sxs-lookup"><span data-stu-id="6b433-231">Depending on how we configure the lifetime for this service, the container will provide either the same or different instances of the service to the requesting class.</span></span> <span data-ttu-id="6b433-232">为弄清楚正在请求的是哪个生存期，将每个生存期选项创建一种类型：</span><span class="sxs-lookup"><span data-stu-id="6b433-232">To make it clear which lifetime is being requested, we will create one type per lifetime option:</span></span>

[!code-csharp[Main](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

<span data-ttu-id="6b433-233">我们使用单一类 `Operation`（其构造函数接受 `Guid`），或使用新的 `Guid`（如果未提供任何类）实现这些接口。</span><span class="sxs-lookup"><span data-stu-id="6b433-233">We implement these interfaces using a single class, `Operation`, that accepts a `Guid` in its constructor, or uses a new `Guid` if none is provided.</span></span>

<span data-ttu-id="6b433-234">接下来，在 `ConfigureServices` 中，将根据其命名生存期向容器添加每种类型：</span><span class="sxs-lookup"><span data-stu-id="6b433-234">Next, in `ConfigureServices`, each type is added to the container according to its named lifetime:</span></span>

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

<span data-ttu-id="6b433-235">注意，`IOperationSingletonInstance` 服务使用的是已知 ID 为 `Guid.Empty` 的特定实例，因此当使用此类型时会很清楚（其 GUID 全部为零）。</span><span class="sxs-lookup"><span data-stu-id="6b433-235">Note that the `IOperationSingletonInstance` service is using a specific instance with a known ID of `Guid.Empty` so it will be clear when this type is in use (its Guid will be all zeroes).</span></span> <span data-ttu-id="6b433-236">我们还注册了依赖所有其他 `Operation` 类型的 `OperationService`，因此请求中将很清楚此服务是否为每种操作类型获取与控制器相同的实例或者新实例。</span><span class="sxs-lookup"><span data-stu-id="6b433-236">We have also registered an `OperationService` that depends on each of the other `Operation` types, so that it will be clear within a request whether this service is getting the same instance as the controller, or a new one, for each operation type.</span></span> <span data-ttu-id="6b433-237">此服务只需将其依赖关系公开为属性，便可在视图中显示。</span><span class="sxs-lookup"><span data-stu-id="6b433-237">All this service does is expose its dependencies as properties, so they can be displayed in the view.</span></span>

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

<span data-ttu-id="6b433-238">若要演示应用程序的各个请求内和各个请求之间的对象生存期，示例将包括请求每种 `IOperation` 类型的 `OperationsController` 以及 `OperationService`。</span><span class="sxs-lookup"><span data-stu-id="6b433-238">To demonstrate the object lifetimes within and between separate individual requests to the application, the sample includes an `OperationsController` that requests each kind of `IOperation` type as well as an `OperationService`.</span></span> <span data-ttu-id="6b433-239">然后，`Index` 操作将显示所有控制器及服务的 `OperationId` 值。</span><span class="sxs-lookup"><span data-stu-id="6b433-239">The `Index` action then displays all of the controller's and service's `OperationId` values.</span></span>

[!code-csharp[Main](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

<span data-ttu-id="6b433-240">现在，向此控制器操作提了如下两个单独请求：</span><span class="sxs-lookup"><span data-stu-id="6b433-240">Now two separate requests are made to this controller action:</span></span>

![Microsoft Edge 中运行的依赖注入示例 Web 应用程序的操作视图对第一个请求显示暂时、限定、单一实例、实例控制器和操作服务操作的操作 ID 值 (GUID)。](dependency-injection/_static/lifetimes_request1.png)

![操作视图对第二个请求显示操作 ID 值。](dependency-injection/_static/lifetimes_request2.png)

<span data-ttu-id="6b433-243">观察请求内和请求之间哪些 `OperationId` 值不同。</span><span class="sxs-lookup"><span data-stu-id="6b433-243">Observe which of the `OperationId` values vary within a request, and between requests.</span></span>

* <span data-ttu-id="6b433-244">暂时对象始终不同；向每个控制器和每项服务提供一个新的实例。</span><span class="sxs-lookup"><span data-stu-id="6b433-244">*Transient* objects are always different; a new instance is provided to every controller and every service.</span></span>

* <span data-ttu-id="6b433-245">限定对象在请求内是相同的，但在不同的请求中是不同的</span><span class="sxs-lookup"><span data-stu-id="6b433-245">*Scoped* objects are the same within a request, but different across different requests</span></span>

* <span data-ttu-id="6b433-246">单一实例对象对每个对象和每个请求都是相同的（无论实例是否在 `ConfigureServices` 中提供）</span><span class="sxs-lookup"><span data-stu-id="6b433-246">*Singleton* objects are the same for every object and every request (regardless of whether an instance is provided in `ConfigureServices`)</span></span>

## <a name="request-services"></a><span data-ttu-id="6b433-247">请求服务</span><span class="sxs-lookup"><span data-stu-id="6b433-247">Request Services</span></span>

<span data-ttu-id="6b433-248">在 `HttpContext` 中的 ASP.NET 请求内可用的服务通过 `RequestServices` 集合进行公开。</span><span class="sxs-lookup"><span data-stu-id="6b433-248">The services available within an ASP.NET request from `HttpContext` are exposed through the `RequestServices` collection.</span></span>

![HttpContext 请求服务 Intellisense 上下文对话框指出请求服务可获取或设置对请求的服务容器提供访问权限的 IServiceProvider。](dependency-injection/_static/request-services.png)

<span data-ttu-id="6b433-250">请求服务表示你作为应用程序的一部分配置的服务和请求。</span><span class="sxs-lookup"><span data-stu-id="6b433-250">Request Services represent the services you configure and request as part of your application.</span></span> <span data-ttu-id="6b433-251">对象指定依赖关系时，由 `RequestServices`（而不是 `ApplicationServices`）中找到的类型满足这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="6b433-251">When your objects specify dependencies, these are satisfied by the types found in `RequestServices`, not `ApplicationServices`.</span></span>

<span data-ttu-id="6b433-252">通常情况下，不应直接使用这些属性，而应该先通过类的构造函数请求其所需的类型，并允许框架注入这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="6b433-252">Generally, you shouldn't use these properties directly, preferring instead to request the types your classes you require via your class's constructor, and letting the framework inject these dependencies.</span></span> <span data-ttu-id="6b433-253">这可生成易于测试（请参阅[测试](../testing/index.md)）并且耦合更加松散的类。</span><span class="sxs-lookup"><span data-stu-id="6b433-253">This yields classes that are easier to test (see [Testing](../testing/index.md)) and are more loosely coupled.</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-254">优先请求依赖关系作为构造函数参数，用于访问 `RequestServices` 集合。</span><span class="sxs-lookup"><span data-stu-id="6b433-254">Prefer requesting dependencies as constructor parameters to accessing the `RequestServices` collection.</span></span>

## <a name="designing-services-for-dependency-injection"></a><span data-ttu-id="6b433-255">设计适用于依赖注入的服务</span><span class="sxs-lookup"><span data-stu-id="6b433-255">Designing services for dependency injection</span></span>

<span data-ttu-id="6b433-256">应将服务设计为使用依赖注入获取其协作者。</span><span class="sxs-lookup"><span data-stu-id="6b433-256">You should design your services to use dependency injection to get their collaborators.</span></span> <span data-ttu-id="6b433-257">这意味着避免使用有状态静态方法调用（将生成代码告知，称为[静态粘贴](http://deviq.com/static-cling/)），以及服务中相关类的直接实例化。</span><span class="sxs-lookup"><span data-stu-id="6b433-257">This means avoiding the use of stateful static method calls (which result in a code smell known as [static cling](http://deviq.com/static-cling/)) and the direct instantiation of dependent classes within your services.</span></span> <span data-ttu-id="6b433-258">选择是否实例化类型或通过依赖注入请求它时，记住短语 [New is Glue](https://ardalis.com/new-is-glue)（新增即是粘附）可能有用。</span><span class="sxs-lookup"><span data-stu-id="6b433-258">It may help to remember the phrase, [New is Glue](https://ardalis.com/new-is-glue), when choosing whether to instantiate a type or to request it via dependency injection.</span></span> <span data-ttu-id="6b433-259">按照[面向对象的设计的 SOLID 原则](http://deviq.com/solid/)，你的类将自然倾向于小型、构造良好和易测试。</span><span class="sxs-lookup"><span data-stu-id="6b433-259">By following the [SOLID Principles of Object Oriented Design](http://deviq.com/solid/), your classes will naturally tend to be small, well-factored, and easily tested.</span></span>

<span data-ttu-id="6b433-260">如果发现类有太多的依赖关系要注入时怎么办？</span><span class="sxs-lookup"><span data-stu-id="6b433-260">What if you find that your classes tend to have way too many dependencies being injected?</span></span> <span data-ttu-id="6b433-261">这通常表示类尝试执行过多操作，并可能违反 SRP，即[Single Responsibility Principle](http://deviq.com/single-responsibility-principle/)（单一责任原则）。</span><span class="sxs-lookup"><span data-stu-id="6b433-261">This is generally a sign that your class is trying to do too much, and is probably violating SRP - the [Single Responsibility Principle](http://deviq.com/single-responsibility-principle/).</span></span> <span data-ttu-id="6b433-262">确认是否可以通过将其部分职责移到新类来重构该类。</span><span class="sxs-lookup"><span data-stu-id="6b433-262">See if you can refactor the class by moving some of its responsibilities into a new class.</span></span> <span data-ttu-id="6b433-263">请记住，`Controller` 类应该关注 UI 问题，因此业务规则和数据访问实现详细信息应保存在这些[单独问题](http://deviq.com/separation-of-concerns/)相应的类中。</span><span class="sxs-lookup"><span data-stu-id="6b433-263">Keep in mind that your `Controller` classes should be focused on UI concerns, so business rules and data access implementation details should be kept in classes appropriate to these [separate concerns](http://deviq.com/separation-of-concerns/).</span></span>

<span data-ttu-id="6b433-264">具体而言，对于数据访问，可以将 `DbContext` 注入控制器（假设已向 `ConfigureServices` 中的服务容器添加 EF）。</span><span class="sxs-lookup"><span data-stu-id="6b433-264">With regards to data access specifically, you can inject the `DbContext` into your controllers (assuming you've added EF to the services container in `ConfigureServices`).</span></span> <span data-ttu-id="6b433-265">部分开发者宁愿使用数据库的存储库接口，而不是直接注入 `DbContext`。</span><span class="sxs-lookup"><span data-stu-id="6b433-265">Some developers prefer to use a repository interface to the database rather than injecting the `DbContext` directly.</span></span> <span data-ttu-id="6b433-266">使用接口将数据访问逻辑封装于一处可以最大程序减少数据更改时需要更改的位置数量。</span><span class="sxs-lookup"><span data-stu-id="6b433-266">Using an interface to encapsulate the data access logic in one place can minimize how many places you will have to change when your database changes.</span></span>

### <a name="disposing-of-services"></a><span data-ttu-id="6b433-267">释放服务</span><span class="sxs-lookup"><span data-stu-id="6b433-267">Disposing of services</span></span>

<span data-ttu-id="6b433-268">容器将为其创建的 `IDisposable` 类型调用 `Dispose`。</span><span class="sxs-lookup"><span data-stu-id="6b433-268">The container will call `Dispose` for `IDisposable` types it creates.</span></span> <span data-ttu-id="6b433-269">但是，如果自行向容器添加实例，容器不会释放。</span><span class="sxs-lookup"><span data-stu-id="6b433-269">However, if you add an instance to the container yourself, it will not be disposed.</span></span>

<span data-ttu-id="6b433-270">示例:</span><span class="sxs-lookup"><span data-stu-id="6b433-270">Example:</span></span>

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
> <span data-ttu-id="6b433-271">在 1.0 版中，容器对所有 `IDisposable` 对象调用了 dispose，包括未创建的对象。</span><span class="sxs-lookup"><span data-stu-id="6b433-271">In version 1.0, the container called dispose on *all* `IDisposable` objects, including those it didn't create.</span></span>

## <a name="replacing-the-default-services-container"></a><span data-ttu-id="6b433-272">替换默认服务容器</span><span class="sxs-lookup"><span data-stu-id="6b433-272">Replacing the default services container</span></span>

<span data-ttu-id="6b433-273">内置服务容器专门服务框架和基于其上生成的大多数应用程序的基本需求。</span><span class="sxs-lookup"><span data-stu-id="6b433-273">The built-in services container is meant to serve the basic needs of the framework and most consumer applications built on it.</span></span> <span data-ttu-id="6b433-274">但是，开发者可将内置容器替换为其首选容器。</span><span class="sxs-lookup"><span data-stu-id="6b433-274">However, developers can replace the built-in container with their preferred container.</span></span> <span data-ttu-id="6b433-275">`ConfigureServices` 方法通常会返回 `void`，但如果其签名更改为返回 `IServiceProvider`，可配置和返回不同的容器。</span><span class="sxs-lookup"><span data-stu-id="6b433-275">The `ConfigureServices` method typically returns `void`, but if its signature is changed to return `IServiceProvider`, a different container can be configured and returned.</span></span> <span data-ttu-id="6b433-276">具有适用于 .NET 的多个 IOC 容器。</span><span class="sxs-lookup"><span data-stu-id="6b433-276">There are many IOC containers available for .NET.</span></span> <span data-ttu-id="6b433-277">在此示例中，将使用 [Autofac](https://autofac.org/) 包。</span><span class="sxs-lookup"><span data-stu-id="6b433-277">In this example, the [Autofac](https://autofac.org/) package is used.</span></span>

<span data-ttu-id="6b433-278">首先，安装适当的容器包：</span><span class="sxs-lookup"><span data-stu-id="6b433-278">First, install the appropriate container package(s):</span></span>

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

<span data-ttu-id="6b433-279">接下来，在 `ConfigureServices` 中配置容器并返回 `IServiceProvider`：</span><span class="sxs-lookup"><span data-stu-id="6b433-279">Next, configure the container in `ConfigureServices` and return an `IServiceProvider`:</span></span>

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
> <span data-ttu-id="6b433-280">使用第三方 DI 容器时，必须更改 `ConfigureServices`，以便其返回 `IServiceProvider`，而不是 `void`。</span><span class="sxs-lookup"><span data-stu-id="6b433-280">When using a third-party DI container, you must change `ConfigureServices` so that it returns `IServiceProvider` instead of `void`.</span></span>

<span data-ttu-id="6b433-281">最后，将 Autofac 在 `DefaultModule` 中配置为正常：</span><span class="sxs-lookup"><span data-stu-id="6b433-281">Finally, configure Autofac as normal in `DefaultModule`:</span></span>

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

<span data-ttu-id="6b433-282">运行时，Autofac 将用来解析类型和注入依赖关系。</span><span class="sxs-lookup"><span data-stu-id="6b433-282">At runtime, Autofac will be used to resolve types and inject dependencies.</span></span> <span data-ttu-id="6b433-283">[深入了解如何使用 Autofac 和 ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html)。</span><span class="sxs-lookup"><span data-stu-id="6b433-283">[Learn more about using Autofac and ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html).</span></span>

### <a name="thread-safety"></a><span data-ttu-id="6b433-284">线程安全</span><span class="sxs-lookup"><span data-stu-id="6b433-284">Thread safety</span></span>

<span data-ttu-id="6b433-285">单一实例服务需要处于线程安全。</span><span class="sxs-lookup"><span data-stu-id="6b433-285">Singleton services need to be thread safe.</span></span> <span data-ttu-id="6b433-286">如果单一实例服务与暂时服务存在依赖关系，暂时服务可能也需要线程安全，具体取决于使用单一实例的方式。</span><span class="sxs-lookup"><span data-stu-id="6b433-286">If a singleton service has a dependency on a transient service, the transient service may also need to be thread safe depending how it's used by the singleton.</span></span>

## <a name="recommendations"></a><span data-ttu-id="6b433-287">建议</span><span class="sxs-lookup"><span data-stu-id="6b433-287">Recommendations</span></span>

<span data-ttu-id="6b433-288">使用依赖注入时，请记住以下建议：</span><span class="sxs-lookup"><span data-stu-id="6b433-288">When working with dependency injection, keep the following recommendations in mind:</span></span>

* <span data-ttu-id="6b433-289">DI 适用于具有复杂依赖关系的对象。</span><span class="sxs-lookup"><span data-stu-id="6b433-289">DI is for objects that have complex dependencies.</span></span> <span data-ttu-id="6b433-290">控制器、服务、适配器和存储库是可添加到 DI 的对象的所有示例。</span><span class="sxs-lookup"><span data-stu-id="6b433-290">Controllers, services, adapters, and repositories are all examples of objects that might be added to DI.</span></span>

* <span data-ttu-id="6b433-291">避免在 DI 中直接存储和配置数据。</span><span class="sxs-lookup"><span data-stu-id="6b433-291">Avoid storing data and configuration directly in DI.</span></span> <span data-ttu-id="6b433-292">例如，用户的购物车通常不应添加到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="6b433-292">For example, a user's shopping cart shouldn't typically be added to the services container.</span></span> <span data-ttu-id="6b433-293">配置应该使用[选项模式](xref:fundamentals/configuration/options)。</span><span class="sxs-lookup"><span data-stu-id="6b433-293">Configuration should use the [options pattern](xref:fundamentals/configuration/options).</span></span> <span data-ttu-id="6b433-294">同样，避免仅存在允许访部分其他对象的“数据持有者”对象。</span><span class="sxs-lookup"><span data-stu-id="6b433-294">Similarly, avoid "data holder" objects that only exist to allow access to some other object.</span></span> <span data-ttu-id="6b433-295">如果可能，最好通过 DI 请求所需的实际项目。</span><span class="sxs-lookup"><span data-stu-id="6b433-295">It's better to request the actual item needed via DI, if possible.</span></span>

* <span data-ttu-id="6b433-296">避免静态访问服务。</span><span class="sxs-lookup"><span data-stu-id="6b433-296">Avoid static access to services.</span></span>

* <span data-ttu-id="6b433-297">应用程序代码中避免服务位置。</span><span class="sxs-lookup"><span data-stu-id="6b433-297">Avoid service location in your application code.</span></span>

* <span data-ttu-id="6b433-298">避免静态访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="6b433-298">Avoid static access to `HttpContext`.</span></span>

> [!NOTE]
> <span data-ttu-id="6b433-299">如所有建议组合一样，你可能会遇到必须忽略一个的情况。</span><span class="sxs-lookup"><span data-stu-id="6b433-299">Like all sets of recommendations, you may encounter situations where ignoring one is required.</span></span> <span data-ttu-id="6b433-300">我们发现异常很少见，大多数是框架本身中非常特殊的情况。</span><span class="sxs-lookup"><span data-stu-id="6b433-300">We have found exceptions to be rare -- mostly very special cases within the framework itself.</span></span>

<span data-ttu-id="6b433-301">记住，依赖注入是静态/局部对象访问模式的备用方案。</span><span class="sxs-lookup"><span data-stu-id="6b433-301">Remember, dependency injection is an *alternative* to static/global object access patterns.</span></span> <span data-ttu-id="6b433-302">如果将 DI 与静态对象访问混合，你将无法实现其好处。</span><span class="sxs-lookup"><span data-stu-id="6b433-302">You won't be able to realize the benefits of DI if you mix it with static object access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b433-303">其他资源</span><span class="sxs-lookup"><span data-stu-id="6b433-303">Additional resources</span></span>

* [<span data-ttu-id="6b433-304">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="6b433-304">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="6b433-305">测试</span><span class="sxs-lookup"><span data-stu-id="6b433-305">Testing</span></span>](xref:testing/index)
* [<span data-ttu-id="6b433-306">基于工厂的中间件激活</span><span class="sxs-lookup"><span data-stu-id="6b433-306">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
* [<span data-ttu-id="6b433-307">使用依赖注入在 ASP.NET Core 中编写干净代码 (MSDN)</span><span class="sxs-lookup"><span data-stu-id="6b433-307">Writing Clean Code in ASP.NET Core with Dependency Injection (MSDN)</span></span>](https://msdn.microsoft.com/magazine/mt703433.aspx)
* <span data-ttu-id="6b433-308">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)（容器托管的应用程序设计，序言：容器属于何处？）</span><span class="sxs-lookup"><span data-stu-id="6b433-308">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)</span></span>
* <span data-ttu-id="6b433-309">[Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显式依赖关系原则）</span><span class="sxs-lookup"><span data-stu-id="6b433-309">[Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)</span></span>
* <span data-ttu-id="6b433-310">[Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html)（控制反转容器和依赖注入模式）</span><span class="sxs-lookup"><span data-stu-id="6b433-310">[Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html) (Fowler)</span></span>
