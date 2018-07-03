---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |Microsoft Docs
author: microsoft
description: 步骤 12 显示了如何开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 0d7986bcff7a0ddc89d40c3c03eb4ebb26a8b230
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402478"
---
<a name="enable-automated-unit-testing"></a>启用自动单元测试
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 12 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 12 显示了如何开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改和对应用程序在将来的改进。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner 步骤 12： 单元测试

让我们来开发一套自动化的单元测试用于验证我们 NerdDinner 的功能，而且这将向我们提供的置信度进行更改和对应用程序在将来的改进。

### <a name="why-unit-test"></a>为什么单元测试？

在工作一天早上的驱动器上可以启发您正在使用的应用程序突然立刻正式投入工作。 您意识到可以实现的更改，可让应用程序极大的改进。 它可能是一个重构的清理代码中，添加一个新功能或修复 bug。

Confronts，当您在您的计算机的问题-"安全是它，使这一改进？" 如果在更改具有副作用或中断的内容？ 更改可能很简单，只需几分钟才能实现，但如果需要手动测试的应用程序方案的所有小时？ 如果忘记方案和损坏的应用程序进入成品阶段？ 正在进行此项改进真的值得下的所有工作？

自动化的单元测试可以提供网络安全，使您能够不断改进您的应用程序，并避免害怕正在处理的代码。 具有自动快速验证功能，可以使用置信度 – 代码，使您可以进行改进可能否则不具有的感觉舒适的测试执行。 它们还帮助创建更易于维护的解决方案，并让较长的生存期的到高得多的潜在客户的投资回报。

ASP.NET MVC 框架可以简单而自然到单元测试应用程序功能。 它还使支持测试优先的基于的开发的测试驱动开发 (TDD) 工作流。

### <a name="nerddinnertests-project"></a>NerdDinner.Tests 项目

我们在本教程开头创建了 NerdDinner 应用程序，我们已收到一个提示对话框询问我们是否想要创建单元测试项目随附的应用程序项目：

![](enable-automated-unit-testing/_static/image1.png)

我们保留"是的创建单元测试项目"单选按钮处于选中状态 – 这将导致"NerdDinner.Tests"项目添加到我们的解决方案：

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Tests 项目引用 NerdDinner 应用程序项目程序集，并使我们能够轻松地将自动的测试添加到其验证应用程序功能。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>为我们 Dinner Model 类创建单元测试

让我们将一些测试添加到验证我们创建当我们构建我们的模型层的 Dinner 类我们 NerdDinner.Tests 项目。

我们将首先创建模型相关的测试，我们将放置我们名为"Models"的测试项目的新文件夹。 我们然后右键单击文件夹并选择**Add-&gt;新的测试**菜单命令。 这将显示"添加新测试"对话框。

我们将选择要创建一个"单元测试"并将其命名为"DinnerTest.cs":

![](enable-automated-unit-testing/_static/image3.png)

当我们单击"确定"按钮时 Visual Studio 将添加 （和打开） DinnerTest.cs 文件到项目：

![](enable-automated-unit-testing/_static/image4.png)

默认 Visual Studio 单元测试模板有大量的样板代码在其中找到略为凌乱。 让我们把它整理出来以只包含以下代码：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

在上面的 DinnerTest 类 [TestClass] 属性将其识别为测试，以及可选的测试初始化和拆卸代码将包含的类。 我们可以通过添加 [TestMethod] 特性对它们的公共方法来定义在其中测试。

下面是我们将添加的两个执行我们的 Dinner 类测试的第一个。 第一个测试将验证我们 Dinner 无效，是否创建新的 Dinner 时没有正确设置所有属性。 第二个测试验证我们 Dinner Dinner 具有所有属性都设置使用有效的值时有效：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

您会注意到上面我们测试名称都是非常明确的 （并且却稍微有些繁琐的）。 因为我们最终可能会创建数百或数千个小测试，并且我们想要轻松地快速确定意向和每个行为 （尤其是在我们正在通过测试运行程序中的失败的列表），我们将执行此操作。 测试名称应以命名要测试的功能。 我们使用更高版本"名词\_应\_谓词"命名模式。

我们构建的测试使用测试模式 –"Arrange，Act，Assert"代表"AAA":

- 排列： 设置要测试的单元
- Act： 执行测试的单元，并捕获结果
- 断言： 验证行为

当我们编写时我们想要避免的各个测试的测试执行过多操作。 而是每个测试应验证仅在一个概念 （这将使其更易于找出失败的原因）。 比较好的原则是尝试，且只能包含一个断言语句为每个测试。 如果你有多个断言测试方法中的语句，请确保它们都被用于测试相同的概念。 如有疑问，请另一个测试。

### <a name="running-tests"></a>正在运行测试

Visual Studio 2008 Professional （和更高版本） 包括可用于运行 Visual Studio 单元测试项目在 IDE 中的内置测试运行程序。 我们可以选择**测试-&gt;运行-&gt;解决方案中的所有测试**菜单命令 （或类型 Ctrl R、 A） 若要运行所有单元测试。 或或者我们可以在特定的测试类或测试方法中我们光标的位置，并使用**测试-&gt;运行-&gt;当前上下文中的测试**菜单命令 （或类型 Ctrl R、 T） 运行的单元测试的子集。

让我们 DinnerTest 类中的我们光标的位置并键入"Ctrl R、 T"到我们刚才定义的运行这两个测试。 当我们执行此操作的"测试结果"窗口将显示在 Visual Studio 中，我们将看到我们测试运行中列出的结果：

![](enable-automated-unit-testing/_static/image5.png)

*注意： VS 测试结果窗口不默认情况下显示的类名称列。可以通过在测试结果窗口内右键单击并使用添加/删除列菜单命令添加此。*

我们的两个测试中花费了只有一小部分第二个运行，并为您可以在这两种传递，请参阅。 我们现在可以继续并通过它们来创建其他测试，验证特定的规则验证，以及涵盖两个帮助器方法-IsUserHost() 和 IsUserRegisterd() – 我们添加到 Dinner 类扩充。 将所有这些测试放在 Dinner 类的位置将使其更容易且更安全，若要向其在将来添加新的业务规则和验证。 我们可以将我们新的规则逻辑添加到 Dinner，然后秒内验证它没有破坏任何我们以前的逻辑功能。

请注意如何使用描述性的测试名称轻松地快速了解每个测试验证。 我建议使用**工具-&gt;选项**菜单命令，打开的测试工具-&gt;测试执行配置屏幕中，并检查"双击已失败或无结论的单元测试结果显示测试失败的点"复选框。 这样，您可以双击测试结果窗口中的故障，立即跳转到断言失败。

### <a name="creating-dinnerscontroller-unit-tests"></a>创建 DinnersController 的单元测试

让我们现在创建验证我们 DinnersController 的功能的一些单元测试。 我们将首先右键单击测试项目中的"控制器"文件夹，然后选择**Add-&gt;新的测试**菜单命令。 我们将创建一个"单元测试"并将其命名为"DinnersControllerTest.cs"。

我们将创建两个验证 DinnersController 的 Details() 操作方法的测试方法。 第一个将验证现有 Dinner 请求时，返回一个视图。 第二个将验证不存在 Dinner 请求时，返回"NotFound"视图：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上面的代码将编译成清理。 当我们运行测试时，不过，它们都失败：

![](enable-automated-unit-testing/_static/image6.png)

如果我们看一下错误消息，我们会看到测试失败的原因是因为我们 DinnersRepository 类无法连接到数据库。 我们 NerdDinner 应用程序到本地 SQL Server Express 文件存在于 \App 下使用连接字符串\_NerdDinner 应用程序项目的数据目录。 因为我们 NerdDinner.Tests 项目编译和运行在不同的目录中然后应用程序项目，我们连接字符串的相对路径位置不正确。

我们*无法*通过将 SQL Express 数据库文件复制到我们的测试项目，修复此问题，然后向其中添加了适当测试的连接字符串，我们的测试项目的 App.config 中。 此参数将被解除阻止，并运行上述测试。

单元测试代码中使用的实际数据库，不过，带来了许多挑战。 尤其是在下列情况下：

- 会显著降低的单元测试执行时间。 它所花费的时间来运行测试，频繁地执行它们的可能性越小。 理想情况下，您希望单元测试，以能够在数秒内 – 运行并将其作为内容的自然作为编译项目。
- 在测试中的设置和清理逻辑比较复杂。 您希望每个单元测试是独立的、 独立于其他人 （不带任何副作用或依赖项）。 实际数据库上运行时需要注意的状态和测试之间将它重置。

让我们看一下名为"依赖关系注入"，可帮助我们解决这些问题，并避免与我们的测试中使用的实际数据库的需求的设计模式。

### <a name="dependency-injection"></a>依赖关系注入

稍后再试 DinnersController"与紧密耦合"DinnerRepository 类。 "耦合"是指在其中一个类显式依赖于另一个类才能正常工作的情况：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

由于 DinnerRepository 类需要对数据库的访问，紧密耦合的依赖关系 DinnersController 类具有 DinnerRepository 两端需要我们要测试的 DinnersController 操作方法的顺序中有一个数据库。

通过使用称为"依赖关系注入"– 这是一种方法在其中依赖项 （如提供数据访问的存储库类） 不再隐式创建中使用它们的类的设计模式，我们可以获得解决此问题。 而是依赖项可以显式传递给使用它们的类使用构造函数自变量。 如果使用接口定义了依赖项，然后，我们可以灵活地在单元测试方案的"假"的依赖项实现中传递。 这让我们来创建实际上并不要求对数据库的访问的特定于测试的依赖项实现。

若要了解此操作，让我们来实现与我们 DinnersController 的依赖关系注入。

#### <a name="extracting-an-idinnerrepository-interface"></a>提取 IDinnerRepository 接口

我们第一步将创建新的 IDinnerRepository 接口封装我们控制器要求以检索和更新 Dinners 的存储库协定。

我们可以通过右键单击 \Models 文件夹，然后选择手动定义此接口协定**Add-&gt;新项**菜单命令，并创建名为 IDinnerRepository.cs 新接口。

或者我们可以使用重构工具内置于 Visual Studio Professional （和更高版本） 自动提取，并为我们创建一个接口，从我们现有的 DinnerRepository 类。 若要提取使用与此接口，只需将光标置于 DinnerRepository 类中，在文本编辑器，然后右键单击并选择**重构-&gt;提取接口**菜单命令：

![](enable-automated-unit-testing/_static/image7.png)

这将启动"提取接口"对话框并提示我们输入要创建的接口的名称。 它将默认为 IDinnerRepository 并自动选择要添加到接口的现有 DinnerRepository 类上的所有公共方法：

![](enable-automated-unit-testing/_static/image8.png)

当我们单击"确定"按钮时，Visual Studio 会将新 IDinnerRepository 接口添加到我们的应用程序：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

并将更新我们现有的 DinnerRepository 类，以便它实现该接口：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>正在更新 DinnersController 以支持构造函数注入

现在，我们将更新要使用的新界面的 DinnersController 类。

当前 DinnersController 已经过硬编码，以便其"dinnerRepository"字段始终是 DinnerRepository 类：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

我们将更改它，以便"dinnerRepository"字段的类型而不是 DinnerRepository IDinnerRepository 是。 然后，我们将添加两个公共 DinnersController 构造函数。 一个构造函数允许将 IDinnerRepository 作为参数传递。 另一个是使用我们现有的 DinnerRepository 实现的默认构造函数：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

由于默认情况下的 ASP.NET MVC 创建控制器类使用默认构造函数，在运行时我们 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。

我们现在可以更新单元测试，不过，在"假"dinner 存储库实现中使用参数的构造函数传递。 此"假"dinner 存储库将不需要访问的实际数据库，而将使用内存中示例数据。

#### <a name="creating-the-fakedinnerrepository-class"></a>创建 FakeDinnerRepository 类

让我们创建 FakeDinnerRepository 类。

我们将首先创建我们 NerdDinner.Tests 项目中的"Fakes"目录，然后向其中添加新的 FakeDinnerRepository 类 (右键单击文件夹并选择**Add-&gt;的新类**):

![](enable-automated-unit-testing/_static/image9.png)

我们将更新代码，以便 FakeDinnerRepository 类实现 IDinnerRepository 接口。 然后，我们可以右键单击它，并选择"实现接口 IDinnerRepository"上下文菜单命令：

![](enable-automated-unit-testing/_static/image10.png)

这会导致 Visual Studio 会自动将所有 IDinnerRepository 接口成员添加到"存根"的默认实现我们 FakeDinnerRepository 类：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

我们然后可以更新 FakeDinnerRepository 实现，以便从内存中列表&lt;Dinner&gt;集合作为构造函数参数传递给它：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

现在，我们不需要数据库，并且可以改为脱离 Dinner 对象的内存中列表的虚设 IDinnerRepository 实现。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>对单元测试使用 FakeDinnerRepository

让我们返回到之前失败，因为该数据库不可用的 DinnersController 单元测试。 我们可以更新测试方法，用于填充向 DinnersController 使用下面的代码示例中内存 Dinner 数据 FakeDinnerRepository:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

和现在当我们运行这些测试都通过：

![](enable-automated-unit-testing/_static/image11.png)

最重要的是，它们需要只有一小部分第二个运行，并且不需要任何复杂的安装程序清理逻辑。 我们可以现在单元测试所有我们 DinnersController 操作方法的代码 （包括列表中，分页的详细信息，创建、 更新和删除），而根本无需连接到真实的数据库。

| **端主题： 依赖关系注入框架** |
| --- |
| 执行手动依赖关系注入 （例如，我们是上面） 可正常使用，但会变成难以维护作为依赖项的数量并提高应用程序中的组件。 为有助于提供更多的依赖关系管理灵活性的.NET 而存在多个依赖关系注入框架。 这些框架，有时也称为"控制反转"(IoC) 容器，提供机制，以使一层额外的配置对指定并将依赖项传递给对象在运行时 （通常使用构造函数注入的支持). 一些更受欢迎的 OSS 依赖关系注入 / IOC 框架在.NET 中的包括： AutoFac、 Ninject、 Spring.NET、 StructureMap 和 Windsor。 ASP.NET MVC 公开扩展性 Api，允许开发人员参与的解决方法和实例化控制器，并可让依赖关系注入 / IoC 框架完全集成此进程中。 使用 DI/IOC 框架还会使我们能够从我们 DinnersController – 将完全删除它和 DinnerRepositorys 之间的耦合删除默认构造函数。 我们不会使用依赖关系注入 / IOC 框架与 NerdDinner 应用程序。 但是，这是一个我们可以考虑在将来，如果 NerdDinner 基本代码和功能的大小增长。 |

### <a name="creating-edit-action-unit-tests"></a>创建编辑操作单元测试

让我们现在创建一些单元测试以确认 DinnersController 的编辑功能。 我们首先测试我们的编辑操作的 HTTP GET 版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

我们将创建一个测试，以便验证时请求有效 dinner 呈现由 DinnerFormViewModel 对象支持的视图：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

当我们运行测试时，不过，我们会发现失败，因为时编辑方法访问 User.Identity.Name 属性执行 Dinner.IsHostedBy() 检查将引发空引用异常。

控制器基类上的用户对象封装有关登录的用户的详细信息，并在运行时创建控制器时，由 ASP.NET MVC 填充。 因为我们要测试 web 服务器环境外部 DinnersController，未设置用户对象 （因此导致 null 引用异常）。

### <a name="mocking-the-useridentityname-property"></a>模拟 User.Identity.Name 属性

模拟框架使测试变得更容易通过使我们能够动态创建虚设支持我们的测试中的依赖对象的版本。 例如，我们可以在我们的编辑操作测试使用的模拟框架，动态创建我们 DinnersController 可用于查找模拟的用户名的用户对象。 这可以避免当我们运行测试时引发空引用。

有很多.NET 模拟可与 ASP.NET MVC 框架 (见下面这些设置的列表： [ http://www.mockframeworks.com/ ](http://www.mockframeworks.com/))。 为了测试我们将使用一种开放源模拟框架名为"Moq"我们 NerdDinner 应用程序，这可以免费从下载[ http://www.mockframeworks.com/moq ](http://www.mockframeworks.com/moq)。

下载完成后，我们将对 Moq.dll 程序集 NerdDinner.Tests 项目中添加的引用：

![](enable-automated-unit-testing/_static/image12.png)

然后，我们将添加一个"CreateDinnersControllerAs(username)"帮助器方法为我们的测试类的用户名将作为参数，哪些则"模拟"DinnersController 实例上的 User.Identity.Name 属性：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

更高版本，我们将使用 Moq 创建 fakes 的 ControllerContext 对象 （这是什么 ASP.NET MVC 将传递到控制器类，以公开运行时对象，如用户、 请求、 响应和会话） 的模拟对象。 我们在模拟来指示的 ControllerContext HttpContext.User.Identity.Name 属性应返回我们传递给帮助器方法的用户名字符串上调用"SetupGet"方法。

我们可以模拟任意数量的 ControllerContext 属性和方法。 为了说明这一点我还添加了 SetupGet() 调用 Request.IsAuthenticated 属性 （这不实际所需的下面 – 的测试，但这有助于解释如何可以模拟请求属性）。 当我们完成我们的 ControllerContext 模拟的一个实例分配向 DinnersController 我们帮助器方法返回。

我们现在可以编写使用此帮助器方法来测试编辑方案涉及不同的用户的单元测试：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

现在当我们运行测试时传递：

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>测试 UpdateModel() 方案

我们创建了测试以涵盖编辑操作的 HTTP GET 版本。 让我们现在创建某些编辑操作的 HTTP POST 版本验证测试：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

有关我们支持与此操作方法的有趣的新测试方案是控制器基类上的 UpdateModel() 帮助器方法的用法。 我们将使用此帮助器方法来将窗体发布值绑定到 Dinner 对象实例。

下面是演示，我们可以如何提供窗体发布 UpdateModel() 帮助器方法，若要使用的值的两个测试。 我们将通过创建和填充 FormCollection 对象执行此操作，然后将其分配给在控制器上的"ValueProvider"属性。

第一个测试验证，成功保存将浏览器重定向到详细信息的操作。 第二个测试将验证发送无效的输入时该操作显示编辑视图再次使用一条错误消息。


[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>测试总结

我们已经介绍了在单元测试控制器类中所涉及的核心概念。 我们可以使用这些技术可以轻松地创建数百个简单的测试，验证我们的应用程序的行为。

我们的控制器和模型的测试不需要的实际数据库，因为它们是极其快速且轻松地运行。 我们将能够在数秒内，执行数百个自动测试并立即获取我们所做的更改是否中断的内容的反馈。 这将有助于向我们提供的置信度来持续改进，重构，并改进我们的应用程序。

我们介绍如何测试作为最后一个主题中这一章 – 但不是因为测试是应在开发过程结束时执行 ！ 相反，应在开发过程中尽早编写自动的测试。 这样做因此可以立即获得反馈开发时，可帮助你仔细考虑应用程序的用例场景，并会引导您设计应用程序分层和记住耦合干净。

本书中的更高版本的章节将讨论测试驱动开发 (TDD) 以及如何使用 ASP.NET MVC。 首先编写的测试，都能满足你生成的代码，TDD 也迭代的编码实践。 与 TDD 开始每项功能通过创建一个测试，以便验证您将要实现的功能。 编写单元测试第一次可帮助确保你清楚地了解此功能，如何它应该适用。 仅编写该测试 （并已验证它失败后） 然后实现此测试将验证的实际功能。 因为您已经花了时间思考的功能是怎样工作的用例，你将具有更好地了解要求和如何最好地实现它们。 完成您可以重新运行测试 – 并立即获得反馈的实现时是否功能能够正常运行。 我们将介绍第 10 章中更 TDD。

### <a name="next-step"></a>下一步

一些最后一个注释总结。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)
