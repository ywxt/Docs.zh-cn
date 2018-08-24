---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 08/15/2018
uid: web-api/index
ms.openlocfilehash: d410f28ff7fda3bf33f73c06b3e626dfd4ee7dd8
ms.sourcegitcommit: 5a2456cbf429069dc48aaa2823cde14100e4c438
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "41822135"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="93f55-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="93f55-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="93f55-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="93f55-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="93f55-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="93f55-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="93f55-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="93f55-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="93f55-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="93f55-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="93f55-108">从控制器（旨在用作 Web API）中的 <xref:Microsoft.AspNetCore.Mvc.ControllerBase> 类继承。</span><span class="sxs-lookup"><span data-stu-id="93f55-108">Inherit from the <xref:Microsoft.AspNetCore.Mvc.ControllerBase> class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="93f55-109">例如:</span><span class="sxs-lookup"><span data-stu-id="93f55-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

<span data-ttu-id="93f55-110">通过 `ControllerBase` 类可使用一些属性和方法。</span><span class="sxs-lookup"><span data-stu-id="93f55-110">The `ControllerBase` class provides access to several properties and methods.</span></span> <span data-ttu-id="93f55-111">在前面的代码中，示例包括 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>。</span><span class="sxs-lookup"><span data-stu-id="93f55-111">In the preceding code, examples include <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>.</span></span> <span data-ttu-id="93f55-112">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="93f55-112">These methods are called within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="93f55-113">将使用 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState>属性（还可由 `ControllerBase` 提供）处理请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="93f55-113">The <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState> property, also provided by `ControllerBase`, is accessed to handle request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="93f55-114">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="93f55-114">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="93f55-115">ASP.NET Core 2.1 引入了 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="93f55-115">ASP.NET Core 2.1 introduces the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="93f55-116">例如:</span><span class="sxs-lookup"><span data-stu-id="93f55-116">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="93f55-117">需要兼容性版本 2.1 或更高版本（通过 <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 设置）来使用此属性。</span><span class="sxs-lookup"><span data-stu-id="93f55-117">A compatibility version of 2.1 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute.</span></span> <span data-ttu-id="93f55-118">例如，Startup.ConfigureServices 中突出显示的代码设置了 2.1 兼容性标志：</span><span class="sxs-lookup"><span data-stu-id="93f55-118">For example, the highlighted code in *Startup.ConfigureServices* sets the 2.1 compatibility flag:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

<span data-ttu-id="93f55-119">有关更多信息，请参见<xref:mvc/compatibility-version>。</span><span class="sxs-lookup"><span data-stu-id="93f55-119">For more information, see <xref:mvc/compatibility-version>.</span></span>

<span data-ttu-id="93f55-120">`[ApiController]` 特性通常结合 `ControllerBase` 来为控制器启用特定于 REST 行为。</span><span class="sxs-lookup"><span data-stu-id="93f55-120">The `[ApiController]` attribute is commonly coupled with `ControllerBase` to enable REST-specific behavior for controllers.</span></span> <span data-ttu-id="93f55-121">通过 `ControllerBase` 可使用<xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> 和 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*> 等方法。</span><span class="sxs-lookup"><span data-stu-id="93f55-121">`ControllerBase` provides access to methods such as <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*>.</span></span>

<span data-ttu-id="93f55-122">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="93f55-122">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="93f55-123">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="93f55-123">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="93f55-124">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="93f55-124">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="93f55-125">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="93f55-125">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="93f55-126">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="93f55-126">The following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

<span data-ttu-id="93f55-127">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="93f55-127">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> property is set to `true`.</span></span> <span data-ttu-id="93f55-128">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="93f55-128">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="93f55-129">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="93f55-129">Binding source parameter inference</span></span>

<span data-ttu-id="93f55-130">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="93f55-130">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="93f55-131">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="93f55-131">The following binding source attributes exist:</span></span>

|<span data-ttu-id="93f55-132">特性</span><span class="sxs-lookup"><span data-stu-id="93f55-132">Attribute</span></span>|<span data-ttu-id="93f55-133">绑定源</span><span class="sxs-lookup"><span data-stu-id="93f55-133">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="93f55-134">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span><span class="sxs-lookup"><span data-stu-id="93f55-134">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span></span>     | <span data-ttu-id="93f55-135">请求正文</span><span class="sxs-lookup"><span data-stu-id="93f55-135">Request body</span></span> |
|<span data-ttu-id="93f55-136">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span><span class="sxs-lookup"><span data-stu-id="93f55-136">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span></span>     | <span data-ttu-id="93f55-137">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="93f55-137">Form data in the request body</span></span> |
|<span data-ttu-id="93f55-138">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span><span class="sxs-lookup"><span data-stu-id="93f55-138">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span></span> | <span data-ttu-id="93f55-139">请求标头</span><span class="sxs-lookup"><span data-stu-id="93f55-139">Request header</span></span> |
|<span data-ttu-id="93f55-140">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span><span class="sxs-lookup"><span data-stu-id="93f55-140">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span></span>   | <span data-ttu-id="93f55-141">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="93f55-141">Request query string parameter</span></span> |
|<span data-ttu-id="93f55-142">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span><span class="sxs-lookup"><span data-stu-id="93f55-142">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span></span>   | <span data-ttu-id="93f55-143">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="93f55-143">Route data from the current request</span></span> |
|<span data-ttu-id="93f55-144">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="93f55-144">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="93f55-145">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="93f55-145">The request service injected as an action parameter</span></span> |

> [!WARNING]
> <span data-ttu-id="93f55-146">当值可能包含 `%2f`（即 `/`）时，请勿使用 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="93f55-146">Don't use `[FromRoute]` when values might contain `%2f` (that is `/`).</span></span> <span data-ttu-id="93f55-147">`%2f` 不会转换为 `/`（非转移形式）。</span><span class="sxs-lookup"><span data-stu-id="93f55-147">`%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="93f55-148">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="93f55-148">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="93f55-149">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="93f55-149">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="93f55-150">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="93f55-150">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

<span data-ttu-id="93f55-151">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="93f55-151">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="93f55-152">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="93f55-152">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="93f55-153">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="93f55-153">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="93f55-154">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="93f55-154">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="93f55-155">此规则不适用于具有特殊含义的任何复杂的内置类型，如 <xref:Microsoft.AspNetCore.Http.IFormCollection> 和 <xref:System.Threading.CancellationToken>。</span><span class="sxs-lookup"><span data-stu-id="93f55-155">An exception to this rule is any complex, built-in type with a special meaning, such as <xref:Microsoft.AspNetCore.Http.IFormCollection> and <xref:System.Threading.CancellationToken>.</span></span> <span data-ttu-id="93f55-156">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="93f55-156">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="93f55-157">对于简单类型（例如 `string` 或 `int`），推断不出 `[FromBody]`。</span><span class="sxs-lookup"><span data-stu-id="93f55-157">`[FromBody]` isn't inferred for simple types such as `string` or `int`.</span></span> <span data-ttu-id="93f55-158">因此，如果需要该功能，对于简单类型，应使用 `[FromBody]` 属性。</span><span class="sxs-lookup"><span data-stu-id="93f55-158">Therefore, the `[FromBody]` attribute should be used for simple types when that functionality is desired.</span></span> <span data-ttu-id="93f55-159">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="93f55-159">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="93f55-160">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="93f55-160">For example, the following action signatures cause an exception:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* <span data-ttu-id="93f55-161">[FromForm] 是针对 <xref:Microsoft.AspNetCore.Http.IFormFile> 和 <xref:Microsoft.AspNetCore.Http.IFormFileCollection> 类型的操作参数推断出来的。</span><span class="sxs-lookup"><span data-stu-id="93f55-161">**[FromForm]** is inferred for action parameters of type <xref:Microsoft.AspNetCore.Http.IFormFile> and <xref:Microsoft.AspNetCore.Http.IFormFileCollection>.</span></span> <span data-ttu-id="93f55-162">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="93f55-162">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="93f55-163">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="93f55-163">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="93f55-164">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="93f55-164">When more than one route matches an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="93f55-165">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="93f55-165">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="93f55-166">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> 属性设置为 `true` 时，会禁用默认推理规则。</span><span class="sxs-lookup"><span data-stu-id="93f55-166">The default inference rules are disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> property is set to `true`.</span></span> <span data-ttu-id="93f55-167">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="93f55-167">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="93f55-168">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="93f55-168">Multipart/form-data request inference</span></span>

<span data-ttu-id="93f55-169">使用 [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="93f55-169">When an action parameter is annotated with the [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="93f55-170">当 <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="93f55-170">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> property is set to `true`.</span></span> <span data-ttu-id="93f55-171">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="93f55-171">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a><span data-ttu-id="93f55-172">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="93f55-172">Attribute routing requirement</span></span>

<span data-ttu-id="93f55-173">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="93f55-173">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="93f55-174">例如:</span><span class="sxs-lookup"><span data-stu-id="93f55-174">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="93f55-175">不能通过在 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 访问操作。</span><span class="sxs-lookup"><span data-stu-id="93f55-175">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> or by <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> in *Startup.Configure*.</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="93f55-176">其他资源</span><span class="sxs-lookup"><span data-stu-id="93f55-176">Additional resources</span></span>

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
