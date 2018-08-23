---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: 确定需要进行的文件部署 (C#) |Microsoft Docs
author: rick-anderson
description: 需要从开发环境部署到生产环境的文件部分取决于 ASP.NET 应用程序是否生成我们...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: ad759cefc372f6276ce1b16beea7282d9685ef82
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825484"
---
<a name="determining-what-files-need-to-be-deployed-c"></a>确定需要进行的文件部署 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip)或[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> 需要从开发环境部署到生产环境的文件部分取决于是否使用网站模型或 Web 应用程序模型生成 ASP.NET 应用程序。 了解有关这两个项目模型以及项目模型如何影响部署的详细信息。


## <a name="introduction"></a>介绍

ASP.NET web 应用程序部署时，需要将与 ASP.NET 相关的文件从开发环境复制到生产环境。 与 ASP.NET 相关的文件包括 ASP.NET web 页面标记和代码和客户端和服务器端支持的文件。 客户端的支持文件是由您的 web 页面引用，并直接发送到浏览器的图像、 CSS 文件和 JavaScript 文件，例如这些文件。 服务器端的支持文件包括用于在服务器端处理某个请求。 这包括对 SQL 文件，以及其他配置文件、 web 服务、 类文件、 类型化数据集和 LINQ。

一般情况下，所有客户端的支持文件应都复制从开发环境到生产环境中，但服务器端支持的文件会都复制取决于是否进行显式编译的服务器端代码为程序集 ( `.dll`文件) 或如果有自动生成这些程序集。 突出显示了本教程，需要显式为程序集而不会自动执行此编译步骤编译代码时，要部署的文件。

## <a name="explicit-compilation-versus-automatic-compilation"></a>显式编译，而不是自动编译

ASP.NET 网页划分为标记和源代码的声明性代码。 声明性标记部分包括 HTML、 Web 控件和数据绑定语法;代码部分包含用 Visual Basic 或 C# 代码编写事件处理程序。 标记和代码部分通常分到多个不同的文件：`WebPage.aspx`包含的声明性标记时`WebPage.aspx.cs`包含代码。

请考虑名为 Clock.aspx 包含其文本属性设置为当前日期和时间加载页面时，一个标签控件的 ASP.NET 页。 声明性标记部分 (在`Clock.aspx`) 将包含标签 Web 控件的标记`<asp:Label runat="server" id="TimeLabel" />`-时的代码部分 (在`Clock.aspx.cs`) 必须`Page_Load`事件处理程序使用以下代码：

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

为了使此页上，该页面的代码部分为请求提供服务的 ASP.NET 引擎 (`WebPage.aspx.cs`文件) 必须首先将其编译。 显式或自动，可能会发生此编译。

如果编译是显式，则整个应用程序的源代码编译到一个或多个程序集 (`.dll`文件) 位于应用程序的`Bin`目录。 如果编译自动发生，则生成自动生成程序集，默认情况下为置于`Temporary ASP.NET`Files 文件夹，请参阅`%WINDOWS%\Microsoft.NET\Framework\` *&lt;版本&gt;*，尽管此位置是可通过配置[`<compilation>`元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中`Web.config`。 必须使用显式编译采取一些措施来将 ASP.NET 应用程序的代码编译为程序集，并在部署前会执行此步骤。 与自动编译在编译过程发生在 web 服务器上首次访问资源时。

无论何种编译模式使用时，所有 ASP.NET 页面的标记部分 (`WebPage.aspx`文件) 需要复制到生产环境。 您需要注册中的程序集将复制与显式编译`Bin`文件夹中，但不是需要复制 ASP.NET 页的代码的各个部分 (`WebPage.aspx.cs`文件)。 使用自动编译，您需要为复制的代码部分文件，以便代码，可以访问页面时自动编译。 每个 ASP.NET web 页面的标记部分包括`@Page`具有属性，指示是否已显式编译页面的关联的代码时，或者它是否需要自动编译指令。 因此，在生产环境可以无缝使用任一编译模型，不需要应用任何特殊的配置设置，以指示使用显式或自动编译。

表 1 总结了要部署使用自动编译与显式编译时，不同的文件。 请注意，而不考虑编译模型使用您应始终将部署中的程序集`Bin`文件夹中，如果该文件夹存在。 `Bin`文件夹包含的程序集特定于 web 应用程序，其中包括使用显式编译模型时的已编译的源代码。 `Bin`目录还包含其他项目中的程序集和您可以使用任何开放源代码或第三方程序集，它们需要在生产服务器上。 因此，作为常规经验，将复制`Bin`直到生产部署时的文件夹。 (如果正在使用自动编译模型并且未使用任何外部程序集则不会有`Bin`目录的确定 ！)

| **编译模式** | **部署标记部分文件？** | **部署源代码文件？** | **部署中的程序集`Bin`目录？** |
| --- | --- | --- | --- |
| 显式编译 | 是 | No | 是 |
| 自动编译 | 是 | 是 | 是 （如果存在） |

**表 1:** 部署哪些文件取决于所使用的编译模型。

## <a name="taking-a-trip-down-memory-lane"></a>内存游

使用哪些编译的方法取决于，情况情况下，如何在 Visual Studio 中管理 ASP.NET 应用程序。 由于。在 2000 年发生了四个不同版本的 Visual Studio-Visual Studio.NET 2002年、 Visual Studio.NET 2003年中，Visual Studio 2005 和 Visual Studio 2008 中的 NET 的开始。 Visual Studio.NET 2002年和 2003年管理 ASP.NET 应用程序使用*Web 应用程序项目模型*。 Web 应用程序项目模型的关键功能包括：

- 构成该项目在单个项目文件中定义的文件。 未在项目文件中定义的任何文件 Visual Studio 不考虑 web 应用程序的一部分。
- 使用显式编译。 生成项目将在项目中的代码文件编译为位于中的单个程序集`Bin`文件夹。

Microsoft 发布了 Visual Studio 2005 他们删除 Web 应用程序项目模型的支持，它替换为网站项目模型。 网站项目模型中区分基本和本身从 Web 应用程序项目模型通过以下方式：

- 而不是让明确指出项目的文件的单个项目文件，而使用文件系统。 简单地说，web 应用程序文件夹 （或子文件夹） 中的任何文件被视为该项目的一部分。
- 构建 Visual Studio 中的项目不会创建中的程序集`Bin`目录。 相反，构建 Web 站点项目报告任何编译时错误。
- 对自动编译支持。 通过将标记和源代码代码复制到生产环境中，通常部署网站项目，但代码可以是预编译 （显式编译）。

Microsoft 发布 Visual Studio 2005 Service Pack 1 时恢复 Web 应用程序项目模型。 但是，Visual Web Developer 不断仅支持网站项目模型。 值得高兴的是 Visual Web Developer 2008 Service Pack 1 已删除此限制。 现在可以在 Visual Studio （和 Visual Web Developer），它使用 Web 应用程序项目模型或网站项目模型中创建 ASP.NET 应用程序。 这两种模型有其优点和缺点。 请参阅[Web 应用程序项目简介： 比较网站项目和 Web 应用程序项目](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5)进行比较的两个模型，并可以帮助您决定哪些项目模型最适合于您的具体情况。

## <a name="exploring-the-sample-web-application"></a>浏览示例 Web 应用程序

对于本教程的此下载包括调用书评的 ASP.NET 应用程序。 网站模仿有人可能会创建一个爱好网站共享他们的著作评审与在线社区。 此 ASP.NET web 应用程序非常简单，它包含的以下资源：

- `Web.config`应用程序的配置文件。
- 母版页 (`Site.master`)。
- 七个不同的 ASP.NET 页： 

    - ~`/Default.aspx`-站点的主页。
    - ~`/About.aspx` -"有关站点"页。
    - ~`/Fiction/Default.aspx` -列出已经过检查小说书籍的页面。 

        - ~`/Fiction/Blaze.aspx` -检查 Richard Bachman 小说*Blaze*。
    - ~/`Tech/Default.aspx` -列出已经过检查本技术书籍的页面。 

        - ~/`Tech/CYOW.aspx`-审查*创建您自己的网站*。
        - ~/`Tech/TYASP35.aspx` -审查*教您自己 ASP.NET 3.5 24 小时内*。
- 在样式文件夹中的三个不同 CSS 文件。
- 四个图像文件的 ASP.NET 徽标和图像的三个已审阅丛书在后台通过提供支持的所有位于`Images`文件夹。
- 一个`Web.sitemap`文件，它定义了站点地图并用于显示中的菜单`Default.aspx`根目录中的网页和`Fiction`和`Tech`文件夹。
- 名为的类文件`BasePage.cs`，它定义基`Page`类。 此类扩展的功能`Page`类的自动设置`Title`属性基于站点图中的页面的位置。 简单地说，任何 ASP.NET 代码隐藏类的扩展`BasePage`(而不是`System.Web.UI.Page`) 将具有其标题设置为值具体取决于其站点图中的位置。 例如，在查看时 ~ /`Tech/CYOW.aspx`页上，标题设置为"主文件夹:: 技术:: 创建您自己的网站"。

图 1 显示了书评网站的浏览器查看时的屏幕截图。 此处可以看到页面 ~ /`Tech/TYASP35.aspx`，该评审本书*教您自己 ASP.NET 3.5 24 小时内*。 跨越页和左侧列中的菜单的顶部痕迹导航基于站点地图结构中定义`Web.sitemap`。 在右上角中的图像是一个通讯簿封面图像位于`Images`文件夹。 通过级联样式表规则拼 Styles 文件夹中的 CSS 文件在主页上，定义总体的页面布局时定义网站的外观和感觉`Site.master`。


[![通讯簿评审网站提供了具有多种类型的标题上的评论](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**图 1:** 通讯簿评审网站提供了具有多种类型的标题上的评论 ([单击以查看实际尺寸的图像](determining-what-files-need-to-be-deployed-cs/_static/image3.png))


此应用程序不使用站点数据库。每个评审为单独的 web 页面在应用程序中实现。 本教程 （和下一步的多个教程） 演练部署不具有数据库的 web 应用程序。 但是，在将来的教程中我们将增强存储评审、 读者评论和其他信息在数据库中，此应用程序并将了解需要执行正确部署数据驱动的 web 应用程序的步骤。

> [!NOTE]
> 这些教程重点介绍承载 ASP.NET 应用程序与 web 宿主提供程序并不浏览等 ASP 辅助主题。NET 的站点映射系统或使用基`Page`类。 有关这些技术的详细信息和在本教程涉及的其他主题的更多背景，请参阅更多参考资料部分末尾的每个教程。


本教程中的下载具有 web 应用程序的两个副本，每个实现为不同的 Visual Studio 项目类型： BookReviewsWAP、 Web 应用程序项目和 BookReviewsWSP，网站项目。 这两个项目使用 Visual Web Developer 2008 SP1 创建的并使用 ASP.NET 3.5 SP1。 若要使用这些项目，启动通过解压缩到您的桌面的内容。 若要打开 Web 应用程序项目 (BookReviewsWAP)，导航到 BookReviewsWAP 文件夹并双击解决方案文件、 `BookReviewsWAP.sln`。 若要打开的网站项目 (BookReviewsWSP)，启动 Visual Studio，然后，从文件菜单中，选择打开网站选项，浏览到`BookReviewsWSP`文件夹在桌面上，单击确定。


在此教程查看哪些文件中的其余两个部分将需要部署该应用程序时将复制到生产环境。 接下来两个教程- *[部署您的站点使用 FTP](deploying-your-site-using-an-ftp-client-cs.md)* 并*[部署您站点使用的 Visual Studio](deploying-your-site-using-visual-studio-cs.md)*  -显示不同的方式将这些文件复制到 web 宿主提供程序。

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>确定要部署的 Web 应用程序的文件

Web 应用程序项目模型使用显式编译-项目的源代码编译到单个程序集生成应用程序每次。 此编译包括 ASP.NET 页的代码隐藏文件 (~ /`Default.aspx.cs`，~ /`About.aspx.cs`，依次类推)，并将`BasePage.cs`类。 生成的程序集名为 BookReviewsWAP.dll，它位于应用程序的`Bin`目录。

图 2 显示了构成了通讯簿评审 Web 应用程序项目的文件。


[![在解决方案资源管理器列出了构成 Web 应用程序项目的文件](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**图 2**: 解决方案资源管理器列出了构成 Web 应用程序项目的文件


若要部署 ASP.NET 应用程序使用开发 Web 应用程序项目模型开始通过构建应用程序，以便显式编译为程序集的最新的源代码。 接下来，将以下文件复制到生产环境：

- 文件包含在声明性标记的每个 ASP.NET 页，如 ~ /`Default.aspx`，~ /`About.aspx`，依次类推。 此外，复制了任何主页面和用户控件的声明性标记。
- 程序集 (`.dll`文件) 中`Bin`文件夹。 不需要的程序数据库文件复制 (`.pdb`) 或可能会发现中的任何 XML 文件`Bin`目录。

不需要将 ASP.NET 页的源代码文件复制到生产环境中，也不需要复制`BasePage.cs`类文件。

> [!NOTE]
> 如图 2 所示，`BasePage`类实现为类文件在项目中，在名为的文件夹中放置`HelperClasses`。 编译项目时中的代码`BasePage.cs`文件编译到单个程序集，以及 ASP.NET 页的代码隐藏类`BookReviewsWAP.dll.`ASP.NET 具有一个名为的特殊文件夹`App_Code`用于保存 Web 类文件网站项目。 中的代码`App_Code`文件夹自动编译并因此不应使用与 Web 应用程序项目。 相反，应将应用程序的类文件放在名为的普通文件夹`HelperClasses`，或`Classes`，或类似。 或者，可以将类文件放在单独的类库项目。


除了复制与 ASP.NET 相关的标记文件和中的程序集`Bin`文件夹中，您还需要将客户端的支持文件的图像和 CSS 文件的复制的其他服务器端的支持文件，以及`Web.config`和`Web.sitemap`。 这些客户端和服务器端需要支持文件复制到生产环境，而不管您使用显式或自动编译。

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>确定要部署的 Web 站点项目文件的文件

网站项目模型支持自动进行编译，没有使用 Web 应用程序项目模型时的功能。 与显式编译必须编译为程序集的项目的源代码，并将该程序集复制到生产环境。 但是，与自动编译您只需将源代码复制到生产环境，并且根据需要由按需运行时编译。

在 Visual Studio 中的生成菜单选项中不存在 Web 应用程序项目和网站项目。 构建 Web 应用程序项目将项目的源代码编译到单个程序集位于`Bin`目录; 构建 Web 站点项目检查是否有任何编译时错误，但不会创建任何程序集。 若要部署 ASP.NET 应用程序使用网站项目模型开发所有需要执行是复制到生产环境中，相应的文件，但我建议您对第一次生成项目以确保没有任何编译时错误。

图 3 显示了构成了通讯簿评审网站项目的文件。


 [![在解决方案资源管理器列出了构成网站项目的文件](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**图 3**: 解决方案资源管理器列出了构成网站项目的文件


部署网站项目涉及将所有与 ASP.NET 相关的文件复制到生产环境-包含 ASP.NET 页、 母版页和用户控件的标记页及其代码文件。 此外需要将任何类文件，如 BasePage.cs 复制。 请注意，`BasePage.cs`文件位于`App_Code`文件夹中，这是一个类文件在网站项目中使用的特殊 ASP.NET 文件夹。 特殊文件夹需要在生产环境，以及创建中的类文件作为`App_Code`开发环境上的文件夹必须复制到`App_Code`生产上的文件夹。

除了复制 ASP.NET 标记和源的代码文件，您还需要将客户端的支持文件的图像和 CSS 文件的复制的其他服务器端的支持文件，以及`Web.config`和`Web.sitemap`。

> [!NOTE]
> 网站项目还可以使用显式编译。 以后的教程将探讨如何显式编译的网站项目。


## <a name="summary"></a>总结

部署 ASP.NET 应用程序时，需要将所需的文件从开发环境复制到生产环境。 精确的需要进行同步的文件集取决于是否 ASP.NET 应用程序的显式或自动编译代码。 是否配置 Visual Studio 会影响编译策略来管理使用 Web 应用程序项目模型或网站项目模型的 ASP.NET 应用程序。

Web 应用程序项目模型使用显式编译，并将项目的代码编译为单个程序集在`Bin`文件夹。 部署应用程序、 ASP.NET 页的标记部分的内容时`Bin`文件夹必须推送到生产环境; 不需要在应用程序中的代码文件和代码隐藏类的源代码若要将复制到生产环境。

网站项目模型默认情况下，使用自动编译，但也可以显式编译的网站项目中，我们会在将来教程。 部署使用自动编译的 ASP.NET 应用程序需要的标记部分*和*源代码必须复制到生产环境。 第一次请求时在生产环境中自动编译代码。

现在，我们所要具备需要开发和生产环境之间进行同步的文件我们已做好部署到 web 主机提供商书评应用程序。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 编译概述](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [正在检查 ASP。NET 的 Site navigation — 站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Web 应用程序项目简介](https://msdn.microsoft.com/library/aa730880.aspx)
- [主页面教程](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [页间共享代码](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [将自定义的基本类用于 ASP.NET 页的代码隐藏类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005 Web 站点项目系统： 它是什么和为什么我们做了它？](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [演练： 将网站项目转换为 Visual Studio 中的 Web 应用程序项目](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [上一页](asp-net-hosting-options-cs.md)
> [下一页](deploying-your-site-using-an-ftp-client-cs.md)
