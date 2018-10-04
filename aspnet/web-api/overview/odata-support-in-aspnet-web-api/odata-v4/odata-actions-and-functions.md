---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 操作和 OData v4 中的函数使用 ASP.NET Web API 2.2 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作和函数是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。 本教程演示如何...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 45b84ec4ee76e83ece99bf6841c28e13c3ab7728
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795262"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="5592b-104">操作和使用 ASP.NET Web API 2.2 OData v4 中的函数</span><span class="sxs-lookup"><span data-stu-id="5592b-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="5592b-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5592b-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="5592b-106">在 OData 中，操作和函数是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。</span><span class="sxs-lookup"><span data-stu-id="5592b-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="5592b-107">本教程演示如何将操作和函数添加到使用 Web API 2.2 的 OData v4 终结点。</span><span class="sxs-lookup"><span data-stu-id="5592b-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="5592b-108">本教程在本教程以[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="5592b-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5592b-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5592b-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="5592b-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="5592b-110">Web API 2.2</span></span>
> - <span data-ttu-id="5592b-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="5592b-111">OData v4</span></span>
> - <span data-ttu-id="5592b-112">Visual Studio 2013 (下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="5592b-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="5592b-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5592b-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="5592b-114">教程版本</span><span class="sxs-lookup"><span data-stu-id="5592b-114">Tutorial versions</span></span>
>
> <span data-ttu-id="5592b-115">OData 版本 3，请参阅[ASP.NET Web API 2 中的 OData 操作](../odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="5592b-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="5592b-116">之间的差异*操作*并*函数*是操作可能会有副作用，并且函数不这样做。</span><span class="sxs-lookup"><span data-stu-id="5592b-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="5592b-117">操作和函数可以返回数据。</span><span class="sxs-lookup"><span data-stu-id="5592b-117">Both actions and functions can return data.</span></span> <span data-ttu-id="5592b-118">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="5592b-118">Some uses for actions include:</span></span>

- <span data-ttu-id="5592b-119">复杂的事务处理。</span><span class="sxs-lookup"><span data-stu-id="5592b-119">Complex transactions.</span></span>
- <span data-ttu-id="5592b-120">在一次处理多个实体。</span><span class="sxs-lookup"><span data-stu-id="5592b-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="5592b-121">允许仅对实体的某些属性的更新。</span><span class="sxs-lookup"><span data-stu-id="5592b-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="5592b-122">不是一个实体的发送数据。</span><span class="sxs-lookup"><span data-stu-id="5592b-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="5592b-123">函数可用于返回直接向某一实体或集合的信息不对应。</span><span class="sxs-lookup"><span data-stu-id="5592b-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="5592b-124">操作 （或函数） 可以针对单个实体或集合。</span><span class="sxs-lookup"><span data-stu-id="5592b-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="5592b-125">在 OData 术语中，这是*绑定*。</span><span class="sxs-lookup"><span data-stu-id="5592b-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="5592b-126">此外可以让&quot;未绑定&quot;操作/函数，作为服务上的静态操作调用。</span><span class="sxs-lookup"><span data-stu-id="5592b-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="5592b-127">示例： 添加操作</span><span class="sxs-lookup"><span data-stu-id="5592b-127">Example: Adding an Action</span></span>

<span data-ttu-id="5592b-128">让我们来定义要对产品评估的操作。</span><span class="sxs-lookup"><span data-stu-id="5592b-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="5592b-129">本教程基于本教程[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="5592b-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>


<span data-ttu-id="5592b-130">首先，添加`ProductRating`模型来表示分级。</span><span class="sxs-lookup"><span data-stu-id="5592b-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="5592b-131">此外将添加**DbSet**到`ProductsContext`基类，因此 EF 将在数据库中创建的分级表。</span><span class="sxs-lookup"><span data-stu-id="5592b-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="5592b-132">将操作添加到 EDM</span><span class="sxs-lookup"><span data-stu-id="5592b-132">Add the Action to the EDM</span></span>

<span data-ttu-id="5592b-133">在 WebApiConfig.cs 中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="5592b-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="5592b-134">**EntityTypeConfiguration.Action**方法将操作添加到实体数据模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="5592b-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="5592b-135">**参数**方法指定操作的类型化的参数。</span><span class="sxs-lookup"><span data-stu-id="5592b-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="5592b-136">此代码还设置 EDM 的命名空间。</span><span class="sxs-lookup"><span data-stu-id="5592b-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="5592b-137">命名空间很重要，因为操作的 URI 包含完全限定的操作名称：</span><span class="sxs-lookup"><span data-stu-id="5592b-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="5592b-138">在典型的 IIS 配置，此 URL 中的点将导致 IIS 返回 404 错误。</span><span class="sxs-lookup"><span data-stu-id="5592b-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="5592b-139">可以通过将以下部分添加到 Web.Config 文件来解决此问题：</span><span class="sxs-lookup"><span data-stu-id="5592b-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="5592b-140">为操作添加一个控制器方法</span><span class="sxs-lookup"><span data-stu-id="5592b-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="5592b-141">若要启用&quot;速率&quot;操作，添加以下方法`ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="5592b-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="5592b-142">请注意方法名与操作名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="5592b-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="5592b-143">**[HttpPost]** 属性指定该方法是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="5592b-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="5592b-144">若要调用的操作，客户端发送一个 HTTP POST 请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5592b-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="5592b-145">&quot;速率&quot;操作绑定到 Product 实例，因此该操作的 URI 是追加到 URI 的实体的完全限定的操作名称。</span><span class="sxs-lookup"><span data-stu-id="5592b-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="5592b-146">(回想一下，我们设置为 EDM 命名空间&quot;ProductService&quot;，因此完全限定的操作名称是&quot;ProductService.Rate&quot;。)</span><span class="sxs-lookup"><span data-stu-id="5592b-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="5592b-147">请求正文包含作为 JSON 有效负载的操作参数。</span><span class="sxs-lookup"><span data-stu-id="5592b-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="5592b-148">Web API 会自动将转换为 JSON 有效负载**ODataActionParameters**对象，它是只是参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="5592b-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="5592b-149">使用此字典来访问你的控制器方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="5592b-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="5592b-150">如果客户端发送错误的操作参数，值的格式设置**ModelState.IsValid**为 false。</span><span class="sxs-lookup"><span data-stu-id="5592b-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="5592b-151">检查此标志在控制器方法中的，如果返回错误**IsValid**为 false。</span><span class="sxs-lookup"><span data-stu-id="5592b-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="5592b-152">示例： 添加函数</span><span class="sxs-lookup"><span data-stu-id="5592b-152">Example: Adding a Function</span></span>

<span data-ttu-id="5592b-153">现在让我们添加返回最贵的产品的 OData 函数。</span><span class="sxs-lookup"><span data-stu-id="5592b-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="5592b-154">如之前，第一步将函数添加到 EDM。</span><span class="sxs-lookup"><span data-stu-id="5592b-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="5592b-155">在 WebApiConfig.cs 中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="5592b-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="5592b-156">在这种情况下，此函数绑定到产品集合，而不是各个实例的产品。</span><span class="sxs-lookup"><span data-stu-id="5592b-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="5592b-157">客户端通过发送 GET 请求来调用此函数：</span><span class="sxs-lookup"><span data-stu-id="5592b-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="5592b-158">下面是此函数的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="5592b-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="5592b-159">请注意，方法名称的函数名称匹配。</span><span class="sxs-lookup"><span data-stu-id="5592b-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="5592b-160">**[HttpGet]** 属性指定的方法是 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="5592b-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="5592b-161">下面是 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="5592b-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="5592b-162">示例： 添加一个未绑定的函数</span><span class="sxs-lookup"><span data-stu-id="5592b-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="5592b-163">上一个示例是绑定到集合的函数。</span><span class="sxs-lookup"><span data-stu-id="5592b-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="5592b-164">在下一个示例，我们将创建*未绑定*函数。</span><span class="sxs-lookup"><span data-stu-id="5592b-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="5592b-165">作为服务上的静态操作称为未绑定的函数。</span><span class="sxs-lookup"><span data-stu-id="5592b-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="5592b-166">在此示例中该函数将返回针对给定的邮政编码销售税。</span><span class="sxs-lookup"><span data-stu-id="5592b-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="5592b-167">在 WebApiConfig 文件中，添加到 EDM 函数：</span><span class="sxs-lookup"><span data-stu-id="5592b-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="5592b-168">请注意，我们将调用**函数**是直接对**ODataModelBuilder**，而不是实体类型或集合。</span><span class="sxs-lookup"><span data-stu-id="5592b-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="5592b-169">这将告知模型生成器的函数是未绑定。</span><span class="sxs-lookup"><span data-stu-id="5592b-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="5592b-170">下面是实现该函数的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="5592b-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="5592b-171">并不重要的 Web API 控制器将放在此方法。</span><span class="sxs-lookup"><span data-stu-id="5592b-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="5592b-172">可以将它放`ProductsController`，或定义单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="5592b-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="5592b-173">**[ODataRoute]** 属性定义了该函数的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="5592b-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="5592b-174">下面是示例客户端请求：</span><span class="sxs-lookup"><span data-stu-id="5592b-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="5592b-175">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="5592b-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
