---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: "属性 ASP.NET Web API 2 中的路由 |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 67ab1536b4a72abf8c0d3ed5aa0c48bc79a8fb5f
ms.sourcegitcommit: 3d512ea991ac36dfd4c800b7d1f8a27bfc50635e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
<a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="5bda8-102">ASP.NET Web API 2 中的属性路由</span><span class="sxs-lookup"><span data-stu-id="5bda8-102">Attribute Routing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="5bda8-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5bda8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5bda8-104">*路由*是 Web API 匹配的操作 URI 的方式。</span><span class="sxs-lookup"><span data-stu-id="5bda8-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="5bda8-105">Web API 2 支持一种新型的路由，调用*的属性路由*。</span><span class="sxs-lookup"><span data-stu-id="5bda8-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="5bda8-106">顾名思义的属性路由使用属性来定义路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="5bda8-107">属性路由可更好地控制 Uri 在你的 web API。</span><span class="sxs-lookup"><span data-stu-id="5bda8-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="5bda8-108">例如，你可以轻松创建描述资源的层次结构的 Uri。</span><span class="sxs-lookup"><span data-stu-id="5bda8-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="5bda8-109">早期样式的路由，调用基于约定的路由，仍完全支持。</span><span class="sxs-lookup"><span data-stu-id="5bda8-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="5bda8-110">事实上，你可以组合在同一项目的这两种技术。</span><span class="sxs-lookup"><span data-stu-id="5bda8-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="5bda8-111">本主题演示如何启用的属性路由，并描述了各种选项的属性路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="5bda8-112">使用的属性路由的端到端教程，请参阅[使用 Web API 2 中的属性路由创建 REST API](create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="5bda8-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5bda8-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="5bda8-113">Prerequisites</span></span>

<span data-ttu-id="5bda8-114">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community、 Professional 或 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="5bda8-114">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional, or Enterprise Edition</span></span>

<span data-ttu-id="5bda8-115">或者，使用 NuGet 包管理器安装所需的包。</span><span class="sxs-lookup"><span data-stu-id="5bda8-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="5bda8-116">从**工具**菜单在 Visual Studio 中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="5bda8-116">From the **Tools** menu in Visual Studio, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="5bda8-117">在 Package Manager Console 窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="5bda8-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="5bda8-118">为什么属性路由？</span><span class="sxs-lookup"><span data-stu-id="5bda8-118">Why Attribute Routing?</span></span>

<span data-ttu-id="5bda8-119">使用 Web API 的第一个版本*基于约定的*路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="5bda8-120">在该类型的路由，则定义一个或多个路由模板，它们基本上是参数化字符串。</span><span class="sxs-lookup"><span data-stu-id="5bda8-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="5bda8-121">当框架收到请求时，它可匹配与路由模板的 URI。</span><span class="sxs-lookup"><span data-stu-id="5bda8-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="5bda8-122">(有关基于约定的路由的详细信息，请参阅[路由在 ASP.NET Web API 中](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="5bda8-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="5bda8-123">基于约定的路由的优势之一是在同一个地方定义模板，并跨所有控制器一致地应用的路由规则。</span><span class="sxs-lookup"><span data-stu-id="5bda8-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="5bda8-124">遗憾的是，基于约定的路由使得很难支持某些常见的 RESTful Api 的 URI 模式。</span><span class="sxs-lookup"><span data-stu-id="5bda8-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="5bda8-125">例如，资源通常包含子资源： 客户下了订单、 电影具有 actors、 丛书具有作者，等等。</span><span class="sxs-lookup"><span data-stu-id="5bda8-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="5bda8-126">它为自然来创建反映这些关系的 Uri:</span><span class="sxs-lookup"><span data-stu-id="5bda8-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="5bda8-127">此类型的 URI 很难创建使用基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="5bda8-128">尽管它可以完成，结果不很好地，如果你有多个控制器或资源类型进行扩展。</span><span class="sxs-lookup"><span data-stu-id="5bda8-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="5bda8-129">属性路由，它很简单了此 uri 定义路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="5bda8-130">只需将特性添加到的控制器操作：</span><span class="sxs-lookup"><span data-stu-id="5bda8-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="5bda8-131">以下是一些其他的属性路由使简单的模式。</span><span class="sxs-lookup"><span data-stu-id="5bda8-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="5bda8-132">**API 版本控制**</span><span class="sxs-lookup"><span data-stu-id="5bda8-132">**API versioning**</span></span>

<span data-ttu-id="5bda8-133">在此示例中，"/ api/v1/产品"将路由到不同的控制器比"/ api/v2/产品"。</span><span class="sxs-lookup"><span data-stu-id="5bda8-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`  
`/api/v2/products`

<span data-ttu-id="5bda8-134">**重载的 URI 段**</span><span class="sxs-lookup"><span data-stu-id="5bda8-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="5bda8-135">在此示例中，"1"订单号，但是"挂起"映射到集合。</span><span class="sxs-lookup"><span data-stu-id="5bda8-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`  
`/orders/pending`

<span data-ttu-id="5bda8-136">**多个参数类型**</span><span class="sxs-lookup"><span data-stu-id="5bda8-136">**Multiple parameter types**</span></span>

<span data-ttu-id="5bda8-137">在此示例中，"1"订单号，但是"2013年/06/16"指定日期。</span><span class="sxs-lookup"><span data-stu-id="5bda8-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`  
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="5bda8-138">启用的属性路由</span><span class="sxs-lookup"><span data-stu-id="5bda8-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="5bda8-139">若要启用的属性路由，请调用**MapHttpAttributeRoutes**在配置期间。</span><span class="sxs-lookup"><span data-stu-id="5bda8-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="5bda8-140">此扩展方法定义中**System.Web.Http.HttpConfigurationExtensions**类。</span><span class="sxs-lookup"><span data-stu-id="5bda8-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="5bda8-141">属性路由可以与组合[基于约定的](routing-in-aspnet-web-api.md)路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="5bda8-142">若要定义基于约定的路由，调用**MapHttpRoute**方法。</span><span class="sxs-lookup"><span data-stu-id="5bda8-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="5bda8-143">有关配置 Web API 的详细信息，请参阅[配置 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="5bda8-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="5bda8-144">注意： 从 Web API 1 迁移</span><span class="sxs-lookup"><span data-stu-id="5bda8-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="5bda8-145">在 Web API 2 之前的 Web API 项目模板生成类似下面的代码：</span><span class="sxs-lookup"><span data-stu-id="5bda8-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="5bda8-146">如果启用了的属性路由，此代码将引发异常。</span><span class="sxs-lookup"><span data-stu-id="5bda8-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="5bda8-147">如果升级现有的 Web API 项目，以使用的属性路由，请确保更新此配置代码所示：</span><span class="sxs-lookup"><span data-stu-id="5bda8-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="5bda8-148">有关详细信息，请参阅[配置与 ASP.NET 承载的 Web API](../advanced/configuring-aspnet-web-api.md#webhost)。</span><span class="sxs-lookup"><span data-stu-id="5bda8-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="5bda8-149">添加路由属性</span><span class="sxs-lookup"><span data-stu-id="5bda8-149">Adding Route Attributes</span></span>

<span data-ttu-id="5bda8-150">下面是路由的使用特性定义的一个示例：</span><span class="sxs-lookup"><span data-stu-id="5bda8-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="5bda8-151">字符串&quot;客户 / {customerId} /orders&quot;是用于路由的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="5bda8-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="5bda8-152">Web API 尝试匹配对模板的请求 URI。</span><span class="sxs-lookup"><span data-stu-id="5bda8-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="5bda8-153">在此示例中，"客户"和"orders"文本段，并且在"{customerId}"是一个变量参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="5bda8-154">下面的 Uri 将匹配此模板：</span><span class="sxs-lookup"><span data-stu-id="5bda8-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="5bda8-155">你可以限制通过匹配[约束](#constraints)，本主题中后面所述。</span><span class="sxs-lookup"><span data-stu-id="5bda8-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="5bda8-156">请注意， &quot;{customerId}&quot;路由模板中的参数与匹配的名称*customerId*方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="5bda8-157">当 Web API 调用的控制器操作时，它将尝试将路由参数绑定。</span><span class="sxs-lookup"><span data-stu-id="5bda8-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="5bda8-158">例如，如果的 URI 是`http://example.com/customers/1/orders`，Web API 将尝试绑定值"1"到*customerId*操作中的参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="5bda8-159">URI 模板可以具有多个参数：</span><span class="sxs-lookup"><span data-stu-id="5bda8-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="5bda8-160">路由属性不具有任何控制器方法使用基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="5bda8-161">这样一来，你可以组合两种类型的同一项目中的路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5bda8-162">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5bda8-162">HTTP Methods</span></span>

<span data-ttu-id="5bda8-163">Web API 还将选择基于请求 （GET、 POST 等） 的 HTTP 方法的操作。</span><span class="sxs-lookup"><span data-stu-id="5bda8-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="5bda8-164">默认情况下，Web API 查找包含控制器方法名称的开头的不区分大小写的匹配项。</span><span class="sxs-lookup"><span data-stu-id="5bda8-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="5bda8-165">例如，一个名为的控制器方法`PutCustomers`匹配发出 HTTP PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="5bda8-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="5bda8-166">您可以重写此约定的修饰与任意方法的以下属性：</span><span class="sxs-lookup"><span data-stu-id="5bda8-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="5bda8-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="5bda8-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-168">**[HttpGet]**</span></span>
- <span data-ttu-id="5bda8-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-169">**[HttpHead]**</span></span>
- <span data-ttu-id="5bda8-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="5bda8-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="5bda8-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-172">**[HttpPost]**</span></span>
- <span data-ttu-id="5bda8-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="5bda8-173">**[HttpPut]**</span></span>

<span data-ttu-id="5bda8-174">下面的示例将 CreateBook 方法映射到 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="5bda8-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="5bda8-175">对于所有其他 HTTP 方法，包括非标准的方法，使用**AcceptVerbs**属性，它采用 HTTP 方法的列表。</span><span class="sxs-lookup"><span data-stu-id="5bda8-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="5bda8-176">路由前缀</span><span class="sxs-lookup"><span data-stu-id="5bda8-176">Route Prefixes</span></span>

<span data-ttu-id="5bda8-177">通常情况下，所有以相同的前缀开头的控制器中路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="5bda8-178">例如:</span><span class="sxs-lookup"><span data-stu-id="5bda8-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="5bda8-179">可以通过使用为整个控制器设置公共前缀**[RoutePrefix]**属性：</span><span class="sxs-lookup"><span data-stu-id="5bda8-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="5bda8-180">方法特性上使用波形符 （~） 来重写的路由前缀：</span><span class="sxs-lookup"><span data-stu-id="5bda8-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="5bda8-181">路由前缀可以包括参数：</span><span class="sxs-lookup"><span data-stu-id="5bda8-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="5bda8-182">路由约束</span><span class="sxs-lookup"><span data-stu-id="5bda8-182">Route Constraints</span></span>

<span data-ttu-id="5bda8-183">路由约束可让你限制如何匹配路由模板中的参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="5bda8-184">常规语法&quot;{参数： 约束}&quot;。</span><span class="sxs-lookup"><span data-stu-id="5bda8-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="5bda8-185">例如:</span><span class="sxs-lookup"><span data-stu-id="5bda8-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="5bda8-186">在这里，第一个路由将只能选择如果&quot;id&quot; URI 段是一个整数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="5bda8-187">否则，将选择第二个路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="5bda8-188">下表列出了受支持的约束。</span><span class="sxs-lookup"><span data-stu-id="5bda8-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="5bda8-189">约束</span><span class="sxs-lookup"><span data-stu-id="5bda8-189">Constraint</span></span> | <span data-ttu-id="5bda8-190">描述</span><span class="sxs-lookup"><span data-stu-id="5bda8-190">Description</span></span> | <span data-ttu-id="5bda8-191">示例</span><span class="sxs-lookup"><span data-stu-id="5bda8-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bda8-192">Alpha</span><span class="sxs-lookup"><span data-stu-id="5bda8-192">alpha</span></span> | <span data-ttu-id="5bda8-193">匹配大写或小写拉丁字母字符 (a-z、 A-Z)</span><span class="sxs-lookup"><span data-stu-id="5bda8-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="5bda8-194">{x： 字母}</span><span class="sxs-lookup"><span data-stu-id="5bda8-194">{x:alpha}</span></span> |
| <span data-ttu-id="5bda8-195">bool</span><span class="sxs-lookup"><span data-stu-id="5bda8-195">bool</span></span> | <span data-ttu-id="5bda8-196">匹配一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-196">Matches a Boolean value.</span></span> | <span data-ttu-id="5bda8-197">{x: bool}</span><span class="sxs-lookup"><span data-stu-id="5bda8-197">{x:bool}</span></span> |
| <span data-ttu-id="5bda8-198">datetime</span><span class="sxs-lookup"><span data-stu-id="5bda8-198">datetime</span></span> | <span data-ttu-id="5bda8-199">匹配**DateTime**值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="5bda8-200">{x: datetime}</span><span class="sxs-lookup"><span data-stu-id="5bda8-200">{x:datetime}</span></span> |
| <span data-ttu-id="5bda8-201">decimal</span><span class="sxs-lookup"><span data-stu-id="5bda8-201">decimal</span></span> | <span data-ttu-id="5bda8-202">匹配十进制值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-202">Matches a decimal value.</span></span> | <span data-ttu-id="5bda8-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="5bda8-203">{x:decimal}</span></span> |
| <span data-ttu-id="5bda8-204">double</span><span class="sxs-lookup"><span data-stu-id="5bda8-204">double</span></span> | <span data-ttu-id="5bda8-205">与 64 位浮点值匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="5bda8-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="5bda8-206">{x:double}</span></span> |
| <span data-ttu-id="5bda8-207">float</span><span class="sxs-lookup"><span data-stu-id="5bda8-207">float</span></span> | <span data-ttu-id="5bda8-208">匹配一个 32 位浮点值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="5bda8-209">{x: float}</span><span class="sxs-lookup"><span data-stu-id="5bda8-209">{x:float}</span></span> |
| <span data-ttu-id="5bda8-210">guid</span><span class="sxs-lookup"><span data-stu-id="5bda8-210">guid</span></span> | <span data-ttu-id="5bda8-211">匹配的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-211">Matches a GUID value.</span></span> | <span data-ttu-id="5bda8-212">{x: guid}</span><span class="sxs-lookup"><span data-stu-id="5bda8-212">{x:guid}</span></span> |
| <span data-ttu-id="5bda8-213">int</span><span class="sxs-lookup"><span data-stu-id="5bda8-213">int</span></span> | <span data-ttu-id="5bda8-214">匹配一个 32 位整数值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="5bda8-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="5bda8-215">{x:int}</span></span> |
| <span data-ttu-id="5bda8-216">length</span><span class="sxs-lookup"><span data-stu-id="5bda8-216">length</span></span> | <span data-ttu-id="5bda8-217">与具有指定长度或长度的指定的范围中的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="5bda8-218">{x:length(6)} {x:length(1,20)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="5bda8-219">long</span><span class="sxs-lookup"><span data-stu-id="5bda8-219">long</span></span> | <span data-ttu-id="5bda8-220">与 64 位整数值匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="5bda8-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="5bda8-221">{x:long}</span></span> |
| <span data-ttu-id="5bda8-222">max</span><span class="sxs-lookup"><span data-stu-id="5bda8-222">max</span></span> | <span data-ttu-id="5bda8-223">匹配一个整数，最大值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="5bda8-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-224">{x:max(10)}</span></span> |
| <span data-ttu-id="5bda8-225">maxlength</span><span class="sxs-lookup"><span data-stu-id="5bda8-225">maxlength</span></span> | <span data-ttu-id="5bda8-226">与最大长度的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="5bda8-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="5bda8-228">min</span><span class="sxs-lookup"><span data-stu-id="5bda8-228">min</span></span> | <span data-ttu-id="5bda8-229">匹配一个整数，最小值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="5bda8-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-230">{x:min(10)}</span></span> |
| <span data-ttu-id="5bda8-231">minlength</span><span class="sxs-lookup"><span data-stu-id="5bda8-231">minlength</span></span> | <span data-ttu-id="5bda8-232">与最小长度的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="5bda8-233">{x:minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="5bda8-234">range</span><span class="sxs-lookup"><span data-stu-id="5bda8-234">range</span></span> | <span data-ttu-id="5bda8-235">一个整数值的范围之内的匹配项。</span><span class="sxs-lookup"><span data-stu-id="5bda8-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="5bda8-236">{x:range(10,50)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="5bda8-237">正则表达式</span><span class="sxs-lookup"><span data-stu-id="5bda8-237">regex</span></span> | <span data-ttu-id="5bda8-238">与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="5bda8-238">Matches a regular expression.</span></span> | <span data-ttu-id="5bda8-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="5bda8-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="5bda8-240">请注意，某些约束，如&quot;min&quot;，在括号中采用自变量。</span><span class="sxs-lookup"><span data-stu-id="5bda8-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="5bda8-241">你可以将多个约束应用于由冒号分隔的参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="5bda8-242">自定义的路由约束</span><span class="sxs-lookup"><span data-stu-id="5bda8-242">Custom Route Constraints</span></span>

<span data-ttu-id="5bda8-243">你可以通过实现来创建自定义的路由约束**IHttpRouteConstraint**接口。</span><span class="sxs-lookup"><span data-stu-id="5bda8-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="5bda8-244">例如，以下限制将限制为非零整数值的参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="5bda8-245">下面的代码演示如何注册约束：</span><span class="sxs-lookup"><span data-stu-id="5bda8-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="5bda8-246">现在你可以将约束应用在你的路由中：</span><span class="sxs-lookup"><span data-stu-id="5bda8-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="5bda8-247">你也可以替换整个**DefaultInlineConstraintResolver**类通过实现**IInlineConstraintResolver**接口。</span><span class="sxs-lookup"><span data-stu-id="5bda8-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="5bda8-248">执行此操作将替换所有内置的约束，除非你实现**IInlineConstraintResolver**专门将它们添加。</span><span class="sxs-lookup"><span data-stu-id="5bda8-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="5bda8-249">可选 URI 参数和默认值</span><span class="sxs-lookup"><span data-stu-id="5bda8-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="5bda8-250">你可以通过将问号添加到路由参数来使 URI 参数可选。</span><span class="sxs-lookup"><span data-stu-id="5bda8-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="5bda8-251">如果路由参数是可选的则必须定义的方法参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="5bda8-252">在此示例中，`/api/books/locale/1033`和`/api/books/locale`返回相同的资源。</span><span class="sxs-lookup"><span data-stu-id="5bda8-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="5bda8-253">或者，可以指定在路由模板中，默认值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bda8-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="5bda8-254">这是前面的示例中，几乎相同，但没有行为的存在细微的差异时应用的默认值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="5bda8-255">在第一个示例 ("{lcid？}") 中，1033年的默认值是直接分配给方法参数，因此该参数将具有此确切值。</span><span class="sxs-lookup"><span data-stu-id="5bda8-255">In the first example ("{lcid?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="5bda8-256">在第二个示例 ("{lcid = 1033年}")，"1033"的默认值将经历模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="5bda8-256">In the second example ("{lcid=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="5bda8-257">默认模型联编程序将转换为数字值 1033年"1033"。</span><span class="sxs-lookup"><span data-stu-id="5bda8-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="5bda8-258">但是，您无法插入自定义模型联编程序，可能会执行的其他内容。</span><span class="sxs-lookup"><span data-stu-id="5bda8-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="5bda8-259">（在大多数情况下，除非你管道中有自定义模型联编程序的两种形式将为等效。）</span><span class="sxs-lookup"><span data-stu-id="5bda8-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="5bda8-260">路由名称</span><span class="sxs-lookup"><span data-stu-id="5bda8-260">Route Names</span></span>

<span data-ttu-id="5bda8-261">在 Web API 中，每个路线有一个名称。</span><span class="sxs-lookup"><span data-stu-id="5bda8-261">In Web API, every route has a name.</span></span> <span data-ttu-id="5bda8-262">路由名称可用于生成的链接，以便你可以在 HTTP 响应中包含一个链接。</span><span class="sxs-lookup"><span data-stu-id="5bda8-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="5bda8-263">若要指定路由名称，设置**名称**属性上的属性。</span><span class="sxs-lookup"><span data-stu-id="5bda8-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="5bda8-264">下面的示例演示如何设置路由名称，以及如何生成一个链接时使用路由名称。</span><span class="sxs-lookup"><span data-stu-id="5bda8-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="5bda8-265">路由顺序</span><span class="sxs-lookup"><span data-stu-id="5bda8-265">Route Order</span></span>

<span data-ttu-id="5bda8-266">当框架会尝试匹配与路由的 URI 时，它会评估按特定顺序的路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="5bda8-267">若要指定的顺序，将设置**RouteOrder**路由属性上的属性。</span><span class="sxs-lookup"><span data-stu-id="5bda8-267">To specify the order, set the **RouteOrder** property on the route attribute.</span></span> <span data-ttu-id="5bda8-268">较低的值都将先评估。</span><span class="sxs-lookup"><span data-stu-id="5bda8-268">Lower values are evaluated first.</span></span> <span data-ttu-id="5bda8-269">默认顺序值为零。</span><span class="sxs-lookup"><span data-stu-id="5bda8-269">The default order value is zero.</span></span>

<span data-ttu-id="5bda8-270">下面是如何确定总排序：</span><span class="sxs-lookup"><span data-stu-id="5bda8-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="5bda8-271">比较**RouteOrder**路由特性属性。</span><span class="sxs-lookup"><span data-stu-id="5bda8-271">Compare the **RouteOrder** property of the route attribute.</span></span>
2. <span data-ttu-id="5bda8-272">查看在路由模板中每个 URI 段。</span><span class="sxs-lookup"><span data-stu-id="5bda8-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="5bda8-273">对于每个段，排序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bda8-273">For each segment, order as follows:</span></span> 

    1. <span data-ttu-id="5bda8-274">文本段。</span><span class="sxs-lookup"><span data-stu-id="5bda8-274">Literal segments.</span></span>
    2. <span data-ttu-id="5bda8-275">具有约束的路由参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="5bda8-276">不受限制的路由参数。</span><span class="sxs-lookup"><span data-stu-id="5bda8-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="5bda8-277">具有约束的通配符参数段。</span><span class="sxs-lookup"><span data-stu-id="5bda8-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="5bda8-278">通配符参数不受限制的段。</span><span class="sxs-lookup"><span data-stu-id="5bda8-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="5bda8-279">对于一次，路由排序使用的不区分大小写的序号字符串比较 ([OrdinalIgnoreCase](https://msdn.microsoft.com/en-us/library/system.stringcomparer.ordinalignorecase.aspx)) 的路由模板。</span><span class="sxs-lookup"><span data-stu-id="5bda8-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/en-us/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="5bda8-280">这是一个示例。</span><span class="sxs-lookup"><span data-stu-id="5bda8-280">Here is an example.</span></span> <span data-ttu-id="5bda8-281">假设定义以下控制器：</span><span class="sxs-lookup"><span data-stu-id="5bda8-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="5bda8-282">这些路由进行排序，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5bda8-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="5bda8-283">orders/details</span><span class="sxs-lookup"><span data-stu-id="5bda8-283">orders/details</span></span>
2. <span data-ttu-id="5bda8-284">orders/{id}</span><span class="sxs-lookup"><span data-stu-id="5bda8-284">orders/{id}</span></span>
3. <span data-ttu-id="5bda8-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="5bda8-285">orders/{customerName}</span></span>
4. <span data-ttu-id="5bda8-286">orders/{\*date}</span><span class="sxs-lookup"><span data-stu-id="5bda8-286">orders/{\*date}</span></span>
5. <span data-ttu-id="5bda8-287">订单 / 挂起</span><span class="sxs-lookup"><span data-stu-id="5bda8-287">orders/pending</span></span>

<span data-ttu-id="5bda8-288">请注意，"详细信息"是文本段和出现之前"{id}"，但"挂起"显示上次因为**RouteOrder**属性为 1。</span><span class="sxs-lookup"><span data-stu-id="5bda8-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **RouteOrder** property is 1.</span></span> <span data-ttu-id="5bda8-289">(本示例假定那里没有客户名为"详细信息"或"挂起"。</span><span class="sxs-lookup"><span data-stu-id="5bda8-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="5bda8-290">通常情况下，尝试避免不明确的路由。</span><span class="sxs-lookup"><span data-stu-id="5bda8-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="5bda8-291">在此示例中，更好的路由模板`GetByCustomer`是"客户 / {customerName}")</span><span class="sxs-lookup"><span data-stu-id="5bda8-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
