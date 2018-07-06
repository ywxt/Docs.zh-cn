---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: Url 中的母版页 (C#) |Microsoft Docs
author: rick-anderson
description: 解决了主页面中的 Url 可能会由于是在不同的相对目录比内容页的主控页文件中中断。 探讨变基...
ms.author: aspnetcontent
ms.date: 06/10/2008
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 827c471074fbfeb049613f5cc5ffb82937284f00
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821555"
---
<a name="urls-in-master-pages-c"></a>母版页 (C#) 中的 Url
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> 解决了主页面中的 Url 可能会由于是在不同的相对目录比内容页的主控页文件中中断。 查看基类重定位通过 Url ~ 的声明性语法和以编程方式使用 ResolveUrl 和 ResolveClientUrl 中。 （还请查看


## <a name="introduction"></a>介绍

所有示例中我们见到目前为止，母版页和内容页所在的文件夹 （网站的根文件夹） 中找到。 但为什么母版页和内容页必须位于同一文件夹中没有理由。 当然可以在子文件夹中创建内容页面。 同样，您可能会创建`~/MasterPages/`文件夹站点的主页面所在的位置。

母版页和内容页放置在不同的文件夹中的一个潜在的问题涉及到中断的 Url。 如果母版页包含超链接、 图像或其他元素中的相对 Url，该链接将驻留在不同的文件夹的内容页面的无效。 在本教程中，我们检查此问题以及解决方法的源。

## <a name="the-problem-with-relative-urls"></a>与相对 Url 的问题

在网页上的 URL 称为*相对 URL*如果它指向该资源的位置是相对于网站的文件夹结构中的 web 页面的位置。 任何不以前导正斜杠开头的 URL (`/`) 或协议 (如`http://`) 是相对的因为它包含 URL 的 web 页的位置上基于浏览器通过解决的。

例如，我们的网站具有`~/Images/`单个图像文件，具有文件夹`PoweredByASPNET.gif`。 主控页文件`Site.master`已`<img>`中的元素`footerContent`区域使用以下标记：


[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

`src`属性中的值`<img>`元素是相对 URL，因为它不会启动与`/`或`http://`。 简单地说，`src`属性值会告诉浏览器中看起来都`Images`为名为的文件的子文件夹`PoweredByASPNET.gif`。

当来访的内容页面，上面的标记是直接发送到浏览器。 请花费片刻时间访问`About.aspx`和查看发送到浏览器的 HTML 源代码。 您会发现在母版页中完全相同的标记已发送到浏览器。


[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

如果内容页的根文件夹中 (按原样`About.aspx`) 一切按预期运行，因为没有`Images`相对于根文件夹的子文件夹。 但是，事情中断，如果内容页处于不同的文件夹的母版页。 若要说明这一点，创建一个名为子`Admin`。 接下来，添加一个名为的内容页`Default.aspx`到`Admin`文件夹，并确保将绑定到的新页`Site.master`母版页。

> [!NOTE]
> 在中[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中，我们创建一个名为的自定义基本页类`BasePage`的自动设置内容页面的标题 (如果它没有显式分配）。 别忘了具有新创建的页面的代码隐藏类派生自`BasePage`，以便它可以利用此功能。


创建此内容页后，在解决方案资源管理器应类似于图 1。


![一个新文件夹和 ASP.NET 网页添加到项目](urls-in-master-pages-cs/_static/image1.png)

**图 01**： 一个新文件夹和 ASP.NET 网页添加到项目


接下来，更新`Web.sitemap`文件以包括新`<siteMapNode>`本课程中的条目。 下面的 XML 演示的完整`Web.sitemap`标记，其中现在包括添加第三个`<siteMapNode>`元素。


[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

新创建`Default.aspx`网页应该有四个内容控件对应于在四个 Contentplaceholder `Site.master`。 将一些文本添加到内容控件引用`MainContent`ContentPlaceHolder，然后访问通过浏览器页面。 如图 2 所示，在浏览器找不到`PoweredByASPNET.gif`图像文件。 这是怎么回事？

`~/Admin/Default.aspx`相同的 HTML 发送内容页`footerContent`区域，如已`About.aspx`页：


[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

因为`<img>`元素的`src`属性是相对 URL，浏览器会尝试查找`Images`web 页面的文件夹位置相对应的文件夹。 换而言之，在浏览器正在寻找的图像文件`Admin/Images/PoweredByASPNET.gif`。


[![找不到 PoweredByASPNET.gif 图像文件](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**图 02**:`PoweredByASPNET.gif`映像找不到文件 ([单击以查看实际尺寸的图像](urls-in-master-pages-cs/_static/image4.png))


### <a name="replacing-relative-urls-with-absolute-urls"></a>相对 Url 替换为绝对 Url

相对 url 反过来也*绝对 URL*，这是一个以正斜杠开头 (`/`) 或如协议`http://`。 绝对 URL 指定从已知的固定点资源的位置，因为相同的绝对 URL 是在任何 web 页面，而不考虑网站的文件夹结构中的 web 页面的位置中有效。

若要解决与图 2 所示的图像无效，我们需要更新`<img>`元素的`src`属性，以便它而不是一个相对使用绝对 URL。 若要确定正确的绝对 URL，请访问你的网站中的 web 页的其中一个，检查地址栏。 如图 2 中的地址栏所示，web 应用程序的完全限定的路径是`http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`。 因此，我们无法更新`<img>`元素的`src`属性为以下两个绝对 url:

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

请花费片刻时间来更新`<img>`元素的`src`属性使用一个如上所示的窗体的绝对 url，然后访问`~/Admin/Default.aspx`通过浏览器的页。 这一次在浏览器将正确地查找并显示`PoweredByASPNET.gif`图像文件 （请参见图 3）。


[![PoweredByASPNET.gif 映像是现在显示](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**图 03**:`PoweredByASPNET.gif`映像是现在显示 ([单击以查看实际尺寸的图像](urls-in-master-pages-cs/_static/image7.png))


中的绝对 URL 进行硬编码的工作原理，尽管它紧密到网站的服务器和文件夹位置，这可能会更改将在 HTML。 使用窗体的绝对 URL`http://localhost:3908/...`脆弱因为前面的端口号`localhost`则会自动选择每次启动 Visual Studio 的内置 ASP.NET Development Web Server。 同样，`http://localhost`一部分在本地测试时才有效。 后的代码部署到生产服务器中，URL 基将更改为其他事情，请如`http://www.yourserver.com`。 在窗体中的绝对 URL`/ASPNET_MasterPages_Tutorial_04_CS/...`还受到相同受到攻击，因为此应用程序路径通常与开发和生产服务器之间有差别。

值得高兴的是，ASP.NET 提供了用于生成在运行时有效的相对 URL 的方法。

## <a name="usingandresolveclienturl"></a>使用`~`和`ResolveClientUrl`

而是不是硬编码的绝对 URL，ASP.NET 允许页面开发人员能够使用波形符 (`~`) 以指示 web 应用程序的根目录。 例如，在本教程前面我使用了表示法`~/Admin/Default.aspx`中的文本来指代`Default.aspx`页中`Admin`文件夹。 `~`指示`Admin`文件夹是 web 应用程序的根的子文件夹。

`Control`类的[`ResolveClientUrl`方法](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx)采用 URL 和到相应控件所驻留的网页的相对 URL 对其进行修改。 例如，调用`ResolveClientUrl("~/Images/PoweredByASPNET.gif")`从`About.aspx`返回`Images/PoweredByASPNET.gif`。 从这称之为`~/Admin/Default.aspx`，但是，返回`../Images/PoweredByASPNET.gif`。

> [!NOTE]
> 因为所有 ASP.NET 服务器控件都派生自`Control`类，所有服务器控件都有权访问`ResolveClientUrl`方法。 甚至`Page`类派生自`Control`类，这意味着您可以使用此方法直接从 ASP.NET 页的代码隐藏类。


### <a name="usingin-the-declarative-markup"></a>使用`~`声明性标记中

多个 ASP.NET Web 控件包含与 URL 相关的属性： 超链接控件已`NavigateUrl`属性; 图像控件具有`ImageUrl`属性; 依此类推。 这些控件呈现时，传递到其 URL 相关的属性值`ResolveClientUrl`。 因此，如果这些属性包含`~`若要指示 web 应用程序的根目录，URL 将修改为有效的相对 URL。

请记住，只有 ASP.NET 服务器控件转换`~`在其 URL 相关的属性。 如果`~`如在静态 HTML 标记中，将出现`<img src="~/Images/PoweredByASPNET.gif" />`，ASP.NET 引擎将发送`~`到其余部分的 HTML 内容的浏览器。 在浏览器将假定`~`是 URL 的一部分。 例如，如果浏览器接收标记`<img src="~/Images/PoweredByASPNET.gif" />`它假定存在名为的子`~`具有一个子文件夹`Images`，其中包含的图像文件`PoweredByASPNET.gif`。

若要修复中的图像标记`Site.master`，替换现有`<img>`与 ASP.NET 图像 Web 控件的元素。 设置图像 Web 控件的`ID`到`PoweredByImage`，将其`ImageUrl`属性设置为`~/Images/PoweredByASPNET.gif`，并将其`AlternateText`属性设置为"提供支持的 asp.net ！"


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

对母版页进行此更改之后, 重新访问`~/Admin/Default.aspx`页。 这一次`PoweredByASPNET.gif`在页中看到的图像文件 （请参见图 3）。 当映像 Web 控件是呈现它使用`ResolveClientUrl`方法来解析其`ImageUrl`属性值。 在中`~/Admin/Default.aspx``ImageUrl`作为 HTML 源显示的以下代码片段转换为适当的相对 URL:


[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> 正在使用中基于 URL 的 Web 控件的属性，除了`~`调用时还可以使用`Response.Redirect`和`Server.MapPath`方法，等等。 此外，`ResolveClientUrl`如果需要可以直接从 ASP.NET 或母版页的声明性标记，调用方法; 请参阅[Fritz Onion](https://www.pluralsight.com/blogs/fritz/)的博客文章[Using`ResolveClientUrl`标记中](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)。


## <a name="fixing-the-master-pages-remaining-relative-urls"></a>修复主页面的剩余的相对 Url

除了`<img>`中的元素`footerContent`我们只需修复，母版页包含需要我们关注的一个更相对 URL。 `topContent`区域包括链接"主页面教程，"用于指向`Default.aspx`。


[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

因为此 URL 是相对路径，它将发送到用户`Default.aspx`他们访问的内容页的文件夹中的页。 能够始终指向此链接`Default.aspx`需要替换的根文件夹中`<a>`元素与超链接 Web 控件，以便我们可以使用`~`表示法。

删除`<a>`元素标记，并在其原位置添加超链接控件。 设置超链接的`ID`到`lnkHome`，将其`NavigateUrl`属性设置为`~/Default.aspx`，并将其`Text`属性设置为"主页面教程"。


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

就这么简单！ 现在所有呈现而不考虑哪些文件夹的内容页面的母版页和内容页面时正确基于我们的主页面中的 Url 位于中。

### <a name="automatic-url-resolution-in-theheadsection"></a>中的自动 URL 解析`<head>`部分

在中[*创建站点范围内布局使用 Master Pages* ](creating-a-site-wide-layout-using-master-pages-cs.md)教程，我们添加了`<link>`到`Styles.css`文件中`<head>`区域：


[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

虽然`<link>`元素的`href`属性是相对的它将自动转换为在运行时的相应路径。 如中所述[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中，`<head>`区域是实际服务器端控件，从而使其能够修改呈现时其内部控件的内容。

若要验证这一点，重新访问`~/Admin/Default.aspx`页面，查看发送到浏览器的 HTML 源代码。 如下面的代码段所示，`<link>`元素的`href`属性自动修改为适当的相对 URL， `../Styles.css`。


[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>总结

母版页经常包括链接、 图像和其他外部资源，必须指定通过 URL。 因为母版页和内容页可能不存在的相同文件夹中，务必 abstain 从使用相对 Url。 虽然可以使用硬编码的绝对 Url，如此严密到 web 应用程序将绝对 URL。 如果绝对 URL 发生更改-像通常那样移动或 web 应用程序的部署时将需要记住以返回并更新绝对 Url。

理想的方法是使用波形符 (`~`) 以指示应用程序根目录。 包含与 URL 相关的属性的 ASP.NET Web 控件映射`~`在运行时应用程序根目录。 Web 控件在内部，使用`Control`类的`ResolveClientUrl`方法来生成有效的相对 URL。 此方法是公共的可从每个服务器控件 (包括`Page`类)，因此您可以使用它以编程方式从您的代码隐藏类，如果需要。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 ASP.NET 中的母版页](http://www.odetocode.com/Articles/419.aspx)
- [URL 基类重定位到母版页中](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [使用`ResolveClientUrl`标记中](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [下一页](control-id-naming-in-content-pages-cs.md)
