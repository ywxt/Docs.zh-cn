---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 创建数据访问层 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: e6ec385c6a4a5507ffae726157f7d52e9c5605da
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826028"
---
<a name="create-the-data-access-layer"></a>创建数据访问层
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


本教程介绍如何创建、 访问和查看使用 ASP.NET Web 窗体和 Entity Framework Code First 数据库中的数据。 本教程基于上一教程"创建项目"，而是 Wingtip Toy 存储教程系列的一部分。 完成本教程后，您便会生成一组中的数据访问类*模型*项目文件夹中的。

## <a name="what-youll-learn"></a>你将学习：

- 如何创建数据模型。
- 如何初始化和设置数据库的种子。
- 如何更新和应用程序配置为支持的数据库。

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>以下是本教程中引入的功能：

- 实体框架代码优先
- LocalDB
- 数据注释

## <a name="creating-the-data-models"></a>创建数据模型

[实体框架](https://msdn.microsoft.com/data/aa937723)是一种对象关系映射 (ORM) 框架。 它允许你为对象，消除了通常需要编写数据访问代码的大部分处理关系数据。 使用实体框架，可以发出查询使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)，然后检索和操作数据作为强类型化对象。 LINQ 提供了用于查询和更新数据的模式。 使用实体框架，可专注于创建你的应用程序的其余部分，而不是专注于数据访问基础知识。 稍后在本系列教程中我们将介绍如何使用数据来填充导航和产品的查询。

实体框架支持名为开发范例*Code First*。 代码优先让您可以定义数据模型使用的类。 类是一个构造，它使您能够创建自己的自定义类型的其他类型、 方法和事件变量组合在一起。 可以将类映射到现有数据库，也可以使用它们来生成数据库。 在本教程中，将通过编写数据模型类来创建数据模型。 然后，将允许从这些新类动态创建数据库的实体框架。

您将首先创建定义 Web 窗体应用程序的数据模型的实体类。 然后您将创建上下文类，其管理的实体类并提供对数据库的数据访问。 此外将创建一个初始值设定项类，它将用于填充数据库。

### <a name="entity-framework-and-references"></a>实体框架和引用

默认情况下，实体框架时包含您创建一个新**ASP.NET Web 应用程序**使用**Web 窗体**模板。 实体框架可以为安装、 卸载，并作为 NuGet 包更新。

此 NuGet 包包括以下**运行时**你的项目中的程序集：

- EntityFramework.dll – 实体框架使用的所有公共运行时代码
- EntityFramework.SqlServer.dll – 实体框架的 Microsoft SQL Server 提供程序

### <a name="entity-classes"></a>实体类

创建定义的数据的架构的类称为实体类。 如果您是初次接触数据库设计，将实体类作为表定义的数据库。 在类中的每个属性指定的数据库的表中的列。 这些类提供面向对象的代码和数据库的关系表结构之间的轻量、 对象关系接口。

在本教程中，您将首先添加表示产品和类别的架构的简单实体类。 产品类将包含每个产品的定义。 每个 product 类的成员的名称将是`ProductID`， `ProductName`， `Description`， `ImagePath`， `UnitPrice`， `CategoryID`，和`Category`。 类别类将包含每个产品可以属于，如汽车、 小船或平面的类别的定义。 每个类别类的成员的名称将是`CategoryID`， `CategoryName`， `Description`，和`Products`。 每个产品将属于一个类别。 这些实体类将添加到项目的现有*模型*文件夹。

1. 在中**解决方案资源管理器**，右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。 

    ![创建数据访问层-新项菜单](create_the_data_access_layer/_static/image1.png)

   随即出现“添加新项”对话框。
2. 下**Visual C#** 从**已安装**左侧窗格中，选择**代码**。 

    ![创建数据访问层-新项菜单](create_the_data_access_layer/_static/image2.png)
3. 选择**类**从中间窗格中，此新类命名*Product.cs*。
4. 单击 **添加**。  
   在编辑器中显示新类文件中。
5. 默认代码替换为以下代码：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 通过重复步骤 1 至 4，但是，命名新类来创建另一个类*Category.cs*和默认代码替换为以下代码：  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

如前面所述，`Category`类的表示用于销售的应用程序的产品类型 (如<a id="a"> </a>&quot;汽车&quot;，&quot;船&quot;， &quot;Rockets&quot;，依次类推)，和`Product`类表示在数据库中的单个产品 (toys)。 每个实例`Product`对象将对应于关系数据库表中的行和每个属性的 Product 类将映射到关系数据库表中的列。 更高版本在本教程中，你将查看数据库中包含的产品数据。

### <a name="data-annotations"></a>数据注释

您可能已经注意到某些类的成员具有属性指定该成员相关的详细信息，如`[ScaffoldColumn(false)]`。 这些是*数据批注*。 数据注释属性可以描述如何验证用户输入，为该成员，以指定格式设置，并指定如何建模时创建的数据库。

### <a name="context-class"></a>Context 类

若要开始使用这些类用于数据访问，必须定义上下文类。 正如前面提到，上下文类管理的实体类 (如`Product`类和`Category`类)，并提供对数据库的数据访问。

此过程添加到的新 C# 上下文类*模型*文件夹。

1. 右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。   
   随即出现“添加新项”对话框。
2. 选择**类**从中间窗格中，其命名*ProductContext.cs*然后单击**添加**。
3. 使用以下代码的类中包含的默认代码替换为：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

此代码将添加`System.Data.Entity`命名空间，以便有权访问的实体框架中，其中包括查询的功能，所有核心功能插入、 更新和删除通过使用强类型化对象数据。

`ProductContext`类表示 Entity Framework 产品的数据库上下文，用于处理提取、 存储和更新`Product`类实例的数据库中。 `ProductContext`类派生自`DbContext`实体框架提供的基类。

### <a name="initializer-class"></a>初始值设定项类

需要运行某些自定义逻辑来初始化数据库第一个时间使用的上下文。 这将允许种子数据添加到数据库，以使您可以立即显示产品和类别。

此过程中添加新 C# 初始值设定项类中的，以便*模型*文件夹。

1. 创建另一个`Class`中*模型*文件夹并将其命名*ProductDatabaseInitializer.cs*。
2. 使用以下代码的类中包含的默认代码替换为：   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

创建和初始化，数据库时，可以看到上述代码中，从`Seed`重写属性，将其设置。 当`Seed`属性设置，类别和产品中的值用于填充数据库。 如果你尝试通过修改上面的代码中创建数据库后更新种子数据，您不会看到任何更新时运行的 Web 应用程序。 上面的代码中使用的实现的原因是`DropCreateDatabaseIfModelChanges`类，以识别在重置种子数据之前是否已更改了模型 （架构）。 如果对不进行任何更改`Category`和`Product`未使用的种子数据重新初始化实体类，该数据库。

> [!NOTE] 
> 
> 如果你想要每次都重新创建的数据库运行该应用程序，可以使用`DropCreateDatabaseAlways`类而不是`DropCreateDatabaseIfModelChanges`类。 但是对于此教程系列中，使用`DropCreateDatabaseIfModelChanges`类。


此时在本教程中，将拥有*模型*具有四个新类和一个默认类文件夹：

![创建 Models 文件夹中的数据访问层-](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>配置应用程序使用的数据模型

现在，已创建表示数据的类，必须配置要使用的类的应用程序。 在中*Global.asax*文件中，您添加初始化模型的代码。 在中*Web.config*文件添加内容数据库，您告诉应用程序的信息将用于存储由新的数据类表示的数据。 *Global.asax*文件可用于处理应用程序事件或方法。 *Web.config*文件，可用于控制 ASP.NET web 应用程序的配置。

#### <a name="updating-the-globalasax-file"></a>正在更新 Global.asax 文件

若要初始化的数据模型中，应用程序启动时，你将更新`Application_Start`处理程序中的*Global.asax.cs*文件。

> [!NOTE] 
> 
> 在解决方案资源管理器，您可以选择*Global.asax*文件或*Global.asax.cs*要编辑文件*Global.asax.cs*文件。


1. 添加以下代码以到黄色突出显示`Application_Start`中的方法*Global.asax.cs*文件。   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 在浏览器必须支持 HTML5，若要查看在浏览器中查看本系列教程时以黄色突出显示的代码。


上述代码中所示，应用程序启动时，应用程序指定访问第一个期间数据将运行初始值设定项。 两个其他命名空间所需的访问权限`Database`对象和`ProductDatabaseInitializer`对象。

 修改 Web.Config 文件 

尽管 Entity Framework Code First 将生成数据库的默认位置中使用种子数据填充数据库时，将你自己的连接信息添加到你的应用程序可以控制数据库位置。 指定此数据库连接时在应用程序中使用的连接字符串*Web.config*根目录下的项目文件。 你可以通过添加新的连接字符串，指示数据库的位置 (*wingtiptoys.mdf*) 在应用程序的数据目录中生成 (*应用\_数据*)，而不是其默认值位置。 进行此更改将允许您查找，以查看在本教程后面的数据库文件。

1. 在中**解决方案资源管理器**，找到并打开*Web.config*文件。
2. 添加到的黄色突出显示的连接字符串`<connectionStrings>`一部分*Web.config*文件，如下所示：  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

第一次运行该应用程序时，它将生成连接字符串指定的位置上的数据库。 但之前运行的应用程序，让我们构建它第一次。

## <a name="building-the-application"></a>生成应用程序

若要确保所有类和更改对 Web 应用程序正常都运行，应生成应用程序。

1. 从**调试**菜单中，选择**生成 WingtipToys**。  
 **输出**窗口将显示，并且如果一切正常，则会看到*成功*消息。  

    ![创建数据访问层-输出 Windows](create_the_data_access_layer/_static/image4.png)

如果在遇到错误，请重新检查上述步骤。 中的信息**输出**窗口将表示哪个文件有问题，并在文件中更改需要的。 此信息将使您可以确定上述步骤的哪部分需要进行审查和修复你的项目中。

## <a name="summary"></a>总结

在本教程中的一系列你已创建数据模型中，以及，添加将用于初始化和设定数据库种子的代码。 你已配置要运行该应用程序时使用的数据模型中的应用程序。

在下一步的教程中，将更新 UI、 添加导航栏中，和从数据库中检索数据。 这将导致自动创建基于本教程中创建的实体类上的数据库。

## <a name="additional-resources"></a>其他资源

[实体框架概述](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET 实体框架的初学者指南](https://msdn.microsoft.com/data/ee712907)   
[代码使用实体框架的第一个开发](http://www.msteched.com/2010/Europe/DEV212)（视频）   
[Code First 关系 Fluent API](https://msdn.microsoft.com/data/hh134698)   
[Code First 数据注释](https://msdn.microsoft.com/data/gg193958)  
[实体框架的工作效率提升](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [上一页](create-the-project.md)
> [下一页](ui_and_navigation.md)
