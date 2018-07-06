---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
title: 多个 Contentplaceholder 和默认内容 (VB) |Microsoft Docs
author: rick-anderson
description: 介绍如何将多个内容占位符添加到主页面，以及如何在内容的占位符中指定默认的内容。
ms.author: aspnetcontent
ms.date: 05/21/2008
ms.assetid: 866a7177-6884-451e-88f4-c934b1dd1af5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
msc.type: authoredcontent
ms.openlocfilehash: 98cb78e03f9f7aff4a36625416188aba04512f6a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839695"
---
<a name="multiple-contentplaceholders-and-default-content-vb"></a>多个 Contentplaceholder 和默认内容 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_VB.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_VB.pdf)

> 介绍如何将多个内容占位符添加到主页面，以及如何在内容的占位符中指定默认的内容。


## <a name="introduction"></a>介绍

在前面的教程，我们探讨母版页启用 ASP.NET 开发人员能够创建一致的网站的布局。 母版页定义普遍适用于所有内容页面的标记和是按页按可自定义的区域。 在上一教程中，我们将创建一个简单的主页面 (`Site.master`) 和两个内容页 (`Default.aspx`和`About.aspx`)。 我们的主页面包含名为两个 Contentplaceholder`head`并`MainContent`，其位于`<head>`元素和 Web 窗体，分别。 尽管内容页都有两个内容控件，我们仅指定对应于一个标记`MainContent`。

中的两个 ContentPlaceHolder 控件众多`Site.master`，主页面可能包含多个 Contentplaceholder。 更重要的是，主页面可以指定 ContentPlaceHolder 控件的默认标记。 内容页中，然后，可以根据需要指定其自身标记或使用默认标记。 在本教程中我们看看在母版页中使用多个内容控件，并了解如何定义 ContentPlaceHolder 控件中的默认标记。

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>步骤 1： 将其他 ContentPlaceHolder 控件添加到母版页

许多网站设计包含在屏幕上按页基础自定义的多个区域。 `Site.master`我们在前面的教程中创建的主页面包含名为 Web 窗体中的单个 ContentPlaceHolder `MainContent`。 具体而言，是位于此 ContentPlaceHolder `mainContent` `<div>`元素。

图 1 显示了`Default.aspx`时的浏览器查看。 用红线圈出的区域是与对应的特定于页面的标记`MainContent`。


[![带圆圈的区域显示的区域目前可自定义基于按页](multiple-contentplaceholders-and-default-content-vb/_static/image2.png)](multiple-contentplaceholders-and-default-content-vb/_static/image1.png)

**图 01**： 有圆形区域显示区域目前可自定义基于页的页 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image3.png))


假设，除了图 1 所示的区域，我们还需要将特定于页面的项添加到左侧列下方的课程和新闻部分。 若要实现此目的，我们将另一个 ContentPlaceHolder 控件添加到母版页。 若要跟着介绍一起操作，请打开`Site.master`母版页 Visual Web Developer 中，然后将 ContentPlaceHolder 控件从工具箱拖到设计器后的新闻部分。 设置 ContentPlaceHolder`ID`到`LeftColumnContent`。


[![将 ContentPlaceHolder 控件添加到母版页左侧的列](multiple-contentplaceholders-and-default-content-vb/_static/image5.png)](multiple-contentplaceholders-and-default-content-vb/_static/image4.png)

**图 02**： 将 ContentPlaceHolder 控件添加到母版页的左侧列 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image6.png))


通过添加`LeftColumnContent`母版页 ContentPlaceHolder，我们可以将此区域的内容按页地定义通过包含内容控件在页`ContentPlaceHolderID`设置为`LeftColumnContent`。 我们将介绍此过程的步骤 2。

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>步骤 2： 在内容页面中定义新 ContentPlaceHolder 的内容

Visual Web Developer 时将新的内容页面添加到该网站，会自动创建一个内容控件中所选的主页面中的每个 ContentPlaceHolder 的页。 添加了`LeftColumnContent`到在步骤 1 中，现在新 ASP.NET 页面将我们母版页 ContentPlaceHolder 具有三个内容控件。

为了说明这一点，请将新的内容页面添加到名为的根目录`MultipleContentPlaceHolders.aspx`绑定到`Site.master`母版页。 Visual Web Developer 中创建包含以下声明性标记此页面：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample1.aspx)]

输入一些内容到内容控件引用`MainContent`Contentplaceholder (`Content2`)。 接下来，添加以下标记到`Content3`内容控件 (引用`LeftColumnContent`ContentPlaceHolder):

[!code-html[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample2.html)]

添加此标记后, 访问通过浏览器页面。 如图 3 所示，标记放入`Content3`（用红线圈出） 的新闻部分下的左侧列中显示内容控件。 标记放入`Content2`（蓝色圆圈） 页的右侧部分中显示。


[![左侧的列现在包含新闻部分下的特定于页面的内容](multiple-contentplaceholders-and-default-content-vb/_static/image8.png)](multiple-contentplaceholders-and-default-content-vb/_static/image7.png)

**图 03**: 左侧列现在包含特定于页面的内容下方新闻部分 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image9.png))


### <a name="defining-content-in-existing-content-pages"></a>在现有内容页面中定义的内容

创建新的内容页面会自动集成了我们在步骤 1 中添加的 ContentPlaceHolder 控件。 但我们两个现有内容页面-`About.aspx`并`Default.aspx`-没有为内容控件`LeftColumnContent`ContentPlaceHolder。 若要指定此 ContentPlaceHolder 这些两个现有页面中的内容，我们需要自行添加内容控件。

不同于大多数 ASP.NET Web 控件，Visual Web Developer 工具箱不包括的内容控件项。 我们可以手动键入内容控件声明性标记中为源视图中，但更方便和快捷的方法是使用设计视图。 打开`About.aspx`页上，并切换到设计视图。 如图 4 所示， `LeftColumnContent` ContentPlaceHolder 将出现在设计视图; 如果鼠标悬停时，将显示的标题显示为:"LeftColumnContent （主）"。 "Master"的标题中包含指示没有为此 ContentPlaceHolder 定义页中的内容控件。 如果那里存在 ContentPlaceHolder，如下所示的内容控件`MainContent`，将读取标题:"*ContentPlaceHolderID* （自定义）。"

若要添加的内容控件`LeftColumnContent`ContentPlaceHolder 到`About.aspx`、 展开 ContentPlaceHolder 的智能标记，然后单击创建自定义内容链接。


[![About.aspx 的设计视图显示了 LeftColumnContent ContentPlaceHolder](multiple-contentplaceholders-and-default-content-vb/_static/image11.png)](multiple-contentplaceholders-and-default-content-vb/_static/image10.png)

**图 04**: 设计视图`About.aspx`演示`LeftColumnContent`ContentPlaceHolder ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image12.png))


单击创建自定义内容链接生成所需的内容控件中的页和集及其`ContentPlaceHolderID`属性设置为 ContentPlaceHolder `ID`。 例如，单击用于创建自定义内容的链接`LeftColumnContent`区域中的`About.aspx`向页面添加以下声明性标记：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>省略内容控件

ASP.NET 不需要所有内容页面的母版页中定义的每个 ContentPlaceHolder 包含内容控件。 如果省略某个内容控件，则 ASP.NET 引擎使用 ContentPlaceHolder 在母版页中定义的标记。 此标记被称为 ContentPlaceHolder*默认内容*和其中内容的某些区域所共有的大部分页，但需要进行自定义对于少量的页面的情况下非常有用。 步骤 3 介绍了在母版页中指定的默认内容。

目前，`Default.aspx`包含两个内容控件`head`并`MainContent`Contentplaceholder; 它不具有的内容控件`LeftColumnContent`。 因此，当`Default.aspx`呈现`LeftColumnContent`使用 ContentPlaceHolder 的默认内容。 因为我们尚未为此 ContentPlaceHolder 定义默认的任何内容的净效果是，没有标记，将发出此区域。 若要验证此行为，请访问`Default.aspx`通过浏览器。 如图 5 所示，没有标记，将发出新闻部分下的左侧列中。


[![为 LeftColumnContent ContentPlaceHolder 不呈现任何内容](multiple-contentplaceholders-and-default-content-vb/_static/image14.png)](multiple-contentplaceholders-and-default-content-vb/_static/image13.png)

**图 05**： 无内容呈现用于`LeftColumnContent`ContentPlaceHolder ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image15.png))


## <a name="step-3-specifying-default-content-in-the-master-page"></a>步骤 3： 在母版页中指定默认的内容

一些网站设计包括其内容是相同的一个或两个例外情况除外站点中的所有页面的区域。 支持用户帐户的网站为例。 此类的网站需要可以在其中访问者输入其凭据以登录到网站的登录页。 要加快在登录过程，网站设计人员可能包括每一页，以允许用户登录而无需显式访问登录页面左上角的用户名和密码的文本框。 虽然这些用户名和密码文本框很有用大多数页面中，它们是冗余的登录页，其中已包含用户的凭据的文本框。

若要实现这种设计，可以在主页面左上角中创建 ContentPlaceHolder 控件。 显示其左上角的用户名和密码文本框所需的每个页将创建用于此 ContentPlaceHolder 的内容控件并添加所需的接口。 登录页上，但是，也会忽略为此 ContentPlaceHolder 添加内容控件，或将创建一个内容控件不带标记定义。 这种方法的缺点是我们不必记住要将用户名和密码文本框添加到每个页上，我们将添加到站点 （除外的登录名页中）。 这请求时遇到问题。 我们可能会忘记将这些文本框添加到一个页面或两个或更糟的是，我们可能不实现接口正确 （可能添加一个文本框中的而不是两个）。

更好的解决方案是将用户名和密码文本框定义为 ContentPlaceHolder 的默认内容。 这样，我们只需重写此默认内容中不显示用户名和密码文本框的几个页面 （例如的登录页）。 为了说明 ContentPlaceHolder 控件指定默认内容，让我们来实现刚刚所讨论的方案。

> [!NOTE]
> 本教程的其余部分更新我们的网站的所有页面，但登录页的左侧列中包括的登录界面。 但是，本教程不检查如何配置网站，以支持用户帐户。 有关本主题的详细信息，请参阅我[窗体身份验证、 授权、 用户帐户和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教程。


### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>添加 ContentPlaceHolder 并指定自己的默认内容

打开`Site.master`母版页并将以下标记添加到左侧的列之间`DateDisplay`标签和课程部分：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample4.aspx)]

以后将此标记添加到母版页的设计视图中看起来应类似于图 6。


[![母版页包含登录控件](multiple-contentplaceholders-and-default-content-vb/_static/image17.png)](multiple-contentplaceholders-and-default-content-vb/_static/image16.png)

**图 06**: 母版页包含登录控件 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image18.png))


此 ContentPlaceHolder `QuickLoginUI`，具有一个登录 Web 控件作为其默认内容。 Login 控件显示提示用户输入其用户名和密码登录按钮以及一个用户界面。 单击登录按钮，登录控件在内部验证针对成员身份 API 的用户的凭据。 若要使用此登录名控件在实践中，然后，需要配置站点，以使用成员身份。 本主题不在本教程; 的范围内请参阅我[窗体身份验证、 授权、 用户帐户和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教程构建的 web 应用程序支持用户帐户的详细信息。

随意自定义登录控件的行为或外观。 我已设置其两个属性：`TitleText`和`FailureAction`。 `TitleText`属性值，该值默认为"登录"，显示顶部的控件的用户界面。 我已将此属性设置，以便它显示为"登录"的文本`<h3>`元素。 `FailureAction`属性指示要执行的操作如果用户的凭据无效。 它将默认值为`Refresh`，用于将用户留在同一页上，并显示登录控件内的失败消息。 我已更改到`RedirectToLoginPage`，后者将用户发送到登录页出现时的凭据无效。 我喜欢将用户发送到登录页上，当用户尝试登录从其他页面上，但会失败，因为登录页面可以包含其他说明和无法轻松地适应左侧列的选项。 例如，登录页可能包括选项可以检索忘记了的密码或创建新的帐户。

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>创建登录页和重写默认内容

与完整母版页后下, 一步是创建的登录页。 将 ASP.NET 页面添加到名为你网站的根目录`Login.aspx`，将其绑定到`Site.master`母版页。 执行此操作将创建具有四个内容控件的页、 一个用于每个 Contentplaceholder 中定义`Site.master`。

添加到登录控件`MainContent`内容控件。 同样，随意添加任何内容到`LeftColumnContent`区域。 但是，请务必选中的内容控件`QuickLoginUI`ContentPlaceHolder 为空。 这将确保控件不会出现在登录页的左侧列中的登录名。

定义的内容后`MainContent`和`LeftColumnContent`区域，登录页的声明性标记应如下所示：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample5.aspx)]

图 7 显示时的浏览器查看此页。 因为此页上指定的内容控件`QuickLoginUI`ContentPlaceHolder，它将替代指定母版页中的默认内容。 实际效果是登录控件显示在母版页的设计视图 （请参阅图 6） 将不呈现在此页。


[![登录页 Represses QuickLoginUI ContentPlaceHolder 默认内容](multiple-contentplaceholders-and-default-content-vb/_static/image20.png)](multiple-contentplaceholders-and-default-content-vb/_static/image19.png)

**图 07**: 登录页 Represses `QuickLoginUI` ContentPlaceHolder 的默认内容 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image21.png))


### <a name="using-the-default-content-in-new-pages"></a>在新页中使用的默认内容

我们想要在除登录页的所有页的左侧列中显示登录控件。 若要实现此目的，除外的登录页的所有内容页面应省略的内容控件`QuickLoginUI`ContentPlaceHolder。 通过省略内容控件，将改为使用 ContentPlaceHolder 的默认内容。

现有内容页面- `Default.aspx`， `About.aspx`，并`MultipleContentPlaceHolders.aspx`-不包含的内容控件`QuickLoginUI`因为之前我们该 ContentPlaceHolder 控件添加到母版页创建它们。 因此，不需要这些现有页面进行更新。 但是，新页添加到该网站包含的内容控件`QuickLoginUI`ContentPlaceHolder，默认情况下。 因此，我们不得不请记得删除这些内容控制每次我们添加一个新的内容页面 （除非我们想要重写 ContentPlaceHolder 的默认内容，例如登录页）。

若要删除内容控件，您可以手动从源视图中删除其声明性标记或时，从设计视图中，选择默认为母版页的内容链接从其智能标记。 这两种方法中删除内容控件从页面并生成相同的净效果。

图 8 显示了`Default.aspx`时的浏览器查看。 请记住，`Default.aspx`仅有两个内容控件在其声明性标记中的另一个用于指定`head`，另一个用于`MainContent`。 因此，默认值的内容`LeftColumnContent`和`QuickLoginUI`Contentplaceholder 会显示。


[![显示内容默认 LeftColumnContent 和 QuickLoginUI Contentplaceholder](multiple-contentplaceholders-and-default-content-vb/_static/image23.png)](multiple-contentplaceholders-and-default-content-vb/_static/image22.png)

**图 08**: 默认的内容`LeftColumnContent`并`QuickLoginUI`Contentplaceholder 显示 ([单击以查看实际尺寸的图像](multiple-contentplaceholders-and-default-content-vb/_static/image24.png))


## <a name="summary"></a>总结

ASP.NET 母版页模型允许任意数目的 Contentplaceholder 母版页中。 什么是多个，Contentplaceholder 包括默认的内容，它在没有对应的情况下，将发出内容在内容页中的控件。 在本教程中我们了解了如何在母版页中包含其他 ContentPlaceHolder 控件以及如何为新的和现有 ASP.NET 页面中的这些新 Contentplaceholder 定义内容控件。 我们还了解了指定默认值在 ContentPlaceHolder 中内容的情况下非常有用，只有极少的页需要自定义否则其中标准化特定的区域中的内容。

在下一教程中我们将介绍`head`ContentPlaceHolder 更详细地了解如何以声明方式和以编程方式定义的标题、 元标记和其他 HTML 标头按页基础上。

快乐编程 ！

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Suchi Banerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](creating-a-site-wide-layout-using-master-pages-vb.md)
> [下一页](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
