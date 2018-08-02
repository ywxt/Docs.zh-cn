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
# <a name="repository-pattern-with-aspnet-core"></a>使用 ASP.NET Core 的存储库模式

作者：[Steve Smith](https://ardalis.com/)、[Scott Addie](https://scottaddie.com) 和 [Luke Latham](https://github.com/guardrex)

存储库模式是一种设计模式，用于隔离接口抽象背后的数据访问。 连接到数据库和操作数据存储对象是通过接口实现提供的方法执行的。 因此，无需调用代码来处理数据库问题，例如连接、命令和读取器。

使用 ASP.NET Core 实现存储库模式具有以下优势：

* 应用的组织不太复杂，业务和数据访问层之间没有直接的相互依赖关系。
* 更容易重用数据库访问代码，因为代码由一个或多个存储库集中管理。
* 业务域可以从数据库层独立进行单元测试。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)使用存储库模式初始化并显示电影角色名称的列表。 该应用使用 [Entity Framework Core](/ef/core/) 和 `ApplicationDbContext` 类来实现其数据持久性，但数据库基础结构在访问数据的位置并不明显。 数据访问和数据库对象是基于[存储库](https://martinfowler.com/eaaCatalog/repository.html)抽象出来的。

## <a name="repository-interface"></a>存储库接口

存储库接口定义实现的属性和方法。 在示例应用中，电影角色数据的存储库接口为 `ICharacterRepository`。 `ICharacterRepository` 定义在应用中使用 `Character` 实例所需的 `ListAll` 和 `Add` 方法：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

`Character` 定义为：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

## <a name="repository-concrete-type"></a>存储库的具体类型

该接口由具体类型实现。 在示例应用中，`CharacterRepository` 管理数据库上下文并实现 `ListAll` 和 `Add` 方法：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

## <a name="register-the-repository-service"></a>注册存储库服务

使用 `Startup.ConfigureServices` 中的服务容器注册存储库和数据库上下文。 在示例应用中，通过调用扩展方法 [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext) 配置 `ApplicationDbContext`。 `ICharacterRepository` 注册为作用域服务：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,18)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,12)]

::: moniker-end

## <a name="inject-an-instance-of-the-repository"></a>注入存储库的实例

在需要数据库访问的类中，通过构造函数请求存储库的实例，并将其分配给私有字段以供类方法使用。 在示例应用中，`ICharacterRepository` 用于：

* 填充数据库（如果不存在任何字符）。
* 获取要显示的字符的列表。

请注意调用代码如何仅与接口的实现 `CharacterRepository` 交互。 调用代码不直接使用 `ApplicationDbContext`：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Pages/Index.cshtml.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Controllers/HomeController.cs?name=snippet1)]

::: moniker-end

## <a name="generic-repository-interface"></a>通用存储库接口

本主题及其示例应用演示了存储库模式的最简单实现，其中为每个业务对象创建了一个存储库。 如果应用增长超过几个对象，则通用存储库接口可能会减少实现存储库模式所需的代码量。 有关详细信息，请参阅 [DevIQ：存储库模式：通用存储库接口](http://deviq.com/repository-pattern/)。

## <a name="additional-resources"></a>其他资源

* [DevIQ：存储库模式](https://deviq.com/repository-pattern/)
* [依赖关系注入](xref:fundamentals/dependency-injection)
* [视图中的依赖关系注入](xref:mvc/views/dependency-injection)
* [控制器中的依赖关系注入](xref:mvc/controllers/dependency-injection)
* [要求处理程序中的依赖关系注入](xref:security/authorization/dependencyinjection)
* [控制反转容器和依赖关系注入模式](https://www.martinfowler.com/articles/injection.html)
