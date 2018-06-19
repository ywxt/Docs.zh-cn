---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: 在 ASP.NET Web API 2 中测试控制器的单元 |Microsoft 文档
author: MikeWasson
description: 本主题介绍一些特定技术进行单元测试 Web API 2 中的控制器。 在阅读本主题之前, 可能需要阅读教程单元...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/11/2014
ms.topic: article
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: bda5148a4c1553d70f3173de66371fbb8576e83f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28039539"
---
<a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="4d0aa-104">在 ASP.NET Web API 2 中测试控制器的单元</span><span class="sxs-lookup"><span data-stu-id="4d0aa-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="4d0aa-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4d0aa-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="4d0aa-106">本主题介绍一些特定技术进行单元测试 Web API 2 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="4d0aa-107">在阅读本主题之前, 可能需要阅读本教程[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，其中说明了如何将单元测试项目添加到你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4d0aa-108">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4d0aa-108">Software versions used in the tutorial</span></span>
> 
> - [<span data-ttu-id="4d0aa-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4d0aa-109">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="4d0aa-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="4d0aa-110">Web API 2</span></span>
> - <span data-ttu-id="4d0aa-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="4d0aa-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="4d0aa-112">我使用 Moq，但相同的思想适用于任何模拟框架。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="4d0aa-113">Moq 4.5.30 （和更高版本） 支持 Visual Studio 2017、 Roslyn 和.NET 4.5 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="4d0aa-114">在单位测试中的常见模式是&quot;排列 act 断言&quot;:</span><span class="sxs-lookup"><span data-stu-id="4d0aa-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="4d0aa-115">排列： 设置测试运行的任何必备组件。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="4d0aa-116">Act： 执行测试。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-116">Act: Perform the test.</span></span>
- <span data-ttu-id="4d0aa-117">断言： 验证测试成功完成。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="4d0aa-118">在准备步骤中，你通常将使用 mock 或存根对象。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="4d0aa-119">最小化依赖项，数以便测试侧重于测试的一件事情。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="4d0aa-120">下面是一些你应在你的 Web API 控制器中的单元测试：</span><span class="sxs-lookup"><span data-stu-id="4d0aa-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="4d0aa-121">操作返回响应的正确的类型。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="4d0aa-122">无效的参数返回正确的错误响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="4d0aa-123">操作在存储库或服务层上调用的正确方法。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="4d0aa-124">如果响应包含域模型，请验证模型类型。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="4d0aa-125">这些是的一些常规操作，若要测试，但具体情况取决于你的控制器实现。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="4d0aa-126">具体而言，它有很大差别是否控制器操作返回**HttpResponseMessage**或**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="4d0aa-127">有关这些结果类型的详细信息，请参阅[Web Api 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="4d0aa-128">返回 HttpResponseMessage 的测试操作</span><span class="sxs-lookup"><span data-stu-id="4d0aa-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="4d0aa-129">下面是控制器的一个示例其操作返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="4d0aa-130">请注意的控制器使用依赖关系注入注入`IProductRepository`。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="4d0aa-131">这使得控制器更可测试性，因为可以插入模拟的存储库。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="4d0aa-132">下面的单元测试验证`Get`方法写入`Product`向响应正文。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="4d0aa-133">假定`repository`是模型`IProductRepository`。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="4d0aa-134">务必要设置**请求**和**配置**在控制器上。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="4d0aa-135">否则，测试将会失败并**ArgumentNullException**或**InvalidOperationException**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="4d0aa-136">测试链接生成</span><span class="sxs-lookup"><span data-stu-id="4d0aa-136">Testing Link Generation</span></span>

<span data-ttu-id="4d0aa-137">`Post`方法调用**UrlHelper.Link**在响应中创建链接。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="4d0aa-138">这需要为单元测试中的一些更多的设置：</span><span class="sxs-lookup"><span data-stu-id="4d0aa-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="4d0aa-139">**UrlHelper**类需要请求 URL 和路由数据，因此测试必须为这些设置的值。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="4d0aa-140">另一个选项是模型或存根 （stub） **UrlHelper**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="4d0aa-141">使用此方法时，将默认值的[ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) mock 或存根 （stub） 的版本，返回固定的值。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="4d0aa-142">让我们重写测试使用[Moq](https://github.com/Moq) framework。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="4d0aa-143">安装`Moq`测试项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="4d0aa-144">在此版本中，你无需设置的任何路由数据，因为 mock **UrlHelper**返回常量字符串。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>


## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="4d0aa-145">返回 IHttpActionResult 的测试操作</span><span class="sxs-lookup"><span data-stu-id="4d0aa-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="4d0aa-146">Web API 2 控制器操作可以返回**IHttpActionResult**，这是类似于**ActionResult** ASP.NET mvc。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="4d0aa-147">**IHttpActionResult**接口定义命令的模式创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="4d0aa-148">而不是直接创建响应，则控制器将返回**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="4d0aa-149">更高版本，管道时，将调用**IHttpActionResult**创建响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="4d0aa-150">此方法使它成为更轻松地编写单元测试，因为你可以跳过的安装程序所需的很多**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="4d0aa-151">下面是示例控制器其操作返回**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="4d0aa-152">此示例演示使用一些常见模式**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="4d0aa-153">让我们看看如何与单元测试它们。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="4d0aa-154">操作返回 200 （正常） 的响应正文</span><span class="sxs-lookup"><span data-stu-id="4d0aa-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="4d0aa-155">`Get`方法调用`Ok(product)`如果找到该产品。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="4d0aa-156">在单元测试，请确保返回的类型是**OkNegotiatedContentResult**和退回的产品具有正确的 id。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="4d0aa-157">请注意，单元测试不会执行的操作结果。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="4d0aa-158">你可以假定的操作结果正确创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="4d0aa-159">(这就是为什么 Web API 框架具有其自己的单元测试 ！)</span><span class="sxs-lookup"><span data-stu-id="4d0aa-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="4d0aa-160">操作返回 404 （未找到）</span><span class="sxs-lookup"><span data-stu-id="4d0aa-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="4d0aa-161">`Get`方法调用`NotFound()`如果找不到产品。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="4d0aa-162">这种情况下，单元测试仅检查，如果返回类型为**NotFoundResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="4d0aa-163">操作返回 200 （正常） 的任何响应正文</span><span class="sxs-lookup"><span data-stu-id="4d0aa-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="4d0aa-164">`Delete`方法调用`Ok()`返回了空的 HTTP 200 响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="4d0aa-165">如前面的示例中，单元测试检查返回类型，在这种情况下**OkResult**。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="4d0aa-166">操作返回 201 （已创建） 使用位置的标头</span><span class="sxs-lookup"><span data-stu-id="4d0aa-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="4d0aa-167">`Post`方法调用`CreatedAtRoute`以位置标头中返回 HTTP 201 响应，其中一个 URI。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="4d0aa-168">在单元测试中，验证操作将设置正确路由值。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="4d0aa-169">操作返回响应正文的另一个的 2xx</span><span class="sxs-lookup"><span data-stu-id="4d0aa-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="4d0aa-170">`Put`方法调用`Content`返回响应正文的 HTTP 202 （已接受） 响应。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="4d0aa-171">这种情况下是类似于返回 200 （正常），但单元测试还应检查的状态代码。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="4d0aa-172">其他资源</span><span class="sxs-lookup"><span data-stu-id="4d0aa-172">Additional Resources</span></span>

- [<span data-ttu-id="4d0aa-173">模拟实体框架时单元测试 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="4d0aa-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="4d0aa-174">[为 ASP.NET Web API 服务编写测试](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx)（通过 Youssef Moussaoui 博客文章）。</span><span class="sxs-lookup"><span data-stu-id="4d0aa-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="4d0aa-175">调试 ASP.NET Web API 与路由调试器</span><span class="sxs-lookup"><span data-stu-id="4d0aa-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
