---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: 母版页 (C#) 中指定的标题、 元标记和其他 HTML 标头 |Microsoft Docs
author: rick-anderson
description: 在不同的技术来定义各种类型的看起来&lt;head&gt;主页面从内容页中的元素。
ms.author: aspnetcontent
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 773d8aee55a3e685c9759f9a9e0b571564f8cd31
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841006"
---
<a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>母版页 (C#) 中指定的标题、 元标记和其他 HTML 标头
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> 在不同的技术来定义各种类型的看起来&lt;head&gt;主页面从内容页中的元素。


## <a name="introduction"></a>介绍

在 Visual Studio 2008 中创建新的主页面有，默认情况下，两个 ContentPlaceHolder 控件： 一个名为 head，并且位于`<head>`元素; 和一个名为`ContentPlaceHolder1`、 Web 窗体中放置。 用途`ContentPlaceHolder1`是可以按页基础自定义 Web 窗体中定义一个区域。 `head` ContentPlaceHolder 启用要添加到自定义内容页`<head>`部分。 （当然，可以修改或删除，这些两个 Contentplaceholder 和其他 ContentPlaceHolder 可能添加到母版页。 我们的主页面， `Site.master`，当前具有四个 ContentPlaceHolder 控件。)

HTML`<head>`元素充当有关不是文档本身的一部分的 web 页文档信息的存储库。 这包括诸如 web 页面的标题等，由搜索引擎或内部爬网程序和指向外部资源，如 RSS 源、 JavaScript 和 CSS 文件元数据信息。 其中一些信息可能相关网站中的所有页面。 例如，你可能想要全局导入相同的 CSS 规则和每个 ASP.NET 页面的 JavaScript 文件。 但是，有的某些部分`<head>`是特定于页面的元素。 页面标题是一个典型示例。

在本教程中，我们将说明如何定义全局和特定于页面的`<head>`部分标记在母版页并在其内容页面中。

## <a name="examining-the-master-pagesheadsection"></a>检查母版页`<head>`部分

由 Visual Studio 2008 创建的默认主控页文件包含中的以下标记其`<head>`部分：


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

请注意，`<head>`元素包含`runat="server"`属性，指示它是服务器控件 （而非静态 HTML）。 所有 ASP.NET 页面都派生[`Page`类](https://msdn.microsoft.com/library/system.web.ui.page.aspx)，位于`System.Web.UI`命名空间。 此类包含`Header`属性，可提供对页面的访问`<head>`区域。 使用[`Header`属性](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx)我们可以设置 ASP.NET 页面的标题，或将其他标记添加到呈现`<head>`部分。 它是有可能，然后，自定义内容页面的`<head>`通过在页面的中编写的代码元素`Page_Load`事件处理程序。 我们介绍如何以编程方式在步骤 1 中设置页面的标题。

中的标记`<head>`上述元素还包括一个名为 head 的 ContentPlaceHolder 控件。 此 ContentPlaceHolder 控件不是有必要，因为内容页可以添加到自定义内容`<head>`元素以编程方式。 它非常有用，但是，在内容页面需要静态将标记添加到的情况下`<head>`到相应的内容控件而不是以编程方式可以以声明方式添加元素作为静态标记。

除了`<title>`元素和 head ContentPlaceHolder，主页面的`<head>`元素应包含任何`<head>`-级别普遍适用于所有页面的标记。 在我们的网站，所有页面都使用中定义的 CSS 规则`Styles.css`文件。 因此，我们更新`<head>`中的元素[*使用母版页创建站点范围内布局*](creating-a-site-wide-layout-using-master-pages-cs.md)教程，包括相应`<link>`元素。 我们`Site.master`母版页的当前`<head>`标记如下所示。


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>步骤 1： 设置内容页面的标题

通过指定 web 页面的标题`<title>`元素。 请务必设置为适当的值的每个页面的标题。 当访问一个页面，其标题将显示在浏览器的标题栏。 此外，当将一个页面加为书签，浏览器使用页面的标题为书签的建议名称。 此外，许多搜索引擎时显示搜索结果显示页面的标题。

> [!NOTE]
> 默认情况下，Visual Studio 设置`<title>`"无标题页"到母版页中的元素。 同样，新的 ASP.NET 页面具有其`<title>`太设置为"无标题页"。 因为它很容易忘记设置为适当的值的页面的标题，许多页面上有了标题为"无标题页"Internet。 Web 页面和此标题搜索 Google 不会返回大致 2,460,000 结果。 即使是 Microsoft 也容易受到了标题为"无标题页"发布 web 页。 在撰写本文时，Google 搜索报告 Microsoft.com 域中的 236 此类网页。


ASP.NET 页可以指定其标题中的以下方法之一：

- 通过将值直接内的放置`<title>`元素
- 使用`Title`属性中`<%@ Page %>`指令
- 以编程方式设置页面的`Title`属性使用如下代码`Page.Title="title"`或`Page.Header.Title="title"`。

内容页没有`<title>`母版页中定义元素，因为它。 因此，若要设置内容页面的标题可以使用`<%@ Page %>`指令的`Title`属性，或以编程方式设置。

### <a name="setting-the-pages-title-declaratively"></a>以声明方式设置页面的标题

可以以声明方式通过设置内容页面的标题`Title`的属性[`<%@ Page %>`指令](https://msdn.microsoft.com/library/ydy4x04a.aspx)。 此属性可以设置通过直接修改`<%@ Page %>`指令或通过属性窗口。 让我们看看这两种方法。

从源视图中，找到`<%@ Page %>`指令，这是在页面的声明性标记的顶部。 `<%@ Page %>`指令`Default.aspx`后面：


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

`<%@ Page %>`指令指定使用 ASP.NET 引擎分析和编译页面时的特定于页面的属性。 这包括其主控页文件、 其代码文件和其标题，以及其他信息的位置。

默认情况下，创建 Visual Studio 将设置新的内容页时`Title`无标题页的属性。 更改`Default.aspx`的`Title`属性从"无标题页"到"主页面教程"，然后查看通过浏览器页面。 图 1 显示了浏览器的标题栏中，这反映了新的页面标题。


![浏览器的标题栏现在显示&quot;Master 页教程&quot;而不是&quot;无标题的页&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**图 01**： 浏览器的标题栏现在显示而不是"无标题页"的"主页面教程"


此外可以从属性窗口设置页面的标题。 从属性窗口中，文档从列表中选择下拉列表到负载页级别的属性，其中包括`Title`属性。 图 2 显示了属性窗口后的`Title`已设置为"主页面教程"。


![可以将标题从属性窗口中，配置过](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**图 02**： 可能过配置从属性窗口的标题


### <a name="setting-the-pages-title-programmatically"></a>以编程方式设置页面的标题

母版页`<head runat="server">`标记转换成[`HtmlHead`类](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx)实例时由 ASP.NET 引擎呈现页面。 `HtmlHead`类具有[`Title`属性](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx)其值将反映在呈现`<title>`元素。 此属性是可从 ASP.NET 页的代码隐藏类通过访问`Page.Header.Title`; 这同样也可以通过访问属性`Page.Title`。

若要练习以编程方式设置页面的标题，请导航到`About.aspx`页面的代码隐藏类，并创建事件处理程序的页面的`Load`事件。 接下来，设置页面的标题为"主页面教程:: 有关::*日期*"，其中*日期*为当前日期。 添加此代码后您`Page_Load`事件处理程序应看起来如下所示：


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

图 3 显示了浏览器的标题栏，访问时`About.aspx`页。


![页面的标题是以编程方式设置，包括当前日期](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**图 03**: 页面的标题是以编程方式设置，包括当前日期


## <a name="step-2-automatically-assigning-a-page-title"></a>步骤 2： 自动分配页标题

正如我们看到在步骤 1 中，可以以声明方式或以编程方式设置页面的标题。 如果你忘记了显式更改为更具描述性标题，但是，在页将提供的默认标题，"无标题页"。 理想情况下，页面的标题会自动被设置为我们的事件中我们未显式指定其值。 例如，如果在运行时页面的标题为"无标题页"，我们可能想要自动更新，使 ASP.NET 页面的文件名相同的标题。 好消息是，使用少量的前期工作，就可以具有自动分配的标题。

所有 ASP.NET web 页面都派生`Page`类中`System.Web.UI`命名空间。 `Page`类定义由 ASP.NET 页面所需的最小功能，并公开基本属性，如`IsPostBack`， `IsValid`， `Request`，和`Response`，此外还有许多其他。 通常，web 应用程序中的每一页需要其他功能。 提供这一常见方法是创建自定义基本页类。 自定义基本页类是派生的类创建`Page`类，并包括附加功能。 一旦创建此基类的类后，你可以从其派生的 ASP.NET 页面 (而不是`Page`类)，从而提供对 ASP.NET 页面的扩展的功能。

在此步骤中我们创建一个基本页面，如果标题不否则已显式设置将自动设置到 ASP.NET 页面的文件名的页面的标题。 步骤 3 介绍设置的站点映射的页面的标题。

> [!NOTE]
> 创建和使用自定义基本页类的全面介绍不在本系列教程的范围。 有关详细信息，请阅读[将自定义基本类用于在 ASP.NET 页的代码隐藏类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)。


### <a name="creating-the-base-page-class"></a>创建基础 Page 类

我们的第一个任务是创建基本页类，这是一个类以扩展`Page`类。 首先，通过添加`App_Code`右键单击解决方案资源管理器中的项目名称，选择添加 ASP.NET 文件夹，然后选择你的项目的文件夹`App_Code`。 接下来，右键单击`App_Code`文件夹，并添加一个名为的新类`BasePage.cs`。 图 4 显示了在解决方案资源管理器后`App_Code`文件夹和`BasePage.cs`类已添加。


![添加 App_Code 文件夹和一个名为 BasePage 类](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**图 04**： 添加`App_Code`文件夹和名为的类 `BasePage`


> [!NOTE]
> Visual Studio 支持的项目管理的两种模式： 网站项目和 Web 应用程序项目。 `App_Code`文件夹旨在与网站项目模型一起使用。 如果使用的 Web 应用程序项目模型，将放`BasePage.cs`不是命名为类似的文件夹中的类`App_Code`，如`Classes`。 有关本主题的详细信息，请参阅[迁移到 Web 应用程序项目的 Web 站点项目](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)。


由于自定义基本页用作 ASP.NET 页的代码隐藏类的基类，它需要扩展`Page`类。


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

每当请求 ASP.NET 页时将继续通过一系列的阶段，通过在请求的页面呈现到 HTML 中。 我们可以通过重写到该阶段点击`Page`类的`OnEvent`方法。 让我们为我们的群页自动设置标题 （如果它尚未显式指定的`LoadComplete`阶段 (其中之后, 您可能已经猜到，发生`Load`阶段)。

若要完成此操作，重写`OnLoadComplete`方法，并输入以下代码：


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

`OnLoadComplete`方法首先会确定如果`Title`尚未已显式设置属性。 如果`Title`属性是`null`，空字符串，或具有"无标题页"的值分配给请求的 ASP.NET 页的文件名。 请求的 ASP.NET 页面-的物理路径`C:\MySites\Tutorial03\Login.aspx`，例如-是可通过访问`Request.PhysicalPath`属性。 `Path.GetFileNameWithoutExtension`方法用于拉出只是文件名的部分，并且此文件名然后分配到`Page.Title`属性。

> [!NOTE]
> 我邀请您来增强此逻辑，用于改进标题的格式。 例如，如果页面的文件名为`Company-Products.aspx`，上面的代码将生成标题"公司的产品"，但理想情况下短划线将替换为一个空格，如"公司产品"中所示。 此外，请考虑大小写更改时添加一个空格。 也就是说，请考虑添加代码，通过转换文件名`OurBusinessHours.aspx`标题的"我们营业时间"。


### <a name="having-the-content-pages-inherit-the-base-page-class"></a>具有继承的基类的页的内容页

现在，我们需要更新我们网站派生自定义基本页中的 ASP.NET 页面 (`BasePage`) 而不是`Page`类。 若要完成此，请转到每个代码隐藏类并将更改从类声明：


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

到:


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

这样做之后，请访问通过浏览器的站点。 如果您访问的页，其标题显式设置，如`Default.aspx`或`About.aspx`，使用显式指定的标题。 如果，但是，在访问其标题未更改默认值 （"无标题页"） 从一个页面，基本页类将设置到页面的文件名的标题。

图 5 显示了`MultipleContentPlaceHolders.aspx`页面的浏览器查看时。 请注意，标题是精确的页的文件名 （不太扩展名），"MultipleContentPlaceHolders"。


[![如果未显式指定一个标题，该页面的文件名是自动使用](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**图 05**： 如果未显式指定一个标题，该页面的文件名是自动使用 ([单击以查看实际尺寸的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png))


## <a name="step-3-basing-the-page-title-on-the-site-map"></a>步骤 3： 将页标题基于站点图

ASP.NET 还提供了一个强大的网站映射框架，允许页面开发人员在外部资源 （如 XML 文件或数据库表） 以及 Web 控件，用于显示信息 （如 SiteMapPath 站点地图中定义分层的站点地图菜单中和 TreeView 控件）。

此外可以从 ASP.NET 页的代码隐藏类以编程方式访问站点地图结构。 以这种方式我们自动在站点地图中设置到其相应的节点的标题的页面的标题。 让我们来改进`BasePage`，以便提供此功能在步骤 2 中创建的类。 但首先我们需要创建我们的站点的站点映射。

> [!NOTE]
> 本教程假设读者已经非常熟悉使用 ASP。NET 的站点映射功能。 使用站点图的详细信息，请查阅我的多个部分的文章系列，[检查 ASP。NET 的站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)。


### <a name="creating-the-site-map"></a>创建站点图

站点映射系统构建之上[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)，其中将站点图 API 从序列化内存和持久存储区之间的站点映射信息的逻辑中分离出来。 .NET Framework 附带[`XmlSiteMapProvider`类](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)，这是默认站点地图提供程序。 正如其名，`XmlSiteMapProvider`使用 XML 文件作为其站点映射存储。 让我们使用此提供程序来定义我们的站点映射。

首先，创建名为的网站的根文件夹中的站点地图文件`Web.sitemap`。 若要完成此操作，右键单击解决方案资源管理器中的网站名称，选择添加新项，然后选择站点图模板。 请确保该文件命名`Web.sitemap`并单击添加。


[![添加一个名为网站的根文件夹的 Web.sitemap 文件](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**图 06**： 添加名为文件`Web.sitemap`网站的根文件夹 ([单击以查看实际尺寸的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png))


添加以下 XML 到`Web.sitemap`文件：


[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

此 XML 定义分层站点地图结构图 7 所示。


![站点图是当前组成的三个站点地图节点](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**图 07**: 站点图是当前组成的三个站点地图节点


我们添加新示例，我们将在将来的教程中更新站点地图结构。

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>更新 Master 页以包含导航 Web 控件

现在，我们已定义的站点图，让我们更新母版页，若要包括导航 Web 控件。 具体而言，让我们向 ListView 控件中呈现在站点地图中定义的每个节点一个列表项的未排序的列表的课程部分左边的列。

> [!NOTE]
> ListView 控件是刚刚接触 ASP.NET 3.5 版。 如果使用的 ASP.NET 的早期版本，请改为使用 Repeater 控件。 ListView 控件的详细信息，请参阅[使用 ASP.NET 3.5 ListView 和 DataPager 控件](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)。


首先，从课程部分中删除现有的未排序的列表标记。 接下来，从工具箱拖动 ListView 控件并将其下方课程标题。 ListView 将位于工具箱中，与其他视图控件的数据部分： GridView、 DetailsView 和 FormView。 将 ListView 的 ID 属性设置为`LessonsList`。

从数据源配置向导选择要绑定到名为的新 SiteMapDataSource 控件的 ListView `LessonsDataSource`。 SiteMapDataSource 控件从站点映射系统返回层次结构。


[![SiteMapDataSource 控件绑定到 LessonsList ListView 控件](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**图 08**： 将绑定到 SiteMapDataSource 控件`LessonsList`ListView 控件 ([单击以查看实际尺寸的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png))


在创建后 SiteMapDataSource 控件，我们需要定义 ListView 的模板，以便它将呈现 SiteMapDataSource 控制返回的每个节点一个列表项的未排序的列表。 可以使用以下模板标记完成此：


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate`生成的未排序列表的标记 (`<ul>...</ul>`) 时`ItemTemplate`呈现为列表项 SiteMapDataSource 所返回每个项 (`<li>`)，其中包含指向特定课程的链接。

在配置后 ListView 的模板，请访问网站。 如图 9 所示，课程部分包含单个项目符号项，主页。 关于和使用多个 ContentPlaceHolder 控件课程在哪里？ SiteMapDataSource 旨在返回一组分层数据，但 ListView 控件可以仅显示单个层次结构的级别。 因此，将显示仅返回 SiteMapDataSource 的站点地图节点的第一个级别。


[![课程部分包含的单个列表项](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**图 09**： 课程部分包含单个列表项 ([单击以查看实际尺寸的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png))


显示多个级别，我们无法嵌套中的多个 Listview `ItemTemplate`。 这种方法在中检查[*母版页和站点导航*教程](../../data-access/introduction/master-pages-and-site-navigation-cs.md)的我[处理数据的系列教程](../../data-access/index.md)。 但是，对于本教程系列中我们站点的地图将包含只需两个级别： 主页 （顶级）;和每个课程为主页的子级。 而不是创建嵌套的 ListView，我们可以改为指示 SiteMapDataSource 使其不返回起始节点通过设置其[`ShowStartingNode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)到`false`。 实际效果是 SiteMapDataSource 首先返回站点地图节点的第二个层。

进行此更改后，ListView 显示关于项目符号项并使用多个 ContentPlaceHolder 控件课程，但忽略针对家庭的项目符号项。 若要解决此问题，我们可以显式添加项目符号项为家庭中`LayoutTemplate`:


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

通过配置 SiteMapDataSource 以忽略此参数起始节点和显式添加主页项目符号项，课程部分现在显示预期的输出。


[![课程部分主页和每个子节点包含项目符号项](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**图 10**： 的课程部分主页和每个子节点包含项目符号项 ([单击以查看实际尺寸的图像](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png))


### <a name="setting-the-title-based-on-the-site-map"></a>设置标题的站点映射

使用就地站点地图，我们可以更新我们`BasePage`类，以使用站点映射中指定的标题。 与我们在步骤 2 中，我们只想要使用站点地图节点的标题，如果页面的标题未显式设置由页面开发人员。 如果所请求的页面没有显式设置页面标题，然后我们会回退到使用请求的页的文件名 （不太扩展名），与我们在步骤 2 中站点图中未找到。 图 11 说明了这一决策。


![如果没有显式设置页面标题，对应的站点地图节点的标题将用作](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**图 11**： 如果没有显式设置页面标题，对应的站点地图节点的标题将用作


更新`BasePage`类的`OnLoadComplete`方法以包括以下代码：


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

与前面一样，`OnLoadComplete`方法开始时确定是否已显式设置页面的标题。 如果`Page.Title`是`null`，为空字符串，则代码会自动分配到的值分配值"无标题页"或`Page.Title`。

若要确定使用的标题，代码将开始通过引用[`SiteMap`类](https://msdn.microsoft.com/library/system.web.sitemap.aspx)的[`CurrentNode`属性](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)。 `CurrentNode` 返回[ `SiteMapNode` ](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx)对应于当前请求页的站点地图中的实例。 假设当前请求的页中站点图中，找到`SiteMapNode`的`Title`属性分配给页面的标题。 如果当前请求的页不在站点地图`CurrentNode`返回`null`和请求的页的文件名用作标题 （如在步骤 2 中完成）。

图 12 显示了`MultipleContentPlaceHolders.aspx`页面的浏览器查看时。 由于未显式设置此页面的标题，则改为使用其对应的站点地图节点的标题。


![从站点地图拉取 MultipleContentPlaceHolders.aspx 页面的标题](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**图 12**:`MultipleContentPlaceHolders.aspx`从站点地图提取页面的标题


## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>步骤 4： 添加到其他特定于页面的标记`<head>`部分

步骤 1、 2 和 3 介绍了自定义`<title>`按页基础上的元素。 除了`<title>`，则`<head>`部分可以包含`<meta>`元素和`<link>`元素。 在本教程前面所述`Site.master`的`<head>`部分包括`<link>`元素`Styles.css`。 因为这`<link>`母版页中定义元素，它包含在`<head>`部分中的所有内容页面。 但我们有关添加`<meta>`和`<link>`按页基础上的元素？

若要添加到特定于页面的内容的最简单方法`<head>`部分是通过 ContentPlaceHolder 控件创建主页面中。 我们已经有了此类 ContentPlaceHolder (名为`head`)。 因此，若要添加自定义`<head>`标记中，创建相应的内容页中的控件并将标记置于其中。

为了说明添加自定义`<head>`标记到页面，让我们来包括`<meta>`向当前集的内容页面的 description 元素。 `<meta>` Description 元素提供了有关 web 页面的简短说明; 大多数搜索引擎将此信息以某种形式合并时显示搜索结果。

一个`<meta>`description 元素具有以下形式：


[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

若要将此标记添加到内容页中，添加到内容控件映射到主页面的 head ContentPlaceHolder 上面的文本。 例如，若要定义`<meta>`的说明元素`Default.aspx`，添加以下标记：


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

由于头 ContentPlaceHolder 不是 HTML 页面的正文中，添加到内容控件的标记不会显示在设计视图中。 若要查看`<meta>`说明元素，请访问`Default.aspx`通过浏览器。 加载页面后，查看源，并请注意，`<head>`部分包括在内容控件中指定的标记。

请花费片刻时间来添加`<meta>`说明元素`About.aspx`， `MultipleContentPlaceHolders.aspx`，和`Login.aspx`。

### <a name="programmatically-adding-markup-to-theheadregion"></a>以编程方式添加到标记`<head>`区域

Head ContentPlaceHolder 使我们能够以声明方式将自定义标记添加到母版页的`<head>`区域。 此外可能以编程方式添加自定义标记。 请记住，`Page`类的`Header`属性将返回`HtmlHead`母版页中定义的实例 ( `<head runat="server">`)。

能够以编程方式将内容添加到`<head>`区域时，要添加的内容是动态的。 可能基于用户访问的页面;也许它是正在从数据库中提取。 无论是什么原因，您可以将内容添加到`HtmlHead`通过将控件添加到自己的控件集合如下所示：


[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

上面的代码将添加`<meta>`keywords 元素到`<head>`区域，提供以逗号分隔的列表，这些关键字描述页。 请注意，若要添加`<meta>`创建的标记[ `HtmlMeta` ](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx)实例，设置其`Name`并`Content`属性，然后将其添加到`Header`的`Controls`集合。 同样，若要以编程方式添加`<link>`元素中，创建[ `HtmlLink` ](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx)对象和设置其属性，然后将其添加到`Header`的`Controls`集合。

> [!NOTE]
> 若要添加任意标记，创建[ `LiteralControl` ](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx)实例，设置其`Text`属性，然后将其添加到`Header`的`Controls`集合。


## <a name="summary"></a>总结

在本教程中我们介绍了各种的方式来添加`<head>`按页按区域标记。 应包括母版页`HtmlHead`实例 (`<head runat="server">`) 使用 ContentPlaceHolder。 `HtmlHead`实例允许以编程方式访问的内容页面`<head>`区域，以声明方式和以编程方式设置页的标题; ContentPlaceHolder 控件启用自定义标记添加到`<head>`以声明方式通过内容控件的部分。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [动态 ASP.NET 中设置页面的标题](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [正在检查 ASP。NET 的 Site navigation — 站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [如何使用 HTML Meta 标记](http://searchenginewatch.com/showPage.html?page=2167931)
- [在 ASP.NET 中的母版页](http://www.odetocode.com/articles/419.aspx)
- [使用 ASP.NET 3.5 的 ListView 和 DataPager 控件](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [将自定义的基本类用于 ASP.NET 页的代码隐藏类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones 和 Suchi Banerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](multiple-contentplaceholders-and-default-content-cs.md)
> [下一页](urls-in-master-pages-cs.md)
