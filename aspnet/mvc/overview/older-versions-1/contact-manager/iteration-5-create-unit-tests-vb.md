---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 迭代 5 — 创建单元测试 (VB) |Microsoft Docs
author: microsoft
description: 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类和构建 o 的单元测试...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: 6aee4c01c1555dd2ea95d26a005d61ddab09f6fe
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831849"
---
<a name="iteration-5--create-unit-tests-vb"></a>迭代 5 — 创建单元测试 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1-创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3-添加窗体验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4-使应用程序松散耦合。 在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6-使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7-添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。


## <a name="this-iteration"></a>此迭代

上一次迭代中的联系人管理器应用程序，我们可以重构要更为松散耦合的应用程序。 我们分隔到不同的控制器、 服务和存储库层应用程序。 与通过接口在它下面的层交互，每个层。

我们重构应用程序，以便更轻松地监视和修改应用程序。 例如，如果我们需要使用新的数据访问技术，我们只需可以直接更改存储库层，而无需涉及控制器或服务层。 松散耦合，联系人管理器发出我们进行了应用程序更具弹性，若要更改。

但是，当我们需要将一项新功能添加到联系人管理器应用程序时，会发生什么情况？ 或者，当我们修复 bug 时，会发生什么情况？ 编写代码的一个很遗憾，但也经实践证明的事实是，每当改动代码创建引入新 bug 的风险。

例如，一个的最好时期，你的经理可能会要求你添加到联系人管理器中的一项新功能。 她希望您将添加对联系人组的支持。 她希望您为了使用户能够将其联系人组织成组如朋友、 业务和等等。

为了实现这一新功能，您将需要修改的联系人管理器应用程序的所有三个层。 你将需要将新功能添加到服务层，并在存储库的所有控制器。 一旦您开始修改代码，则可能会破坏正常运行过的功能。

正如我们在上一次迭代，做重构到不同的层，我们的应用程序是一件好事。 它是一件好事，因为它使我们能够对整个层进行更改，无需接触应用程序的其余部分。 但是，如果你想要使在层内的代码更易于维护和修改，则需要创建单元测试的代码。

你使用单元测试来测试单个代码单元。 这些单位代码是小于整个应用程序层。 通常情况下，您可以使用单元测试以验证你的代码中的特定方法的行为是否在预期的方式。 例如，将创建由 ContactManagerService 类公开的 CreateContact() 方法的单元测试。

只是应用程序工作的单元测试，如网络安全。 每当修改代码的应用程序，可以运行单元测试，以检查是否修改中断现有功能的一组。 单元测试使您的代码安全地修改。 单元测试的所有代码中进行应用程序更具弹性，若要更改。

在此迭代中，我们将单元测试添加到我们的联系人管理器应用程序。 这样一来，在下一个迭代中，我们可以添加联系人组对我们的应用程序而无需担心破坏现有功能。

> [!NOTE] 
> 
> 多种测试框架，包括 NUnit 和 xUnit.net，MbUnit 的单元。 在本教程中，我们使用的单元测试框架与 Visual Studio 附带。 但是，您可以轻松地使用其中一种替代框架。


## <a name="what-gets-tested"></a>获取测试内容

在理想情况下，所有代码将包含一些单元测试。 在理想情况下，您必须完美的网络安全。 您可以修改应用程序中代码的任何行，并就可马上知道，通过执行单元测试，是否更改中断了现有功能。

但是，我们并不完美的世界中的实时 t。 在实践中，编写单元测试时，您专注于编写您的业务逻辑 （例如，验证逻辑） 的测试。 具体而言，你*不这样做*编写单元测试为你的数据访问逻辑或视图逻辑。

若要很有用，单元测试必须执行非常快速地。 您轻松地可能会累积 （成百上千台） 的应用程序的单元测试。 如果单元测试可能需要很长时间才能运行您要防止执行它们。 换而言之，长时间运行的单元测试是无用的日常编码用途。

出于此原因，您通常做不编写与数据库交互的代码的单元测试。 针对实时数据库运行数百个单元测试会太慢。 不过，您可以模拟你的数据库，编写与 （我们讨论模拟以下数据库） 的模拟数据库交互的代码。

出于类似原因，您通常不写入视图的单元测试。 若要测试一个视图，必须启动 web 服务器。 由于启动 web 服务器是一个相对较慢的过程，不建议创建单元测试您的视图。

如果您的视图包含复杂的逻辑则应考虑将逻辑移到帮助程序方法。 您可以编写单元测试的执行而无需启动 web 服务器的帮助器方法。

> [!NOTE] 
> 
> 虽然编写测试的数据访问逻辑或视图逻辑不是一个不错的主意，编写单元测试时，这些测试可能会非常有价值，构建功能或集成测试时。


> [!NOTE] 
> 
> ASP.NET MVC 是 Web 窗体视图引擎。 Web 窗体视图引擎依赖于 web 服务器时，可能不是其他视图引擎。


## <a name="using-a-mock-object-framework"></a>使用模拟对象框架

在生成单元测试时，几乎总是需要利用的模拟对象框架。 模拟对象框架，可在应用程序中创建模拟和存根 （stub） 的类。

例如，可以使用模拟对象框架来生成你的存储库类的模型版本。 这样一来，您可以使用模拟存储库类而不是实际的存储库类在单元测试中。 使用模拟的存储库，可避免执行数据库的代码执行单元测试时。

Visual Studio 不会包含模拟对象框架。 但是，有可用于.NET framework 的多个商业和开源模拟对象框架：

1. Moq-此框架是开放源 BSD 许可下提供。 您可以下载从 Moq [ https://code.google.com/p/moq/ ](https://code.google.com/p/moq/)。
2. Rhino Mocks-此框架是开放源 BSD 许可下提供。 您可以下载从 Rhino Mocks [ http://ayende.com/projects/rhino-mocks.aspx ](http://ayende.com/projects/rhino-mocks.aspx)。
3. Typemock Isolator-这是一个商业的框架。 您可以下载从试用版[ http://www.typemock.com/ ](http://www.typemock.com/)。

在本教程中，我决定使用 Moq。 但是，您可以轻松地使用 Rhino Mocks 或 Typemock Isolator 创建 Mock 对象为联系人管理器应用程序。

可以使用 Moq 之前，需要完成以下步骤：

1. .
2. 解压缩下载之前，请确保右键单击该文件，并单击标记的按钮**解除阻止**（参见图 1）。
3. 解压缩下载。
4. 通过选择菜单选项将 Moq 程序集的引用添加到你的测试项目**项目中，添加引用**以打开**添加引用**对话框。 在浏览选项卡，浏览到你在其中解压缩 Moq 文件夹并选择 Moq.dll 程序集。 单击**确定**按钮 （请参见图 2）。


[![取消阻塞 Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**图 01**： 取消阻塞 Moq ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image2.png))


[![添加 Moq 后引用](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**图 02**： 添加 Moq 后的引用 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image4.png))


## <a name="creating-unit-tests-for-the-service-layer"></a>为服务层创建单元测试

让我们来首先创建一组我们联系人管理器应用程序 s 的服务层的单元测试。 我们将使用这些测试来验证我们的验证逻辑。

创建 ContactManager.Tests 项目中名为 Models 的新文件夹。 接下来，右键单击模型文件夹并选择**添加、 新测试**。 **添加新测试**此时将显示图 3 所示的对话框。 选择**单元测试**模板并命名新测试 ContactManagerServiceTest.vb。 单击**确定**按钮将新测试添加到测试项目。

> [!NOTE] 
> 
> 一般情况下，所需测试项目以匹配你的 ASP.NET MVC 项目的文件夹结构的文件夹的结构。 例如，您将测试控制器放置在控制器文件夹中，在模型文件夹中，模型测试等。


[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**图 03**: Models\ContactManagerServiceTest.cs ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image6.png))


最初，我们想要测试由 ContactManagerService 类公开的 CreateContact() 方法。 我们将创建以下五个测试：

- CreateContact()-向方法传递了有效的联系人时，测试该 CreateContact() 返回值 true。
- CreateContactRequiredFirstName()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时缺少的名字的联系人。
- CreateContactRequredLastName()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时缺少姓氏的联系人。
- CreateContactInvalidPhone()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时的联系人电话号码无效。
- CreateContactInvalidEmail()-测试，将一条错误消息添加到模型状态无效的电子邮件地址的联系人时传递给 CreateContact() 方法...

第一个测试验证了有效的联系人不会生成验证错误。 剩余测试检查每个验证规则。

对于这些测试的代码包含在列表 1 中。

**Listing 1 - Models\ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]


由于我们在列表 1 中使用 Contact 类，我们需要将对 Microsoft 实体框架的引用添加到我们的测试项目。 添加对 system.data.entity 的引用程序集的引用。


代码清单 1 包含一个名为使用 [TestInitialize] 特性修饰的 initialize （） 方法。 每个单元测试运行之前自动调用此方法 （它每个单元测试前调用 5 次）。 使用以下代码行，initialize （） 方法创建 mock 存储库：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

这行代码使用 Moq 框架来生成从 IContactManagerRepository 接口的 mock 存储库。 Mock 存储库而不是实际 EntityContactManagerRepository 用于避免在每个单元测试运行时访问数据库。 Mock 存储库实现 IContactManagerRepository 接口的方法，但方法 don t 实际执行任何操作。

> [!NOTE] 
> 
> 使用 Moq 框架时，会区分\_mockRepository 和\_mockRepository.Object。 前者是指包含用于指定模拟存储库的行为方式的方法的模拟 (的 IContactManagerRepository) 类。 后者是指实际的 mock 存储库，实现 IContactManagerRepository 接口。


创建 ContactManagerService 类的实例时，将在 initialize （） 方法中使用模拟的存储库。 所有的各个单元测试使用 ContactManagerService 类的此实例。

代码清单 1 包含五个方法对应于每个单元测试。 每种方法是使用 [TestMethod] 特性修饰。 当您运行单元测试时，被调用具有此属性的任何方法。 换而言之，任何使用 [TestMethod] 特性修饰的方法是单元测试。

第一个单元测试，名为 CreateContact()，验证，有效 Contact 类的实例传递给方法时，调用 CreateContact() 返回值 true。 测试创建 Contact 类的实例，调用 CreateContact() 方法，并验证 CreateContact() 返回值 true。

剩余测试验证，当使用无效的联系人调用 CreateContact() 方法然后方法返回 false，预期的验证错误消息添加到模型状态。 例如，CreateContactRequiredFirstName() 测试与空字符串作为其 FirstName 属性创建联系人类的实例。 接下来，使用无效的联系人调用 CreateContact() 方法。 最后，此测试将验证 CreateContact() 返回 false，并且模型状态包含预期的验证错误消息"名字是必填。"

可以通过选择菜单选项在列表 1 中运行单元测试**测试，运行，解决方案 （CTRL + R、 A） 中的所有测试**。 在测试结果窗口中显示测试结果 （请参阅图 4）。


[![测试结果](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**图 04**： 测试结果 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image8.png))


## <a name="creating-unit-tests-for-controllers"></a>为控制器创建单元测试

ASP.NET MVC 应用程序控制流的用户交互。 当测试控制器时，你想要测试是否将控制器返回正确的操作结果和查看数据。 此外可能想要测试是否与预期的方式中的模型类交互，一个控制器。

例如，代码清单 2 包含联系人控制器 create （） 方法的两个单元测试。 第一个单元测试验证了有效的联系人传递给 create （） 方法，则 create （） 方法将重定向到的索引操作时。 换而言之，当传递了有效的联系人，create （） 方法应返回表示索引操作 RedirectToRouteResult。

我们不想测试 ContactManager 服务层，我们将测试控制器层时。 因此，我们模拟服务层提供的 Initialize 方法中的以下代码：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

在 CreateValidContact() 单元测试中，我们模拟调用服务层具有以下代码行 CreateContact() 方法的行为：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

这行代码会导致模拟的 ContactManager 服务，以调用其 CreateContact() 方法返回的值为 true。 由模拟服务层，我们可以测试控制器的行为而无需执行的服务层中的任何代码。

第二个单元测试验证无效联系人传递给方法时，create （） 操作，返回创建视图。 我们会导致服务层 CreateContact() 方法返回值 false，使用以下代码行：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

如果 create （） 方法的行为我们预期它应在服务层，则返回值 false 时返回创建视图。 这样一来，控制器可以显示验证错误消息，在创建视图和用户有机会更正该无效联系人属性。


如果您计划生成你的控制器的单元测试然后您需要的控制器操作返回显式视图名称。 例如，不返回此类的视图：

返回 View()

改为返回的视图如下：

返回 View("Create")

如果不能显式返回视图时 ViewResult.ViewName 属性将返回空字符串。


**Listing 2 - Controllers\ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>总结

在此迭代中，我们为我们的联系人管理器应用程序创建单元测试。 若要验证我们的应用程序仍行为我们预期的方式在任何时候，我们可以运行这些单元测试。 单元测试作为使应用程序，使我们能够安全地修改我们的应用程序在将来的安全网。

我们创建了两个集的单元测试。 首先，我们通过创建我们的服务层的单元测试来测试我们的验证逻辑。 接下来，我们通过创建我们的控制器层的单元测试来测试我们的流控制逻辑。 当测试我们的服务层，我们独立的我们的测试为我们的服务层从我们的存储库层通过模拟我们存储库层。 当测试控制器层，我们独立的我们的测试我们控制器层由模拟服务层。

在下一个迭代中，我们将修改联系人管理器应用程序，以便它支持联系人组。 我们将此新功能添加到我们的应用程序使用名为测试驱动开发的软件设计过程。

> [!div class="step-by-step"]
> [上一页](iteration-4-make-the-application-loosely-coupled-vb.md)
> [下一页](iteration-6-use-test-driven-development-vb.md)
