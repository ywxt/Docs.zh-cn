---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 什么是 Entity Framework 4.0 中的新增功能 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: aspnetcontent
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 960aaf7aa7c2cff5c51079ecfe50031fa82d5508
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827836"
---
<a name="whats-new-in-the-entity-framework-40"></a>什么是 Entity Framework 4.0 中的新增功能
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。 如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。


在上一教程中，您将看到一些用于使用实体框架的 web 应用程序的性能的方法。 本教程介绍了一些 Entity Framework 的版本 4 中的最重要新功能，而且它链接到提供的所有新功能的更完整介绍的资源。 在本教程中突出显示的功能包括：

- 外键关联。
- 正在执行用户定义的 SQL 命令。
- 模型优先开发。
- POCO 支持。

此外，本教程将简要介绍*代码优先的开发*，实体框架的下一个版本中即将推出的功能。

若要开始本教程，启动 Visual Studio 并打开在您使用在上一教程中的 Contoso University web 应用程序。

## <a name="foreign-key-associations"></a>外键关联

Entity Framework 3.5 版包含导航属性，但它不在数据模型中包括外键属性。 例如，`CourseID`并`StudentID`的列`StudentGrade`表将省略从`StudentGrade`实体。

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

这种方法的原因是，严格地说外, 键是物理实现细节，不属于概念数据模型中。 但是，在实践中，通常很容易地直接访问的外键时处理代码中的实体。

有关如何外键的数据模型中的示例可以简化你的代码，请考虑如何你将获得了对代码*DepartmentsAdd.aspx*页，但它们没有。 在中`Department`实体，`Administrator`属性是对应于一个外键`PersonID`中`Person`实体。 若要建立新系和它的管理员之间的关联，您所要做已设置的值`Administrator`中的属性`ItemInserting`数据绑定控件的事件处理程序：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

不用数据模型中的外键，将处理`Inserting`事件的数据源控件，而不是`ItemInserting`数据绑定控件，以获取对实体本身的引用，该实体添加到实体集之前的事件。 该引用后，你建立使用类似于下面的示例中的代码的关联：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

正如您可以在实体框架团队看到[外键关联上的博客文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)，其他情况下，代码复杂性的区别是要多得多。 为了满足这些面向更愿意忍受为了代码较简单的概念数据模型中的实现详细信息的需求，实体框架将会提供的数据模型中包括外键的选项。

在实体框架术语中，如果数据模型中包括外键使用的*外键关联*，并且如果排除正在使用的外键*独立关联*。

## <a name="executing-user-defined-sql-commands"></a>执行用户定义的 SQL 命令

在早期版本的实体框架中，没有简单方法来动态创建自己的 SQL 命令并运行它们。 实体框架动态生成的 SQL 命令，或者您必须创建一个存储的过程并将其作为函数导入。 添加了版本 4`ExecuteStoreQuery`并`ExecuteStoreCommand`方法`ObjectContext`使你更轻松地直接向数据库传递任何查询的类。

假设 Contoso 大学管理员想要能够在数据库中执行大容量更改，而无需经历创建存储的过程并导入数据模型的过程。 其第一个请求是用于将允许他们更改数据库中的所有课程的可修读人数的页面。 在 web 页上，他们想要能够输入一个数字，以用于将的值相乘，每个`Course`行的`Credits`列。

创建新的页面，使用*Site.Master*母版页并将其命名*UpdateCredits.aspx*。 然后添加以下标记到`Content`名为控件`Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

此标记创建`TextBox`控制用户可以在其中输入乘数值，`Button`才能执行该命令中，单击控件和一个`Label`控件用于指示受影响的行数。

打开*UpdateCredits.aspx.cs*，并添加以下`using`语句，并为按钮的处理程序`Click`事件：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

此代码执行 SQL`Update`命令在文本框中使用的值，并使用标签来显示受影响的行数。 运行该页面之前，请运行*Courses.aspx*页面以获取"before"图片的一些数据。

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

运行*UpdateCredits.aspx*，作为乘数，输入"10"，然后单击**Execute**。

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

运行*Courses.aspx*页上再次看到已更改的数据。

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(如果你想要在设置回其原始值的可修读人数*UpdateCredits.aspx.cs*更改`Credits * {0}`到`Credits / {0}`，然后重新运行页上，输入 10 与除数的符号。)

有关执行查询，以在代码中定义的详细信息，请参阅[如何： 直接执行命令针对数据源](https://msdn.microsoft.com/library/ee358769.aspx)。

## <a name="model-first-development"></a>模型优先开发

在这些演练将首先创建数据库和数据库结构所基于的数据模型，则生成。 Entity Framework 4 可以改为开始使用数据模型，生成基于数据模型结构的数据库。 如果要创建应用程序数据库已不存在，模型为先的方法，可创建实体和关系从概念上讲适合应用程序，而不需担心如何物理实现详细信息. （也不例外仅通过初始阶段的开发，但是。 最终数据库将创建将生产数据，并且让模型中重新创建它将不再是实际;此时，您会回数据库为先的方法。）

在本教程的此部分中，将创建一个简单数据模型并从中生成数据库。

在中**解决方案资源管理器**，右键单击*DAL*文件夹，然后选择**添加新项**。 在中**添加新项**对话框中的**已安装的模板**选择**数据**，然后选择**ADO.NET 实体数据模型**模板. 将新文件命名*AlumniAssociationModel.edmx*然后单击**添加**。

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

这将启动实体数据模型向导。 在中**选择模型内容**步骤中，选择**空模型**，然后单击**完成**。

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

**实体数据模型设计器**打开与空白设计图面。 拖动**实体**项从**工具箱**拖到设计图面。

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

更改从实体名称`Entity1`到`Alumnus`，更改`Id`属性名称设置为`AlumnusId`，并添加名为的新标量属性`Name`。 若要添加新属性，您可以更改的名称后按 Enter`Id`列中，或右键单击该实体，然后选择**添加标量属性**。 新的属性的默认类型是`String`，这样很好此简单演示，但当然可以更改中的数据类型等**属性**窗口。

创建相同的方式的另一个实体并将其命名`Donation`。 更改`Id`属性设置为`DonationId`并添加名为的标量属性`DateAndAmount`。

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

若要添加这两个实体之间的关联，请右键单击`Alumnus`实体中，选择**添加**，然后选择**关联**。

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

中的默认值**添加关联**是您需要的对话框 （一个多，包括导航属性，包括外键），因此只需单击**确定**。

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

在设计器添加一条关联连线和外键属性。

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

现在你已准备好创建数据库。 右键单击设计图面，然后选择**根据模型生成数据库**。

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

这将启动生成数据库向导。 （如果看到警告，指示未映射实体，你可以忽略这些暂时。）

在中**选择数据连接**步骤中，单击**新的连接**。

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

在中**连接属性**对话框中选择本地 SQL Server Express 实例，数据库命名为`AlumniAsssociation`。

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

单击**是**时，会询问你是否想要创建数据库。 当**选择数据连接**再次显示步骤中，单击**下一步**。

在中**摘要和设置**步骤中，单击**完成**。

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

一个 *.sql*创建为文件数据定义语言 (DDL) 命令，但命令尚未运行。

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

使用一种工具，如**SQL Server Management Studio**运行该脚本并创建表，如可能在创建时已完成`School`数据库[入门教程系列中的第一个教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). （除非您下载此数据库）。

现在，您可以使用`AlumniAssociation`数据模型在您的 web 页你所用的相同方式`School`模型。 若要试用此项，向表中添加一些数据并创建一个网页，显示的数据。

使用**服务器资源管理器**，添加以下行`Alumnus`和`Donation`表。

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

创建一个名为的新 web 页*Alumni.aspx* ，它使用*Site.Master*母版页。 添加到以下标记`Content`名为控件`Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

此标记创建嵌套`GridView`控制，外部显示校友名称和内部显示捐赠日期和数量。

打开*Alumni.aspx.cs*。 添加`using`语句的数据访问层和外部的处理程序`GridView`控件的`RowDataBound`事件：

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

此代码 databinds 内部`GridView`控件并使用`Donations`导航属性的当前行`Alumnus`实体。

运行页。

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(注意： 此页包含在可下载的项目中，但以使其起作用，您必须在数据库中创建本地 SQL Server Express 实例; 在数据库中不包含作为 *.mdf*中的文件*应用\_数据*文件夹。)

有关使用实体框架实体数据模型功能的详细信息，请参阅[Entity Framework 4 模型优先](https://msdn.microsoft.com/data/ff830362.aspx)。

## <a name="poco-support"></a>POCO 支持

当使用域驱动设计方法时，您设计数据类表示数据和与业务域相关的行为。 这些类应是独立于用来存储任何特定技术 （保留） 数据;换而言之，它们应*持久性未知*。 此外，持久性无感知可以使一个类容易进行单元测试因为单元测试项目可以使用的任何持久性技术是最方便进行测试。 Entity Framework 的早期版本提供对持久化透明的支持有限，因为实体类必须继承自`EntityObject`类，并因此包含大量特定于实体框架的功能。

Entity Framework 4 引入了使用不继承的实体类的功能`EntityObject`类，并因此为持久性未知。 在实体框架的上下文中，通常称为类，如这*普通旧 CLR 对象*（POCO 或 Poco）。 您可以手动编写的 POCO 类或可以自动生成基于现有数据模型使用由实体框架提供的文本模板转换工具包 (T4) 模板。

有关使用 Poco 实体框架中的详细信息，请参阅以下资源：

- [使用 POCO 实体](https://msdn.microsoft.com/library/dd456853.aspx)。 这是 Poco，概述以及指向其他文档的更多详细信息的 MSDN 文档。
- [演练： POCO 实体框架的模板](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)这是实体框架开发团队，其中包含指向其他有关 Poco 的博客文章的一篇博客文章。

## <a name="code-first-development"></a>代码优先开发

Entity Framework 4 中的 POCO 支持仍需要创建数据模型，并链接到数据模型的实体类。 实体框架的下一个版本将包含一个称为功能*代码优先的开发*。 此功能，可使用实体框架使用自己的 POCO 类而无需使用数据模型设计器或数据模型 XML 文件。 (因此，此选项也已调用*仅限代码的*;*代码优先*并*仅限代码的*都引用相同的实体框架功能。)

有关使用开发的代码优先方法的详细信息，请参阅以下资源：

- [代码优先的开发使用 Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。 这是由 Scott Guthrie 介绍代码优先开发的博客文章。
- [实体框架开发团队博客-文章标记的 CodeOnly](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [实体框架开发团队博客-文章标记 Code First](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC Music 商店教程-第 4 部分： 模型和数据访问](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [开始使用 MVC 3-第 4 部分： 实体框架代码优先开发](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

此外，生成类似于 Contoso 大学应用程序的应用程序的新 MVC 代码的第一个教程预计在 2011 年春季发布 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>详细信息

这将完成到实体框架和此继续与实体框架教程系列中新增的概述。 有关 Entity Framework 4，这里没有涉及的新功能的详细信息，请参阅以下资源：

- [What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN 上的 Entity Framework 版本 4 中的新增功能的主题。
- [宣布发布 Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)版本 4 中的新增功能有关的实体框架开发团队的博客文章。

> [!div class="step-by-step"]
> [上一篇](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
