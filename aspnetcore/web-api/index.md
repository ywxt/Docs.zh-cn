---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 08/15/2018
uid: web-api/index
ms.openlocfilehash: 763b95fb8ed3806bc67b7ad199153ea1027efa57
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090415"
---
# <a name="build-web-apis-with-aspnet-core"></a>使用 ASP.NET Core 构建 Web API

作者：[Scott Addie](https://github.com/scottaddie)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。

## <a name="derive-class-from-controllerbase"></a>从 ControllerBase 派生类

从控制器（旨在用作 Web API）中的 <xref:Microsoft.AspNetCore.Mvc.ControllerBase> 类继承。 例如:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

通过 `ControllerBase` 类可使用一些属性和方法。 在前面的代码中，示例包括 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>。 将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。 将使用 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState>属性（还可由 `ControllerBase` 提供）处理请求模型验证。

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a>使用 ApiControllerAttribute 批注类

ASP.NET Core 2.1 引入了 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 特性，用于批注 Web API 控制器类。 例如:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

需要兼容性版本 2.1 或更高版本（通过 <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 设置）来使用此属性。 例如，Startup.ConfigureServices 中突出显示的代码设置了 2.2 兼容性标志：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

有关更多信息，请参见<xref:mvc/compatibility-version>。

`[ApiController]` 特性通常结合 `ControllerBase` 来为控制器启用特定于 REST 行为。 通过 `ControllerBase` 可使用<xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*> 等方法。

另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

以下各部分说明该特性添加的便利功能。

### <a name="problem-details-responses-for-error-status-codes"></a>错误状态代码的问题详细信息响应

ASP.NET Core 2.1 及更高版本包括 [ProblemDetails](xref:Microsoft.AspNetCore.Mvc.ProblemDetails)，这是一种基于 [RFC 7807 规范](https://tools.ietf.org/html/rfc7807)的类型。 `ProblemDetails` 类型提供了标准化格式，用于传达 HTTP 响应中计算机可读的错误详细信息。

在 ASP.NET Core 2.2 及更高版本中，MVC 将错误状态代码结果（状态代码 400 及更高）转换为带 `ProblemDetails` 的结果。 考虑下列代码：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_ProblemDetails_StatusCode&highlight=4)]

`NotFound` 结果的 HTTP 响应具有 404 状态代码，其 `ProblemDetails` 主体如下所示：

```js
{
    type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    title: "Not Found",
    status: 404,
    traceId: "0HLHLV31KRN83:00000001"
}
```

需具备 2.2 版本或更高版本的兼容性标志，才可使用问题详细信息功能。 当 [SuppressMapClientErrors](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressMapClientErrors> -->属性设置为 `true` 时，会禁用默认行为。 下面突出显示的 `Startup.ConfigureServices` 代码会禁用问题详细信息：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=8)]

使用 [ClientErrorMapping](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.ClientErrorMapping> -->属性配置 `ProblemDetails` 响应的内容。 例如，以下代码会更新 404 响应的 `type` 属性：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=10)]

### <a name="automatic-http-400-responses"></a>自动 HTTP 400 响应

验证错误会自动触发 HTTP 400 响应。 操作中不需要以下代码：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

使用 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> 自定义所生成的响应的输出。

当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> 属性设置为 `true` 时，会禁用默认行为。 将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

使用 2.2 或更高版本的兼容性标志时，为 400 响应返回的默认响应类型为 <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>。 通过 [SuppressUseValidationProblemDetailsForInvalidModelStateResponses](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressUseValidationProblemDetailsForInvalidModelStateResponses> --> 属性使用 ASP.NET Core 2.1 错误格式。

### <a name="binding-source-parameter-inference"></a>绑定源参数推理

绑定源特性定义可找到操作参数值的位置。 存在以下绑定源特性：

|特性|绑定源 |
|---------|---------|
|**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**     | 请求正文 |
|**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**     | 请求正文中的表单数据 |
|**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)** | 请求标头 |
|**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**   | 请求查询字符串参数 |
|**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**   | 当前请求中的路由数据 |
|**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)** | 作为操作参数插入的请求服务 |

> [!WARNING]
> 当值可能包含 `%2f`（即 `/`）时，请勿使用 `[FromRoute]`。 `%2f` 不会转换为 `/`（非转移形式）。 如果值可能包含 `%2f`，则使用 `[FromQuery]`。

没有 `[ApiController]` 特性时，将显式定义绑定源特性。 在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

推理规则应用于操作参数的默认数据源。 这些规则将配置绑定资源，否则你可以手动应用操作参数。 绑定源特性的行为如下：

* **[FromBody]**，针对复杂类型参数进行推断。 此规则不适用于具有特殊含义的任何复杂的内置类型，如 <xref:Microsoft.AspNetCore.Http.IFormCollection> 和 <xref:System.Threading.CancellationToken>。 绑定源推理代码将忽略这些特殊类型。 对于简单类型（例如 `string` 或 `int`），推断不出 `[FromBody]`。 因此，如果需要该功能，对于简单类型，应使用 `[FromBody]` 属性。 当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。 例如，下面的操作签名会导致异常：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* [FromForm] 是针对 <xref:Microsoft.AspNetCore.Http.IFormFile> 和 <xref:Microsoft.AspNetCore.Http.IFormFileCollection> 类型的操作参数推断出来的。 该特性不针对任何简单类型或用户定义类型进行推断。
* **[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。 当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。
* **[FromQuery]**，针对任何其他操作参数进行推断。

当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> 属性设置为 `true` 时，会禁用默认推理规则。 将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a>Multipart/form-data 请求推理

使用 [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。

当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> 属性设置为 `true` 时，会禁用默认行为。 将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a>特性路由要求

特性路由是必要条件。 例如:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

不能通过在 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 访问操作。

::: moniker-end

## <a name="additional-resources"></a>其他资源

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>