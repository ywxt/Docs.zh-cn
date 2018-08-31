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
# <a name="test-controller-logic-in-aspnet-core"></a>ASP.NET Core 中的测试控制器逻辑

作者：[Steve Smith](https://ardalis.com/)

控制器是任意 ASP.NET Core MVC 应用程序的核心部分。 因此，应该对它们按应用计划表现有信心。 自动测试可以给你这种信心，还能在生成前检测错误。 避免在控制器中安置不必要的职责并确保测试仅专注于控制器职责非常重要。

控制器应采用最简单的逻辑，而不应关注业务逻辑或基础结构问题（例如数据访问）。 测试控制器逻辑，而不是框架。 测试控制器基于有效或无效输入的行为。 测试控制器如何相应其所执行业务操作的结果。

典型控制器职责：

* 验证 `ModelState.IsValid`。
* 如果 `ModelState` 无效，则返回错误响应。
* 从持久性检索业务实体。
* 对业务实体执行操作。
* 将业务实体保存到持久性。
* 返回相应的 `IActionResult`。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/testing/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="unit-tests-of-controller-logic"></a>控制器逻辑的单元测试

[单元测试](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)涉及通过基础结构和依赖项单独测试应用的一部分。 单元测试控制器逻辑时，仅测试单个操作的内容，不测试其依赖项或框架自身的行为。 单元测试控制器操作时，请确保仅关注其行为。 控制器单元测试将避开[筛选器](xref:mvc/controllers/filters)、[路由](xref:fundamentals/routing)或[模型绑定](xref:mvc/models/model-binding)等。 仅专注测试一项内容，单位测试通常编写简单、运行迅速。 正确编写的单位测试集无需过多开销即可经常运行。 但单元测试不检测组件间交互的问题，[集成测试](xref:test/integration-tests)才会检测。

如果编写自定义筛选器和路由，应对其单独进行单元测试，而不是在测试特定控制器操作时进行。

> [!TIP]
> [使用 Visual Studio 创建和运行单位测试](/visualstudio/test/unit-test-your-code)。

若要演示单位测试，请查看以下控制器。 它显示集体讨论会话的列表并允许使用 POST 创建新的集体讨论会话：

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/HomeController.cs?highlight=12,16,21,42,43)]

控制器遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)，需要依赖关系注入提供 `IBrainstormSessionRepository` 实例。 因此使用 mock 对象框架（例如 [Moq](https://www.nuget.org/packages/Moq/)）进行测试很简单。 `HTTP GET Index` 方法没有循环或分支，且仅调用一个方法。 若要测试此 `Index` 方法，我们需要验证返回了 `ViewResult`，附带来自存储库 `List` 方法的 `ViewModel`。

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=17-18&range=1-33,76-95)]

`HomeController` `HTTP POST Index` 方法（如上所示）应该验证：

* 操作方法在 `ModelState.IsValid` 为 `false` 时返回有相应数据的错误请求 `ViewResult`。

* `ModelState.IsValid` 为 true 时，调用存储库上的 `Add` 方法并返回有正确参数的 `RedirectToActionResult`。

通过使用 `AddModelError` 添加错误，可以测试无效模型状态，如下第一个测试所示。

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/HomeControllerTests.cs?highlight=8,15-16,37-39&range=35-75)]

第一个测试确认在 `ModelState` 无效时，返回与 `GET` 请求相同的 `ViewResult`。 请注意，测试不会尝试传入无效模型。 即使传入也无济于事，因为模型绑定不会运行（虽然[集成测试](xref:test/integration-tests)将使用练习模型绑定）。 在本例中，不测试模型绑定。 这些单位测试仅测试操作方法中代码的行为。

第二个测试验证 `ModelState` 有效时，（通过存储库）添加了新的 `BrainstormSession`，且该方法返回有所需属性的 `RedirectToActionResult`。 通常会忽略未调用的模拟调用，但在设置调用末尾调用 `Verifiable` 就可以在测试中对其进行验证。 这通过对 `mockRepo.Verify` 的调用完成，进行这种调用时，如果未调用所需方法，则测试将失败。

> [!NOTE]
> 通过此示例中使用的 Moq 库，可轻松混合可验证（或称“严格”）mock 和非可验证 mock（也称为“宽松”mock 或存根）。 详细了解[使用 Moq 自定义 Mock 行为](https://github.com/Moq/moq4/wiki/Quickstart#customizing-mock-behavior)。

应用中的另一个控制器显示与特定集体讨论会话相关的信息。 它包括用于处理无效 ID 值的逻辑：

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Controllers/SessionController.cs?highlight=19,20,21,22,25,26,27,28)]

控制器操作有三个要测试的事例，每个 `return` 语句对应一个：

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/SessionControllerTests.cs?highlight=27,28,29,46,47,64,65,66,67,68)]

应用将功能公开为 Web API（与集体讨论会话相关的想法的列表，以及将新想法添加到会话的方法）：

[!code-csharp[](testing/sample/TestingControllersSample/src/TestingControllersSample/Api/IdeasController.cs?highlight=21,22,27,30,31,32,33,34,35,36,41,42,46,52,65)]

`ForSession` 方法返回 `IdeaDTO` 类型的列表。 避免直接通过 API 调用返回业务域实体，因为它们常包含 API 客户端所需以外的数据，且它们会不必要地将应用的内部域模型与外部公开的 API 配对。 域实体和通过网络返回的类型之间的映射可以手动完成（使用 LINQ `Select`，如此处所示）或使用 [AutoMapper](https://github.com/AutoMapper/AutoMapper) 等库完成。

`Create` 和 `ForSession` API 方法的单位测试：

[!code-csharp[](testing/sample/TestingControllersSample/tests/TestingControllersSample.Tests/UnitTests/ApiIdeasControllerTests.cs?highlight=18,23,29,33,38-39,43,50,58-59,68-70,76-78&range=1-83,121-135)]

如前所述，若要测试方法在 `ModelState` 无效时的行为，请在测试zho 将模型错误添加到控制器。 请勿在单位测试中尝试测试模型有效性或模型绑定 - 仅测试操作方法在遇到特定 `ModelState` 值时的行为。

第二个测试依赖存储库返回 null，所以 mock 存储库配置为返回 null。 无需创建测试数据库（在内存中或其他位置）并构建将返回此结果的查询 - 它可以在单个语句中完成，如下所示。

最后一个测试验证调用了存储库的 `Update` 方法。 正如我们之前所做，使用 `Verifiable` 调用 mock，然后调用模拟存储库的 `Verify` 方法，以确认执行了可验证方法。 确保 `Update` 方法保存数据不是单位测试的职责，这可以通过集成测试完成。

## <a name="additional-resources"></a>其他资源

* <xref:test/integration-tests>
