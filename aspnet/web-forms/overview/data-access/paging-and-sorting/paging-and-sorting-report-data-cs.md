---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: 分页和排序报表数据 (C#) |Microsoft Docs
author: rick-anderson
description: 分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。 在本教程中我们将首先看一下添加排序和...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ebef919deeda409cfa6805b603f67ef96ff003e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830058"
---
<a name="paging-and-sorting-report-data-c"></a>分页和排序报表数据 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe)或[下载 PDF](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> 分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。 在本教程中，我们将首先看一下添加排序和分页至我们的报表，然后，我们将生成后在将来的教程。


## <a name="introduction"></a>介绍

分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。 例如，搜索的一家网上书店在 ASP.NET 书籍时，可能有数百个此类书籍，但搜索结果中列出该报表列出每页的十个匹配项。 此外，可以按标题、 价格、 页数、 作者姓名等对结果进行排序。 而的过去 23 教程已介绍了如何生成各种报告，包括接口，它允许添加、 编辑和删除数据，我们不了解了如何对数据和唯一进行排序的已分页示例我们 ve 看到已与 DetailsView 和 FormView控件。

在本教程中我们将了解如何添加排序和分页至我们的报表，这可以通过只需检查几个复选框来完成。 遗憾的是，这个简单的实施有排序接口会使一些需要其缺点和分页例程并不设计用于高效地进行分页的大结果集。 将来的教程将探讨如何克服这些限制--现成的分页和排序的解决方案。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步骤 1： 添加分页和排序教程网页

在开始本教程之前，让我们来首先请花费片刻时间以添加我们需要为本教程和下一步的三个 ASP.NET 页面。 首先，创建一个新的文件夹在项目中名为`PagingAndSorting`。 接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面](paging-and-sorting-report-data-cs/_static/image1.png)

**图 1**： 创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面


接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。 此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中，枚举站点图，并在项目符号列表中的当前部分中显示这些教程。


![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](paging-and-sorting-report-data-cs/_static/image2.png)

**图 2**: SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx


为了使显示分页和排序的教程中我们将创建的项目符号列表，我们需要将它们添加到的站点映射。 打开`Web.sitemap`文件，并编辑、 插入、 和删除站点映射节点标记后添加以下标记：


[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](paging-and-sorting-report-data-cs/_static/image3.png)

**图 3**： 更新包括新的 ASP.NET 页面的站点图


## <a name="step-2-displaying-product-information-in-a-gridview"></a>步骤 2： 在 GridView 中显示的产品信息

我们实际上实现分页和排序功能之前，让我们来首先创建标准非-srotable，列出了产品信息的非可分页 GridView。 这是一项任务我们已多次在此之前完成本教程系列因此以下步骤应该比较熟悉。 首先打开`SimplePagingSorting.aspx`页上，并将 GridView 控件从工具箱拖到设计器中，设置其`ID`属性设置为`Products`。 接下来，创建新对象数据源使用 ProductsBLL 类的`GetProducts()`方法以返回所有产品信息。


![检索有关所有使用 GetProducts() 方法的产品信息](paging-and-sorting-report-data-cs/_static/image4.png)

**图 4**： 检索有关所有使用 GetProducts() 方法的产品信息


由于此报表不是只读的报告，在该处 s 需要映射的 ObjectDataSource s `Insert()`， `Update()`，或`Delete()`方法添加到相应`ProductsBLL`方法; 因此，（无） 从列表中选择下拉列表的 INSERT、 UPDATE和删除选项卡。


![选择 （无） 选项的下拉列表中插入、 更新和删除选项卡](paging-and-sorting-report-data-cs/_static/image5.png)

**图 5**： 选择 （无） 选项的下拉列表中插入、 更新和删除选项卡


接下来，让 s 自定义 GridView 的字段，以便显示仅产品名称、 供应商、 类别、 价格和已停止使用的状态。 此外，随意进行任何字段级格式设置发生更改，例如调整`HeaderText`属性或格式设置为货币的价格。 以后这些更改，您的 GridView s 声明性标记看起来应类似于下面：


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

图 6 显示了我们到目前为止的浏览器查看时。 请注意页面列出所有在一个屏幕中，显示每个产品的名称、 类别、 供应商、 价格、 产品和停用状态。


[![列出了每个产品](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**图 6**： 列出了每个产品 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image8.png))


## <a name="step-3-adding-paging-support"></a>步骤 3： 添加分页支持

列出*所有*的一个屏幕上的产品可能会导致用户仔细阅读数据的信息过载。 若要帮助使结果更易于管理，我们可以分解成较小的数据页的数据，并允许用户一次遍历一页数据。 若要完成这只需检查从 GridView s 智能标记启用分页复选框 (这将设置 GridView s [ `AllowPaging`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)到`true`)。


[![检查启用分页复选框来添加分页支持](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**图 7**： 选中启用分页复选框以添加分页支持 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image11.png))


启用分页限制每个页面所显示的记录数和添加*分页界面*到 GridView。 图 7 中所示的默认分页界面是页码，这样就允许用户从一页数据快速导航到另一系列。 此分页接口应该很熟悉，因为我们已在过去的教程中将分页支持添加到 DetailsView 和 FormView 控件时看到它。

在 DetailsView 和 FormView 控件仅显示每页的单个记录。 GridView 中，但是，会查询其[`PageSize`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)以确定每页显示的记录数 （此属性默认为值为 10）。

可以使用以下属性自定义此 GridView、 DetailsView 和 FormView 的分页接口：

- `PagerStyle` 指示分页界面的样式信息可以指定设置，例如`BackColor`， `ForeColor`， `CssClass`， `HorizontalAlign`，依次类推。
- `PagerSettings` 包含一系列的属性，可以自定义分页界面中; 的功能`PageButtonCount`指示数字页号 （默认值为 10） 在分页界面中显示的最大数目; [ `Mode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)指示分页界面如何进行操作并可以将设置为： 

    - `NextPrevious` 显示允许用户若要逐步向前或向后一页一次下一步和上一步按钮
    - `NextPreviousFirstLast` 除了下一步和上一步按钮，第一个和最后一个按钮，还提供了，这样就允许用户快速移动到第一个或最后一个数据页
    - `Numeric` 显示页码，这样就允许用户立即跳转到任何页面的系列
    - `NumericFirstLast` 除了页码，包括第一个和最后一个按钮，允许用户以快速移动到的数据; 第一个或最后一页第一个/最后一个按钮才会显示是否所有的数字页号不适合

此外，GridView、 DetailsView 和所有产品/服务的 FormView`PageIndex`和`PageCount`属性，分别指示当前正在查看的页和数据的总页数。 `PageIndex`属性编制了索引 0，这意味着，查看数据的第一页时开始`PageIndex`将等于 0。 `PageCount`计数 1，这意味着，但是，启动`PageIndex`仅限于值介于 0 和`PageCount - 1`。

允许 s 请花费片刻时间来提高我们 GridView 的分页接口的默认外观。 具体而言，让 s 具有浅灰色背景与右对齐的分页界面。 而不是设置这些属性直接通过 GridView s`PagerStyle`属性，让 s 创建中的 CSS 类`Styles.css`名为`PagerRowStyle`，然后将分配`PagerStyle`s`CssClass`通过我们的主题的属性。 首先打开`Styles.css`并添加以下 CSS 类定义：


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

接下来，打开`GridView.skin`文件中`DataWebControls`文件夹内的`App_Themes`文件夹。 如中所述*母版页和站点导航*教程，外观文件可用于指定 Web 控件的默认属性值。 因此，增加现有设置，以包含设置`PagerStyle`s`CssClass`属性设置为`PagerRowStyle`。 此外，let s 配置要显示最多五个数字页按钮使用的分页界面`NumericFirstLast`分页界面。


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>分页的用户体验

图 8 显示了 web 页上选中的 GridView s 启用分页复选框后，通过浏览器访问时，`PagerStyle`并`PagerSettings`通过进行了配置`GridView.skin`文件。 请注意如何唯一十个记录将显示，并且分页界面指示我们正在查看数据的第一页。


[![使用启用了分页，每次显示仅记录的子集](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**图 8**： 一次使用已启用分页，显示记录的一个子集 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image14.png))


当用户单击其中一个分页界面中的页码时，回发时，才会和页面重新加载请求的页面 + s 记录显示。 图 9 显示的结果，如果选择查看数据的最后一页。 请注意，最后一页仅包含一条记录;这是因为总数，从而导致与单独记录每个页面以及一页的 10 条记录的 8 个页面中有 81 记录。


[![单击页码导致回发，并显示相应记录的子集](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**图 9**： 单击页码导致回发并显示相应记录子集 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image17.png))


## <a name="paging-s-server-side-workflow"></a>分页的服务器端工作流

当最终用户单击分页界面中的按钮上时，回发时，才会和在以下服务器端工作流开始：

1. GridView s （或 DetailsView 或 FormView）`PageIndexChanging`触发事件
2. 重新请求 ObjectDataSource*所有*BLL; 中的数据的 GridView s`PageIndex`和`PageSize`属性值用于确定需要在 GridView 中显示的 BLL 从返回的记录
3. GridView 的`PageIndexChanged`触发事件

步骤 2 中，在 ObjectDataSource 重新请求所有其数据源中的数据。 这种样式的分页通常称为*默认分页*，因为它的分页行为使用默认情况下设置时`AllowPaging`属性设置为`true`。 默认值天真分页数据 Web 控件检索的数据，每个页面的所有记录，即使仅记录的子集实际呈现到的 HTML 发送到浏览器的 s。 除非数据库数据缓存的 BLL 或对象数据源，则默认分页，为足够大的结果集或 web 应用程序与多个并发用户处于无法工作。

在下一教程中，我们将介绍如何实现*自定义分页*。 使用自定义分页，您可以专门指示 ObjectDataSource 来仅检索精确的所需的请求的数据页的记录集。 可以想象，自定义分页极大地提高了效率较大的结果集进行分页。

> [!NOTE]
> 虽然许多用户同时使用分页通过足够大的结果集或的站点时，默认的分页不适合，意识到，自定义分页需要更多的更改和精力来实现，并且不是像选中一个复选框 （如是默认设置一样简单分页）。 因此，默认的分页可能是小型、 低流量的网站或相对较小的结果进行分页的设置时，因为它的最佳选择 s 更轻松、 更快速地实现。


例如，如果我们知道我们将在我们的数据库中永远不会有超过 100 个产品，通过它实现所需的工作量可能偏移享受的自定义分页的最小的性能提升。 如果，但是，我们可能会一天有数千甚至上万个产品*不*实现自定义分页会极大地妨碍我们的应用程序的可伸缩性。

## <a name="step-4-customizing-the-paging-experience"></a>步骤 4： 自定义分页体验

数据 Web 控件提供多个可用于增强用户的分页体验的属性。 `PageCount`属性，例如，指示有多少总页数是，虽然`PageIndex`属性指示当前正在访问的页，可以设置将用户快速移动到特定的页。 为了说明如何使用这些属性来改进用户的分页体验，让我们来添加一个标签 Web 控制对我们将通知用户哪些页面的页面它们重新当前访问，以及将 DropDownList 控件，其可快速跳转到任何给定页面.

首先，将标签 Web 控件添加到您的页面，设置其`ID`属性设置为`PagingInformation`，并将清除其`Text`属性。 接下来，创建事件处理程序的 GridView s`DataBound`事件，并添加以下代码：


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

此事件处理程序将分配`PagingInformation`标签 s`Text`属性设置为消息通知用户页面当前访问`Products.PageIndex + 1`出多少总页数`Products.PageCount`(我们将添加到 1`Products.PageIndex`属性因为`PageIndex`编制索引的索引从 0 开始)。 我选择将此标签 s`Text`中的属性`DataBound`事件处理程序，而不是`PageIndexChanged`事件处理程序由于`DataBound`事件将激发每次数据绑定到 GridView 而`PageIndexChanged`事件处理程序页索引更改时激发。 当 GridView 最初是绑定到的第一页上的数据访问时，`PageIndexChanging`事件不是 t 火灾 (而`DataBound`事件的作用)。

添加此元素后，用户现已显示一条消息指出正在访问哪些页面和有多少总页的数据。


[![显示当前页码和总页数](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**图 10**： 显示当前页码和总页数 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image20.png))


除了标签控件，让我们来还添加 DropDownList 控件，其中列出与当前正在查看的页面选择了 GridView 中的页码。 这里的思路是，用户可快速跳转从当前页到另一个只需从下拉列表中选择新的页索引。 首先将 DropDownList 添加到设计器中，设置其`ID`属性设置为`PageList`，从其智能标记启用自动回发选项。

接下来，返回到`DataBound`事件处理程序并添加以下代码：


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

此代码首先清除中项的布局`PageList`DropDownList。 这可能是多余的因为一个对 t 期望的页数，若要更改，但其他用户可能会同时使用系统、 添加或删除的记录`Products`表。 此类插入或删除无法更改数据的页数。

接下来，我们需要再次创建页号并具有一个映射到当前的 GridView`PageIndex`默认选中状态。 我们实现此目的使用从 0 到循环`PageCount - 1`，添加一个新`ListItem`中每个迭代和设置其`Selected`属性设置为 true，如果当前迭代索引等于 GridView 的`PageIndex`属性。

最后，我们需要创建的事件处理程序的 DropDownList s`SelectedIndexChanged`触发的事件，每当用户选择从列表中的另一个项。 若要创建此事件处理程序，只需双击在设计器，DropDownList，然后添加以下代码：


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

如图 11 所示，只更改 GridView 的`PageIndex`属性会导致数据重新绑定到 GridView。 在 GridView`DataBound`事件处理程序，相应的 DropDownList`ListItem`处于选中状态。


[![用户将自动转到第六个页时选择页面 6 下拉列表项](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**图 11**: 用户将自动转到第六个页时选择页面 6 下拉列表项 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image23.png))


## <a name="step-5-adding-bi-directional-sorting-support"></a>步骤 5： 添加排序的双向支持

添加双向语言排序支持非常简单，只添加分页支持只需选中 GridView s 智能标记中的启用排序选项 (用于设置 GridView s [ `AllowSorting`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)到`true`)。 这会使每个的 GridView 的字段标头作为 Linkbutton，单击时，会导致回发并返回按所单击的列以升序排序的数据。 再次单击 LinkButton 的同一个标头重新对数据进行排序降序排序。

> [!NOTE]
> 如果使用自定义的数据访问层而不是类型化数据集，您可能没有启用排序的选项中的 GridView s 智能标记。 仅绑定到数据源以本机方式支持排序的 Gridview 有可用此复选框。 类型化数据集提供了开箱排序支持，因为 ADO.NET DataTable 提供`Sort`方法，调用时，对使用指定的条件的 Datarow 的 DataTable s 进行排序。


如果将 DAL 不返回由 DAL 的本机支持排序将需要配置 ObjectDataSource 要传递给业务逻辑层，以对数据进行排序或具有数据的排序信息排序的对象。 我们将探讨如何对数据的业务逻辑和数据访问层在将来的教程中进行排序。

排序 Linkbutton 呈现为 HTML 超链接，其当前的颜色 （蓝色表示未访问的链接和已访问链接深红色） 冲突与标题行的背景色。 相反，let s 具有所有标头行链接中显示为空白，而不管是否它们 ve 已或未访问过。 这可以通过添加以下`Styles.css`类：


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

此语法指示要显示的元素，使用 HeaderStyle 类中的这些超链接时使用白色文本。

之后此 CSS 元素后，访问通过浏览器页面时在屏幕上将看到类似于图 12。 具体而言，图 12 显示结果后单击价格字段 s 标头链接。


[![结果已按升序排序单价](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**图 12**: 结果具有已按升序顺序单价 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image26.png))


## <a name="examining-the-sorting-workflow"></a>检查排序的工作流

所有 GridView 都字段 BoundField、 CheckBoxField、 TemplateField，并等具有`SortExpression`属性，指示应使用对数据进行排序时单击该字段 s 排序标头链接的表达式。 这个 GridView 也有`SortExpression`属性。 GridView 时单击 LinkButton 排序的标头，将该字段 s 分配`SortExpression`值设为其`SortExpression`属性。 接下来，并将数据重新检索 ObjectDataSource 中根据 GridView s 排序`SortExpression`属性。 以下列表详细说明了怎样时最终用户对 GridView 中的数据进行排序步骤的顺序：

1. GridView s [Sorting 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)激发
2. GridView s [ `SortExpression`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)设置为`SortExpression`字段的单击 LinkButton 了其排序的标头
3. ObjectDataSource 重新检索所有 BLL 中的数据，然后对使用 GridView s 的数据进行排序 `SortExpression`
4. GridView 的`PageIndex`属性重置为 0，这意味着，对用户进行排序时返回到数据 （假设实现分页支持） 的第一页
5. GridView s [ `Sorted`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)激发

像默认分页，请使用默认排序选项重新检索*所有*的 BLL 中的记录。 使用排序没有分页或在使用使用进行排序时的默认分页，那里 s 没有办法避开此性能下降 （除了缓存数据库数据）。 但是，正如我们在将来的教程中，将看到它可以有效地对数据进行排序时使用自定义分页。

每个 GridView 字段绑定到 GridView s 智能标记中的下拉列表通过 GridView ObjectDataSource 时, 自动有其`SortExpression`属性分配给中的数据字段的名称`ProductsRow`类。 例如， `ProductName` BoundField s`SortExpression`设置为`ProductName`，如下面的声明性标记中所示：


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

可以配置一个字段，以便它 s 不可排序通过清除其`SortExpression`属性 （将其分配给一个空字符串）。 为了说明这一点，想象一下，我们并没有 t 想要让客户对我们的产品价格进行排序。 `UnitPrice` BoundField 的`SortExpression`从声明性标记或通过字段对话框中 （这是通过单击 GridView s 智能标记中的编辑列链接的访问），可以删除属性。


![结果已按升序排序单价](paging-and-sorting-report-data-cs/_static/image27.png)

**图 13**： 结果已按升序排序单价


一次`SortExpression`属性已被移除。 `UnitPrice` BoundField 标头将呈现为文本而不是作为链接，从而防止用户对数据进行排序的价格。


[![通过删除 SortExpression 属性，用户不再可以进行排序的产品价格](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**图 14**： 通过删除 SortExpression 属性，用户可以不再对产品的价格 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image30.png))


## <a name="programmatically-sorting-the-gridview"></a>以编程方式排序 GridView

您还可以进行排序的 GridView 内容以编程方式使用 GridView s [ `Sort`方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)。 只需传入`SortExpression`值作为排序依据连同[ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending`或`Descending`)，GridView 的数据都将重新排序。

假设原因我们关闭排序通过`UnitPrice`是的因为我们担心我们的客户会只是购买仅价格最低的产品。 但是，我们想要鼓励他们购买的成本最高的产品，因此我们 d 喜欢它们能够进行排序的产品的价格，但只能从成本最高价格到最少。

若要完成这将按钮 Web 控件添加到页上，设置其`ID`属性设置为`SortPriceDescending`，并将其`Text`价格按排序的属性。 接下来，为 s 按钮创建一个事件处理程序`Click`通过双击设计器中的按钮控件的事件。 将以下代码添加到此事件处理程序：


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

单击此按钮使用户返回到第一页与按定价从最代价高昂的开销最少 （请参阅图 15） 排序的产品。


[![单击按钮进行排序的产品从成本最高到最低](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**图 15**： 单击的按钮进行排序的产品从最高到最少 ([单击以查看实际尺寸的图像](paging-and-sorting-report-data-cs/_static/image33.png))


## <a name="summary"></a>总结

在本教程中我们已了解如何实现默认分页和排序功能，这两个已像选中一个复选框一样简单 ！ 当用户进行排序或数据进行分页时，则展开类似的工作流：

1. 回发时，才会
2. 数据 Web 控件 s 预级别触发事件 (`PageIndexChanging`或`Sorting`)
3. 所有数据将重新检索对象数据源
4. 数据 Web 控件 s 后级别触发事件 (`PageIndexChanged`或`Sorted`)

尽管实现基本的分页和排序非常简单，以利用更有效的自定义分页或进一步增强分页或排序接口必须施加更多的工作。 将来的教程将探讨这些主题。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [下一篇](efficiently-paging-through-large-amounts-of-data-cs.md)
