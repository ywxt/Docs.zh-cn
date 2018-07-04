---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
uid: web-api/index
ms.openlocfilehash: ab672667d1ca349d80c4ca80f8d1f32f4871c7e6
ms.sourcegitcommit: 18339e3cb5a891a3ca36d8146fa83cf91c32e707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "36274961"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="2e877-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="2e877-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="2e877-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="2e877-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="2e877-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="2e877-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="2e877-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="2e877-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="2e877-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="2e877-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="2e877-108">从控制器（旨在用作 Web API）中的 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 类继承。</span><span class="sxs-lookup"><span data-stu-id="2e877-108">Inherit from the [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="2e877-109">例如:</span><span class="sxs-lookup"><span data-stu-id="2e877-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]
::: moniker-end

<span data-ttu-id="2e877-110">通过 `ControllerBase` 类可使用大量属性和方法。</span><span class="sxs-lookup"><span data-stu-id="2e877-110">The `ControllerBase` class provides access to numerous properties and methods.</span></span> <span data-ttu-id="2e877-111">前面的示例中包含某些此类方法，如 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 和 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)。</span><span class="sxs-lookup"><span data-stu-id="2e877-111">In the preceding example, some such methods include [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) and [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span></span> <span data-ttu-id="2e877-112">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="2e877-112">These methods are invoked within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="2e877-113">将使用 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 属性（还可由 `ControllerBase` 提供）执行请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="2e877-113">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property, also provided by `ControllerBase`, is accessed to perform request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="2e877-114">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="2e877-114">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="2e877-115">ASP.NET Core 2.1 引入了 [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="2e877-115">ASP.NET Core 2.1 introduces the [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="2e877-116">例如:</span><span class="sxs-lookup"><span data-stu-id="2e877-116">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="2e877-117">此特性通常与 `ControllerBase` 配合使用以获得其他有用的方法和属性。</span><span class="sxs-lookup"><span data-stu-id="2e877-117">This attribute is commonly coupled with `ControllerBase` to gain access to useful methods and properties.</span></span> <span data-ttu-id="2e877-118">通过 `ControllerBase` 可使用 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 和 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file) 等方法。</span><span class="sxs-lookup"><span data-stu-id="2e877-118">`ControllerBase` provides access to methods such as [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) and [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span></span>

<span data-ttu-id="2e877-119">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="2e877-119">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="2e877-120">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="2e877-120">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="2e877-121">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="2e877-121">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="2e877-122">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="2e877-122">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="2e877-123">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="2e877-123">The following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]

<span data-ttu-id="2e877-124">在 Startup.ConfigureServices 中使用以下代码将禁用此默认行为：</span><span class="sxs-lookup"><span data-stu-id="2e877-124">This default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="2e877-125">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="2e877-125">Binding source parameter inference</span></span>

<span data-ttu-id="2e877-126">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="2e877-126">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="2e877-127">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="2e877-127">The following binding source attributes exist:</span></span>

|<span data-ttu-id="2e877-128">特性</span><span class="sxs-lookup"><span data-stu-id="2e877-128">Attribute</span></span>|<span data-ttu-id="2e877-129">绑定源</span><span class="sxs-lookup"><span data-stu-id="2e877-129">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="2e877-130">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span><span class="sxs-lookup"><span data-stu-id="2e877-130">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span></span>     | <span data-ttu-id="2e877-131">请求正文</span><span class="sxs-lookup"><span data-stu-id="2e877-131">Request body</span></span> |
|<span data-ttu-id="2e877-132">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span><span class="sxs-lookup"><span data-stu-id="2e877-132">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span></span>     | <span data-ttu-id="2e877-133">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="2e877-133">Form data in the request body</span></span> |
|<span data-ttu-id="2e877-134">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span><span class="sxs-lookup"><span data-stu-id="2e877-134">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span></span> | <span data-ttu-id="2e877-135">请求标头</span><span class="sxs-lookup"><span data-stu-id="2e877-135">Request header</span></span> |
|<span data-ttu-id="2e877-136">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span><span class="sxs-lookup"><span data-stu-id="2e877-136">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span></span>   | <span data-ttu-id="2e877-137">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="2e877-137">Request query string parameter</span></span> |
|<span data-ttu-id="2e877-138">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span><span class="sxs-lookup"><span data-stu-id="2e877-138">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span></span>   | <span data-ttu-id="2e877-139">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="2e877-139">Route data from the current request</span></span> |
|<span data-ttu-id="2e877-140">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="2e877-140">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="2e877-141">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="2e877-141">The request service injected as an action parameter</span></span> |

> [!NOTE]
> <span data-ttu-id="2e877-142">如果值可能包含 `%2f`（即 `/`），请不要使用 `[FromRoute]`，因为 `%2f` 不会非转义为 `/`。</span><span class="sxs-lookup"><span data-stu-id="2e877-142">Do **not** use `[FromRoute]` when values might contain `%2f` (that is `/`) because `%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="2e877-143">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="2e877-143">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="2e877-144">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="2e877-144">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="2e877-145">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="2e877-145">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]

<span data-ttu-id="2e877-146">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="2e877-146">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="2e877-147">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="2e877-147">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="2e877-148">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="2e877-148">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="2e877-149">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="2e877-149">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="2e877-150">此规则不适用于具有特殊含义的任何复杂的内置类型，如 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 和 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)。</span><span class="sxs-lookup"><span data-stu-id="2e877-150">An exception to this rule is any complex, built-in type with a special meaning, such as [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) and [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span></span> <span data-ttu-id="2e877-151">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="2e877-151">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="2e877-152">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="2e877-152">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="2e877-153">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="2e877-153">For example, the following action signatures cause an exception:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* <span data-ttu-id="2e877-154">**[FromForm]**，针对 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 类型的操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="2e877-154">**[FromForm]** is inferred for action parameters of type [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span></span> <span data-ttu-id="2e877-155">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="2e877-155">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="2e877-156">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="2e877-156">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="2e877-157">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="2e877-157">When multiple routes match an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="2e877-158">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="2e877-158">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="2e877-159">在 Startup.ConfigureServices 中使用以下代码将禁用默认推理规则：</span><span class="sxs-lookup"><span data-stu-id="2e877-159">The default inference rules are disabled with the following code in *Startup.ConfigureServices*:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="2e877-160">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="2e877-160">Multipart/form-data request inference</span></span>

<span data-ttu-id="2e877-161">使用 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="2e877-161">When an action parameter is annotated with the [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="2e877-162">在 Startup.ConfigureServices 中使用以下代码将禁用默认行为：</span><span class="sxs-lookup"><span data-stu-id="2e877-162">The default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a><span data-ttu-id="2e877-163">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="2e877-163">Attribute routing requirement</span></span>

<span data-ttu-id="2e877-164">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="2e877-164">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="2e877-165">例如:</span><span class="sxs-lookup"><span data-stu-id="2e877-165">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="2e877-166">不能通过在 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 访问操作。</span><span class="sxs-lookup"><span data-stu-id="2e877-166">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) or by [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) in *Startup.Configure*.</span></span>
::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="2e877-167">其他资源</span><span class="sxs-lookup"><span data-stu-id="2e877-167">Additional resources</span></span>

* [<span data-ttu-id="2e877-168">控制器操作返回类型</span><span class="sxs-lookup"><span data-stu-id="2e877-168">Controller action return types</span></span>](xref:web-api/action-return-types)
* [<span data-ttu-id="2e877-169">自定义格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e877-169">Custom formatters</span></span>](xref:web-api/advanced/custom-formatters)
* [<span data-ttu-id="2e877-170">格式化响应数据</span><span class="sxs-lookup"><span data-stu-id="2e877-170">Format response data</span></span>](xref:web-api/advanced/formatting)
* [<span data-ttu-id="2e877-171">使用 Swagger 的帮助页</span><span class="sxs-lookup"><span data-stu-id="2e877-171">Help pages using Swagger</span></span>](xref:tutorials/web-api-help-pages-using-swagger)
* [<span data-ttu-id="2e877-172">路由到控制器操作</span><span class="sxs-lookup"><span data-stu-id="2e877-172">Routing to controller actions</span></span>](xref:mvc/controllers/routing)
