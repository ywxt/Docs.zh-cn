---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API 中的异常处理 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 03/12/2012
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: 2db00c1ab241e0dad051c2a3bcd3b0e4bbf4d5c4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807656"
---
<a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="9ef4d-102">ASP.NET Web API 中的异常处理</span><span class="sxs-lookup"><span data-stu-id="9ef4d-102">Exception Handling in ASP.NET Web API</span></span>
====================
<span data-ttu-id="9ef4d-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9ef4d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9ef4d-104">本指南介绍了错误和异常处理 ASP.NET Web API 中。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="9ef4d-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="9ef4d-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="9ef4d-106">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="9ef4d-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="9ef4d-107">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="9ef4d-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="9ef4d-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="9ef4d-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="9ef4d-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="9ef4d-109">HttpResponseException</span></span>

<span data-ttu-id="9ef4d-110">如果 Web API 控制器引发未捕获的异常，则会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="9ef4d-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="9ef4d-111">默认情况下，大多数异常将转换为状态代码 500 内部服务器错误的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="9ef4d-112">**HttpResponseException**类型是一种特殊情况。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="9ef4d-113">此异常将返回异常构造函数中指定任何 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="9ef4d-114">例如，以下方法将返回 404，找不到，如果*id*参数无效。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="9ef4d-115">更好地响应的控制，还可以构造的整个响应消息，并将其与包含**HttpResponseException:**</span><span class="sxs-lookup"><span data-stu-id="9ef4d-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="9ef4d-116">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="9ef4d-116">Exception Filters</span></span>

<span data-ttu-id="9ef4d-117">您可以自定义 Web API 通过编写处理异常的方式*异常筛选器*。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="9ef4d-118">异常筛选器时，控制器方法引发任何未处理的异常时执行*不* **HttpResponseException**异常。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="9ef4d-119">**HttpResponseException**类型是一种特殊情况，因为它专为返回的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="9ef4d-120">异常筛选器实现**System.Web.Http.Filters.IExceptionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="9ef4d-121">编写异常筛选器的最简单方法是从派生**System.Web.Http.Filters.ExceptionFilterAttribute**类并重写**OnException**方法。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef4d-122">ASP.NET Web API 中的异常筛选器是 ASP.NET MVC 中类似的。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="9ef4d-123">但是，它们是在一个单独的命名空间和函数中单独声明。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="9ef4d-124">具体而言， **HandleErrorAttribute**在 MVC 中使用的类不处理由 Web API 控制器引发的异常。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>


<span data-ttu-id="9ef4d-125">下面是将转换的筛选器**NotImplementedException**异常转化为 HTTP 状态代码 501，未实现：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="9ef4d-126">**响应**的属性**HttpActionExecutedContext**对象包含将发送到客户端的 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="9ef4d-127">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="9ef4d-127">Registering Exception Filters</span></span>

<span data-ttu-id="9ef4d-128">有几种方法来注册 Web API 异常筛选器：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="9ef4d-129">由操作</span><span class="sxs-lookup"><span data-stu-id="9ef4d-129">By action</span></span>
- <span data-ttu-id="9ef4d-130">由控制器</span><span class="sxs-lookup"><span data-stu-id="9ef4d-130">By controller</span></span>
- <span data-ttu-id="9ef4d-131">全局</span><span class="sxs-lookup"><span data-stu-id="9ef4d-131">Globally</span></span>

<span data-ttu-id="9ef4d-132">筛选器应用到特定的操作，请将作为属性的筛选器添加到操作：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="9ef4d-133">筛选器应用到所有控制器上的操作，将筛选器作为属性添加到控制器类：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="9ef4d-134">若要对 Web API 的所有控制器全局应用筛选器，将添加到筛选器的实例**GlobalConfiguration.Configuration.Filters**集合。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="9ef4d-135">在此集合中的异常筛选器适用于任何 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-135">Exeption filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="9ef4d-136">如果使用"ASP.NET MVC 4 Web 应用程序"项目模板来创建你的项目，将 Web API 配置代码内的放`WebApiConfig`类，该类在应用程序位于\_开始文件夹：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="9ef4d-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="9ef4d-137">HttpError</span></span>

<span data-ttu-id="9ef4d-138">**HttpError**对象提供一致的方法来响应正文中返回的错误信息。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="9ef4d-139">下面的示例演示如何返回 HTTP 状态代码 404 （找不到） 与**HttpError**响应正文中。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="9ef4d-140">**CreateErrorResponse**中定义的扩展方法**System.Net.Http.HttpRequestMessageExtensions**类。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="9ef4d-141">在内部， **CreateErrorResponse**创建**HttpError**实例，然后创建**HttpResponseMessage** ，其中包含**HttpError**.</span><span class="sxs-lookup"><span data-stu-id="9ef4d-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="9ef4d-142">在此示例中，如果该方法成功，它将返回 HTTP 响应中的产品。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="9ef4d-143">但是，如果找不到请求的产品，包含 HTTP 响应**HttpError**请求正文中。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="9ef4d-144">响应可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="9ef4d-145">请注意， **HttpError**在此示例中，已将它们序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="9ef4d-146">使用的一个优点**HttpError**是转到通过同一[内容协商](../formats-and-model-binding/content-negotiation.md)和序列化处理任何其他强类型化模型。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="9ef4d-147">HttpError 和模型验证</span><span class="sxs-lookup"><span data-stu-id="9ef4d-147">HttpError and Model Validation</span></span>

<span data-ttu-id="9ef4d-148">可以为模型验证，请将传递到模型状态**CreateErrorResponse**，以在响应中包括的验证错误：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="9ef4d-149">此示例中可能会返回以下响应：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="9ef4d-150">有关模型验证的详细信息，请参阅[ASP.NET Web API 中的模型验证](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="9ef4d-151">使用 HttpResponseException HttpError</span><span class="sxs-lookup"><span data-stu-id="9ef4d-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="9ef4d-152">前面的示例返回**HttpResponseMessage**消息从控制器操作，但您还可以使用**HttpResponseException**返回**HttpError**。</span><span class="sxs-lookup"><span data-stu-id="9ef4d-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="9ef4d-153">这样就可以返回强类型化模型中正常成功的情况下，同时仍返回**HttpError**如果出现错误：</span><span class="sxs-lookup"><span data-stu-id="9ef4d-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
