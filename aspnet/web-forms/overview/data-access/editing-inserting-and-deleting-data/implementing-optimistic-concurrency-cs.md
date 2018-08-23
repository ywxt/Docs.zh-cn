---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: 实现乐观并发 (C#) |Microsoft Docs
author: rick-anderson
description: 对于允许多个用户编辑数据的 web 应用程序，没有在同一时间可能两个用户编辑相同的数据的风险。 在此 tutori...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 700770946caa68fca2b3101dd91a683d10aae052
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833710"
---
<a name="implementing-optimistic-concurrency-c"></a>实现乐观并发 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe)或[下载 PDF](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> 对于允许多个用户编辑数据的 web 应用程序，没有在同一时间可能两个用户编辑相同的数据的风险。 在本教程中，我们将实现乐观并发控制来处理这种风险。


## <a name="introduction"></a>介绍

对于 web 应用程序只允许用户查看数据，或者对于那些包括只有一个用户可修改数据的人员，没有两个并发用户意外覆盖其他人的更改会受到威胁。 对于 web 应用程序允许多个用户更新或删除数据，但是，没有一个用户的修改，以与其他并发用户的冲突的可能性。 而无需部署任何并发策略，当两个用户同时编辑同一个记录，提交她的更改的用户上次将覆盖第一个所做的更改。

例如，假设，两个用户，Jisun 和 Sam，同时也已访问我们允许访问者以更新和删除通过 GridView 控件的产品的应用程序中的页。 同时单击时间大致相同 GridView 中的编辑按钮。 Jisun 产品名称更改为"Chai 茶"，并单击更新按钮。 最终结果是`UPDATE`语句发送到数据库，这会设置*所有*的产品的可更新的字段 (即使 Jisun 仅更新一个字段， `ProductName`)。 在此时间点，数据库将具有值"Chai 茶，"饮料，供应商特殊液体等用于此特定产品的类别。 但是，Sam 的屏幕上 GridView 仍显示产品名称可编辑的 GridView 行中为"Chai"。 几秒钟后 Jisun 的更改已提交，Sam 调味品到更新类别，并单击更新。 这会导致`UPDATE`语句发送到的数据库的设置为"Chai，"产品名称`CategoryID`到相应的饮料类别 ID 和等等。 已覆盖的产品名称 Jisun 的更改。 图 1 以图形方式描绘了这一系列的事件。


[![两个用户同时更新记录时那里一个用户 s 可能更改覆盖其他 s](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**图 1**： 当两个用户同时更新的记录那里 s 可能有一个用户 s 将更改为覆盖其他 s ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image3.png))


同样，当两个用户正在访问页面，一位用户可能撰写时其他用户删除记录。 或者，当用户加载一个页面，在单击删除按钮时，另一个用户可能已修改该记录的内容。

有三个[并发控制](http://en.wikipedia.org/wiki/Concurrency_control)提供策略：

- **不执行任何操作**-如果并发用户要修改同一条记录，请让赢取 （默认行为） 的最后一个提交
- [**乐观并发**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)的假设，可能会有并发冲突不时地，大多数情况下不会产生此类冲突; 因此，如果确实会发生冲突，只需通知用户，他们的更改无法保存，因为另一个用户已修改相同的数据
- **悲观并发**的假设，并发冲突日益普及，用户将不允许是告诉他们的更改未保存由于另一个用户的并发活动; 因此，当一个用户启动更新记录时，将其锁定从而防止任何其他用户编辑或删除该记录，直到用户提交其修改

所有我们的教程到目前为止已使用默认的并发解析策略-也就是说，我们已让赢取最后一次写入。 在本教程中我们将介绍如何实现乐观并发控制。

> [!NOTE]
> 我们不会介绍本系列教程中的保守式并发示例。 悲观并发很少使用，因为此类将锁定，如果未正确释放，可以防止其他用户更新数据。 例如，如果用户锁定以进行编辑的记录，然后离开前对其解除锁定一天，没有其他用户将能够更新该记录，直到原始用户返回并完成其更新。 因此，在保守式并发使用的情况下，没有通常了超时，如果达到，将取消该锁。 票证销售网站，而在用户完成订单流程短时间内锁定特定的安装位置，例如的悲观并发控制。


## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>步骤 1： 查看如何乐观并发被实现

乐观并发控制的工作原理是确保要更新或删除的记录具有相同的值，像以前那样也随之更新或删除进程启动时。 例如，单击编辑按钮可编辑的 GridView 中后，记录的值将从数据库读取并显示在文本框和其他 Web 控件。 GridView 情况保存这些原始值。 更高版本，用户可以她的更改，并单击更新按钮后，原始值加上新的值发送到业务逻辑层，然后再到数据访问层。 数据访问层必须发出一条 SQL 语句将仅更新的记录，如果用户已开始编辑的原始值仍在数据库中的值相同。 图 2 描绘了这一序列的事件。


[![若要成功执行 Update 或 Delete，对于原始值必须等于当前的数据库值](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**图 2**: For Update 或 Delete succeed，原始值必须为等于当前的数据库值 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image6.png))


有多种方法实现乐观并发 (请参阅[Peter A.Bromberg](http://peterbromberg.net/)的[Optmistic 并发更新逻辑](http://www.eggheadcafe.com/articles/20050719.asp)的简要介绍一下使用多种)。 ADO.NET 类型化数据集提供了一种可配置为只是一个复选框的刻度线的实现。 为类型化数据集在 TableAdapter 扩充 TableAdapter 的启用乐观并发`UPDATE`并`DELETE`语句以包括所有中的原始值的比较`WHERE`子句。 以下`UPDATE`语句，例如，更新的名称和产品的价格仅当当前的数据库值是否等于更新 GridView 中的记录时最初检索到的值。 `@ProductName`并`@UnitPrice`参数包含由用户输入的新值，而`@original_ProductName`和`@original_UnitPrice`包含最初加载到了 GridView 时单击编辑按钮的值：


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> 这`UPDATE`语句已得到简化，以提高可读性。 在实践中，`UnitPrice`签入`WHERE`子句是因为更多地涉及`UnitPrice`可以包含`NULL`s 和检查是否`NULL = NULL`始终返回 False (而是必须使用`IS NULL`)。


除了使用不同的基础`UPDATE`语句中，配置 TableAdapter 使用乐观并发还会修改其 DB 签名直接方法。 从我们的第一个教程，请记住[*创建数据访问层*](../introduction/creating-a-data-access-layer-cs.md)，DB 直接方法是那些接受一组标量值作为输入的参数 (而不是强类型化的数据行或DataTable 实例）。 使用乐观并发，直接 DB 时`Update()`和`Delete()`方法包括输入的参数的原始值。 此外，使用 batch BLL 中的代码更新模式 (`Update()`接受 Datarow 和数据表，而不是标量值的方法重载) 也必须更改。

而是不是扩展了现有 DAL 的 Tableadapter 使用乐观并发 （这就势必会造成更改以适应 BLL），让我们改为创建新类型化数据集名为`NorthwindOptimisticConcurrency`，我们将添加到`Products`TableAdapter 的使用乐观并发。 接下来，我们将创建`ProductsOptimisticConcurrencyBLL`具有适当的修改来支持乐观并发 DAL 的业务逻辑层类。 一旦已排列该基础内容，我们就可以创建 ASP.NET 页。

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>步骤 2： 创建数据访问层支持乐观并发

若要创建新的类型化数据集，请右键单击`DAL`中的文件夹`App_Code`文件夹，并添加名为的新数据集`NorthwindOptimisticConcurrency`。 正如我们看到的第一个教程中，这样做将新的 TableAdapter 类型化数据集，会自动启动 TableAdapter 配置向导。 在第一个屏幕中，我们会提示你指定要连接到-连接到相同的 Northwind 数据库使用的数据库`NORTHWNDConnectionString`设置从`Web.config`。


[![连接到相同的 Northwind 数据库](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**图 3**： 连接到相同的 Northwind 数据库 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image9.png))


接下来，我们会提示方式来查询数据： 通过临时 SQL 语句，一个新的存储过程，或将现有存储过程。 由于我们在我们原始 DAL 中使用的即席 SQL 查询，使用此选项在此处也。


[![指定要使用的临时 SQL 语句检索的数据](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**图 4**： 指定要使用的临时 SQL 语句检索的数据 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image12.png))


在以下屏幕上，输入要用于检索产品信息的 SQL 查询。 让我们使用用于完全匹配的同一个 SQL 查询`Products`TableAdapter 从返回的所有我们原始 DAL`Product`以及产品的供应商和类别名称的列：


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]


[![在原始 DAL 中使用相同的 SQL 查询从产品 TableAdapter](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**图 5**： 使用从相同的 SQL 查询`Products`原始 DAL 中的 TableAdapter ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image15.png))


然后再移至下一个屏幕中，单击高级选项按钮。 若要让此 TableAdapter 使用乐观并发控制，只需选中"使用开放式并发"复选框。


[![启用乐观并发控制通过支票&quot;使用乐观并发&quot;复选框](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**图 6**： 通过检查"使用开放式并发"复选框来启用乐观并发控制 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image18.png))


最后，指示 TableAdapter 应使用的数据访问模式，填充 DataTable 和返回 DataTable;此外指示应创建 DB 直接方法。 更改方法名称返回 DataTable 模式从 GetData getproducts，以便反映我们在我们原始 DAL 中使用的命名约定。


[![已使用所有数据访问模式的 TableAdapter](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**图 7**： 具有 TableAdapter 利用所有数据访问模式 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image21.png))


完成向导，完成后，数据集设计器将包括一个强类型`Products`DataTable 和 TableAdapter。 请花费片刻时间来重命名从 DataTable`Products`到`ProductsOptimisticConcurrency`，您可以通过该 DataTable 的标题栏上右键单击并从上下文菜单中选择重命名来执行此操作。


[![已添加到类型化数据集的数据表和 TableAdapter](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**图 8**: 数据表和 TableAdapter 已添加到类型化数据集 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image24.png))


若要查看之间的差异`UPDATE`并`DELETE`之间的查询的`ProductsOptimisticConcurrency`TableAdapter （它使用乐观并发） 和产品 TableAdapter （这不会），单击 TableAdapter，然后转到属性窗口。 在中`DeleteCommand`并`UpdateCommand`属性的`CommandText`子属性可以看到实际调用 DAL 的更新或删除相关的方法时发送到数据库的 SQL 语法。 有关`ProductsOptimisticConcurrency`TableAdapter`DELETE`使用语句是：


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

而`DELETE`产品 TableAdapter 中原始 DAL 的语句是简单得多：


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

正如您所看到的`WHERE`中的子句`DELETE`TableAdapter 使用乐观并发的语句中包含的每个之间的比较`Product`表的时间在现有列的值和原始值上次填充 GridView （或 DetailsView 或 FormView）。 由于以外的其他所有字段`ProductID`， `ProductName`，并`Discontinued`可以有`NULL`其他参数和检查的值是包括在内，以正确比较`NULL`中的值`WHERE`子句。

我们不会添加任何其他 DataTables 到乐观并发启用数据集为本教程中，为我们的 ASP.NET 页面将仅为您提供更新和删除产品信息。 但是，我们仍需要添加`GetProductByProductID(productID)`方法`ProductsOptimisticConcurrency`TableAdapter。

若要完成此操作，右键单击 TableAdapter 的标题栏 (上方区域右侧`Fill`和`GetProducts`方法名称)，然后从上下文菜单中选择添加查询。 这将启动 TableAdapter 查询配置向导。 使用我们 TableAdapter 的初始配置时，选择创建如`GetProductByProductID(productID)`方法使用的临时 SQL 语句 （请参阅图 4）。 由于`GetProductByProductID(productID)`方法返回有关特定产品的信息，指示此查询是`SELECT`查询返回行的类型。


[![查询将类型标记为&quot;返回行的选择&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**图 9**： 将为该查询类型标记"`SELECT`返回的行"([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image27.png))


在下一个屏幕上，我们系统提示输入要用于预加载的 TableAdapter 的默认查询的 SQL 查询。 增加现有查询以包含子句`WHERE ProductID = @ProductID`，如图 10 中所示。


[![添加 WHERE 子句为预加载的查询，以返回特定产品记录](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**图 10**： 添加`WHERE`Pre-Loaded 查询以返回特定的产品记录的子句 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image30.png))


最后，更改到生成的方法名`FillByProductID`和`GetProductByProductID`。


[![将方法重命名为 FillByProductID 和 GetProductByProductID](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**图 11**： 重命名的方法`FillByProductID`并`GetProductByProductID`([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image33.png))


完成此向导中，使用 TableAdapter 现在包含两种方法来检索数据： `GetProducts()`，它将返回*所有*产品; 和`GetProductByProductID(productID)`，这会返回指定的产品。

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>步骤 3： 为乐观并发启用 DAL 创建业务逻辑层

我们现有`ProductsBLL`类具有使用批处理更新和 DB 直接模式的示例。 `AddProduct`方法和`UpdateProduct`这两个重载都使用批更新模式，并传入`ProductRow`TableAdapter 的 Update 方法的实例。 `DeleteProduct`方法，但是，使用 DB 直接模式，调用 TableAdapter 的`Delete(productID)`方法。

与新`ProductsOptimisticConcurrency`TableAdapter，DB 直接方法现在要求还中传递的原始值。 例如，`Delete`方法现在需要 10 个输入参数： 原始`ProductID`， `ProductName`， `SupplierID`， `CategoryID`， `QuantityPerUnit`， `UnitPrice`， `UnitsInStock`， `UnitsOnOrder`， `ReorderLevel`，和`Discontinued`。 它将使用这些其他输入的参数的值中`WHERE`子句`DELETE`语句发送到数据库，仅删除指定的记录，如果数据库的当前值映射到原始的编译器。

尽管为 TableAdapter 的方法签名`Update`批更新模式中使用的方法未发生更改时，记录的原始和新值所需的代码。 因此，而不是尝试将乐观并发启用 DAL 与我们现有`ProductsBLL`类中，让我们创建一个新的业务逻辑层类为使用新 DAL。

添加名为的类`ProductsOptimisticConcurrencyBLL`到`BLL`文件夹内的`App_Code`文件夹。


![将 ProductsOptimisticConcurrencyBLL 类添加到 BLL 文件夹](implementing-optimistic-concurrency-cs/_static/image34.png)

**图 12**： 添加`ProductsOptimisticConcurrencyBLL`BLL 文件夹类


接下来，将以下代码添加到`ProductsOptimisticConcurrencyBLL`类：


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

请注意使用`NorthwindOptimisticConcurrencyTableAdapters`开始上述的类声明的语句。 `NorthwindOptimisticConcurrencyTableAdapters`命名空间包含`ProductsOptimisticConcurrencyTableAdapter`类，该类提供了为 DAL 的方法。 此外在类声明之前找到`System.ComponentModel.DataObject`属性，指示 Visual Studio 在 ObjectDataSource 向导的下拉列表中包括此类。

`ProductsOptimisticConcurrencyBLL`的`Adapter`属性提供快速访问的实例`ProductsOptimisticConcurrencyTableAdapter`类，并遵循在我们原始 BLL 类中使用的模式 (`ProductsBLL`， `CategoriesBLL`，依此类推)。 最后，`GetProducts()`方法只是调用向下到 DAL`GetProducts()`方法并返回`ProductsOptimisticConcurrencyDataTable`对象填充`ProductsOptimisticConcurrencyRow`数据库中每个产品记录的实例。

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>正在删除产品 DB 直接模式中使用乐观并发

使用针对使用开放式并发的 DAL DB 直接模式时，方法必须传递新的和原始值。 用于删除，没有任何新值，因此需要在传递仅的原始值。 在我们 BLL，然后，我们必须接受所有原始参数作为输入参数。 让我们`DeleteProduct`中的方法`ProductsOptimisticConcurrencyBLL`类使用 DB 直接方法。 这意味着此方法需要所有 10 个产品数据字段作为输入参数，并将这些值交给 DAL，如下面的代码中所示：


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

如果当用户单击删除按钮，从数据库中的值不同的原始值-上次已加载到 GridView （或 DetailsView 或 FormView） 这些值-`WHERE`子句不会与任何数据库记录和任何记录匹配将会受到影响。 因此，TableAdapter`Delete`方法将返回`0`和 BLL`DeleteProduct`方法将返回`false`。

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>更新产品批更新模式中使用乐观并发

如前文所述，TableAdapter 的`Update`批更新模式的方法具有相同的方法签名，而不考虑是否使用乐观并发。 也就是说，`Update`方法需要 DataRow，Datarow、 DataTable 或类型化数据集的数组。 没有其他输入的参数用于指定的原始值。 这可能是因为 DataTable 会跟踪有关其 DataRow(s) 的原始和已修改值。 当 DAL 发出其`UPDATE`语句中，`@original_ColumnName`参数将填入 DataRow 的原始值，而`@ColumnName`参数都填入 DataRow 的修改后的值。

在`ProductsBLL`类 （它使用我们的原始的非乐观并发 DAL），使用批更新模式以更新我们的代码执行以下一系列事件的产品信息时：

1. 将当前的数据库产品信息读入`ProductRow`实例使用 TableAdapter 的`GetProductByProductID(productID)`方法
2. 将分配到的新值`ProductRow`步骤 1 中的实例
3. 调用 TableAdapter`Update`方法，传入`ProductRow`实例

这一序列的步骤，但是，不会正确支持乐观并发，因为`ProductRow`中填充步骤 1 填充直接从数据库中，这意味着使用 DataRow 的原始值指那些中当前存在数据库，而不是绑定到 GridView 编辑过程的开头。 相反，当使用乐观并发的 DAL，我们需要 alter`UpdateProduct`方法重载，可使用以下步骤：

1. 将当前的数据库产品信息读入`ProductsOptimisticConcurrencyRow`实例使用 TableAdapter 的`GetProductByProductID(productID)`方法
2. 将分配*原始*值到`ProductsOptimisticConcurrencyRow`步骤 1 中的实例
3. 调用`ProductsOptimisticConcurrencyRow`实例的`AcceptChanges()`方法，指示其当前值是"原始"的 DataRow
4. 将分配*新*值到`ProductsOptimisticConcurrencyRow`实例
5. 调用 TableAdapter`Update`方法，传入`ProductsOptimisticConcurrencyRow`实例

步骤 1 指定的产品记录中的所有当前的数据库值的读取。 这一步是在多余`UpdateProduct`更新的重载*所有*的产品列 （作为这些值将被覆盖在步骤 2 中），但对于其中的列的值的一个子集作为传入这些重载至关重要输入的参数。 一旦原始值已分配给`ProductsOptimisticConcurrencyRow`实例，`AcceptChanges()`调用方法时，这会将当前的 DataRow 值标记为要在中使用的原始值`@original_ColumnName`中的参数`UPDATE`语句。 接下来，将新的参数值分配给`ProductsOptimisticConcurrencyRow`以及最终`Update`调用方法时，传入 DataRow。

下面的代码演示`UpdateProduct`重载接受产品的所有数据字段作为输入的参数。 虽然未在此处，显示`ProductsOptimisticConcurrencyBLL`对于本教程还包含下载中包含的类`UpdateProduct`接受只是该产品的名称和价格作为输入参数的重载。


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>步骤 4： 将原始值和新值从 ASP.NET 页传递给 BLL 方法

DAL 和 BLL 完成后，所有的就是要创建可以使用乐观并发逻辑内置于系统中的 ASP.NET 页。 具体而言，数据 Web 控件 (GridView、 detailsview 和 FormView) 必须记住其原始值和对象数据源必须将这两组值传递给业务逻辑层。 此外，必须配置 ASP.NET 页面妥善处理并发冲突。

首先打开`OptimisticConcurrency.aspx`页中`EditInsertDelete`文件夹，然后将 GridView 添加到设计器中，设置其`ID`属性设置为`ProductsGrid`。 从 GridView 的智能标记上，选择创建名为新 ObjectDataSource `ProductsOptimisticConcurrencyDataSource`。 因为我们希望此 ObjectDataSource 用于支持乐观并发 DAL，将其配置为使用`ProductsOptimisticConcurrencyBLL`对象。


[![具有 ObjectDataSource 使用 ProductsOptimisticConcurrencyBLL 对象](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**图 13**： 拥有 ObjectDataSource`ProductsOptimisticConcurrencyBLL`对象 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image37.png))


选择`GetProducts`， `UpdateProduct`，和`DeleteProduct`向导中的下拉列表中的方法。 对于 UpdateProduct 方法中，请使用接受的所有产品的数据字段的重载。

## <a name="configuring-the-objectdatasource-controls-properties"></a>配置 ObjectDataSource 控件的属性

完成向导后，ObjectDataSource 的声明性标记应如下所示：


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

正如您所看到的`DeleteParameters`集合中包含`Parameter`实例中的十个输入参数的每个`ProductsOptimisticConcurrencyBLL`类的`DeleteProduct`方法。 同样，`UpdateParameters`集合中包含`Parameter`中的输入参数的每个实例`UpdateProduct`。

对于涉及数据修改这些上一教程，我们将删除 ObjectDataSource 的`OldValuesParameterFormatString`这一时刻，因为此属性指示的 BLL 方法需要中传递的旧 （或原始） 值，以及新值的属性。 此外，此属性的值指示原始值的输入的参数的名称。 由于我们要到 BLL 传递的原始值中，执行操作*不*删除此属性。

> [!NOTE]
> 值`OldValuesParameterFormatString`属性必须映射到预期的原始值 BLL 中的输入的参数名称。 因为我们已命名为这些参数`original_productName`， `original_supplierID`，依此类推，您可以保留`OldValuesParameterFormatString`属性值作为`original_{0}`。 如果，但是，BLL 方法的输入的参数具有类似名称`old_productName`， `old_supplierID`，依此类推，需要更新`OldValuesParameterFormatString`属性设置为`old_{0}`。


没有一种不需要为了使对象数据源以正确地将原始值传递给 BLL 方法进行的最后一个属性设置。 具有 ObjectDataSource [ConflictDetection 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx)，可以分配给[两个值之一](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx):

- `OverwriteChanges` -默认值;不向 BLL 方法的原始输入参数发送的原始值
- `CompareAllValues` -does 将原始值发送到的 BLL 方法;选择此选项时使用乐观并发

请花费片刻时间来设置`ConflictDetection`属性设置为`CompareAllValues`。

## <a name="configuring-the-gridviews-properties-and-fields"></a>配置 GridView 的属性和字段

使用 ObjectDataSource 的属性正确配置，让我们把注意力转向设置 GridView。 首先，因为我们希望 GridView，支持编辑和删除，则单击 GridView 的智能标记中的启用编辑并启用删除复选框。 这将添加 CommandField 其`ShowEditButton`并`ShowDeleteButton`都设置为`true`。

当绑定到`ProductsOptimisticConcurrencyDataSource`ObjectDataSource，GridView 包含字段的每个产品的数据字段。 虽然可以编辑此类 GridView，用户体验是任何内容，但是可接受的。 `CategoryID`和`SupplierID`BoundFields 将呈现为文本框中，因此需要用户输入的相应的类别和供应商作为 ID 号。 将有无格式的数值字段并不验证控制措施来确保已提供该产品的名称，且的单位价格，库存数量、 顺序和重新排序的级别值上单位是这两个正确的数字值并大于或等于为零。

如中所述*向编辑和插入界面添加验证控件*并*自定义数据修改界面*教程中，用户界面可以自定义使用 Templatefield 替换 BoundFields。 我已按以下方式修改此 GridView 和其编辑界面：

- 删除`ProductID`， `SupplierName`，和`CategoryName`BoundFields
- 转换`ProductName`到 TemplateField BoundField 和添加了 RequiredFieldValidation 控件。
- 转换`CategoryID`和`SupplierID`BoundFields 到 Templatefield，并且调整编辑界面使用 Dropdownlist，而不是文本框。 在这些 Templatefield `ItemTemplates`，则`CategoryName`和`SupplierName`数据字段的显示。
- 转换`UnitPrice`， `UnitsInStock`， `UnitsOnOrder`，和`ReorderLevel`BoundFields Templatefield 和添加了的 CompareValidator 控件。

由于我们已经探讨了如何在前面的教程中完成这些任务，我只是列出的最后一个声明性语法，并将作为操作的实现。


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

我们已经非常接近具有完全工作示例。 但是，有一些微妙之处，将向上扩大并使我们的问题。 此外，我们仍需要一些接口，当发生并发冲突时提醒用户。

> [!NOTE]
> 为了使数据 Web 控件以正确地将原始值传递给 ObjectDataSource （它随后传递到 BLL），非常重要的 GridView`EnableViewState`属性设置为`true`（默认值）。 如果禁用视图状态，会在回发时丢失的原始值。


## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>将正确的原始值传递到 ObjectDataSource

有几个问题与配置 GridView 的方式。 如果 ObjectDataSource`ConflictDetection`属性设置为`CompareAllValues`（按原样我们），当 ObjectDataSource 的`Update()`或`Delete()`GridView （或 DetailsView 或 FormView） 调用方法，ObjectDataSource 会尝试复制GridView 的原始值到其相应`Parameter`实例。 回顾图 2 用于此过程的图形表示形式。

具体而言，GridView 的原始值分配了在每次将数据绑定到 GridView 的双向数据绑定语句中的值。 因此，很重要通过双向数据绑定均捕获的所有所需的原始值并为其提供转换格式。

若要查看这为什么很重要，花点时间访问我们的页面在浏览器中。 按预期运行，GridView 列出了每个产品的最左侧列中的编辑和删除按钮。


[![在 GridView 中列出的产品](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**图 14**： 在 GridView 中列出了产品 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image40.png))


如果单击删除按钮对任何产品`FormatException`引发。


[![尝试删除 FormatException 中的任何产品结果](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**图 15**： 尝试在删除任何产品结果`FormatException`([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image43.png))


`FormatException` ObjectDataSource 尝试在原始读取时，将引发`UnitPrice`值。 由于`ItemTemplate`已`UnitPrice`设置为货币格式 (`<%# Bind("UnitPrice", "{0:C}") %>`)，它包含一个货币符号，如 19.95 美元。 `FormatException` ObjectDataSource 尝试将此字符串转换会出现`decimal`。 若要避免此问题，我们有许多选项：

- 删除货币格式从`ItemTemplate`。 也就是说，而不是使用`<%# Bind("UnitPrice", "{0:C}") %>`，只需使用`<%# Bind("UnitPrice") %>`。 此的缺点是价格不能再设置格式。
- 显示`UnitPrice`格式设置为在货币`ItemTemplate`，但使用`Eval`关键字来实现此目的。 请记住，`Eval`执行单向数据绑定。 我们仍需要提供`UnitPrice`值的原始值，因此，我们仍需要中的双向数据绑定语句`ItemTemplate`，但这可以放置标签 Web 控件中的`Visible`属性设置为`false`。 我们可以在 ItemTemplate 中使用以下标记：


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- 删除从格式设置的货币`ItemTemplate`，并使用`<%# Bind("UnitPrice") %>`。 在 GridView`RowDataBound`标签 Web 事件处理程序中，以编程方式访问控制在其中`UnitPrice`显示值并且将其设置其`Text`属性设置为带格式的版本。
- 将保留`UnitPrice`设置为货币格式。 在 GridView`RowDeleting`事件处理程序替换现有的原始`UnitPrice`值 (19.95 美元) 与实际的十进制值使用`Decimal.Parse`。 我们已了解如何实现中的类似`RowUpdating`中的事件处理程序[*处理 BLL-和 DAL 级别 ASP.NET 页面中的异常*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)教程。

我选择使用第二种方法，例如添加隐藏的标签 Web 控件`Text`属性是双向数据绑定到未格式化`UnitPrice`值。

后解决此问题，请尝试再次单击删除按钮对任何产品。 这将获得一次`InvalidOperationException`ObjectDataSource 尝试调用 BLL`UpdateProduct`方法。


[![ObjectDataSource 找不到具有它需要发送到输入参数的方法](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**图 16**: ObjectDataSource 找不到具有它需要发送到输入参数的方法 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image46.png))


查看异常的消息时，很明显 ObjectDataSource 想要调用 BLL`DeleteProduct`方法，包括`original_CategoryName`和`original_SupplierName`输入参数。 这是因为`ItemTemplate`s`CategoryID`并`SupplierID`Templatefield 当前包含具有双向绑定语句`CategoryName`和`SupplierName`数据字段。 相反，我们需要包括`Bind`语句替换`CategoryID`和`SupplierID`数据字段。 若要完成此操作，将为使用的现有绑定语句`Eval`语句，以及如何将隐藏的标签控件`Text`属性绑定到`CategoryID`和`SupplierID`使用双向数据绑定，如所示的数据字段如下：


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

这些更改，我们现已成功删除和编辑产品信息 ！ 在步骤 5 中，我们将介绍如何验证检测到并发冲突。 但现在，需要几分钟的时间来尝试更新和删除几个记录，以确保该更新和删除适用于单个用户按预期方式工作。

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>步骤 5： 测试乐观并发支持

若要验证是否存在并发冲突正在检测到 （而不是导致数据被盲目地覆盖），我们需要打开到此页的两个浏览器窗口。 在这两个浏览器情况下，单击编辑按钮 Chai。 然后，只需在浏览器之一，将名称更改为"Chai 茶"并单击更新。 更新应成功并返回到其预先编辑状态，使用"Chai 茶"作为新的产品名称的 GridView。

在其他浏览器窗口实例，但是，产品名称文本框中仍将显示"Chai"。 在此第二个浏览器窗口中，更新`UnitPrice`到`25.00`。 没有乐观并发支持，单击在第二个浏览器实例的更新会更改产品名称返回到"Chai"，从而覆盖第一个浏览器实例所做的更改。 利用乐观并发使用，但是，单击第二个浏览器实例中的更新按钮会导致[DBConcurrencyException](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)。


[![检测到并发冲突时，引发 DBConcurrencyException](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**图 17**： 检测到时的并发冲突，则`DBConcurrencyException`引发 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image49.png))


`DBConcurrencyException`利用 DAL 的批更新模式时才会引发。 DB 直接模式不会引发异常，它只是表示没影响任何行。 若要说明这一点，返回到预先编辑的状态，这两个浏览器实例的 GridView。 接下来，在第一个浏览器实例中，单击编辑按钮并更改回"Chai"从"Chai 茶"产品名称并单击更新。 在第二个浏览器窗口中，为 Chai 中单击删除按钮。

单击删除，页面回发，GridView 调用 ObjectDataSource`Delete()`方法和 ObjectDataSource 调用向下`ProductsOptimisticConcurrencyBLL`类的`DeleteProduct`方法，传递的原始值。 原始`ProductName`值的第二个浏览器实例为"Chai 茶"，这不符合当前`ProductName`数据库中的值。 因此`DELETE`语句向数据库发出会影响任何行，因为在数据库中没有记录的`WHERE`子句满足。 `DeleteProduct`方法将返回`false`和对象数据源的数据重新绑定到 GridView。

从最终用户的角度来看，Chai 茶第二个浏览器窗口中，单击删除按钮上导致屏幕闪烁，且后恢复，, 该产品是仍然存在，但现在它列出为"Chai"（产品名称更改所做的第一个浏览器实例）。 如果用户再次单击删除按钮，将成功删除，如 GridView 的原始`ProductName`值 ("Chai") 现在与数据库中的值匹配。

在这种情况下，用户体验并不理想。 我们显然不想要向用户显示的细枝末节`DBConcurrencyException`异常时使用批更新模式。 并使用 DB 直接模式时的行为是有些令人费解，因为用户命令失败，但是没有精确的原因的迹象。

若要纠正这两个问题，我们可以创建更新或删除失败的原因提供到说明页上的标签 Web 控件。 对于批更新模式中，我们可以确定是否`DBConcurrencyException`异常发生在 GridView 的后续级别事件处理程序中，根据需要显示警告标签。 对于 DB 直接方法，我们可以检查 BLL 方法的返回值 (即`true`受到了影响一行，如果`false`否则为)，并根据需要显示一条信息性消息。

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>步骤 6： 添加信息性消息，并在遇到并发冲突时显示它们

当发生并发冲突时，展示的行为取决于是否为 DAL 的批处理更新或 DB 直接模式时使用。 在本教程中使用这两种模式，使用批更新模式用于更新和删除使用的数据库直接模式。 若要开始，让我们向我们介绍了并发冲突发生时正在尝试删除或更新数据的页面中添加两个标签 Web 控件。 设置标签控件的`Visible`并`EnableViewState`属性设置为`false`; 这将导致它们为在每个页，请访问上隐藏，但对于那些特定页访问的位置及其`Visible`属性以编程方式设置为`true`。


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

除了设置其`Visible`， `EnabledViewState`，并`Text`属性，我还设置`CssClass`属性设置为`Warning`，这将导致该标签的大型、 红色、 斜体、 粗体的字体中显示。 此 CSS`Warning`已定义类并将其添加到 Styles.css 回到*检查与插入、 更新和删除的事件相关联*教程。

以后将添加这些标签，Visual Studio 中的设计器看起来应类似于图 18。


[![两个标签控件已添加到页面](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**图 18**： 两个标签控件已添加到页面 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image52.png))


使用这些标签 Web 控制，我们已准备好检查如何确定当发生并发冲突，在这一时刻的相应标签`Visible`属性可以设置为`true`，显示信息性消息。

## <a name="handling-concurrency-violations-when-updating"></a>更新时处理并发冲突

让我们首先看一下如何处理并发冲突时使用批更新模式。 由于此类违规情况与批处理更新模式的原因`DBConcurrencyException`异常抛出，我们需要将代码添加到了 ASP.NET 页，确定是否`DBConcurrencyException`更新过程中出现异常。 因此，我们应显示一条消息向用户解释，他们的更改未保存，因为另一个用户已修改之间的相同数据，它们启动编辑记录时是否以及何时他们单击更新按钮。

中可以看到*处理 BLL-和 DAL 级别 ASP.NET 页面中的异常*教程中，可以检测并在数据 Web 控件的后续级别事件处理程序中禁止显示此类异常。 因此，我们需要为 GridView 的创建事件处理程序`RowUpdated`事件检查是否`DBConcurrencyException`引发异常。 此事件处理程序传递对更新过程中引发任何异常的引用，如事件处理程序下面的代码中所示：


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

面对`DBConcurrencyException`异常，此事件处理程序显示`UpdateConflictMessage`标签控件，并指示已处理了异常。 利用此代码，当更新记录时，会发生并发冲突时用户的更改都将丢失，因为它们可能已覆盖另一个用户修改一次。 具体而言，GridView 是返回到其预先编辑状态，并且绑定到当前的数据库数据。 这将更新的 GridView 行与其他用户的更改，这是以前不可见。 此外，`UpdateConflictMessage`标签控件将向用户说明只需完成的操作。 图 19 中详细说明了这一序列的事件。


[![用户 s 在并发冲突的人脸会丢失更新](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**图 19**: 用户 s 在并发冲突的人脸会丢失更新 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image55.png))


> [!NOTE]
> 或者，而不是返回到预先编辑状态 GridView，我们无法将保留 GridView 处于编辑状态通过设置`KeepInEditMode`传入的属性`GridViewUpdatedEventArgs`为 true 的对象。 如果采用此方法，不过，请确保重新绑定到 GridView 数据 (通过调用其`DataBind()`方法)，以便其他用户的值加载到编辑界面。 本教程中下载的代码具有以下两个行中的代码`RowUpdated`事件处理程序被注释掉; 只需取消注释以下行代码有 GridView 并发冲突后继续处于编辑模式。


## <a name="responding-to-concurrency-violations-when-deleting"></a>删除时响应并发冲突

使用 DB 直接模式时，没有遇到并发冲突时引发异常。 相反，database 语句只会影响任何记录，作为与任何记录不匹配的 WHERE 子句。 所有在 BLL 中创建的数据修改方法的设计，以便它们返回一个布尔值，该值指示在受影响的准确地说一条记录。 因此，若要确定删除记录时，是否发生了并发冲突，我们可以检查返回值的 BLL`DeleteProduct`方法。

可以在通过 ObjectDataSource 的后续级别事件处理程序中检查的 BLL 方法的返回值`ReturnValue`属性的`ObjectDataSourceStatusEventArgs`对象传递给事件处理程序。 由于我们感兴趣的返回值确定`DeleteProduct`方法中，我们需要为 ObjectDataSource 的创建事件处理程序`Deleted`事件。 `ReturnValue`属性属于类型`object`可以是`null`如果引发了异常，并且它无法返回值之前，该方法已中断。 因此，我们应该首先确保`ReturnValue`属性不是`null`和是一个布尔值。 假设此项检查成功，我们展示`DeleteConflictMessage`标签控件，如果`ReturnValue`是`false`。 这可以通过使用以下代码：


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

遇到并发冲突，会取消用户的 delete 请求。 刷新时 GridView，其中显示该记录的时间之间用户发生的更改加载页面，但他单击删除按钮时。 当这种冲突怎样时，`DeleteConflictMessage`显示标签，解释发生 （请参阅图 20）。


[![在遇到并发冲突时取消用户的删除](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**图 20**： 在遇到并发冲突时取消删除用户 s ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-cs/_static/image58.png))


## <a name="summary"></a>总结

允许多个，每个应用程序中存在并发冲突的机会并发用户更新或删除数据。 如果此类违规情况的两个用户同时更新相同的数据，任何人获取最后一个写入"胜出"中，覆盖其他用户的更改的更改都不考虑在内。 或者，开发人员可以实现任一乐观或悲观并发控制。 乐观并发控制假定并发冲突不太频繁出现，并只是不允许更新或删除会形成并发冲突的命令。 悲观并发控制假定的并发冲突较频繁，只需拒绝一个用户更新或删除命令是不可接受的。 使用悲观并发控制更新记录涉及到锁定，从而防止修改或删除记录锁定时的任何其他用户。

类型化数据集在.NET 中提供了有关支持乐观并发控制的功能。 具体而言，`UPDATE`和`DELETE`语句向数据库发出包括所有表的列，从而确保，update 或 delete 时才进行记录的当前数据的原始数据与用户相匹配具有正在执行其 update 或 delete。 一旦配置了 DAL，支持乐观并发，BLL 方法需要更新。 此外，必须配置到 BLL 调用向下的 ASP.NET 页，以便 ObjectDataSource 从其数据 Web 控件中检索原始值并将其向下传递到 BLL。

正如我们看到在本教程中，在 ASP.NET web 应用程序中实现乐观并发控制涉及更新 DAL 和 BLL 和 ASP.NET 页中添加的支持。 此添加的工作是比较明智的做法投入的时间和精力取决于你的应用程序。 如果不常有的并发用户更新数据，或要更新的数据是从另一个不同，则并发控制不是一个关键问题。 如果，但是，您通常有多个用户使用相同的数据在站点上，并发控制有助于防止一个用户更新或删除明智地覆盖其他人。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](customizing-the-data-modification-interface-cs.md)
> [下一页](adding-client-side-confirmation-when-deleting-cs.md)
