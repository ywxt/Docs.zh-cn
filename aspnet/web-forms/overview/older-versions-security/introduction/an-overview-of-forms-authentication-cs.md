---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
title: 窗体身份验证 (C#) 的概述 |Microsoft Docs
author: rick-anderson
description: 创建自定义路由
ms.author: aspnetcontent
ms.date: 01/14/2008
ms.assetid: de2d65b9-aadc-42ba-abe1-4e87e66521a0
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: a523e3c6ff79e7445813e2ef50eabc5b55d00144
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814441"
---
<a name="an-overview-of-forms-authentication-c"></a>窗体身份验证 (C#) 的概述
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_CS.zip)或[下载 PDF](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_cs.pdf)

> 在本教程中我们将只讨论到的新实现。具体而言，我们将介绍在实现窗体身份验证。 我们开始构造在本教程中的 web 应用程序将继续在基础上构建在后续教程中，随着我们从简单的窗体身份验证到成员资格和角色。
> 
> 有关此主题，请参阅此视频，详细信息：[使用基本窗体中的身份验证 ASP.NET](# "using-basic-forms-authentication-in-aspnet")。


## <a name="introduction"></a>介绍

在中[前面的教程](security-basics-and-asp-net-support-cs.md)我们讨论了 ASP.NET 提供的各种身份验证、 授权和用户帐户选项。 在本教程中我们将只讨论到的新实现。具体而言，我们将介绍在实现窗体身份验证。 我们开始构造在本教程中的 web 应用程序将继续在基础上构建在后续教程中，随着我们从简单的窗体身份验证到成员资格和角色。

本教程开始深入探讨了窗体身份验证工作流，我们在上一教程中介绍的主题。 接下来，我们将创建一个 ASP.NET 网站用来演示窗体身份验证的概念。 接下来，我们会将站点配置为使用 forms 身份验证，创建一个简单的登录页，并了解如何确定，在代码中，是否对用户身份验证，如果是这样，用户名他们登录时使用。

了解窗体身份验证工作流，使其在 web 应用程序，并创建登录名和注销页是在生成的 ASP.NET 应用程序支持用户帐户，并通过 web 页面的用户进行身份验证过程中的所有重要步骤。 正因为如此 – 因为这些教程制作的其他-我建议您就可以完成本教程中完全之前移至下一个即使你已有有体验配置窗体身份验证在过去的项目中。

## <a name="understanding-the-forms-authentication-workflow"></a>了解窗体身份验证工作流

当 ASP.NET 运行时处理对于 ASP.NET 资源，例如 ASP.NET 页或 ASP.NET Web 服务请求时请求在其生命周期期间引发事件的数。 当前请求的请求进行身份验证和授权，在未经处理的异常和等的情况下引发的事件时引发的非常初级和非常结束时引发的事件。 若要查看事件的完整列表，请参阅[HttpApplication 对象的事件](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)。

*HTTP 模块*是在响应特定事件在请求生命周期中执行其代码的托管的类。 ASP.NET 附带有多个执行的基本任务在后台的 HTTP 模块。 尤其是与我们讨论的两个内置的 HTTP 模块包括：

- **[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** – 对用户进行身份验证通过检查通常包含用户的 cookie 集合中的窗体身份验证票证。 如果存在任何窗体身份验证票证，不则该用户是匿名的。
- **[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** – 确定当前用户是否有权访问所请求的 URL。 此模块通过咨询应用程序的配置文件中指定的授权规则来确定该颁发机构。 ASP.NET 还提供了[ `FileAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) ，它确定颁发机构咨询服务的请求的文件的 Acl。

`FormsAuthenticationModule`尝试之前的用户进行身份验证`UrlAuthorizationModule`(和`FileAuthorizationModule`) 执行。 如果发出请求的用户无权访问请求的资源，授权模块终止请求，并返回[HTTP 401 未授权](http://www.checkupdown.com/status/E401.html)状态。 在 Windows 身份验证方案，HTTP 401 状态将返回到浏览器。 此状态代码会导致浏览器，以提示用户输入其凭据通过模式对话框。 使用窗体身份验证，但是，HTTP 401 未授权状态是永远不会发送到浏览器因为 FormsAuthenticationModule 检测到此状态，并修改它以将用户重定向到登录页面而是 (通过[HTTP 302 重定向](http://www.checkupdown.com/status/E302.html)状态)。

登录页的职责是确定是否在用户的凭据是否有效，如果是这样，若要创建窗体身份验证票证，并将用户重定向回页它们正在尝试的访问。 对网站的页面上的后续请求中包含身份验证票证的`FormsAuthenticationModule`用于标识用户。


![窗体身份验证工作流](an-overview-of-forms-authentication-cs/_static/image1.png)

**图 1**： 窗体身份验证工作流


### <a name="remembering-the-authentication-ticket-across-page-visits"></a>记住跨页面访问的身份验证票证

登录后，窗体身份验证票证必须发送回 web 服务器上每个请求，以便在浏览站点时，保持已登录的用户。 这通常通过将身份验证票证放在用户的 cookie 集合中。 [Cookie](http://en.wikipedia.org/wiki/HTTP_cookie)是驻留在用户计算机上，在创建 cookie 的网站的每个请求的 HTTP 标头中传输的小文本文件。 因此，一旦创建并存储在浏览器 cookie 中的窗体身份验证票证，对该站点的每个后续访问对将发送请求，从而在识别用户以及身份验证票证。

Cookie 的一个方面是其过期，这是日期和时间在浏览器将放弃该 cookie。 窗体身份验证 cookie 过期后，可以不再进行身份验证并因此成为匿名用户。 当用户从公共终端来访时，很可能它们希望其身份验证票证过期时它们关闭其浏览器。 当来访从主页时，通过但是，相同的用户可能想要记住在浏览器重新启动时，这样它们不具有的身份验证票证在每次访问该站点中重新登录。 此决定通常由用户在的"记住我"窗体中的登录页上的复选框。 在步骤 3 中，我们将说明如何在登录页中实现"记住我"复选框。 以下教程介绍详细信息中的身份验证票证超时设置。

> [!NOTE]
> 就可以用来登录到网站的用户代理可能不支持 cookie。 在这种情况下，ASP.NET 可以使用无 cookie forms 身份验证票证。 在此模式下，身份验证票证被编码为 URL。 我们将在何时使用无 cookie 身份验证票证和它们的创建和管理在下一步的教程。


### <a name="the-scope-of-forms-authentication"></a>窗体身份验证的范围

`FormsAuthenticationModule`是托管代码的是 ASP.NET 运行时的一部分。 之前的 Microsoft 的版本 7 [Internet 信息服务 (IIS)](https://www.iis.net/) web 服务器没有 IIS 的 HTTP 管道，ASP.NET 运行时的管道之间的非重复障碍。 简单地说，在 IIS 6 和更早版本，`FormsAuthenticationModule`时请求从 IIS 委派给 ASP.NET 运行时才会执行。 默认情况下，IIS 处理类似 HTML 页面和 CSS 和图像文件 – 仅将 ASP.NET 运行时的请求传送静态内容本身 – 请求一个扩展名为.aspx、.asmx 或.ashx 页时。

IIS 7，但是，允许集成的 IIS 和 ASP.NET 管道。 使用几项配置设置，你可以设置 IIS 7 来调用为 FormsAuthenticationModule*所有*请求。 此外，使用 IIS 7，您可以定义为任何类型的文件的 URL 授权规则。 有关详细信息，请参阅[更改之间 IIS6 与 IIS7 安全](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above)，[你的 Web 平台安全性](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)，并[了解 IIS7 URL 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。

长话短说，在 IIS 7 之前的版本，您可以只使用窗体身份验证来保护由 ASP.NET 运行时处理的资源。 同样，URL 授权规则仅应用于由 ASP.NET 运行时处理的资源。 但与 IIS 7 则可以将 FormsAuthenticationModule 和 UrlAuthorizationModule 集成到 IIS 的 HTTP 管道，从而将扩展到所有请求此功能。

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>步骤 1： 为本系列教程中创建一个 ASP.NET 网站

若要访问尽可能多的受众，我们将在整个系列中生成 ASP.NET 网站将创建与 Microsoft 的免费版本的 Visual Studio 2008 中， [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)。 我们将实现`SqlMembershipProvider`中的用户存储区[Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)数据库。 如果使用 Visual Studio 2005 或 Visual Studio 2008 或 SQL Server 的不同版本时，别担心-步骤将几乎完全相同并且将指出任何重要的差异。

> [!NOTE]
> 每个教程中使用的演示 web 应用程序是可通过下载获得。 此可下载的应用程序是通过面向.NET Framework 3.5 版的 Visual Web Developer 2008 中创建的。 由于.NET 3.5 为目标应用程序，其 Web.config 文件包含特定于 3.5 的其他配置元素。 长话短说，如果你尚未然后可下载的 web 应用程序在计算机上安装.NET 3.5 不会无需第一个从 Web.config 移除特定于 3.5 的标记。


我们可以配置窗体身份验证之前，我们首先需要将 ASP.NET 网站。 首先创建一个新文件系统基于 ASP.NET 网站。 若要完成此操作，启动 Visual Web Developer 然后转到文件菜单并选择新网站，显示新建网站对话框。 选择 ASP.NET 网站模板、 将位置下拉列表设置为文件系统、 选择一个文件夹以将该 web 站点，并将语言设置为 C#。 这将创建新的 web 站点的 Default.aspx ASP.NET 页面，应用\_数据文件夹和 Web.config 文件。

> [!NOTE]
> Visual Studio 支持的项目管理的两种模式： 网站项目和 Web 应用程序项目。 网站项目缺少项目文件中，而 Web 应用程序项目模拟项目体系结构在 Visual Studio.NET 2002/2003年 – 它们包括项目文件并放在 /bin 文件夹中的单个程序集编译项目的源代码。 Visual Studio 2005 最初唯一受支持的 Web 站点项目，尽管 Web 应用程序项目模型已重新引入 Service Pack 1;Visual Studio 2008 提供了这两种项目模型。 Visual Web Developer 2005 和 2008年版本，但是，仅支持网站项目。 我将使用网站项目模型。 如果你使用的是非速成版，并想要使用[Web 应用程序项目模型](https://msdn.microsoft.com/library/aa730880%28vs.80%29.aspx)相反，随时执行此操作，但请注意您所见的屏幕，而不是必须执行的步骤之间可能存在某些差异屏幕截图所示，在这些教程中提供的说明。


[![创建新的文件基于系统的 Web 站点](an-overview-of-forms-authentication-cs/_static/image3.png)](an-overview-of-forms-authentication-cs/_static/image2.png)

**图 2**： 创建 New File System-Based 网站 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image4.png))


### <a name="adding-a-master-page"></a>添加母版页

接下来，将新的主页面添加到名为 Site.master 的根目录中的站点。 [母版页](https://msdn.microsoft.com/library/wtxbf3hh.aspx)启用页面开发人员定义可以应用于 ASP.NET 页的整个站点模板。 为母版页的主要优势是，站点的整体外观可以定义在一个位置，从而使它可以轻松地更新或调整站点的布局。


[![添加母版页名为 Site.master 到网站](an-overview-of-forms-authentication-cs/_static/image6.png)](an-overview-of-forms-authentication-cs/_static/image5.png)

**图 3**： 将主页面名为 Site.master 添加到网站 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image7.png))


在母版页中定义站点级页面布局。 可以使用设计视图并添加所需的任何布局或 Web 控件也可以手动在源视图中手动添加标记。 我构建我的母版页的布局来模拟布局中使用我*[使用 ASP.NET 2.0 中的数据](../../data-access/index.md)* （请参阅图 4） 的系列教程。 使用母版页[级联样式表](http://www.w3schools.com/css/default.asp)定位和使用 CSS 设置文件 （其中包含在本教程中的关联的下载中） 的 Style.css 中定义的样式。 但您不能从标记如下所示，定义的 CSS 规则，以便导航&lt;div&gt;的内容绝对定位，以便它显示在左侧，并且具有固定的宽度为 200 像素。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample1.aspx)]

母版页定义静态页面布局和使用的主页面的 ASP.NET 页可以编辑的区域。 这些内容的可编辑区域所指示的`ContentPlaceHolder`控件，可以在内容中看到该&lt;div&gt;。 我们的主页面都有一个`ContentPlaceHolder`（主要内容），但主该页可能具有多个 Contentplaceholder。

与上面输入的标记，切换到设计视图显示了主页面的布局。 使用此母版页任何 ASP.NET 页面将具有指定的标记的功能具有此统一布局`MainContent`区域。


[![Master 页上，通过设计视图查看](an-overview-of-forms-authentication-cs/_static/image9.png)](an-overview-of-forms-authentication-cs/_static/image8.png)

**图 4**： 在母版页，当查看通过设计视图 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image10.png))


### <a name="creating-content-pages"></a>创建内容页面

现在我们有 Default.aspx 页面中我们的网站，但它不使用我们刚刚创建的母版页。 还可以处理 web 页后，可以使用母版页，在声明性标记，如果页面不包含任何内容时是更轻松地只需删除页并重新将其添加到项目中，指定要使用的母版页。 因此，首先从项目删除 Default.aspx。

接下来，右键单击解决方案资源管理器中的项目名称并选择要添加新 Web 窗体命名为 Default.aspx。 这一次，选中"选择母版页"复选框，并从列表中选择 Site.master 母版页。


[![添加一个新的 Default.aspx 页面，选择选择主机页](an-overview-of-forms-authentication-cs/_static/image12.png)](an-overview-of-forms-authentication-cs/_static/image11.png)

**图 5**： 添加新 Default.aspx 页上选择选择主机页 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image13.png))


![使用 Site.master 母版页](an-overview-of-forms-authentication-cs/_static/image14.png)

**图 6**： 使用 Site.master 母版页


> [!NOTE]
> 如果您正在使用 Web 应用程序项目模型添加新项对话框中不包括"选择母版页"复选框。 相反，您需要添加的项类型"Web 内容窗体。" 选择"Web 内容窗体"选项并单击添加之后, Visual Studio 将显示相同的选择主图 6 所示的对话框。


新 Default.aspx 页面的声明性标记只包括@Page指令指定的主路径的母版页的主要内容 ContentPlaceHolder 页面文件和内容控件。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample2.aspx)]

现在，将 Default.aspx 留空。 我们将稍后在本教程中添加内容返回到它。

> [!NOTE]
> 我们母版页包含为菜单或一些其他的导航界面的部分。 我们将在以后的教程中创建此类接口。

## <a name="step-2-enabling-forms-authentication"></a>步骤 2： 启用窗体身份验证

创建的 ASP.NET 网站，我们的下一个任务是启用表单身份验证。 通过指定应用程序的身份验证配置[`<authentication>`元素](https://msdn.microsoft.com/library/532aee0e.aspx)在 Web.config 中。`<authentication>`元素包含单个属性名为指定应用程序使用的身份验证模型的模式。 此属性可以具有以下四个值之一：

- **Windows** – 如所述在前面的教程中，当应用程序使用 Windows 身份验证 web 服务器负责进行身份验证访问者，并且这通常是通过基本、 摘要或集成 Windows身份验证。
- **窗体**– 用户进行身份验证通过在网页上窗体。
- **Passport**– 用户进行身份验证使用 Microsoft Passport 网络。
- **无**– 使用无身份验证模型; 是匿名的所有访问者。

默认情况下，ASP.NET 应用程序使用 Windows 身份验证。 若要更改为窗体身份验证的身份验证类型，然后，我们需要修改`<authentication>`向窗体元素的 mode 属性。

如果你的项目尚未包含 Web.config 文件，添加一个现在通过右键单击解决方案资源管理器中的项目名称，选择添加新项，然后添加 Web 配置文件。


[![如果你的项目尚未包含 Web.config，将其添加到](an-overview-of-forms-authentication-cs/_static/image16.png)](an-overview-of-forms-authentication-cs/_static/image15.png)

**图 7**： 如果你项目不会不尚未包括 Web.config，现在添加 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image17.png))


接下来，找到`<authentication>`元素，并更新为使用 forms 身份验证。 以后此更改后，Web.config 文件的标记看起来应类似于下面：

[!code-xml[Main](an-overview-of-forms-authentication-cs/samples/sample3.xml)]

> [!NOTE]
> 由于 Web.config 是一个 XML 文件，大小写很重要。 请确保以大写"F"将模式属性设置为窗体。 如果使用不同的大小写，例如"窗体"，将收到配置错误，访问通过浏览器网站时。


`<authentication>`元素可以根据需要包含`<forms>`子元素，其中包含窗体身份验证特定的设置。 现在，让我们只需使用默认窗体身份验证设置。 我们将探讨`<forms>`在下一教程中的更多详细信息中的子元素。

## <a name="step-3-building-the-login-page"></a>步骤 3： 生成登录页

为了支持窗体身份验证我们的网站需要登录页。 在"了解窗体身份验证工作流"部分中所述`FormsAuthenticationModule`将自动重定向到登录页的用户如果用户尝试访问的页，它们不是有权查看。 也有对匿名用户在登录页将显示一个链接的 ASP.NET Web 控件。 这带来了这样一个问题，"什么是登录页面的 URL？"

默认情况下，窗体身份验证系统需要登录页后，可以将命名为 login.aspx 的情况，并放置在 web 应用程序的根目录中。 如果你想要使用不同的登录页 URL，就可以做到通过在 Web.config 中指定。我们将了解如何执行此操作在后续的教程。

登录页有三项职责：

1. 提供允许输入其凭据的访问者的接口。
2. 确定已提交的凭据是否有效。
3. "登录"用户创建窗体身份验证票证。

### <a name="creating-the-login-pages-user-interface"></a>创建登录页的用户界面

让我们开始使用第一个任务。 将一个新的 ASP.NET 页面添加到站点的根目录下名为 login.aspx 的情况并将其与 Site.master 母版页相关联。


[![添加新的 ASP.NET 页名为 login.aspx 的情况](an-overview-of-forms-authentication-cs/_static/image19.png)](an-overview-of-forms-authentication-cs/_static/image18.png)

**图 8**： 添加新 ASP.NET 页名为 login.aspx 的情况 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image20.png))


典型的登录页面接口包含两个文本框 – 一个用于用户的名称，另一个用于其密码 – 和一个用于提交窗体按钮。 网站通常包括一个"记住我"复选框，如果选中，能在浏览器重新启动后保存生成的身份验证票证。

将两个文本框添加到 login.aspx 的情况并设置其`ID`为用户名和密码，属性分别。 此外设置密码的`TextMode`属性设置为密码。 接下来，添加一个复选框控件，设置其`ID`RememberMe 属性并将其`Text`属性设置为"记住我"。 接下来，添加一个名为 LoginButton 按钮其`Text`属性设置为"登录"。 最后，添加一个标签 Web 控件并设置其`ID`属性设置为 InvalidCredentialsMessage，其`Text`属性设置为"用户名或密码无效。 请重试。"，将其`ForeColor`属性设置为红色，并将其`Visible`属性设置为 False。

此时您的屏幕应类似于屏幕快照中图 9 和页面的声明性语法应如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample4.aspx)]


[![登录页包含两个文本框、 复选框、 按钮和标签](an-overview-of-forms-authentication-cs/_static/image22.png)](an-overview-of-forms-authentication-cs/_static/image21.png)

**图 9**: 登录页包含两个文本框、 复选框、 按钮和标签 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image23.png))


最后，创建一个事件处理程序，为 LoginButton 的 Click 事件。 从设计器中，只需双击按钮控件，以创建此事件处理程序。

### <a name="determining-if-the-supplied-credentials-are-valid"></a>确定提供的凭据是否有效

现在，我们需要实现任务 2 中按钮的 Click 事件处理程序 – 确定提供的凭据是否有效。 若要执行此操作那里必须是包含所有用户的凭据，以便我们可以确定是否提供的凭据与匹配任何已知的凭据的用户存储。

ASP.NET 2.0 中，开发人员之前负责实现其自己两个用户存储区和编写代码来验证针对存储提供的凭据。 大多数开发人员在实现用户存储在数据库中，创建名为列如用户名、 密码、 电子邮件、 LastLoginDate，等用户表。 然后，此表中，将包含每个用户帐户的一条记录。 正在验证的用户提供的凭据将涉及查询数据库中的匹配用户名，然后确保在数据库中的密码对应于提供的密码。

使用 ASP.NET 2.0，开发人员应使用一个成员资格提供程序来管理用户存储区。 在本系列教程中我们将使用 SqlMembershipProvider，为用户存储区使用 SQL Server 数据库。 使用 SqlMembershipProvider 时我们需要实现包括表、 视图和存储的过程所需的提供程序特定的数据库架构。 我们将说明如何实现此架构中的***SQL Server 中创建成员身份架构***教程。 使用成员资格提供程序已就绪，验证用户的凭据就像调用一样简单[成员资格类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)的[ValidateUser (*用户名*，*密码*)方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)，它返回一个布尔值，该值指示是否的有效性*用户名*并*密码*组合。 因为看看我们未实现 SqlMembershipProvider 的用户存储区，我们不能使用成员资格类的 ValidateUser 方法这一次。

而不是花时间来生成我们自己自定义用户数据库表 （它将是已过时，我们实现 SqlMembershipProvider 后），让我们改为硬编码中登录名的有效凭据的页面本身。 在 LoginButton 的单击事件处理程序中，添加以下代码：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample5.cs)]

正如您所看到的有三个有效的用户帐户-Scott、 Jisun 和 Sam-和所有这三个具有相同的密码 （"密码"）。 该代码循环访问用户和密码数组查找有效的用户名和密码匹配。 如果用户名和密码都有效，我们需要以登录用户，然后将其重定向到相应的页。 如果凭据无效，我们显示 InvalidCredentialsMessage 标签。

当用户输入有效的凭据时，如我提到的它们被重定向到"相应页"。 不过是合适的页面，什么？ 请记住，当用户访问他们无权查看的页面，FormsAuthenticationModule 自动将他们重定向到登录页。 在执行此操作，它包含通过 ReturnUrl 参数在查询字符串中所请求的 URL。 也就是说，如果用户试图访问 ProtectedPage.aspx，并且它们无权执行此操作，FormsAuthenticationModule 将重定向到：

Login.aspx?ReturnUrl=ProtectedPage.aspx

在成功登录，用户应重定向回到 ProtectedPage.aspx。 或者，用户可以访问登录页上他们自己自觉。 在这种情况下，在用户登录后它们应发送到根文件夹的 Default.aspx 页面。

### <a name="logging-in-the-user"></a>在用户中的日志记录

假定提供的凭据是有效的我们需要创建窗体身份验证票证，从而用户访问该站点中的日志记录。 [FormsAuthentication 类](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx)中[System.Web.Security 命名空间](https://msdn.microsoft.com/library/system.web.security.aspx)提供身份验证系统的日志记录和日志记录用户通过窗体中的各种的方法。 虽然 FormsAuthentication 类中有几种方法，我们此时，必须查明感兴趣的三个是：

- [GetAuthCookie (*用户名*， *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) – 创建所提供的名称的窗体身份验证票证*用户名*。 接下来，此方法创建并返回一个 HttpCookie 对象，保存身份验证票证的内容。 如果*persistCookie*为 true，在创建持久性 cookie。
- [SetAuthCookie (*用户名*， *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) – 调用 GetAuthCookie (*用户名*， *persistCookie*)若要生成的窗体身份验证 cookie 的方法。 然后，此方法将添加到 （假设基于 cookie 的 forms 身份验证正在使用; 否则为此方法调用的内部类处理无 cookie 票证逻辑） 的 Cookie 集合 GetAuthCookie 返回的 cookie。
- [RedirectFromLoginPage (*用户名*， *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) – 此方法调用 SetAuthCookie (*用户名*， *persistCookie*)，然后将用户重定向到相应的页。

当您需要写出到的 Cookie 集合的 cookie 之前修改身份验证票证时，GetAuthCookie 非常方便。 如果想要创建窗体身份验证票证，并将其添加到的 Cookie 集合，但不是希望将用户重定向到相应的页面，SetAuthCookie 非常有用。 也许你想要将它们保留在登录页或将其发送到某些备用的页面。

由于我们想要将用户登录并将它们重定向到相应的页面，让我们使用 RedirectFromLoginPage。 更新 LoginButton 的单击事件处理程序，两个已注释的 TODO 行替换为以下代码行：

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked);

创建窗体身份验证票证时我们使用用户名文本框的 Text 属性的窗体身份验证票证*用户名*参数和 RememberMe 复选框的选中的状态*persistCookie*参数。

若要测试登录页，请在浏览器中访问它。 首先输入凭据无效，如用户名为"Nope"和"错误"的密码。 单击登录按钮时将发生一个回发和 InvalidCredentialsMessage 标签将显示。


[![InvalidCredentialsMessage 标签是显示时输入无效凭据](an-overview-of-forms-authentication-cs/_static/image25.png)](an-overview-of-forms-authentication-cs/_static/image24.png)

**图 10**: InvalidCredentialsMessage 标签是显示时输入无效凭据 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image26.png))


接下来，输入有效的凭据，然后单击登录按钮。 创建这一次回发发生窗体身份验证票证时，你会自动重定向回 Default.aspx。 此时您已登录到网站，尽管没有视觉提示，用于指示当前登录。 在步骤 4 中我们将了解如何以编程方式确定用户是否已经登录还是不以及如何确定用户访问的页面。

步骤 5 检查日志记录将用户从该网站的方法。

### <a name="securing-the-login-page"></a>保护登录页

当用户输入其凭据，并提交登录页表单时，通过 Internet 到 web 服务器中传输 （包括密码） 的凭据*纯文本*。 这意味着任何探查的网络流量的黑客可以看到的用户名和密码。 若要防止此情况，是必须使用加密的网络流量[安全套接字层 (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)。 这将确保从那一刻起，它们将保留在浏览器，直到 web 服务器接收加密的凭据 （以及整个页面的 HTML 标记）。

除非你的网站包含敏感信息，只需要使用其中用户的密码将否则会通过网络发送以纯文本形式 SSL 登录页上和其他页上。 不需要担心如何保护窗体身份验证票证，因为默认情况下，则会同时加密和数字签名 （以防止篡改）。 以下教程中会显示在窗体身份验证票证安全的更深入讨论。

> [!NOTE]
> 很多财务和医疗网站配置为在上使用 SSL*所有*页可以访问身份验证的用户。 如果你正在构建网站可以配置窗体身份验证系统，以便窗体身份验证票证只传输通过安全连接。 我们将探讨在下一教程中的各种窗体身份验证配置选项*[窗体身份验证配置和高级主题](forms-authentication-configuration-and-advanced-topics-cs.md)*。


## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>步骤 4： 检测已经过身份验证的访问者，并确定其标识

现在我们已启用窗体身份验证并创建一个基本的登录页面，但我们还未检查如何我们可以确定用户是否已经过身份验证或匿名。 在某些情况下我们可能想要显示不同的数据或信息取决于是否已经过身份验证或匿名用户访问的页面。 此外，我们通常需要知道已经过身份验证的用户的标识。

让我们来增强现有的 Default.aspx 页面，以说明了这些方法。 在 Default.aspx 中将添加两个面板控件、 一个命名的 AuthenticatedMessagePanel 和另一个命名的 AnonymousMessagePanel。 添加名为 WelcomeBackMessage 中第一个面板的标签控件。 第二个面板中添加超链接控件，将其 Text 属性改"登录"并将其 NavigateUrl 属性为"~ / Login.aspx"。 此时 Default.aspx 的声明性标记应类似于下面：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample6.aspx)]

您有可能猜到目前为止，这里的思路是向经过身份验证的访问者和只是对匿名的访客 AnonymousMessagePanel 显示只 AuthenticatedMessagePanel。 若要实现此目的，我们需要设置这些面板的可视属性，具体取决于是否用户登录或未。

[Request.IsAuthenticated 属性](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx)返回一个布尔值，该值指示是否已验证请求。 下面的代码输入到页面\_加载事件处理程序代码：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample7.cs)]

利用此代码，通过浏览器中访问 Default.aspx。 假设你尚未登录，你将看到一个链接到登录页 （请参阅图 11）。 单击此链接，登录到站点。 正如我们看到在步骤 3 中，输入你的凭据后，将返回到 Default.aspx，但这次该页面会显示"欢迎回到 ！" 消息 （请参阅图 12）。


![匿名访问，日志中链接显示时](an-overview-of-forms-authentication-cs/_static/image27.png)

**图 11**： 显示时访问以匿名方式、 日志中链接


![将显示已经过身份验证的用户](an-overview-of-forms-authentication-cs/_static/image28.png)

**图 12**： 将显示"欢迎回来 ！"进行身份验证的用户 消息


我们可以确定通过当前登录的用户的标识[HttpContext 对象](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)的[用户属性](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)。 HttpContext 对象表示有关当前请求的信息，以及其他是为响应、 请求和会话中，此类公共 ASP.NET 对象的主服务器。 用户属性表示当前 HTTP 请求和实现的安全上下文[IPrincipal 接口](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)。

由 FormsAuthenticationModule 设置用户属性。 具体而言，当 FormsAuthenticationModule 传入请求中找到的窗体身份验证票证，它创建一个新的 GenericPrincipal 对象，并将其分配给用户属性。

主体对象 （如 GenericPrincipal) 提供有关用户的标识和到其所属的角色信息。 IPrincipal 接口定义了两个成员：

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) – 返回一个布尔值，该值指示主体是否属于指定角色的方法。
- [标识](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx)– 返回实现的对象的属性[IIdentity 接口](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)。 IIdentity 接口定义了三个属性： [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx)， [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)，并[名称](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)。

我们可以确定当前的访问者使用下面的代码的名称：

字符串 currentUsersName = User.Identity.Name;

使用窗体身份验证，当[FormsIdentity 对象](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx)创建 GenericPrincipal 的标识属性。 FormsIdentity 类始终返回字符串"Forms"其 AuthenticationType 属性和其 IsAuthenticated 属性为 true。 Name 属性返回在创建窗体身份验证票证时指定的用户名。 FormsIdentity 除了这三个属性，包括通过基础的身份验证票证访问其[票证属性](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)。 票证属性返回类型的对象[FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)，其中包含属性，如过期、 IsPersistent、 IssueDate、 名称和等等。

重要的一点需要注意此处在于*用户名*FormsAuthentication.GetAuthCookie 中指定的参数 (*用户名*， *persistCookie*)，FormsAuthentication.SetAuthCookie (*用户名*， *persistCookie*)，和 FormsAuthentication.RedirectFromLoginPage (*用户名*， *persistCookie*) 方法是通过 User.Identity.Name 返回的相同值。 此外，通过这些方法创建的身份验证票证已提供着将 User.Identity 强制转换为 FormsIdentity 对象，然后访问该票证属性：

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample8.cs)]

让我们来提供在 Default.aspx 中更具个性化的消息。 更新页面\_加载事件处理程序，以便 WelcomeBackMessage 标签的 Text 属性分配字符串"欢迎回来，*用户名*！"

WelcomeBackMessage.Text ="欢迎使用后，"+ User.Identity.Name +"！";

图 13 显示了此修改的影响 （当用户 Scott 登录）。


![欢迎使用消息包含当前已登录用户的名称中](an-overview-of-forms-authentication-cs/_static/image29.png)

**图 13**： 欢迎消息包含当前已登录用户的名称中


### <a name="using-the-loginview-and-loginname-controls"></a>使用 LoginView 和 LoginName 控件

向经过身份验证和匿名用户显示不同的内容是常见的要求;因此显示当前登录用户的名称。 因此，ASP.NET 包括提供相同的功能在图 13 中，但无需编写一行代码所示的两个 Web 控件。

[LoginView 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)是基于模板的 Web 控件，它可以更轻松地向经过身份验证和匿名用户显示不同的数据。 登录视图包括两个预定义的模板：

- 仅系统 AnonymousTemplate – 任何标记添加到此模板会向匿名访问者。
- LoggedInTemplate – 仅向经过身份验证的用户显示此模板的标记。

让我们将 LoginView 控件添加到我们的站点的母版页，Site.master 中。 而不是添加不仅仅是 LoginView 控件，不过，让我们来添加这两个新 ContentPlaceHolder 控件，然后将该新 ContentPlaceHolder 内的 LoginView 控件。 此决策的理由将很快成为明显。

> [!NOTE]
> 除了 AnonymousTemplate 和 LoggedInTemplate，LoginView 控件可以包含特定于角色的模板。 特定于角色的模板仅向这些用户属于指定角色显示标记。 在将来的教程中，我们将检查 LoginView 控件的基于角色的功能。


首先，通过添加母版页中导航到名为 LoginContent ContentPlaceHolder &lt;div&gt;元素。 只需将 ContentPlaceHolder 控件从工具箱拖到源视图中，将所得的标记的正上方"TODO： 菜单将转到此处..."文本。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample9.aspx)]

接下来，添加内 LoginContent ContentPlaceHolder LoginView 控件。 放置到母版页的 ContentPlaceHolder 控件的内容被视为*默认内容*ContentPlaceHolder 的。 也就是说，使用此母版页的 ASP.NET 页面可以为每个 ContentPlaceHolder 指定自己的内容，或使用母版页的默认内容。

登录视图和其他与登录相关的控件位于工具箱的登录选项卡中。


![在工具箱 LoginView 控件](an-overview-of-forms-authentication-cs/_static/image30.png)

**图 14**: LoginView 控件工具箱中


接下来，添加两个&lt;b /&gt;元素紧 LoginView 控件，但仍在 ContentPlaceHolder 内。 在此情况下，导航&lt;div&gt;元素的标记应如下所示：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample10.aspx)]

登录视图的模板可以定义从设计器或声明性标记。 从 Visual Studio 设计器中，展开登录视图的智能标记，其中列出了在下拉列表中配置的模板。 在文本中的类型的"Hello，stranger"到 AnonymousTemplate;接下来，添加超链接控件并设置其文本和 NavigateUrl 属性设置为"登录"和"~ / Login.aspx"分别。

配置后 AnonymousTemplate，切换到 LoggedInTemplate 并输入文本、"欢迎使用后，"。 然后将登录名控件从工具箱拖到 LoggedInTemplate，将其放在"欢迎回来，"文本后立即中。 [LoginName 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)，如其名，显示当前登录用户的名称。 在内部，LoginName 控件只是输出 User.Identity.Name 属性

以后进行到登录视图的模板的这些新增功能，标记看起来应类似于下面：

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample11.aspx)]

通过这一附加到 Site.master 母版页，我们的网站中每个页面将显示不同的消息，具体取决于是否对用户进行身份验证。 图 15 显示了用户 Jisun 通过浏览器访问时的 Default.aspx 页。 "欢迎回来，Jisun"消息会重复两次： 一次 （通过我们刚添加的 LoginView 控件） 左侧的主页面的导航部分中，一次是在 Default.aspx 的内容 （通过面板控件和编程逻辑） 的区域。


![LoginView 控件显示](an-overview-of-forms-authentication-cs/_static/image31.png)

**图 15**: LoginView 控件显示"欢迎回来，Jisun。"


因为我们登录视图添加到母版页时，它可以出现在我们的网站上的每一页。 但是，可能有网页我们不想要显示此消息。 此类的一页是登录页上，由于链接到登录页有点站不住脚存在。 由于我们在母版页中 ContentPlaceHolder 中放置 LoginView 控件，我们可以在我们的内容页面中重写此默认标记。 打开 login.aspx 的情况，并转到设计器。 由于我们没有显式定义的某个内容控件在母版页中 LoginContent ContentPlaceHolder 为 login.aspx 的情况，登录页将为此 ContentPlaceHolder 显示主页面的默认标记。 您可以看到这通过设计器 – LoginContent ContentPlaceHolder 显示默认标记 （LoginView 控件）。


[![登录页显示的默认内容的母版页的 LoginContent ContentPlaceHolder](an-overview-of-forms-authentication-cs/_static/image33.png)](an-overview-of-forms-authentication-cs/_static/image32.png)

**图 16**： 登录页会显示默认内容的母版页的 LoginContent ContentPlaceHolder ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image34.png))


要为 LoginContent ContentPlaceHolder 重写默认标记，只需右键单击设计器中的区域，并从上下文菜单中选择创建自定义内容选项。 (选中时，如果使用 Visual Studio 2008 ContentPlaceHolder 包含智能标记，提供了相同的选项。)这会添加新的内容控件到页面的标记，从而允许我们定义的此页的自定义内容。 您可以添加自定义消息，如"请的日志..."，但是让我们只需将其留空。

> [!NOTE]
> 在 Visual Studio 2005 中，创建自定义内容创建一个空内容 ASP.NET 页中的控件。 在 Visual Studio 2008 中，但是，创建自定义内容的母版页默认将内容复制到新创建的内容控件。 如果使用 Visual Studio 2008，然后，创建新的内容控件后请务必清除复制从主页面的内容。


图 17 显示了 Login.aspx 页面时进行此更改后从浏览器访问。 请注意，没有任何"Hello，stranger"或"欢迎回来，*用户名*"左侧的导航窗格中的消息&lt;div&gt;因为没有访问 Default.aspx 时。


[![登录页上隐藏默认 LoginContent ContentPlaceHolder 标记](an-overview-of-forms-authentication-cs/_static/image36.png)](an-overview-of-forms-authentication-cs/_static/image35.png)

**图 17**： 登录页上隐藏默认 LoginContent ContentPlaceHolder 的标记 ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image37.png))


## <a name="step-5-logging-out"></a>步骤 5： 注销

在步骤 3 中探讨了构建登录页面，使用户登录到站点，但我们尚未看到如何注销用户。日志记录中的用户的方法，除了 FormsAuthentication 类还提供[SignOut 方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)。 注销方法只需销毁窗体身份验证票证，从而日志记录将用户从该站点。

ASP.NET 提供注销链接此类的常见功能包括专门用于注销用户的控件。[LoginStatus 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx)显示"登录"LinkButton 或"注销"LinkButton，具体取决于用户的身份验证状态。 而向经过身份验证的用户显示"注销"LinkButton"登录"LinkButton 呈现为匿名用户。 可通过 LoginStatus 的配置的"登录名"和"注销"Linkbutton 的文本 LoginText 和 LogoutText 属性。

单击"登录"LinkButton 导致回发，从中发出重定向到登录页。 单击"注销"LinkButton 导致 LoginStatus 控件调用 FormsAuthentication.SignOff 方法，然后将用户重定向到一个页面。 登录页上关闭用户被重定向为依赖于 LogoutAction 属性，可以分配给三个以下值之一：

- 刷新-默认设置;将用户重定向到他们只需访问的页面。 如果他们只需访问的页面不允许匿名用户，则 FormsAuthenticationModule 将自动将用户重定向到登录页。

您可能很想知道为什么在此处执行重定向。 如果用户想要保留在同一页上，为什么需要显式重定向？ 原因是在用户单击"注销"LinkButton 时，其 cookie 集合中的窗体身份验证票证仍有。 因此，在回发请求是已经过身份验证的请求。 LoginStatus 控件调用注销方法，但 FormsAuthenticationModule 已完成用户身份验证后将发生这种情况。 因此，显式重定向会导致浏览器重新请求的页面。 重新请求页面时浏览器时，窗体身份验证票证已删除并因此是匿名的传入请求。

- 重定向 – 用户将重定向到 LoginStatus LogoutPageUrl 属性指定的 URL。
- RedirectToLoginPage – 用户重定向到登录页。

让我们将登录状态控件添加到母版页并将其配置为使用重定向选项向用户发送到显示一条消息确认，它们已注销的页面。首先，创建名为 Logout.aspx 的根目录中的页面。 别忘了将此页与 Site.master 母版页相关联。 接下来，在页面的标记向它们已被注销用户解释输入消息。

接下来，返回到 Site.master 母版页并在 LoginContent ContentPlaceHolder 添加下 LoginView LoginStatus 控件。 设置到重定向的登录状态控件 LogoutAction 属性并将其 LogoutPageUrl 属性为"~ / Logout.aspx"。

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample12.aspx)]

由于 LoginStatus LoginView 控件之外，它将显示为匿名和经过身份验证的用户，但这是确定，因为"登录"或"注销"LinkButton LoginStatus 将正确显示。 LoginStatus 控件添加后，"登录"中的超链接 AnonymousTemplate 多余，因此将其删除。

图 18 显示了 Default.aspx，当 Jisun 访问。 请注意左侧的列显示该消息，"欢迎回来，Jisun"以及将其注销的链接。单击 LinkButton 注销导致回发、 从系统中注销 Jisun，然后将她重定向到 Logout.aspx。 如图 19 所示，通过 Jisun 达到的 Logout.aspx 她已注销，并因此是匿名的时间。 因此，左列显示文本"stranger 欢迎"和登录页面的链接。


[![Default.aspx 显示](an-overview-of-forms-authentication-cs/_static/image39.png)](an-overview-of-forms-authentication-cs/_static/image38.png)

**图 18**: Default.aspx 显示"欢迎回来，Jisun"以及"注销"LinkButton ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image40.png))


[![Logout.aspx 显示](an-overview-of-forms-authentication-cs/_static/image42.png)](an-overview-of-forms-authentication-cs/_static/image41.png)

**图 19**: Logout.aspx 显示"欢迎使用，stranger"以及"登录"LinkButton ([单击以查看实际尺寸的图像](an-overview-of-forms-authentication-cs/_static/image43.png))


> [!NOTE]
> 我鼓励您自定义 Logout.aspx 页后，可以隐藏主页面 LoginContent ContentPlaceHolder （例如，我们为 Login.aspx 在步骤 4 中所做的那样）。 "登录"LinkButton 呈现的登录状态控件的原因是 (下的一个"Hello，stranger") 将用户发送到 ReturnUrl 查询字符串参数中传递的当前 URL 的登录页。 简单地说，如果已注销的用户单击此 LoginStatus"登录"LinkButton，然后日志中的，他们将被重定向回 Logout.aspx，可以轻松地让用户迷惑。


## <a name="summary"></a>总结

在本教程中，我们开始的窗体身份验证工作流分析作为开篇，然后转变为在 ASP.NET 应用程序中实现窗体身份验证。 窗体身份验证由 FormsAuthenticationModule，具有两项职责： 标识用户根据其窗体身份验证票证，并将未经授权的用户重定向到登录页。

.NET Framework 的 FormsAuthentication 类包含用于创建、 检查和删除窗体身份验证票证的方法。 Request.IsAuthenticated 属性和用户对象提供用于确定是否对请求进行身份验证和用户的标识信息的其他编程支持。 也有 LoginView、 LoginStatus 和 LoginName Web 控件，为开发人员提供了一种快速、 无代码方法用于执行许多与登录相关的常见任务。 在将来的教程中，我们将检查这些和其他与登录相关的 Web 控件中更详细地介绍。

本教程提供窗体身份验证的粗略的概述。 我们未检查的各种的配置选项，看看如何无 cookie forms 身份验证票证的工作，或浏览 ASP.NET 如何保护窗体身份验证票证的内容。 我们将讨论这些主题，详细信息[下一教程](forms-authentication-configuration-and-advanced-topics-cs.md)。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [IIS6 与 IIS7 安全之间的更改](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [登录 ASP.NET 控件](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [专业 ASP.NET 2.0 安全、 成员资格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)(ISBN: 978-0-7645-9698-8)
- [`<authentication>`元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [`<forms>`元素 `<authentication>`](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>在本教程中包含的主题的视频培训

- [在 ASP.NET 中使用基本 Forms 身份验证](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是许多有用的审阅者已评审本系列本教程。 本教程中的潜在顾客审阅者包括 Alicja Maziarz、 John Suru 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](security-basics-and-asp-net-support-cs.md)
> [下一页](forms-authentication-configuration-and-advanced-topics-cs.md)
