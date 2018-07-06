---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: 与母版页 (VB) 从内容页交互 |Microsoft Docs
author: rick-anderson
description: 探讨如何调用方法，从母版页中的代码中设置属性等的内容页。
ms.author: aspnetcontent
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 41cfd5e65fbe0a5ef4930ce3a4c84556cedcdfd6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807643"
---
<a name="interacting-with-the-content-page-from-the-master-page-vb"></a>与母版页 (VB) 从内容页交互
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip)或[下载 PDF](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> 探讨如何调用方法，从母版页中的代码中设置属性等的内容页。


## <a name="introduction"></a>介绍

前面的教程介绍了如何有内容页以编程方式与其主页面进行交互。 回想一下，我们更新母版页包含列出五个最近的 GridView 控件添加产品。 然后，我们创建的内容页面，用户可以从中添加一个新的产品。 后添加一个新的产品，需要指示主页面刷新其 GridView，以便它包含刚添加产品内容页。 此功能已通过将一个公共方法添加到母版页，刷新数据绑定到 GridView，然后再调用该方法从内容页。

最常见的内容和母版页交互形式源自内容页。 但是，很可能要实现价值，rouse 维护当前内容页面的母版页并且可能需要此类功能，如果主页面包含用户界面元素，使用户能够修改数据也会显示在内容页。 请考虑内容页显示 GridView 中的产品信息控件和母版页包含一个按钮控件，单击时，所有产品将价格乘 2。 类似于前面的教程中的示例，GridView 需要刷新，以便它将显示新的价格中，单击按钮的双精度价格后但在此方案需要为操作 rouse 维护内容页面的母版页。

本教程探讨了如何通过母版页调用内容页中定义的功能。

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>决定通过事件和事件处理程序的编程交互

调用从母版页的内容页面功能是比前者更具挑战性。 内容页时决定以编程方式从内容页交互具有单一的主页面，因为我们知道什么公共方法和属性可供我们使用。 但是，主页面，可以具有不同内容页的数量，每个都有自己的属性和方法集。 如何，然后，编写代码时我们不知道哪些内容页将调用直到运行时在其内容页面中执行某些操作的母版页中？

请考虑一个 ASP.NET Web 控件，例如按钮控件。 按钮控件可以显示在任意数量的 ASP.NET 页面上，并需要依据它会发出警告页已被单击的机制。 这通过*事件*。 具体而言，按钮控件引发其`Click`事件时单击; 包含按钮的 ASP.NET 页面 （可选） 可以响应通过该通知*事件处理程序*。

此相同的模式可用于在其内容页面中有母版页触发器功能：

1. 将事件添加到母版页。
2. 引发事件时主页面需要其内容页与进行通信。 例如，如果主页面需要提醒用户加倍价格其内容页面，其事件将后立即引发价格已增加一倍。
3. 在需要执行一些操作这些内容页面中创建一个事件处理程序。

本教程的余下内容实现引入; 中所述的示例也就是说，列出数据库中的产品的内容页和母版页包含一个按钮控制翻倍，价格。

## <a name="step-1-displaying-products-in-a-content-page"></a>步骤 1： 在内容页面中显示的产品

我们首要任务是创建内容页，其中列出了 Northwind 数据库中的产品。 (我们 Northwind 数据库到项目中添加前面的教程[*与母版页从内容页交互*](interacting-with-the-master-page-from-the-content-page-vb.md)。)首先，通过添加新的 ASP.NET 页面到`~/Admin`名为的文件夹`Products.aspx`，确保将将其绑定到`Site.master`母版页。 图 1 显示此页添加到网站后的解决方案资源管理器。


[![向管理员文件夹添加新的 ASP.NET 页面](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**图 01**： 添加到新的 ASP.NET 页`Admin`文件夹 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png))


回想一下，在[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)教程中，我们创建一个名为的自定义基本页类`BasePage`，如果它不生成页面的标题显式设置。 转到`Products.aspx`页面的代码隐藏类，并将其派生`BasePage`(而不是从`System.Web.UI.Page`)。

最后，更新`Web.sitemap`文件以便包括本课程中的一个条目。 添加以下标记下方`<siteMapNode>`Master 页交互的课程内容：


[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

此加法`<siteMapNode>`元素反映在课程列表 （请参阅图 5）。

返回到`Products.aspx`。 中的内容控件`MainContent`中，添加 GridView 控件并将其命名`ProductsGrid`。 将 GridView 绑定到名为的新 SqlDataSource 控件`ProductsDataSource`。


[![将 GridView 绑定到新的 SqlDataSource 控件](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**图 02**： 将 GridView 绑定到新的 SqlDataSource 控件 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png))


将向导配置，使其使用 Northwind 数据库。 如果您已完成上一教程中，则应该已拥有一个名为的连接字符串`NorthwindConnectionString`在`Web.config`。 从下拉列表中，选择此连接字符串，如图 3 中所示。


[![配置 SqlDataSource 使用 Northwind 数据库](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**图 03**： 配置 SqlDataSource 使用 Northwind 数据库 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png))


接下来，指定数据源控件`SELECT`通过从下拉列表中选择产品表并返回语句`ProductName`和`UnitPrice`（请参阅图 4） 的列。 单击下一步并在完成以完成配置数据源向导。


[![返回产品表中的产品名称和单价字段](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**图 04**： 返回`ProductName`并`UnitPrice`字段从`Products`表 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png))


这就是一切就这么简单 ！ 完成向导后 Visual Studio 将两个 BoundFields 添加到 GridView 镜像 SqlDataSource 控件返回的两个字段。 遵循 GridView 和 SqlDataSource 控件的标记。 图 5 显示了通过浏览器查看时的结果。


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]


[![GridView 中列出每个产品和它的价格](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**图 05**： 每个产品和它的价格 GridView 中列出 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png))


> [!NOTE]
> 随意清理的 GridView 的外观。 某些建议包括格式化为货币的显示的单价值以及如何使用背景颜色和字体以改善该网格的外观。 有关显示和格式设置在 ASP.NET 中的数据的详细信息，请参阅我[使用数据的系列教程](../../data-access/index.md)。


## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>步骤 2： 将一个双精度价格按钮添加到母版页

我们的下一个任务是要添加到主按钮 Web 控件页上，单击时，将双精度的数据库中的所有产品的价格。 打开`Site.master`母版页和将一个按钮从工具箱拖到设计器中，将其下放置`RecentProductsDataSource`SqlDataSource 控件，我们添加了在上一教程。 设置按钮的`ID`属性设置为`DoublePrice`并将其`Text`属性设置为"双产品价格"。

接下来，将使用 SqlDataSource 控件添加到主页上，其命名为`DoublePricesDataSource`。 此 SqlDataSource 将用于执行`UPDATE`语句翻倍，所有价格。 具体而言，我们需要设置其`ConnectionString`并`UpdateCommand`属性设置为适当的连接字符串和`UPDATE`语句。 然后我们需要调用此 SqlDataSource 控件`Update`方法时`DoublePrice`单击按钮。 若要设置`ConnectionString`和`UpdateCommand`属性中，选择 SqlDataSource 控件，然后转到属性窗口。 `ConnectionString`属性列出了已存储在这些连接字符串`Web.config`在下拉列表中; 选择`NorthwindConnectionString`选项如图 6 中所示。


[![配置为使用 NorthwindConnectionString SqlDataSource](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**图 06**： 配置为使用 SqlDataSource `NorthwindConnectionString` ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png))


若要设置`UpdateCommand`属性，在属性窗口中找到 UpdateQuery 选项。 此属性，请选中时，显示一个具有省略号; 的按钮单击此按钮将显示在图 7 所示的命令和参数编辑器对话框。 键入以下内容`UPDATE`到对话框的文本框中的语句：


[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

此语句中，执行时，将会翻倍`UnitPrice`值中的每条`Products`表。


[![设置 SqlDataSource 的 UpdateCommand 属性](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**图 07**： 设置 SqlDataSource`UpdateCommand`属性 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png))


以后设置这些属性，这些按钮和 SqlDataSource 控件的声明性标记看起来应类似于下面：


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

剩下的就是调用其`Update`方法时`DoublePrice`单击按钮。 创建`Click`事件处理程序`DoublePrice`按钮并添加以下代码：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

若要测试此功能，请访问`~/Admin/Products.aspx`页面，我们在步骤 1 中创建，并单击"双产品价格"按钮。 单击按钮会导致回发，并执行`DoublePrice`按钮的`Click`事件处理程序，使所有产品的价格。 然后重新呈现页面标记则返回并重新显示在浏览器中。 GridView 中内容页上，但是，列出了相同的价格"双产品价格"按钮被单击。 这是因为最初加载在 GridView 中的数据必须存储在视图状态，因此它不重新加载在回发除非规定，否则其状态。 如果访问不同的页面，然后返回到`~/Admin/Products.aspx`页上，将看到更新后的价格。

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>步骤 3： 引发事件时的价格将增加一倍

因为在 GridView`~/Admin/Products.aspx`页不会立即反映价格加倍，用户可以理解的是可能会认为它们未单击"双产品价格"按钮，否则它不起作用。 它们可以尝试单击按钮更多时间，反复地价格乘 2。 若要修复此，我们需要的内容中有在网格页的新价格后立即显示它们增加一倍。

在本教程前面所述，我们需要引发母版页中的事件，每当用户单击`DoublePrice`按钮。 事件是一个类 （事件发布者） 的方式通知另一组的一些有趣的事情发生了其他类 （事件订阅服务器）。 在此示例中，主页面是事件发布服务器。这些内容时要注意的页`DoublePrice`单击按钮是订阅服务器。

一个类，通过创建订阅的事件*事件处理程序*，这是在响应所引发的事件中执行的方法。 发布服务器上定义他通过定义引发的事件*事件委托*。 事件委托指定的事件处理程序必须接受的输入的参数。 在.NET Framework 中，事件委托执行不返回任何值，并接受两个输入的参数：

- `Object`，用于标识事件源和
- 派生自的类 `System.EventArgs`

第二个参数传递给事件处理程序可以包括有关事件的其他信息。 虽然基`EventArgs`类不传递任何信息、.NET Framework 包括大量的扩展的类`EventArgs`和包含其他属性。 例如，`CommandEventArgs`实例传递给事件处理程序响应`Command`事件，并包括两个信息性的属性：`CommandArgument`和`CommandName`。

> [!NOTE]
> 有关创建的详细信息，提高，和处理事件，请参阅[事件和委托](https://msdn.microsoft.com/library/17sde2xt.aspx)并[简单英语中的事件委托](http://www.codeproject.com/KB/cs/eventdelegates.aspx)。


若要定义一个事件，请使用以下语法：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

因为我们只需要用户单击时发出警报内容页`DoublePrice`按钮并不需要传递任何其他附加信息，我们可以使用事件委托`EventHandler`，用于定义的事件处理程序接受作为第二个操作数参数类型的对象`System.EventArgs`。 若要创建主页面中的事件，请到母版页的代码隐藏类添加以下代码行：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

上面的代码将公共事件添加到名为母版页`PricesDoubled`。 现在，我们需要引发此事件后的价格已增加一倍。 若要引发事件，请使用以下语法：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

其中*发件人*并*eventArgs*是你想要传递到订阅服务器的事件处理程序的值。

更新`DoublePrice``Click`事件处理程序使用以下代码：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

与前面一样，`Click`事件处理程序通过调用来启动`DoublePricesDataSource`SqlDataSource 控件`Update`方法翻倍的所有产品的价格。 以下有两个添加到事件处理程序。 首先， `RecentProducts` GridView 的数据刷新。 此 GridView 已添加到母版页中前面的教程，并显示最近添加的五种产品。 我们需要刷新该网格，使之显示这些五种产品的只是双写价格。 之后，`PricesDoubled`引发事件。 对主页面本身的引用 (`Me`) 作为事件源和一个空发送到事件处理程序`EventArgs`作为事件参数发送对象。

## <a name="step-4-handling-the-event-in-the-content-page"></a>步骤 4： 处理的内容页中的事件

主页面现在引发其`PricesDoubled`事件时`DoublePrice`单击按钮控件。 但是，这是只完成了一半任务-我们仍需处理订阅服务器中的事件。 这涉及到两个步骤： 创建事件处理程序并添加事件绑定代码，以便当引发事件时执行的事件处理程序。

首先，创建名为一个事件处理程序`Master_PricesDoubled`。 由于我们是如何定义`PricesDoubled`母版页中的事件的事件处理程序的两个输入的参数必须是类型`Object`和`EventArgs`分别。 在事件处理程序调用`ProductsGrid`GridView 的`DataBind`方法重新绑定到网格的数据。


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

事件处理程序的代码已完成，但我们尚未为关联母版页的`PricesDoubled`到此事件处理程序的事件。 订阅服务器上将事件与事件处理程序通过以下语法：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

*发布服务器*是对提供事件的对象的引用*eventName*，和*methodName*是在订阅服务器中定义的事件处理程序的名称。

此事件绑定代码必须执行的第一次页面访问和后续回发，而应出现在之前可能会引发该事件时的页面生命周期中的点。 添加事件绑定代码的好时机是在 PreInit 阶段中，很早在页面生命周期中出现这种情况。

打开`~/Admin/Products.aspx`并创建`Page_PreInit`事件处理程序：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

若要完成此绑定代码，我们需要对主页面从内容页的以编程方式引用。 上一教程中所述，有两种方法来执行此操作：

- 通过强制转换松散类型`Page.Master`属性设置为适当的母版页类型，或
- 通过添加`@MasterType`指令`.aspx`页，然后使用强类型`Master`属性。

让我们使用后一种方法。 以下代码添加到`@MasterType`指令的声明性标记中页面的顶部：


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

然后添加以下事件绑定代码在`Page_PreInit`事件处理程序：


[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

在内容页中的 GridView 刷新使用此代码，只要`DoublePrice`单击按钮。

图 8 和 9 说明了此行为。 图 8 显示了页面在首次访问时。 请注意，在这种价格值`RecentProducts`（在主页面的左侧列） 的 GridView 和`ProductsGrid`GridView （在内容页）。 图 9 显示了相同屏幕后立即`DoublePrice`单击按钮。 正如您所看到的新价格会立即反映在这两个 Gridview。


[![初始的价格值](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**图 08**: 初始的价格值 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png))


[![在 Gridview 中显示 Just-Doubled 价格](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**图 09**： 在 Gridview 中显示 The Just-Doubled 价格 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png))


## <a name="summary"></a>总结

理想情况下，主页面和其内容的页面是从另一个完全独立，不需要交互的任何级别。 但是，如果你有主页面或内容页面，其中显示可以从主页或内容页面修改的数据，然后您可能需要具有母版页内容页 （或进行相反的转换） 发出警报，以便可以更新显示的数据修改时。 在前面的教程中我们已了解如何以编程方式与其主页面; 进行交互的内容页面在本教程中我们介绍了如何通过母版页启动交互。

虽然编程交互内容和母版页之间可以源自的内容或母版页，所使用的交互模式取决于资助创始费。 差异是由于访问的内容页面含有单个主页面，但主页面可能有许多不同的内容页面。 而不是让母版页与内容页直接交互，更好的方法将引发一个事件来指示某项操作已发生的母版页。 有关操作处理这些内容页可以创建事件处理程序。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问和更新在 ASP.NET 中的数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [事件和委托](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [内容和母版页之间传递信息](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [在 ASP.NET 教程中使用的数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Suchi Banerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](interacting-with-the-master-page-from-the-content-page-vb.md)
> [下一页](master-pages-and-asp-net-ajax-vb.md)
