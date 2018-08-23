---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
title: 与母版页从内容页 (C#) 进行交互 |Microsoft Docs
author: rick-anderson
description: 探讨如何调用方法，从内容页中的代码中设置属性的母版页等。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 32d54638-71b2-491d-81f4-f7417a13a62f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
msc.type: authoredcontent
ms.openlocfilehash: afcec6cb7a6763d068301c7afdd28ff560a3065b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833271"
---
<a name="interacting-with-the-master-page-from-the-content-page-c"></a>与母版页从内容页 (C#) 进行交互
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_CS.zip)或[下载 PDF](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_CS.pdf)

> 探讨如何调用方法，从内容页中的代码中设置属性的母版页等。


## <a name="introduction"></a>介绍

在过去的过去的五个教程已介绍了如何创建主页面、 定义内容区域中，将 ASP.NET 页面绑定到母版页，和定义特定于页面的内容。 当访问者请求特定的内容页面时，内容和母版页的标记融合在运行时，从而导致统一的控件层次结构的呈现。 因此，我们已经看到了一种方式的主页面，其内容页面的另一个可以进行交互： 拼写 transfuse 到母版页的 ContentPlaceHolder 控件的标记为内容页。

什么我们必须尚未检查是如何以编程方式交互的母版页和内容页。 除了定义母版页的 ContentPlaceHolder 控件的标记，内容页可以将值分配到其主页面的公共属性和调用它的公共方法。 同样，母版页可能会使用其内容页交互。 其声明性标记之间的交互比不太常见编程之间母版页和内容页交互时，有很多情况下需要此类编程交互的位置。

在本教程中我们介绍如何内容页面能以编程方式交互与其母版页;在下一教程将探讨如何母版页同样能与及其内容页交互。

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>之间的内容页和其母版页编程交互的示例

当一个页面的特定区域需要按页根据配置时，我们使用 ContentPlaceHolder 控件。 但是情况下，大多数页需要发出特定输出，但少量的页面需要自定义，以便显示其他内容呢？ 此类一个中，我们探讨的示例[*多个 Contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-cs.md)教程中，涉及到每个页面上显示登录界面。 虽然大多数页面应包含登录界面，它要抑制的少量的页面，如： 主登录页 (`Login.aspx`); 在创建帐户页和只是经过身份验证的用户可以访问其他页面。 [*多个 Contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-cs.md)教程介绍了如何为 ContentPlaceHolder 母版页中定义的默认内容和如何在这些重写该页面的位置不需要默认的内容。

另一种方法是创建的公共属性或母版页，该值指示是否显示或隐藏登录界面中的方法。 例如，主页面可能包含名为的公共属性`ShowLoginUI`其值用于设置`Visible`母版页中的登录名控件的属性。 然后可以以编程方式设置这些内容页面应取消显示登录用户界面`ShowLoginUI`属性设置为`false`。

可能的数据显示在母版页需要某种操作已经在内容页中产生后刷新时发生内容与母版页交互的最常见的例子。 请考虑包括一个 GridView，显示 5 个最新的主页面从特定数据库表中添加记录和其内容页面的一个包含用于将新记录添加到同一个表的接口。

当用户访问页后，可以添加新记录时，她会看到的五个最近添加的记录显示在母版页。 在填写新记录的列的值，她将提交窗体。 假设在母版页中的这个 GridView 有其`EnableViewState`属性设置为 true （默认值），从视图状态重新加载其内容，并且即使只是较新记录添加到数据库，因此，显示 5 个同一个记录。 这可能会使用户感到困惑。

> [!NOTE]
> 即使禁用 GridView 的视图状态到在每个回发时其基础数据源重新绑定，它仍不会显示刚添加的记录因为数据绑定到 GridView 前面的页面生命周期比新记录添加到数据库时ase。


若要解决此问题，以便刚添加的记录显示在母版页中的 GridView 在回发时我们需要指示 GridView 重新绑定到其数据源*后*新记录已添加到数据库。 这需要的内容和主页面之间的交互，因为用于添加新记录 （和其事件处理程序） 都在内容页，但需要刷新 GridView 接口是在母版页中。

由于刷新从内容页中的事件处理程序的主页面的显示是一个对内容和母版页交互最常见的需求，我们来探讨本主题中更多详细信息。 本教程中下载内容还包括名为的 Microsoft SQL Server 2005 Express Edition 数据库`NORTHWIND.MDF`在网站的`App_Data`文件夹。 Northwind 数据库存储产品、 员工和针对虚构公司，Northwind Traders 的销售信息。

步骤 1 演练显示的五个最近在母版页中的 GridView 中添加产品。 步骤 2 创建一个内容页面中添加新的产品。 步骤 3 介绍如何创建主页面中的公共属性和方法和步骤 4 说明了如何以编程方式与这些属性和方法从内容页交互。

> [!NOTE]
> 本教程不会不深入探讨在 ASP.NET 中使用数据的具体情况。 设置主页面以显示数据和插入数据的内容页的步骤是完整的尚未轻松。 显示和插入数据以及使用 SqlDataSource 和 GridView 控件的更深入信息，请在本教程末尾查阅中进一步读数部分资源。


## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>步骤 1： 最近显示五个母版页中添加产品

打开`Site.master`母版页并添加一个标签和 GridView 控件与`leftContent` `<div>`。 清除的标签`Text`属性，则设置其`EnableViewState`属性设置为 false，并将其`ID`属性设置为`GridMessage`; 设置 GridView`ID`属性设置为`RecentProducts`。 接下来，从设计器中，展开 GridView 的智能标记，并选择将其绑定到新的数据源。 这将启动数据源配置向导。 因为 Northwind 数据库中`App_Data`文件夹是 Microsoft SQL Server 数据库中，选择通过选择 （见图 1） 创建 SqlDataSource; 名称 SqlDataSource `RecentProductsDataSource`。


[![将 GridView 绑定到名为 RecentProductsDataSource SqlDataSource 控件](interacting-with-the-master-page-from-the-content-page-cs/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image1.png)

**图 01**： 将 GridView 绑定到 SqlDataSource 控件命名为`RecentProductsDataSource`([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image3.png))


下一步会要求我们指定要连接到内容数据库。 选择`NORTHWIND.MDF`数据库文件从下拉列表中，单击下一步。 由于这是首次我们使用此数据库，该向导将提供用于存储连接字符串中的`Web.config`。 将其存储连接字符串使用名称`NorthwindConnectionString`。


[![连接到 Northwind 数据库](interacting-with-the-master-page-from-the-content-page-cs/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image4.png)

**图 02**： 连接到 Northwind 数据库 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image6.png))


配置数据源向导提供了通过其中我们可以指定用于检索数据的查询的两个方法：

- 通过指定自定义 SQL 语句或存储的过程，或
- 通过选择表或视图，然后指定要返回的列

因为我们想要返回 5 个最新添加的产品，我们需要指定自定义 SQL 语句。 使用以下 SELECT 查询：


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample1.sql)]

`TOP 5`关键字的查询返回只有前五个记录。 `Products`表的主键`ProductID`，是`IDENTITY`列中，从而确保我们添加到表中每个新产品，将具有更大的值比以前的条目。 因此，对通过结果进行排序`ProductID`以降序返回从开始最新创建的产品。


[![返回最近添加的五种产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image7.png)

**图 03**： 返回五种最最近添加的产品 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image9.png))


完成向导后，Visual Studio 将生成的 GridView，其中显示两个 BoundFields`ProductName`和`UnitPrice`从数据库返回的字段。 此时主页面的声明性标记应包括标记类似于以下内容：


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample2.aspx)]

正如您所看到的包含标记： 标签 Web 控件 (`GridMessage`); GridView `RecentProducts`，两个 BoundFields; 并且返回的五个最近添加的产品使用 SqlDataSource 控件。

与此 GridView 创建和配置，其 SqlDataSource 控件访问网站，通过浏览器。 如图 4 所示，你将看到其中列出了五个最近左下角中的一个网格添加产品。


[![GridView 显示五个最近添加的产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image10.png)

**图 04**: GridView 显示五种最最近添加的产品 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image12.png))


> [!NOTE]
> 随意清理的 GridView 的外观。 某些建议包括格式设置在显示`UnitPrice`值作为货币和使用背景颜色和字体以改善该网格的外观。


## <a name="step-2-creating-a-content-page-to-add-new-products"></a>步骤 2： 创建内容页添加的新产品

我们的下一个任务是创建用户可以从其添加到新产品的内容页面`Products`表。 添加到新的内容页`Admin`名为的文件夹`AddProduct.aspx`，确保将将其绑定到`Site.master`母版页。 此页添加到网站后，图 5 显示了在解决方案资源管理器。


[![向管理员文件夹添加新的 ASP.NET 页面](interacting-with-the-master-page-from-the-content-page-cs/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image13.png)

**图 05**： 添加到新的 ASP.NET 页`Admin`文件夹 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image15.png))


回想一下，在[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中，我们创建一个名为的自定义基本页类`BasePage`如果它已生成了页面的标题未显式设置。 转到`AddProduct.aspx`页面的代码隐藏类，并将其派生`BasePage`(而不是从`System.Web.UI.Page`)。

最后，更新`Web.sitemap`文件以便包括本课程中的一个条目。 添加以下标记下方`<siteMapNode>`控件 ID 命名问题课程：


[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample3.xml)]

图 6 中，添加此中所示`<siteMapNode>`元素将反映在课程列表。

返回到`AddProduct.aspx`。 中的内容控件`MainContent`ContentPlaceHolder，添加的 DetailsView 控件并将其命名`NewProduct`。 绑定到名为的新 SqlDataSource 控件的 DetailsView `NewProductDataSource`。 例如，使其使用 Northwind 数据库，则使用在步骤 1 中 SqlDataSource，配置向导和选择来指定自定义 SQL 语句。 由于 DetailsView 将用于将项添加到数据库，我们需要同时指定`SELECT`语句和一个`INSERT`语句。 使用以下`SELECT`查询：


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample4.sql)]

然后，从插入选项卡，添加以下`INSERT`语句：


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample5.sql)]

完成向导后转到 DetailsView 的智能标记，并选中"启用插入"复选框。 这会向与 DetailsView 添加 CommandField 其`ShowInsertButton`属性设置为 true。 由于此 DetailsView 将使用仅用于插入数据，因此设置 DetailsView`DefaultMode`属性设置为`Insert`。

这就是一切就这么简单 ！ 让我们来测试此页。 请访问`AddProduct.aspx`通过浏览器中，输入名称和价格 （请参见图 6）。


[![向数据库添加一个新的产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image16.png)

**图 06**： 向数据库添加一个新的产品 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image18.png))


键入后的名称和新产品的价格中，单击插入按钮。 这会导致窗体回发。 在回发时，SqlDataSource 控件的`INSERT`执行语句; 其两个参数都填入 DetailsView 的两个 TextBox 控件中的用户输入值。 遗憾的是，没有插入发生任何可视反馈。 很高兴有消息显示，确认已添加新记录。 我将此当作练习留给读者。 此外，从 DetailsView 添加一条新记录后在母版页中的 GridView 仍显示相同的五个记录作为之前;它不包括刚添加的记录。 我们将介绍如何解决此问题在即将发布的步骤。

> [!NOTE]
> 除了添加某种形式的可视反馈，已成功插入，我建议您也更新 DetailsView 插入接口，以包括验证。 目前，没有任何验证。 如果用户输入的值无效`UnitPrice`字段，如"过高，"时，系统尝试将该字符串转换成十进制数字，将在回发时引发异常。 有关自定义插入的详细信息的接口，请参阅[*自定义数据修改界面*教程](../../data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)从我[使用数据教程系列](../../data-access/index.md).


## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>步骤 3： 在母版页中创建的公共属性和方法

步骤 1 中我们添加了一个名为标签 Web 控件`GridMessage`上面在母版页中 GridView。 此标签用于根据需要显示一条消息。 例如，在添加新记录到`Products`表中，我们可能想要显示一条消息:"*ProductName*已添加到数据库。" 而不是硬编码的母版页中的此标签的文本，我们可能想要通过内容页可自定义的消息。

因为它不能直接从内容页访问的母版页中的受保护的成员变量作为实现标签控件。 我们需要在公开 Web 控件或充当其属性之一可以进行的代理的主页面中创建的公共属性才能使用母版页从内容页 （或，就此而言，母版页中的任何 Web 控件） 中的标签 访问。 将以下语法添加到主页面的代码隐藏类公开的标签`Text`属性：


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample6.cs)]

当一条新记录添加到`Products`从内容页表`RecentProducts`母版页中的 GridView 需要重新绑定到其基础数据源。 若要重新绑定的 GridView 调用其`DataBind`方法。 由于在母版页中的 GridView 不是以编程方式访问内容的页面，我们需要创建一个公共方法，主页面中，调用时，重新绑定到 GridView 数据。 将以下方法添加到主页面的代码隐藏类：


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample7.cs)]

与`GridMessageText`属性和`RefreshRecentProductsGrid`方法准备就绪后的，任何内容的页面可以以编程方式设置或读取的值`GridMessage`标签的`Text`属性或重新绑定到数据`RecentProducts`GridView。 步骤 4 探讨如何从内容页访问母版页的公共属性和方法。

> [!NOTE]
> 别忘了将母版页的属性和方法作为标记`public`。 如果您不显式表示这些属性和方法作为`public`，它们将无法从内容页访问。


## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>步骤 4： 从内容页调用母版页的公共成员

现在，主页面具有必要的公共属性和方法，我们已准备好调用这些属性和方法从`AddProduct.aspx`内容页。 具体而言，我们需要设置的母版页`GridMessageText`属性并调用其`RefreshRecentProductsGrid`方法后已添加到数据库的新产品。 所有 ASP.NET 数据 Web 控件都触发事件之前和之后完成各种任务，这样可以方便页面开发人员采取某些编程操作之前或之后的任务。 例如，当最终用户单击 DetailsView 的插入按钮，在回发，DetailsView 将引发其`ItemInserting`开始插入工作流之前的事件。 然后，它将记录插入到数据库。 接下来，DetailsView 引发其`ItemInserted`事件。 因此，若要添加的新产品后使用母版页，DetailsView 为创建事件处理程序`ItemInserted`事件。

有两种方法的内容页面以编程方式可通过使用其主页面：

- 使用`Page.Master`属性，它返回到母版页的松散类型化引用，或
- 指定通过该页面的母版页类型或文件路径`@MasterType`指令; 这会自动将强类型属性添加到名为页`Master`。

让我们看一下这两种方法。

### <a name="using-the-loosely-typedpagemasterproperty"></a>使用松散类型`Page.Master`属性

所有 ASP.NET web 页面必须都派生自`Page`类，该类位于`System.Web.UI`命名空间。 `Page`类包括[`Master`属性](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx)返回到页面的母版页的引用。 如果页面没有母版页`Master`返回`null`。

`Master`属性返回类型的对象[ `MasterPage` ](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) (也位于`System.Web.UI`命名空间) 这是所有的主页面中从其派生的基类型。 因此，若要使用公共属性或方法定义在我们网站的主页面，我们必须强制转换`MasterPage`返回对象`Master`为适当的类型的属性。 由于我们命名我们主控页文件，因此`Site.master`，代码隐藏类名为`Site`。 因此，下面的代码转换`Page.Master`指向站点类的实例的属性。


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample8.cs)]

现在，我们已强制转换后的松散类型`Page.Master`属性设置为`Site`我们可以引用的属性和特定于站点的方法的类型。 如图 7 所示，公共属性`GridMessageText`IntelliSense 下拉列表中显示。


[![IntelliSense 显示了我们的主页面的公共属性和方法](interacting-with-the-master-page-from-the-content-page-cs/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image19.png)

**图 07**: IntelliSense 显示了我们的主页面的公共属性和方法 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image21.png))


> [!NOTE]
> 如果您在主页面文件命名为`MasterPage.master`母版页的代码隐藏类名为`MasterPage`。 这可能导致不明确的代码时的类型强制转换`System.Web.UI.MasterPage`到你`MasterPage`类。 简单地说，您需要完全限定的类型转换为，使用网站项目模型时，可以有点棘手。 我的建议是要确保，创建主页面时将其命名名称不是`MasterPage.master`或甚至更好地创建主页面的强类型引用。


### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>创建具有强类型化引用`@MasterType`指令

如果您仔细查看您所见，ASP.NET 页面的代码隐藏类是分部类 (请注意`partial`类定义中的关键字)。 分部类在 C# 和 Visual Basic 使用.net Framework 2.0 中引入，并简单地说，允许跨多个文件中定义的类的成员。 代码隐藏类文件- `AddProduct.aspx.cs`，例如-包含页面开发人员，我们创建的代码。 除了我们代码中，ASP.NET 引擎会自动创建单独的类文件具有属性和事件处理程序中，将声明性标记转换为页的类层次结构。

只要访问 ASP.NET 页面时就会发生的自动代码生成铺平了一些相当有趣且有用的可能性。 对于主页面，如果我们告诉我们内容的页面正在使用哪些母版页的 ASP.NET 引擎就会生成强类型`Master`为我们的属性。

使用[`@MasterType`指令](https://msdn.microsoft.com/library/ms228274.aspx)以通知 ASP.NET 引擎的内容页面的母版页类型。 `@MasterType`指令可以接受的母版页的类型名称或其文件路径。 若要指定的`AddProduct.aspx`页上使用`Site.master`作为其主页面的顶部添加以下指令`AddProduct.aspx`:


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample9.aspx)]

此指令指示要添加到名为的属性通过母版页的强类型化引用的 ASP.NET 引擎`Master`。 与`@MasterType`指令中的位置，我们可以调用`Site.master`主页面的公共属性和方法直接通过`Master`而无需任何强制转换的属性。

> [!NOTE]
> 如果省略`@MasterType`指令，语法`Page.Master`和`Master`返回相同的操作： 将松散类型化对象传递给页面的母版页。 如果包括`@MasterType`指令然后`Master`返回对指定的母版页的强类型引用。 `Page.Master`但是，仍然会返回一个松散类型化的引用。 如原因更全面地了解这种情况以及如何`Master`构造属性时`@MasterType`指令是包含，请参阅[K.Scott Allen](http://odetocode.com/blogs/scott/default.aspx)的博客文章[`@MasterType`在 ASP.NET 2.0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx).


### <a name="updating-the-master-page-after-adding-a-new-product"></a>添加一个新的产品后更新母版页

既然我们知道如何调用主页面的公共属性和内容页面中的方法，我们就准备好更新`AddProduct.aspx`页，以便添加一个新的产品后刷新主页面。 我们的第 4 步开始处创建 DetailsView 控件的事件处理程序`ItemInserting`事件，新产品添加到数据库后立即执行。 将以下代码添加到该事件处理程序：


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample10.cs)]

上述代码使用这两种松散类型化`Page.Master`属性的和强类型`Master`属性。 请注意，`GridMessageText`属性设置为"*ProductName*添加到网格..."刚添加产品的值是可通过访问`e.Values`集合; 正如您所看到的刚添加`ProductName`通过访问值`e.Values["ProductName"]`。

图 8 显示了`AddProduct.aspx`立即后一种新产品-Scott 的 Soda 的页已添加到数据库。 请注意，刚添加的产品名称将其记录在母版页的标签和 GridView 刷新以包括产品和它的价格。


[![母版页的标签和 GridView 显示刚添加产品](interacting-with-the-master-page-from-the-content-page-cs/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image22.png)

**图 08**： 在母版页的标签和 GridView 显示 Just-Added 产品 ([单击以查看实际尺寸的图像](interacting-with-the-master-page-from-the-content-page-cs/_static/image24.png))


## <a name="summary"></a>总结

理想情况下，主页面和其内容的页面是从另一个完全独立，不需要交互的任何级别。 母版页和内容页面应设计为具有该目标，虽然有多种常见方案中的内容页必须与其主页面。 最常见原因之一是围绕更新母版页显示根据在内容页中发生某些操作的特定部分。

好消息是，它是相对比较简单，在内容页面中以编程方式与其主页面进行交互。 首先在封装的功能，需要调用的内容页面的母版页中创建公共属性或方法。 然后，在内容页访问母版页的属性和方法通过松散类型化`Page.Master`属性或使用`@MasterType`指令来创建到母版页的强类型引用。

在下一步的教程中，我们将说明如何有母版页与内容页面之一以编程方式进行交互。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问和更新在 ASP.NET 中的数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 母版页： 提示、 技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [`@MasterType` 在 ASP.NET 2.0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [内容和母版页之间传递信息](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [在 ASP.NET 教程中使用的数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](control-id-naming-in-content-pages-cs.md)
> [下一页](interacting-with-the-content-page-from-the-master-page-cs.md)
