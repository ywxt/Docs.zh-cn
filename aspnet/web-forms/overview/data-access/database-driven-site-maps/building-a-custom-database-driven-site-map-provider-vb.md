---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: 生成自定义数据库驱动站点地图提供程序 (VB) |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET 2.0 中的默认站点地图提供静态的 XML 文件中检索其数据。 适用于许多小型和中等大小的基于 XML 的提供程序时...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 55658c563b6dd3c3b097e562cb1fe036bbfce815
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831096"
---
<a name="building-a-custom-database-driven-site-map-provider-vb"></a>生成自定义数据库驱动站点地图提供程序 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip)或[下载 PDF](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> 在 ASP.NET 2.0 中的默认站点地图提供静态的 XML 文件中检索其数据。 适用于许多小型和中型 Web 站点的基于 XML 的提供程序时，更大的 Web 应用程序需要更多动态站点地图。 在本教程中，我们将构建自定义站点地图提供程序的业务逻辑层中检索其数据，这又从数据库检索数据。


## <a name="introduction"></a>介绍

ASP.NET 2.0 的站点地图功能使页面开发人员的 XML 文件中，如定义一些持久介质中的 web 应用程序的站点图。 定义后，可以通过以编程方式访问站点地图数据[`SiteMap`类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)中[`System.Web`命名空间](https://msdn.microsoft.com/library/system.web.aspx)或通过各种导航 Web 控件，如SiteMapPath、 菜单和树视图控件。 使用站点映射系统[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，以便可以创建不同的站点映射的序列化实现，并将其插入到 web 应用程序。 默认站点映射提供程序使用 ASP.NET 2.0 随附仍然存在站点地图结构中的 XML 文件。 回到[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，我们创建一个名为文件`Web.sitemap`，包含此结构中，并且具有与每个新的教程部分已更新其 XML。

默认的基于 XML 的站点映射提供程序还适用于站点地图的结构是相当静态的如为这些教程。 在许多情况下，但是，更具动态站点地图需要。 请考虑在图 1 中，每个类别和产品出现的位置为网站的结构中的一段所示的站点映射。 与此站点图中，访问与根节点相对应的 web 页面中可能会列出所有类别，而访问特定类别 s web 页面将列出该类别的产品和查看特定产品 s web 页面将显示该产品 s 详细信息。


[![类别和产品构成站点地图的结构](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**图 1**: 类别和产品构成站点地图的结构 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png))


虽然此基于类别和产品的结构可能是硬编码到`Web.sitemap`文件，该文件将需要一个类别时进行更新，或添加、 移除或重命名为产品。 因此，站点映射维护会极大地简化如果从数据库或，理想情况下，业务逻辑层的应用程序 s 体系结构中检索到它的结构。 这样一来，如已添加产品和类别，请重命名或删除，站点图将自动更新以反映这些更改。

由于 ASP.NET 2.0 的站点映射序列化提供程序模型之上构建，因此我们可以创建我们自己自定义站点地图提供程序获取其数据从备用数据存储，例如数据库或体系结构。 在本教程中我们将构建的自定义提供程序从 BLL 中检索其数据。 让我们来开始 ！

> [!NOTE]
> 在本教程中创建的自定义站点映射提供程序紧密耦合到应用程序 s 体系结构和数据模型。 Jeff Prosise s[存储在 SQL Server 中的站点映射](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)并[SQL 站点地图提供程序以前已等待](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)文章检查 SQL Server 中存储站点地图数据的通用的方法。


## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>步骤 1： 创建自定义站点映射提供程序 Web 页

我们开始创建自定义的站点地图提供程序之前，让我们来首先添加我们需要本教程中的 ASP.NET 页。 首先，通过添加一个名为的新文件夹`SiteMapProvider`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

此外将添加`CustomProviders`文件夹的子`App_Code`文件夹。


![将 ASP.NET 页面添加站点映射提供程序与相关的教程](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**图 2**： 添加站点的 ASP.NET 页将映射与提供程序相关的教程


由于没有为本部分中只有一个教程，我们不需要`Default.aspx`列出节的教程。 相反，`Default.aspx`将 GridView 控件中显示的类别。 我们将在步骤 2 中来解决此问题。

接下来，更新`Web.sitemap`包括对引用`Default.aspx`页。 具体而言，缓存后添加以下标记`<siteMapNode>`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包括唯一的站点映射提供程序教程所需的项。


![站点图现在包含一个条目的站点映射提供程序教程](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**图 3**： 站点图现在包含一个条目的站点映射提供程序教程


此教程 s 主要焦点是为了说明创建自定义的站点地图提供程序和 web 应用程序配置为使用该提供程序。 具体而言，我们将构建的提供程序返回包括为每个类别和产品，节点以及一个根节点的站点映射，如下图中图 1 所示。 一般情况下，站点图的每个节点可能指定的 URL。 对于我们站点地图的根节点的 URL 将为`~/SiteMapProvider/Default.aspx`，这将列出所有数据库中的类别。 站点地图中的每个类别节点将具有指向的 URL `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`，这将列出在指定的产品的所有*categoryID*。 最后，每个产品的站点地图节点将指向`~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`，随后会显示特定产品 s 详细信息。

若要开始我们需要创建`Default.aspx`， `ProductsByCategory.aspx`，和`ProductDetails.aspx`页。 这些页面分别在步骤 2、 3 和 4 中完成。 由于本教程的主旨是位于在站点地图提供程序，并且由于过去教程已介绍如何创建报告的这种多页母版/详细信息，我们将一蹴而就完成步骤 2 至 4。 如果你需要在创建跨越多个页面的母版/详细信息报表刷新程序，请返回到[母版/详细信息筛选跨两个页面](../masterdetail/master-detail-filtering-across-two-pages-vb.md)教程。

## <a name="step-2-displaying-a-list-of-categories"></a>步骤 2： 显示类别的列表

打开`Default.aspx`页中`SiteMapProvider`文件夹，然后拖动 GridView 从工具箱拖到设计器中，设置其`ID`到`Categories`。 从 GridView s 智能标记，请将其绑定到名为新 ObjectDataSource`CategoriesDataSource`并将其配置，以便它将检索其数据使用`CategoriesBLL`类的`GetCategories`方法。 由于此 GridView 只显示类别，并且不提供数据修改功能，设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![配置对象数据源返回类别使用 GetCategories 方法](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**图 4**： 配置到返回类别使用 ObjectDataSource`GetCategories`方法 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png))


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**图 5**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png))


完成配置数据源向导后，Visual Studio 将添加为 BoundField `CategoryID`， `CategoryName`， `Description`， `NumberOfProducts`，和`BrochurePath`。 编辑，使其仅包含 GridView`CategoryName`并`Description`BoundFields 和更新`CategoryName`BoundField 的`HeaderText`类别的属性。

接下来，添加 HyperLinkField 并因此放置其 s 最左侧的字段。 设置`DataNavigateUrlFields`属性设置为`CategoryID`并`DataNavigateUrlFormatString`属性设置为`~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`。 设置`Text`查看产品的属性。


![将 HyperLinkField 添加到类别 GridView](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**图 6**： 添加到 HyperLinkField `Categories` GridView


创建 ObjectDataSource 和自定义 GridView 的字段后, 两个控件声明性标记将如下所示：


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

图 7 显示了`Default.aspx`时的浏览器查看。 单击类别的查看产品链接将你带到`ProductsByCategory.aspx?CategoryID=categoryID`，其在步骤 3 中，我们将生成。


[![每个类别是列出沿与视图产品链接](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**图 7**： 列出沿与视图产品链接为每个类别 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png))


## <a name="step-3-listing-the-selected-category-s-products"></a>步骤 3： 列出所选的类别的产品

打开`ProductsByCategory.aspx`页上，添加一个 GridView，其命名为`ProductsByCategory`。 从其智能标记将 GridView 绑定到名为新 ObjectDataSource `ProductsByCategoryDataSource`。 配置要使用 ObjectDataSource`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法，设置下拉列表中的更新、 插入和删除选项卡为 （无） 列表。


[![使用 ProductsBLL 类的 GetProductsByCategoryID(categoryID) 方法](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**图 8**： 使用`ProductsBLL`类 s`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png))


配置数据源向导的最后一步会提示输入参数源*categoryID*。 因为此信息将通过查询字符串字段`CategoryID`、 从下拉列表中选择查询字符串和 QueryStringField 文本框中输入类别 id，如图 9 中所示。 单击完成以完成向导。


[![使用 CategoryID 查询字符串字段的 categoryID 参数](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**图 9**： 使用`CategoryID`查询字符串字段*categoryID*参数 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png))


完成向导后，Visual Studio 将添加相应 BoundFields 和 CheckBoxField 到产品数据字段的 GridView。 删除所有除`ProductName`， `UnitPrice`，和`SupplierName`BoundFields。 自定义以下三个 BoundFields`HeaderText`属性分别读取产品、 价格和供应商。 格式`UnitPrice`BoundField 作为一种货币。

接下来，添加 HyperLinkField 并将其移动到的最左边的位置。 设置其`Text`属性设置为视图的详细信息，其`DataNavigateUrlFields`属性设置为`ProductID`，并将其`DataNavigateUrlFormatString`属性设置为`~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`。


![添加指向 ProductDetails.aspx 视图的详细信息 HyperLinkField](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**图 10**： 添加视图详细信息指向 HyperLinkField `ProductDetails.aspx`


进行这些自定义之后, 的 GridView 和 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

返回到查看`Default.aspx`通过浏览器和查看产品上的单击链接饮料对应的。 这会转到`ProductsByCategory.aspx?CategoryID=1`，Northwind 数据库属于饮料类别中显示名称、 价格和产品的供应商 （请参阅图 11）。 可随意进一步增强此页以包含将其返回到类别列表页的用户的链接 (`Default.aspx`) 和 detailsview FormView 控件显示所选的类别的名称和说明。


[![显示饮料名称、 价格和供应商](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**图 11**： 显示饮料名称、 价格和供应商 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png))


## <a name="step-4-showing-a-product-s-details"></a>步骤 4： 显示产品 s 详细信息

最后一页， `ProductDetails.aspx`，显示所选的产品的详细信息。 打开`ProductDetails.aspx`并从工具箱拖动到设计器中拖动 DetailsView。 设置 DetailsView s`ID`属性设置为`ProductInfo`并将清除其`Height`和`Width`属性值。 从其智能标记将 DetailsView 绑定到名为新 ObjectDataSource `ProductDataSource`，配置将从其数据 ObjectDataSource`ProductsBLL`类的`GetProductByProductID(productID)`方法。 如步骤 2 和 3 中创建的上一个网页，设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![配置对象数据源使用 GetProductByProductID(productID) 方法](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**图 12**： 配置为使用 ObjectDataSource`GetProductByProductID(productID)`方法 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))


配置数据源向导的最后一步会提示输入的源*productID*参数。 因为这些数据包括通过查询字符串字段`ProductID`，将下拉列表设置为查询字符串和到 ProductID QueryStringField 文本框。 最后，单击完成按钮以完成向导。


[![配置产品 id 参数，以从产品 id 查询字符串字段中提取其值](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**图 13**： 配置*productID*参数来提取其值从`ProductID`查询字符串字段 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))


完成配置数据源向导后，Visual Studio 将创建相应 BoundFields 和 CheckBoxField 产品数据字段的 DetailsView 中。 删除`ProductID`， `SupplierID`，和`CategoryID`BoundFields 并根据需要配置剩余的字段。 少量的美观的配置之后, 我 DetailsView 和 ObjectDataSource s 的声明性标记看起来如下所示：


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

若要测试此页，请返回到`Default.aspx`然后单击查看产品的饮料类别。 从饮料产品列表中，单击 Chai 茶的查看详细信息链接。 这会转到`ProductDetails.aspx?ProductID=1`，其中显示 Chai 茶 s （请参阅图 14） 的详细信息。


[![显示 Chai 茶 s 供应商、 类别、 价格和其他信息](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**图 14**： 显示 Chai 茶 s 供应商、 类别、 价格和其他信息 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png))


## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>步骤 5： 了解站点地图提供程序的内部工作机制

站点图在 web 服务器的内存中表示为一系列`SiteMapNode`构成了层次结构的实例。 必须有且只有一个根、 所有非根节点必须有且只有一个父节点，和的所有节点可能都包含任意数目的子级。 每个`SiteMapNode`对象表示网站的结构中的某个部分; 这些部分通常具有相应的 web 页。 因此， [ `SiteMapNode`类](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)具有属性，如`Title`， `Url`，和`Description`，其中介绍的部分`SiteMapNode`表示。 此外，还有`Key`属性，用于唯一地标识每个`SiteMapNode`中的层次结构，以及用来建立此层次结构的属性`ChildNodes`， `ParentNode`， `NextSibling`， `PreviousSibling`，依次类推。

图 15 显示了常规的站点地图结构，来自图 1 中，但具有更精细地草绘的实现详细信息。


[![每个 SiteMapNode 具有属性如标题、 Url、 密钥等等](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**图 15**： 每个`SiteMapNode`都有一些属性例如`Title`， `Url`，`Key`等 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif))


站点图是可通过访问[`SiteMap`类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)中[`System.Web`命名空间](https://msdn.microsoft.com/library/system.web.aspx)。 此类 s`RootNode`属性返回的站点映射的根目录`SiteMapNode`实例;`CurrentNode`将返回`SiteMapNode`其`Url`属性与当前请求页的 URL 匹配。 ASP.NET 2.0 的导航 Web 控件在内部使用此类。

当`SiteMap`的类属性进行访问，它必须序列从一些持久介质站点地图结构化到内存中。 但是，站点映射的序列化逻辑不是硬编码到`SiteMap`类。 相反，在运行时`SiteMap`类确定哪些站点图*提供程序*用于序列化。 默认情况下[`XmlSiteMapProvider`类](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)使用时，这从格式正确的 XML 文件中读取站点地图的结构。 但是，很少的工作与我们可以创建我们自己自定义站点地图提供程序。

所有站点地图提供程序必须都派生自[`SiteMapProvider`类](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)，其中包括基本的方法和属性所需的站点映射提供程序，但省略的许多实现细节。 第二个类的[ `StaticSiteMapProvider` ](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)，扩展了`SiteMapProvider`类，其中包含所需的功能的更可靠的实现。 在内部，`StaticSiteMapProvider`存储`SiteMapNode`实例的站点中的映射`Hashtable`，并提供等方法`AddNode(child, parent)`，`RemoveNode(siteMapNode),`和`Clear()`的添加和删除`SiteMapNode`到内部 s `Hashtable`。 `XmlSiteMapProvider` 派生自 `StaticSiteMapProvider`。

当创建自定义的站点地图提供程序扩展了`StaticSiteMapProvider`，必须重写的两种抽象方法： [ `BuildSiteMap` ](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx)并[ `GetRootNodeCore` ](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)。 `BuildSiteMap`正如其名，负责从持久性存储区加载站点地图结构和构造内存中。 `GetRootNodeCore` 在站点地图中返回的根节点。

前一个 web 应用程序可以使用它必须在应用程序配置中注册站点映射提供程序。 默认情况下`XmlSiteMapProvider`类使用的名称注册`AspNetXmlSiteMapProvider`。 若要注册其他站点地图提供程序，添加以下标记到`Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*名称*值为指定用户可读名称时提供程序*类型*指定站点地图提供程序的完全限定类型名称。 我们将探讨的具体值的*名称*并*类型*在步骤 7 中的值后，我们制作了我们自定义站点地图提供程序。

站点映射提供程序类实例化第一次从访问`SiteMap`类并且保持在内存中为 web 应用程序的生存期。 由于没有站点地图提供程序，可能从多个并发网站访问者调用的一个实例，它是命令性提供程序的方法将*线程安全*。

出于性能和可伸缩性原因，它非常重要，我们在缓存在内存中的站点映射结构并将返回此缓存的结构，而不是无需重新创建每次`BuildSiteMap`调用方法。 `BuildSiteMap` 不能调用多次，每个页请求，每个用户，具体取决于页和站点地图结构的深度中使用导航控件。 在任何情况下，如果我们不会缓存在站点地图结构`BuildSiteMap`每次调用它时我们将需要重新检索已从 （这将在查询中对数据库产生） 的体系结构的产品和类别信息。 如我们在前面的缓存教程所述，缓存的数据可能会失效。 若要应对这种情况，我们可以使用时间-或 SQL 缓存依赖项基于满。

> [!NOTE]
> 站点地图提供程序可能会根据需要重写[`Initialize`方法](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)。 `Initialize` 站点地图提供程序首次实例化并传递任何自定义属性分配给中的提供程序时调用`Web.config`中`<add>`元素一样的元素： `<add name="name" type="type" customAttribute="value" />`。 如果你想要允许页面开发人员可以指定各种站点映射提供程序相关设置，而无需修改提供程序的代码，它非常有用。 例如，如果我们已读取的类别和产品数据直接从数据库而不是通过体系结构，d 我们可能想要让页面开发人员指定数据库连接字符串通过`Web.config`而不是使用硬编码提供程序的代码中的值。 第 6 步中，我们将构建的自定义站点映射提供程序不会覆盖此`Initialize`方法。 有关使用的示例`Initialize`方法，请参阅[Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s[存储在 SQL Server 中的站点映射](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)文章。


## <a name="step-6-creating-the-custom-site-map-provider"></a>步骤 6： 创建自定义站点映射提供程序

若要创建自定义站点地图提供程序的生成中的类别和产品 Northwind 数据库中的站点映射，我们需要创建一个类以扩展`StaticSiteMapProvider`。 在步骤 1 中要求您将添加`CustomProviders`文件夹中的`App_Code`文件夹-将新类添加到此文件夹名为`NorthwindSiteMapProvider`。 将下面的代码添加到 `NorthwindSiteMapProvider` 类中:


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

让我们来首先了解此类 s`BuildSiteMap`方法，开头[`lock`语句](https://msdn.microsoft.com/library/c5kehkcz.aspx)。 `lock`语句只允许一个线程每次输入，从而序列化其代码的访问权限和防止两个并发线程上另一个 s 数量屈指可数单步执行。

在类级别`SiteMapNode`变量`root`用于缓存站点地图结构。 第一次，或后已修改基础数据，第一次构造站点图时`root`将为`Nothing`并将构建站点地图结构。 站点地图的根节点分配给`root`在构造期间进程，以便下一次此方法调用时，`root`不会`Nothing`。 因此，只要`root`不是`Nothing`站点地图结构将返回到调用方无需重新创建它。

如果根是`Nothing`，站点地图结构创建中的产品和类别信息。 创建生成站点地图`SiteMapNode`实例，然后组成的层次结构，通过调用`StaticSiteMapProvider`类的`AddNode`方法。 `AddNode` 执行存储各种内部簿记`SiteMapNode`实例中`Hashtable`。 我们开始构造层次结构之前，首先通过调用`Clear`方法，从内部的元素将清除`Hashtable`。 下一步，`ProductsBLL`类 s`GetProducts`方法，并生成`ProductsDataTable`存储在本地变量中。

站点映射的构造首先创建根节点并将其分配给`root`。 重载[ `SiteMapNode` s 构造函数](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx)用于此处并在这整个`BuildSiteMap`传递以下信息：

- 对站点地图提供程序的引用 (`Me`)。
- `SiteMapNode` S `Key`。 这所必需的值必须是唯一的每个`SiteMapNode`。
- `SiteMapNode` S `Url`。 `Url` 是可选的但是，如果提供，每个`SiteMapNode`s`Url`值必须唯一。
- `SiteMapNode` S `Title`，这是所必需。

`AddNode(root)`方法调用添加`SiteMapNode``root`到作为根站点映射。 下一步，每个`ProductRow`在`ProductsDataTable`枚举。 如果已存在`SiteMapNode`当前产品 s 类别，引用它。 否则为新`SiteMapNode`创建并添加为的子类别`SiteMapNode``root`通过`AddNode(categoryNode, root)`方法调用。 之后相应的类别`SiteMapNode`已找到或创建的节点`SiteMapNode`是为当前的产品创建和添加为类别的子`SiteMapNode`通过`AddNode(productNode, categoryNode)`。 请注意，类别`SiteMapNode`s`Url`属性值是`~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`while 产品`SiteMapNode`s`Url`属性分配`~/SiteMapNode/ProductDetails.aspx?ProductID=productID`。

> [!NOTE]
> 这些产品的数据库`NULL`值及其`CategoryID`按类别分组`SiteMapNode`其`Title`属性设置为 None，它的`Url`属性设置为空字符串。 我决定设置`Url`为空字符串以来`ProductBLL`类 s`GetProductsByCategory(categoryID)`方法目前缺少的功能，以返回与仅对这些产品`NULL``CategoryID`值。 此外，我要演示导航控件的呈现方式`SiteMapNode`缺少的值及其`Url`属性。 我鼓励您扩展本教程中，以便无`SiteMapNode`s`Url`属性指向`ProductsByCategory.aspx`，但仅显示与产品`NULL``CategoryID`值。


构造站点图后, 的任意对象添加到使用 SQL 缓存依赖项上的数据缓存`Categories`并`Products`表通过`AggregateCacheDependency`对象。 我们探讨了前面教程中，使用 SQL 缓存依赖项*使用 SQL 缓存依赖项*。 自定义站点地图提供程序，但是，使用的数据缓存的重载`Insert`方法，我们 ve 有待探索。 此重载接受作为其最后一个输入参数从缓存中移除对象时调用的委托。 具体而言，我们传入的新[`CacheItemRemovedCallback`委托](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx)指向`OnSiteMapChanged`方法定义中的进一步`NorthwindSiteMapProvider`类。

> [!NOTE]
> 站点地图的内存中表示缓存通过类级别变量`root`。 由于只有一个实例的自定义站点映射提供程序类，因为该实例在所有线程之间共享 web 应用程序中，此类变量用作缓存。 `BuildSiteMap`方法还将使用数据缓存，但仅作为一种方法在基础数据库中的数据时收到通知`Categories`或`Products`表的更改。 请注意，将放入数据缓存的值只是当前日期和时间。 实际的站点地图数据是*不*放入数据缓存中。


`BuildSiteMap`方法完成通过返回站点地图的根节点。

剩余方法都是非常简单。 `GetRootNodeCore` 负责返回的根节点。 由于`BuildSiteMap`返回的根`GetRootNodeCore`只需返回`BuildSiteMap`s 返回值。 `OnSiteMapChanged`方法设置`root`回`Nothing`中删除缓存项的时间。 使用重新设置为根`Nothing`，则下次`BuildSiteMap`是调用，站点地图结构将重新生成。 最后，`CachedDate`属性返回的数据缓存中存储的日期和时间值，如果存在这样的值。 页面开发人员可以使用此属性来确定上次缓存站点地图数据。

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>步骤 7： 注册`NorthwindSiteMapProvider`

为了使 web 应用程序以使用`NorthwindSiteMapProvider`站点地图提供程序在步骤 6 中创建，我们需要将其在注册`<siteMap>`一部分`Web.config`。 具体而言，添加以下标记内的`<system.web>`中的元素`Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

此标记有两个用途： 首先，它表明内置`AspNetXmlSiteMapProvider`是默认站点映射提供程序; 其次，它会注册的自定义站点地图提供程序在步骤 6 中创建与 Northwind 的用户友好名称。

> [!NOTE]
> 在站点地图提供程序位于应用程序 s`App_Code`文件夹中，值`type`属性是只是类名称。 或者，自定义站点映射提供程序无法在一个单独的类库项目中使用创建编译的程序集放置在 web 应用程序的`/Bin`目录。 在这种情况下，`type`属性的值将是*Namespace*。*ClassName*， *AssemblyName* 。


更新后`Web.config`，请花费片刻时间浏览器中查看任何页上，从这些教程。 请注意，在左侧的导航界面仍显示的各个部分，教程中定义`Web.sitemap`。 这是因为我们已将保留`AspNetXmlSiteMapProvider`作为默认提供程序。 若要创建使用的导航用户界面元素`NorthwindSiteMapProvider`，我们将需要显式指定，应使用 Northwind 站点地图提供程序。 我们将了解如何在步骤 8 中实现这一点。

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>步骤 8： 显示使用的自定义站点地图提供程序的站点映射信息

使用自定义站点映射提供程序创建并注册中`Web.config`，我们已准备好添加到导航控件重新`Default.aspx`， `ProductsByCategory.aspx`，和`ProductDetails.aspx`中的页面`SiteMapProvider`文件夹。 首先打开`Default.aspx`页上，并将其拖`SiteMapPath`从工具箱拖到设计器。 SiteMapPath 控件位于工具箱的导航部分。


[![将 SiteMapPath 添加到 Default.aspx](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**图 16**： 添加到 SiteMapPath `Default.aspx` ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif))


SiteMapPath 控件显示痕迹导航，，该值指示站点地图中的当前页的位置。 我们添加到主页面顶部的 SiteMapPath 回到*母版页和站点导航*教程。

请花费片刻时间来查看此页上的通过浏览器。 在图 16 中添加 SiteMapPath 使用的默认站点地图提供程序，将从其数据提取`Web.sitemap`。 因此，则痕迹导航主页显示&gt;自定义站点地图，就像在右上角痕迹导航。


[![痕迹导航中使用的默认站点地图提供程序](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**图 17**： 痕迹导航使用默认站点映射提供程序 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif))


如果希望使用我们在步骤 6 中创建的自定义站点地图提供 SiteMapPath 图 16 中添加，请设置其[`SiteMapProvider`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx)到 Northwind，我们分配给的名称`NorthwindSiteMapProvider`中`Web.config`。 遗憾的是，在设计器仍会继续使用的默认站点地图提供程序，但如果通过浏览器页面访问此属性更改后您将看到痕迹导航现在使用的自定义站点地图提供程序。


[![痕迹导航现在使用自定义站点映射提供程序 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**图 18**： 痕迹导航现在使用自定义站点地图提供程序`NorthwindSiteMapProvider`([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))


SiteMapPath 控件显示中的功能更强的用户界面`ProductsByCategory.aspx`和`ProductDetails.aspx`页。 将 SiteMapPath 添加到这些页面，设置`SiteMapProvider`向 Northwind 中的属性。 从`Default.aspx`单击饮料，查看产品链接，然后单击 Chai 茶的查看详细信息链接。 痕迹导航如图 19 所示，包括当前的站点映射节 （Chai 茶） 和其祖先： Beverages 和所有类别。


[![痕迹导航现在使用自定义站点映射提供程序 NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**图 19**： 痕迹导航现在使用自定义站点地图提供程序`NorthwindSiteMapProvider`([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))


除了 SiteMapPath，如菜单和 TreeView 控件，可以使用其他导航用户界面元素。 `Default.aspx`， `ProductsByCategory.aspx`，和`ProductDetails.aspx`页面中的下载本教程中，例如，所有包括菜单控件 （请参阅图 20）。 请参阅[检查 ASP.NET 2.0 的站点导航功能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)并[使用站点导航控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx)部分[ASP.NET 2.0 快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/)，更深入了解导航控件和 ASP.NET 2.0 中的站点映射系统。


[![菜单控件列出每个类别和产品](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**图 20**: 菜单控件列出了每个类别和产品 ([单击以查看实际尺寸的图像](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif))


在本教程前面所述，可以通过以编程方式访问站点地图结构`SiteMap`类。 以下代码将返回根目录`SiteMapNode`的默认提供程序：


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

由于`AspNetXmlSiteMapProvider`是默认提供程序对于我们的应用程序，上面的代码将返回定义中的根节点`Web.sitemap`。 若要引用而不是默认的站点地图提供，使用`SiteMap`类 s [ `Providers`属性](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx)如下所示：


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

其中*名称*是自定义站点映射提供程序 （web 应用程序罗斯文数据库） 的名称。

若要访问特定于站点地图提供程序的成员，请使用`SiteMap.Providers["name"]`来检索提供程序实例，然后将其转换为适当的类型。 例如，若要显示`NorthwindSiteMapProvider`s`CachedDate`属性在 ASP.NET 页中，使用以下代码：


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> 请确保测试出 SQL 缓存依赖项功能。 访问后`Default.aspx`， `ProductsByCategory.aspx`，和`ProductDetails.aspx`页，请转到之一中编辑、 插入和删除部分的教程和编辑类别或产品的名称。 然后返回到中的页面之一`SiteMapProvider`文件夹。 假设要注意到基础数据库更改的轮询机制已经历了足够的时间，站点图应更新以显示新产品或类别名称。


## <a name="summary"></a>总结

ASP.NET 2.0 的站点映射功能包括`SiteMap`类，大量的内置导航 Web 控件，并保存到 XML 文件的默认站点地图提供程序所需的站点映射信息。 若要使用来自其他源如从数据库中，应用程序 s 体系结构或远程 Web 服务，我们需要创建自定义的站点地图提供程序站点映射信息。 这涉及到创建直接或间接派生的类从`SiteMapProvider`类。

在本教程中我们已了解如何创建基于从应用程序体系结构中拣出的产品和类别信息的站点映射的自定义站点映射提供程序。 我们的提供程序扩展`StaticSiteMapProvider`类和引起创建`BuildSiteMap`检索了数据的方法构造站点映射层次结构，并缓存在类级别变量中生成的结构。 我们使用 SQL 缓存依赖项的回调函数具有要使之无效的已缓存结构时的基础`Categories`或`Products`修改数据。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [SQL Server 中存储的站点地图](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)和[以前已久的 SQL 站点地图提供程序](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)
- [ASP.NET 2.0 看 s 提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [提供程序工具包](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [检查 ASP.NET 2.0 的站点导航功能](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Dave Gardner、 Zack Jones、 Teresa Murphy 和伯纳黛特 Leigh。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](building-a-custom-database-driven-site-map-provider-cs.md)
