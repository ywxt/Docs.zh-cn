---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: web-api/index
ms.openlocfilehash: f0368258d078673ab5eab21c5ce07f2437cb8ea4
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="build-web-apis-with-aspnet-core"></a>使用 ASP.NET Core 构建 Web API

作者：[Scott Addie](https://github.com/scottaddie)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。

## <a name="derive-class-from-controllerbase"></a>从 ControllerBase 派生类

从控制器（旨在用作 Web API）中的 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 类继承。 例如:

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]
::: moniker-end

通过 `ControllerBase` 类可使用大量属性和方法。 前面的示例中包含某些此类方法，如 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 和 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)。 将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。 将使用 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 属性（还可由 `ControllerBase` 提供）执行请求模型验证。

::: moniker range=">= aspnetcore-2.1"
## <a name="annotate-class-with-apicontrollerattribute"></a>使用 ApiControllerAttribute 批注类

ASP.NET Core 2.1 引入了 `[ApiController]` 特性，用于批注 Web API 控制器类。 例如:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

此特性通常与 `ControllerBase` 配合使用以获得其他有用的方法和属性。 通过 `ControllerBase` 可使用 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 和 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file) 等方法。

另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

以下各部分说明该特性添加的便利功能。

### <a name="automatic-http-400-responses"></a>自动 HTTP 400 响应

验证错误会自动触发 HTTP 400 响应。 操作中不需要以下代码：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]

在 Startup.ConfigureServices 中使用以下代码将禁用此默认行为：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

### <a name="binding-source-parameter-inference"></a>绑定源参数推理

绑定源特性定义可找到操作参数值的位置。 存在以下绑定源特性：

|特性|绑定源 |
|---------|---------|
|**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**     | 请求正文 |
|**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**     | 请求正文中的表单数据 |
|**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)** | 请求标头 |
|**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**   | 请求查询字符串参数 |
|**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**   | 当前请求中的路由数据 |
|**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)** | 作为操作参数插入的请求服务 |

> [!NOTE]
> 如果值可能包含 `%2f`（即 `/`），请不要使用 `[FromRoute]`，因为 `%2f` 不会非转义为 `/`。 如果值可能包含 `%2f`，则使用 `[FromQuery]`。

没有 `[ApiController]` 特性时，将显式定义绑定源特性。 在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]

推理规则应用于操作参数的默认数据源。 这些规则将配置绑定资源，否则你可以手动应用操作参数。 绑定源特性的行为如下：

* **[FromBody]**，针对复杂类型参数进行推断。 此规则不适用于具有特殊含义的任何复杂的内置类型，如 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 和 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)。 绑定源推理代码将忽略这些特殊类型。 当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。 例如，下面的操作签名会导致异常：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* **[FromForm]**，针对 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 类型的操作参数进行推断。 该特性不针对任何简单类型或用户定义类型进行推断。
* **[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。 当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。
* **[FromQuery]**，针对任何其他操作参数进行推断。

在 Startup.ConfigureServices 中使用以下代码将禁用默认推理规则：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a>Multipart/form-data 请求推理

使用 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。

在 Startup.ConfigureServices 中使用以下代码将禁用默认行为：

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a>特性路由要求

特性路由是必要条件。 例如:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

不能通过在 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 访问操作。
::: moniker-end

## <a name="additional-resources"></a>其他资源

* [控制器操作返回类型](xref:web-api/action-return-types)
* [自定义格式化程序](xref:web-api/advanced/custom-formatters)
* [格式化响应数据](xref:web-api/advanced/formatting)
* [使用 Swagger 的帮助页](xref:tutorials/web-api-help-pages-using-swagger)
* [路由到控制器操作](xref:mvc/controllers/routing)
