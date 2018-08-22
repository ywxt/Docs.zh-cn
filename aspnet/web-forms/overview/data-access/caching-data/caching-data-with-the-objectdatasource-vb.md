---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: 使用 ObjectDataSource (VB) 缓存数据 |Microsoft Docs
author: rick-anderson
description: 缓存可能意味着速度较慢和快速的 Web 应用程序之间的差异。 本教程是第一种四个需要在 ASP.NET 中缓存的详细的信息...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: baa6fd0c290c0b09cf137f12ce62f50bae52be23
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825806"
---
<a name="caching-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource (VB) 缓存数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe)或[下载 PDF](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> 缓存可能意味着速度较慢和快速的 Web 应用程序之间的差异。 本教程的是第一四个需要在 ASP.NET 中缓存的详细的信息。 了解缓存的关键概念以及如何将应用到通过 ObjectDataSource 控件表示层缓存。


## <a name="introduction"></a>介绍

在计算机科学中，*缓存*是获取数据或获取成本较高的信息并将它的副本存储在速度更快访问的位置的过程。 对于数据驱动的应用程序，大型和复杂的查询通常占用大多数应用程序的执行时间。 此类应用程序 s 改进的性能，然后，通常是通过在应用程序的内存中存储的成本高昂的数据库查询的结果。

ASP.NET 2.0 提供了各种各样的缓存选项。 可以通过缓存的整个 web 页或用户控件呈现的 s 标记*输出缓存*。 ObjectDataSource 和 SqlDataSource 控件提供缓存功能，从而允许数据缓存在控制级别。 和 ASP.NET s*数据缓存*提供了丰富的缓存 API，使页面开发人员能够以编程方式缓存对象。 在本教程，我们将探讨使用 ObjectDataSource s 的下一步三种缓存功能，以及数据缓存。 我们还将探讨如何缓存应用程序范围内的数据，在启动时以及如何使缓存的数据保持最新通过使用 SQL 缓存依赖项。 这些教程不探索输出缓存。 在输出缓存的详细信息，请参阅[在 ASP.NET 2.0 中输出缓存](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)。

缓存可在任意位置在体系结构中，从数据访问层会通过应用表示层。 在本教程中我们将介绍将应用到通过 ObjectDataSource 控件表示层缓存。 在下一教程将探讨如何使用缓存数据的业务逻辑层。

## <a name="key-caching-concepts"></a>密钥缓存概念

缓存可以极大地提高应用程序 s 整体性能和可伸缩性的生成开销很大的数据并将它的副本存储在可以更有效地访问的位置。 由于缓存包含只是实际的基础数据的副本，它会过期，或*过时*，如果基础数据发生更改。 若要应对这种情况，页面开发人员可以指示来缓存项的条件*逐出*从缓存中，使用：

- **基于时间的条件**可能会将该项添加到缓存中用于绝对或可调持续时间。 例如，页面开发人员可能指示持续时间为说，60 秒。 使用绝对的持续时间，缓存的项将被逐出 60 秒后已添加到缓存，而不考虑访问的频率。 使用滑动的持续时间，缓存的项将被逐出的上次访问后 60 秒。
- **基于依赖关系的条件**依赖关系将项添加到缓存时与相关联。 S 项依赖项发生更改时它是从缓存中逐出。 依赖项可能是文件、 另一个缓存项或两者的组合。 ASP.NET 2.0 还允许 SQL 缓存依赖关系，使开发人员可以将项添加到缓存并将其逐出基础数据库数据发生更改时。 我们将检查 SQL 缓存依赖项中即将推出[使用 SQL 缓存依赖项](using-sql-cache-dependencies-vb.md)教程。

缓存中的项可能是指定的逐出条件，无论*清理*之前满足基于时间的或基于依赖关系的条件。 如果缓存已达到其容量，可以添加新的之前必须删除现有项。 因此，以编程方式使用缓存数据时它 s 重要，您始终假定的缓存的数据可能不会显示。 我们将介绍用于访问数据时从缓存以编程方式在我们的下一教程中的模式*体系结构中缓存数据*。

缓存提供了一种经济实惠的方法榨出更多来自应用程序的性能。 作为[Steven Smith](http://aspadvice.com/blogs/ssmith/)在他的文章来阐述[ASP.NET 缓存： 技术和最佳实践](https://msdn.microsoft.com/library/aa478965.aspx):

缓存可以获得很好足够的性能而无需大量时间和分析的好方法。 内存是比较便宜，因此可以获得所需的输出缓存 30 秒，而无需花费一天或每周尝试优化您的代码或数据库的性能，如果执行的缓存解决方案 （假定为第二个旧-30 数据是确定），然后继续。 最终，不好的设计将可能同步，因此，应尝试在课程的正确设计应用程序。 但如果您只需获得良好今天的足够性能，缓存可能是一个极好 [方法]，购买你有时间重构你的应用程序在更高版本的日期后的时间来执行此操作。

虽然缓存可提供明显的性能增强功能，它不是适用于所有情况，如使用经常更新的实时数据，或甚至很快长期存在过时的数据是不可接受的应用程序。 但对于大多数应用程序时，应使用缓存。 有关更多背景信息缓存在 ASP.NET 2.0 中，请参阅[缓存以提高性能](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx)一部分[ASP.NET 2.0 快速入门教程](https://quickstarts.asp.net/QuickStartv20/aspnet/)。

## <a name="step-1-creating-the-caching-web-pages"></a>步骤 1： 创建缓存的 Web 页

我们开始我们的探索的 ObjectDataSource s 缓存功能之前，让 s 先花点时间在我们的网站项目，我们需要为本教程中下, 一步 3 中创建 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`Caching`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`


![将 ASP.NET 页面添加与缓存相关的教程](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**图 1**： 将 ASP.NET 页面添加与缓存相关的教程


在其他文件夹中，喜欢`Default.aspx`在`Caching`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![图 2： 将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**图 2**： 图 2： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image4.png))


最后，将这些页面添加到条目为`Web.sitemap`文件。 具体而言，在处理二进制数据后添加以下标记`<siteMapNode>`:


[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在为缓存教程包括的项。


![站点图现在包括项的缓存的教程](caching-data-with-the-objectdatasource-vb/_static/image5.png)

**图 3**： 站点图现在包括项的缓存的教程


## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>步骤 2： 在 Web 页中显示产品的列表

本教程探讨了如何使用 ObjectDataSource 控件 s 内置缓存功能。 我们可以看看这些功能之前，不过，我们首先需要页后，可以从工作。 允许 s 创建使用 GridView 从 ObjectDataSource 来检索列出产品信息的网页`ProductsBLL`类。

首先打开`ObjectDataSource.aspx`页中`Caching`文件夹。 从工具箱拖到设计器中拖动一个 GridView，设置其`ID`属性设置为`Products`，并从其智能标记上，选择要绑定到名为的新 ObjectDataSource 控件`ProductsDataSource`。 配置对象数据源以使用`ProductsBLL`类。


[![配置对象数据源以使用 ProductsBLL 类](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**图 4**： 配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image8.png))


有关此页上，让我们来创建可编辑的 GridView，以便我们可以检查在 ObjectDataSource 中缓存数据修改通过 GridView 的接口时，会发生什么情况。 将下拉列表保留在设置为其默认情况下，选择选项卡`GetProducts()`，但更改到更新选项卡中的选定的项`UpdateProduct`重载接受`productName`， `unitPrice`，和`productID`作为其输入参数。


[![将更新选项卡的下拉列表设置为适当的 UpdateProduct 重载](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**图 5**： 设置为适用的更新选项卡的下拉列表`UpdateProduct`重载 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image11.png))


最后，将下拉列表设置为 （无） 插入和删除选项卡中，单击完成。 Visual Studio 将在完成配置数据源向导，请设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`。 如中所述[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程中，此属性需要从声明性语法中删除或重新设置其默认值为`{0}`，以便为我们更新工作流无错误继续执行。

此外，在向导完成 Visual Studio 将字段添加到 GridView 每个产品的数据字段。 删除所有除`ProductName`， `CategoryName`，和`UnitPrice`BoundFields。 接下来，更新`HeaderText`的每个产品、 类别和价格，到这些 BoundFields 属性分别。 由于`ProductName`字段是必填，BoundField 转换为 TemplateField 并添加到一个 RequiredFieldValidator `EditItemTemplate`。 同样，将转换`UnitPrice`转换为 TemplateField BoundField 和添加 CompareValidator 以确保用户输入的值是有效的货币值的 s 大于或等于零。 除了这些修改内容，可随意执行任何美观的更改，如右对齐`UnitPrice`值，或指定的格式设置`UnitPrice`其只读和编辑接口中的文本。

使 GridView GridView s 智能标记中的启用编辑复选框可编辑。 此外选中启用分页和启用排序复选框。

> [!NOTE]
> 需要如何自定义 GridView s 编辑界面的评审？ 如果是这样，回头[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程。


[![用于编辑、 排序和分页启用 GridView 支持](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**图 6**： 启用对编辑，排序和分页的 GridView 支持 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image14.png))


以后进行这些 GridView 修改，GridView 和 ObjectDataSource s 声明性标记看起来应类似于下面：


[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

如图 7 所示，可编辑的 GridView 列出名称、 类别和每个数据库中产品的价格。 请花费片刻时间测试页的功能排序结果页，查看和编辑记录。


[![可排序、 Pageable、 可编辑的 GridView 中列出每个产品名称、 类别和价格](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**图 7**： 可排序、 Pageable、 可编辑的 GridView 中列出每个产品的名称、 类别和价格 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image17.png))


## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>步骤 3： 检查时 ObjectDataSource 是请求数据

`Products` GridView 中检索其数据以显示通过调用`Select`方法的`ProductsDataSource`对象数据源。 此对象数据源创建的业务逻辑层的实例`ProductsBLL`类并调用其`GetProducts()`方法，后者又调用数据访问层 s `ProductsTableAdapter` s`GetProducts()`方法。 DAL 方法连接到 Northwind 数据库，并发出的已配置`SELECT`查询。 此数据然后返回到 DAL，它打包在`NorthwindDataTable`。 DataTable 对象返回到的 BLL，将其返回给对象数据源，将其返回到 GridView。 然后创建 GridView`GridViewRow`为每个对象`DataRow`DataTable 中和每个`GridViewRow`最终呈现的 HTML，返回到客户端和访问者 s 浏览器上显示。

GridView 需要绑定到其基础数据的每个时出现以下事件序列。 当首次访问页面，当在一个数据页之间移动，排序 GridView 中，或修改通过其内置编辑或删除接口的 GridView 的数据时，将发生这种情况。 如果禁用 GridView 的视图状态，则将在每个回发时也重新绑定 GridView。 GridView 可以还显式重新绑定到其数据通过调用其`DataBind()`方法。

若要完全认识与从数据库检索的数据的频率，让我们来显示一条消息，指示重新检索数据时。 添加名为 GridView 上方的一个标签 Web 控件`ODSEvents`。 清除其`Text`属性并设置其`EnableViewState`属性设置为`False`。 下方是标签，添加一个按钮 Web 控件，并设置其`Text`属性设置为回发。


[![将一个标签和按钮添加到页面上方 GridView](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**图 8**： 向的 GridView 页面上方添加一个标签和按钮 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image20.png))


在数据访问工作流使用 ObjectDataSource 的`Selecting`之前创建的基础对象的事件触发和调用其配置的方法。 创建此事件的事件处理程序并添加以下代码：


[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

ObjectDataSource 发出请求时，数据体系结构每次该标签将显示文本选择事件触发。

请访问此页在浏览器中。 当首次访问页面时，会显示文本选择事件触发。 单击回发的按钮并记下该文本将消失 (假设 GridView s`EnableViewState`属性设置为`True`，默认值)。 这是因为，在回发时，从其视图状态重建 GridView 并不因此求助于其数据的对象数据源。 排序、 分页，或编辑数据，但是，导致 GridView 重新绑定到其数据源，并因此触发文本随即再次显示选择事件。


[![每当 GridView 重新绑定到其数据源，显示触发选择事件](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**图 9**： 每当的 GridView 重新绑定到其数据源时，将显示选择事件触发 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image23.png))


[![单击回发按钮会导致要从其视图状态重新构造 GridView](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**图 10**： 单击该回发的按钮使 GridView，若要从其视图状态重新构造 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image26.png))


这可能看起来比较浪费，每次通过分页或排序的数据检索的数据库数据。 毕竟，我们重新使用默认的分页，因为 ObjectDataSource 已检索的所有记录时显示的第一页。 即使 GridView 不提供排序和分页支持，首次访问页面时的任何用户 （以及每次回发，如果禁用视图状态） 每次必须检索的数据从数据库。 但如果 GridView 显示相同的数据对所有用户，这些额外的数据库请求是多余的。 为什么不缓存从返回的结果`GetProducts()`方法和绑定到 GridView 缓存结果？

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>步骤 4： 缓存数据使用 ObjectDataSource

通过只需设置几个属性，可以配置 ObjectDataSource 来自动缓存其 ASP.NET 数据缓存中检索到的数据。 以下列表总结了 ObjectDataSource 的与缓存相关的属性：

- [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx)必须设置为`True`若要启用缓存。 默认值为 `False`。
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx)的时间，以秒为单位，缓存数据。 默认值为 0。 ObjectDataSource 仅缓存数据，如果`EnableCaching`是`True`和`CacheDuration`设置为值大于零。
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx)可以设置为`Absolute`或`Sliding`。 如果`Absolute`，ObjectDataSource 缓存为其检索到的数据`CacheDuration`秒; 如果`Sliding`，才不访问的数据会过期`CacheDuration`秒。 默认值为 `Absolute`。
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx)使用此属性与现有的缓存依赖项相关联的 ObjectDataSource 的缓存条目。 ObjectDataSource 的数据条目可以被过早地逐出缓存中过期及其关联`CacheKeyDependency`。 此属性通常用于将 SQL 缓存依赖项与 ObjectDataSource 的缓存相关联，本主题将探讨在将来[使用 SQL 缓存依赖项](using-sql-cache-dependencies-vb.md)教程。

让我们来配置`ProductsDataSource`ObjectDataSource 30 秒内对绝对刻度缓存其数据。 设置 ObjectDataSource s`EnableCaching`属性设置为`True`并将其`CacheDuration`属性设置为 30。 将保留`CacheExpirationPolicy`属性设置为其默认值， `Absolute`。


[![配置对象数据源在 30 秒内缓存其数据](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**图 11**： 配置 ObjectDataSource 30 秒内缓存其数据 ([单击以查看实际尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image29.png))


保存所做的更改并重新访问此页在浏览器中。 选择触发事件文本将显示当您首次访问页上，为最初的数据不在缓存中。 而是指后续回发触发单击回发的按钮，排序、 分页，或单击编辑或取消按钮*不*起选择事件触发的文本。 这是因为`Selecting`ObjectDataSource 从其基础对象; 获取其数据时，仅会触发事件`Selecting`事件不会引发，如果从数据缓存中提取数据。

30 秒后，将从缓存逐出数据。 此外会从缓存逐出数据 ObjectDataSource s `Insert`， `Update`，或`Delete`调用方法。 因此，过了 30 秒或已单击了更新按钮，排序、 分页，或单击编辑或取消按钮将导致 ObjectDataSource 后，若要从其基础对象中获取其数据后，显示选择事件触发文本时`Selecting`事件触发。 这些返回的结果放置到的数据缓存。

> [!NOTE]
> 如果你经常看到选择触发事件文本，即使预期对象数据源以使用缓存的数据，可能会由于内存限制。 如果没有足够的可用内存，可能会清理通过对象数据源添加到缓存的数据。 如果对象数据源不是 t 似乎正确缓存的数据或仅缓存数据将个别情况下，关闭一些应用程序以释放内存，然后重试。


图 12 显示了缓存的工作流使用 ObjectDataSource s。 选择事件激发时文本显示在屏幕上，这是因为数据不是在缓存中而不得不从基础对象中检索。 如果缺少此文本，但是，它 s 由于从缓存数据可用。 当从缓存返回的数据那里 s 对基础对象的任何调用，因此，没有数据库查询执行。


![对象数据源存储和检索其数据从数据缓存](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**图 12**: ObjectDataSource 存储并检索其数据从数据缓存


每个 ASP.NET 应用程序具有其自己的数据缓存实例在所有页和访问者之间共享该 s。 这意味着访问页面的所有用户同样共享数据缓存中存储的对象数据源的数据。 若要验证这一点，请打开`ObjectDataSource.aspx`页在浏览器中。 当首次访问的页面，选择触发事件文本将显示 （假定由以前的测试添加到缓存的数据，到目前为止，已被逐出）。 打开第二个浏览器实例并复制并粘贴到第二个中的第一个浏览器实例的 URL。 在第二个浏览器实例中，选择触发事件文本没有显示，因为它使用相同的缓存数据与第一个。

对象数据源在检索到的数据插入到缓存时，使用包含的缓存密钥值：`CacheDuration`和`CacheExpirationPolicy`属性值; 正由对象数据源，指定基础业务对象的类型通过[`TypeName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx)(`ProductsBLL`，在此示例中); 的值`SelectMethod`属性的名称和值中的参数的`SelectParameters`集合; 和值的其`StartRowIndex`并`MaximumRows`属性，在实现时使用[自定义分页](../paging-and-sorting/paging-and-sorting-report-data-vb.md)。

在这些值更改时，为这些属性的组合创建的缓存密钥值可确保唯一缓存项。 例如，在过去的教程中我们已介绍了使用`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`，这会返回为指定类别的所有产品。 一个用户可能会进入页并查看饮料，其中包含`CategoryID`为 1。 如果 ObjectDataSource 缓存而不考虑其结果`SelectParameters`值，当另一个用户到页以查看调味品饮料产品时已在缓存中，d 他们将看到缓存的饮料产品而非调味品。 通过不同的缓存键的两个属性，其中包括的值`SelectParameters`，ObjectDataSource 维护 beverages 和调味品的单独的缓存项。

## <a name="stale-data-concerns"></a>过时的数据问题

ObjectDataSource 自动逐出缓存时的任何一个从其项及其`Insert`， `Update`，或`Delete`调用的方法。 这有助于防止时完成的页修改的数据清除的缓存项过时的数据。 但是，它有可能使用缓存仍显示过时的数据对象数据源。 在最简单的情况下，它可能是由于直接在数据库中更改的数据。 可能是数据库管理员只需运行修改的某些数据库中记录的脚本。

这种情况下还可以展开以更巧妙的方法。 虽然 ObjectDataSource 逐出其项从缓存某一数据修改方法调用时，删除缓存的项是 ObjectDataSource s 特定组合的属性值 (`CacheDuration`， `TypeName`， `SelectMethod`，等等）。 如果必须使用不同的两个 Objectdatasource`SelectMethods`或`SelectParameters`，但仍可以进行更新相同的数据，则一个 ObjectDataSource 可能更新的行，并使其自己的缓存项，但相应的行的第二个对象数据源无效仍将处理来自缓存。 建议您创建页以进行展示此功能。 创建一个显示从 ObjectDataSource 使用缓存和配置从中获取数据提取其数据可编辑 GridView 页面`ProductsBLL`类的`GetProducts()`方法。 添加另一个可编辑的 GridView 和 ObjectDataSource 到此页 （或另一个），但对于此第二个对象数据源将使用其`GetProductsByCategoryID(categoryID)`方法。 由于两个 Objectdatasource`SelectMethod`属性不同，它们将每个具有其自己的缓存的值。 如果您编辑在一个网格中，产品下一次将数据返回到其他网格绑定 （由分页、 排序和等），它将仍为旧的缓存数据提供服务并不会反映在其他网格中所做更改。

如果您愿意将有可能过时的数据，并对方案使用较短的满数据的新鲜度是重要简单地说，只能使用基于时间的满。 如果过时的数据不是可接受的则会放弃缓存或使用 SQL 缓存依赖项 (假定它数据库数据则重新缓存)。 在将来的教程中，我们将探讨 SQL 缓存依赖项。

## <a name="summary"></a>总结

在本教程中，我们探讨 ObjectDataSource s 内置缓存功能。 我们可以通过只需设置几个属性，指示 ObjectDataSource 缓存返回从指定的结果`SelectMethod`到 ASP.NET 数据缓存。 `CacheDuration`和`CacheExpirationPolicy`属性指示缓存项的持续时间以及它是否是绝对或可调过期。 `CacheKeyDependency`属性将与现有的缓存依赖项关联的所有对象数据源的缓存条目。 这可以用于基于时间的过期为止，并通常与 SQL 缓存依赖项一起使用之前逐出缓存中的 ObjectDataSource 的项。

由于 ObjectDataSource 只是缓存的数据缓存到其值，我们可以以编程方式将复制的 ObjectDataSource s 内置功能。 它不适合执行此操作在表示层，因为 ObjectDataSource 提供默认情况下，此功能，但我们可以在一个单独的体系结构层中实现缓存功能。 为此，我们将需要重复使用 ObjectDataSource 的相同逻辑。 我们将探讨如何以编程方式使用的数据缓存从体系结构中，在我们下一步的教程。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 缓存： 技术和最佳实践](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework 应用程序的缓存体系结构指南](https://msdn.microsoft.com/library/ee817645.aspx)
- [在 ASP.NET 2.0 中的输出缓存](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-sql-cache-dependencies-cs.md)
> [下一页](caching-data-in-the-architecture-vb.md)
