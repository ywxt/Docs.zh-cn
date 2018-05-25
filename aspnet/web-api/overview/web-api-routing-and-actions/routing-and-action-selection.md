---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 路由和 ASP.NET Web API 中的操作选择 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2012
ms.topic: article
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 997582263bd48590b74434ee0ffc6be928fa1e08
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="bf1e9-102">路由和 ASP.NET Web API 中的操作选择</span><span class="sxs-lookup"><span data-stu-id="bf1e9-102">Routing and Action Selection in ASP.NET Web API</span></span>
====================
<span data-ttu-id="bf1e9-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bf1e9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bf1e9-104">本指南介绍了 ASP.NET Web API 将 HTTP 请求路由到在控制器上的特定操作的方式。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-105">有关路由的高级概述，请参阅[路由在 ASP.NET Web API 中](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>


<span data-ttu-id="bf1e9-106">本文探讨路由过程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="bf1e9-107">如果你创建的 Web API 项目，并且不会获得一些请求的查找路由按你期望的方式，希望本文将帮助。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="bf1e9-108">路由具有三个主要阶段：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="bf1e9-109">到路由模板对 URI 进行匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="bf1e9-110">选择一个控制器。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-110">Selecting a controller.</span></span>
3. <span data-ttu-id="bf1e9-111">选择操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-111">Selecting an action.</span></span>

<span data-ttu-id="bf1e9-112">可以使用你自己的自定义行为来替换该过程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="bf1e9-113">在本文中，我将介绍的默认行为。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="bf1e9-114">在结束时，我注意可以在其中自定义行为的位置。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="bf1e9-115">路由模板</span><span class="sxs-lookup"><span data-stu-id="bf1e9-115">Route Templates</span></span>

<span data-ttu-id="bf1e9-116">路由模板看起来类似于 URI 路径，但它可以具有占位符值，指示用大括号：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="bf1e9-117">当您创建一个路由时，你可以为某些或所有占位符提供默认值：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="bf1e9-118">你还可以提供约束，限制 URI 段匹配占位符的方式：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="bf1e9-119">框架会尝试匹配模板的 URI 路径段。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="bf1e9-120">在模板中的文本必须完全匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="bf1e9-121">一个占位符匹配任何值，除非指定约束。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="bf1e9-122">框架不匹配的 URI，如主机名或查询参数的其他部分。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="bf1e9-123">框架将选择的第一个路由的 URI 相匹配的路由表中。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="bf1e9-124">有两个特殊的占位符:"{controller}"和"{action}"。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="bf1e9-125">"{controller}"提供的控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="bf1e9-126">"{action}"提供的操作的名称。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="bf1e9-127">在 Web API 的常用的约定是省略"{action}"。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="bf1e9-128">默认值</span><span class="sxs-lookup"><span data-stu-id="bf1e9-128">Defaults</span></span>

<span data-ttu-id="bf1e9-129">如果你提供默认值，路由将与缺少这些段的 URI 匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="bf1e9-130">例如:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="bf1e9-131">URI"`http://localhost/api/products`"与此路由匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-131">The URI "`http://localhost/api/products`" matches this route.</span></span> <span data-ttu-id="bf1e9-132">"{类别}"段分配默认值"all"。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-132">The "{category}" segment is assigned the default value "all".</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="bf1e9-133">路由字典</span><span class="sxs-lookup"><span data-stu-id="bf1e9-133">Route Dictionary</span></span>

<span data-ttu-id="bf1e9-134">如果框架找到的匹配项的 uri，它将创建一个字典，其中对于每个占位符包含的值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="bf1e9-135">键是占位符名称，不包括大括号。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="bf1e9-136">值都作为从 URI 路径或默认值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="bf1e9-137">字典存储在**IHttpRouteData**对象。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="bf1e9-138">在此路由匹配的阶段，特殊"{controller}"和"{action}"占位符就像其他占位符一样对待。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="bf1e9-139">它们只存储在字典中，其他值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="bf1e9-140">默认值可以具有的特殊值**RouteParameter.Optional**。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="bf1e9-141">如果占位符获取分配此值的值不会添加到路由字典。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="bf1e9-142">例如:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="bf1e9-143">对于 URI 路径"api/products"中，将包含路由字典：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="bf1e9-144">控制器:"products"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-144">controller: "products"</span></span>
- <span data-ttu-id="bf1e9-145">类别:"全部"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-145">category: "all"</span></span>

<span data-ttu-id="bf1e9-146">对于"api/产品/toys/123"，但是，路由字典将包含：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="bf1e9-147">控制器:"products"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-147">controller: "products"</span></span>
- <span data-ttu-id="bf1e9-148">类别:"toys"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-148">category: "toys"</span></span>
- <span data-ttu-id="bf1e9-149">id:"123"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-149">id: "123"</span></span>

<span data-ttu-id="bf1e9-150">默认值还可以在路由模板中包含一个值，不会出现任何位置。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="bf1e9-151">如果路由与匹配，则会将该值存储在字典中。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="bf1e9-152">例如:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="bf1e9-153">如果该 URI 路径是"根/api/8"，字典将包含两个值：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="bf1e9-154">控制器:"客户"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-154">controller: "customers"</span></span>
- <span data-ttu-id="bf1e9-155">id: "8"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="bf1e9-156">选择一个控制器</span><span class="sxs-lookup"><span data-stu-id="bf1e9-156">Selecting a Controller</span></span>

<span data-ttu-id="bf1e9-157">控制器所选内容由**IHttpControllerSelector.SelectController**方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="bf1e9-158">此方法采用**HttpRequestMessage**实例并返回**HttpControllerDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="bf1e9-159">由提供的默认实现**DefaultHttpControllerSelector**类。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="bf1e9-160">此类使用简单的算法：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="bf1e9-161">在密钥"控制器"路由字典中查找。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="bf1e9-162">采用此键的值并将"控制器"获取控制器类型名称的字符串追加。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="bf1e9-163">查找具有此类型名称的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="bf1e9-164">例如，如果路由字典包含键 / 值对"控制器"="products"，则控制器类型是"ProductsController"。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="bf1e9-165">如果没有任何匹配的类型或多个匹配项，框架会将错误返回到客户端。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="bf1e9-166">步骤 3， **DefaultHttpControllerSelector**使用**IHttpControllerTypeResolver**接口来获取 Web API 控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="bf1e9-167">默认实现**IHttpControllerTypeResolver**返回 （a） 实现的所有公共类**IHttpController**，（b） 是不抽象，而 （c） 有以"Controller"结尾的名称。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="bf1e9-168">操作选择</span><span class="sxs-lookup"><span data-stu-id="bf1e9-168">Action Selection</span></span>

<span data-ttu-id="bf1e9-169">选择后控制器，则框架将选择该操作通过调用**IHttpActionSelector.SelectAction**方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="bf1e9-170">此方法采用**HttpControllerContext**并返回**HttpActionDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="bf1e9-171">由提供的默认实现**ApiControllerActionSelector**类。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="bf1e9-172">若要选择一项操作，它会查看以下：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="bf1e9-173">请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="bf1e9-174">在路由模板中，如果存在"{action}"占位符。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="bf1e9-175">在控制器上的操作的参数。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="bf1e9-176">之前查看选择算法，我们需要了解有关控制器操作的一些事项。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="bf1e9-177">**在控制器上的方法被认为"操作"？**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="bf1e9-178">当选择某个操作，框架仅查看公共实例方法在控制器上。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="bf1e9-179">此外，它不包括["特殊 name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)方法 （构造函数、 事件、 运算符重载等） 和从继承方法**ApiController**类。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="bf1e9-180">**HTTP 方法。**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-180">**HTTP Methods.**</span></span> <span data-ttu-id="bf1e9-181">框架仅选择匹配的请求，按以下方式确定的 HTTP 方法的操作：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="bf1e9-182">你可以使用属性中指定的 HTTP 方法： **AcceptVerbs**， **HttpDelete**， **HttpGet**， **HttpHead**， **HttpOptions**， **HttpPatch**， **HttpPost**，或**HttpPut**。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="bf1e9-183">否则，如果控制器方法的名称以"Get"、"Post"、"Put"、"删除"，"Head"、"选项"或"补丁日"开头，然后按照约定操作支持该 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="bf1e9-184">如果上述任何，该方法支持 POST。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="bf1e9-185">**参数绑定。**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-185">**Parameter Bindings.**</span></span> <span data-ttu-id="bf1e9-186">参数绑定是如何 Web API 创建参数的值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="bf1e9-187">下面是参数绑定的默认规则：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="bf1e9-188">从 URI 中获取简单类型。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="bf1e9-189">从请求正文中获取复杂类型。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="bf1e9-190">简单类型包括的所有[.NET Framework 基元类型](https://msdn.microsoft.com/library/system.type.isprimitive)，加上**DateTime**，**十进制**， **Guid**，**字符串**，和**TimeSpan**。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="bf1e9-191">对于每个操作，最多一个参数可以读取请求正文。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1e9-192">它是可以重写默认绑定规则。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="bf1e9-193">请参阅[WebAPI 参数绑定实质上的](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>


<span data-ttu-id="bf1e9-194">该背景，下面是操作选择算法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="bf1e9-195">匹配的 HTTP 请求方法在控制器上创建的所有操作的列表。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="bf1e9-196">如果路由字典具有的"操作"条目，删除其名称与此值不匹配的操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="bf1e9-197">尝试匹配到 URI 的操作参数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="bf1e9-198">对于每个操作，可以获取是一种简单类型，其中绑定的 URI 中获取的参数的参数的列表。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="bf1e9-199">排除可选参数。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="bf1e9-200">从此列表中，尝试路由字典中或在 URI 查询字符串中查找每个参数名称的匹配项。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="bf1e9-201">匹配项区分大小，并不依赖于参数顺序。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="bf1e9-202">选择列表中的每个参数的 URI 中具有匹配的其中一项操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="bf1e9-203">如果多该一个操作不符合这些标准，选取大多数的参数匹配的一个。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="bf1e9-204">忽略操作 **[NonAction]** 属性。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="bf1e9-205">步骤 #3 是可能最容易混淆。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="bf1e9-206">基本理念都是从 URI、 从请求正文中，或从自定义绑定，参数可以获取其值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="bf1e9-207">对于来自 URI 的参数，我们想要确保 URI 实际包含该参数，在 （通过路由字典） 的路径或查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="bf1e9-208">例如，考虑以下操作：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="bf1e9-209">*Id*参数绑定到的 URI。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="bf1e9-210">因此，此操作只能匹配一个 URI，包含"id"，路由字典中或查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="bf1e9-211">可选参数是一个例外，因为它们是可选。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="bf1e9-212">对于一个可选参数，它将是确定，如果绑定无法从 URI 中获得的值。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="bf1e9-213">复杂类型适用不同的原因的异常。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="bf1e9-214">通过自定义绑定的复杂类型只能绑定到的 URI。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="bf1e9-215">但在这种情况下，框架不能预先知道是否会将参数绑定到特定 URI。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="bf1e9-216">若要找出，它将需要调用绑定。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="bf1e9-217">选择算法的目的是从静态的说明，然后再调用任何绑定选择一项操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="bf1e9-218">因此，从匹配算法会排除复杂类型。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="bf1e9-219">选择操作后，会调用所有参数绑定。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="bf1e9-220">摘要:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-220">Summary:</span></span>

- <span data-ttu-id="bf1e9-221">Action 必须与匹配请求的 HTTP 的方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="bf1e9-222">如果存在，操作名称必须与匹配路由字典中的"操作"条目。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="bf1e9-223">对于操作的每个参数，如果参数则来自 URI，然后参数名称必须找路由字典中或在 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="bf1e9-224">（可选参数和复杂类型的参数被排除。）</span><span class="sxs-lookup"><span data-stu-id="bf1e9-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="bf1e9-225">尝试最大参数数量匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="bf1e9-226">最佳匹配可能是不带任何参数的方法。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="bf1e9-227">扩展的示例</span><span class="sxs-lookup"><span data-stu-id="bf1e9-227">Extended Example</span></span>

<span data-ttu-id="bf1e9-228">路由：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="bf1e9-229">控制器:</span><span class="sxs-lookup"><span data-stu-id="bf1e9-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="bf1e9-230">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="bf1e9-231">将路由匹配</span><span class="sxs-lookup"><span data-stu-id="bf1e9-231">Route Matching</span></span>

<span data-ttu-id="bf1e9-232">URI 匹配名为"DefaultApi"的路由。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="bf1e9-233">路由字典包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="bf1e9-234">控制器:"products"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-234">controller: "products"</span></span>
- <span data-ttu-id="bf1e9-235">id: "1"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-235">id: "1"</span></span>

<span data-ttu-id="bf1e9-236">路由字典不包含查询字符串参数、"版本"和"详细信息"，但这些仍会被视为期间操作选择。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="bf1e9-237">控制器所选内容</span><span class="sxs-lookup"><span data-stu-id="bf1e9-237">Controller Selection</span></span>

<span data-ttu-id="bf1e9-238">从路由字典中的"控制器"条目，该控制器类型是`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="bf1e9-239">操作选择</span><span class="sxs-lookup"><span data-stu-id="bf1e9-239">Action Selection</span></span>

<span data-ttu-id="bf1e9-240">HTTP 请求是 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="bf1e9-241">支持 GET 的控制器操作`GetAll`， `GetById`，和`FindProductsByName`。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="bf1e9-242">路由字典不包含"操作"的条目，因此我们无需与操作名称匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="bf1e9-243">接下来，我们尝试匹配的参数名称用于操作，只查看的 GET 操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="bf1e9-244">操作</span><span class="sxs-lookup"><span data-stu-id="bf1e9-244">Action</span></span> | <span data-ttu-id="bf1e9-245">到匹配项的参数</span><span class="sxs-lookup"><span data-stu-id="bf1e9-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="bf1e9-246">无</span><span class="sxs-lookup"><span data-stu-id="bf1e9-246">none</span></span> |
| `GetById` | <span data-ttu-id="bf1e9-247">"id"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="bf1e9-248">"name"</span><span class="sxs-lookup"><span data-stu-id="bf1e9-248">"name"</span></span> |

<span data-ttu-id="bf1e9-249">请注意，*版本*参数`GetById`不被视为，因为它是一个可选参数。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="bf1e9-250">`GetAll`方法完全匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="bf1e9-251">`GetById`方法也匹配项，因为路由字典包含"id"。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="bf1e9-252">`FindProductsByName`方法不匹配。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="bf1e9-253">`GetById`方法 wins，因为它与一个参数，而不是为指定参数匹配`GetAll`。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="bf1e9-254">使用以下参数值调用的方法：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="bf1e9-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="bf1e9-255">*id* = 1</span></span>
- <span data-ttu-id="bf1e9-256">*版本*= 1.5</span><span class="sxs-lookup"><span data-stu-id="bf1e9-256">*version* = 1.5</span></span>

<span data-ttu-id="bf1e9-257">请注意，即使*版本*不使用选择算法中参数的值来自 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="bf1e9-258">扩展点</span><span class="sxs-lookup"><span data-stu-id="bf1e9-258">Extension Points</span></span>

<span data-ttu-id="bf1e9-259">Web API 提供对路由过程的某些部分的扩展点。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="bf1e9-260">接口</span><span class="sxs-lookup"><span data-stu-id="bf1e9-260">Interface</span></span> | <span data-ttu-id="bf1e9-261">描述</span><span class="sxs-lookup"><span data-stu-id="bf1e9-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf1e9-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="bf1e9-263">选择控制器。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-263">Selects the controller.</span></span> |
| <span data-ttu-id="bf1e9-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="bf1e9-265">获取控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-265">Gets the list of controller types.</span></span> <span data-ttu-id="bf1e9-266">**DefaultHttpControllerSelector**从此列表中选择控制器类型。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="bf1e9-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="bf1e9-268">获取项目程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="bf1e9-269">**IHttpControllerTypeResolver**接口使用此列表以找到控制器的类型。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="bf1e9-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="bf1e9-271">创建新的控制器实例。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="bf1e9-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="bf1e9-273">选择的操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-273">Selects the action.</span></span> |
| <span data-ttu-id="bf1e9-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="bf1e9-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="bf1e9-275">将调用该操作。</span><span class="sxs-lookup"><span data-stu-id="bf1e9-275">Invokes the action.</span></span> |

<span data-ttu-id="bf1e9-276">若要为任何这些接口提供您自己的实现，请使用**服务**集合**HttpConfiguration**对象：</span><span class="sxs-lookup"><span data-stu-id="bf1e9-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
