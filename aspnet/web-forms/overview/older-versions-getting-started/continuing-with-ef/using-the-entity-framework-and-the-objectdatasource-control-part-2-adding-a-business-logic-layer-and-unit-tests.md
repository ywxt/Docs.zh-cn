---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 使用实体框架 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 6517f037a03bb520ee4f3b3185a255b0eaa9de9a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834143"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>使用实体框架 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。 如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。


在上一教程中创建使用实体框架的 n 层 web 应用程序和`ObjectDataSource`控件。 本教程演示如何添加业务逻辑，同时保持业务逻辑层 (BLL) 和数据访问层 (DAL) 是独立的以及如何为 BLL 创建自动化的单元测试。

在本教程中将完成以下任务：

- 创建存储库接口声明所需的数据访问方法。
- 存储库类中实现存储库的接口。
- 创建调用存储库类以执行数据访问功能的业务逻辑类。
- 连接`ObjectDataSource`业务逻辑类而不是存储库类的控件。
- 创建单元测试项目和使用内存中集合来存储其数据的存储库类。
- 创建你想要添加到业务逻辑类，然后运行测试并查看其失败的业务逻辑的单元测试。
- 在业务逻辑类中，实现业务逻辑，然后重新运行单元测试并查看它的传递。

您将使用*Departments.aspx*并*DepartmentsAdd.aspx*在上一教程中创建的页。

## <a name="creating-a-repository-interface"></a>创建存储库接口

您将首先创建存储库接口。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

在中*DAL*文件夹中，创建一个新类文件，将其命名*ISchoolRepository.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

该接口定义的一种方法为每个 CRUD （创建、 读取、 更新、 删除） 存储库类中创建的方法。

在中`SchoolRepository`类中*SchoolRepository.cs*，指示此类实现`ISchoolRepository`接口：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>创建业务逻辑类

接下来，你将创建业务逻辑类。 执行此操作，以便可以添加将由执行的业务逻辑`ObjectDataSource`控件，但不会尚未执行的。 现在，新的业务逻辑类将仅执行相同的 CRUD 操作的存储库。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

创建一个新文件夹并将其命名*BLL*。 (在实际应用程序中，业务逻辑层将通常作为实现的类库，一个单独的项目，但为了简化本教程中，BLL 类将保留在项目文件夹中。)

在中*BLL*文件夹中，创建一个新类文件，将其命名*SchoolBL.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

此代码将创建前面在存储库类中，您看到的相同的 CRUD 方法，但调用而不是直接访问的实体框架方法，它在存储库类方法。

保存对存储库类的引用的类变量定义为接口类型，并实例化存储库类的代码包含在两个构造函数。 无参数构造函数将由`ObjectDataSource`控件。 它创建的实例`SchoolRepository`前面创建的类。 另一个构造函数允许实例化业务逻辑类将实现存储库接口的任何对象中传递的任何代码。

调用存储库类和两个构造函数的 CRUD 方法，使其可以与您选择任何后端数据存储区一起使用的业务逻辑类。 业务逻辑类不需要，需要注意的调用类如何持久保存数据。 (此情况通常称作*持久性无感知*。)这有利于进行单元测试，因为你可以连接到使用的内容作为一种简单的存储库实现的业务逻辑类作为内存中`List`集合来存储数据。

> [!NOTE]
> 从技术上讲，实体对象是仍不持久性未知，因为它们从实体框架的继承的类实例化`EntityObject`类。 可以使用完整的持久性无感知*普通旧 CLR 对象*，或*Poco*，来替代继承的对象`EntityObject`类。 使用 Poco 不在本教程的范围。 有关详细信息，请参阅[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) MSDN 网站上。)


现在可以连接`ObjectDataSource`控件添加到业务逻辑类而不是到存储库并验证一切正常就像以前一样。

在中*Departments.aspx*并*DepartmentsAdd.aspx*，更改每个匹配项`TypeName="ContosoUniversity.DAL.SchoolRepository"`到`TypeName="ContosoUniversity.BLL.SchoolBL`"。 (有四个实例中所有。）

运行*Departments.aspx*并*DepartmentsAdd.aspx*页以验证它们仍能够与以前一样。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>创建单元测试项目和存储库实现

将新项目添加到解决方案： 使用**测试项目**模板，并将其命名`ContosoUniversity.Tests`。

在测试项目中，添加对的引用`System.Data.Entity`并添加到项目引用`ContosoUniversity`项目。

现在可以创建将用于单元测试的存储库类。 此存储库的数据存储将在类中。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

在测试项目中，创建一个新类文件，将其命名*MockSchoolRepository.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

此存储库类将具有与直接访问 Entity Framework 相同的 CRUD 方法，但它们适用于`List`内存而不是与数据库中的集合。 这简化了安装和验证业务逻辑类的单元测试的测试类。

## <a name="creating-unit-tests"></a>创建单元测试

**测试**项目模板创建存根 （stub） 单元测试类，并将下一个任务是通过的业务逻辑的你想要添加到业务逻辑类向其添加单元测试方法中修改此类。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso 大学，任何单个 instructor 只能单个部门的管理员，您需要添加业务逻辑以强制实施此规则。 首先，将通过添加测试和运行测试后，若要查看这些失败。 然后，将添加代码，并重新运行测试，预期会看到它们通过。

打开*UnitTest1.cs*文件，并添加`using`ContosoUniversity 项目中创建业务逻辑和数据访问层的语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

替换为`TestMethod1`方法使用以下方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL`方法创建的存储库类创建的单元测试项目，然后将其传递到业务逻辑类的新实例的一个实例。 然后，该方法使用业务逻辑类在测试方法中插入三个可以使用的部门。

测试方法验证业务逻辑类引发异常，如果有人试图插入新系与现有院系，作为同一管理员或者有人尝试通过将其设置为一个人的 ID 来更新部门的管理员谁已经是另一部门的管理员。

你尚未创建异常类，因此此代码将不进行编译。 若要获取其进行编译，请右键单击`DuplicateAdministratorException`，然后选择**生成**，然后**类**。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

这将创建一个类中的测试项目，您可以删除在主项目中创建的异常类后。 和实现业务逻辑。

运行测试项目。 按预期运行，则测试失败。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>添加业务逻辑，以使测试通过

接下来，将实现使我们无法设置为某个部门的管理员已经是另一部门的管理员的人员的业务逻辑。 将业务逻辑层中，从引发异常，然后将其表示层中捕获如果用户编辑院系，并单击**更新**选择已是管理员的人后。 （你还可以从下拉列表中的用户已是管理员之前呈现页上，, 删除教师，但此处的目的是要使用业务逻辑层。)

首先创建在用户尝试使多个部门的管理员的一名讲师时将引发的异常类。 在主项目中，创建新的类文件中*BLL*文件夹中，其命名*DuplicateAdministratorException.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

现在，删除临时*DuplicateAdministratorException.cs*中创建测试项目之前为了能够编译的文件。

在主项目中，打开*SchoolBL.cs*文件，并添加以下方法，以便包含验证逻辑。 （代码将引用你将更高版本创建的方法。）

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

要插入或更新时，将调用此方法`Department`以检查另一部门是否已具有相同的管理员的实体。

该代码调用方法要搜索的数据库`Department`具有相同的实体`Administrator`作为正在插入或更新的实体的属性值。 如果找到一个对象，该代码将引发异常。 不进行验证检查是必需的如果正在插入或更新的实体不具有`Administrator`如果在更新过程中调用该方法，将引发值和任何异常并`Department`找到匹配项的实体`Department`实体正在更新。

调用中的新方法`Insert`和`Update`方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

在中*ISchoolRepository.cs*，添加新的数据访问方法的以下声明：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

在中*SchoolRepository.cs*，添加以下`using`语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

在中*SchoolRepository.cs*，添加以下新的数据访问方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

此代码检索`Department`具有指定的管理员的实体。 可以看到只有一个部门和 （如果有）。 但是，由于没有约束内置到数据库中，返回类型是集合找到多个部门的情况下。

默认情况下，对象上下文从数据库检索实体时，它跟踪的它们在其对象状态管理器中。 `MergeOption.NoTracking`参数指定此查询将无法完成此跟踪。 这是必需的因为查询可能返回确切想要更新的实体，然后您就会无法附加该实体。 例如，如果您编辑在历史记录院系*Departments.aspx*页并将管理员保留不变，此查询将返回历史系。 如果`NoTracking`未设置，对象上下文将其对象状态管理器中已有的历史记录 department 实体。 对象上下文附加时重新创建从视图状态的历史记录 department 实体，将引发异常，指示`"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`。

(为指定的替代方法`MergeOption.NoTracking`，可以创建新的对象上下文只需为此查询。 因为新的对象上下文会有其自己的对象状态管理器，会有不会发生冲突时调用`Attach`方法。 新的对象上下文将与原始对象上下文中，共享元数据和数据库连接，因此此备用方法的性能损失最少。 但是，会在这里，所示的方法引入`NoTracking`选项，您会发现在其他上下文中非常有用。 `NoTracking`讨论选项进一步在本系列中下一个教程。)

在测试项目中，将添加到新的数据访问方法*MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

此代码使用 LINQ 来执行相同的数据选择的`ContosoUniversity`项目存储库使用 LINQ to Entities 的。

再次运行测试项目。 这次测试通过了。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>处理的异常对象数据源

在中`ContosoUniversity`项目中，运行*Departments.aspx*页上，并尝试将某个部门的管理员更改的人已经是另一部门的管理员。 （请记住，你只能编辑部门添加在本教程中，因为在数据库恢复包含无效的数据预加载。）获取以下服务器错误页：

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

您不希望用户看到错误页上，此类，因此需要添加错误处理代码。 打开*Departments.aspx*并指定的处理程序`OnUpdated`事件的`DepartmentsObjectDataSource`。 `ObjectDataSource`现在开始标记类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

在中*Departments.aspx.cs*，添加以下`using`语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

添加以下处理程序`Updated`事件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

如果`ObjectDataSource`控制捕获异常，当其尝试执行更新时，它将异常传递事件参数中 (`e`) 向此处理程序。 在处理程序中的代码检查异常是否重复管理员异常。 如果是，代码将创建包含的错误消息的验证程序控件`ValidationSummary`控件来显示。

运行页面并尝试再次使人成为两个部门的管理员。 这一次`ValidationSummary`控件将显示一条错误消息。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

进行到类似的更改*DepartmentsAdd.aspx*页。 在中*DepartmentsAdd.aspx*，指定的处理程序`OnInserted`事件的`DepartmentsObjectDataSource`。 所得的标记将类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

在中*DepartmentsAdd.aspx.cs*，将同一`using`语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

添加以下事件处理程序：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

现在可以测试*DepartmentsAdd.aspx.cs*页以验证它也可以正确处理尝试使多个部门的管理员的人。

这将完成对实现使用的存储库模式引入`ObjectDataSource`使用实体框架的控件。 有关存储库模式和可测试性的详细信息，请参阅 MSDN 白皮书[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)。

以下教程中你将了解如何添加排序和筛选的应用程序的功能。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [下一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
