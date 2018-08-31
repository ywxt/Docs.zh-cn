---
title: ASP.NET Core 中的测试控制器逻辑
author: ardalis
description: 了解如何使用 Moq 和 xUnit 测试 ASP.NET Core 中的控制器逻辑。
ms.author: riande
ms.date: 10/14/2016
uid: mvc/controllers/testing
ms.openlocfilehash: d0b2a25d00187c088671be147844aa892f824c6e
ms.sourcegitcommit: 64c2ca86fff445944b155635918126165ee0f8aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2018
ms.locfileid: "41751771"
---
# <a name="test-controller-logic-in-aspnet-core"></a><span data-ttu-id="450f9-103">ASP.NET Core 中的测试控制器逻辑</span><span class="sxs-lookup"><span data-stu-id="450f9-103">Test controller logic in ASP.NET Core</span></span>

<span data-ttu-id="450f9-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="450f9-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="450f9-105">控制器是任意 ASP.NET Core MVC 应用程序的核心部分。</span><span class="sxs-lookup"><span data-stu-id="450f9-105">Controllers are a central part of any ASP.NET Core MVC application.</span></span> <span data-ttu-id="450f9-106">因此，应该对它们按应用计划表现有信心。</span><span class="sxs-lookup"><span data-stu-id="450f9-106">As such, you should have confidence they behave as intended for your app.</span></span> <span data-ttu-id="450f9-107">自动测试可以给你这种信心，还能在生成前检测错误。</span><span class="sxs-lookup"><span data-stu-id="450f9-107">Automated tests can provide you with this confidence and can detect errors before they reach production.</span></span> <span data-ttu-id="450f9-108">避免在控制器中安置不必要的职责并确保测试仅专注于控制器职责非常重要。</span><span class="sxs-lookup"><span data-stu-id="450f9-108">It's important to avoid placing unnecessary responsibilities within your controllers and ensure your tests focus only on controller responsibilities.</span></span>

<span data-ttu-id="450f9-109">控制器应采用最简单的逻辑，而不应关注业务逻辑或基础结构问题（例如数据访问）。</span><span class="sxs-lookup"><span data-stu-id="450f9-109">Controller logic should be minimal and not be focused on business logic or infrastructure concerns (for example, data access).</span></span> <span data-ttu-id="450f9-110">测试控制器逻辑，而不是框架。</span><span class="sxs-lookup"><span data-stu-id="450f9-110">Test controller logic, not the framework.</span></span> <span data-ttu-id="450f9-111">测试控制器基于有效或无效输入的行为。</span><span class="sxs-lookup"><span data-stu-id="450f9-111">Test how the controller *behaves* based on valid or invalid inputs.</span></span> <span data-ttu-id="450f9-112">测试控制器如何相应其所执行业务操作的结果。</span><span class="sxs-lookup"><span data-stu-id="450f9-112">Test controller responses based on the result of the business operation it performs.</span></span>

<span data-ttu-id="450f9-113">典型控制器职责：</span><span class="sxs-lookup"><span data-stu-id="450f9-113">Typical controller responsibilities:</span></span>

* <span data-ttu-id="450f9-114">验证 `ModelState.IsValid`。</span><span class="sxs-lookup"><span data-stu-id="450f9-114">Verify `ModelState.IsValid`.</span></span>
* <span data-ttu-id="450f9-115">如果 `ModelState` 无效，则返回错误响应。</span><span class="sxs-lookup"><span data-stu-id="450f9-115">Return an error response if `ModelState` is invalid.</span></span>
* <span data-ttu-id="450f9-116">从持久性检索业务实体。</span><span class="sxs-lookup"><span data-stu-id="450f9-116">Retrieve a business entity from persistence.</span></span>
* <span data-ttu-id="450f9-117">对业务实体执行操作。</span><span class="sxs-lookup"><span data-stu-id="450f9-117">Perform an action on the business entity.</span></span>
* <span data-ttu-id="450f9-118">将业务实体保存到持久性。</span><span class="sxs-lookup"><span data-stu-id="450f9-118">Save the business entity to persistence.</span></span>
* <span data-ttu-id="450f9-119">返回相应的 `IActionResult`。</span><span class="sxs-lookup"><span data-stu-id="450f9-119">Return an appropriate `IActionResult`.</span></span>

<span data-ttu-id="450f9-120">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="450f9-120">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="unit-tests-of-controller-logic"></a><span data-ttu-id="450f9-121">控制器逻辑的单元测试</span><span class="sxs-lookup"><span data-stu-id="450f9-121">Unit tests of controller logic</span></span>

<span data-ttu-id="450f9-122">[单元测试](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)涉及通过基础结构和依赖项单独测试应用的一部分。</span><span class="sxs-lookup"><span data-stu-id="450f9-122">[Unit tests](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) involve testing a part of an app in isolation from its infrastructure and dependencies.</span></span> <span data-ttu-id="450f9-123">单元测试控制器逻辑时，仅测试单个操作的内容，不测试其依赖项或框架自身的行为。</span><span class="sxs-lookup"><span data-stu-id="450f9-123">When unit testing controller logic, only the contents of a single action is tested, not the behavior of its dependencies or of the framework itself.</span></span> <span data-ttu-id="450f9-124">单元测试控制器操作时，请确保仅关注其行为。</span><span class="sxs-lookup"><span data-stu-id="450f9-124">As you unit test your controller actions, make sure you focus only on its behavior.</span></span> <span data-ttu-id="450f9-125">控制器单元测试将避开[筛选器](xref:mvc/controllers/filters)、[路由](xref:fundamentals/routing)或[模型绑定](xref:mvc/models/model-binding)等。</span><span class="sxs-lookup"><span data-stu-id="450f9-125">A controller unit test avoids things like [filters](xref:mvc/controllers/filters), [routing](xref:fundamentals/routing), or [model binding](xref:mvc/models/model-binding).</span></span> <span data-ttu-id="450f9-126">仅专注测试一项内容，单位测试通常编写简单、运行迅速。</span><span class="sxs-lookup"><span data-stu-id="450f9-126">By focusing on testing just one thing, unit tests are generally simple to write and quick to run.</span></span> <span data-ttu-id="450f9-127">正确编写的单位测试集无需过多开销即可经常运行。</span><span class="sxs-lookup"><span data-stu-id="450f9-127">A well-written set of unit tests can be run frequently without much overhead.</span></span> <span data-ttu-id="450f9-128">但单元测试不检测组件间交互的问题，[集成测试](xref:test/integration-tests)才会检测。</span><span class="sxs-lookup"><span data-stu-id="450f9-128">However, unit tests don't detect issues in the interaction between components, which is the purpose of [integration tests](xref:test/integration-tests).</span></span>

<span data-ttu-id="450f9-129">如果编写自定义筛选器和路由，应对其单独进行单元测试，而不是在测试特定控制器操作时进行。</span><span class="sxs-lookup"><span data-stu-id="450f9-129">If you're writing custom filters and routes, you should unit test them in isolation, not as part of your tests on a particular controller action.</span></span>

> [!TIP]
> <span data-ttu-id="450f9-130">[使用 Visual Studio 创建和运行单位测试](/visualstudio/test/unit-test-your-code)。</span><span class="sxs-lookup"><span data-stu-id="450f9-130">[Create and run unit tests with Visual Studio](/visualstudio/test/unit-test-your-code).</span></span>

<span data-ttu-id="450f9-131">若要演示单位测试，请查看以下控制器。</span><span class="sxs-lookup"><span data-stu-id="450f9-131">To demonstrate unit testing, review the following controller.</span></span> <span data-ttu-id="450f9-132">它显示集体讨论会话的列表并允许使用 POST 创建新的集体讨论会话：</span><span class="sxs-lookup"><span data-stu-id="450f9-132">It displays a list of brainstorming sessions and allows new brainstorming sessions to be created with a POST:</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/HomeController.cs?highlight=12,16,21,42,43)]

<span data-ttu-id="450f9-133">控制器遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)，需要依赖关系注入提供 `IBrainstormSessionRepository` 实例。</span><span class="sxs-lookup"><span data-stu-id="450f9-133">The controller is following the [explicit dependencies principle](http://deviq.com/explicit-dependencies-principle/), expecting dependency injection to provide it with an instance of `IBrainstormSessionRepository`.</span></span> <span data-ttu-id="450f9-134">因此使用 mock 对象框架（例如 [Moq](https://www.nuget.org/packages/Moq/)）进行测试很简单。</span><span class="sxs-lookup"><span data-stu-id="450f9-134">This makes it fairly easy to test using a mock object framework, like [Moq](https://www.nuget.org/packages/Moq/).</span></span> <span data-ttu-id="450f9-135">`HTTP GET Index` 方法没有循环或分支，且仅调用一个方法。</span><span class="sxs-lookup"><span data-stu-id="450f9-135">The `HTTP GET Index` method has no looping or branching and only calls one method.</span></span> <span data-ttu-id="450f9-136">若要测试此 `Index` 方法，我们需要验证返回了 `ViewResult`，附带来自存储库 `List` 方法的 `ViewModel`。</span><span class="sxs-lookup"><span data-stu-id="450f9-136">To test this `Index` method, we need to verify that a `ViewResult` is returned, with a `ViewModel` from the repository's `List` method.</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=17-18&range=1-33,76-95)]

<span data-ttu-id="450f9-137">`HomeController` `HTTP POST Index` 方法（如上所示）应该验证：</span><span class="sxs-lookup"><span data-stu-id="450f9-137">The `HomeController` `HTTP POST Index` method (shown above) should verify:</span></span>

* <span data-ttu-id="450f9-138">操作方法在 `ModelState.IsValid` 为 `false` 时返回有相应数据的错误请求 `ViewResult`。</span><span class="sxs-lookup"><span data-stu-id="450f9-138">The action method returns a Bad Request `ViewResult` with the appropriate data when `ModelState.IsValid` is `false`.</span></span>

* <span data-ttu-id="450f9-139">`ModelState.IsValid` 为 true 时，调用存储库上的 `Add` 方法并返回有正确参数的 `RedirectToActionResult`。</span><span class="sxs-lookup"><span data-stu-id="450f9-139">The `Add` method on the repository is called and a `RedirectToActionResult` is returned with the correct arguments when `ModelState.IsValid` is true.</span></span>

<span data-ttu-id="450f9-140">通过使用 `AddModelError` 添加错误，可以测试无效模型状态，如下第一个测试所示。</span><span class="sxs-lookup"><span data-stu-id="450f9-140">Invalid model state can be tested by adding errors using `AddModelError` as shown in the first test below.</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=8,15-16,37-39&range=35-75)]

<span data-ttu-id="450f9-141">第一个测试确认在 `ModelState` 无效时，返回与 `GET` 请求相同的 `ViewResult`。</span><span class="sxs-lookup"><span data-stu-id="450f9-141">The first test confirms when `ModelState` isn't valid, the same `ViewResult` is returned as for a `GET` request.</span></span> <span data-ttu-id="450f9-142">请注意，测试不会尝试传入无效模型。</span><span class="sxs-lookup"><span data-stu-id="450f9-142">Note that the test doesn't attempt to pass in an invalid model.</span></span> <span data-ttu-id="450f9-143">即使传入也无济于事，因为模型绑定不会运行（虽然[集成测试](xref:test/integration-tests)将使用练习模型绑定）。</span><span class="sxs-lookup"><span data-stu-id="450f9-143">That wouldn't work anyway since model binding isn't running (though an [integration test](xref:test/integration-tests) would use exercise model binding).</span></span> <span data-ttu-id="450f9-144">在本例中，不测试模型绑定。</span><span class="sxs-lookup"><span data-stu-id="450f9-144">In this case, model binding isn't being tested.</span></span> <span data-ttu-id="450f9-145">这些单位测试仅测试操作方法中代码的行为。</span><span class="sxs-lookup"><span data-stu-id="450f9-145">These unit tests are only testing what the code in the action method does.</span></span>

<span data-ttu-id="450f9-146">第二个测试验证 `ModelState` 有效时，（通过存储库）添加了新的 `BrainstormSession`，且该方法返回有所需属性的 `RedirectToActionResult`。</span><span class="sxs-lookup"><span data-stu-id="450f9-146">The second test verifies that when `ModelState` is valid, a new `BrainstormSession` is added (via the repository), and the method returns a `RedirectToActionResult` with the expected properties.</span></span> <span data-ttu-id="450f9-147">通常会忽略未调用的模拟调用，但在设置调用末尾调用 `Verifiable` 就可以在测试中对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="450f9-147">Mocked calls that aren't called are normally ignored, but calling `Verifiable` at the end of the setup call allows it to be verified in the test.</span></span> <span data-ttu-id="450f9-148">这通过对 `mockRepo.Verify` 的调用完成，进行这种调用时，如果未调用所需方法，则测试将失败。</span><span class="sxs-lookup"><span data-stu-id="450f9-148">This is done with the call to `mockRepo.Verify`, which will fail the test if the expected method wasn't called.</span></span>

> [!NOTE]
> <span data-ttu-id="450f9-149">通过此示例中使用的 Moq 库，可轻松混合可验证（或称“严格”）mock 和非可验证 mock（也称为“宽松”mock 或存根）。</span><span class="sxs-lookup"><span data-stu-id="450f9-149">The Moq library used in this sample makes it easy to mix verifiable, or "strict", mocks with non-verifiable mocks (also called "loose" mocks or stubs).</span></span> <span data-ttu-id="450f9-150">详细了解[使用 Moq 自定义 Mock 行为](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior)。</span><span class="sxs-lookup"><span data-stu-id="450f9-150">Learn more about [customizing Mock behavior with Moq](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior).</span></span>

<span data-ttu-id="450f9-151">应用中的另一个控制器显示与特定集体讨论会话相关的信息。</span><span class="sxs-lookup"><span data-stu-id="450f9-151">Another controller in the app displays information related to a particular brainstorming session.</span></span> <span data-ttu-id="450f9-152">它包括用于处理无效 ID 值的逻辑：</span><span class="sxs-lookup"><span data-stu-id="450f9-152">It includes some logic to deal with invalid id values:</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/SessionController.cs?highlight=19,20,21,22,25,26,27,28)]

<span data-ttu-id="450f9-153">控制器操作有三个要测试的事例，每个 `return` 语句对应一个：</span><span class="sxs-lookup"><span data-stu-id="450f9-153">The controller action has three cases to test, one for each `return` statement:</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/SessionControllerTests.cs?highlight=27,28,29,46,47,64,65,66,67,68)]

<span data-ttu-id="450f9-154">应用将功能公开为 Web API（与集体讨论会话相关的想法的列表，以及将新想法添加到会话的方法）：</span><span class="sxs-lookup"><span data-stu-id="450f9-154">The app exposes functionality as a web API (a list of ideas associated with a brainstorming session and a method for adding new ideas to a session):</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Api/IdeasController.cs?highlight=21,22,27,30,31,32,33,34,35,36,41,42,46,52,65)]

<span data-ttu-id="450f9-155">`ForSession` 方法返回 `IdeaDTO` 类型的列表。</span><span class="sxs-lookup"><span data-stu-id="450f9-155">The `ForSession` method returns a list of `IdeaDTO` types.</span></span> <span data-ttu-id="450f9-156">避免直接通过 API 调用返回业务域实体，因为它们常包含 API 客户端所需以外的数据，且它们会不必要地将应用的内部域模型与外部公开的 API 配对。</span><span class="sxs-lookup"><span data-stu-id="450f9-156">Avoid returning your business domain entities directly via API calls, since frequently they include more data than the API client requires, and they unnecessarily couple your app's internal domain model with the API you expose externally.</span></span> <span data-ttu-id="450f9-157">域实体和通过网络返回的类型之间的映射可以手动完成（使用 LINQ `Select`，如此处所示）或使用 [AutoMapper](https://github.com/AutoMapper/AutoMapper) 等库完成。</span><span class="sxs-lookup"><span data-stu-id="450f9-157">Mapping between domain entities and the types you will return over the wire can be done manually (using a LINQ `Select` as shown here) or using a library like [AutoMapper](https://github.com/AutoMapper/AutoMapper).</span></span>

<span data-ttu-id="450f9-158">`Create` 和 `ForSession` API 方法的单位测试：</span><span class="sxs-lookup"><span data-stu-id="450f9-158">The unit tests for the `Create` and `ForSession` API methods:</span></span>

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/ApiIdeasControllerTests.cs?highlight=18,23,29,33,38-39,43,50,58-59,68-70,76-78&range=1-83,121-135)]

<span data-ttu-id="450f9-159">如前所述，若要测试方法在 `ModelState` 无效时的行为，请在测试zho 将模型错误添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="450f9-159">As stated previously, to test the behavior of the method when `ModelState` is invalid, add a model error to the controller as part of the test.</span></span> <span data-ttu-id="450f9-160">请勿在单位测试中尝试测试模型有效性或模型绑定 - 仅测试操作方法在遇到特定 `ModelState` 值时的行为。</span><span class="sxs-lookup"><span data-stu-id="450f9-160">Don't try to test model validation or model binding in your unit tests - just test your action method's behavior when confronted with a particular `ModelState` value.</span></span>

<span data-ttu-id="450f9-161">第二个测试依赖存储库返回 null，所以 mock 存储库配置为返回 null。</span><span class="sxs-lookup"><span data-stu-id="450f9-161">The second test depends on the repository returning null, so the mock repository is configured to return null.</span></span> <span data-ttu-id="450f9-162">无需创建测试数据库（在内存中或其他位置）并构建将返回此结果的查询 - 它可以在单个语句中完成，如下所示。</span><span class="sxs-lookup"><span data-stu-id="450f9-162">There's no need to create a test database (in memory or otherwise) and construct a query that will return this result - it can be done in a single statement as shown.</span></span>

<span data-ttu-id="450f9-163">最后一个测试验证调用了存储库的 `Update` 方法。</span><span class="sxs-lookup"><span data-stu-id="450f9-163">The last test verifies that the repository's `Update` method is called.</span></span> <span data-ttu-id="450f9-164">正如我们之前所做，使用 `Verifiable` 调用 mock，然后调用模拟存储库的 `Verify` 方法，以确认执行了可验证方法。</span><span class="sxs-lookup"><span data-stu-id="450f9-164">As we did previously, the mock is called with `Verifiable` and then the mocked repository's `Verify` method is called to confirm the verifiable method was executed.</span></span> <span data-ttu-id="450f9-165">确保 `Update` 方法保存数据不是单位测试的职责，这可以通过集成测试完成。</span><span class="sxs-lookup"><span data-stu-id="450f9-165">It's not a unit test responsibility to ensure that the `Update` method saved the data; that can be done with an integration test.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="450f9-166">其他资源</span><span class="sxs-lookup"><span data-stu-id="450f9-166">Additional resources</span></span>

* <xref:test/integration-tests>
