---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 操作和函数在 OData v4 使用 ASP.NET Web API 2.2 |Microsoft 文档
author: MikeWasson
description: 在 OData 中，操作和函数都可添加轻松未定义为对实体的 CRUD 操作的服务器端行为的方法。 本教程演示如何...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 532362f0c0faaaf0cb0c04726856f0497e5261b5
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508226"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="803ef-104">操作和使用 ASP.NET Web API 2.2 中 OData v4 函数</span><span class="sxs-lookup"><span data-stu-id="803ef-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="803ef-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="803ef-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="803ef-106">在 OData 中，操作和函数都可添加轻松未定义为对实体的 CRUD 操作的服务器端行为的方法。</span><span class="sxs-lookup"><span data-stu-id="803ef-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="803ef-107">本教程演示如何向 OData v4 终结点，使用 Web API 2.2 添加操作和函数。</span><span class="sxs-lookup"><span data-stu-id="803ef-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="803ef-108">本教程以教程为基础[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="803ef-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="803ef-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="803ef-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="803ef-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="803ef-110">Web API 2.2</span></span>
> - <span data-ttu-id="803ef-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="803ef-111">OData v4</span></span>
> - [<span data-ttu-id="803ef-112">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="803ef-112">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="803ef-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="803ef-113">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="803ef-114">教程版本</span><span class="sxs-lookup"><span data-stu-id="803ef-114">Tutorial versions</span></span>
> 
> <span data-ttu-id="803ef-115">有关 OData 版本 3，请参阅[ASP.NET Web API 2 中的 OData 操作](../odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="803ef-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>


<span data-ttu-id="803ef-116">之间的差异*操作*和*函数*是操作可能会有副作用，并且函数不这样做。</span><span class="sxs-lookup"><span data-stu-id="803ef-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="803ef-117">操作和函数可返回数据。</span><span class="sxs-lookup"><span data-stu-id="803ef-117">Both actions and functions can return data.</span></span> <span data-ttu-id="803ef-118">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="803ef-118">Some uses for actions include:</span></span>

- <span data-ttu-id="803ef-119">复杂的事务处理。</span><span class="sxs-lookup"><span data-stu-id="803ef-119">Complex transactions.</span></span>
- <span data-ttu-id="803ef-120">同时对多个实体进行操作。</span><span class="sxs-lookup"><span data-stu-id="803ef-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="803ef-121">允许仅对某些属性的实体的更新。</span><span class="sxs-lookup"><span data-stu-id="803ef-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="803ef-122">不是实体的发送数据。</span><span class="sxs-lookup"><span data-stu-id="803ef-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="803ef-123">函数可用于直接于实体或集合中返回不对应的信息。</span><span class="sxs-lookup"><span data-stu-id="803ef-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="803ef-124">操作 （或函数） 可以针对单个实体或集合。</span><span class="sxs-lookup"><span data-stu-id="803ef-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="803ef-125">在 OData 术语中，这是*绑定*。</span><span class="sxs-lookup"><span data-stu-id="803ef-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="803ef-126">此外可以让&quot;未绑定&quot;操作/函数，作为服务上的静态操作调用。</span><span class="sxs-lookup"><span data-stu-id="803ef-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="803ef-127">示例： 添加操作</span><span class="sxs-lookup"><span data-stu-id="803ef-127">Example: Adding an Action</span></span>

<span data-ttu-id="803ef-128">让我们定义要对产品评估的操作。</span><span class="sxs-lookup"><span data-stu-id="803ef-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="803ef-129">本教程基于本教程[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="803ef-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>


<span data-ttu-id="803ef-130">首先，添加`ProductRating`模型来表示分级。</span><span class="sxs-lookup"><span data-stu-id="803ef-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="803ef-131">此外添加**DbSet**到`ProductsContext`类，以便 EF 将在数据库中创建分级表。</span><span class="sxs-lookup"><span data-stu-id="803ef-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="803ef-132">将操作添加到 EDM</span><span class="sxs-lookup"><span data-stu-id="803ef-132">Add the Action to the EDM</span></span>

<span data-ttu-id="803ef-133">在 WebApiConfig.cs 中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="803ef-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="803ef-134">**EntityTypeConfiguration.Action**方法将操作添加到实体数据模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="803ef-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="803ef-135">**参数**方法指定操作的类型化的参数。</span><span class="sxs-lookup"><span data-stu-id="803ef-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="803ef-136">此代码还设置 EDM 的命名空间。</span><span class="sxs-lookup"><span data-stu-id="803ef-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="803ef-137">命名空间很重要，因为操作 URI 包含完全限定的操作名称：</span><span class="sxs-lookup"><span data-stu-id="803ef-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="803ef-138">在典型的 IIS 配置中，此 URL 中的点则会导致 IIS 返回 404 错误。</span><span class="sxs-lookup"><span data-stu-id="803ef-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="803ef-139">可以通过将以下部分添加到你的 Web.Config 文件来解决此问题：</span><span class="sxs-lookup"><span data-stu-id="803ef-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="803ef-140">操作中添加一个控制器方法</span><span class="sxs-lookup"><span data-stu-id="803ef-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="803ef-141">若要启用&quot;速率&quot;操作，添加以下方法`ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="803ef-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="803ef-142">请注意的方法名称匹配的操作名称。</span><span class="sxs-lookup"><span data-stu-id="803ef-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="803ef-143">**[HttpPost]** 属性指定该方法是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="803ef-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="803ef-144">若要调用的操作，客户端发送 HTTP POST 请求如下所示：</span><span class="sxs-lookup"><span data-stu-id="803ef-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="803ef-145">&quot;速率&quot;操作绑定到产品实例，因此操作 URI 是追加到 URI 的实体的完全限定的操作名称。</span><span class="sxs-lookup"><span data-stu-id="803ef-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="803ef-146">(回想一下，我们设置 EDM 命名空间为&quot;ProductService&quot;，因此完全限定的操作名称是&quot;ProductService.Rate&quot;。)</span><span class="sxs-lookup"><span data-stu-id="803ef-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="803ef-147">请求正文以 JSON 负载形式包含的操作参数。</span><span class="sxs-lookup"><span data-stu-id="803ef-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="803ef-148">Web API 会自动将转换为 JSON 负载**ODataActionParameters**对象，它是只是参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="803ef-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="803ef-149">使用此字典访问控制器方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="803ef-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="803ef-150">如果客户端发送在正确的操作参数的值格式化**ModelState.IsValid**为 false。</span><span class="sxs-lookup"><span data-stu-id="803ef-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="803ef-151">检查控制器方法中的此标志，如果返回错误**IsValid**为 false。</span><span class="sxs-lookup"><span data-stu-id="803ef-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="803ef-152">示例： 添加函数</span><span class="sxs-lookup"><span data-stu-id="803ef-152">Example: Adding a Function</span></span>

<span data-ttu-id="803ef-153">现在让我们添加一个 OData 函数，返回成本最高的产品。</span><span class="sxs-lookup"><span data-stu-id="803ef-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="803ef-154">如之前，第一步将该函数添加到 EDM 中。</span><span class="sxs-lookup"><span data-stu-id="803ef-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="803ef-155">在 WebApiConfig.cs 中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="803ef-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="803ef-156">在这种情况下，将函数绑定到产品集合，而不是各个实例的产品。</span><span class="sxs-lookup"><span data-stu-id="803ef-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="803ef-157">客户端通过发送 GET 请求调用此函数：</span><span class="sxs-lookup"><span data-stu-id="803ef-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="803ef-158">下面是此函数在控制器方法：</span><span class="sxs-lookup"><span data-stu-id="803ef-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="803ef-159">请注意的方法名称匹配的函数名称。</span><span class="sxs-lookup"><span data-stu-id="803ef-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="803ef-160">**[HttpGet]** 属性指定方法是 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="803ef-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="803ef-161">下面是 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="803ef-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="803ef-162">示例： 添加未绑定的函数</span><span class="sxs-lookup"><span data-stu-id="803ef-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="803ef-163">前面的示例已绑定到集合的函数。</span><span class="sxs-lookup"><span data-stu-id="803ef-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="803ef-164">在下一个示例，我们将创建*未绑定*函数。</span><span class="sxs-lookup"><span data-stu-id="803ef-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="803ef-165">未绑定的函数是作为服务上的静态操作调用的。</span><span class="sxs-lookup"><span data-stu-id="803ef-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="803ef-166">此示例中的函数将返回的增值税给定邮政编码。</span><span class="sxs-lookup"><span data-stu-id="803ef-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="803ef-167">在 WebApiConfig 文件中，添加到 EDM 的函数：</span><span class="sxs-lookup"><span data-stu-id="803ef-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="803ef-168">请注意，我们正在呼叫**函数**直接基于**ODataModelBuilder**，而不是实体类型或集合。</span><span class="sxs-lookup"><span data-stu-id="803ef-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="803ef-169">这将告知模型生成器函数是未绑定。</span><span class="sxs-lookup"><span data-stu-id="803ef-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="803ef-170">以下是实现了该函数的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="803ef-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="803ef-171">它并不重要放置在此方法的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="803ef-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="803ef-172">无法将其放入`ProductsController`，或定义单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="803ef-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="803ef-173">**[ODataRoute]** 属性定义用于函数的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="803ef-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="803ef-174">下面是一个示例客户端请求：</span><span class="sxs-lookup"><span data-stu-id="803ef-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="803ef-175">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="803ef-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
