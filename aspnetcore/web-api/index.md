---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 08/15/2018
uid: web-api/index
ms.openlocfilehash: e4615e5d416ba2433d55309b25ee3643c6c636ac
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206986"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="29416-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="29416-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="29416-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="29416-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="29416-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="29416-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="29416-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="29416-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="29416-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="29416-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="29416-108">从控制器（旨在用作 Web API）中的 <xref:Microsoft.AspNetCore.Mvc.ControllerBase> 类继承。</span><span class="sxs-lookup"><span data-stu-id="29416-108">Inherit from the <xref:Microsoft.AspNetCore.Mvc.ControllerBase> class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="29416-109">例如:</span><span class="sxs-lookup"><span data-stu-id="29416-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

<span data-ttu-id="29416-110">通过 `ControllerBase` 类可使用一些属性和方法。</span><span class="sxs-lookup"><span data-stu-id="29416-110">The `ControllerBase` class provides access to several properties and methods.</span></span> <span data-ttu-id="29416-111">在前面的代码中，示例包括 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>。</span><span class="sxs-lookup"><span data-stu-id="29416-111">In the preceding code, examples include <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>.</span></span> <span data-ttu-id="29416-112">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="29416-112">These methods are called within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="29416-113">将使用 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState>属性（还可由 `ControllerBase` 提供）处理请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="29416-113">The <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState> property, also provided by `ControllerBase`, is accessed to handle request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="29416-114">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="29416-114">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="29416-115">ASP.NET Core 2.1 引入了 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="29416-115">ASP.NET Core 2.1 introduces the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="29416-116">例如:</span><span class="sxs-lookup"><span data-stu-id="29416-116">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="29416-117">需要兼容性版本 2.1 或更高版本（通过 <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 设置）来使用此属性。</span><span class="sxs-lookup"><span data-stu-id="29416-117">A compatibility version of 2.1 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute.</span></span> <span data-ttu-id="29416-118">例如，Startup.ConfigureServices 中突出显示的代码设置了 2.2 兼容性标志：</span><span class="sxs-lookup"><span data-stu-id="29416-118">For example, the highlighted code in *Startup.ConfigureServices* sets the 2.2 compatibility flag:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

<span data-ttu-id="29416-119">有关更多信息，请参见<xref:mvc/compatibility-version>。</span><span class="sxs-lookup"><span data-stu-id="29416-119">For more information, see <xref:mvc/compatibility-version>.</span></span>

<span data-ttu-id="29416-120">`[ApiController]` 特性通常结合 `ControllerBase` 来为控制器启用特定于 REST 行为。</span><span class="sxs-lookup"><span data-stu-id="29416-120">The `[ApiController]` attribute is commonly coupled with `ControllerBase` to enable REST-specific behavior for controllers.</span></span> <span data-ttu-id="29416-121">通过 `ControllerBase` 可使用<xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*> 等方法。</span><span class="sxs-lookup"><span data-stu-id="29416-121">`ControllerBase` provides access to methods such as <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*>.</span></span>

<span data-ttu-id="29416-122">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="29416-122">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="29416-123">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="29416-123">The following sections describe convenience features added by the attribute.</span></span>

### <a name="problem-details-responses-for-error-status-codes"></a><span data-ttu-id="29416-124">错误状态代码的问题详细信息响应</span><span class="sxs-lookup"><span data-stu-id="29416-124">Problem details responses for error status codes</span></span>

<span data-ttu-id="29416-125">ASP.NET Core 2.1 及更高版本包括 [ProblemDetails](xref:Microsoft.AspNetCore.Mvc.ProblemDetails)，这是一种基于 [RFC 7807 规范](https://tools.ietf.org/html/rfc7807)的类型。</span><span class="sxs-lookup"><span data-stu-id="29416-125">ASP.NET Core 2.1 and later includes [ProblemDetails](xref:Microsoft.AspNetCore.Mvc.ProblemDetails), a type based on the [RFC 7807 specification](https://tools.ietf.org/html/rfc7807).</span></span> <span data-ttu-id="29416-126">`ProblemDetails` 类型提供了标准化格式，用于传达 HTTP 响应中计算机可读的错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="29416-126">The `ProblemDetails` type provides a standardized format for conveying machine readable details of errors in a HTTP response.</span></span>

<span data-ttu-id="29416-127">在 ASP.NET Core 2.2 及更高版本中，MVC 将错误状态代码结果（状态代码 400 及更高）转换为带 `ProblemDetails` 的结果。</span><span class="sxs-lookup"><span data-stu-id="29416-127">In ASP.NET Core 2.2 and later, MVC transforms error status code results (status code 400 and higher) to a result with `ProblemDetails`.</span></span> <span data-ttu-id="29416-128">考虑下列代码：</span><span class="sxs-lookup"><span data-stu-id="29416-128">Consider the following code:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_ProblemDetails_StatusCode&highlight=4)]

<span data-ttu-id="29416-129">`NotFound` 结果的 HTTP 响应具有 404 状态代码，其 `ProblemDetails` 主体如下所示：</span><span class="sxs-lookup"><span data-stu-id="29416-129">The HTTP response for the `NotFound` result has a 404 status code with a `ProblemDetails` body similar to the following:</span></span>

```js
{
    type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    title: "Not Found",
    status: 404,
    traceId: "0HLHLV31KRN83:00000001"
}
```

<span data-ttu-id="29416-130">需具备 2.2 版本或更高版本的兼容性标志，才可使用问题详细信息功能。</span><span class="sxs-lookup"><span data-stu-id="29416-130">The problem details feature requires a compatibility flag of 2.2 or later.</span></span> <span data-ttu-id="29416-131">当 [SuppressMapClientErrors](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressMapClientErrors> -->属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="29416-131">The default behavior is disabled when the [SuppressMapClientErrors](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressMapClientErrors> --> property is set to `true`.</span></span> <span data-ttu-id="29416-132">下面突出显示的 `Startup.ConfigureServices` 代码会禁用问题详细信息：</span><span class="sxs-lookup"><span data-stu-id="29416-132">The following highlighted code from `Startup.ConfigureServices` disables problem details:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=8)]

<span data-ttu-id="29416-133">使用 [ClientErrorMapping](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.ClientErrorMapping> -->属性配置 `ProblemDetails` 响应的内容。</span><span class="sxs-lookup"><span data-stu-id="29416-133">Use the [ClientErrorMapping](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  Until these resolve, link to the parent class <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.ClientErrorMapping> --> property to configure the contents of the `ProblemDetails` response.</span></span> <span data-ttu-id="29416-134">例如，以下代码会更新 404 响应的 `type` 属性：</span><span class="sxs-lookup"><span data-stu-id="29416-134">For example, the following code updates the `type` property for 404 responses:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=10)]

### <a name="automatic-http-400-responses"></a><span data-ttu-id="29416-135">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="29416-135">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="29416-136">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="29416-136">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="29416-137">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="29416-137">The following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

<span data-ttu-id="29416-138">使用 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> 自定义所生成的响应的输出。</span><span class="sxs-lookup"><span data-stu-id="29416-138">Use <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> to customize the output of the the resulting response.</span></span>

<span data-ttu-id="29416-139">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="29416-139">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> property is set to `true`.</span></span> <span data-ttu-id="29416-140">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="29416-140">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

<span data-ttu-id="29416-141">使用 2.2 或更高版本的兼容性标志时，为 400 响应返回的默认响应类型为 <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>。</span><span class="sxs-lookup"><span data-stu-id="29416-141">With a compatibility flag of 2.2 or later, the default response type returned for 400 responses is a <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>.</span></span> <span data-ttu-id="29416-142">通过 [SuppressUseValidationProblemDetailsForInvalidModelStateResponses](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressUseValidationProblemDetailsForInvalidModelStateResponses> --> 属性使用 ASP.NET Core 2.1 错误格式。</span><span class="sxs-lookup"><span data-stu-id="29416-142">Use the [SuppressUseValidationProblemDetailsForInvalidModelStateResponses](/dotnet/api/microsoft.aspnetcore.Mvc.ApiBehaviorOptions) <!--  <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressUseValidationProblemDetailsForInvalidModelStateResponses> --> property to use the ASP.NET Core 2.1 error format.</span></span>

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="29416-143">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="29416-143">Binding source parameter inference</span></span>

<span data-ttu-id="29416-144">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="29416-144">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="29416-145">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="29416-145">The following binding source attributes exist:</span></span>

|<span data-ttu-id="29416-146">特性</span><span class="sxs-lookup"><span data-stu-id="29416-146">Attribute</span></span>|<span data-ttu-id="29416-147">绑定源</span><span class="sxs-lookup"><span data-stu-id="29416-147">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="29416-148">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span><span class="sxs-lookup"><span data-stu-id="29416-148">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span></span>     | <span data-ttu-id="29416-149">请求正文</span><span class="sxs-lookup"><span data-stu-id="29416-149">Request body</span></span> |
|<span data-ttu-id="29416-150">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span><span class="sxs-lookup"><span data-stu-id="29416-150">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span></span>     | <span data-ttu-id="29416-151">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="29416-151">Form data in the request body</span></span> |
|<span data-ttu-id="29416-152">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span><span class="sxs-lookup"><span data-stu-id="29416-152">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span></span> | <span data-ttu-id="29416-153">请求标头</span><span class="sxs-lookup"><span data-stu-id="29416-153">Request header</span></span> |
|<span data-ttu-id="29416-154">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span><span class="sxs-lookup"><span data-stu-id="29416-154">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span></span>   | <span data-ttu-id="29416-155">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="29416-155">Request query string parameter</span></span> |
|<span data-ttu-id="29416-156">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span><span class="sxs-lookup"><span data-stu-id="29416-156">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span></span>   | <span data-ttu-id="29416-157">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="29416-157">Route data from the current request</span></span> |
|<span data-ttu-id="29416-158">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="29416-158">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="29416-159">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="29416-159">The request service injected as an action parameter</span></span> |

> [!WARNING]
> <span data-ttu-id="29416-160">当值可能包含 `%2f`（即 `/`）时，请勿使用 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="29416-160">Don't use `[FromRoute]` when values might contain `%2f` (that is `/`).</span></span> <span data-ttu-id="29416-161">`%2f` 不会转换为 `/`（非转移形式）。</span><span class="sxs-lookup"><span data-stu-id="29416-161">`%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="29416-162">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="29416-162">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="29416-163">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="29416-163">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="29416-164">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="29416-164">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

<span data-ttu-id="29416-165">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="29416-165">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="29416-166">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="29416-166">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="29416-167">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="29416-167">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="29416-168">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="29416-168">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="29416-169">此规则不适用于具有特殊含义的任何复杂的内置类型，如 <xref:Microsoft.AspNetCore.Http.IFormCollection> 和 <xref:System.Threading.CancellationToken>。</span><span class="sxs-lookup"><span data-stu-id="29416-169">An exception to this rule is any complex, built-in type with a special meaning, such as <xref:Microsoft.AspNetCore.Http.IFormCollection> and <xref:System.Threading.CancellationToken>.</span></span> <span data-ttu-id="29416-170">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="29416-170">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="29416-171">对于简单类型（例如 `string` 或 `int`），推断不出 `[FromBody]`。</span><span class="sxs-lookup"><span data-stu-id="29416-171">`[FromBody]` isn't inferred for simple types such as `string` or `int`.</span></span> <span data-ttu-id="29416-172">因此，如果需要该功能，对于简单类型，应使用 `[FromBody]` 属性。</span><span class="sxs-lookup"><span data-stu-id="29416-172">Therefore, the `[FromBody]` attribute should be used for simple types when that functionality is desired.</span></span> <span data-ttu-id="29416-173">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="29416-173">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="29416-174">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="29416-174">For example, the following action signatures cause an exception:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* <span data-ttu-id="29416-175">[FromForm] 是针对 <xref:Microsoft.AspNetCore.Http.IFormFile> 和 <xref:Microsoft.AspNetCore.Http.IFormFileCollection> 类型的操作参数推断出来的。</span><span class="sxs-lookup"><span data-stu-id="29416-175">**[FromForm]** is inferred for action parameters of type <xref:Microsoft.AspNetCore.Http.IFormFile> and <xref:Microsoft.AspNetCore.Http.IFormFileCollection>.</span></span> <span data-ttu-id="29416-176">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="29416-176">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="29416-177">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="29416-177">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="29416-178">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="29416-178">When more than one route matches an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="29416-179">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="29416-179">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="29416-180">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> 属性设置为 `true` 时，会禁用默认推理规则。</span><span class="sxs-lookup"><span data-stu-id="29416-180">The default inference rules are disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> property is set to `true`.</span></span> <span data-ttu-id="29416-181">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="29416-181">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="29416-182">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="29416-182">Multipart/form-data request inference</span></span>

<span data-ttu-id="29416-183">使用 [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="29416-183">When an action parameter is annotated with the [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="29416-184">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="29416-184">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> property is set to `true`.</span></span> <span data-ttu-id="29416-185">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="29416-185">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a><span data-ttu-id="29416-186">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="29416-186">Attribute routing requirement</span></span>

<span data-ttu-id="29416-187">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="29416-187">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="29416-188">例如:</span><span class="sxs-lookup"><span data-stu-id="29416-188">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="29416-189">不能通过在 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 访问操作。</span><span class="sxs-lookup"><span data-stu-id="29416-189">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> or by <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> in *Startup.Configure*.</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="29416-190">其他资源</span><span class="sxs-lookup"><span data-stu-id="29416-190">Additional resources</span></span>

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
