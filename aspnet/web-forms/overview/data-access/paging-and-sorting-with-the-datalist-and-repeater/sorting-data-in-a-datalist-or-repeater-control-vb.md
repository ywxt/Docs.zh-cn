---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
title: 排序 DataList 或 Repeater 控件 (VB) 中的数据 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将介绍如何包含排序 DataList 和 Repeater 中的支持，以及如何构造其数据可以 DataList 或 Repeater...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 97c13898-0741-45f9-b3fa-7540ab1679e6
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ad940afd03b66c17a4d8b1e5c727c317022fbc0a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834571"
---
<a name="sorting-data-in-a-datalist-or-repeater-control-vb"></a>排序 DataList 或 Repeater 控件 (VB) 中的数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_VB.exe)或[下载 PDF](sorting-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial45vb1.pdf)

> 在本教程中我们将介绍如何包含排序 DataList 和 Repeater 中的支持，以及如何构造 DataList 或 Repeater 分页和排序的数据。


## <a name="introduction"></a>介绍

在中[前一篇教程](paging-report-data-in-a-datalist-or-repeater-control-vb.md)中，我们探讨如何将分页支持添加到 DataList。 我们创建了中的新方法`ProductsBLL`类 (`GetProductsAsPagedDataSource`) 返回`PagedDataSource`对象。 当绑定到 DataList 或 Repeater、 DataList 或 Repeater 将显示只是请求的数据页。 此技术非常类似于使用在内部由 GridView、 DetailsView 和 FormView 控件来提供其内置的默认分页功能。

除了提供分页支持的 GridView 还包括现成排序支持。 DataList 和 Repeater 都不提供内置排序功能;但是，使用少量的代码添加排序功能。 在本教程中我们将介绍如何包含排序 DataList 和 Repeater 中的支持，以及如何构造 DataList 或 Repeater 分页和排序的数据。

## <a name="a-review-of-sorting"></a>排序的评审

中可以看到[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程中，提供排序支持现成的 GridView 控件。 GridView 中的每个字段可以具有关联`SortExpression`，指示对数据进行排序所依据的数据字段。 当 GridView s`AllowSorting`属性设置为`true`，具有每个 GridView 字段`SortExpression`属性值已作为 LinkButton 呈现其标头。 当用户单击特定的 GridView 字段 s 标头时，产生的回发和被单击字段 s 根据数据进行排序`SortExpression`。

GridView 控件具有`SortExpression`属性，它将存储`SortExpression`GridView 字段的数据进行排序。 此外，`SortDirection`属性指示数据是否按升序或降序 （如果用户单击切换中的某个特定 GridView 字段 s 标头链接两次连续的排序顺序） 排序。

当 GridView 绑定到其数据源控件时，将提交其`SortExpression`和`SortDirection`属性对数据源控件。 数据源控件检索数据，然后对其进行排序根据所提供`SortExpression`和`SortDirection`属性。 对数据进行排序之后, 的数据源控件将其返回到 GridView。

若要复制的 DataList 或 Repeater 控件使用此功能，我们必须：

- 创建排序的接口
- 请记住要作为排序依据的数据字段，以及是否按升序还是降序排序
- 指示对象数据源的特定数据字段的数据进行排序

例如，我们将介绍这三个任务在步骤 3 和 4。 接下来，我们将介绍如何包含都分页和排序 DataList 或 Repeater 中的支持。

## <a name="step-2-displaying-the-products-in-a-repeater"></a>步骤 2： 在 Repeater 中显示产品

我们担心实现任何与排序相关的功能之前，让 s 首先列出 Repeater 控件中的产品。 首先打开`Sorting.aspx`页中`PagingSortingDataListRepeater`文件夹。 将 Repeater 控件添加到 web 页上，设置其`ID`属性设置为`SortableProducts`。 从 Repeater s 智能标记，创建名为新 ObjectDataSource`ProductsDataSource`并将其配置为从`ProductsBLL`类的`GetProducts()`方法。 （无） 从下拉列表中的 INSERT、 UPDATE 和 DELETE 的选项卡中选项的选择。


[![创建对象数据源，并将其配置为使用 GetProductsAsPagedDataSource() 方法](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**图 1**： 创建对象数据源，并将其配置为使用`GetProductsAsPagedDataSource()`方法 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image3.png))


[![设置下拉列表中插入、 更新和删除选项卡添加到 （无）](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)

**图 2**： 设置的下拉列表中插入、 更新和删除选项卡添加到 （无） ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image6.png))


与使用 DataList 和 Visual Studio 不会自动创建`ItemTemplate`Repeater 控件后将其绑定到数据源。 此外，我们必须添加此`ItemTemplate`以声明方式，因为 Repeater 控件 s 智能标记缺少 DataList s 中找到编辑模板选项。 允许 s 使用相同`ItemTemplate`从前面的教程，其中显示 s 产品名称、 供应商和类别。

添加后`ItemTemplate`，Repeater 和 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample1.aspx)]

图 3 显示时的浏览器查看此页。


[![显示每个产品的名称、 供应商和类别](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**图 3**： 显示每个产品名称、 供应商和类别 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image9.png))


## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>步骤 3： 指示 ObjectDataSource 对数据进行排序

若要显示中继器中的数据进行排序，我们需要通知的数据进行排序所依据的排序表达式的对象数据源。 对象数据源中检索其数据之前，它会首先触发其[`Selecting`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)，其中提供了机会，我们要指定排序表达式。 `Selecting`事件处理程序传递类型的对象[ `ObjectDataSourceSelectingEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)，其中有一个名为[ `Arguments` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx)类型的[ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)。 `DataSourceSelectArguments`类用于将与数据相关的请求的数据使用者从传递到数据源控件，并包含[`SortExpression`属性](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)。

若要将从 ASP.NET 页的排序信息传递到对象数据源，创建的事件处理程序`Selecting`事件并使用以下代码：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

*SortExpression*应将值分配 （例如产品名称) 的数据进行排序的数据字段的名称。 没有任何排序方向相关属性，因此如果你想要将数据按降序排序，追加字符串 DESC 到*sortExpression*值 （如 ProductName DESC)。

请继续并尝试一些不同硬编码的值*sortExpression*和浏览器中测试的结果。 如图 4 所示，当使用作为产品名称 DESC *sortExpression*，产品按反向字母顺序在其名称进行排序。


[![按其名称按反向字母顺序排序的产品](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**图 4**： 按其名称按反向字母顺序排序的产品 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))


## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>步骤 4： 创建排序的接口，然后记住的排序表达式和方向

开启排序 GridView 中的支持将 LinkButton 转换为每个排序字段 s 标头文本，单击时，相应地排序数据。 此类排序接口有意义的 GridView，其中其整齐地布置数据列中。 DataList 和 Repeater 控件，但是，不同的排序接口需要。 一组数据 （而不是数据网格中），一个常见排序界面是提供的数据可以进行排序所依据的字段的下拉列表。 让我们来实现本教程的此类接口。

添加上述 DropDownList Web 控件`SortableProducts`Repeater 并设置其`ID`属性设置为`SortBy`。 从属性窗口中，单击省略号中的`Items`属性可以打开 ListItem 集合编辑器。 添加`ListItem`s 的数据进行排序`ProductName`， `CategoryName`，和`SupplierName`字段。 此外将添加`ListItem`要按其名称按反向字母顺序排序产品。

`ListItem` `Text`属性可以设置为任何值 （如名称），但`Value`属性必须设置为 （例如产品名称) 的数据字段的名称。 按降序对结果进行排序，请将字符串 DESC 追加到 ProductName DESC 类似的数据字段名称。


![将 ListItem 添加每个可排序的数据字段](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**图 5**： 添加`ListItem`每个可排序的数据字段


最后，右侧的下拉列表中添加一个按钮 Web 控件。 设置其`ID`到`RefreshRepeater`并将其`Text`刷新属性。

在创建后`ListItem`s，并添加刷新按钮，DropDownList 和按钮 s 声明性语法应看起来类似于下面：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

与排序下拉列表中完成，我们接下来需要更新的 ObjectDataSource s`Selecting`事件处理程序，以便使用所选`SortBy``ListItem`s`Value`属性而不是硬编码的排序表达式。


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample4.vb)]

在首次访问页面时此点产品将最初按排序`ProductName`数据字段，因为它 s `SortBy` `ListItem`默认情况下选择 （请参阅图 6）。 选择一个不同的排序选项，如类别和单击刷新将导致回发，并重新对数据进行排序的类别名称，如图 7 所示。


[![产品是最初按其名称排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)

**图 6**: 产品是最初按其名称 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image16.png))


[![产品是现在按类别排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)

**图 7**: 产品是现在，按类别进行排序 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image19.png))


> [!NOTE]
> 单击刷新按钮会导致数据自动进行重新排序因为已禁用的 Repeater 的视图状态，从而导致 Repeater 重新绑定到其数据源上每次回发。 如果你已留 Repeater s 启用视图状态，更改排序下拉列表结束-赢得 t 上的排序顺序产生任何影响。 若要解决此问题，创建事件处理程序的刷新按钮 s`Click`事件和重新绑定到其数据源 Repeater (通过调用 Repeater 的`DataBind()`方法)。


## <a name="remembering-the-sort-expression-and-direction"></a>记住的排序表达式和方向

在非排序相关可能会发生回发，页面上创建的可排序 DataList 或 Repeater 时它 s 命令性，在回发之间记住的排序表达式和方向。 例如，假设我们在此教程，包括每个产品的删除按钮更新 Repeater。 当用户单击删除按钮 d 我们运行一些代码以删除所选的产品，然后重新绑定到 Repeater 的数据。 如果不会在回发之间保留排序详细信息，在屏幕上显示的数据将恢复为原始的排序顺序。

对于本教程，DropDownList 隐式排序表达式和方向在中保存其视图状态为我们。 如果我们使用不同的排序接口之一，即 Linkbutton 提供不同的排序选项 d 我们需要小心回发之间保留排序顺序。 这可以通过将排序参数存储在页的视图状态中，通过包括排序参数，在查询字符串中或通过某些其他状态暂留技术来实现。

在本教程中的未来示例探索如何持久保存页面的视图状态中的排序详细信息。

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>步骤 5： 添加到使用默认的分页 DataList 排序的支持

在中[前面的教程](paging-report-data-in-a-datalist-or-repeater-control-vb.md)介绍了如何实现使用 DataList 默认分页。 让我们来扩展这一示例，包括能够对分页的数据进行排序。 首先打开`SortingWithDefaultPaging.aspx`并`Paging.aspx`中的页面`PagingSortingDataListRepeater`文件夹。 从`Paging.aspx`页上，单击源按钮以查看页面 s 声明性标记。 复制选定的文本 （请参阅图 8） 将其粘贴到的声明性标记`SortingWithDefaultPaging.aspx`之间`<asp:Content>`标记。


[![复制中的声明性标记&lt;asp: Content&gt; SortingWithDefaultPaging.aspx 从 Paging.aspx 标记](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)

**图 8**： 复制中的声明性标记`<asp:Content>`从标记`Paging.aspx`到`SortingWithDefaultPaging.aspx`([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image22.png))


复制后的声明性标记，请将复制的方法和属性中的`Paging.aspx`页上的代码隐藏类的代码隐藏类`SortingWithDefaultPaging.aspx`。 接下来，花点时间查看`SortingWithDefaultPaging.aspx`页在浏览器中。 它应表现出相同的功能和外观`Paging.aspx`。

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>增强 ProductsBLL 包括默认分页和排序方法

在上一教程中，我们将创建`GetProductsAsPagedDataSource(pageIndex, pageSize)`中的方法`ProductsBLL`类返回`PagedDataSource`对象。 这`PagedDataSource`对象已填入*所有*的产品 (通过 BLL s`GetProducts()`方法)，但只有那些对应于指定的记录时绑定到 DataList *pageIndex*并*pageSize*显示输入的参数。

在本教程前面添加了排序支持通过指定的排序表达式从 ObjectDataSource 的`Selecting`事件处理程序。 此用法非常有效 ObjectDataSource 时返回一个对象，可以进行排序，如`ProductsDataTable`返回的`GetProducts()`方法。 但是，`PagedDataSource`返回对象`GetProductsAsPagedDataSource`方法不支持其内部数据源的排序。 相反，我们需要进行排序，从返回的结果`GetProducts()`方法*之前*我们将其放入`PagedDataSource`。

若要实现此目的，创建中的新方法`ProductsBLL`类， `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`。 若要进行排序`ProductsDataTable`返回的`GetProducts()`方法中，指定`Sort`其默认值的属性`DataTableView`:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`GetProductsSortedAsPagedDataSource`方法只稍有不同从`GetProductsAsPagedDataSource`在上一教程中创建的方法。 具体而言，`GetProductsSortedAsPagedDataSource`接受其他输入的参数`sortExpression`，并将分配此值设置为`Sort`的属性`ProductDataTable`s `DefaultView`。 少量的代码更高版本，行`PagedDataSource`分配对象 s 数据源`ProductDataTable`s `DefaultView`。

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>调用 GetProductsSortedAsPagedDataSource 方法并指定 SortExpression 输入参数的值

使用`GetProductsSortedAsPagedDataSource`方法完成下, 一步是为此参数提供值。 在 ObjectDataSource`SortingWithDefaultPaging.aspx`当前配置为调用`GetProductsAsPagedDataSource`方法，并通过其两个在两个输入参数中的传递`QueryStringParameters`，指定在`SelectParameters`集合。 这两个`QueryStringParameters`指示的源`GetProductsAsPagedDataSource`s 方法*pageIndex*并*pageSize*参数来自查询字符串字段`pageIndex`和`pageSize`。

更新的 ObjectDataSource s`SelectMethod`属性，以便它调用新`GetProductsSortedAsPagedDataSource`方法。 然后，添加一个新`QueryStringParameter`，以便*sortExpression*从查询字符串字段访问输入的参数`sortExpression`。 设置`QueryStringParameter`s`DefaultValue`为产品名称。

这些更改后的 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample6.aspx)]

此时，`SortingWithDefaultPaging.aspx`页将按产品名称按字母顺序排序其结果 （请参阅图 9）。 这是因为，默认情况下，值为产品名称作为传入`GetProductsSortedAsPagedDataSource`s 方法*sortExpression*参数。


[![默认情况下，对结果进行排序的产品名称](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)

**图 9**： 默认情况下，对结果进行排序由`ProductName`([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image25.png))


如果你手动添加`sortExpression`查询字符串字段，如`SortingWithDefaultPaging.aspx?sortExpression=CategoryName`将对结果进行排序由指定`sortExpression`。 但是，这`sortExpression`参数未包含在查询字符串中，将移动到另一页数据时。 事实上，单击下一步或最后一页按钮的操作我们返回`Paging.aspx`！ 此外，有 s 当前未排序的接口。 用户可以更改分页的数据的排序顺序的唯一方法是通过直接操作在查询字符串。

## <a name="creating-the-sorting-interface"></a>创建排序的接口

我们首先需要更新`RedirectUser`方法将向用户发送`SortingWithDefaultPaging.aspx`(而不是`Paging.aspx`)，它包括`sortExpression`在查询字符串中的值。 我们还应添加一个只读的页面级名为`SortExpression`属性。 此属性，类似于`PageIndex`并`PageSize`在上一教程中创建的属性返回的值`sortExpression`查询字符串字段存在，如果和默认值 (ProductName)，否则。

当前`RedirectUser`方法接受仅单个输入的参数，要显示的页的索引。 但是，可能是我们想要将用户重定向到特定页面使用以外的新增功能在查询字符串中指定的排序表达式的数据。 稍后我们将创建此页上，将包括一系列按钮 Web 控件，用于对数据进行排序的指定列的排序接口。 单击这些按钮之一时，我们想要传递相应的排序表达式值中将用户重定向。 若要提供此功能，创建两个版本的`RedirectUser`方法。 第一个应接受仅页索引若要显示，而第二个接受的页索引和排序表达式。


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

在本教程中的第一个示例，我们将创建使用 DropDownList 排序接口。 对于此示例中，let s 使用三个按钮 Web 控件进行排序的上方 DataList 一个定位`ProductName`、 一个用于`CategoryName`，，另一个用于`SupplierName`。 添加三个按钮 Web 控件，设置其`ID`和`Text`属性正确：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample8.aspx)]

接下来，创建`Click`为每个事件处理程序。 事件处理程序应调用`RedirectUser`方法，并返回到使用相应的排序表达式的第一页的用户。


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

当首次访问的页面，按产品名称按字母顺序进行排序数据 （回头查看图 9）。 单击下一步按钮以转到第二个数据页，然后单击类别按钮的排序。 这将我们返回到按类别名称排序的数据的第一页 （请参阅图 10）。 同样，由供应商按钮单击排序对从数据的第一页开始的供应商数据进行排序。 如将数据分页通过记住排序选项。 图 11 显示后按类别排序，然后然后转到第 13 个数据页的页。


[![产品按类别排序](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)

**图 10**： 按类别排序的产品 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image28.png))


[![排序表达式是记住分页通过数据时](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image29.png)

**图 11**: 排序表达式是记住分页通过数据时 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image31.png))


## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>通过 Repeater 中的记录的步骤 6： 自定义分页

DataList 示例检查在步骤中通过使用效率低下默认分页方法及其数据的 5 个页面。 时分页的数据量足够大，则必须使用自定义分页。 回到[有效地分页通过大数量的数据](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)和[自定义分页对数据进行排序](../paging-and-sorting/sorting-custom-paged-data-vb.md)教程，我们检查的 BLL 中默认和自定义分页和创建的方法的区别利用自定义分页和排序自定义分页的数据。 具体而言，在这些两个以前的教程，我们添加到以下三种方法`ProductsBLL`类：

- `GetProductsPaged(startRowIndex, maximumRows)` 返回从开始记录的特定子集*startRowIndex*和不超过*值*。
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` 返回按指定的记录的特定子集*sortExpression*输入的参数。
- `TotalNumberOfProducts()` 提供了中的记录总数`Products`数据库表。

这些方法可用于高效地页上，并通过使用 DataList 或 Repeater 控件的数据进行排序。 为了说明这一点，让我们来首先创建 Repeater 控件具有自定义分页支持;然后，我们将添加排序功能。

打开`SortingWithCustomPaging.aspx`页中`PagingSortingDataListRepeater`文件夹并将 Repeater 添加到页上，设置其`ID`属性设置为`Products`。 在 Repeater s 智能标记，创建名为新 ObjectDataSource `ProductsDataSource`。 将其配置为选择从其数据`ProductsBLL`类的`GetProductsPaged`方法。


[![配置对象数据源使用 ProductsBLL 类的 GetProductsPaged 方法](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image32.png)

**图 12**： 配置为使用 ObjectDataSource`ProductsBLL`类 s`GetProductsPaged`方法 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image34.png))


设置下拉列表中插入、 更新和删除选项卡添加到 （无），然后单击下一步按钮。 配置数据源向导现在会提示对的源`GetProductsPaged`s 方法*startRowIndex*并*值*输入参数。 在现实中，将忽略这些输入的参数。 相反， *startRowIndex*并*值*值将通过传入`Arguments`属性中的 ObjectDataSource 的`Selecting`事件处理程序，就像我们指定的方式*sortExpression*中第一篇教程 s 的演示。 因此，将参数源保留在向导中设置为 None 的下拉列表。


[![将参数源设置为 None](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image35.png)

**图 13**： 保留参数源设置为无 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image37.png))


> [!NOTE]
> 不要*不*设置的 ObjectDataSource s`EnablePaging`属性设置为`true`。 这将导致对象数据源，将自动包含其自身*startRowIndex*并*值*参数`SelectMethod`s 现有参数列表。 `EnablePaging`属性绑定自定义分页到 GridView、 detailsview 和 FormView 控件的数据，因为遇到 ObjectDataSource s 中的某些行为，这些控件时很有用时才可用`EnablePaging`属性是`true`。 由于我们必须手动添加的 DataList 和 Repeater 分页支持，因此将此属性设置为`false`（默认值），因为我们将直接在我们的 ASP.NET 页面中完了所需的功能。


最后，定义 Repeater 的`ItemTemplate`以便显示产品的名称、 类别和供应商。 这些更改后 Repeater 和 ObjectDataSource s 声明性语法应看起来类似于下面：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample10.aspx)]

请花费片刻时间，请访问通过浏览器页面，并记下不返回任何记录。 这是因为我们尚未以指定的 ve *startRowIndex*和*值*参数值; 因此，值为 0 传递中两个。 若要指定这些值，请创建事件处理程序的 ObjectDataSource s`Selecting`事件并设置这些参数值以编程方式为硬编码值为 0，5，分别：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample11.vb)]

进行此更改后，页上，当浏览器中，通过查看显示前五个产品。


[![显示前五个记录](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image38.png)

**图 14**： 显示前五个记录 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image40.png))


> [!NOTE]
> 图 14 中列出的产品碰巧按产品名称排序，因为`GetProductsPaged`执行高效的自定义分页查询的存储的过程通过对结果进行排序`ProductName`。


若要允许用户浏览所有页面，我们需要跟踪的起始行索引和最大行数和回发之间保留这些值。 在默认的分页示例中我们使用查询字符串字段以保留这些值;对于此演示，让我们来永久保存此页的视图状态信息。 创建以下两个属性：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample12.vb)]

接下来，更新选择事件处理程序中的代码，以便它使用`StartRowIndex`和`MaximumRows`属性而不是 0 和 5 的硬编码值：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample13.vb)]

此时我们的页面仍将显示的前五个记录为止。 但是，使用这些属性中的位置，我们准备就绪后，若要创建我们分页界面。

## <a name="adding-the-paging-interface"></a>添加分页接口

允许的使用相同的第一个、 上一步、 下一步上, 一次分页接口用于默认分页示例，其中包括查看显示哪些页数据的控件，则标签 Web 和存在多少总页数。 添加四个按钮 Web 控件和 Repeater 下方的标签。


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample14.aspx)]

接下来，创建`Click`的四个按钮的事件处理程序。 单击其中一个按钮时，我们需要更新`StartRowIndex`和重新绑定到 Repeater 的数据。 第一个、 上一步，和下一步按钮的代码非常简单，但对于最后一个按钮如何我们确定数据的最后一页的起始行索引？ 若要计算此索引，以及能够确定是否应启用下一步和最后一个按钮，我们需要知道总共多少条记录已被分页通过。 我们可以通过调用来确定这`ProductsBLL`类的`TotalNumberOfProducts()`方法。 允许 s 创建一个名为只读的、 页面级别属性`TotalRowCount`返回的结果`TotalNumberOfProducts()`方法：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample15.vb)]

使用此属性现在我们可以确定最后一个页面 + s 起始行索引。 具体而言，它 s 整数结果的`TotalRowCount`减 1 除以`MaximumRows`，再乘以`MaximumRows`。 现在，我们可以编写`Click`的四个分页界面按钮事件处理程序：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample16.vb)]

最后，我们需要查看的最后一页时查看数据和下一步和最后一个按钮的第一页时禁用分页界面中的第一个和上一步按钮。 若要完成此操作，请将以下代码添加到 ObjectDataSource 的`Selecting`事件处理程序：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample17.vb)]

添加这些后`Click`事件处理程序和代码以启用或禁用分页界面元素基于当前的起始行索引，在浏览器中测试页。 如图 15 所示，当首次访问页面第一个和上一步按钮将处于禁用状态。 单击下一步显示第二个数据页中的，单击上一次显示的最后一页时 （请参阅图 16 和 17）。 查看数据的最后一页时的下一步和最后一个按钮被禁用。


[![上一步和最后一个按钮已禁用时查看第一个产品页](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image41.png)

**图 15**： 查看第一个产品页时，将禁用上一个和最后一个按钮 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image43.png))


[![第二个产品页是全都](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image44.png)

**图 16**： 产品第二个页面是全都 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image46.png))


[![单击最后一个显示数据的最后一页](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image47.png)

**图 17**： 单击上一次显示的最后一个数据页 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image49.png))


## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>步骤 7： 包括排序使用的自定义支持分页 Repeater

现在，已实现自定义分页，我们准备就绪后，若要包括排序支持。 `ProductsBLL`类 s`GetProductsPagedAndSorted`方法具有相同*startRowIndex*并*值*输入参数作为`GetProductsPaged`，但它允许其他*sortExpression*输入的参数。 若要使用`GetProductsPagedAndSorted`方法从`SortingWithCustomPaging.aspx`，我们需要执行以下步骤：

1. 更改 ObjectDataSource s`SelectMethod`属性从`GetProductsPaged`到`GetProductsPagedAndSorted`。
2. 添加*sortExpression* `Parameter`对象为 ObjectDataSource 的`SelectParameters`集合。
3. 创建专用的页级`SortExpression`通过页的视图状态的回发中保留其值的属性。
4. 更新的 ObjectDataSource s`Selecting`事件处理程序分配的 ObjectDataSource s *sortExpression*参数的值的页级`SortExpression`属性。
5. 创建排序的接口。

通过更新 ObjectDataSource s 开始`SelectMethod`属性并添加*sortExpression* `Parameter`。 请确保*sortExpression* `Parameter` s`Type`属性设置为`String`。 以后完成前两项任务，ObjectDataSource s 声明性标记看起来应如下所示：


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample18.aspx)]

接下来，我们需要一个页面级`SortExpression`属性的值序列化，以查看状态。 如果已设置排序表达式值，使用产品名称为默认值：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample19.vb)]

ObjectDataSource 调用之前`GetProductsPagedAndSorted`方法，我们需要设置*sortExpression* `Parameter`的值`SortExpression`属性。 在`Selecting`事件处理程序中，添加以下代码行：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample20.vb)]

所有的就是实现排序的接口。 与我们在上一示例中，可让具有排序实现的接口使用三个按钮 Web 控件允许用户对结果进行排序的产品名称、 类别或供应商的 s。


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample21.aspx)]

创建`Click`这三个按钮控件的事件处理程序。 在事件处理程序，重置`StartRowIndex`为 0，设置`SortExpression`到适当的值，并重新绑定到 Repeater 的数据：


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample22.vb)]

该 s 都在这里就简单 ！ 虽然没有一系列步骤，若要获取自定义分页和排序实现，已非常类似于所需的默认分页执行步骤。 图 18 查看数据时按类别排序的最后一页时显示的产品。


[![显示数据的最后一页上，按类别中，](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image50.png)

**图 18**： 显示数据最后一页上，按类别 ([单击以查看实际尺寸的图像](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image52.png))


> [!NOTE]
> 在上一示例中，供应商供应商名称已使用的排序表达式进行排序时。 但是，有关自定义分页实现过程，我们需要使用公司名称。 这是因为存储的过程负责实现自定义分页`GetProductsPagedAndSorted`将传递到排序表达式`ROW_NUMBER()`关键字，`ROW_NUMBER()`关键字需要实际的列名称而不是别名。 因此，我们必须使用`CompanyName`(在列的名称`Suppliers`表) 而不是在中使用的别名`SELECT`查询 (`SupplierName`) 的排序表达式。


## <a name="summary"></a>总结

既不 DataList 和 Repeater 提供排序的内置支持，但可以在进行少量的代码和自定义排序界面，添加此类功能。 在实现排序，但不是分页时，可以通过指定的排序表达式`DataSourceSelectArguments`对象传递到 ObjectDataSource 的`Select`方法。 这`DataSourceSelectArguments`对象 s`SortExpression`可以将属性分配中的 ObjectDataSource 的`Selecting`事件处理程序。

若要添加到 DataList 或 Repeater 已提供分页支持的排序功能，最简单的方法是自定义业务逻辑层包含接受的排序表达式的方法。 此信息然后中通过 ObjectDataSource s 中的参数传递`SelectParameters`。

本教程中完成分页和排序使用 DataList 和 Repeater 控件的探讨。 我们的下一步和最后一个教程将介绍如何将按钮 Web 控件添加到 DataList 和 Repeater 的模板，以便在每个项的基础上提供某些自定义、 用户启动的功能。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 David Suru。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
