---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
title: 以编程方式指定母版页 (C#) |Microsoft Docs
author: rick-anderson
description: 设置内容页面的母版页 PreInit 事件处理程序通过以编程方式来看待。
ms.author: aspnetcontent
ms.date: 07/28/2008
ms.assetid: 7c4a3445-2440-4aee-b9fd-779c05e6abb2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: fa5de936d3b515e5c60223002fe51dbc23fed66c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809266"
---
<a name="specifying-the-master-page-programmatically-c"></a>以编程方式指定母版页 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip)或[下载 PDF](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> 设置内容页面的母版页 PreInit 事件处理程序通过以编程方式来看待。


## <a name="introduction"></a>介绍

由于中的开篇示例[*创建站点范围内布局使用 Master Pages*](creating-a-site-wide-layout-using-master-pages-cs.md)，则所有内容页面已引用以声明方式通过其主页面`MasterPageFile`中属性`@Page`指令。 例如，以下`@Page`指令将内容页面链接到母版页`Site.master`:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

[ `Page`类](https://msdn.microsoft.com/library/system.web.ui.page.aspx)中`System.Web.UI`命名空间包括[`MasterPageFile`属性](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx)的返回内容页面的母版页的路径; 它是由设置此属性`@Page`指令。 此属性还可以用于以编程方式指定内容页面的母版页。 此方法非常有用，如果你想要动态分配基于外部因素，例如，用户访问的页面的母版页。

在本教程中，我们将第二个主页面添加到我们的网站和动态决定要在运行时使用的主页面。

## <a name="step-1-a-look-at-the-page-lifecycle"></a>步骤 1： 查看页面生命周期

每当请求到达 ASP.NET 页面的内容页面的 web 服务器时，ASP.NET 引擎必须 fuse 页面的内容控件添加到母版页的相应 ContentPlaceHolder 控件。 此合成创建然后，可以继续完成典型的页面生命周期的单个控件层次结构。

图 1 显示了此合成。 步骤 1 中图 1 显示的初始内容和主页面控件层次结构。 末端的 PreInit 阶段内容页中的控件添加到相应 Contentplaceholder 母版页 (步骤 2) 中。 之后此合成母版页用作浮点混合的控件层次结构的根。 这融合在控件层次结构随后将添加到页后，可以生成已完成的控件层次结构 (第 3 步)。 最终结果是页面的控件层次结构，包括浮点混合的控件层次结构。


[![母版页和内容页面的控件层次结构是融合在一起的 PreInit 阶段](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**图 01**： 在母版页和内容页面的控件层次结构是融合在一起的 PreInit 阶段 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image3.png))


## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>步骤 2： 设置`MasterPageFile`代码中的属性

哪些母版页 partakes 中此合成取决于值`Page`对象的`MasterPageFile`属性。 设置`MasterPageFile`中的属性`@Page`指令具有分配的净效果`Page`的`MasterPageFile`属性在初始化阶段，这是页面的生命周期的第一个阶段。 或者，我们可以以编程方式设置此属性。 但是，它是命令性合成图 1 中的发生之前设置此属性。

开头的 PreInit 阶段`Page`对象会引发其[`PreInit`事件](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx)，并调用其[`OnPreInit`方法](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)。 若要以编程方式设置主页面，然后，我们可以创建的事件处理程序`PreInit`事件或重写`OnPreInit`方法。 让我们看看这两种方法。

首先打开`Default.aspx.cs`，我们的站点的主页的代码隐藏类文件。 添加事件处理程序的页面的`PreInit`通过键入下面的代码中的事件：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

从此处，我们可以设置`MasterPageFile`属性。 更新代码，以便它将的值"~ / Site.master"到`MasterPageFile`属性。


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

如果设置了断点并开始调试你会看到，每当`Default.aspx`访问页面时，或者每当没有回发到此页上，`Page_PreInit`事件处理程序执行和`MasterPageFile`属性分配给"~ / Site.master"。

或者，您可以重写`Page`类的`OnPreInit`方法，设置`MasterPageFile`那里属性。 对于此示例中，让我们不设置母版页的特定页上，而从`BasePage`。 回想一下，我们创建一个自定义基本页类 (`BasePage`) 返回[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程。 目前`BasePage`重写`Page`类的`OnLoadComplete`方法，它在其中设置页面的`Title`属性基于站点地图数据。 让我们更新`BasePage`还重写`OnPreInit`方法以编程方式指定母版页。


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

由于所有内容页面派生`BasePage`，现在必须所有人以编程方式分配其主页面。 此时`PreInit`中的事件处理程序`Default.aspx.cs`是多余的; 可以删除它。

### <a name="what-about-thepagedirective"></a>怎样`@Page`指令？

什么可能有点令人困惑的是内容页的`MasterPageFile`属性现在在两个位置指定： 以编程方式在`BasePage`类的`OnPreInit`方法也`MasterPageFile`中每个内容页面的属性`@Page`指令。

页面生命周期中的第一个阶段是初始化阶段。 在此阶段`Page`对象的`MasterPageFile`属性分配的值`MasterPageFile`属性中`@Page`指令 （如果提供）。 PreInit 阶段遵循初始化阶段，并就在这里，我们以编程方式设置`Page`对象的`MasterPageFile`属性，从而覆盖从分配的值`@Page`指令。 因为我们将设置`Page`对象的`MasterPageFile`属性以编程方式，我们无法移除`MasterPageFile`属性从`@Page`指令而不会影响最终用户体验。 若要使此您自己确信，请继续并删除`MasterPageFile`属性从`@Page`指令`Default.aspx`，然后访问通过浏览器页面。 如您所料，输出之前已删除的属性是与相同。

是否`MasterPageFile`属性设置通过`@Page`指令或以编程方式并向最终用户体验不重要。 但是，`MasterPageFile`属性中`@Page`指令用于 Visual studio 在设计时生成所见即所得设计器中的视图。 如果返回到`Default.aspx`Visual Studio 中，并导航到设计器中，您将看到该消息，"母版页错误： 页具有控件需要母版页引用，但未指定"（请参见图 2）。

简单地说，您需要离开`MasterPageFile`属性中`@Page`指令以享受 Visual Studio 中丰富的设计时体验。


[![Visual Studio 使用@Page指令的 MasterPageFile 属性来呈现设计视图](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**图 02**: Visual Studio 将使用`@Page`指令的`MasterPageFile`特性呈现到设计视图 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image6.png))


## <a name="step-3-creating-an-alternative-master-page"></a>步骤 3： 创建一个替代方法的母版页

因为在运行时以编程方式设置内容页面的母版页就可以动态加载特定母版页根据某些外部条件。 此功能可在其中的站点布局需要改变基于用户的情况下很有用。 例如，博客引擎 web 应用程序可能允许其用户选择一个布局，以他们的博客，其中每个布局是与不同的母版页相关联。 在运行时，访问者查看用户的网络日志时的 web 应用程序需要确定博客的布局和动态将相应的母版页与内容页相关联。

让我们看一下如何动态加载母版页在运行时根据某些外部条件。 我们的网站当前包含一个母版页 (`Site.master`)。 我们需要另一个主页面，以说明选择母版页在运行时。 此步骤中重点介绍创建和配置新的主页面。 步骤 4 所示在确定哪些主页后，可以在运行时使用。

在名为的根文件夹中创建新的主页面`Alternate.master`。 此外将新的样式表添加到名为网站`AlternateStyles.css`。


[![添加另一个母版页和 CSS 文件到网站](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**图 03**： 添加另一个母版页和 CSS 文件到网站 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image9.png))


我已经设计`Alternate.master`主页面顶部的中心页和深蓝色背景上显示的标题都有。 我已分配的左侧的列，已将该内容下方移动`MainContent`ContentPlaceHolder 控件，它现在跨越整个页面的宽度。 此外，我 nixed 无序的课程列表，并替换上面水平列表`MainContent`。 我还将更新的字体和颜色以及使用的母版页 （，扩展，其内容的页面）。 图 4 所示`Default.aspx`时使用`Alternate.master`母版页。

> [!NOTE]
> ASP.NET 包括能够定义*主题*。 主题是图像、 CSS 文件和与样式有关的 Web 控件属性设置可以应用于在运行时的页面的集合。 主题是如果您的站点布局各不相同，这是仅在显示的图像中和通过其 CSS 规则的方式。 如果布局如使用不同的 Web 控件更大不相同，或具有截然不同布局，然后你将需要使用单独的主页面。 有关详细信息主题本教程结束时查阅更多参考资料部分。


[![内容页面现在可以使用新的外观和感觉](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**图 04**： 我们内容页面现在可以使用新的外观 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image12.png))


当融合在 master 和内容页的标记时，`MasterPage`类检查，以确保每个内容控件在内容页中的引用 ContentPlaceHolder 母版页中的。 如果找到了引用不存在 ContentPlaceHolder 内容控件，将引发异常。 换而言之，它是命令性母版页分配给内容页，为每个具有 ContentPlaceHolder 内容在内容页中的控件。

`Site.master`母版页包含四个 ContentPlaceHolder 控件：

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

一些我们的网站中的内容页包括只是一个或两个内容控件;其他可用 Contentplaceholder 的每个包括的内容控件。 如果我们新的主页面 (`Alternate.master`) 可能曾经分配给具有内容控件中 Contentplaceholder 的所有这些内容页面`Site.master`则非常基本的`Alternate.master`还包括相同的 ContentPlaceHolder 控件，如`Site.master`.

若要获取你`Alternate.master`母版页中以看起来类似于我的 （请参阅图 4），首先定义中的主页面的样式`AlternateStyles.css`样式表。 添加到以下规则`AlternateStyles.css`:


[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

接下来，添加以下声明性标记到`Alternate.master`。 正如您所看到的`Alternate.master`包含具有相同的四个 ContentPlaceHolder 控件`ID`值中的 ContentPlaceHolder 控件作为`Site.master`。 此外，它包括一个 ScriptManager 控件，它是我们的网站使用 ASP.NET AJAX 框架的这些页面的必要条件。


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>测试新的主页面

若要测试此新的主页面更新`BasePage`类的`OnPreInit`方法，以便`MasterPageFile`属性赋予值"~ / Alternate.master"，然后访问该网站。 每个页面应函数而无需除两个错误：`~/Admin/AddProduct.aspx`和`~/Admin/Products.aspx`。 将产品添加到在 DetailsView`~/Admin/AddProduct.aspx`会导致`NullReferenceException`从尝试设置主页面的代码行`GridMessageText`属性。 访问时`~/Admin/Products.aspx``InvalidCastException`并显示消息的页面加载上引发:"找不到类型的对象强制转换 ASP.alternate\_master 键入 ASP.site\_master。"

之所以发生这些错误`Site.master`代码隐藏类包括公共事件、 属性和方法中未定义`Alternate.master`。 这两页的标记部分有`@MasterType`指令，它引用`Site.master`母版页。


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

此外，DetailsView 的`ItemInserted`中的事件处理程序`~/Admin/AddProduct.aspx`包括强制转换松散类型代码`Page.Master`类型的对象的属性`Site`。 `@MasterType`指令 （这种方式使用） 和在 cast`ItemInserted`事件处理程序紧密耦合`~/Admin/AddProduct.aspx`并`~/Admin/Products.aspx`到页`Site.master`母版页。

若要中断此我们可以具有的紧密耦合`Site.master`和`Alternate.master`派生自包含的公共成员定义一个公共基类。 接下来，我们可以更新`@MasterType`指令以引用此公共基类型。

### <a name="creating-a-custom-base-master-page-class"></a>创建自定义基本 Master Page 类

添加到一个新类文件`App_Code`名为的文件夹`BaseMasterPage.cs`，并将其从派生`System.Web.UI.MasterPage`。 我们需要定义`RefreshRecentProductsGrid`方法和`GridMessageText`属性中的`BaseMasterPage`，但我们不能只是移动它们那里从`Site.master`因为这些成员使用特定于的 Web 控件`Site.master`母版页 ( `RecentProducts`GridView 和`GridMessage`标签)。

我们需要做什么是配置`BaseMasterPage`这些成员，定义，但实际上由实现的方式`BaseMasterPage`的派生类 (`Site.master`和`Alternate.master`)。 这种类型的继承可通过将标记的类和作为其成员`abstract`。 简单地说，添加`abstract`这两个成员的关键字宣布`BaseMasterPage`尚未实现`RefreshRecentProductsGrid`和`GridMessageText`，但将其派生的类。

我们还需要定义`PricesDoubled`中的事件`BaseMasterPage`并提供一种方法由派生的类来引发事件。 在.NET Framework 中用于促进这种行为模式是基类中创建的公共事件，并添加一个受保护`virtual`名为方法`OnEventName`。 派生的类然后可以调用此方法来引发事件，或可重写它之前或之后引发该事件时，才执行代码。

更新你`BaseMasterPage`类，使其包含以下代码：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

接下来，请转到`Site.master`代码隐藏类，并将其从派生`BaseMasterPage`。 因为`BaseMasterPage`是`abstract`我们需要重写这些`abstract`中的成员此处`Site.master`。 添加`override`方法和属性定义的关键字。 此外更新代码，将引发`PricesDoubled`中的事件`DoublePrice`按钮的`Click`事件处理程序通过调用基类的`OnPricesDoubled`方法。

这些修改后`Site.master`代码隐藏类应包含以下代码：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

我们还需要更新`Alternate.master`的代码隐藏类派生自`BaseMasterPage`并重写两个`abstract`成员。 但是，由于`Alternate.master`不包含一个 GridView，最新的产品，也不新产品后显示一条消息的标签添加到数据库的列表，这些方法不需要执行任何操作。


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>引用基本 Master Page 类

现在，我们已完成`BaseMasterPage`类并已将其扩展我们两个主页面中，我们最后一步是更新`~/Admin/AddProduct.aspx`和`~/Admin/Products.aspx`页来指代该公共类型。 首先更改`@MasterType`指令从这两个页中：


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

到:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

而不是引用文件路径，`@MasterType`属性现在引用的基类型 (`BaseMasterPage`)。 因此，强类型化`Master`现已在这两个页的代码隐藏类中使用的属性的类型`BaseMasterPage`(而不是类型`Site`)。 与此更改后重新访问`~/Admin/Products.aspx`。 以前，这会导致转换错误原因页面配置为使用`Alternate.master`母版页，但`@MasterType`指令引用`Site.master`文件。 但现在没有错误呈现页面。 这是因为`Alternate.master`母版页可以强制转换为类型的对象`BaseMasterPage`（因为它扩展了它）。

不需要进行中的一个小更改`~/Admin/AddProduct.aspx`。 在 DetailsView 控件`ItemInserted`事件处理程序使用这两个强类型化`Master`属性和松散类型`Page.Master`属性。 我们修复的强类型化引用时，我们更新`@MasterType`指令，但我们仍需要更新松散类型化引用。 替换为以下代码行：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

使用以下命令，这将强制转换`Page.Master`为基类型：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>步骤 4： 确定哪些绑定到内容页面的母版页

我们`BasePage`类当前设置的所有内容页的`MasterPageFile`为页面生命周期的 PreInit 阶段中硬编码值的属性。 我们可以更新此代码根据某些外部因素所基于的母版页。 可能是主页面的加载取决于当前登录用户的首选项。 在这种情况下，我们需要在编写代码`OnPreInit`中的方法`BasePage`查找当前正在访问用户的主页面首选项。

让我们创建一个网页，允许用户选择的主控页后，可以使用-`Site.master`或`Alternate.master`-并在会话变量中保存此选项。 首先在名为的根目录中创建新的 web 页`ChooseMasterPage.aspx`。 创建此页 （或任何其他内容页之后） 时无需将其绑定到主页面，因为主页面中以编程方式设置`BasePage`。 但是，如果不绑定新页面母版页然后新页面的默认声明性标记包含 Web 窗体和其他内容提供的主页面。 你将需要手动将此标记替换为相应的内容控件。 为此，我发现更轻松地将新的 ASP.NET 页面绑定到母版页。

> [!NOTE]
> 因为`Site.master`和`Alternate.master`具有一组相同的 ContentPlaceHolder 控件并不重要选择创建新的内容页面时哪些母版页。 为了保持一致，我会建议使用`Site.master`。


[![向网站添加新的内容页面](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**图 05**： 将新的内容页面添加到网站 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image15.png))


更新`Web.sitemap`文件以便包括本课程中的一个条目。 添加以下标记下方`<siteMapNode>`母版页和 ASP.NET AJAX 课程：


[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

添加到任何内容之前`ChooseMasterPage.aspx`页上花点时间来更新页面的代码隐藏类，使它派生`BasePage`(而非`System.Web.UI.Page`)。 接下来，将 DropDownList 控件添加到页，设置其`ID`属性设置为`MasterPageChoice`，并添加具有两个 Listitem`Text`的值"~ / Site.master"和"~ / Alternate.master"。

向页面添加一个按钮 Web 控件并设置其`ID`并`Text`属性设置为`SaveLayout`和"保存的布局选择"，分别。 此时页面的声明性标记应类似于下面：


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

当首次访问页面时我们需要显示用户的当前选定的主页面选择。 创建`Page_Load`事件处理程序并添加以下代码：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

上面的代码执行仅在第一次的页面访问 （和不在后续回发）。 它首先检查以查看是否在会话变量`MyMasterPage`存在。 如果是这样，它会尝试查找列表中的项匹配`MasterPageChoice`DropDownList。 如果找到匹配的 ListItem，其`Selected`属性设置为`true`。

我们还需要将保存到的用户的选择的代码`MyMasterPage`会话变量。 创建事件处理程序`SaveLayout`按钮的`Click`事件，并添加以下代码：


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> 按时间`Click`在回发时执行事件处理程序时，已选择主页面。 因此，用户的下拉列表中选择不会生效直到下一个页面访问。 `Response.Redirect`强制浏览器以重新请求`ChooseMasterPage.aspx`。


与`ChooseMasterPage.aspx`页上完成，最后一项任务是让`BasePage`分配`MasterPageFile`属性值的基础`MyMasterPage`会话变量。 如果未设置会话变量有`BasePage`默认为`Site.master`。


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> 我将分配的代码移`Page`对象的`MasterPageFile`共属性`OnPreInit`事件处理程序并为两个单独的方法。 此第一种方法， `SetMasterPageFile`，将分配`MasterPageFile`属性设置为第二种方法，返回的值`GetMasterPageFileFromSession`。 我所做`SetMasterPageFile`方法`virtual`，以便将来类扩展`BasePage`可以根据需要以使其实现自定义逻辑，根据需要重写。 我们会举例说明重写`BasePage`的`SetMasterPageFile`下一教程中的属性。


利用此代码，请访问`ChooseMasterPage.aspx`页。 最初，`Site.master`母版页是所选 （见图 6），但用户可以选择不同的主页面，从下拉列表。


[![显示使用 Site.master 母版页内容页](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**图 06**： 显示使用内容页都`Site.master`母版页 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image18.png))


[![内容页现在显示使用 Alternate.master 母版页](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**图 07**： 内容页面会显示使用现在`Alternate.master`母版页 ([单击以查看实际尺寸的图像](specifying-the-master-page-programmatically-cs/_static/image21.png))


## <a name="summary"></a>总结

当访问内容页面时，其内容控件融合在一起，其主页面 ContentPlaceHolder 控件。 内容页面的母版页为由`Page`类的`MasterPageFile`属性，它分配给`@Page`指令的`MasterPageFile`属性在初始化阶段。 与本教程介绍了，我们可以将值赋给`MasterPageFile`属性，只要我们之前 PreInit 阶段结束时进行。 能够以编程方式指定母版页大门更高级的方案，例如动态绑定到基于外部因素的母版页的内容页。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 页面生命周期关系图](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 页面生命周期概述](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 主题和外观概述](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [母版页： 提示、 技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [在 ASP.NET 中的主题](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Suchi Banerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-pages-and-asp-net-ajax-cs.md)
> [下一页](nested-master-pages-cs.md)
