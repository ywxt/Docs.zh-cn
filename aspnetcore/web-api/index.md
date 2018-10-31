---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 10/30/2018
uid: web-api/index
ms.openlocfilehash: b3e26bee5e4dc8937e810bc5db300a486437f568
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244757"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="8a0fd-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="8a0fd-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="8a0fd-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="8a0fd-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="8a0fd-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8a0fd-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="8a0fd-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="8a0fd-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="8a0fd-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="8a0fd-108">从控制器（旨在用作 Web API）中的 <xref:Microsoft.AspNetCore.Mvc.ControllerBase> 类继承。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-108">Inherit from the <xref:Microsoft.AspNetCore.Mvc.ControllerBase> class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="8a0fd-109">例如:</span><span class="sxs-lookup"><span data-stu-id="8a0fd-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

<span data-ttu-id="8a0fd-110">通过 `ControllerBase` 类可使用一些属性和方法。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-110">The `ControllerBase` class provides access to several properties and methods.</span></span> <span data-ttu-id="8a0fd-111">在前面的代码中，示例包括 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-111">In the preceding code, examples include <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>.</span></span> <span data-ttu-id="8a0fd-112">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-112">These methods are called within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="8a0fd-113">将使用 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState>属性（还可由 `ControllerBase` 提供）处理请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-113">The <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState> property, also provided by `ControllerBase`, is accessed to handle request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="annotation-with-apicontrollerattribute"></a><span data-ttu-id="8a0fd-114">使用 ApiControllerAttribute 进行注释</span><span class="sxs-lookup"><span data-stu-id="8a0fd-114">Annotation with ApiControllerAttribute</span></span>

<span data-ttu-id="8a0fd-115">ASP.NET Core 2.1 引入了 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-115">ASP.NET Core 2.1 introduces the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="8a0fd-116">例如:</span><span class="sxs-lookup"><span data-stu-id="8a0fd-116">For example:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="8a0fd-117">为在控制器级别使用此特性，需要兼容性版本 2.1 或更高版本（通过 <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 设置）。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-117">A compatibility version of 2.1 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute at the controller level.</span></span> <span data-ttu-id="8a0fd-118">例如，`Startup.ConfigureServices` 中突出显示的代码设置了 2.1 兼容性标志：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-118">For example, the highlighted code in `Startup.ConfigureServices` sets the 2.1 compatibility flag:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

<span data-ttu-id="8a0fd-119">有关更多信息，请参见<xref:mvc/compatibility-version>。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-119">For more information, see <xref:mvc/compatibility-version>.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="8a0fd-120">在 ASP.NET Core 2.2 或更高版本中，可将 `[ApiController]` 特性应用于程序集。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-120">In ASP.NET Core 2.2 or later, the `[ApiController]` attribute can be applied to an assembly.</span></span> <span data-ttu-id="8a0fd-121">以这种方式进行注释，会将 web API 行为应用到程序集中的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-121">Annotation in this manner applies web API behavior to all controllers in the assembly.</span></span> <span data-ttu-id="8a0fd-122">请注意，无法针对单个控制器执行选择退出操作。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-122">Beware that there's no way to opt out for individual controllers.</span></span> <span data-ttu-id="8a0fd-123">建议将程序集级别的特性应用于 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-123">As a recommendation, assembly-level attributes should be applied to the `Startup` class:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ApiControllerAttributeOnAssembly&highlight=1)]

<span data-ttu-id="8a0fd-124">为在程序集级别使用此特性，需要兼容性版本 2.2 或更高版本（通过 <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 设置）。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-124">A compatibility version of 2.2 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute at the assembly level.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="8a0fd-125">`[ApiController]` 特性通常结合 `ControllerBase` 来为控制器启用特定于 REST 行为。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-125">The `[ApiController]` attribute is commonly coupled with `ControllerBase` to enable REST-specific behavior for controllers.</span></span> <span data-ttu-id="8a0fd-126">通过 `ControllerBase` 可使用<xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*> 等方法。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-126">`ControllerBase` provides access to methods such as <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*>.</span></span>

<span data-ttu-id="8a0fd-127">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-127">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="8a0fd-128">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-128">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="8a0fd-129">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="8a0fd-129">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="8a0fd-130">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-130">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="8a0fd-131">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-131">The following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

<span data-ttu-id="8a0fd-132">使用 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> 自定义所生成的响应的输出。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-132">Use <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> to customize the output of the resulting response.</span></span>

<span data-ttu-id="8a0fd-133">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-133">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> property is set to `true`.</span></span> <span data-ttu-id="8a0fd-134">在 `Startup.ConfigureServices` 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);` 后添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-134">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);`:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=7)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="8a0fd-135">使用 2.2 或更高版本的兼容性标志时，HTTP 400 响应的默认响应类型为 <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-135">With a compatibility flag of 2.2 or later, the default response type for HTTP 400 responses is <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>.</span></span> <span data-ttu-id="8a0fd-136">`ValidationProblemDetails` 类型符合 [RFC 7807 规范](https://tools.ietf.org/html/rfc7807)。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-136">The `ValidationProblemDetails` type complies with the [RFC 7807 specification](https://tools.ietf.org/html/rfc7807).</span></span> <span data-ttu-id="8a0fd-137">将 `SuppressUseValidationProblemDetailsForInvalidModelStateResponses` 属性设置为 `true` 以返回 ASP.NET Core 2.1 错误格式 <xref:Microsoft.AspNetCore.Mvc.SerializableError>。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-137">Set the `SuppressUseValidationProblemDetailsForInvalidModelStateResponses` property to `true` to instead return the ASP.NET Core 2.1 error format of <xref:Microsoft.AspNetCore.Mvc.SerializableError>.</span></span> <span data-ttu-id="8a0fd-138">在 `Startup.ConfigureServices` 中添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-138">Add the following code in `Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2)
    .ConfigureApiBehaviorOptions(options =>
    {
        options
          .SuppressUseValidationProblemDetailsForInvalidModelStateResponses = true;
    });
```

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="8a0fd-139">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="8a0fd-139">Binding source parameter inference</span></span>

<span data-ttu-id="8a0fd-140">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-140">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="8a0fd-141">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-141">The following binding source attributes exist:</span></span>

|<span data-ttu-id="8a0fd-142">特性</span><span class="sxs-lookup"><span data-stu-id="8a0fd-142">Attribute</span></span>|<span data-ttu-id="8a0fd-143">绑定源</span><span class="sxs-lookup"><span data-stu-id="8a0fd-143">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="8a0fd-144">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-144">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span></span>     | <span data-ttu-id="8a0fd-145">请求正文</span><span class="sxs-lookup"><span data-stu-id="8a0fd-145">Request body</span></span> |
|<span data-ttu-id="8a0fd-146">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-146">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span></span>     | <span data-ttu-id="8a0fd-147">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="8a0fd-147">Form data in the request body</span></span> |
|<span data-ttu-id="8a0fd-148">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-148">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span></span> | <span data-ttu-id="8a0fd-149">请求标头</span><span class="sxs-lookup"><span data-stu-id="8a0fd-149">Request header</span></span> |
|<span data-ttu-id="8a0fd-150">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-150">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span></span>   | <span data-ttu-id="8a0fd-151">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="8a0fd-151">Request query string parameter</span></span> |
|<span data-ttu-id="8a0fd-152">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-152">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span></span>   | <span data-ttu-id="8a0fd-153">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="8a0fd-153">Route data from the current request</span></span> |
|<span data-ttu-id="8a0fd-154">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="8a0fd-154">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="8a0fd-155">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="8a0fd-155">The request service injected as an action parameter</span></span> |

> [!WARNING]
> <span data-ttu-id="8a0fd-156">当值可能包含 `%2f`（即 `/`）时，请勿使用 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-156">Don't use `[FromRoute]` when values might contain `%2f` (that is `/`).</span></span> <span data-ttu-id="8a0fd-157">`%2f` 不会转换为 `/`（非转移形式）。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-157">`%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="8a0fd-158">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-158">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="8a0fd-159">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-159">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="8a0fd-160">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-160">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

<span data-ttu-id="8a0fd-161">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-161">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="8a0fd-162">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-162">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="8a0fd-163">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-163">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="8a0fd-164">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-164">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="8a0fd-165">此规则不适用于具有特殊含义的任何复杂的内置类型，如 <xref:Microsoft.AspNetCore.Http.IFormCollection> 和 <xref:System.Threading.CancellationToken>。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-165">An exception to this rule is any complex, built-in type with a special meaning, such as <xref:Microsoft.AspNetCore.Http.IFormCollection> and <xref:System.Threading.CancellationToken>.</span></span> <span data-ttu-id="8a0fd-166">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-166">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="8a0fd-167">对于简单类型（例如 `string` 或 `int`），推断不出 `[FromBody]`。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-167">`[FromBody]` isn't inferred for simple types such as `string` or `int`.</span></span> <span data-ttu-id="8a0fd-168">因此，如果需要该功能，对于简单类型，应使用 `[FromBody]` 属性。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-168">Therefore, the `[FromBody]` attribute should be used for simple types when that functionality is needed.</span></span> <span data-ttu-id="8a0fd-169">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-169">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="8a0fd-170">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-170">For example, the following action signatures cause an exception:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* <span data-ttu-id="8a0fd-171">[FromForm] 是针对 <xref:Microsoft.AspNetCore.Http.IFormFile> 和 <xref:Microsoft.AspNetCore.Http.IFormFileCollection> 类型的操作参数推断出来的。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-171">**[FromForm]** is inferred for action parameters of type <xref:Microsoft.AspNetCore.Http.IFormFile> and <xref:Microsoft.AspNetCore.Http.IFormFileCollection>.</span></span> <span data-ttu-id="8a0fd-172">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-172">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="8a0fd-173">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-173">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="8a0fd-174">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-174">When more than one route matches an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="8a0fd-175">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-175">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="8a0fd-176">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> 属性设置为 `true` 时，会禁用默认推理规则。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-176">The default inference rules are disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> property is set to `true`.</span></span> <span data-ttu-id="8a0fd-177">在 `Startup.ConfigureServices` 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);` 后添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-177">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);`:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=6)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="8a0fd-178">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="8a0fd-178">Multipart/form-data request inference</span></span>

<span data-ttu-id="8a0fd-179">使用 [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-179">When an action parameter is annotated with the [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="8a0fd-180">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-180">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> property is set to `true`.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="8a0fd-181">在 `Startup.ConfigureServices` 中添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-181">Add the following code in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="8a0fd-182">在 `Startup.ConfigureServices` 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-182">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="attribute-routing-requirement"></a><span data-ttu-id="8a0fd-183">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="8a0fd-183">Attribute routing requirement</span></span>

<span data-ttu-id="8a0fd-184">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-184">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="8a0fd-185">例如:</span><span class="sxs-lookup"><span data-stu-id="8a0fd-185">For example:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="8a0fd-186">不能通过 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> 中定义的[传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 `Startup.Configure` 中的 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 访问操作。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-186">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> or by <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> in `Startup.Configure`.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

### <a name="problem-details-responses-for-error-status-codes"></a><span data-ttu-id="8a0fd-187">错误状态代码的问题详细信息响应</span><span class="sxs-lookup"><span data-stu-id="8a0fd-187">Problem details responses for error status codes</span></span>

<span data-ttu-id="8a0fd-188">在 ASP.NET Core 2.2 或更高版本中，MVC 会将错误结果（状态代码为 400 或更高的结果）转换为状态代码为 <xref:Microsoft.AspNetCore.Mvc.ProblemDetails> 的结果。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-188">In ASP.NET Core 2.2 or later, MVC transforms an error result (a result with status code 400 or higher) to a result with <xref:Microsoft.AspNetCore.Mvc.ProblemDetails>.</span></span> <span data-ttu-id="8a0fd-189">`ProblemDetails` 为：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-189">`ProblemDetails` is:</span></span>

* <span data-ttu-id="8a0fd-190">基于 [RFC 7807 规范](https://tools.ietf.org/html/rfc7807)的类型。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-190">A type based on the [RFC 7807 specification](https://tools.ietf.org/html/rfc7807).</span></span>
* <span data-ttu-id="8a0fd-191">用于指定 HTTP 响应中计算机可读的错误详细信息的标准化格式。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-191">A standardized format for specifying machine-readable error details in an HTTP response.</span></span>

<span data-ttu-id="8a0fd-192">考虑在控制器操作中使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-192">Consider the following code in a controller action:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Controllers/ProductsController.cs?name=snippet_ProblemDetailsStatusCode)]

<span data-ttu-id="8a0fd-193">`NotFound` 的 HTTP 响应具有 404 状态代码和 `ProblemDetails` 正文。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-193">The HTTP response for `NotFound` has a 404 status code with a `ProblemDetails` body.</span></span> <span data-ttu-id="8a0fd-194">例如:</span><span class="sxs-lookup"><span data-stu-id="8a0fd-194">For example:</span></span>

```json
{
    type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    title: "Not Found",
    status: 404,
    traceId: "0HLHLV31KRN83:00000001"
}
```

<span data-ttu-id="8a0fd-195">需具备 2.2 版本或更高版本的兼容性标志，才可使用问题详细信息功能。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-195">The problem details feature requires a compatibility flag of 2.2 or later.</span></span> <span data-ttu-id="8a0fd-196">当 `SuppressMapClientErrors` 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-196">The default behavior is disabled when the `SuppressMapClientErrors` property is set to `true`.</span></span> <span data-ttu-id="8a0fd-197">在 `Startup.ConfigureServices` 中添加下列代码：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-197">Add the following code in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=8)]

<span data-ttu-id="8a0fd-198">使用 `ClientErrorMapping` 属性配置 `ProblemDetails` 响应的内容。</span><span class="sxs-lookup"><span data-stu-id="8a0fd-198">Use the `ClientErrorMapping` property to configure the contents of the `ProblemDetails` response.</span></span> <span data-ttu-id="8a0fd-199">例如，以下代码会更新 404 响应的 `type` 属性：</span><span class="sxs-lookup"><span data-stu-id="8a0fd-199">For example, the following code updates the `type` property for 404 responses:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=10-11)]

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="8a0fd-200">其他资源</span><span class="sxs-lookup"><span data-stu-id="8a0fd-200">Additional resources</span></span>

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
