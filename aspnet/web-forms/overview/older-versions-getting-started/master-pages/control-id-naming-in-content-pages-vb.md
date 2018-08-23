---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: 控件 ID 命名 (VB) 的内容页面中 |Microsoft Docs
author: rick-anderson
description: 说明了如何 ContentPlaceHolder 控件作为命名容器的因此可以以编程方式使用困难 （通过 FindConrol) 控件...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e9a751538ca28250e4e776ff2c6c3f0185ffbe6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833261"
---
<a name="control-id-naming-in-content-pages-vb"></a>控件 ID 命名 (VB) 的内容页面中
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> 说明了如何 ContentPlaceHolder 控件作为命名容器的因此可以以编程方式使用困难 （通过 FindConrol) 控件。 探讨此问题和解决方法。 此外介绍了如何以编程方式访问生成的 ClientID 值。


## <a name="introduction"></a>介绍

所有 ASP.NET 服务器控件都包括`ID`属性，用于唯一标识该控件并是依据此控件以编程方式访问中的代码隐藏类的方法。 同样，在 HTML 文档中的元素可能包括`id`唯一标识此元素的属性; 这些`id`值通常用于在客户端脚本中以编程方式引用特定的 HTML 元素。 鉴于此，你可能假设的 ASP.NET 服务器控件呈现为 HTML，其`ID`值将用作`id`呈现的 HTML 元素的值。 这不一定是这种情况因为在某些情况下一个控制与单个`ID`值可能会多次出现在呈现的标记。 请考虑 GridView 控件包含与标签 Web 控件使用 TemplateField`ID`的值`ProductName`。 在 GridView 绑定到其数据源在运行时，此标签将对每个 GridView 行一次重复。 每个呈现标签需求的唯一`id`值。

若要处理这种情况下，ASP.NET 允许某些控件表示为命名容器。 命名容器将用作新`ID`命名空间。 所有服务器控件的命名容器内显示都具有其呈现`id`值带有前缀`ID`命名的容器控件。 例如，`GridView`和`GridViewRow`类都是命名的容器。 因此，在使用 GridView TemplateField 中定义的标签控件`ID``ProductName`给定呈现`id`的值`GridViewID_GridViewRowID_ProductName`。 因为*GridViewRowID*是唯一的每个 GridView 行，生成`id`值是唯一的。

> [!NOTE]
> [ `INamingContainer`接口](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx)用于指示特定的 ASP.NET 服务器控件应充当命名容器。 `INamingContainer`接口不会不拼写出任何服务器控件必须实现的方法; 而是使用作为的标记。 在生成呈现的标记，如果某个控件实现此接口然后 ASP.NET 引擎自动添加前缀及其`ID`其子的值呈现`id`属性值。 在步骤 2 中的更详细地介绍此过程。


命名容器不只更改呈现`id`属性值，但也会影响如何控件可能以编程方式从引用 ASP.NET 页面的代码隐藏类。 `FindControl("controlID")`方法通常用于以编程方式引用的 Web 控件。 但是，`FindControl`不入侵通过命名容器。 因此，不能直接使用`Page.FindControl`方法来引用 GridView 或其他命名容器中的控件。

你可能已猜测到的如母版页和 Contentplaceholder 同时实现为容器命名。 在本教程中我们介绍如何 master pages 影响 HTML 元素`id`值和方法来以编程方式引用 Web 控件中内容页使用`FindControl`。

## <a name="step-1-adding-a-new-aspnet-page"></a>步骤 1： 添加一个新的 ASP.NET 页面

为了演示在本教程中讨论的概念，让我们将一个新的 ASP.NET 页面添加到我们的网站。 创建一个名为的新内容页`IDIssues.aspx`在根文件夹中，将其绑定到`Site.master`母版页。


![将内容页 IDIssues.aspx 添加到根文件夹](control-id-naming-in-content-pages-vb/_static/image1.png)

**图 01**： 添加内容页`IDIssues.aspx`的根文件夹


Visual Studio 自动为每个母版页的四个 Contentplaceholder 创建内容控件。 如中所述[*多个 Contentplaceholder 和默认内容*](multiple-contentplaceholders-and-default-content-vb.md)教程中，如果内容控件不存在主页面的默认 ContentPlaceHolder 内容，将改为发出。 因为`QuickLoginUI`并`LeftColumnContent`Contentplaceholder 包含此页的合适的默认标记、 继续和删除其相应的内容控件从`IDIssues.aspx`。 此时，内容页的声明性标记应如下所示：


[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

在中[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)教程中，我们创建一个自定义基本页类 (`BasePage`)，它是否会自动配置页面的标题未显式设置。 有关`IDIssues.aspx`页上使用此功能，该页面的代码隐藏类必须派生自`BasePage`类 (而不是`System.Web.UI.Page`)。 修改代码隐藏类的定义，使它看起来如下所示：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

最后，更新`Web.sitemap`文件以便包括本课程中新建一个条目。 添加`<siteMapNode>`元素，并设置其`title`并`url`属性为"控件 ID 命名问题"和`~/IDIssues.aspx`分别。 进行此添加后你`Web.sitemap`文件的标记应如下所示：


[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

如图 2 所示，在新的站点映射条目`Web.sitemap`立即反映在左侧列中的课程部分。


![课程部分现在包括一个指向&quot;控件 ID 命名问题&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**图 02**： 课程部分现在包含"控件 ID 命名问题"的链接


## <a name="step-2-examining-the-renderedidchanges"></a>第 2 步： 检查呈现`ID`更改

若要更好地了解所做的修改 ASP.NET 向呈现引擎发出`id`server 的值控制，让我们添加到的几个 Web 控件`IDIssues.aspx`页上，然后查看呈现的标记发送到浏览器。 具体而言，在文本中的类型"请输入你的年龄:"跟 TextBox Web 控件。 进一步向下的页上添加一个按钮 Web 控件和标签 Web 控件。 设置文本框的`ID`并`Columns`属性设置为`Age`和 3，分别。 设置按钮的`Text`并`ID`属性设置为"提交"和`SubmitButton`。 清除的标签`Text`属性并设置其`ID`到`Results`。

此时内容控件的声明性标记应类似于下面：


[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

图 3 显示了通过 Visual Studio 设计器进行查看时页。


[![此页包含三个 Web 控件： 文本框、 按钮和标签](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**图 03**: 页包含三个 Web 控件： 文本框、 按钮和标签 ([单击以查看实际尺寸的图像](control-id-naming-in-content-pages-vb/_static/image5.png))


访问通过浏览器页面，然后查看 HTML 源。 以下标记显示，作为`id`文本框、 按钮和标签 Web 控件的 HTML 元素的值的多种`ID`Web 控件的值和`ID`页中的命名容器的值。


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

正如本教程前面部分所述，母版页和其 Contentplaceholder 作为命名容器。 因此，同时参与呈现`ID`其嵌套的控件的值。 采用文本框的`id`属性，例如： `ctl00_MainContent_Age`。 请记住，TextBox 控件`ID`的值为`Age`。 这其 ContentPlaceHolder 控件的带有前缀`ID`值， `MainContent`。 此外，此值以前缀与母版页`ID`值， `ctl00`。 实际效果是`id`属性值，其中包括`ID`母版页、 ContentPlaceHolder 控件和文本框本身的值。

图 4 说明了此行为。 若要确定呈现`id`的`Age`文本框中，使用启动`ID`值的文本框控件， `Age`。 接下来，努力完善控件层次结构。 在每个命名容器 （桃色颜色与这些节点），前缀呈现当前`id`使用的命名容器`id`。


![Rendered id 属性是基于上 ID 值的命名容器](control-id-naming-in-content-pages-vb/_static/image6.png)

**图 04**: 呈现`id`属性是基于上`ID`命名容器的值


> [!NOTE]
> 如我们所述，`ctl00`部分呈现`id`属性构成`ID`值的主页上，但你可能想知道如何将此`ID`值的灵感。 我们未指定其任意位置在我们的主数据库或内容页面中。 ASP.NET 页面中的大多数服务器控件通过页面的声明性标记显式添加。 `MainContent`的标记中显式指定 ContentPlaceHolder 控件`Site.master`;`Age`文本框中已定义`IDIssues.aspx`的标记。 我们可以指定`ID`这些控件通过属性窗口或从声明性语法类型的值。 声明性标记中未定义其他控件，主页面本身，所示。 因此，其`ID`值必须为我们自动生成。 ASP.NET 引擎集`ID`在运行时对其 Id 未显式设置这些控件的值。 它使用的命名模式`ctlXX`，其中*XX*是按顺序递增的整数值。


主页面本身中提供的命名容器，因为在母版页中定义的 Web 控件也已更改呈现`id`属性值。 例如，`DisplayDate`标签，我们添加到中的母版页[*使用母版页创建站点范围内布局*](creating-a-site-wide-layout-using-master-pages-vb.md)教程具有以下呈现标记：


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

请注意，`id`属性包含这两个主页面的`ID`值 (`ctl00`) 和`ID`标签 Web 控件的值 (`DateDisplay`)。

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>步骤 3： 以编程方式引用通过 Web 控件`FindControl`

每个 ASP.NET 服务器控件包含`FindControl("controlID")`方法搜索名为的控件的控件的后代*controlID*。 如果找到这样的控件，则返回;如果不找到任何匹配控件，则`FindControl`返回`Nothing`。

`FindControl` 在所需的访问控制，但没有对它的直接引用方案中非常有用。 在 GridView 的字段中的控件时使用的数据 Web 控件，如 GridView，例如，在声明性语法中，一次定义但在运行时控件的实例创建的每个 GridView 行。 因此，在运行时生成的控件存在，但我们不提供可从代码隐藏类的直接引用。 因此我们需要使用`FindControl`以编程方式使用 GridView 的字段内的特定控件。 (有关使用的详细信息`FindControl`若要访问的数据 Web 控件模板中的控件，请参阅[自定义格式设置基于数据的](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md)。)动态地将 Web 控件添加到 Web 窗体时发生这同一情况下，本主题中所述[创建动态数据输入用户界面](https://msdn.microsoft.com/library/aa479330.aspx)。

若要演示如何使用`FindControl`方法搜索内容页中的控件创建的事件处理程序`SubmitButton`的`Click`事件。 事件处理程序中，添加以下代码，以编程方式引用`Age`文本框中并`Results`标签使用`FindControl`方法，然后显示一条消息中的`Results`基于用户的输入。

> [!NOTE]
> 当然，我们无需使用`FindControl`以引用此示例中的标签和文本框控件。 我们可以引用它们直接通过其`ID`属性值。 我使用`FindControl`这里要说明使用时，会发生什么情况`FindControl`从内容页。


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

尽管用来调用的语法`FindControl`方法会稍有不同的前两行`SubmitButton_Click`，它们在语义上等效。 回想一下，所有 ASP.NET 服务器控件都包括`FindControl`方法。 这包括`Page`从所有 ASP.NET 代码隐藏类必须派生自的类。 因此，调用`FindControl("controlID")`等效于调用`Page.FindControl("controlID")`，假定尚未重写`FindControl`方法中代码隐藏类或自定义基类中。

后输入此代码，请访问`IDIssues.aspx`通过浏览器页上，输入你的年龄，然后单击"提交"按钮。 单击"提交"按钮时`NullReferenceException`引发 （请参见图 5）。


[![引发 NullReferenceException](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**图 05**： 一个`NullReferenceException`引发 ([单击以查看实际尺寸的图像](control-id-naming-in-content-pages-vb/_static/image9.png))


如果在中设置断点`SubmitButton_Click`事件处理程序会同时调用`FindControl`返回`Nothing`。 `NullReferenceException`我们尝试访问时，将引发`Age`文本框的`Text`属性。

问题在于`Control.FindControl`仅搜索*控制*的相同的命名容器中的后代。 因为主页面构成新的命名容器，调用`Page.FindControl("controlID")`永远不会 permeates 母版页对象`ctl00`。 (图 4，若要查看的控件层次结构，其中显示了将回指`Page`对象作为主页面对象的父对象`ctl00`。)因此，`Results`标签并`Age`找不到文本框中并`ResultsLabel`并`AgeTextBox`分配的值`Nothing`。

有两个到这一难题的解决方法： 我们可以向下钻取，一个命名的容器一次，于相应的控件;或者，我们可以创建我们自己`FindControl`permeates 命名容器的方法。 让我们检查每个选项。

### <a name="drilling-into-the-appropriate-naming-container"></a>钻取到相应的命名容器

若要使用`FindControl`引用`Results`标签或`Age`文本框中，我们需要调用`FindControl`从相同的命名容器中的一个祖先控件。 图 4 显示了，如`MainContent`ContentPlaceHolder 控件是唯一的祖先`Results`或`Age`的是同一个命名容器中。 换而言之，调用`FindControl`方法从`MainContent`控件，如下面的代码段中所示将正确返回对引用`Results`或`Age`控件。


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

但是，我们不能使用`MainContent`ContentPlaceHolder 从使用上面的语法，因为在母版页中定义 ContentPlaceHolder 我们内容页面的代码隐藏类。 相反，我们必须使用`FindControl`来获取对引用`MainContent`。 中的代码替换为`SubmitButton_Click`事件处理程序并进行以下修改：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

如果在访问通过浏览器页面，输入您的年龄，然后单击"提交"按钮，`NullReferenceException`引发。 如果在中设置断点`SubmitButton_Click`事件处理程序会尝试进行调用时，会发生此异常`MainContent`对象的`FindControl`方法。 `MainContent`对象是否等于`Nothing`因为`FindControl`方法找不到名为"主要内容"的对象。 根本原因是与相同`Results`标签并`Age`TextBox 控件：`FindControl`从控件层次结构的顶部开始其搜索，并不入侵命名容器，但`MainContent`ContentPlaceHolder 是在主页上，这是命名容器。

我们可以使用之前`FindControl`来获取对引用`MainContent`，我们首先需要对主页面控件的引用。 母版页引用后我们可以获取对的引用`MainContent`通过 ContentPlaceHolder`FindControl`并从那里，引用`Results`标签和`Age`文本框中 (同样，通过使用`FindControl`)。 但是，我们如何获取对母版页的引用？ 通过检查`id`呈现的标记中的属性是显而易见的主页面`ID`值是`ctl00`。 因此，我们可以使用`Page.FindControl("ctl00")`若要获取对母版页的引用，然后使用该对象获取对引用`MainContent`，依次类推。 以下代码片段说明了此逻辑：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

尽管此代码也肯定可以生效，它假定主页面的自动生成`ID`始终为`ctl00`。 它永远不会是一个好办法使有关自动生成值的假设。

幸运的是，对母版页的引用是可通过访问`Page`类的`Master`属性。 因此，而无需使用`FindControl("ctl00")`若要获取母版页的引用，以便访问`MainContent`ContentPlaceHolder，我们可以改为使用`Page.Master.FindControl("MainContent")`。 更新`SubmitButton_Click`事件处理程序使用以下代码：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

这一次，访问该网页通过浏览器中，输入你的年龄，然后单击"提交"按钮显示在消息`Results`标签、 按预期方式。


[![标签中显示用户的年龄](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**图 06**： 标签中显示的用户的年龄 ([单击以查看实际尺寸的图像](control-id-naming-in-content-pages-vb/_static/image12.png))


### <a name="recursively-searching-through-naming-containers"></a>以递归方式搜索容器命名

引用前面的代码示例的原因`MainContent`ContentPlaceHolder 控件从主页，然后`Results`标签和`Age`TextBox 控件从`MainContent`，是因为`Control.FindControl`方法只搜索内*控制*的命名容器。 无`FindControl`命名容器中的保持在大多数情况下使意义上，因为在两个不同的命名容器中的两个控件可能具有相同`ID`值。 请考虑一个 GridView，定义一个名为标签 Web 控件的大小写`ProductName`在其 Templatefield 之一中。 在数据绑定到在运行时，GridView`ProductName`会为每个 GridView 行创建标签。 如果`FindControl`搜索通过所有命名容器，我们调用`Page.FindControl("ProductName")`，哪些标签实例应`FindControl`返回？ `ProductName`中第一个 GridView 行标签？ 最后一行中的一个？

因此`Control.FindControl`只需搜索*控制*的命名容器的意义在大多数情况下。 但其他情况下，如面向我们，我们具有一个唯一的一个`ID`跨所有容器都命名，并且想要避免这种引用来访问控件的控件层次结构中每个都命名容器。 具有`FindControl`太以递归方式搜索所有命名容器使感应的变体。 遗憾的是，.NET Framework 不包括此类方法。

值得高兴的是，我们可以创建我们自己`FindControl`方法，以递归方式搜索所有命名容器。 事实上，使用*扩展方法*我们可以添加`FindControlRecursive`方法`Control`类来搭配其现有的`FindControl`方法。

> [!NOTE]
> 扩展方法是 C# 3.0 和 Visual Basic 9 随附的.NET Framework 版本 3.5 和 Visual Studio 2008 的语言的新功能。 简单地说，扩展方法允许开发人员创建特殊的语法通过现有的类类型的新方法。 有关此有用的功能的详细信息，请参阅我的文章[使用扩展方法扩展基类型的功能](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)。


若要创建扩展方法，将添加到新的文件`App_Code`文件夹名为`PageExtensionMethods.vb`。 添加名为的扩展方法`FindControlRecursive`作为输入，采用`String`参数名为`controlID`。 扩展方法才能正常工作，非常重要的类标记为`Module`且带有前缀的扩展方法`<Extension()>`属性。 此外，所有扩展方法必须都接受作为其第一个参数对象，该类型对其应用的扩展方法。

将以下代码添加到`PageExtensionMethods.vb`文件来定义此`Module`和`FindControlRecursive`扩展方法：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

利用此代码，返回到`IDIssues.aspx`页面的代码隐藏类并注释掉当前`FindControl`方法调用。 将它们替换为对调用`Page.FindControlRecursive("controlID")`。 什么是关于扩展方法是，它们显示直接在 IntelliSense 下拉列表中。 如图 7 所示，当您键入`Page`，然后点击句点`FindControlRecursive`IntelliSense 以及其他下拉列表中包含方法`Control`类方法。


[![扩展方法均包含在 IntelliSense 下拉列表](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**图 07**： 在 IntelliSense 下拉列表包括扩展方法 ([单击以查看实际尺寸的图像](control-id-naming-in-content-pages-vb/_static/image15.png))


输入以下代码到`SubmitButton_Click`事件处理程序，然后对其进行测试方法访问的页面，输入你的年龄，然后单击"提交"按钮。 返回中图 6 所示，生成的输出将为消息，"您是年龄岁 ！"


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> 因为扩展方法不熟悉 C# 3.0 和 Visual Basic 9 中，如果您使用的 Visual Studio 2005 不能使用扩展方法。 相反，您需要实现`FindControlRecursive`中的帮助器类的方法。 [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx)在他的博客文章中具有此类示例[微波激射器的 ASP.NET 网页和`FindControl` ](http://www.west-wind.com/WebLog/posts/5127.aspx)。


## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>步骤 4： 使用正确`id`属性在客户端脚本中的值

在本教程中的简介中所述，Web 控件的呈现`id`属性通常用于在客户端脚本中以编程方式引用特定的 HTML 元素。 例如，以下 JavaScript 引用 HTML 元素由其`id`然后在一个模式消息框中显示其值：


[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

回想一下，在 ASP.NET 页，不包括命名容器，呈现的 HTML 元素的`id`属性等同于 Web 控件的`ID`属性值。 因此，很容易中进行硬编码`id`属性值为 JavaScript 代码。 也就是说，如果您知道您想要访问`Age`TextBox Web 控件通过客户端脚本，这样通过调用`document.getElementById("Age")`。

此方法的问题是，当使用主页面 （或其他命名容器控件中），呈现的 HTML`id`不是 Web 控件的同义词，`ID`属性。 您首先会想到可能访问通过浏览器页并查看源以确定实际`id`属性。 一旦您知道呈现`id`值，您可以将其粘贴到对调用`getElementById`访问需要通过客户端侧脚本使用的 HTML 元素。 这种方法是不太理想，因为某些更改页面的控件层次结构或将更改为`ID`命名控件的属性会更改生成`id`属性，从而破坏您的 JavaScript 代码。

值得高兴的是`id`呈现的属性值是在服务器端代码中通过 Web 控件的可访问[`ClientID`属性](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)。 应使用此属性来确定`id`属性在客户端脚本中使用的值。 例如，若要向页面添加 JavaScript 函数，调用时，显示的值`Age`文本框中模式消息框中，将以下代码添加到`Page_Load`事件处理程序：


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

上面的代码中插入的值`Age`文本框中的`ClientID`属性转换成 JavaScript 调用`getElementById`。 如果您访问此页上的通过浏览器并查看 HTML 源，您会发现以下 JavaScript 代码：


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

请注意如何正确`id`属性值， `ctl00_MainContent_Age`，将显示在调用`getElementById`。 在运行时计算此值，因为它的工作而不考虑对页面控件层次结构的更高版本更改。

> [!NOTE]
> 此 JavaScript 示例只是演示如何将添加正确引用由服务器控件呈现的 HTML 元素的 JavaScript 函数。 若要使用此函数将需要编写额外的 JavaScript 调用该函数，或当文档加载时某些特定的用户操作怎样。 有关这些详细信息和相关的主题，阅读[使用客户端侧脚本](https://msdn.microsoft.com/library/aa479302.aspx)。


## <a name="summary"></a>总结

某些 ASP.NET 服务器控件用作命名的容器，这会影响呈现`id`属性值及其后代控件以及通过 canvassed 的控件的作用域`FindControl`方法。 有关主页面，主页面本身和其 ContentPlaceHolder 控件命名容器。 因此，我们需要将提出更多工作要以编程方式引用中内容页中使用的控件`FindControl`。 在本教程中，我们将探讨两种方法： 钻入 ContentPlaceHolder 控件并调用其`FindControl`方法; 和实施我们自己`FindControl`实现它以递归方式搜索所有命名容器。

除了与引用 Web 控件引入命名容器的服务器端的问题，还有一些客户端的问题。 如果没有命名容器，Web 控件`ID`属性值并在其中呈现`id`属性值都是相同。 但添加了命名容器，呈现`id`属性包括这两个`ID`Web 控件和在其控件层次结构体系中命名的容器的值。 这些命名问题是不产生问题，只要您使用 Web 控件`ClientID`属性来确定呈现`id`属性在客户端脚本中的值。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 母版页和 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [创建动态数据输入用户界面](https://msdn.microsoft.com/library/aa479330.aspx)
- [将使用扩展方法的基类型功能扩展](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [如何： 引用 ASP.NET 主机页面内容](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [本地主页： 提示、 技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [使用客户端脚本](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones 和 Suchi Barnerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](urls-in-master-pages-vb.md)
> [下一页](interacting-with-the-master-page-from-the-content-page-vb.md)
