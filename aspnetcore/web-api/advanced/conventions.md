---
title: 使用 Web API 约定
author: pranavkm
description: 了解 ASP.NET Core 中的 Web API 约定。
monikerRange: '>= aspnetcore-2.2'
ms.author: pranavkm
ms.custom: mvc
ms.date: 11/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: ede9a46c160cf6a49aa93da710af0bf0b8f59acc
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710070"
---
# <a name="use-web-api-conventions"></a>使用 Web API 约定

ASP.NET Core 2.2 引入了一种方法，可提取常见的 [API 文档](xref:tutorials/web-api-help-pages-using-swagger)并将其应用于多个操作、控制器或某程序集内的所有控制器。 Web API 约定可替代使用 [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute) 来装饰单个操作。 使用该约定，可定义从操作返回的最通用的“常规”返回类型和状态代码，并选择适用于某个操作的约定方法。

默认情况下，ASP.NET Core MVC 2.2 附带一组默认约定，`Microsoft.AspNetCore.Mvc.DefaultApiConventions`。 这些约定基于 ASP.NET Core 为其提供基架的控制器。 若操作遵循基架产生的模式，则应成功使用默认约定。

在运行时，<xref:Microsoft.AspNetCore.Mvc.ApiExplorer> 会了解约定。 `ApiExplorer` 是 MVC 与开放 API 文档生成器进行通信的抽象内容。 已应用的约定中的属性与某个操作相关联，并包含在操作的 Swagger 文档中。 API 分析器也会了解约定。 若操作为非常规操作（例如，它返回已应用的约定未记录的状态代码），则会生成警告，建议记录该操作。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="apply-web-api-conventions"></a>应用 Web API 约定

应用约定有三种方法。 约定不是组合而成的。 每个操作可能只与一个约定相关联。 更明确的约定（详见下文）优先于不太明确的约定。 当具有相同优先级的两个或更多约定应用于某个操作时，选择是不确定的。 存在以下可将约定应用于操作的选项，明确性依次降低：

1. `Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; 适用于单独的操作，并指定适用的约定类型和约定方法。 在以下示例中，将约定方法 `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` 应用于 `Update` 操作：

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventionmethod&highlight=2-3)]

1. `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` 应用于控制器 &mdash; 将约定类型应用于控制器上的所有操作。 约定方法通过确定将应用于哪些操作的提示进行装饰（作为创作约定的一部分的详细信息）。 例如:

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventiontypeattribute)]

1. `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` 应用于程序集 &mdash; 将约定类型应用于当前程序集的所有控制器。 例如:

    [!code-csharp[](conventions/sample/Startup.cs?name=apiconventiontypeattribute)]

## <a name="create-web-api-conventions"></a>创建 Web API 约定

约定是带有方法的静态类型。 这些方法使用 `[ProducesResponseType]` 或 `[ProducesDefaultResponseType]` 属性进行批注。

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

将此约定应用于程序集会导致约定方法应用于名称为 `Find` 的任何操作，并且在这些约定方法不具有其他更明确的元数据属性情况下，它们只有一个名为 `id` 的参数。

除了 `[ProducesResponseType]` 和 `[ProducesDefaultResponseType]` 之外，`[ApiConventionNameMatch]` 和 `[ApiConventionTypeMatch]` 还可应用于确定它们所适用的方法的约定方法。 例如:

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

* 应用于该方法的 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` 选项表示该约定可匹配任何操作，前提是以“Find”作为前缀。 这包括 `Find`、`FindPet` 或 `FindById` 等方法。
* 应用于该参数的 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix` 表示该约定可匹配以标识符作为后缀结尾的唯一参数的方法。 这包括 `id` 或 `petId` 等参数。 与此类似，可将 `ApiConventionTypeMatch` 应用于类型，以约束参数的类型。 `params[]` 参数可用于指示无需显式匹配的剩余参数。
