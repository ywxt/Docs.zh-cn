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
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="53f59-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="53f59-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="53f59-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="53f59-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="53f59-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="53f59-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="53f59-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="53f59-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="53f59-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="53f59-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="53f59-108">从控制器（旨在用作 Web API）中的 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 类继承。</span><span class="sxs-lookup"><span data-stu-id="53f59-108">Inherit from the [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="53f59-109">例如:</span><span class="sxs-lookup"><span data-stu-id="53f59-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="53f59-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="53f59-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="53f59-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="53f59-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end

<span data-ttu-id="53f59-112">通过 `ControllerBase` 类可使用大量属性和方法。</span><span class="sxs-lookup"><span data-stu-id="53f59-112">The `ControllerBase` class provides access to numerous properties and methods.</span></span> <span data-ttu-id="53f59-113">前面的示例中包含某些此类方法，如 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 和 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)。</span><span class="sxs-lookup"><span data-stu-id="53f59-113">In the preceding example, some such methods include [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) and [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span></span> <span data-ttu-id="53f59-114">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="53f59-114">These methods are invoked within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="53f59-115">将使用 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 属性（还可由 `ControllerBase` 提供）执行请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="53f59-115">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property, also provided by `ControllerBase`, is accessed to perform request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="53f59-116">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="53f59-116">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="53f59-117">ASP.NET Core 2.1 引入了 `[ApiController]` 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="53f59-117">ASP.NET Core 2.1 introduces the `[ApiController]` attribute to denote a web API controller class.</span></span> <span data-ttu-id="53f59-118">例如:</span><span class="sxs-lookup"><span data-stu-id="53f59-118">For example:</span></span>

<span data-ttu-id="53f59-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="53f59-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span></span>

<span data-ttu-id="53f59-120">此特性通常与 `ControllerBase` 配合使用以获得其他有用的方法和属性。</span><span class="sxs-lookup"><span data-stu-id="53f59-120">This attribute is commonly coupled with `ControllerBase` to gain access to useful methods and properties.</span></span> <span data-ttu-id="53f59-121">通过 `ControllerBase` 可使用 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 和 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file) 等方法。</span><span class="sxs-lookup"><span data-stu-id="53f59-121">`ControllerBase` provides access to methods such as [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) and [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span></span>

<span data-ttu-id="53f59-122">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="53f59-122">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

<span data-ttu-id="53f59-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span><span class="sxs-lookup"><span data-stu-id="53f59-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span></span>

<span data-ttu-id="53f59-124">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="53f59-124">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="53f59-125">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="53f59-125">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="53f59-126">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="53f59-126">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="53f59-127">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="53f59-127">The following code becomes unnecessary in your actions:</span></span>

<span data-ttu-id="53f59-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span><span class="sxs-lookup"><span data-stu-id="53f59-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span></span>

<span data-ttu-id="53f59-129">在 Startup.ConfigureServices 中使用以下代码将禁用此默认行为：</span><span class="sxs-lookup"><span data-stu-id="53f59-129">This default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="53f59-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span><span class="sxs-lookup"><span data-stu-id="53f59-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span></span>

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="53f59-131">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="53f59-131">Binding source parameter inference</span></span>

<span data-ttu-id="53f59-132">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="53f59-132">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="53f59-133">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="53f59-133">The following binding source attributes exist:</span></span>

|<span data-ttu-id="53f59-134">特性</span><span class="sxs-lookup"><span data-stu-id="53f59-134">Attribute</span></span>|<span data-ttu-id="53f59-135">绑定源</span><span class="sxs-lookup"><span data-stu-id="53f59-135">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="53f59-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span><span class="sxs-lookup"><span data-stu-id="53f59-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span></span>     | <span data-ttu-id="53f59-137">请求正文</span><span class="sxs-lookup"><span data-stu-id="53f59-137">Request body</span></span> |
|<span data-ttu-id="53f59-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span><span class="sxs-lookup"><span data-stu-id="53f59-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span></span>     | <span data-ttu-id="53f59-139">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="53f59-139">Form data in the request body</span></span> |
|<span data-ttu-id="53f59-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span><span class="sxs-lookup"><span data-stu-id="53f59-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span></span> | <span data-ttu-id="53f59-141">请求标头</span><span class="sxs-lookup"><span data-stu-id="53f59-141">Request header</span></span> |
|<span data-ttu-id="53f59-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span><span class="sxs-lookup"><span data-stu-id="53f59-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span></span>   | <span data-ttu-id="53f59-143">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="53f59-143">Request query string parameter</span></span> |
|<span data-ttu-id="53f59-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span><span class="sxs-lookup"><span data-stu-id="53f59-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span></span>   | <span data-ttu-id="53f59-145">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="53f59-145">Route data from the current request</span></span> |
|<span data-ttu-id="53f59-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="53f59-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="53f59-147">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="53f59-147">The request service injected as an action parameter</span></span> |

> [!NOTE]
> <span data-ttu-id="53f59-148">如果值可能包含 `%2f`（即 `/`），请不要使用 `[FromRoute]`，因为 `%2f` 不会非转义为 `/`。</span><span class="sxs-lookup"><span data-stu-id="53f59-148">Do **not** use `[FromRoute]` when values might contain `%2f` (that is `/`) because `%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="53f59-149">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="53f59-149">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="53f59-150">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="53f59-150">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="53f59-151">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="53f59-151">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

<span data-ttu-id="53f59-152">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="53f59-152">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span></span>

<span data-ttu-id="53f59-153">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="53f59-153">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="53f59-154">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="53f59-154">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="53f59-155">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="53f59-155">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="53f59-156">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="53f59-156">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="53f59-157">此规则不适用于具有特殊含义的任何复杂的内置类型，如 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 和 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)。</span><span class="sxs-lookup"><span data-stu-id="53f59-157">An exception to this rule is any complex, built-in type with a special meaning, such as [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) and [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span></span> <span data-ttu-id="53f59-158">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="53f59-158">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="53f59-159">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="53f59-159">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="53f59-160">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="53f59-160">For example, the following action signatures cause an exception:</span></span>

<span data-ttu-id="53f59-161">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span><span class="sxs-lookup"><span data-stu-id="53f59-161">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span></span>

* <span data-ttu-id="53f59-162">**[FromForm]**，针对 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 类型的操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="53f59-162">**[FromForm]** is inferred for action parameters of type [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span></span> <span data-ttu-id="53f59-163">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="53f59-163">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="53f59-164">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="53f59-164">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="53f59-165">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="53f59-165">When multiple routes match an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="53f59-166">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="53f59-166">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="53f59-167">在 Startup.ConfigureServices 中使用以下代码将禁用默认推理规则：</span><span class="sxs-lookup"><span data-stu-id="53f59-167">The default inference rules are disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="53f59-168">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span><span class="sxs-lookup"><span data-stu-id="53f59-168">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span></span>

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="53f59-169">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="53f59-169">Multipart/form-data request inference</span></span>

<span data-ttu-id="53f59-170">使用 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="53f59-170">When an action parameter is annotated with the [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="53f59-171">在 Startup.ConfigureServices 中使用以下代码将禁用默认行为：</span><span class="sxs-lookup"><span data-stu-id="53f59-171">The default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="53f59-172">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="53f59-172">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span></span>

### <a name="attribute-routing-requirement"></a><span data-ttu-id="53f59-173">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="53f59-173">Attribute routing requirement</span></span>

<span data-ttu-id="53f59-174">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="53f59-174">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="53f59-175">例如:</span><span class="sxs-lookup"><span data-stu-id="53f59-175">For example:</span></span>

<span data-ttu-id="53f59-176">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span><span class="sxs-lookup"><span data-stu-id="53f59-176">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span></span>

<span data-ttu-id="53f59-177">不能通过在 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 访问操作。</span><span class="sxs-lookup"><span data-stu-id="53f59-177">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) or by [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) in *Startup.Configure*.</span></span>
::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="53f59-178">其他资源</span><span class="sxs-lookup"><span data-stu-id="53f59-178">Additional resources</span></span>

* [<span data-ttu-id="53f59-179">控制器操作返回类型</span><span class="sxs-lookup"><span data-stu-id="53f59-179">Controller action return types</span></span>](xref:web-api/action-return-types)
* [<span data-ttu-id="53f59-180">自定义格式化程序</span><span class="sxs-lookup"><span data-stu-id="53f59-180">Custom formatters</span></span>](xref:web-api/advanced/custom-formatters)
* [<span data-ttu-id="53f59-181">格式化响应数据</span><span class="sxs-lookup"><span data-stu-id="53f59-181">Format response data</span></span>](xref:web-api/advanced/formatting)
* [<span data-ttu-id="53f59-182">使用 Swagger 的帮助页</span><span class="sxs-lookup"><span data-stu-id="53f59-182">Help pages using Swagger</span></span>](xref:tutorials/web-api-help-pages-using-swagger)
* [<span data-ttu-id="53f59-183">路由到控制器操作</span><span class="sxs-lookup"><span data-stu-id="53f59-183">Routing to controller actions</span></span>](xref:mvc/controllers/routing)
