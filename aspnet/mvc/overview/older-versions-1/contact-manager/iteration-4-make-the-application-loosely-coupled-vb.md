---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: 迭代 4 – 使应用程序松散耦合 (VB) |Microsoft Docs
author: microsoft
description: 在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 预测...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 37aef9b3bb1221902c1eb84bd4218a30c758b81a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401232"
---
<a name="iteration-4--make-the-application-loosely-coupled-vb"></a>迭代 4 – 使应用程序松散耦合 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> 在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序 (VB)

在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。 联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。

我们通过多个迭代中生成应用程序。 每次迭代时，我们逐渐提高应用程序。 此多个迭代方法的目标是帮助你了解每个更改的原因。

- 迭代 1-创建应用程序。 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。

- 迭代 2 – 使应用程序看上去更美观。 在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。

- 迭代 3-添加窗体验证。 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证电子邮件地址和电话号码。

- 迭代 4-使应用程序松散耦合。 在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。 例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 5 — 创建单元测试。 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。

- 迭代 6-使用测试驱动的开发。 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。

- 迭代 7-添加 Ajax 功能。 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。

## <a name="this-iteration"></a>此迭代

在联系人管理器应用程序的此第四个迭代中，我们将重构应用程序以使应用程序更为松散耦合。 时松散耦合应用程序，可以修改应用程序的一个部分中的代码，而无需修改应用程序的其他部分中的代码。 松散耦合应用程序是更具弹性，若要更改。

目前，所有联系人管理器应用程序使用的数据访问和验证逻辑都包含在控制器类。 这是一个好主意。 无论何时需要修改你的应用程序的一部分，则可能 bug 引入你的应用程序的另一个部分。 例如，如果您修改您的验证逻辑，则可能你的数据访问或控制器逻辑中引入新 bug。

> [!NOTE] 
> 
> (SRP)，一个类应永远不会有多个理由更改。 混合使用控制器、 验证和数据库的逻辑是大规模违反了单一责任原则。


有可能需要修改你的应用程序的多个原因。 可能需要将一项新功能添加到你的应用程序，可能需要修复你的应用程序中的 bug 或可能需要修改你的应用程序的一项功能的实现方式。 应用程序是很少静态的。 他们往往增长且随着时间的推移发生变化。

例如，假设你决定如何实现数据访问层更改。 右现在，联系人管理器应用程序使用 Microsoft Entity Framework 访问数据库。 但是，您可能决定将迁移到新的或可选的数据访问技术，如 ADO.NET 数据服务或 NHibernate。 但是，由于数据访问代码不是独立于验证和控制器代码，将无法修改你的应用程序中的数据访问代码而无需修改其他与数据访问不直接相关的代码。

当松散耦合应用程序时，但是，您可以进行更改的一部分应用程序无需接触应用程序的其他部分。 例如，您可以切换数据访问技术而无需修改你验证或控制器的逻辑。

在此迭代中，我们将充分利用，我们可以重构我们的联系人管理器应用程序更松散耦合的应用程序的多个软件设计模式。 我们完成时结束-赢得 t 联系人管理器执行任何操作，它并没有未这样做之前。 但是，我们将能够将应用程序在将来更轻松地更改。

> [!NOTE] 
> 
> 重构是重写的方式不丢失任何现有功能的应用程序的过程。


## <a name="using-the-repository-software-design-pattern"></a>使用存储库软件设计模式

我们第一项更改是充分利用称为存储库模式的软件设计模式。 我们将使用存储库模式来隔离数据访问代码从我们的应用程序的其余部分。

实现存储库模式需要完成以下两个步骤：

1. 创建一个接口
2. 创建实现接口的具体类

首先，我们需要创建一个描述所有我们需要执行的数据访问方法的接口。 IContactManagerRepository 接口包含在列表 1 中。 此接口描述五种方法： CreateContact()、 DeleteContact()、 EditContact()、 GetContact 和 ListContacts()。

**代码清单 1-Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

接下来，我们需要创建实现 IContactManagerRepository 接口的具体类。 由于我们使用 Microsoft 实体框架来访问数据库，我们将创建一个名为 EntityContactManagerRepository 的新类。 此类包含在代码清单 2 中。

**代码清单 2-Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

请注意 EntityContactManagerRepository 类实现 IContactManagerRepository 接口。 类实现该接口所述的方法的所有五个。

您可能想知道为什么我们需要使用接口会很麻烦。 我们为什么需要创建一个接口和类来实现它？

有一个例外，我们的应用程序的其余部分将使用接口而不是具体类进行交互。 而不是调用由 EntityContactManagerRepository 类公开的方法，我们将调用由 IContactManagerRepository 接口公开的方法。

这样一来，我们可以实现新类的接口，而无需修改我们的应用程序的其余部分。 例如，在将来某天中，我们可能想要实现 DataServicesContactManagerRepository 类实现 IContactManagerRepository 接口。 DataServicesContactManagerRepository 类可以使用 ADO.NET 数据服务来访问数据库而不是 Microsoft 实体框架。

如果应用程序代码进行编程，针对而不是具体的 EntityContactManagerRepository 类 IContactManagerRepository 接口然后我们可以切换具体类而无需修改任何代码的其余部分。 例如，我们可以从切换 EntityContactManagerRepository 类到 DataServicesContactManagerRepository 类而无需修改我们的数据访问或验证逻辑。

针对接口 （抽象） 而不是具体类的编程使我们的应用程序更具弹性，若要更改。

> [!NOTE] 
> 
> 通过选择菜单选项重构，提取接口，可以快速从 Visual Studio 中的具体类创建接口。 例如，您可以首先创建 EntityContactManagerRepository 类，然后使用提取接口来自动生成 IContactManagerRepository 接口。


## <a name="using-the-dependency-injection-software-design-pattern"></a>使用依赖关系注入软件设计模式

现在，我们已迁移到一个单独的存储库类的数据访问代码，我们需要修改联系人控制器使用此类。 我们将利用称为依赖关系注入在控制器中使用的存储库类的软件设计模式。

修改后的联系人控制器都包含在清单 3。

**代码清单 3-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

请注意，在列表 3 中的联系人控制器包含两个构造函数。 第一个构造函数将 IContactManagerRepository 接口的具体实例传递给第二个构造函数。 请联系控制器类使用*构造函数依赖关系注入*。

一个，仅使用 EntityContactManagerRepository 类的位置是在第一个构造函数中。 类的其余部分使用 IContactManagerRepository 接口而不是具体的 EntityContactManagerRepository 类。

这样可以方便地在将来切换 IContactManagerRepository 类的实现。 如果你想要使用 DataServicesContactRepository 类而不是 EntityContactManagerRepository 类，只需修改第一个构造函数。

构造函数依赖关系注入还使 Contact 控制器类非常可测试性。 在单元测试中，您可以通过传递 IContactManagerRepository 类的模拟实现实例化联系人控制器。 我们构建的联系人管理器应用程序单元测试时，此功能依赖关系注入将下一次迭代对我们非常重要。

> [!NOTE] 
> 
> 如果你想要完全分离 Contact 控制器类从 IContactManagerRepository 接口的特定实现然后你可以利用一个框架，支持如 StructureMap 或 Microsoft 依赖关系注入实体框架 (MEF)。 通过利用依赖关系注入框架，永远不需要引用在代码中的具体类。


## <a name="creating-a-service-layer"></a>创建服务层

您可能已经注意到我们的验证逻辑仍混合在一起我们清单 3 中的已修改的控制器类中的控制器逻辑。 出于同一原因，它是一个好办法隔离我们的数据访问逻辑，它是一个好办法隔离我们验证逻辑。

若要解决此问题，我们可以创建一个单独[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)。 服务层是一个单独的层，我们可以将插入之间，我们的控制器和存储库类。 服务层包含我们包括所有我们验证逻辑的业务逻辑。

列表 4 中包含 ContactManagerService。 它包含联系人控制器类中的验证逻辑。

**Listing 4 - Models\ContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

请注意 ContactManagerService 的构造函数需要 ValidationDictionary。 服务层与通过此 ValidationDictionary 控制器层进行通信。 我们将讨论以下节中详细介绍 ValidationDictionary 时我们讨论的修饰器模式。

此外，请注意，ContactManagerService 实现 IContactManagerService 接口。 您应始终致力于针对接口而不是具体类进行编程。 联系人管理器应用程序中的其他类并直接与 ContactManagerService 类交互。 相反，有一个例外，联系人管理器应用程序的其余部分进行编程，针对 IContactManagerService 接口。

IContactManagerService 接口包含在列表 5 中。

**列表 5-Models\IContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

列表 6 中包含已修改的联系人控制器类。 请注意联系人控制器不再与 ContactManager 存储库交互。 相反，请联系控制器与 ContactManager 服务进行交互。 每一层隔离尽可能多地从其他层。

**代码清单 6-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

我们的应用程序不再运行落入最常见的单一责任原则 (SRP)。 列表 6 中的联系人控制器已去除以外控制流的应用程序执行的每个责任。 已从联系人控制器中删除所有验证逻辑并推送到服务层。 所有数据库逻辑已推送到存储库层。

## <a name="using-the-decorator-pattern"></a>使用修饰器模式

我们想要能够完全分离我们从我们的控制器层的服务层。 从原理上讲，我们应能够编译我们的服务层在单独的程序集从我们的控制器层而无需添加对 MVC 应用程序的引用。

但是，我们的服务层需要能够将验证错误消息传递回控制器层。 如何才能使服务层进行通信而无需联系在一起的控制器和服务层验证错误消息？ 我们可以利用名为软件设计模式[Decorator 模式](http://en.wikipedia.org/wiki/Decorator_pattern)。

在控制器使用名为 ModelState ModelStateDictionary 来表示验证错误。 因此，你可能想要将 ModelState 从控制器层传递到服务层。 但是，在服务层中使用 ModelState 将使您的服务层依赖于 ASP.NET MVC framework 的一项功能。 这会十分严重，因为某一天，可能想要使用的服务层与 WPF 应用程序而不是 ASP.NET MVC 应用程序。 在这种情况下，对 t 想要引用 ASP.NET MVC 框架使用 ModelStateDictionary 类。

修饰器模式使您能够以实现接口的新类中包装现有的类。 我们的联系人管理器项目中包括列表 7 中包含的 ModelStateWrapper 类。 ModelStateWrapper 类在代码清单 8 中实现该接口。

**Listing 7 - Models\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**代码清单 8-Models\Validation\IValidationDictionary.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

如果您仔细研究一下列表 5 您会发现 ContactManager 服务层以独占方式使用 IValidationDictionary 接口。 ContactManager 服务不依赖于 ModelStateDictionary 类。 当联系控制器创建 ContactManager 服务时，控制器将包装其 ModelState 如下：

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>总结

在此迭代中，我们未向联系人管理器应用程序添加任何新功能。 此迭代的目标是重构联系人管理器应用程序就是更轻松地监视和修改。

首先，我们实现了存储库软件设计模式。 我们将所有数据访问代码迁移到一个单独的 ContactManager 存储库类。

我们还与我们的控制器逻辑隔离我们验证逻辑。 我们创建一个单独的服务层，包含所有验证代码。 控制器层与服务层进行交互并与存储库层的服务层进行交互。

我们创建的服务层，我们利用了要从我们的服务层中隔离 ModelState 的修饰器模式。 在我们的服务层，我们将编写针对而不是 ModelState IValidationDictionary 接口。

最后，我们利用了名为依赖关系注入模式的软件设计模式。 此模式可让我们针对接口 （抽象） 而不是具体类进行编程。 实现依赖关系注入设计模式还使我们的代码更具可测性。 在下一个迭代中，我们将单元测试添加到我们的项目。

> [!div class="step-by-step"]
> [上一页](iteration-3-add-form-validation-vb.md)
> [下一页](iteration-5-create-unit-tests-vb.md)
