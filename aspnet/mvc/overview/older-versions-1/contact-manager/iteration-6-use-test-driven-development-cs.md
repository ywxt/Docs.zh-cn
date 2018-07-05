---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 迭代 6 – 使用测试驱动开发 (C#) |Microsoft Docs
author: microsoft
description: 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 此小版本中...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: 58e1ab5a0a65e65b70a8f8a9f5e45564499efd63
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830064"
---
<a name="iteration-6--use-test-driven-development-c"></a>迭代 6 – 使用测试驱动开发 (C#)
====================
by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 在此迭代中，我们将添加联系人组。


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>生成联系人管理 ASP.NET MVC 应用程序 (C#)
  

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

在联系人管理器应用程序上一次迭代，我们创建单元测试，以提供网络安全代码。 用于创建单元测试的动机是使我们的代码更具弹性，若要更改。 使用中的位置的单元测试，我们可以值得庆幸的是对我们的代码进行任何更改，并立即知道是否我们破坏现有功能。

在此迭代中，我们使用单元测试进行完全不同的用途。 在此迭代中，我们使用单元测试作为一部分调用应用程序设计理念*测试驱动开发，*。 当您练习测试驱动开发，首先编写测试，然后编写针对测试的代码。

更确切地说，实践测试驱动开发，有三个步骤，在完成后创建的代码 (红 / 绿/重构):

1. 编写的单元测试失败 （红色）
2. 编写代码，通过的单元测试 （绿色）
3. 重构代码 （重构）

首先，您编写单元测试。 单元测试应表达你打算为您的代码的预期行为。 当你首次创建单元测试时，单元测试应失败。 测试应失败，因为尚未编写满足测试任何应用程序代码。

接下来，为了使单元测试通过编写刚好足够的代码。 目标是 laziest、 sloppiest 和可能最快的方式编写的代码。 你不应浪费时间考虑您的应用程序的体系结构。 相反，您应集中精力编写单元测试所表达的意图满足所需代码的最少工作量。

最后，编写足够的代码后，你可以回过头想想您的应用程序的整体体系结构。 在此步骤中，重写 （重构） 你的代码通过利用的软件设计模式-存储库模式-例如，使代码更易于维护。 支持下大胆可以请你在此步骤中的代码重写原因由单元测试纳入您的代码。

有很多好处所产生的测试驱动开发，在其中完成练习。 首先，测试驱动开发强制您专注于实际需要编写的代码。 因为你不断地关注只需编写足够的代码来传递特定的测试，请您不能进入的这个井水和写入大量永远不会将使用的代码。

其次，"首先测试"的设计方法会强制您从将如何使用你的代码的角度来看编写代码。 换而言之，实践测试驱动开发，您会不断地编写你的测试从用户角度来看。 因此，测试驱动开发，可能导致更干净且更易于理解的 Api。

最后，测试驱动开发，会强制你编写单元测试编写的应用程序的正常过程的一部分。 项目截止时间的临近，测试是通常超出窗口第一件事。 实践测试驱动开发，但是，则更有可能是良性有关编写单元测试，因为测试驱动开发，使单元测试中央为构建应用程序的过程。

> [!NOTE] 
> 
> 若要了解有关测试驱动开发的详细信息，建议您阅读 Michael Feathers 书籍**处理有效地使用旧代码**。


在此迭代中，我们将一项新功能添加到我们的联系人管理器应用程序。 我们将添加对联系人组的支持。 可以使用联系人组来组织你的联系人为如业务的类别和友元组。

我们将这一新功能添加到我们的应用程序，通过的测试驱动的开发过程。 我们将首先编写单元测试，我们将编写所有这些测试针对我们的代码。

## <a name="what-gets-tested"></a>获取测试内容

如我们在上一次迭代中所述，通常没有为数据访问逻辑编写单元测试或查看逻辑。 您不 t 写入的数据访问逻辑的单元测试，因为访问数据库是一个相对较慢的操作。 您不视图逻辑的 t 写入单元测试，因为访问视图需要快速启动的 web 服务器，这是一个相对较慢的操作。 长度应不 t 编写单元测试，除非可以执行测试，非常快

由于测试驱动开发，由单元测试，我们专注于最初编写控制器和业务逻辑。 我们避免触及视图的数据库。 我们获得了 t 修改数据库或本教程的最后才创建我们的视图。 我们开始可以测试内容。

## <a name="creating-user-stories"></a>创建用户情景

实践测试驱动开发，始终首先编写测试。 这将立即引发问题： 如何确定哪些测试，以首先编写？ 若要回答此问题，应编写一套[**用户情景**](http://en.wikipedia.org/wiki/User_stories)。

用户情景是很短的软件要求 （通常一个句子） 说明。 它应该是从用户角度编写需求的非技术说明。

下面提供的一组描述新的联系人组功能所需的功能的用户情景：

1. 用户可以查看联系人组的列表。
2. 用户可以创建新的联系人组。
3. 用户可以删除现有的联系人组。
4. 创建一个新的联系人时，用户可以选择联系人组。
5. 编辑现有联系人时，用户可以选择联系人组。
6. 在索引视图中显示的联系人组列表。
7. 当用户单击联系人组时，显示的匹配的联系人列表。

请注意，此列表的用户情景的客户完全可以理解。 并没有提及的技术实现详细信息。

虽然在构建过程中你的应用程序，一组用户情景可能会变得更完善。 为多个情景 （要求），则可能会中断用户情景。 例如，可能会决定创建新的联系人组应涉及验证。 提交联系人组没有名称应返回验证错误。

创建用户情景的列表后，已准备好编写第一个单元测试。 我们将首先创建单元测试用于查看联系人组的列表。

## <a name="listing-contact-groups"></a>列表联系人组

我们第一个用户情景是用户应该能够查看联系人组的列表。 我们需要使用测试 express 这篇文章。

创建新的单元测试，请右键单击 Controllers 文件夹在 ContactManager.Tests 项目中，选择**添加、 新测试**，并选择**单元测试**模板 （参见图 1）。 名称在新的单元测试 GroupControllerTest.cs，然后单击**确定**按钮。


[![添加 GroupControllerTest 单元测试](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**图 01**： 添加 GroupControllerTest 单元测试 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image2.png))


在列表 1 中包含了第一个单元测试。 此测试验证组控制器的 index （） 方法返回一系列组。 此测试将验证组的集合视图中返回数据。

**代码清单 1-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

当你首次在列表 1 中在 Visual Studio 中键入代码时，您将获得大量的红色波浪线。 我们尚未创建 GroupController 或组类。

此时，我们可以 t 甚至生成我们的应用程序，以便我们可以 t 执行了第一个单元测试。 很好的 s。 作为失败测试计数。 因此，我们现在必须开始编写应用程序代码的权限。 我们需要编写足够的代码来执行我们的测试。

代码清单 2 中的组控制器类包含通过单元测试所需代码的最低。 Index （） 操作返回组 （组类定义中清单 3） 以静态方式编码的的列表。

**代码清单 2-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**代码清单 3-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

我们将在 GroupController 和组类添加到我们的项目后，我们的第一个单元测试成功完成 （请参见图 2）。 我们已经通过该测试所需的最小工作。 为了庆祝就。


[![成功 ！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**图 02**： 成功 ！ ([单击此项可查看原尺寸图像](iteration-6-use-test-driven-development-cs/_static/image4.png))


## <a name="creating-contact-groups"></a>创建联系人组

现在，我们可以转到第二个用户情景。 我们需要能够创建新联系人组。 我们需要与测试 express 此目的。

列表 4 中的测试验证调用 create （） 方法，通过新组将组添加到组 index （） 方法返回的列表。 换而言之，如果我创建一个新组然后我应该能够收到新的组的 index （） 方法返回的组的列表。

**列表 4-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

列表 4 中的测试会调用组控制器与新联系人组 create （） 方法。 接下来，测试将验证，调用组控制器 index （） 方法返回新的组中查看数据。

列表 5 中已修改的组控制器包含的更改通过新的测试所需的最低要求。

**列表 5-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>列表 5 中的组控制器具有一个新的 create （） 操作。 此操作将一组添加到组的集合。 请注意，index （） 操作已被修改以返回组的集合的内容。

再次重申，我们已执行利用最少量的通过单元测试所需的工作。 我们对组控制器进行这些更改后，我们单位的所有测试都通过。

## <a name="adding-validation"></a>添加验证

显式用户情景中，未规定此要求。 但是，有理由需要一个组具有一个名称。 否则，将联系人组织到组将不会非常有用。

代码清单 6 包含新的测试表明此目的。 此测试验证尝试无需提供在模型状态中的验证错误消息中的名称结果中创建组。

**代码清单 6-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

为了满足此测试，我们需要添加到组类 （请参阅列表 7） 的 Name 属性。 此外，我们需要将小小的验证逻辑添加到组控制器 s create （） 操作 （请参阅代码清单 8）。

**列表 7-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**代码清单 8-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

请注意组控制器 create （） 操作现在包含验证和数据库的逻辑。 当前，组控制器使用的数据库所包含的没有什么比内存中集合。

## <a name="time-to-refactor"></a>重构的时间

红/绿/重构的第三步是重构部分。 此时，我们需要我们的代码中，并考虑如何，我们可以重构应用程序以提高它的设计。 重构阶段是的我们认真考虑的最佳方法的实现软件设计原则和模式的阶段。

我们可以随意修改我们的代码以任何方式，我们选择以提高代码的设计。 我们有单元测试，使我们无法破坏现有功能的安全网。

现在，我们组控制器是从优秀的软件设计的角度来看乱。 组控制器包含纷繁混乱现象验证和数据访问代码。 为了避免违反单一责任原则，我们需要将这些问题分离到不同的类。

我们重构的组控制器类都包含在程序列表 9。 控制器已被修改为使用 ContactManager 服务层。 这是我们向联系人控制器使用的相同服务层。

代码清单 10 包含添加到 ContactManager 服务层以支持验证、 列出和创建组的新方法。 IContactManagerService 界面已更新为包括新的方法。

代码清单 11 包含实现 IContactManagerRepository 接口的新 FakeContactManagerRepository 类。 与 EntityContactManagerRepository 类还实现 IContactManagerRepository 接口，不同新 FakeContactManagerRepository 类不与数据库通信。 FakeContactManagerRepository 类使用的内存中集合的代理的数据库。 我们将在我们的单元测试中使用此类，作为一个虚设储存库层。

**列表 9-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**代码清单 10-Controllers\ContactManagerService.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**代码清单 11-Controllers\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

修改接口需要的 IContactManagerRepository 使用 EntityContactManagerRepository 类中实现的 CreateGroup() 和 ListGroups() 方法。 执行此操作的 laziest 和最快方法是添加存根 （stub） 的方法如下所示：   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]


最后，我们的应用程序设计这些更改需要我们对我们的单元测试中进行一些修改。 我们现在需要执行单元测试时使用 FakeContactManagerRepository。 更新后的 GroupControllerTest 类都包含在列表 12。

**列表 12-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

建立所有这些后，再次重申，所有更改的我们通过单元测试。 我们已经完成红/绿/重构整个周期。 我们已实现的第一个的两个用户情景。 现在，我们具有支持单元测试的用户情景以表示的要求。 实现用户情景的剩余部分包括重复红/绿/重构的同一个周期。

## <a name="modifying-our-database"></a>修改我们的数据库

遗憾的是，尽管我们已经满足所有要求通过我们的单元测试来表示，我们的工作不会进行。 我们仍需要修改我们的数据库。

我们需要创建一个新的组数据库表。 请执行这些步骤：

1. 在服务器资源管理器窗口中，右键单击表文件夹，然后选择菜单选项**添加新表**。
2. 输入在表设计器中，如下所述的两个列。
3. 将标记 Id 列作为主键和标识列。
4. 通过单击的软盘图标与命名组保存的新表。

<a id="0.11_table01"></a>


| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | int | False |
| name | nvarchar （50) | False |


接下来，我们需要从联系人表中删除的所有数据 (否则，我们获得了能够创建联系人和组表之间的关系)。 请执行这些步骤：

1. 右键单击联系人表，然后选择菜单选项**显示表数据**。
2. 删除的所有行。

接下来，我们需要定义组数据库表和现有的联系人数据库表之间的关系。 请执行这些步骤：

1. 双击服务器资源管理器窗口打开表设计器中的联系人表。
2. 将新的整数列添加到名为 GroupId 联系人表。
3. 单击关系按钮以打开外键关系对话框 （参见图 3）。
4. 单击添加按钮。
5. 单击显示表和列规范按钮旁边的省略号按钮。
6. 在表和列对话框中，选择作为主键表和作为主键列的 Id 的组。 选择联系人作为外键表和外键列作为 GroupId （请参阅图 4）。 单击确定按钮。
7. 下**INSERT 和 UPDATE 规范**，选择的值**Cascade**有关**删除规则**。
8. 单击关闭按钮以关闭外键关系对话框。
9. 单击保存按钮以将所做的更改保存到 Contacts 表。


[![创建数据库表关系](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**图 03**： 创建数据库表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image6.png))


[![指定表关系](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**图 04**： 指定表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image8.png))


### <a name="updating-our-data-model"></a>更新数据模型

接下来，我们需要更新数据模型以表示新的数据库表。 请执行这些步骤：

1. 双击 ContactManagerModel.edmx 文件在 Models 文件夹中打开实体设计器。
2. 右键单击设计器图面，然后选择菜单选项**从数据库更新模型**。
3. 在更新向导中，选择组表，然后单击完成按钮 （请参见图 5）。
4. 右键单击组实体，然后选择菜单选项**重命名**。 更改的名称*组*实体与*组*（单数）。
5. 右键单击联系人实体的底部将显示的组导航属性。 更改的名称*组*导航属性设置为*组*（单数）。


[![更新数据库中的实体框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**图 05**： 更新数据库中的实体框架模型 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image10.png))


完成这些步骤后，你的数据模型将表示的联系人和组的表。 在实体设计器应显示这两个实体 （请参阅图 6）。


[![实体设计器显示组和联系人](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**图 06**： 显示组和联系人实体设计器 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image12.png))


### <a name="creating-our-repository-classes"></a>创建存储库类

接下来，我们需要实现我们的存储库类。 此迭代的过程中，我们添加了几个新方法到 IContactManagerRepository 接口编写代码以满足我们的单元测试时。 IContactManagerRepository 接口的最终版本包含在列表 14。

**代码清单 14-Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

我们还没有真正实现任何与使用联系人组相关的方法。 目前，EntityContactManagerRepository 类 IContactManagerRepository 界面中列出的联系人组方法的每个具有存根 （stub） 方法。 例如，ListGroups() 方法当前如下所示：

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

存根 （stub） 方法使我们能够编译我们的应用程序并通过单元测试。 但是，现在就来实施这些方法。 EntityContactManagerRepository 类的最终版本包含在列表 13。

**代码清单 13-Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>创建视图

ASP.NET MVC 应用程序时使用的默认 ASP.NET 视图引擎。 因此，don t 创建视图以响应特定的单元测试。 但是，因为应用程序都是毫无用处，除非视图，我们可以 t 完成此迭代而无需创建和修改联系人管理器应用程序中包含的视图。

我们需要创建以下新视图，用于管理联系人组 （请参阅图 7）：

- Views\Group\Index.aspx-联系人组的显示列表
- Views\Group\Delete.aspx-用于删除联系人组显示确认窗体


[![组索引视图](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**图 07**: 组索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image14.png))


我们需要修改以下现有视图，使其包含联系人组：

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

通过查看此教程中随附的 Visual Studio 应用程序，可以看到修改后的视图。 例如，图 8 显示了联系人索引视图。


[![请联系索引视图](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**图 08**: 请联系索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image16.png))


## <a name="summary"></a>总结

在此迭代中，我们添加新功能到我们的联系人管理器应用程序按照测试驱动开发应用程序设计方法。 我们首先创建了一组用户情景。 我们创建了一组单元测试用户情景所表达的要求相对应。 最后，我们编写了刚好足够的代码以满足表示的单元测试的要求。

我们完成编写足够的代码以满足表示的单元测试的要求后，我们将更新我们的数据库和视图。 我们对我们的数据库添加新组表，并更新我们实体框架数据模型。 我们还创建和修改的一组视图。

在下一次迭代-最后一个迭代-我们重写应用程序以充分利用 Ajax。 通过利用 Ajax，我们将提高响应能力和联系人管理器应用程序的性能。

> [!div class="step-by-step"]
> [上一页](iteration-5-create-unit-tests-cs.md)
> [下一页](iteration-7-add-ajax-functionality-cs.md)
