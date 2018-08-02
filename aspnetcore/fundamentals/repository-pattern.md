---
title: 使用 ASP.NET Core 的存储库模式
author: ardalis
description: 了解如何在 ASP.NET Core 应用中实现存储库应用设计模式。
ms.author: riande
ms.custom: mvc
ms.date: 07/02/2018
uid: fundamentals/repository-pattern
ms.openlocfilehash: d64c3d090f62c580ebc05a6bbc2744a4508bb9bc
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342574"
---
# <a name="repository-pattern-with-aspnet-core"></a><span data-ttu-id="379cc-103">使用 ASP.NET Core 的存储库模式</span><span class="sxs-lookup"><span data-stu-id="379cc-103">Repository pattern with ASP.NET Core</span></span>

<span data-ttu-id="379cc-104">作者：[Steve Smith](https://ardalis.com/)、[Scott Addie](https://scottaddie.com) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="379cc-104">By [Steve Smith](https://ardalis.com/), [Scott Addie](https://scottaddie.com), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="379cc-105">存储库模式是一种设计模式，用于隔离接口抽象背后的数据访问。</span><span class="sxs-lookup"><span data-stu-id="379cc-105">The *repository pattern* is a design pattern that isolates data access behind interface abstractions.</span></span> <span data-ttu-id="379cc-106">连接到数据库和操作数据存储对象是通过接口实现提供的方法执行的。</span><span class="sxs-lookup"><span data-stu-id="379cc-106">Connecting to the database and manipulating data storage objects is performed through methods provided by the interface's implementation.</span></span> <span data-ttu-id="379cc-107">因此，无需调用代码来处理数据库问题，例如连接、命令和读取器。</span><span class="sxs-lookup"><span data-stu-id="379cc-107">Consequently, there's no need for calling code to deal with database concerns, such as connections, commands, and readers.</span></span>

<span data-ttu-id="379cc-108">使用 ASP.NET Core 实现存储库模式具有以下优势：</span><span class="sxs-lookup"><span data-stu-id="379cc-108">Implementation of the repository pattern with ASP.NET Core has the following benefits:</span></span>

* <span data-ttu-id="379cc-109">应用的组织不太复杂，业务和数据访问层之间没有直接的相互依赖关系。</span><span class="sxs-lookup"><span data-stu-id="379cc-109">Organization of the app is less complex with no direct interdependency between the business and data access layers.</span></span>
* <span data-ttu-id="379cc-110">更容易重用数据库访问代码，因为代码由一个或多个存储库集中管理。</span><span class="sxs-lookup"><span data-stu-id="379cc-110">It's easier to reuse database access code because the code is centrally managed by one or more repositories.</span></span>
* <span data-ttu-id="379cc-111">业务域可以从数据库层独立进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="379cc-111">The business domain can be independently unit tested from the database layer.</span></span>

<span data-ttu-id="379cc-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="379cc-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="379cc-113">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)使用存储库模式初始化并显示电影角色名称的列表。</span><span class="sxs-lookup"><span data-stu-id="379cc-113">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples) uses the repository pattern to initialize and display a list of movie character names.</span></span> <span data-ttu-id="379cc-114">该应用使用 [Entity Framework Core](/ef/core/) 和 `ApplicationDbContext` 类来实现其数据持久性，但数据库基础结构在访问数据的位置并不明显。</span><span class="sxs-lookup"><span data-stu-id="379cc-114">The app uses [Entity Framework Core](/ef/core/) and an `ApplicationDbContext` class for its data persistence, but the database infrastructure isn't apparent where the data is accessed.</span></span> <span data-ttu-id="379cc-115">数据访问和数据库对象是基于[存储库](https://martinfowler.com/eaaCatalog/repository.html)抽象出来的。</span><span class="sxs-lookup"><span data-stu-id="379cc-115">Data access and database objects are abstracted behind a [repository](https://martinfowler.com/eaaCatalog/repository.html).</span></span>

## <a name="repository-interface"></a><span data-ttu-id="379cc-116">存储库接口</span><span class="sxs-lookup"><span data-stu-id="379cc-116">Repository interface</span></span>

<span data-ttu-id="379cc-117">存储库接口定义实现的属性和方法。</span><span class="sxs-lookup"><span data-stu-id="379cc-117">A repository interface defines the properties and methods for implementation.</span></span> <span data-ttu-id="379cc-118">在示例应用中，电影角色数据的存储库接口为 `ICharacterRepository`。</span><span class="sxs-lookup"><span data-stu-id="379cc-118">In the sample app, the repository interface for movie character data is `ICharacterRepository`.</span></span> <span data-ttu-id="379cc-119">`ICharacterRepository` 定义在应用中使用 `Character` 实例所需的 `ListAll` 和 `Add` 方法：</span><span class="sxs-lookup"><span data-stu-id="379cc-119">`ICharacterRepository` defines the `ListAll` and `Add` methods required to work with `Character` instances in the app:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="379cc-120">`Character` 定义为：</span><span class="sxs-lookup"><span data-stu-id="379cc-120">`Character` is defined as:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

## <a name="repository-concrete-type"></a><span data-ttu-id="379cc-121">存储库的具体类型</span><span class="sxs-lookup"><span data-stu-id="379cc-121">Repository concrete type</span></span>

<span data-ttu-id="379cc-122">该接口由具体类型实现。</span><span class="sxs-lookup"><span data-stu-id="379cc-122">The interface is implemented by a concrete type.</span></span> <span data-ttu-id="379cc-123">在示例应用中，`CharacterRepository` 管理数据库上下文并实现 `ListAll` 和 `Add` 方法：</span><span class="sxs-lookup"><span data-stu-id="379cc-123">In the sample app, `CharacterRepository` manages the database context and implements the `ListAll` and `Add` methods:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

## <a name="register-the-repository-service"></a><span data-ttu-id="379cc-124">注册存储库服务</span><span class="sxs-lookup"><span data-stu-id="379cc-124">Register the repository service</span></span>

<span data-ttu-id="379cc-125">使用 `Startup.ConfigureServices` 中的服务容器注册存储库和数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="379cc-125">The repository and database context are registered with the service container in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="379cc-126">在示例应用中，通过调用扩展方法 [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext) 配置 `ApplicationDbContext`。</span><span class="sxs-lookup"><span data-stu-id="379cc-126">In the sample app, `ApplicationDbContext` is configured with the call to the extension method [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext).</span></span> <span data-ttu-id="379cc-127">`ICharacterRepository` 注册为作用域服务：</span><span class="sxs-lookup"><span data-stu-id="379cc-127">`ICharacterRepository` is registered as a scoped service:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,18)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,12)]

::: moniker-end

## <a name="inject-an-instance-of-the-repository"></a><span data-ttu-id="379cc-128">注入存储库的实例</span><span class="sxs-lookup"><span data-stu-id="379cc-128">Inject an instance of the repository</span></span>

<span data-ttu-id="379cc-129">在需要数据库访问的类中，通过构造函数请求存储库的实例，并将其分配给私有字段以供类方法使用。</span><span class="sxs-lookup"><span data-stu-id="379cc-129">In a class where database access is required, an instance of the repository is requested via the constructor and assigned to a private field for use by class methods.</span></span> <span data-ttu-id="379cc-130">在示例应用中，`ICharacterRepository` 用于：</span><span class="sxs-lookup"><span data-stu-id="379cc-130">In the sample app, `ICharacterRepository` is used to:</span></span>

* <span data-ttu-id="379cc-131">填充数据库（如果不存在任何字符）。</span><span class="sxs-lookup"><span data-stu-id="379cc-131">Populate the database if no characters exist.</span></span>
* <span data-ttu-id="379cc-132">获取要显示的字符的列表。</span><span class="sxs-lookup"><span data-stu-id="379cc-132">Obtain a list of the characters for display.</span></span>

<span data-ttu-id="379cc-133">请注意调用代码如何仅与接口的实现 `CharacterRepository` 交互。</span><span class="sxs-lookup"><span data-stu-id="379cc-133">Notice how the calling code only interacts with the interface's implementation, `CharacterRepository`.</span></span> <span data-ttu-id="379cc-134">调用代码不直接使用 `ApplicationDbContext`：</span><span class="sxs-lookup"><span data-stu-id="379cc-134">Calling code doesn't use the `ApplicationDbContext` directly:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Pages/Index.cshtml.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Controllers/HomeController.cs?name=snippet1)]

::: moniker-end

## <a name="generic-repository-interface"></a><span data-ttu-id="379cc-135">通用存储库接口</span><span class="sxs-lookup"><span data-stu-id="379cc-135">Generic repository interface</span></span>

<span data-ttu-id="379cc-136">本主题及其示例应用演示了存储库模式的最简单实现，其中为每个业务对象创建了一个存储库。</span><span class="sxs-lookup"><span data-stu-id="379cc-136">This topic and its sample app demonstrate the simplest implementation of the repository pattern, where one repository is created for each business object.</span></span> <span data-ttu-id="379cc-137">如果应用增长超过几个对象，则通用存储库接口可能会减少实现存储库模式所需的代码量。</span><span class="sxs-lookup"><span data-stu-id="379cc-137">If the app grows beyond a few objects, a *generic repository interface* may reduce the amount of code required to implement the repository pattern.</span></span> <span data-ttu-id="379cc-138">有关详细信息，请参阅 [DevIQ：存储库模式：通用存储库接口](http://deviq.com/repository-pattern/)。</span><span class="sxs-lookup"><span data-stu-id="379cc-138">For more information, see [DevIQ: Repository Pattern: Generic Repository Interface](http://deviq.com/repository-pattern/).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="379cc-139">其他资源</span><span class="sxs-lookup"><span data-stu-id="379cc-139">Additional resources</span></span>

* [<span data-ttu-id="379cc-140">DevIQ：存储库模式</span><span class="sxs-lookup"><span data-stu-id="379cc-140">DevIQ: Repository Pattern</span></span>](https://deviq.com/repository-pattern/)
* [<span data-ttu-id="379cc-141">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="379cc-141">Dependency injection</span></span>](xref:fundamentals/dependency-injection)
* [<span data-ttu-id="379cc-142">视图中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="379cc-142">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
* [<span data-ttu-id="379cc-143">控制器中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="379cc-143">Dependency injection into controllers</span></span>](xref:mvc/controllers/dependency-injection)
* [<span data-ttu-id="379cc-144">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="379cc-144">Dependency injection in requirement handlers</span></span>](xref:security/authorization/dependencyinjection)
* [<span data-ttu-id="379cc-145">控制反转容器和依赖关系注入模式</span><span class="sxs-lookup"><span data-stu-id="379cc-145">Inversion of Control Containers and the Dependency Injection Pattern</span></span>](https://www.martinfowler.com/articles/injection.html)
