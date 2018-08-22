---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
title: 母版页和站点导航 (VB) |Microsoft Docs
author: rick-anderson
description: 用户友好的一个常见特性是网站的它们具有一致的、 站点范围的页面布局和导航方案。 本教程将探讨如何 y...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 022801d8-a327-4d0c-8780-6094c9cee00d
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
msc.type: authoredcontent
ms.openlocfilehash: 2a814fe8ed4a902061b2c50fd9d63983c4f6b2e8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830053"
---
<a name="master-pages-and-site-navigation-vb"></a>母版页和站点导航 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_3_VB.exe)或[下载 PDF](master-pages-and-site-navigation-vb/_static/datatutorial03vb1.pdf)

> 用户友好的一个常见特性是网站的它们具有一致的、 站点范围的页面布局和导航方案。 本教程介绍如何在可以轻松地进行更新的所有页面之间创建一致的外观。


## <a name="introduction"></a>介绍

用户友好的一个常见特性是网站的它们具有一致的、 站点范围的页面布局和导航方案。 ASP.NET 2.0 引入了两项新功能，可以大大简化实现了站点范围的页面布局和导航方案： 母版页和站点导航。 母版页使开发人员可以创建具有指定的可编辑区域的网站的模板。 然后，此模板都可以应用于站点中的 ASP.NET 页面。 为母版页指定的可编辑区域，此类的 ASP.NET 页面只需要提供内容使用的主页面的所有 ASP.NET 页面都是相同的母版页中的所有其他标记。 此模型允许开发人员定义和集中管理的站点级页面布局，从而使其更轻松地跨所有页面，可以轻松地更新创建一致的外观。

[站点导航系统](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)提供的两个页面开发人员定义站点地图的机制和该站点图的 API 以编程方式查询。 新导航 Web 控件的菜单、 树视图和 SiteMapPath 可以轻松快速地呈现全部或部分常见的导航用户界面元素中的站点映射。 我们将使用默认站点的导航提供程序，这意味着，将在 XML 格式文件中定义我们的站点映射。

若要说明这些概念，并让我们教程的网站更易于使用，让我们花本课程中定义的站点级页面布局、 实现站点地图，并将添加的导航用户界面。 本教程结束时，我们将用于构建我们教程的 web 页面的精美的网站设计。


[![本教程的最终结果](master-pages-and-site-navigation-vb/_static/image2.png)](master-pages-and-site-navigation-vb/_static/image1.png)

**图 1**: 最终结果的本教程 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image3.png))


## <a name="step-1-creating-the-master-page"></a>步骤 1： 创建主页面

第一步是创建站点的主页面。 现在，我们的网站包含仅将类型化数据集 (`Northwind.xsd`，请在`App_Code`文件夹)，BLL 类 (`ProductsBLL.vb`， `CategoriesBLL.vb`，依此类推，在所有`App_Code`文件夹)，数据库 (`NORTHWND.MDF`，在`App_Data`文件夹中），配置文件 (`Web.config`)，和 CSS 样式表文件 (`Styles.css`)。 我清除了这些页和文件演示由于我们将在将来的教程中重新中更详细地介绍这些示例使用前两个教程的 DAL 和 BLL。


![在我们的项目文件](master-pages-and-site-navigation-vb/_static/image4.png)

**图 2**： 我们的项目中的文件


若要创建主页面，请右键单击解决方案资源管理器中的项目名称并选择添加新项。 然后从模板列表中选择母版页类型并将其命名`Site.master`。


[![向网站添加新的主页面](master-pages-and-site-navigation-vb/_static/image6.png)](master-pages-and-site-navigation-vb/_static/image5.png)

**图 3**： 将新的主页面添加到网站 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image7.png))


在母版页中定义站点级页面布局。 可以使用设计视图并添加所需的任何布局或 Web 控件也可以手动在源视图中手动添加标记。 我使用我的母版页[级联样式表](http://www.w3schools.com/css/default.asp)定位和外部文件中定义的 CSS 设置样式`Style.css`。 但您不能从标记如下所示，定义的 CSS 规则，以便导航`<div>`的内容绝对定位，以便它显示在左侧，并且具有固定的宽度为 200 像素。

Site.master


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample1.aspx)]

母版页定义静态页面布局和使用的主页面的 ASP.NET 页可以编辑的区域。 这些内容的可编辑区域所指示的 ContentPlaceHolder 控件，可以在内容中看到该`<div>`。 我们的主页面具有单个 ContentPlaceHolder (`MainContent`)，但主该页可能具有多个 Contentplaceholder。

与上面输入的标记，切换到设计视图显示了主页面的布局。 使用此母版页任何 ASP.NET 页面将具有指定的标记的功能具有此统一布局`MainContent`区域。


[![Master 页上，通过设计视图查看](master-pages-and-site-navigation-vb/_static/image9.png)](master-pages-and-site-navigation-vb/_static/image8.png)

**图 4**： 在母版页，当查看通过设计视图 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image10.png))


## <a name="step-2-adding-a-homepage-to-the-website"></a>步骤 2： 添加到网站主页

与定义母版页，我们已经准备好添加网站的 ASP.NET 页。 让我们首先添加`Default.aspx`，我们网站的主页。 右键单击解决方案资源管理器中的项目名称并选择添加新项。 选择从模板列表和名称的 Web 窗体选项文件`Default.aspx`。 此外，选中"选择母版页"复选框。


[![添加新的 Web 窗体，检查选择母版页复选框](master-pages-and-site-navigation-vb/_static/image12.png)](master-pages-and-site-navigation-vb/_static/image11.png)

**图 5**： 添加新的 Web 窗体，检查选择母版页复选框 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image13.png))


单击确定按钮后，我们会要求选择这个新的 ASP.NET 页面应使用哪个主页面。 虽然可以在项目中有多个母版页，我们只能有一个。


[![选择应使用此 ASP.NET 页面的母版页](master-pages-and-site-navigation-vb/_static/image15.png)](master-pages-and-site-navigation-vb/_static/image14.png)

**图 6**： 选择此 ASP.NET 页应使用的母版页 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image16.png))


母版页后，新的 ASP.NET 页面将包含以下标记：

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample2.aspx)]

在中`@Page`指令有是对使用的母版页文件的引用 (`MasterPageFile="~/Site.master"`)，且 ASP.NET 页面的标记包含内容控件的每个 ContentPlaceHolder 控件在母版页，与该控件中定义`ContentPlaceHolderID`特定 ContentPlaceHolder 映射内容控件。 内容控件是所在的位置标记您想要显示在相应 ContentPlaceHolder。 设置`@Page`指令的`Title`属性到主页，并将一些受到欢迎内容添加到内容控件：

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample3.aspx)]

`Title`中的属性`@Page`指令可用于设置页面的标题从 ASP.NET 页上，即使`<title>`母版页中定义元素。 我们还可以设置标题，以编程方式使用`Page.Title`。 另请注意，对样式表的母版页的引用 (如`Style.css`) 会自动更新，使它们在任何 ASP.NET 页中，而无论 ASP.NET 页面相对于主页面是在哪些目录如何工作。

切换到我们可以看到我们的页面在浏览器中查看呈现的设计视图。 请注意，在设计中的内容可编辑区域是可编辑的 ASP.NET 页查看在母版页中定义的非 ContentPlaceHolder 标记灰显。


[![在 ASP.NET 页的设计视图显示了这两个可编辑的和非可编辑区域](master-pages-and-site-navigation-vb/_static/image18.png)](master-pages-and-site-navigation-vb/_static/image17.png)

**图 7**： 为 ASP.NET 页显示了两个可编辑的设计视图和非可编辑区域 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image19.png))


当`Default.aspx`访问页面时浏览器、 ASP.NET 引擎会自动将页面的母版页内容和 ASP。NET 的内容，并将合并的内容呈现到最后一个向下发送到请求的浏览器的 HTML。 当更新母版页的内容时，所有使用此母版页的 ASP.NET 页面将具有其重新合并了新的主页面内容请求下一次其内容。 简单地说，主页面模型允许单个页布局模板可定义 （master 页） 的更改将立即反映在整个网站。

## <a name="adding-additional-aspnet-pages-to-the-website"></a>向网站添加其他 ASP.NET 页面

让我们看一段时间来将其他 ASP.NET 页存根 （stub） 添加到最终将包含各种报告演示站点。 将有多个不是 35 演示总的来说，因此让我们创建的所有存根 （stub） 页面，而是只是创建的第几个。 此外将演示的许多类别，因为若要更好地管理演示添加类别的文件夹。 现在添加以下三个文件夹：

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

最后，添加新文件，如图 8 中的解决方案资源管理器中所示。 添加每个文件时，务必选中"选择母版页"复选框。


![添加以下文件](master-pages-and-site-navigation-vb/_static/image20.png)

**图 8**： 添加以下文件


## <a name="step-2-creating-a-site-map"></a>步骤 2： 创建站点图

管理组成大量页面的详细信息的网站的挑战之一提供一种简单方式为该站点中导航的访问者。 开始时，必须定义站点的导航结构。 接下来，此结构必须转换为可导航用户界面元素，如菜单或痕迹导航。 最后，整个过程需要需要维护和更新，因为新页添加到的站点，并删除现有的。 ASP.NET 2.0 中，开发人员之前在自己的用于创建站点的导航结构，维护它，并将其转换为可导航用户界面元素。 使用 ASP.NET 2.0 中，但是，开发人员可以利用非常灵活的站点导航系统中生成。

ASP.NET 2.0 站点导航系统提供一种开发人员定义站点图，然后通过编程 API 来访问此信息。 ASP.NET 附带的站点映射提供程序需要以特定方式设置格式的 XML 文件中存储的站点映射数据。 但由于站点导航系统基于[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)可以扩展以支持用于序列化的站点映射信息的替代方法。 Jeff Prosise 的文章[SQL 站点映射提供程序您期待已等待 For](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)显示了如何创建站点地图提供程序，将站点图存储在 SQL Server 数据库; 另一个选项是创建[站点地图提供程序基于文件系统结构](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)。

对于本教程中，但是，我们使用默认站点映射提供程序提供使用 ASP.NET 2.0。 若要创建的站点映射，只需右键单击解决方案资源管理器中的项目名称，选择添加新项，并选择站点映射选项。 保留的名称作为`Web.sitemap`并单击添加按钮。


[![将站点图添加到你的项目](master-pages-and-site-navigation-vb/_static/image22.png)](master-pages-and-site-navigation-vb/_static/image21.png)

**图 9**： 将站点图添加到你的项目 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image23.png))


站点地图文件是一个 XML 文件。 请注意，Visual Studio 提供了 IntelliSense 站点地图结构。 站点地图文件必须具有`<siteMap>`节点作为其根节点，必须包含一个精确`<siteMapNode>`子元素。 该第一个`<siteMapNode>`元素然后可以包含任意数目的后代`<siteMapNode>`元素。

定义要模拟的文件系统结构的站点映射。 也就是说，添加`<siteMapNode>`的每个三个文件夹和子元素`<siteMapNode>`这些文件夹中的 ASP.NET 页面的每个元素如下所示：

Web.sitemap


[!code-xml[Main](master-pages-and-site-navigation-vb/samples/sample4.xml)]

站点图定义网站的导航结构，它是描述该站点的各个部分的层次结构。 每个`<siteMapNode>`中的元素`Web.sitemap`表示站点的导航结构中的节。


[![站点图表示的分层导航结构](master-pages-and-site-navigation-vb/_static/image25.png)](master-pages-and-site-navigation-vb/_static/image24.png)

**图 10**： 站点图表示的分层导航结构 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image26.png))


ASP.NET 公开站点图的结构通过.NET Framework [SiteMap 类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)。 此类具有`CurrentNode`属性，它返回有关的信息部分用户当前访问;`RootNode`属性返回站点地图的根 （本组织，我们的站点映射中）。 同时`CurrentNode`并`RootNode`属性返回[SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)实例，将属性等`ParentNode`， `ChildNodes`， `NextSibling`， `PreviousSibling`，依此类推，它们允许站点图要遍历的层次结构。

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>步骤 3： 显示菜单的站点映射

访问 ASP.NET 2.0 中的数据可以是以编程方式来实现，例如在 ASP.NET 1.x 中，或以声明方式，通过新[数据源控件](https://msdn.microsoft.com/library/ms227679.aspx)。 有几个内置数据源控件，如 SqlDataSource 控件访问关系数据库的数据，ObjectDataSource 控件，从类和其他人访问数据。 您甚至可以创建您自己[自定义数据源控件](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)。

数据源控件充当您的 ASP.NET 页面和基础数据之间的代理。 为了显示一个数据源控件检索到的数据，我们通常将向页面添加另一个 Web 控件，并将其绑定到数据源控件。 若要将 Web 控件绑定到数据源控件，只需设置 Web 控件的`DataSourceID`属性的值的数据源控件`ID`属性。

为了帮助进行处理的站点映射的数据，ASP.NET 包括 SiteMapDataSource 控件，使我们可以将针对我们的网站的站点映射 Web 控件绑定。 两个 Web 控件的树视图和菜单通常用于提供导航用户界面。 若要将站点地图数据绑定到这两个控件之一，只需将 SiteMapDataSource 添加到该页面和 TreeView 或菜单控件`DataSourceID`相应地设置属性。 例如，我们可以将菜单控件添加到母版页使用以下标记：


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample5.aspx)]

对于更精细的控制 HTML，我们可以将 SiteMapDataSource 控件绑定到 Repeater 控件中，如下所示：


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample6.aspx)]

SiteMapDataSource 控件返回的站点映射层次结构一个级别时，从根站点地图节点 （本组织，我们的站点映射中），然后将下一个级别 （基本报告、 筛选报表和自定义格式设置），依次类推。 当绑定到 Repeater SiteMapDataSource，它枚举第一个级别返回并实例化`ItemTemplate`为每个`SiteMapNode`第一个级别中的实例。 若要访问的特定属性`SiteMapNode`，我们可以使用`Eval(propertyName)`，这是我们如何获取每个`SiteMapNode`的`Url`和`Title`超链接控件的属性。

上面的 Repeater 示例将呈现以下标记：


[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample7.html)]

（基本报告、 筛选报表和自定义格式设置） 这些站点站点地图节点构成*第二个*级别所呈现的第一个不的站点映射。 这是因为 SiteMapDataSource`ShowStartingNode`属性设置为 False，从而导致 SiteMapDataSource 绕过站点地图根节点并改为通过站点映射层次结构中返回的第二个级别开始。

基本报告、 筛选报表和自定义格式设置为显示子级`SiteMapNode`s，我们可以将另一个转发器添加到初始 Repeater `ItemTemplate`。 此第二个 Repeater 将绑定到`SiteMapNode`实例的`ChildNodes`属性，如下所示：


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample8.aspx)]

这些两个重复字符会导致以下标记 （一些标记已删除为简便起见）：


[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample9.html)]

使用 CSS 样式选择从[Rachel Andrew](http://www.rachelandrew.co.uk/)的预订[CSS Anthology: 101 的基本提示、 技巧&amp;Hacks](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance)，则`<ul>`和`<li>`样式元素，以便标记将生成以下可视化输出：


![由两个重复字符和某些 CSS 组合成一个菜单](master-pages-and-site-navigation-vb/_static/image27.png)

**图 11**： 由两个重复字符和某些 CSS 组合成一个菜单


此菜单在母版页和绑定到在中定义了站点地图`Web.sitemap`，这意味着对站点图的任何更改将立即反映在所有页使用`Site.master`母版页。

## <a name="disabling-viewstate"></a>禁用视图状态

所有 ASP.NET 控件可以根据需要都保留其状态的[视图状态](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)，这序列化为中呈现的 HTML 隐藏的窗体字段。 视图状态用于由控件回发之间保留它们以编程方式更改的状态如数据绑定到数据 Web 控件。 尽管视图状态允许在回发之间要记住的信息，它会增加必须发送到客户端可能会导致严重的页膨胀，如果不，加以密切监视的标记的大小。 数据 Web 控件特别是标记的 GridView 是标记的特别让人诟病向页面添加数十个额外千字节为单位。 尽管这种增加可能是宽带或 intranet 用户可以忽略不计，视图状态可以添加拨号用户在往返行程数秒钟的时间。

若要查看视图状态、 访问页，可在浏览器中，然后查看发送的网页上的源的影响 （在 Internet Explorer 中，转到视图菜单并选择源选项）。 你还可以启用[页上跟踪](https://msdn.microsoft.com/library/sfbfw58f.aspx)若要查看使用的每个页面上的控件的视图状态分配。 在名为的隐藏窗体字段中的视图状态信息序列化`__VIEWSTATE`，它位于`<div>`紧跟左括号之后元素`<form>`标记。 Web 窗体的使用情况; 时，仅保存视图状态如果您的 ASP.NET 页面不包含`<form runat="server">`也不会有其声明性语法中`__VIEWSTATE`隐藏窗体中呈现的标记的字段。

`__VIEWSTATE`由主页面生成的窗体字段将约 1,800 个字节添加到页面的生成的标记。 此额外膨胀主要是由于 Repeater 控件，如 SiteMapDataSource 控件的内容在持久保存到视图状态。 虽然额外的 1800 字节起来可能不需要进行很多令人兴奋，具有许多字段和记录使用 GridView 时，视图状态可以轻松地提升到原来的 10 或更多。

可以通过设置页面或控件级别禁用视图状态`EnableViewState`属性设置为`False`，从而减少呈现的标记的大小。 数据 Web 控件仍然存在跨回发绑定到数据 Web 控件的数据的视图状态，因为时禁用视图状态数据 Web 控件数据必须绑定每个回发。 在 ASP.NET 版本 1.x 得归功于页面开发人员; 此职责灵感来源使用 ASP.NET 2.0 中，但是，数据 Web 控件将重新绑定到其数据源控件在每个回发时根据需要。

若要让我们来减少页面的视图状态将设置 Repeater 控件的`EnableViewState`属性设置为`False`。 这可以通过在设计器中或以声明方式在源视图中的属性窗口来完成。 进行此更改后 Repeater 的声明性标记应如下所示：


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample10.aspx)]

此更改后，页面的呈现的视图状态大小收缩到仅仅后 52 个字节，节省 97%在视图状态大小 ！ 在本系列教程中我们将禁用默认情况下的数据 Web 控件的视图状态，以减少呈现的标记的大小。 在示例的大多数`EnableViewState`属性将设置为`False`并没有规定执行此操作。 唯一一次将讨论状态的视图是在其中必须在数据中启用它的情况下 Web 控制以提供其预期的功能。

## <a name="step-4-adding-breadcrumb-navigation"></a>步骤 4： 添加痕迹导航

若要完成主页面，让我们痕迹导航 UI 元素添加到每个页面。 痕迹导航快速向用户显示其站点层次结构中的当前位置。 添加痕迹导航栏中 ASP.NET 2.0 只轻松将 SiteMapPath 控件添加到页;不需要任何代码。

对于我们的站点，将此控件添加到标头`<div>`:


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample11.aspx)]

痕迹导航显示当前页用户时所访问的站点映射层次结构，以及站点地图节点的"上级"该站点中一直到根目录 （本组织，我们的站点映射中）。


![痕迹导航显示当前页和其站点中的上级映射层次结构](master-pages-and-site-navigation-vb/_static/image28.png)

**图 12**： 痕迹导航显示当前页和其站点中的上级映射层次结构


## <a name="step-5-adding-the-default-page-for-each-section"></a>步骤 5： 添加每个部分的默认页

我们的站点中的教程分为不同的类别基本报告筛选、 自定义格式设置，使用文件夹中的每个类别并为该文件夹中的 ASP.NET 页面的相应教程，等等。 此外，每个文件夹包含`Default.aspx`页。 此默认页面，让我们来显示所有当前部分的教程。 也就是说，对于`Default.aspx`中`BasicReporting`文件夹，我们将提供的链接`SimpleDisplay.aspx`， `DeclarativeParams.aspx`，和`ProgrammaticParams.aspx`。 我们在这里，可以使用再次`SiteMap`中定义的类和数据 Web 控件要显示此信息基于站点图`Web.sitemap`。

让我们来显示同样，但这次我们将显示的标题和说明的教程使用 Repeater 的未排序的列表。 由于标记和代码来完成此将需要为每个重复`Default.aspx`页上，我们可以封装在此 UI 逻辑[用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)。 名为的网站中创建一个文件夹`UserControls`并将类型名为 Web 用户控件的新项添加到该`SectionLevelTutorialListing.ascx`，并添加以下标记：


[![将新的 Web 用户控件添加到用户控件文件夹](master-pages-and-site-navigation-vb/_static/image30.png)](master-pages-and-site-navigation-vb/_static/image29.png)

**图 13**： 添加到新的 Web 用户控件`UserControls`文件夹 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image31.png))


SectionLevelTutorialListing.ascx


[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.vb


[!code-vb[Main](master-pages-and-site-navigation-vb/samples/sample13.vb)]

在 Repeater 上例中，我们绑定`SiteMap`Repeater 的数据以声明方式;`SectionLevelTutorialListing`用户控件，但是，会以编程方式。 在`Page_Load`事件处理程序，则进行检查以确保此页 URL 映射到站点图中的节点的 s。 如果在不具有相应的页面中使用此用户控件`<siteMapNode>`条目，`SiteMap.CurrentNode`将返回`Nothing`和任何数据将会绑定到 Repeater。 假设我们有`CurrentNode`，我们将绑定其`ChildNodes`Repeater 的集合。 由于我们站点地图设置以便`Default.aspx`每个部分中的页的父节点的所有内该部分的教程，此代码将显示的所有部分的教程到链接和说明，如以下屏幕截图中所示。

一旦创建此 Repeater 后，打开`Default.aspx`页中的每个文件夹，请转到设计视图中，并只需将用户控件拖动到设计图面上的解决方案资源管理器从想要显示的教程列表。


[![用户控件具有已添加到 Default.aspx](master-pages-and-site-navigation-vb/_static/image33.png)](master-pages-and-site-navigation-vb/_static/image32.png)

**图 14**: 用户控件具有已添加到`Default.aspx`([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image34.png))


[![列出基本 Reporting 教程](master-pages-and-site-navigation-vb/_static/image36.png)](master-pages-and-site-navigation-vb/_static/image35.png)

**图 15**： 列出基本 Reporting 教程 ([单击以查看实际尺寸的图像](master-pages-and-site-navigation-vb/_static/image37.png))


## <a name="summary"></a>总结

与定义了站点地图并完成了母版页，我们就具有了一致的页面布局和导航方案与数据相关的教程。 我们将添加到我们的站点的多少页，无论更新站点级页面布局或站点导航信息是由于此信息在集中式快速而简单的过程。 具体而言，在母版页中定义的页面布局信息`Site.master`和站点中的映射`Web.sitemap`。 我们不需要编写*任何*代码来实现此站点级页面布局和导航机制，并将保留在 Visual Studio 中的完整所见即所得设计器支持。

已完成的数据访问层和业务逻辑层和具有定义一个一致的页面布局和站点导航，我们已准备好开始浏览报告的常见模式。 在接下来三个教程中我们将介绍基本报表的任务显示从 GridView、 DetailsView 和 FormView 控件在 BLL 中检索到的数据。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 主机页面概述](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [在 ASP.NET 2.0 母版页](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 设计模板](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 站点导航概述](https://msdn.microsoft.com/library/e468hxky.aspx)
- [检查 ASP.NET 2.0 的 Site navigation — 站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 网站导航功能](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [了解 ASP.NET 视图状态](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [如何： 启用 ASP.NET 页跟踪](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Liz Shulok、 Dennis Patterson 和 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](creating-a-business-logic-layer-vb.md)
