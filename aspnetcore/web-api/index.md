---
title: 使用 ASP.NET Core 构建 Web API
author: scottaddie
description: 了解用于在 ASP.NET Core 中构建 Web API 的功能以及每项功能的适用场景。
ms.author: scaddie
ms.custom: mvc
ms.date: 07/06/2018
uid: web-api/index
ms.openlocfilehash: 84e4a51a8a8ab031752ef054cba834bd202a4927
ms.sourcegitcommit: ea7ec8d47f94cfb8e008d771f647f86bbb4baa44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2018
ms.locfileid: "37894210"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="46056-103">使用 ASP.NET Core 构建 Web API</span><span class="sxs-lookup"><span data-stu-id="46056-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="46056-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="46056-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="46056-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="46056-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="46056-106">本文档说明如何在 ASP.NET Core 中构建 Web API 以及每项功能的最佳适用场景。</span><span class="sxs-lookup"><span data-stu-id="46056-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="46056-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="46056-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="46056-108">从控制器（旨在用作 Web API）中的 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 类继承。</span><span class="sxs-lookup"><span data-stu-id="46056-108">Inherit from the [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="46056-109">例如:</span><span class="sxs-lookup"><span data-stu-id="46056-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

<span data-ttu-id="46056-110">通过 `ControllerBase` 类可使用一些属性和方法。</span><span class="sxs-lookup"><span data-stu-id="46056-110">The `ControllerBase` class provides access to several properties and methods.</span></span> <span data-ttu-id="46056-111">在前面的代码中，示例包含 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 和 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)。</span><span class="sxs-lookup"><span data-stu-id="46056-111">In the preceding code, examples include [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) and [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span></span> <span data-ttu-id="46056-112">将在操作方法中调用这些方法以分别返回 HTTP 400 和 201 状态代码。</span><span class="sxs-lookup"><span data-stu-id="46056-112">These methods are called within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="46056-113">将使用 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 属性（还可由 `ControllerBase` 提供）处理请求模型验证。</span><span class="sxs-lookup"><span data-stu-id="46056-113">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property, also provided by `ControllerBase`, is accessed to handle request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="46056-114">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="46056-114">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="46056-115">ASP.NET Core 2.1 引入了 [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) 特性，用于批注 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="46056-115">ASP.NET Core 2.1 introduces the [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="46056-116">例如:</span><span class="sxs-lookup"><span data-stu-id="46056-116">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="46056-117">需要兼容性版本 2.1 或更高版本（通过 [SetCompatibilityVersion](/dotnet/api/microsoft.extensions.dependencyinjection.mvccoremvcbuilderextensions.setcompatibilityversion) 设置）来使用此属性。</span><span class="sxs-lookup"><span data-stu-id="46056-117">A compatibility version of 2.1 or later, set via [SetCompatibilityVersion](/dotnet/api/microsoft.extensions.dependencyinjection.mvccoremvcbuilderextensions.setcompatibilityversion), is required to use this attribute.</span></span> <span data-ttu-id="46056-118">例如，Startup.ConfigureServices 中突出显示的代码设置了 2.1 兼容性标志：</span><span class="sxs-lookup"><span data-stu-id="46056-118">For example, the highlighted code in *Startup.ConfigureServices* sets the 2.1 compatibility flag:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

<span data-ttu-id="46056-119">`[ApiController]` 特性通常结合 `ControllerBase` 来为控制器启用特定于 REST 行为。</span><span class="sxs-lookup"><span data-stu-id="46056-119">The `[ApiController]` attribute is commonly coupled with `ControllerBase` to enable REST-specific behavior for controllers.</span></span> <span data-ttu-id="46056-120">通过 `ControllerBase` 可使用 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 和 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file) 等方法。</span><span class="sxs-lookup"><span data-stu-id="46056-120">`ControllerBase` provides access to methods such as [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) and [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span></span>

<span data-ttu-id="46056-121">另一种方法是创建使用 `[ApiController]` 特性进行批注的自定义基本控制器类：</span><span class="sxs-lookup"><span data-stu-id="46056-121">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="46056-122">以下各部分说明该特性添加的便利功能。</span><span class="sxs-lookup"><span data-stu-id="46056-122">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="46056-123">自动 HTTP 400 响应</span><span class="sxs-lookup"><span data-stu-id="46056-123">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="46056-124">验证错误会自动触发 HTTP 400 响应。</span><span class="sxs-lookup"><span data-stu-id="46056-124">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="46056-125">操作中不需要以下代码：</span><span class="sxs-lookup"><span data-stu-id="46056-125">The following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]

<span data-ttu-id="46056-126">当 [SuppressModelStateInvalidFilter](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressmodelstateinvalidfilter) 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="46056-126">The default behavior is disabled when the [SuppressModelStateInvalidFilter](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressmodelstateinvalidfilter) property is set to `true`.</span></span> <span data-ttu-id="46056-127">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="46056-127">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="46056-128">绑定源参数推理</span><span class="sxs-lookup"><span data-stu-id="46056-128">Binding source parameter inference</span></span>

<span data-ttu-id="46056-129">绑定源特性定义可找到操作参数值的位置。</span><span class="sxs-lookup"><span data-stu-id="46056-129">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="46056-130">存在以下绑定源特性：</span><span class="sxs-lookup"><span data-stu-id="46056-130">The following binding source attributes exist:</span></span>

|<span data-ttu-id="46056-131">特性</span><span class="sxs-lookup"><span data-stu-id="46056-131">Attribute</span></span>|<span data-ttu-id="46056-132">绑定源</span><span class="sxs-lookup"><span data-stu-id="46056-132">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="46056-133">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span><span class="sxs-lookup"><span data-stu-id="46056-133">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span></span>     | <span data-ttu-id="46056-134">请求正文</span><span class="sxs-lookup"><span data-stu-id="46056-134">Request body</span></span> |
|<span data-ttu-id="46056-135">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span><span class="sxs-lookup"><span data-stu-id="46056-135">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span></span>     | <span data-ttu-id="46056-136">请求正文中的表单数据</span><span class="sxs-lookup"><span data-stu-id="46056-136">Form data in the request body</span></span> |
|<span data-ttu-id="46056-137">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span><span class="sxs-lookup"><span data-stu-id="46056-137">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span></span> | <span data-ttu-id="46056-138">请求标头</span><span class="sxs-lookup"><span data-stu-id="46056-138">Request header</span></span> |
|<span data-ttu-id="46056-139">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span><span class="sxs-lookup"><span data-stu-id="46056-139">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span></span>   | <span data-ttu-id="46056-140">请求查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="46056-140">Request query string parameter</span></span> |
|<span data-ttu-id="46056-141">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span><span class="sxs-lookup"><span data-stu-id="46056-141">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span></span>   | <span data-ttu-id="46056-142">当前请求中的路由数据</span><span class="sxs-lookup"><span data-stu-id="46056-142">Route data from the current request</span></span> |
|<span data-ttu-id="46056-143">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="46056-143">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="46056-144">作为操作参数插入的请求服务</span><span class="sxs-lookup"><span data-stu-id="46056-144">The request service injected as an action parameter</span></span> |

> [!WARNING]
> <span data-ttu-id="46056-145">当值可能包含 `%2f`（即 `/`）时，请勿使用 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="46056-145">Don't use `[FromRoute]` when values might contain `%2f` (that is `/`).</span></span> <span data-ttu-id="46056-146">`%2f` 不会转换为 `/`（非转移形式）。</span><span class="sxs-lookup"><span data-stu-id="46056-146">`%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="46056-147">如果值可能包含 `%2f`，则使用 `[FromQuery]`。</span><span class="sxs-lookup"><span data-stu-id="46056-147">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="46056-148">没有 `[ApiController]` 特性时，将显式定义绑定源特性。</span><span class="sxs-lookup"><span data-stu-id="46056-148">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="46056-149">在下面的示例中，`[FromQuery]` 特性指示 `discontinuedOnly` 参数值在请求 URL 的查询字符串中提供：</span><span class="sxs-lookup"><span data-stu-id="46056-149">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]

<span data-ttu-id="46056-150">推理规则应用于操作参数的默认数据源。</span><span class="sxs-lookup"><span data-stu-id="46056-150">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="46056-151">这些规则将配置绑定资源，否则你可以手动应用操作参数。</span><span class="sxs-lookup"><span data-stu-id="46056-151">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="46056-152">绑定源特性的行为如下：</span><span class="sxs-lookup"><span data-stu-id="46056-152">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="46056-153">**[FromBody]**，针对复杂类型参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="46056-153">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="46056-154">此规则不适用于具有特殊含义的任何复杂的内置类型，如 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 和 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)。</span><span class="sxs-lookup"><span data-stu-id="46056-154">An exception to this rule is any complex, built-in type with a special meaning, such as [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) and [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span></span> <span data-ttu-id="46056-155">绑定源推理代码将忽略这些特殊类型。</span><span class="sxs-lookup"><span data-stu-id="46056-155">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="46056-156">当操作中的多个参数为显式指定（通过 `[FromBody]`）或在请求正文中作为绑定进行推断时，将会引发异常。</span><span class="sxs-lookup"><span data-stu-id="46056-156">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="46056-157">例如，下面的操作签名会导致异常：</span><span class="sxs-lookup"><span data-stu-id="46056-157">For example, the following action signatures cause an exception:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* <span data-ttu-id="46056-158">**[FromForm]**，针对 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 和 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 类型的操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="46056-158">**[FromForm]** is inferred for action parameters of type [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span></span> <span data-ttu-id="46056-159">该特性不针对任何简单类型或用户定义类型进行推断。</span><span class="sxs-lookup"><span data-stu-id="46056-159">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="46056-160">**[FromRoute]**，针对与路由模板中的参数相匹配的任何操作参数名称进行推断。</span><span class="sxs-lookup"><span data-stu-id="46056-160">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="46056-161">当多个路由与一个操作参数匹配时，任何路由值都视为 `[FromRoute]`。</span><span class="sxs-lookup"><span data-stu-id="46056-161">When more than one route matches an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="46056-162">**[FromQuery]**，针对任何其他操作参数进行推断。</span><span class="sxs-lookup"><span data-stu-id="46056-162">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="46056-163">当 [SuppressInferBindingSourcesForParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressinferbindingsourcesforparameters) 属性设为 `true` 时，会禁用默认推理规则。</span><span class="sxs-lookup"><span data-stu-id="46056-163">The default inference rules are disabled when the [SuppressInferBindingSourcesForParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressinferbindingsourcesforparameters) property is set to `true`.</span></span> <span data-ttu-id="46056-164">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="46056-164">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="46056-165">Multipart/form-data 请求推理</span><span class="sxs-lookup"><span data-stu-id="46056-165">Multipart/form-data request inference</span></span>

<span data-ttu-id="46056-166">使用 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 特性批注操作参数时，将推断 `multipart/form-data` 请求内容类型。</span><span class="sxs-lookup"><span data-stu-id="46056-166">When an action parameter is annotated with the [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="46056-167">当 [SuppressConsumesConstraintForFormFileParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressconsumesconstraintforformfileparameters) 属性设置为 `true` 时，会禁用默认行为。</span><span class="sxs-lookup"><span data-stu-id="46056-167">The default behavior is disabled when the [SuppressConsumesConstraintForFormFileParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressconsumesconstraintforformfileparameters) property is set to `true`.</span></span> <span data-ttu-id="46056-168">将以下代码添加至 Startup.ConfigureServices 中的 `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 后：</span><span class="sxs-lookup"><span data-stu-id="46056-168">Add the following code in *Startup.ConfigureServices* after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a><span data-ttu-id="46056-169">特性路由要求</span><span class="sxs-lookup"><span data-stu-id="46056-169">Attribute routing requirement</span></span>

<span data-ttu-id="46056-170">特性路由是必要条件。</span><span class="sxs-lookup"><span data-stu-id="46056-170">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="46056-171">例如:</span><span class="sxs-lookup"><span data-stu-id="46056-171">For example:</span></span>

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="46056-172">不能通过在 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) 中定义的 [传统路由](xref:mvc/controllers/routing#conventional-routing)或通过 Startup.Configure 中的 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 访问操作。</span><span class="sxs-lookup"><span data-stu-id="46056-172">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) or by [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) in *Startup.Configure*.</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="46056-173">其他资源</span><span class="sxs-lookup"><span data-stu-id="46056-173">Additional resources</span></span>

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
