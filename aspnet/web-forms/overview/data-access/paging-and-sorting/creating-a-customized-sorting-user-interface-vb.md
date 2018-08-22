---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
title: 创建自定义的排序用户界面 (VB) |Microsoft Docs
author: rick-anderson
description: 显示一长串的已排序数据，它可以是非常有帮助通过引入分隔符行组相关的数据。 在本教程中我们将了解如何创建...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: f3897a74-cc6a-4032-8f68-465f155e296a
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: b12baa5075b4e67018d8a98a92e807d1778737c8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824844"
---
<a name="creating-a-customized-sorting-user-interface-vb"></a>创建自定义的排序用户界面 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_VB.exe)或[下载 PDF](creating-a-customized-sorting-user-interface-vb/_static/datatutorial27vb1.pdf)

> 显示一长串的已排序数据，它可以是非常有帮助通过引入分隔符行组相关的数据。 在本教程中我们将了解如何创建此类的排序用户界面。


## <a name="introduction"></a>介绍

当显示一长串的已排序数据有少量的已排序的列中的不同值，最终用户可能会发现很难识别，确实如此，区别边界发生。 例如，有在数据库中，但仅有九个不同的类别选项 81 产品 (八个唯一类别以及`NULL`选项)。 请考虑有兴趣查看属于 Seafood 类别的产品的用户的情况。 从列出的页面*所有*单一 GridView 中的产品，用户可能会决定其最好的方法就是对结果进行排序的类别，将组合在一起的所有 Seafood 产品组合在一起。 按类别进行排序后, 用户然后需要 hunt 整个列表，寻找 Seafood 分组产品开始和结束的位置。 由于对结果进行按字母顺序排序的查找 Seafood 产品类别名称并不困难，但它仍需要仔细扫描中网格项的列表。

为了突出显示已排序组之间的边界，很多网站，请使用一个用户界面，将添加此类组之间的分隔符。 图 1 所示类似的分隔符使用户能够更快地查找特定组和标识其边界，以及确定在数据中存在哪些不同的组。


[![每个类别组是明确标识](creating-a-customized-sorting-user-interface-vb/_static/image2.png)](creating-a-customized-sorting-user-interface-vb/_static/image1.png)

**图 1**： 每个类别组是明确标识 ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image3.png))


在本教程中我们将了解如何创建此类的排序用户界面。

## <a name="step-1-creating-a-standard-sortable-gridview"></a>步骤 1： 创建标准的可排序的 GridView

我们将探讨如何增强 GridView 来提供增强的排序接口之前，让我们来首先创建一个标准的可排序的 GridView，列出的产品。 首先打开`CustomSortingUI.aspx`页中`PagingAndSorting`文件夹。 向页面添加一个 GridView，设置其`ID`属性设置为`ProductList`，并将其绑定到新对象数据源。 配置要使用 ObjectDataSource`ProductsBLL`类的`GetProducts()`用于选择记录的方法。

接下来，以便它仅包含配置 GridView `ProductName`， `CategoryName`， `SupplierName`，和`UnitPrice`BoundFields 和停用 CheckBoxField。 最后，配置 GridView 支持排序 GridView s 智能标记中的启用排序复选框 (或通过设置其`AllowSorting`属性设置为`true`)。 建立到这些新增功能后`CustomSortingUI.aspx`页上，在声明性标记应如下所示：


[!code-aspx[Main](creating-a-customized-sorting-user-interface-vb/samples/sample1.aspx)]

请花费片刻时间为止的浏览器中查看我们的进度。 图 2 显示了可排序的 GridView，其数据按类别按字母顺序进行排序时。


[![可排序的 GridView s 数据按类别排序](creating-a-customized-sorting-user-interface-vb/_static/image5.png)](creating-a-customized-sorting-user-interface-vb/_static/image4.png)

**图 2**： 按类别排序数据的可排序的 GridView s ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image6.png))


## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>步骤 2： 添加分隔符行浏览技术

使用通用的可排序 GridView 中完成，所有的就是为了能够在每个唯一的已排序组之前 GridView 中添加分隔符行。 但如何可以这样的行注入到 GridView？ 从根本上来说，我们需要进行循环访问，GridView 的行，确定已排序的列的值之间的差异的发生位置，然后添加适当的分隔符行。 当考虑此问题，人们似乎很自然的解决方案处于某个位置中的 GridView 的`RowDataBound`事件处理程序。 如中所述[自定义格式设置基于数据的](../custom-formatting/custom-formatting-based-upon-data-vb.md)教程中，应用行级别格式基于行的数据时，通常使用此事件处理程序。 但是，`RowDataBound`事件处理程序不在这里，该解决方案，因为行不能添加到 GridView 以编程方式从此事件处理程序。 GridView 的`Rows`集合，实际上，是只读的。

若要将其他行添加到 GridView 我们有三个选择：

- 将这些元数据分隔符行添加到绑定到 GridView 的实际数据
- GridView 已绑定到数据后，将添加其他`TableRow`实例到 GridView s 控制集合
- 创建扩展了 GridView 控件并重写这些方法负责构造 GridView 的结构的自定义服务器控件

创建自定义服务器控件将是最好的方法，此功能需要多个网页上或跨多个网站。 但是，它将需要一小段代码和到探索的全面探讨，GridView s 内部工作原理。 因此，我们将不考虑该选项对于本教程。

其他两种选项添加分隔符行的实际数据被绑定到 GridView 和 GridView 的控件集合后操作其已绑定-以不同方式攻击问题，值得讨论。

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>将行添加到数据绑定到 GridView

在 GridView 绑定到数据源，它会创建`GridViewRow`为数据源返回每个记录。 因此，我们可以通过添加分隔符记录到数据源绑定到 GridView 之前插入所需的分隔符行。 图 3 说明了这一概念。


![一种方法涉及将分隔符行添加到数据源](creating-a-customized-sorting-user-interface-vb/_static/image7.png)

**图 3**： 一种方法涉及将分隔符行添加到数据源


我在引号中使用术语分隔符记录，因为没有特殊的分隔符记录;相反，我们必须以某种方式的标记中的数据源的特定记录用作分隔符，而不是普通的数据行。 有关我们的示例，我们重新绑定`ProductsDataTable`实例与 GridView，由组成`ProductRows`。 我们可能会通过设置一条记录标记为一个分隔符行及其`CategoryID`属性设置为`-1`（因为通常情况下存在一个此类值无法 t）。

若要利用此技术 d 我们需要执行以下步骤：

1. 以编程方式检索的数据绑定到 GridView (`ProductsDataTable`实例)
2. 基于 GridView s 上的数据进行排序`SortExpression`和`SortDirection`属性
3. 循环访问`ProductsRows`在`ProductsDataTable`，他们寻求在已排序的列中的差异的存在位置
4. 在每个组边界注入分隔符记录`ProductsRow`实例到 DataTable，它具有 s`CategoryID`设置为`-1`（或任何指定决定时将标记作为分隔符记录一条记录）
5. 插入分隔符行之后, 以编程方式将数据绑定到 GridView

除了上述五个步骤 d 我们还需要提供事件处理程序的 GridView s`RowDataBound`事件。 在这里，我们 d 检查每个`DataRow`并确定它是一个分隔符行，其中一个其`CategoryID`设置的`-1`。 如果是这样，我们 d 可能想要调整其格式设置或单元中显示的文本。

使用此方法，因为您需要一个事件处理程序还为 GridView s 注入排序组边界需要多做一些工作不是，上面所述`Sorting`的跟踪事件并保留`SortExpression`和`SortDirection`值。

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>操作 GridView s s 控制其后集合被数据绑定

而不是消息之前将其绑定到 GridView 数据，我们可以添加分隔符行*后*数据绑定到 GridView。 GridView 的控件层次结构，这实际上是生成的数据绑定过程只需`Table`实例组成的行，其中每个由单元格的集合的集合。 具体而言，GridView 的控件集合包含`Table`对象在其根目录`GridViewRow`(它派生自`TableRow`类) 中每个记录`DataSource`绑定到 GridView，和一个`TableCell`中每个对象`GridViewRow`实例中每个数据字段`DataSource`。

若要添加每个排序组之间的分隔符行，我们可以直接操作此控件层次结构后已创建。 我们可以确信 GridView 的控件层次结构已创建最后一次通过呈现页面时的时间。 因此，这种方法都会重写`Page`类的`Render`方法，此时 GridView s 最终的控件层次结构更新以包含所需的分隔符的行。 图 4 说明了此过程。


[![一种替代方式操作 GridView 的控件层次结构](creating-a-customized-sorting-user-interface-vb/_static/image9.png)](creating-a-customized-sorting-user-interface-vb/_static/image8.png)

**图 4**： 一种替代方式操作 GridView 的控件层次结构 ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image10.png))


对于本教程，我们将使用此后一种方法自定义排序的用户体验。

> [!NOTE]
> 代码我在本教程中的 m 呈现基于中提供的示例[Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx)的博客条目[播放与 GridView 排序分组位](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)。


## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>步骤 3： 将分隔符行添加到 GridView 的控件层次结构

由于我们只想要将分隔符行添加到 GridView 的控件层次结构，被创建并在该页面，请访问最后一次创建其控件层次结构后，我们希望执行结束时此添加的页面生命周期，但在实际的 GridView c 之前管理下层次结构已呈现为 HTML。 此时我们可以实现此目的的最新可能点是`Page`类的`Render`事件，我们可以在我们使用以下方法签名的代码隐藏类中重写：


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample2.vb)]

当`Page`类 s 原始`Render`方法调用`base.Render(writer)`每个页面中控件将呈现，生成基于其控件层次结构的标记。 因此，它是命令性，我们都调用`base.Render(writer)`，以便呈现页面时，和我们处理的 GridView s 控件层次结构在调用之前`base.Render(writer)`，以便分隔符行已添加到之前的 GridView 的控件层次结构s 已呈现。

若要插入排序组标头我们首先需要确保用户已请求对数据进行排序。 默认情况下，未排序的 GridView 的内容，并因此我们不需要输入任何组排序标头。

> [!NOTE]
> 如果你想 GridView，其中首次加载页面时按特定列进行排序，调用 GridView 的`Sort`方法上第一次的页面访问 （但不是在后续回发）。 若要完成此操作，添加此调用中的`Page_Load`事件处理程序内的`if (!Page.IsPostBack)`条件。 回头[分页和排序报表数据](paging-and-sorting-report-data-vb.md)有关的详细信息的教程信息`Sort`方法。


假设数据已排序，我们的下一个任务是确定哪些列的数据已按排序，然后扫描查找差异 s，该列中的行值。 下面的代码可确保数据已排序和查找数据已排序所依据的列：


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample3.vb)]

如果这个 GridView 有尚未为排序，GridView 的`SortExpression`属性将不设置。 因此，我们只想添加分隔符行，如果此属性具有某个值。 如果是这样，我们接下来需要确定的数据已排序所依据的列的索引。 这通过循环遍历 GridView s 实现`Columns`集合，它的搜索列`SortExpression`属性等于 GridView 的`SortExpression`属性。 除了列的索引中，我们还获取`HeaderText`显示分隔符行时使用的属性。

对数据进行排序所依据的索引，最后一步是列的要枚举的 GridView 行。 每个行，我们需要确定是否已排序的列的值与以前的行排序的 s 列的值不同。 因此，我们需要将一个新如果`GridViewRow`在控件层次结构的实例。 这是使用以下代码来实现：


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample4.vb)]

此代码以编程方式引用`Table`对象的 GridView 的控件层次结构的根位置找到并创建一个名为的字符串变量`lastValue`。 `lastValue` 用于当前行排序的 s 列值与上一个行的值进行比较。 下一步，GridView s`Rows`枚举集合和每个行的已排序的列的值存储在`currentValue`变量。

> [!NOTE]
> 若要确定特定行排序的 s 列的值，我使用的单元格的`Text`属性。 这非常适合 BoundFields，但将不按预期方式工作的 Templatefield，CheckBoxFields，等等。 我们将介绍如何立即考虑备用 GridView 字段。


`currentValue`和`lastValue`变量然后进行比较。 如果它们不同，我们需要将一个新的分隔符行添加到的控件层次结构。 这通过确定的索引来实现`GridViewRow`中`Table`对象 s`Rows`集合中，创建新`GridViewRow`并`TableCell`实例，并添加`TableCell`和`GridViewRow`到控件层次结构。

注意分隔符行 s 单独`TableCell`的格式设置该视图所跨越整个宽度的 GridView 中，使用格式化`SortHeaderRowStyle`CSS 类，并具有其`Text`属性等，其中显示这两个组的排序名称 （如类别） 和组 s 的值 （如饮料）。 最后，`lastValue`将更新的值为`currentValue`。

用于设置格式的排序的组头行的 CSS 类`SortHeaderRowStyle`需要在指定`Styles.css`文件。 可随意使用任何样式设置有吸引力;我使用了以下程序：


[!code-css[Main](creating-a-customized-sorting-user-interface-vb/samples/sample5.css)]

当前代码的排序接口添加排序组标头，通过任何 BoundField 进行排序时 （请参阅图 5 中，其中显示了屏幕截图，供应商进行排序时）。 但是，按任何其他字段类型 （如 CheckBoxField 或 TemplateField） 进行排序，排序组标头时，却找不到 （见图 6）。


[![排序接口通过 BoundFields 进行排序时包含对组排序标头](creating-a-customized-sorting-user-interface-vb/_static/image12.png)](creating-a-customized-sorting-user-interface-vb/_static/image11.png)

**图 5**: 排序接口包括排序组标头时排序通过 BoundFields ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image13.png))


[![排序组标头是缺少时排序 CheckBoxField](creating-a-customized-sorting-user-interface-vb/_static/image15.png)](creating-a-customized-sorting-user-interface-vb/_static/image14.png)

**图 6**: 排序组标头是缺少时排序 CheckBoxField ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image16.png))


通过 CheckBoxField 进行排序时，排序组标头会缺失的原因在于，代码当前只需使用`TableCell`s`Text`属性来确定已排序的列的每一行的值。 CheckBoxFields，对于`TableCell`s`Text`属性为空字符串; 相反，值是可通过位于内的复选框 Web 控件`TableCell`s`Controls`集合。

若要处理 BoundFields 以外的字段类型，我们需要扩充代码位置`currentValue`变量赋值来检查是否存在中的复选框`TableCell`s`Controls`集合。 而不是使用`currentValue = gvr.Cells(sortColumnIndex).Text`，此代码替换为以下代码：


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample6.vb)]

此代码会检查已排序的列`TableCell`确定是否有任何控件中的当前行`Controls`集合。 如果有，并且第一个控件是一个复选框`currentValue`变量设置为是或否，具体取决于复选框的`Checked`属性。 否则，值取自`TableCell`s`Text`属性。 可以复制此逻辑以处理对 GridView 中可能存在任何 Templatefield 进行排序。

上面的代码添加，现通过停止使用 CheckBoxField 进行排序时存在排序组标头 （请参阅图 7）。


[![排序组标头是现在存在时排序 CheckBoxField](creating-a-customized-sorting-user-interface-vb/_static/image18.png)](creating-a-customized-sorting-user-interface-vb/_static/image17.png)

**图 7**: 排序组标头是现在存在时排序 CheckBoxField ([单击以查看实际尺寸的图像](creating-a-customized-sorting-user-interface-vb/_static/image19.png))


> [!NOTE]
> 如果使用的产品`NULL`数据库的值`CategoryID`， `SupplierID`，或`UnitPrice`字段，这些值将显示为 GridView 中的空字符串默认情况下，这分隔符行的文本意味着与这些产品`NULL`值将读取为类似类别: (即，有 s 类别之后没有名称： 喜欢个类别： 饮料)。 如果你想在此处显示的值可以设置 BoundFields [ `NullDisplayText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx)于文本要显示或分配时，可以在 Render 方法中添加一个条件语句`currentValue`为分隔符行的`Text`属性。


## <a name="summary"></a>总结

GridView 不包括用于自定义排序接口的多个内置选项。 但是，对于一些低级别代码，它可以调整 GridView 的控件层次结构，以创建更多自定义的接口。 在本教程中我们已了解如何为一个可排序的 GridView，更轻松地标识不同的组和这些组边界添加排序组分隔符行。 有关自定义排序接口的其他示例，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/) s[几个 ASP.NET 2.0 GridView 排序提示和技巧](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx)博客文章。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一篇](sorting-custom-paged-data-vb.md)
