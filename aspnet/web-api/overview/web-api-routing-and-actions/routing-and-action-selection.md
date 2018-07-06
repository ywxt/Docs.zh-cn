---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 路由和 ASP.NET Web API 中的操作选择 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/27/2012
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 2421d3dd134e9188faf6933b076fb9d22a119617
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832825"
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="31c4a-102">路由和 ASP.NET Web API 中的操作选择</span><span class="sxs-lookup"><span data-stu-id="31c4a-102">Routing and Action Selection in ASP.NET Web API</span></span>
====================
<span data-ttu-id="31c4a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="31c4a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="31c4a-104">本指南介绍了 ASP.NET Web API 将 HTTP 请求路由到控制器上的特定操作的方式。</span><span class="sxs-lookup"><span data-stu-id="31c4a-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="31c4a-105">有关路由的高级别概述，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="31c4a-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>


<span data-ttu-id="31c4a-106">本文探讨路由过程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="31c4a-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="31c4a-107">如果你创建 Web API 项目，别让我打开某些请求的查找路由按你期望的方式，希望这篇文章将帮助。</span><span class="sxs-lookup"><span data-stu-id="31c4a-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="31c4a-108">路由具有三个主要阶段：</span><span class="sxs-lookup"><span data-stu-id="31c4a-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="31c4a-109">匹配的路由模板的 URI。</span><span class="sxs-lookup"><span data-stu-id="31c4a-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="31c4a-110">选择一个控制器。</span><span class="sxs-lookup"><span data-stu-id="31c4a-110">Selecting a controller.</span></span>
3. <span data-ttu-id="31c4a-111">选择一个操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-111">Selecting an action.</span></span>

<span data-ttu-id="31c4a-112">可以使用你自己的自定义行为来替换该过程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="31c4a-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="31c4a-113">在本文中，我介绍的默认行为。</span><span class="sxs-lookup"><span data-stu-id="31c4a-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="31c4a-114">在结束时，我注意到在其中自定义行为的位置。</span><span class="sxs-lookup"><span data-stu-id="31c4a-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="31c4a-115">路由模板</span><span class="sxs-lookup"><span data-stu-id="31c4a-115">Route Templates</span></span>

<span data-ttu-id="31c4a-116">路由模板看起来类似于一个 URI 的路径，但它可以具有占位符值，指示用大括号：</span><span class="sxs-lookup"><span data-stu-id="31c4a-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="31c4a-117">当您创建一个路由时，您可以为某些或所有占位符提供默认值：</span><span class="sxs-lookup"><span data-stu-id="31c4a-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="31c4a-118">此外可以提供约束，限制 URI 段匹配占位符的方式：</span><span class="sxs-lookup"><span data-stu-id="31c4a-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="31c4a-119">该框架会尝试匹配中模板的 URI 路径段。</span><span class="sxs-lookup"><span data-stu-id="31c4a-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="31c4a-120">在模板中的文本必须完全匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="31c4a-121">一个占位符匹配任何值，除非指定约束。</span><span class="sxs-lookup"><span data-stu-id="31c4a-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="31c4a-122">框架不匹配的 URI，例如主机名或查询参数的其他部分。</span><span class="sxs-lookup"><span data-stu-id="31c4a-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="31c4a-123">框架将与 URI 匹配的路由表中选择第一个路由。</span><span class="sxs-lookup"><span data-stu-id="31c4a-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="31c4a-124">有两个特殊的占位符:"{controller}"和"{action}"。</span><span class="sxs-lookup"><span data-stu-id="31c4a-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="31c4a-125">"{controller}"提供的控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="31c4a-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="31c4a-126">"{action}"提供的操作的名称。</span><span class="sxs-lookup"><span data-stu-id="31c4a-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="31c4a-127">在 Web API 中，常规约定，是忽略"{action}"。</span><span class="sxs-lookup"><span data-stu-id="31c4a-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="31c4a-128">默认值</span><span class="sxs-lookup"><span data-stu-id="31c4a-128">Defaults</span></span>

<span data-ttu-id="31c4a-129">如果提供的默认值，该路由将匹配缺少这些段的 URI。</span><span class="sxs-lookup"><span data-stu-id="31c4a-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="31c4a-130">例如：</span><span class="sxs-lookup"><span data-stu-id="31c4a-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="31c4a-131">URI"`http://localhost/api/products`"与此路由匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-131">The URI "`http://localhost/api/products`" matches this route.</span></span> <span data-ttu-id="31c4a-132">"{Category}"段分配默认值"all"。</span><span class="sxs-lookup"><span data-stu-id="31c4a-132">The "{category}" segment is assigned the default value "all".</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="31c4a-133">路由字典</span><span class="sxs-lookup"><span data-stu-id="31c4a-133">Route Dictionary</span></span>

<span data-ttu-id="31c4a-134">如果框架找到一个 URI 的匹配项，则会创建一个字典，其中包含每个占位符的值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="31c4a-135">键是占位符名称，不包括大括号。</span><span class="sxs-lookup"><span data-stu-id="31c4a-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="31c4a-136">值会从 URI 路径或默认值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="31c4a-137">字典存储在**IHttpRouteData**对象。</span><span class="sxs-lookup"><span data-stu-id="31c4a-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="31c4a-138">在路由匹配此阶段中，特殊"{controller}"和"{action}"占位符就像其他占位符一样处理。</span><span class="sxs-lookup"><span data-stu-id="31c4a-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="31c4a-139">它们只存储在字典中，其他值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="31c4a-140">默认值可以具有特殊值**RouteParameter.Optional**。</span><span class="sxs-lookup"><span data-stu-id="31c4a-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="31c4a-141">如果占位符获取分配此值，该值是不会添加到路由字典中。</span><span class="sxs-lookup"><span data-stu-id="31c4a-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="31c4a-142">例如：</span><span class="sxs-lookup"><span data-stu-id="31c4a-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="31c4a-143">URI 路径的"api/产品"中，将包含路由字典：</span><span class="sxs-lookup"><span data-stu-id="31c4a-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="31c4a-144">控制器:"产品"</span><span class="sxs-lookup"><span data-stu-id="31c4a-144">controller: "products"</span></span>
- <span data-ttu-id="31c4a-145">类别:"all"</span><span class="sxs-lookup"><span data-stu-id="31c4a-145">category: "all"</span></span>

<span data-ttu-id="31c4a-146">对于"api/产品/toys/123"，但是，路由字典将包含：</span><span class="sxs-lookup"><span data-stu-id="31c4a-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="31c4a-147">控制器:"产品"</span><span class="sxs-lookup"><span data-stu-id="31c4a-147">controller: "products"</span></span>
- <span data-ttu-id="31c4a-148">类别:"toys"</span><span class="sxs-lookup"><span data-stu-id="31c4a-148">category: "toys"</span></span>
- <span data-ttu-id="31c4a-149">id:"123"</span><span class="sxs-lookup"><span data-stu-id="31c4a-149">id: "123"</span></span>

<span data-ttu-id="31c4a-150">默认值还可以在路由模板中包含一个值，未显示任何位置。</span><span class="sxs-lookup"><span data-stu-id="31c4a-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="31c4a-151">如果路由与匹配，此值存储在字典中。</span><span class="sxs-lookup"><span data-stu-id="31c4a-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="31c4a-152">例如：</span><span class="sxs-lookup"><span data-stu-id="31c4a-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="31c4a-153">如果 URI 路径为"根/api/8"，该字典将包含两个值：</span><span class="sxs-lookup"><span data-stu-id="31c4a-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="31c4a-154">控制器:"客户"</span><span class="sxs-lookup"><span data-stu-id="31c4a-154">controller: "customers"</span></span>
- <span data-ttu-id="31c4a-155">id:"8"</span><span class="sxs-lookup"><span data-stu-id="31c4a-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="31c4a-156">选择控制器</span><span class="sxs-lookup"><span data-stu-id="31c4a-156">Selecting a Controller</span></span>

<span data-ttu-id="31c4a-157">控制器选择处理通过**IHttpControllerSelector.SelectController**方法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="31c4a-158">此方法采用**HttpRequestMessage**实例，并返回**HttpControllerDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="31c4a-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="31c4a-159">提供的默认实现**DefaultHttpControllerSelector**类。</span><span class="sxs-lookup"><span data-stu-id="31c4a-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="31c4a-160">此类使用简单算法：</span><span class="sxs-lookup"><span data-stu-id="31c4a-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="31c4a-161">在"控制器"的键的路由字典中查找。</span><span class="sxs-lookup"><span data-stu-id="31c4a-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="31c4a-162">此密钥的值和追加"Controller"来获取控制器的类型名称的字符串。</span><span class="sxs-lookup"><span data-stu-id="31c4a-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="31c4a-163">查找具有此类型名称的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="31c4a-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="31c4a-164">例如，如果路由字典包含键 / 值对"controller"="产品"，则控制器类型是"ProductsController"。</span><span class="sxs-lookup"><span data-stu-id="31c4a-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="31c4a-165">如果没有匹配的类型或多个匹配项，框架将返回到客户端错误。</span><span class="sxs-lookup"><span data-stu-id="31c4a-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="31c4a-166">步骤 3 中，对于**DefaultHttpControllerSelector**使用**IHttpControllerTypeResolver**接口，用于获取 Web API 控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="31c4a-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="31c4a-167">默认实现**IHttpControllerTypeResolver**返回的所有公共类 （a） 实现**IHttpController**，（b） 是不抽象，和 （c） 具有以"Controller"结尾的名称。</span><span class="sxs-lookup"><span data-stu-id="31c4a-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="31c4a-168">操作选择</span><span class="sxs-lookup"><span data-stu-id="31c4a-168">Action Selection</span></span>

<span data-ttu-id="31c4a-169">后选择的控制器，则框架将选择该操作通过调用**IHttpActionSelector.SelectAction**方法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="31c4a-170">此方法采用**HttpControllerContext** ，并返回**HttpActionDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="31c4a-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="31c4a-171">提供的默认实现**ApiControllerActionSelector**类。</span><span class="sxs-lookup"><span data-stu-id="31c4a-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="31c4a-172">若要选择一项操作，它会查看以下：</span><span class="sxs-lookup"><span data-stu-id="31c4a-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="31c4a-173">请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="31c4a-174">在路由模板中，如果存在"{action}"占位符。</span><span class="sxs-lookup"><span data-stu-id="31c4a-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="31c4a-175">在控制器上的操作的参数。</span><span class="sxs-lookup"><span data-stu-id="31c4a-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="31c4a-176">在查看选择算法时之前, 需要了解关于控制器操作的一些内容。</span><span class="sxs-lookup"><span data-stu-id="31c4a-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="31c4a-177">**在控制器上的方法被认为是"操作"？**</span><span class="sxs-lookup"><span data-stu-id="31c4a-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="31c4a-178">当选择一个操作，框架仅查看公共实例方法的控制器上。</span><span class="sxs-lookup"><span data-stu-id="31c4a-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="31c4a-179">此外，它不包括["特殊名称"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) （构造函数、 事件、 运算符重载等） 的方法和方法继承自**ApiController**类。</span><span class="sxs-lookup"><span data-stu-id="31c4a-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="31c4a-180">**HTTP 方法。**</span><span class="sxs-lookup"><span data-stu-id="31c4a-180">**HTTP Methods.**</span></span> <span data-ttu-id="31c4a-181">框架仅选择匹配的请求，确定，如下所示的 HTTP 方法的操作：</span><span class="sxs-lookup"><span data-stu-id="31c4a-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="31c4a-182">可以使用属性指定的 HTTP 方法： **AcceptVerbs**， **HttpDelete**， **HttpGet**， **HttpHead**， **HttpOptions**， **HttpPatch**， **HttpPost**，或**HttpPut**。</span><span class="sxs-lookup"><span data-stu-id="31c4a-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="31c4a-183">否则，如果控制器方法的名称以"Get"、"Post"、"Put"、"删除"、"Head"、"选项"或"修补"开头，然后按照约定操作支持的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="31c4a-184">如果上述任何订阅，该方法支持 POST。</span><span class="sxs-lookup"><span data-stu-id="31c4a-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="31c4a-185">**参数绑定。**</span><span class="sxs-lookup"><span data-stu-id="31c4a-185">**Parameter Bindings.**</span></span> <span data-ttu-id="31c4a-186">参数绑定是如何将 Web API 创建某个参数的值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="31c4a-187">下面是参数绑定的默认规则：</span><span class="sxs-lookup"><span data-stu-id="31c4a-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="31c4a-188">从 URI 中获取简单类型。</span><span class="sxs-lookup"><span data-stu-id="31c4a-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="31c4a-189">从请求正文中获取复杂类型。</span><span class="sxs-lookup"><span data-stu-id="31c4a-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="31c4a-190">简单类型包含的所有[.NET Framework 基元类型](https://msdn.microsoft.com/library/system.type.isprimitive)，加上**DateTime**，**十进制**， **Guid**，**字符串**，并**TimeSpan**。</span><span class="sxs-lookup"><span data-stu-id="31c4a-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="31c4a-191">对于每个操作，最多一个参数可以读取请求正文。</span><span class="sxs-lookup"><span data-stu-id="31c4a-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="31c4a-192">它是可以重写默认绑定规则。</span><span class="sxs-lookup"><span data-stu-id="31c4a-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="31c4a-193">请参阅[WebAPI 参数绑定实质上](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)。</span><span class="sxs-lookup"><span data-stu-id="31c4a-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>


<span data-ttu-id="31c4a-194">这种背景，下面是操作选择算法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="31c4a-195">匹配的 HTTP 请求方法的控制器中创建的所有操作的列表。</span><span class="sxs-lookup"><span data-stu-id="31c4a-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="31c4a-196">如果路由字典具有"操作"条目，删除其名称与此值不匹配的操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="31c4a-197">尝试匹配到 URI 操作参数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31c4a-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="31c4a-198">对于每个操作，获取一系列是一种简单类型，其中，绑定将参数从 URI 参数。</span><span class="sxs-lookup"><span data-stu-id="31c4a-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="31c4a-199">排除的可选参数。</span><span class="sxs-lookup"><span data-stu-id="31c4a-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="31c4a-200">从此列表中，尝试路由字典中或在 URI 查询字符串中查找每个参数名称的匹配项。</span><span class="sxs-lookup"><span data-stu-id="31c4a-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="31c4a-201">匹配是不区分大小写，不依赖于参数顺序。</span><span class="sxs-lookup"><span data-stu-id="31c4a-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="31c4a-202">选择列表中的每个参数在 URI 中存在匹配项的其中一项操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="31c4a-203">如果有多个操作满足这些条件，选择其中一个的大多数参数匹配项。</span><span class="sxs-lookup"><span data-stu-id="31c4a-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="31c4a-204">忽略操作 **[NonAction]** 属性。</span><span class="sxs-lookup"><span data-stu-id="31c4a-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="31c4a-205">步骤 #3 是可能最容易引起混淆。</span><span class="sxs-lookup"><span data-stu-id="31c4a-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="31c4a-206">基本理念是 URI 中，从请求正文中，或者从自定义绑定，参数可以获取其值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="31c4a-207">对于来自 URI 的参数，我们想要确保 URI 实际上包含该参数中 （通过路由字典） 的路径或查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="31c4a-208">例如，考虑以下操作：</span><span class="sxs-lookup"><span data-stu-id="31c4a-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="31c4a-209">*Id*参数绑定到的 URI。</span><span class="sxs-lookup"><span data-stu-id="31c4a-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="31c4a-210">因此，此操作只能匹配一个 URI，包含"id"，在路由字典中或在查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="31c4a-211">可选参数是个例外，因为它们是可选的。</span><span class="sxs-lookup"><span data-stu-id="31c4a-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="31c4a-212">可选参数，它将是确定，如果绑定不能从 URI 中获取的值。</span><span class="sxs-lookup"><span data-stu-id="31c4a-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="31c4a-213">复杂类型是由于其他原因的异常。</span><span class="sxs-lookup"><span data-stu-id="31c4a-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="31c4a-214">通过自定义绑定的复杂类型只能绑定到的 URI。</span><span class="sxs-lookup"><span data-stu-id="31c4a-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="31c4a-215">但在这种情况下，该框架不能提前知道参数将绑定到特定的 URI。</span><span class="sxs-lookup"><span data-stu-id="31c4a-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="31c4a-216">若要了解，它需要调用绑定。</span><span class="sxs-lookup"><span data-stu-id="31c4a-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="31c4a-217">选择算法的目的是从静态的说明，然后再调用任何绑定选择一项操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="31c4a-218">因此，复杂类型不从匹配算法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="31c4a-219">选择操作后，会调用参数的所有绑定。</span><span class="sxs-lookup"><span data-stu-id="31c4a-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="31c4a-220">摘要:</span><span class="sxs-lookup"><span data-stu-id="31c4a-220">Summary:</span></span>

- <span data-ttu-id="31c4a-221">Action 必须与请求的 HTTP 方法匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="31c4a-222">如果存在，则操作名称必须与匹配路由字典中的"操作"条目。</span><span class="sxs-lookup"><span data-stu-id="31c4a-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="31c4a-223">对于操作的每个参数，如果该参数来自 URI，则参数名称必须找到路由字典中或在 URI 查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="31c4a-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="31c4a-224">（可选参数和复杂类型的参数被排除。）</span><span class="sxs-lookup"><span data-stu-id="31c4a-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="31c4a-225">尝试匹配最大数量的参数。</span><span class="sxs-lookup"><span data-stu-id="31c4a-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="31c4a-226">最佳匹配项可能是不带任何参数的方法。</span><span class="sxs-lookup"><span data-stu-id="31c4a-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="31c4a-227">扩展的示例</span><span class="sxs-lookup"><span data-stu-id="31c4a-227">Extended Example</span></span>

<span data-ttu-id="31c4a-228">路由：</span><span class="sxs-lookup"><span data-stu-id="31c4a-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="31c4a-229">控制器:</span><span class="sxs-lookup"><span data-stu-id="31c4a-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="31c4a-230">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="31c4a-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="31c4a-231">路由匹配</span><span class="sxs-lookup"><span data-stu-id="31c4a-231">Route Matching</span></span>

<span data-ttu-id="31c4a-232">URI 匹配名为"DefaultApi"的路由。</span><span class="sxs-lookup"><span data-stu-id="31c4a-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="31c4a-233">路由字典包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="31c4a-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="31c4a-234">控制器:"产品"</span><span class="sxs-lookup"><span data-stu-id="31c4a-234">controller: "products"</span></span>
- <span data-ttu-id="31c4a-235">id:"1"</span><span class="sxs-lookup"><span data-stu-id="31c4a-235">id: "1"</span></span>

<span data-ttu-id="31c4a-236">路由字典不包含查询字符串参数、"版本"和"详细信息"，但它们仍被视为在操作选择过程。</span><span class="sxs-lookup"><span data-stu-id="31c4a-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="31c4a-237">控制器所选内容</span><span class="sxs-lookup"><span data-stu-id="31c4a-237">Controller Selection</span></span>

<span data-ttu-id="31c4a-238">控制器类型是从路由字典中的"控制器"条目， `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="31c4a-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="31c4a-239">操作选择</span><span class="sxs-lookup"><span data-stu-id="31c4a-239">Action Selection</span></span>

<span data-ttu-id="31c4a-240">HTTP 请求是 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="31c4a-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="31c4a-241">支持 GET 的控制器操作`GetAll`， `GetById`，和`FindProductsByName`。</span><span class="sxs-lookup"><span data-stu-id="31c4a-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="31c4a-242">路由字典不包含"操作"的项，因此我们无需与操作名称匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="31c4a-243">接下来，我们尝试匹配参数名称的操作，只查看在 GET 操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="31c4a-244">操作</span><span class="sxs-lookup"><span data-stu-id="31c4a-244">Action</span></span> | <span data-ttu-id="31c4a-245">匹配的参数</span><span class="sxs-lookup"><span data-stu-id="31c4a-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="31c4a-246">无</span><span class="sxs-lookup"><span data-stu-id="31c4a-246">none</span></span> |
| `GetById` | <span data-ttu-id="31c4a-247">"id"</span><span class="sxs-lookup"><span data-stu-id="31c4a-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="31c4a-248">"name"</span><span class="sxs-lookup"><span data-stu-id="31c4a-248">"name"</span></span> |

<span data-ttu-id="31c4a-249">请注意，*版本*参数的`GetById`不被视为，因为它是一个可选参数。</span><span class="sxs-lookup"><span data-stu-id="31c4a-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="31c4a-250">`GetAll`方法完全匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="31c4a-251">`GetById`方法也与匹配，因为路由字典包含"id"。</span><span class="sxs-lookup"><span data-stu-id="31c4a-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="31c4a-252">`FindProductsByName`方法不匹配。</span><span class="sxs-lookup"><span data-stu-id="31c4a-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="31c4a-253">`GetById`方法 wins，因为它与一个参数，而不是任何参数匹配`GetAll`。</span><span class="sxs-lookup"><span data-stu-id="31c4a-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="31c4a-254">使用以下参数值调用该方法：</span><span class="sxs-lookup"><span data-stu-id="31c4a-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="31c4a-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="31c4a-255">*id* = 1</span></span>
- <span data-ttu-id="31c4a-256">*版本*= 1.5</span><span class="sxs-lookup"><span data-stu-id="31c4a-256">*version* = 1.5</span></span>

<span data-ttu-id="31c4a-257">请注意，即使*版本*不使用在选择算法参数的值来自 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="31c4a-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="31c4a-258">扩展点</span><span class="sxs-lookup"><span data-stu-id="31c4a-258">Extension Points</span></span>

<span data-ttu-id="31c4a-259">Web API 路由过程的某些部分提供了扩展点。</span><span class="sxs-lookup"><span data-stu-id="31c4a-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="31c4a-260">接口</span><span class="sxs-lookup"><span data-stu-id="31c4a-260">Interface</span></span> | <span data-ttu-id="31c4a-261">描述</span><span class="sxs-lookup"><span data-stu-id="31c4a-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31c4a-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="31c4a-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="31c4a-263">选择控制器。</span><span class="sxs-lookup"><span data-stu-id="31c4a-263">Selects the controller.</span></span> |
| <span data-ttu-id="31c4a-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="31c4a-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="31c4a-265">获取控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="31c4a-265">Gets the list of controller types.</span></span> <span data-ttu-id="31c4a-266">**DefaultHttpControllerSelector**从此列表中选择控制器类型。</span><span class="sxs-lookup"><span data-stu-id="31c4a-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="31c4a-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="31c4a-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="31c4a-268">获取项目的程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="31c4a-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="31c4a-269">**IHttpControllerTypeResolver**接口使用此列表以找到控制器的类型。</span><span class="sxs-lookup"><span data-stu-id="31c4a-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="31c4a-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="31c4a-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="31c4a-271">创建新的控制器实例。</span><span class="sxs-lookup"><span data-stu-id="31c4a-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="31c4a-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="31c4a-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="31c4a-273">选择操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-273">Selects the action.</span></span> |
| <span data-ttu-id="31c4a-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="31c4a-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="31c4a-275">调用的操作。</span><span class="sxs-lookup"><span data-stu-id="31c4a-275">Invokes the action.</span></span> |

<span data-ttu-id="31c4a-276">若要为任何这些接口提供您自己的实现，使用**Services**上的收集**HttpConfiguration**对象：</span><span class="sxs-lookup"><span data-stu-id="31c4a-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
