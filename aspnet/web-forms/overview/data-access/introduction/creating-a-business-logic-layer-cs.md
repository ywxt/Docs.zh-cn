---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
title: 创建业务逻辑层 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何集中用作数据交换 t 之间的中介业务逻辑层 (BLL) 到您的业务规则...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 85554606-47cb-4e4f-9848-eed9da579056
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 191b85b4e57055041d3fc281a9ff30e397b51ec7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373141"
---
<a name="creating-a-business-logic-layer-c"></a>创建业务逻辑层 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_2_CS.exe)或[下载 PDF](creating-a-business-logic-layer-cs/_static/datatutorial02cs1.pdf)

> 在本教程中，我们将了解如何集中用作表示层 DAL 之间交换数据的中介业务逻辑层 (BLL) 到您的业务规则。


## <a name="introduction"></a>介绍

数据访问层 (DAL) 中创建[第一篇教程](creating-a-data-access-layer-cs.md)完全分隔数据访问逻辑与表示逻辑。 但是，尽管 DAL 从表示层清楚地划分数据访问详细信息，它不会强制任何可能适用的业务规则。 例如，我们的应用程序我们可能希望禁止`CategoryID`或`SupplierID`的字段`Products`表，以修改`Discontinued`字段设置为 1，或者我们可能想要强制实施资历规则，禁止情况下，员工的人在其之后雇佣的管理。 另一个常见方案是属于特定角色的授权可能只有用户可以删除产品，或者可以更改`UnitPrice`值。

在本教程中，我们将了解如何集中用作表示层 DAL 之间交换数据的中介业务逻辑层 (BLL) 到这些业务规则。 在实际应用程序中，BLL 应实现作为一个单独的类库项目;但是，对于这些教程，我们将实现 BLL 作为一系列中的类我们`App_Code`文件夹，以便简化项目结构。 图 1 说明在表示层、 BLL 和 DAL 的体系结构关系。


![BLL 将表示层与数据访问层隔离和实施业务规则](creating-a-business-logic-layer-cs/_static/image1.png)

**图 1**: BLL 将表示层与数据访问层隔离和实施业务规则


## <a name="step-1-creating-the-bll-classes"></a>步骤 1： 创建 BLL 类

我们 BLL 将组成以下四个类，一个用于在 DAL; 每个 TableAdapter每个 BLL 类将具有用于检索、 插入、 更新和删除从 DAL，将相应的业务规则应用中各自的 TableAdapter 方法。

来更顺利分隔 DAL 和 BLL 相关的类，让我们创建两个子文件夹中的`App_Code`文件夹中，`DAL`和`BLL`。 只需右键单击`App_Code`在解决方案资源管理器中的文件夹，然后选择新文件夹。 创建以下两个文件夹之后, 将移到第一个教程中创建的类型化数据集`DAL`子文件夹。

接下来，创建四个 BLL 类文件中的`BLL`子文件夹。 若要完成此操作，右键单击`BLL`子文件夹中，选择添加新项，然后选择类模板。 命名的四个类`ProductsBLL`， `CategoriesBLL`， `SuppliersBLL`，和`EmployeesBLL`。


![将四个新类添加到 App_Code 文件夹](creating-a-business-logic-layer-cs/_static/image2.png)

**图 2**： 添加到四个新类`App_Code`文件夹


接下来，让我们将方法添加到每个类仅封装定义为从第一个教程 Tableadapter 的方法。 现在，这些方法将只需直接调用到 DAL;我们将返回更高版本中添加任何所需的业务逻辑。

> [!NOTE]
> 如果使用 Visual Studio Standard Edition 或更高版本 (即，正在*不*使用 Visual Web Developer)，您可以根据需要设计您直观地使用的类[类设计器](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)。 请参阅[类设计器博客](https://blogs.msdn.com/classdesigner/default.aspx)的 Visual Studio 中的此新功能的详细信息。


有关`ProductsBLL`我们需要添加总共七种方法的类：

- `GetProducts()` 返回所有产品
- `GetProductByProductID(productID)` 返回具有指定的产品 ID 的产品
- `GetProductsByCategoryID(categoryID)` 返回从指定的类别的所有产品
- `GetProductsBySupplier(supplierID)` 返回指定供应商提供的所有产品
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` 将新产品插入到数据库中使用的值传入的程序;返回`ProductID`新插入记录的值
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` 更新现有产品使用传入的值; 在数据库中返回`true`精确一行已更新，如果`false`否则为
- `DeleteProduct(productID)` 从数据库中删除指定的产品

ProductsBLL.cs


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample1.cs)]

只需返回数据的方法`GetProducts`， `GetProductByProductID`， `GetProductsByCategoryID`，和`GetProductBySuppliersID`是非常简单，因为它们只是向下调用 DAL 到。 尽管在某些情况下可能需要实现的业务规则在此级别 （例如，基于当前登录的用户或用户所属的角色的授权规则），我们将只是将这些方法作为-是。 有关这些方法，然后，BLL 用作只是通过该表示层所访问的数据访问层中的基础数据的代理。

`AddProduct`和`UpdateProduct`方法同时作为参数采用各种产品字段的值并添加一个新的产品或分别更新一个现有。 因为其中许多`Product`表的列可以接受`NULL`值 (`CategoryID`， `SupplierID`，并`UnitPrice`，仅举几例)，这些输入参数`AddProduct`和`UpdateProduct`映射到此类列使用[为 null 的类型](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)。 可以为 null 的类型不熟悉.NET 2.0 和，该值指示是否是值类型，而是提供一种技术`null`。 在 C# 中可以标记值类型为 null 的类型通过添加`?`在类型后面 (如`int? x;`)。 请参阅[为 Null 的类型](https://msdn.microsoft.com/library/1t3y8s4s.aspx)主题中[C# 编程指南](https://msdn.microsoft.com/library/67ef8sbd%28VS.80%29.aspx)有关详细信息。

所有三个方法返回布尔值，该值指示行是否已插入、 更新或删除，因为该操作不可能会导致受影响的行。 例如，如果页面开发人员调用`DeleteProduct`传入`ProductID`不存在产品，`DELETE`向数据库发出语句会有任何影响，因此`DeleteProduct`方法将返回`false`。

请注意，当添加一个新的产品或更新现有我们需要新的或修改产品的字段值中的标量而不是接受列表作为`ProductsRow`实例。 选择这种方法是因为`ProductsRow`类派生自 ADO.NET`DataRow`类，其不具有默认的无参数构造函数。 若要创建一个新`ProductsRow`实例，必须先创建`ProductsDataTable`实例，然后调用其`NewProductRow()`方法 (中执行的操作`AddProduct`)。 我们打开到插入和更新使用 ObjectDataSource 产品时，这种缺陷 rears 它的头。 简单地说，ObjectDataSource 将尝试创建的输入参数的实例。 如果 BLL 方法需要`ProductsRow`实例，ObjectDataSource 将尝试创建一个，但由于缺少默认的无参数构造函数会失败。 有关此问题的详细信息，请参阅以下两个 ASP.NET 论坛帖子： [Strongly-Typed 数据集更新 Objectdatasource](https://forums.asp.net/1098630/ShowPost.aspx)，和[问题与 ObjectDataSource 和 Strongly-Typed 数据集](https://forums.asp.net/1048212/ShowPost.aspx).

接下来，在这种`AddProduct`并`UpdateProduct`，该代码会创建`ProductsRow`实例并填充它只是传递中的值。 将值分配到 DataRow 的 Datacolumn 会发生各种字段级验证检查。 因此，手动将传入的值返回放入 DataRow 有助于确保传递给 BLL 方法的数据的有效性。 遗憾的是由 Visual Studio 生成的强类型化 DataRow 类不使用 null 的类型。 相反，以指示应对应 DataRow 中的特定 DataColumn`NULL`数据库的值，必须使用`SetColumnNameNull()`方法。

在中`UpdateProduct`我们首先在要更新使用的产品中加载`GetProductByProductID(productID)`。 虽然这可能看起来与数据库的不必要行程，此额外经历一次将证明值得在将来的教程中，探索了开放式并发。 乐观并发是一种技术，以确保要同时处理相同数据的两个用户避免意外覆盖彼此发生的变化。 获取整个记录还使在仅修改 DataRow 的列子集的 BLL 中创建的更新方法更加容易。 我们将探讨当`SuppliersBLL`我们会看到此类示例的类。

最后，请注意，`ProductsBLL`类具有[DataObject 属性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx)对其应用 (`[System.ComponentModel.DataObject]`之前的文件的顶部附近 class 语句的语法) 以及这些方法没有[DataObjectMethodAttribute 属性](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)。 `DataObject`特性标记为适合绑定到的对象的类[ObjectDataSource 控件](https://msdn.microsoft.com/library/9a4kyhcx.aspx)，而`DataObjectMethodAttribute`指示此方法的用途。 我们将看到在将来教程，ASP.NET 2.0 ObjectDataSource 便于以声明方式访问类中的数据。 若要帮助筛选可能的类为 ObjectDataSource 的向导中要绑定到列表，默认情况下，只有标记为这些类`DataObjects`向导的下拉列表中所示。 `ProductsBLL`类也只是将工作而无需这些属性，但添加它们可以更轻松地使用 ObjectDataSource 的向导中。

## <a name="adding-the-other-classes"></a>添加其他类

使用`ProductsBLL`类完成后，我们仍需要添加用于处理类别、 供应商和员工的类。 请花费片刻时间来创建以下类和方法使用从上面的示例中的概念：

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

值得注意的一个方法是`SuppliersBLL`类的`UpdateSupplierAddress`方法。 此方法用于更新只是供应商的地址信息提供的接口。 此方法在内部，在读取`SupplierDataRow`的指定对象的`supplierID`(使用`GetSupplierBySupplierID`)，设置其与地址相关的属性，然后调入`SupplierDataTable`的`Update`方法。 `UpdateSupplierAddress`方法如下所示：


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample2.cs)]

请参阅本文的下载完整的 BLL 类实现的。

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>步骤 2： 通过 BLL 类访问类型化数据集

第一个教程中我们已了解示例直接使用的类型化数据集以编程方式，但添加了我们 BLL 类，与表示层应针对工作 BLL 相反。 在中`AllProducts.aspx`从第一个教程中，示例`ProductsTableAdapter`用于将产品列表绑定到 GridView 中后，如下面的代码中所示：


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample3.cs)]

若要使用新的 BLL 类，所有需要的更改是第一行代码来代替`ProductsTableAdapter`对象与`ProductBLL`对象：


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample4.cs)]

此外可以通过使用对象数据源 （如可能是类型化数据集） 以声明方式访问的 BLL 类。 我们将讨论 ObjectDataSource 中更详细地介绍以下教程中。


[![在 GridView 中显示的产品列表](creating-a-business-logic-layer-cs/_static/image4.png)](creating-a-business-logic-layer-cs/_static/image3.png)

**图 3**： 在 GridView 中显示的产品列表 ([单击以查看实际尺寸的图像](creating-a-business-logic-layer-cs/_static/image5.png))


## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>步骤 3： 将字段级验证添加到 DataRow 类

字段级验证会检查与插入或更新时的业务对象的属性值相关。 产品的某些字段级验证规则包括：

- `ProductName`字段必须为 40 个字符或更少字符
- `QuantityPerUnit`字段必须为 20 个字符或更少字符
- `ProductID`， `ProductName`，和`Discontinued`字段是必需的但所有其他字段为可选
- `UnitPrice`， `UnitsInStock`， `UnitsOnOrder`，和`ReorderLevel`字段必须为大于或等于零

这些规则可以和应表示在数据库级别。 字符的限制`ProductName`并`QuantityPerUnit`字段中的这些列的数据类型由捕获`Products`表 (`nvarchar(40)`和`nvarchar(20)`分别)。 如果数据库表列允许字段必选和可选来表示`NULL`s。 四个[check 约束](https://msdn.microsoft.com/library/ms188258.aspx)存在，确保只有大于或等于零的值可发出到`UnitPrice`， `UnitsInStock`， `UnitsOnOrder`，或`ReorderLevel`列。

除了强制实施这些规则应用于数据库它们应还在进行强制数据集级别。 事实上，字段长度和一个值是必需还是可选已捕获的 Datacolumn 的每个 DataTable 的组。 若要查看自动提供的现有字段级别验证，请转到数据集设计器、 从 DataTables 之一中选择字段，然后转到属性窗口。 如图 4 所示，`QuantityPerUnit`中的 DataColumn `ProductsDataTable` 20 个字符的最大长度且允许`NULL`值。 如果我们尝试设置`ProductsDataRow`的`QuantityPerUnit`属性的长度超过 20 个字符的字符串值`ArgumentException`将引发。


[![DataColumn 提供基本字段级验证](creating-a-business-logic-layer-cs/_static/image7.png)](creating-a-business-logic-layer-cs/_static/image6.png)

**图 4**: DataColumn 提供基本字段级验证 ([单击以查看实际尺寸的图像](creating-a-business-logic-layer-cs/_static/image8.png))


遗憾的是，我们不能指定边界检查，如`UnitPrice`值必须大于或等于零，通过属性窗口。 为了提供此类型的字段级验证我们需要创建的 DataTable 的事件处理程序[ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx)事件。 如中所述[前面的教程](creating-a-data-access-layer-cs.md)，可以通过使用分部类扩展由类型化数据集创建的数据集、 数据表和 DataRow 对象。 使用这种方法，我们可以创建`ColumnChanging`事件处理程序`ProductsDataTable`类。 首先创建中的类`App_Code`文件夹名为`ProductsDataTable.ColumnChanging.cs`。


[![将新类添加到 App_Code 文件夹](creating-a-business-logic-layer-cs/_static/image10.png)](creating-a-business-logic-layer-cs/_static/image9.png)

**图 5**： 添加新类中，以便`App_Code`文件夹 ([单击以查看实际尺寸的图像](creating-a-business-logic-layer-cs/_static/image11.png))


接下来，创建的事件处理程序`ColumnChanging`事件可确保`UnitPrice`， `UnitsInStock`， `UnitsOnOrder`，并`ReorderLevel`列的值 (如果不是`NULL`) 是大于或等于零。 如果任何此类列不在范围内，则引发`ArgumentException`。

ProductsDataTable.ColumnChanging.cs


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample5.cs)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>步骤 4： 将自定义业务规则添加到 BLL 的类

除了字段级验证可能需要高级自定义业务规则来如涉及不同的实体或级别的单个列不表达的概念：

- 如果产品缺货，其`UnitPrice`无法更新
- 未成年人的员工的国家/地区必须与他们的经理的居住的国家/地区相同
- 如果它是唯一的产品的供应商提供，不能停止产品

BLL 类应包含检查，以确保对应用程序的业务规则的遵从性。 这些检查可以直接添加到它们适用于的方法。

假设我们的业务规则规定，产品无法将标记已停止使用是否它是唯一的产品从给定的供应商。 也就是说，如果产品*X*是唯一的产品，我们从供应商购买*Y*，我们无法将标记*X*如弃用; 如果有，但是，供应商*Y*提供三种产品，我们*A*， *B*，并*C*，然后我们可以将任何标记，并停止使用所有这些作为。 始终不被对齐的奇数的业务规则，但业务规则和常识 ！

若要执行此业务规则中的`UpdateProducts`方法，我们将首先检查是否`Discontinued`已设置为`true`，因此，我们将调用`GetProductsBySupplierID`来确定多少产品我们从购买此产品的供应商。 如果只有一个产品购买此供应商，我们引发`ApplicationException`。


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample6.cs)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>响应的表示层中的验证错误

从表示层调用 BLL 时我们可以决定是否尝试处理可能会引发或让他们归因于 ASP.NET 的任何异常 (这将引发`HttpApplication`的`Error`事件)。 若要处理的异常时以编程方式使用 BLL，我们可以使用[try...catch](https://msdn.microsoft.com/library/0yd65esw.aspx)块，如以下示例所示：


[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample7.cs)]

因为我们会在将来的教程、 处理异常向上冒泡 BLL 时使用的数据从 Web 控件的插入，更新，或删除数据可以直接在事件处理程序而不是无需换行中的代码中处理`try...catch`块。

## <a name="summary"></a>总结

良好的应用程序构建到不同的层，其中每个封装一个特定的角色。 在本系列文章的第一个教程中，我们将创建使用类型化数据集; 的数据访问层在本教程中我们构建业务逻辑层作为一系列类在应用程序中的`App_Code`向下调用 DAL 到的文件夹。 BLL 实现我们的应用程序的字段级别和业务级逻辑。 除了创建单独的 BLL，与我们在本教程中的另一个选项是扩展 Tableadapter 的方法通过使用分部类。 但是，使用此方法不允许我们重写现有方法也不会其单独的 DAL 和我们 BLL 清晰地为我们在本文中所用的方法。

DAL 和 BLL 完成后，我们准备好在我们的表示层上启动。 在中[下一教程](master-pages-and-site-navigation-cs.md)我们将会从数据访问主题简要 detour，并定义在整个教程中使用一致的页面布局。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Liz Shulok、 Dennis Patterson、 Carlos Santos 和 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](creating-a-data-access-layer-cs.md)
> [下一页](master-pages-and-site-navigation-cs.md)
