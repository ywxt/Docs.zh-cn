---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 支持 ASP.NET Web API 2 中的 OData 操作 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。 操作的一些用途包括： 实现...
ms.author: aspnetcontent
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: e02ab21b864e328fe6892a00e5d5aca3f88eb9a2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837767"
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="435d8-104">支持 ASP.NET Web API 2 中的 OData 操作</span><span class="sxs-lookup"><span data-stu-id="435d8-104">Supporting OData Actions in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="435d8-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="435d8-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="435d8-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="435d8-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="435d8-107">在 OData 中，*操作*是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。</span><span class="sxs-lookup"><span data-stu-id="435d8-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="435d8-108">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="435d8-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="435d8-109">实现复杂的事务处理。</span><span class="sxs-lookup"><span data-stu-id="435d8-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="435d8-110">在一次处理多个实体。</span><span class="sxs-lookup"><span data-stu-id="435d8-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="435d8-111">允许仅对实体的某些属性的更新。</span><span class="sxs-lookup"><span data-stu-id="435d8-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="435d8-112">将信息发送到未定义实体中的服务器。</span><span class="sxs-lookup"><span data-stu-id="435d8-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="435d8-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="435d8-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="435d8-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="435d8-114">Web API 2</span></span>
> - <span data-ttu-id="435d8-115">OData 版本 3</span><span class="sxs-lookup"><span data-stu-id="435d8-115">OData Version 3</span></span>
> - <span data-ttu-id="435d8-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="435d8-116">Entity Framework 6</span></span>


## <a name="example-rating-a-product"></a><span data-ttu-id="435d8-117">示例： 评级产品</span><span class="sxs-lookup"><span data-stu-id="435d8-117">Example: Rating a Product</span></span>

<span data-ttu-id="435d8-118">在此示例中，我们想要让用户评级的产品，并公开的每个产品的平均分级。</span><span class="sxs-lookup"><span data-stu-id="435d8-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="435d8-119">在数据库中，我们会存储一组分级，对产品进行键控。</span><span class="sxs-lookup"><span data-stu-id="435d8-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="435d8-120">下面是我们可能会用于表示实体框架中的评级的模型：</span><span class="sxs-lookup"><span data-stu-id="435d8-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="435d8-121">但我们不希望客户端针对 POST `ProductRating` "比率"集合的对象。</span><span class="sxs-lookup"><span data-stu-id="435d8-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="435d8-122">直观地说，此级别与产品集合中，关联，客户端应只需发布的分级值。</span><span class="sxs-lookup"><span data-stu-id="435d8-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="435d8-123">因此，而不是使用普通的 CRUD 操作，我们定义客户端可以调用的操作在产品上。</span><span class="sxs-lookup"><span data-stu-id="435d8-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="435d8-124">在 OData 术语中，该操作是*绑定*对产品实体。</span><span class="sxs-lookup"><span data-stu-id="435d8-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="435d8-125">操作在服务器上产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="435d8-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="435d8-126">出于此原因，它们会调用使用 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="435d8-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="435d8-127">操作可以具有参数和返回类型，服务元数据中所述。</span><span class="sxs-lookup"><span data-stu-id="435d8-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="435d8-128">客户端请求正文中发送参数和服务器响应正文中发送的返回值。</span><span class="sxs-lookup"><span data-stu-id="435d8-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="435d8-129">若要调用的"速率产品"操作，客户端将 POST 发送到如下所示的 URI:</span><span class="sxs-lookup"><span data-stu-id="435d8-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="435d8-130">POST 请求中的数据是只需产品评级：</span><span class="sxs-lookup"><span data-stu-id="435d8-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="435d8-131">声明的实体数据模型中的操作</span><span class="sxs-lookup"><span data-stu-id="435d8-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="435d8-132">在 Web API 配置中，将添加到实体数据模型 (EDM 中) 的操作：</span><span class="sxs-lookup"><span data-stu-id="435d8-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="435d8-133">此代码定义"RateProduct"作为可以对产品实体执行的操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="435d8-134">它还声明将的操作**int**参数名为"Rating"，并返回**int**值。</span><span class="sxs-lookup"><span data-stu-id="435d8-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="435d8-135">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="435d8-135">Add the Action to the Controller</span></span>

<span data-ttu-id="435d8-136">"RateProduct"操作绑定到产品实体。</span><span class="sxs-lookup"><span data-stu-id="435d8-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="435d8-137">若要实现此操作，添加一个名为`RateProduct`到产品控制器：</span><span class="sxs-lookup"><span data-stu-id="435d8-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="435d8-138">请注意方法名与 EDM 中的操作的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="435d8-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="435d8-139">该方法具有两个参数：</span><span class="sxs-lookup"><span data-stu-id="435d8-139">The method has two parameters:</span></span>

- <span data-ttu-id="435d8-140">*密钥*： 速率的产品密钥。</span><span class="sxs-lookup"><span data-stu-id="435d8-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="435d8-141">*参数*： 操作参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="435d8-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="435d8-142">如果使用的默认路由约定，key 参数必须命名为"密钥"。</span><span class="sxs-lookup"><span data-stu-id="435d8-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="435d8-143">还有一点需要包括 **[FromOdataUri]** 属性，如所示。</span><span class="sxs-lookup"><span data-stu-id="435d8-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="435d8-144">此属性告知 Web API 使用 OData 语法规则分析请求 URI 中的键时。</span><span class="sxs-lookup"><span data-stu-id="435d8-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="435d8-145">使用*参数*获取操作参数的字典：</span><span class="sxs-lookup"><span data-stu-id="435d8-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="435d8-146">如果客户端中正确发送操作参数，值的格式设置**ModelState.IsValid**为 true。</span><span class="sxs-lookup"><span data-stu-id="435d8-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="435d8-147">在这种情况下，可以使用**ODataActionParameters**获取参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="435d8-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="435d8-148">在此示例中，`RateProduct`操作采用单个参数名为"Rating"。</span><span class="sxs-lookup"><span data-stu-id="435d8-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="435d8-149">操作元数据</span><span class="sxs-lookup"><span data-stu-id="435d8-149">Action Metadata</span></span>

<span data-ttu-id="435d8-150">若要查看的服务元数据，请向 /odata/$ metadata 发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="435d8-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="435d8-151">下面是声明的元数据一部分`RateProduct`操作：</span><span class="sxs-lookup"><span data-stu-id="435d8-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="435d8-152">**FunctionImport**元素声明了操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="435d8-153">大多数字段都很容易理解，但两个值得一提：</span><span class="sxs-lookup"><span data-stu-id="435d8-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="435d8-154">**IsBindable**意味着操作可以调用目标实体上至少部分时间。</span><span class="sxs-lookup"><span data-stu-id="435d8-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="435d8-155">**IsAlwaysBindable**意味着始终可以在目标实体上调用操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="435d8-156">不同之处是，某些操作始终都可供客户端，但其他操作可能取决于实体的状态。</span><span class="sxs-lookup"><span data-stu-id="435d8-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="435d8-157">例如，假设您定义一个操作，"购买"。</span><span class="sxs-lookup"><span data-stu-id="435d8-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="435d8-158">你可以只购买是库存的项。</span><span class="sxs-lookup"><span data-stu-id="435d8-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="435d8-159">如果该项是脱销，客户端不能调用该操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="435d8-160">定义 EDM 中，当**操作**方法创建一个始终可绑定的操作：</span><span class="sxs-lookup"><span data-stu-id="435d8-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="435d8-161">我将讨论不始终-绑定操作 (也称为*暂时性*操作) 在此主题的后面。</span><span class="sxs-lookup"><span data-stu-id="435d8-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="435d8-162">调用操作</span><span class="sxs-lookup"><span data-stu-id="435d8-162">Invoking the Action</span></span>

<span data-ttu-id="435d8-163">现在让我们看如何在客户端将调用此操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="435d8-164">假设客户端想要让其分级为 2 的产品 ID = 4。</span><span class="sxs-lookup"><span data-stu-id="435d8-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="435d8-165">下面是使用 JSON 格式的请求正文的示例请求消息：</span><span class="sxs-lookup"><span data-stu-id="435d8-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="435d8-166">下面是响应消息：</span><span class="sxs-lookup"><span data-stu-id="435d8-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="435d8-167">绑定到实体集的操作</span><span class="sxs-lookup"><span data-stu-id="435d8-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="435d8-168">在上一示例中，操作绑定到单个实体： 客户端费率一个产品。</span><span class="sxs-lookup"><span data-stu-id="435d8-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="435d8-169">您还可以绑定到实体的集合的操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="435d8-170">只需进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="435d8-170">Just make the following changes:</span></span>

<span data-ttu-id="435d8-171">在 EDM 中，将操作添加到实体的**集合**属性。</span><span class="sxs-lookup"><span data-stu-id="435d8-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="435d8-172">在控制器方法中，省略*密钥*参数。</span><span class="sxs-lookup"><span data-stu-id="435d8-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="435d8-173">现在客户端调用 Products 实体集上的操作：</span><span class="sxs-lookup"><span data-stu-id="435d8-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="435d8-174">使用集合参数的操作</span><span class="sxs-lookup"><span data-stu-id="435d8-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="435d8-175">操作可以获取的值的集合的参数。</span><span class="sxs-lookup"><span data-stu-id="435d8-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="435d8-176">在 EDM 中，使用**CollectionParameter&lt;T&gt;** 若要将参数声明。</span><span class="sxs-lookup"><span data-stu-id="435d8-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="435d8-177">这会将名为"分级"采用的集合的参数声明**int**值。</span><span class="sxs-lookup"><span data-stu-id="435d8-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="435d8-178">在控制器方法中，您仍获取参数值从**ODataActionParameters**对象，但现在的值是**ICollection&lt;int&gt;** 值：</span><span class="sxs-lookup"><span data-stu-id="435d8-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="435d8-179">暂时性的操作</span><span class="sxs-lookup"><span data-stu-id="435d8-179">Transient Actions</span></span>

<span data-ttu-id="435d8-180">在"RateProduct"示例中，用户可以始终对产品评估，因此操作都可用。</span><span class="sxs-lookup"><span data-stu-id="435d8-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="435d8-181">但是，某些操作取决于实体的状态。</span><span class="sxs-lookup"><span data-stu-id="435d8-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="435d8-182">例如，在视频租赁服务中，"签出"操作不是始终可用。</span><span class="sxs-lookup"><span data-stu-id="435d8-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="435d8-183">（它取决于是否提供了该视频的一个副本。）此类型的操作称为*暂时性*操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="435d8-184">在服务元数据，暂时性操作具有**IsAlwaysBindable**等于 false。</span><span class="sxs-lookup"><span data-stu-id="435d8-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="435d8-185">这是实际的默认值，因此元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="435d8-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="435d8-186">此处为什么这很重要： 如果操作是暂时性的服务器需要告诉客户端操作时可用。</span><span class="sxs-lookup"><span data-stu-id="435d8-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="435d8-187">通过在实体中包含指向操作的执行此操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="435d8-188">下面是一个示例，用于电影实体：</span><span class="sxs-lookup"><span data-stu-id="435d8-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="435d8-189">"#CheckOut"属性包含签出操作的链接。</span><span class="sxs-lookup"><span data-stu-id="435d8-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="435d8-190">如果操作不可用，则服务器会忽略链接。</span><span class="sxs-lookup"><span data-stu-id="435d8-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="435d8-191">若要声明 EDM 中的暂时性操作，请调用**TransientAction**方法：</span><span class="sxs-lookup"><span data-stu-id="435d8-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="435d8-192">此外，必须提供一个函数，返回给定实体的操作链接。</span><span class="sxs-lookup"><span data-stu-id="435d8-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="435d8-193">设置此函数通过调用**HasActionLink**。</span><span class="sxs-lookup"><span data-stu-id="435d8-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="435d8-194">您可以编写函数作为 lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="435d8-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="435d8-195">如果操作不可用，lambda 表达式返回一个链接到的操作。</span><span class="sxs-lookup"><span data-stu-id="435d8-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="435d8-196">OData 序列化程序包括此链接时序列化实体。</span><span class="sxs-lookup"><span data-stu-id="435d8-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="435d8-197">当操作不可用时，该函数返回`null`。</span><span class="sxs-lookup"><span data-stu-id="435d8-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="435d8-198">其他资源</span><span class="sxs-lookup"><span data-stu-id="435d8-198">Additional Resources</span></span>

[<span data-ttu-id="435d8-199">OData 操作示例</span><span class="sxs-lookup"><span data-stu-id="435d8-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
