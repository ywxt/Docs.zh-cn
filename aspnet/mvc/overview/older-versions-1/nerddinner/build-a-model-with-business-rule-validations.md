---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证功能构建模型 |Microsoft Docs
author: microsoft
description: 步骤 3 显示了如何创建一个模型，我们可以使用这两个查询，并为 NerdDinner 应用程序更新数据库。
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 4bed4dd794c7c34551cd3c7543e08ed12d83505a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836763"
---
<a name="build-a-model-with-business-rule-validations"></a>使用业务规则验证功能构建模型
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 3 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 3 显示了如何创建一个模型，我们可以使用这两个查询，并为 NerdDinner 应用程序更新数据库。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner 步骤 3： 生成模型

在一个模型-视图-控制器框架术语"模型"是指表示数据的应用程序，以及与之集成验证规则和业务规则的相应域逻辑的对象。 模型在很多方面"核心"的基于 MVC 的应用程序，并且正如我们将看到更高版本从根本上驱动器的行为。

ASP.NET MVC 框架支持使用任何数据访问技术和开发人员可以选择使用不同的丰富的.NET 数据选项，来实现其模型，包括： LINQ to 实体、 LINQ to SQL、 NHibernate、 LLBLGen Pro，SubSonic、 WilsonORM 或只是原始的 ADO。NET Datareader 或数据集。

NerdDinner 应用程序，我们将使用 LINQ to SQL 创建简单的模型的方法相当接近于我们的数据库设计，并将一些自定义验证逻辑和业务规则。 我们然后将实现存储库类，可帮助立即抽象应用程序，并允许我们轻松单元测试的其余部分的数据持久性实现。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL 是作为.NET 3.5 的一部分提供的 ORM （对象关系映射程序）。

LINQ to SQL 提供轻松地将数据库表映射到我们可以编写代码的.NET 类。 NerdDinner 应用程序我们将使用它来将 Dinners 和 RSVP 表映射到 Dinner 和 RSVP 类我们数据库中。 Dinners 和 RSVP 表的列将相对应的 Dinner 和 RSVP 类上的属性。 每个 Dinner 和 RSVP 对象将表示数据库中的 Dinners 或 RSVP 表内一个单独的行。

LINQ to SQL 允许我们可以避免不得不手动构造 SQL 语句以检索和更新 Dinner 的 RSVP 数据库数据的对象。 相反，我们将定义的 Dinner 和 RSVP 的类，它们映射到如何存储或从数据库和它们之间的关系。 然后，LINQ to SQL 将将负责生成用于进行交互并使用它们时，在运行时使用的相应 SQL 执行逻辑。

我们可以使用 VB 和 C# 中的 LINQ 语言支持编写检索 Dinner 和 RSVP 的表达查询数据库中的对象。 这将减少我们需要编写，数据代码量，并让我们来构建真正清理应用程序。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>将 LINQ to SQL 类添加到我们的项目

我们将首先右键单击"Models"文件夹中我们的项目，并选择**Add-&gt;新项**菜单命令：

![](build-a-model-with-business-rule-validations/_static/image1.png)

这将显示"添加新项"对话框。 我们将按"数据"类别筛选，并选择在其中的"LINQ to SQL Classes"模板：

![](build-a-model-with-business-rule-validations/_static/image2.png)

我们将命名项"NerdDinner"，然后单击"添加"按钮。 Visual Studio 将添加我们 \Models 的目录下的 NerdDinner.dbml 文件并打开 LINQ to SQL 对象关系设计器：

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>使用 LINQ to SQL 创建数据模型类

LINQ to SQL，我们能够快速从现有数据库架构创建数据模型类。 待办事项我们想要在其中建模的此我们将在服务器资源管理器中打开 NerdDinner 数据库并选择的表：

![](build-a-model-with-business-rule-validations/_static/image4.png)

然后，我们可以将表拖到 LINQ 到 SQL 设计器图面。 当我们进行此 LINQ to SQL 将自动创建 Dinner 的 RSVP 类使用 （包括类将映射到数据库表列的属性） 的表的架构：

![](build-a-model-with-business-rule-validations/_static/image5.png)

默认情况下，LINQ to SQL 设计器自动"为"表名和列名时它将创建基于数据库架构的类。 例如： 在上述示例中的"Dinners"表会导致"Dinner"类。 此类命名可帮助使我们的模型与.NET 命名约定保持一致，我经常发现该具有设计器修复这向上方便 （尤其是在添加许多表）。 如果您不喜欢类或该设计器生成，但你始终可以重写它并将其更改为所需的任何名称的属性的名称。 您可以执行此操作通过编辑实体/属性名称串联在设计器中或通过修改通过属性网格。

默认情况下，LINQ to SQL 设计器还会检查表的主键/外键关系和自动基于它们创建默认"关系关联的的之间的不同模型类，它将创建。 例如，当我们拖动 Dinners 和 RSVP 表到 LINQ to SQL 设计器上两者之间的一个对多关系关联推断基于的事实，RSVP 表具有外键，到 Dinners 表 (这会由中的箭头指示设计器）：

![](build-a-model-with-business-rule-validations/_static/image6.png)

上面的关联会导致 LINQ to SQL 将强类型化"Dinner"属性添加到开发人员可用于访问与给定的 RSVP Dinner 的 RSVP 类。 它将导致 Dinner 类具有一个"RSVPs"集合属性，使开发人员能够检索和更新关联与特定 Dinner 的 RSVP 对象。

下面介绍 Visual Studio 中的 intellisense 的示例，当我们创建一个新的 RSVP 对象并将其添加到 Dinner 的 Rsvp 集合时。 请注意如何 LINQ to SQL 会自动添加"Rsvp"集合上的 Dinner 对象：

![](build-a-model-with-business-rule-validations/_static/image7.png)

通过将 RSVP 对象添加到 Dinner 的 Rsvp 集合，我们将指示 LINQ to SQL 将 Dinner 和我们的数据库中的 RSVP 行之间的外键关系相关联：

![](build-a-model-with-business-rule-validations/_static/image8.png)

如果您不喜欢如何在设计器已建模或名为表关联，可以重写它。 只需单击设计器中的关联箭头，然后访问其属性通过属性网格，若要重命名、 删除或修改它。 我们 NerdDinner 的应用程序，不过，默认关联规则适用于我们正在创建数据模型类和我们可以直接使用的默认行为。

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext 类

Visual Studio 将自动创建表示模型和使用 LINQ to SQL 设计器定义的数据库关系的.NET 类。 LINQ to SQL DataContext 类还会为每个 LINQ to SQL 设计器文件添加到解决方案中生成。 因为我们命名为我们 LINQ to SQL 类项"NerdDinner"，创建的 DataContext 类将名为"NerdDinnerDataContext"。 此 NerdDinnerDataContext 类是我们将与数据库交互的主要方法。

我们 NerdDinnerDataContext 类公开两个属性-"Dinners"和"RSVPs"-表示我们在数据库中建模的两个表。 我们可以使用 C# 来编写 LINQ 查询对这些属性对查询和检索 Dinner 和 RSVP 对象从数据库。

下面的代码演示如何实例化 NerdDinnerDataContext 对象并执行针对它以获取 Dinners 将来发生的一系列的 LINQ 查询。 编写 LINQ 查询时，visual Studio 提供了完整的 intellisense 和从其返回的对象都是强类型，而且还支持 intellisense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

除了允许我们 Dinner 和 RSVP 对象查询，NerdDinnerDataContext 还会自动跟踪我们随后对我们通过它检索的 Dinner 和 RSVP 对象进行任何更改。 我们可以使用此功能来轻松地将所做的更改保存回数据库-而无需编写任何显式的 SQL 更新代码。

例如，下面的代码演示如何使用 LINQ 查询以从数据库中检索单个 Dinner 对象更新两个 Dinner 属性，然后将所做的更改保存回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

在上面的代码的 NerdDinnerDataContext 对象自动跟踪对我们从它检索的 Dinner 对象的属性更改。 当我们调用"SubmitChanges()"方法时，它将执行到要保存更新后的值返回的数据库的相应 SQL"更新"语句。

### <a name="creating-a-dinnerrepository-class"></a>创建 DinnerRepository 类

对于小型应用程序是有时可以将具有控制器直接对 LINQ to SQL DataContext 类工作，并将嵌入控制器中的 LINQ 查询。 随着应用程序变得更长，不过，这种方法变得难以维护和测试。 它可能还会导致我们复制多个位置中的相同 LINQ 查询。

可以使应用程序更易于维护和测试的一种方法是使用"存储库"模式。 存储库类可帮助封装数据查询和持久性逻辑和提取了从应用程序的数据持久性的实现细节。 除了使应用程序代码更简洁，使用存储库模式可以轻松地在将来，更改数据存储实现，它可以帮助简化单元测试的应用程序而无需实际数据库。

NerdDinner 应用程序中，我们将定义 DinnerRepository 类具有以下签名：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注意： 更高版本在本章我们将从此类提取 IDinnerRepository 接口，使我们控制器上使用它的依赖关系注入。开始时，不过，我们将简单的开始和只需直接使用 DinnerRepository 类。*

若要实现此类，我们将在我们"Models"文件夹上右键单击并选择**Add-&gt;新项**菜单命令。 在"添加新项"对话框中，我们将选择"类"模板，并将文件命名"DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

然后，我们可以实现我们使用下面的代码的 DinnerRespository 类：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>检索、 更新、 插入和删除使用 DinnerRepository 类

现在，我们已创建我们的 DinnerRepository 类，让我们看一些代码示例演示我们可以用它完成常见任务：

#### <a name="querying-examples"></a>查询示例

下面的代码检索单个 Dinner 使用 DinnerID 值：


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

下面的代码会通过其检索所有即将推出 dinners 和循环：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>插入和更新示例

下面的代码演示如何添加两个新 dinners。 在其上调用"save （）"方法之前，对存储库中添加/修改不会提交到数据库。 LINQ to SQL 会自动将所有更改都包装在数据库事务 – 因此发生了所有更改或其中任何一个执行时我们的存储库将保存：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

下面的代码检索现有 Dinner 对象，并修改它的两个属性。 在我们的存储库上调用"save （）"方法时，在提交回数据库更改：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

下面的代码检索 dinner，然后向其添加 RSVP。 这样做 （因为在数据库中两者之间没有主键键/外键关系），为我们创建 LINQ to SQL 的 Dinner 对象上使用 Rsvp 集合。 在存储库上调用"save （）"方法时，此更改为新的 RSVP 表行保存回数据库中：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>删除示例

下面的代码检索现有 Dinner 对象，并随后会被删除标记。 在存储库上调用"save （）"方法时它将删除提交回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>将与模型类集成验证和业务规则逻辑

集成验证和业务规则逻辑是适用于数据的任何应用程序的关键部分。

#### <a name="schema-validation"></a>架构验证

模型类定义时使用 LINQ to SQL 设计器，在数据模型类中属性的数据类型对应于数据库表的数据类型。 例如： 如果 Dinners 表中的"EventDate"列"datetime"，创建 linq to SQL 的数据模型类将类型为"DateTime"（这是内置的.NET 数据类型）。 这意味着如果你尝试从代码中，为其分配一个整数或布尔值，并且如果尝试将隐式非有效的字符串类型转换为它在运行时，它将自动引发错误，则会收到编译错误。

使用的字符串-它有助于保护您免受 SQL 注入攻击时使用它时，LINQ to SQL 还会自动将为你处理转义 SQL 值。

#### <a name="validation-and-business-rule-logic"></a>验证和业务规则逻辑

架构验证作为第一个步骤，非常有用，但很少足够。 大多数实际情况下，需要指定更丰富的验证逻辑可以跨越多个属性、 执行代码，且通常有意识的模型的状态的功能 (例如： 它正在创建/更新/删除，或在某一特定于域的状态例如"已存档"）。 有各种不同的模式和框架，可用于定义并将验证规则应用于模型的类，并有几个基于.NET 框架有可用于帮助实现此目的。 可以使用几乎任何这些 ASP.NET MVC 应用程序中。

对于我们 NerdDinner 的应用程序的目的，我们将使用相对简单，简单的模式，我们会在我们 Dinner 的模型对象上公开 IsValid 属性和 GetRuleViolations() 方法。 IsValid 属性将返回 true 或 false 具体取决于是否所有有效的验证和业务规则。 GetRuleViolations() 方法将返回一组规则的任何错误。

我们将实现 IsValid 和 GetRuleViolations() Dinner 模型通过将"分部类"添加到我们的项目。 分部类可用于将方法/属性/事件添加到维护的 VS 设计器 （如 linq to SQL 设计器生成的 Dinner 类） 的类和帮助避免产生混淆，我们的代码中的工具。 我们可以右键单击 \Models 文件夹中，将新的分部类添加到我们的项目，然后选择"添加新项"菜单命令。 我们然后可以选择在"添加新项"对话框的"类"模板并将其命名 Dinner.cs。

![](build-a-model-with-business-rule-validations/_static/image11.png)

单击"添加"按钮将 Dinner.cs 文件添加到我们的项目，并在 IDE 中打开它。 我们然后可以实现基本的规则验证强制框架，它使用以下代码：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

有关上述代码中的几个注意事项：

- Dinner 类开头，但使用 partial 关键字 – 这意味着它所包含的代码将是与生成/维护的类结合使用 linq to SQL 设计器，编译到单个类。
- RuleViolation 类是一个帮助器类，我们将添加到项目，可用于提供有关规则冲突的详细信息。
- Dinner.GetRuleViolations() 方法使我们验证规则和业务规则进行评估 （我们将马上要实现它们）。 然后返回一系列 RuleViolation 对象，它提供有关规则的任何错误的更多详细信息。
- Dinner.IsValid 属性提供了一个便利的帮助器属性，指示 Dinner 对象是否具有任何活动 RuleViolations。 它可以主动检查由开发人员在任何时候使用 Dinner 对象 （并不会引发异常）。
- Dinner.OnValidate() 分部方法是 LINQ to SQL 提供，可用于 Dinner 对象由要保留在数据库中的任何时间收到通知的挂钩。 上述我们 OnValidate() 实现可确保 Dinner 有没有 RuleViolations，之后再将其保存。 如果处于无效状态，它会引发异常，这将导致 LINQ to SQL 中止事务。

这种方法提供了一个简单的框架，我们可以将验证和到业务规则集成。 现在让我们添加到我们的 GetRuleViolations() 方法的规则如下：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

我们将使用 C#"yield return"的功能可返回任何 RuleViolations 的序列。 上面的第六个规则检查只是强制执行我们 Dinner 的字符串属性不能为 null 或为空。 最后一条规则是一些更有趣，并调用 PhoneValidator.IsValidNumber() 帮助器方法，我们可以将添加到我们的项目以验证 contactphone 编号格式匹配 Dinner 国家/地区。

我们可以使用。NET 的正则表达式支持，以实现此电话验证支持。 下面是一个简单的 PhoneValidator 实现，我们可以添加到项目，使我们可以添加特定于国家/地区的正则表达式模式检查：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>处理验证和业务逻辑冲突

现在，我们已添加上述验证和业务规则代码中，我们尝试创建或更新 Dinner 任何时候，我们验证逻辑规则将进行评估和强制执行。

开发人员可以编写的代码类似下面主动确定 Dinner 对象是否有效，并检索在其中的所有冲突，并且不会引发任何异常的列表：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

如果我们尝试在无效状态中保存 Dinner，当我们在 DinnerRepository 上调用 save （） 方法时将引发异常。 这是因为 LINQ to SQL 会自动调用我们 Dinner.OnValidate() 分部方法之前它将保存 Dinner 的更改，我们将代码添加到 Dinner.OnValidate() 引发异常，如果在 Dinner 中存在任何规则冲突。 我们可以捕获此异常和被动检索冲突后，若要修复的列表：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

因为在我们的模型层，而不是在 UI 层，并实现我们验证和业务规则，它们将应用和我们的应用程序中的所有方案中都使用。 我们稍后可以更改或添加业务规则，具有适用于我们的 Dinner 对象遵循它们的所有代码。

可以灵活地更改业务规则在一个位置，而无需波及整个应用程序和 UI 逻辑，这些更改就编写良好的应用程序和的 MVC 框架可帮助支持权益的登录。

### <a name="next-step"></a>下一步

我们现在有一个模型，我们可以使用查询和更新我们的数据库。

现在让我们添加一些控制器和视图的项目的我们可用于构建在其周围的 HTML UI 体验。

> [!div class="step-by-step"]
> [上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
