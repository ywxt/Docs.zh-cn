---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API 中的异常处理 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2012
ms.topic: article
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: c65ddcca012840d70ab5a33af92edb30041be971
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506956"
---
<a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="54b62-102">ASP.NET Web API 中的异常处理</span><span class="sxs-lookup"><span data-stu-id="54b62-102">Exception Handling in ASP.NET Web API</span></span>
====================
<span data-ttu-id="54b62-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="54b62-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="54b62-104">本指南介绍了错误和异常处理在 ASP.NET Web API 中。</span><span class="sxs-lookup"><span data-stu-id="54b62-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="54b62-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="54b62-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="54b62-106">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="54b62-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="54b62-107">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="54b62-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="54b62-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="54b62-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="54b62-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="54b62-109">HttpResponseException</span></span>

<span data-ttu-id="54b62-110">如果 Web API 控制器引发未捕获的异常，则会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="54b62-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="54b62-111">默认情况下，大多数异常被转换为状态代码 500 内部服务器错误的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="54b62-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="54b62-112">**HttpResponseException**类型是一种特殊情况。</span><span class="sxs-lookup"><span data-stu-id="54b62-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="54b62-113">此异常返回异常构造函数中指定任何 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="54b62-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="54b62-114">例如，以下方法将返回 404，找不到，如果*id*参数无效。</span><span class="sxs-lookup"><span data-stu-id="54b62-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="54b62-115">更灵活地控制响应，还可以构造的整个响应消息，并将其与包含**HttpResponseException:**</span><span class="sxs-lookup"><span data-stu-id="54b62-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="54b62-116">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="54b62-116">Exception Filters</span></span>

<span data-ttu-id="54b62-117">你可以自定义 Web API 通过编写处理异常的方式*异常筛选器*。</span><span class="sxs-lookup"><span data-stu-id="54b62-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="54b62-118">异常筛选器时的控制器方法引发任何未处理的异常时执行*不* **HttpResponseException**异常。</span><span class="sxs-lookup"><span data-stu-id="54b62-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="54b62-119">**HttpResponseException**类型是一种特殊情况，因为它专为返回 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="54b62-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="54b62-120">异常筛选器实现**System.Web.Http.Filters.IExceptionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="54b62-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="54b62-121">编写异常筛选器的最简单方法是为派生自**System.Web.Http.Filters.ExceptionFilterAttribute**类并重写**OnException**方法。</span><span class="sxs-lookup"><span data-stu-id="54b62-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="54b62-122">ASP.NET Web API 中的异常筛选器是 ASP.NET MVC 相似。</span><span class="sxs-lookup"><span data-stu-id="54b62-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="54b62-123">但是，声明它们在一个单独的命名空间和函数分开。</span><span class="sxs-lookup"><span data-stu-id="54b62-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="54b62-124">具体而言， **HandleErrorAttribute**在 MVC 中使用的类并不处理由 Web API 控制器引发的异常。</span><span class="sxs-lookup"><span data-stu-id="54b62-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>


<span data-ttu-id="54b62-125">下面是将转换的筛选器**NotImplementedException**异常 HTTP 状态代码 501，未实现：</span><span class="sxs-lookup"><span data-stu-id="54b62-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="54b62-126">**响应**属性**HttpActionExecutedContext**对象包含将发送到客户端的 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="54b62-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="54b62-127">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="54b62-127">Registering Exception Filters</span></span>

<span data-ttu-id="54b62-128">有多种，注册 Web API 异常筛选器：</span><span class="sxs-lookup"><span data-stu-id="54b62-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="54b62-129">由操作</span><span class="sxs-lookup"><span data-stu-id="54b62-129">By action</span></span>
- <span data-ttu-id="54b62-130">由控制器</span><span class="sxs-lookup"><span data-stu-id="54b62-130">By controller</span></span>
- <span data-ttu-id="54b62-131">全局</span><span class="sxs-lookup"><span data-stu-id="54b62-131">Globally</span></span>

<span data-ttu-id="54b62-132">若要将筛选器应用到特定的操作，请将作为属性的筛选器添加到操作：</span><span class="sxs-lookup"><span data-stu-id="54b62-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="54b62-133">将筛选器应用于所有在控制器上的操作，请将作为属性的筛选器添加到控制器类：</span><span class="sxs-lookup"><span data-stu-id="54b62-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="54b62-134">若要将筛选器全局应用于所有的 Web API 控制器，将添加到筛选器的实例**GlobalConfiguration.Configuration.Filters**集合。</span><span class="sxs-lookup"><span data-stu-id="54b62-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="54b62-135">在此集合中的异常筛选器适用于任何 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="54b62-135">Exeption filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="54b62-136">如果你使用"ASP.NET MVC 4 Web 应用程序"项目模板创建你的项目，将 Web API 配置代码内的放置`WebApiConfig`类，该类在应用程序位于\_开始文件夹：</span><span class="sxs-lookup"><span data-stu-id="54b62-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="54b62-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="54b62-137">HttpError</span></span>

<span data-ttu-id="54b62-138">**HttpError**对象提供一致的方法来响应正文中返回错误信息。</span><span class="sxs-lookup"><span data-stu-id="54b62-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="54b62-139">下面的示例演示如何返回 HTTP 状态代码 404 （未找到） 与**HttpError**响应正文中。</span><span class="sxs-lookup"><span data-stu-id="54b62-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="54b62-140">**CreateErrorResponse**中定义的扩展方法**System.Net.Http.HttpRequestMessageExtensions**类。</span><span class="sxs-lookup"><span data-stu-id="54b62-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="54b62-141">在内部， **CreateErrorResponse**创建**HttpError**实例，然后创建**HttpResponseMessage**包含**HttpError**.</span><span class="sxs-lookup"><span data-stu-id="54b62-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="54b62-142">在此示例中，如果此方法成功，它将返回 HTTP 响应中的产品。</span><span class="sxs-lookup"><span data-stu-id="54b62-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="54b62-143">但是，如果未找到请求的产品，包含 HTTP 响应**HttpError**请求正文中。</span><span class="sxs-lookup"><span data-stu-id="54b62-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="54b62-144">响应可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="54b62-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="54b62-145">请注意， **HttpError**在此示例中，已将它们序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="54b62-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="54b62-146">使用的一个优点**HttpError**是它将经历相同[内容协商](../formats-and-model-binding/content-negotiation.md)和序列化处理任何其他强类型的模型。</span><span class="sxs-lookup"><span data-stu-id="54b62-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="54b62-147">HttpError 和模型验证</span><span class="sxs-lookup"><span data-stu-id="54b62-147">HttpError and Model Validation</span></span>

<span data-ttu-id="54b62-148">对于模型的验证，你可以将传递到在模型状态**CreateErrorResponse**，若要在响应中包含的验证错误：</span><span class="sxs-lookup"><span data-stu-id="54b62-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="54b62-149">此示例可能会返回以下响应：</span><span class="sxs-lookup"><span data-stu-id="54b62-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="54b62-150">有关模型验证的详细信息，请参阅[ASP.NET Web API 中的模型验证](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="54b62-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="54b62-151">使用 HttpResponseException HttpError</span><span class="sxs-lookup"><span data-stu-id="54b62-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="54b62-152">前面的示例返回**HttpResponseMessage**消息从控制器操作，但你还可以使用**HttpResponseException**返回**HttpError**。</span><span class="sxs-lookup"><span data-stu-id="54b62-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="54b62-153">这样就可以时仍返回在正常成功情况下，返回强类型模型**HttpError**如果错误：</span><span class="sxs-lookup"><span data-stu-id="54b62-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
