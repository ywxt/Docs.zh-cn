---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 入门 |Microsoft Docs
author: Rick-Anderson
description: WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。 使用 Visual Studio 或 Visual Studio Code。 本指南...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 79f76410e091b137e2792127b0a42524270761e8
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021490"
---
<a name="getting-started"></a>入门
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。 使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。
> 
> 
> 此指南和应用程序提供您的 ASP.NET Web Pages （版本 2 或更高版本） 概述和 Razor 语法，用于创建动态网站一款轻量级框架。 它还介绍 WebMatrix 中，用于创建网页和网站的工具。
> 
> **级别**： 新的 ASP.NET Web 页面。  
> **假定技能**: HTML、 基本的级联样式表 (CSS)。
> 
> 学习内容集的第一个教程中：
> 
> - ASP.NET Web Pages 何种技术，它为是。
> - WebMatrix 是什么。
> - 如何安装的所有内容。
> - 如何使用 WebMatrix 创建网站。
>   
> 
> 功能/技术讨论：
> 
> - Microsoft Web 平台安装程序。
> - WebMatrix。
> - *.cshtml*页
>   
> 
> Mike 教皇最初编写了本教程。 Tom FitzMacken 针对 Microsoft WebMatrix 3 更新它。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 3


## <a name="what-should-you-know"></a>您应该知道哪些内容？

我们假定您熟悉：

- **HTML**。 没有深入专业知识是必需的。 我们将不再对 HTML，但我们也不使用任何复杂。 我们将提供指向 HTML 教程，我们认为这非常有用。
- **级联样式表 (CSS)**。 与相同 HTML。
- **基本数据库的想法**。 如果已使用电子表格的数据和排序和筛选的专业技能级别的数据，我们通常假定用于本教程系列。

我们还假定你感兴趣学习基本编程。 ASP.NET Web Pages 使用名为 C# 的编程语言。 您无需具有任何背景中编程，只需在其中的关注。 如果您曾经编写任何 JavaScript 在网页上之前，您有充足的背景。

请注意，是否您熟悉编程，你可能会发现我们就将新程序员加快时，最初设置了本教程将缓慢移动。 随着我们过去的几个的第一个教程，不过，会有不到基本编程来解释，操作会将上，在更快的剪辑。

## <a name="what-do-you-need"></a>你需要什么？

你将需要以下项目：

- 在运行 Windows 8、 Windows 7、 Windows Server 2008 或 Windows Server 2012 的计算机。
- 实时的 internet 连接。
- （需要在安装过程） 具有管理员特权。

## <a name="what-is-aspnet-web-pages"></a>什么是 ASP.NET 网页？

ASP.NET Web Pages 是一个框架，可用于创建动态网页。 简单的 HTML web 页面是静态的;其内容取决于固定的页的 HTML 标记。 如您创建使用 ASP.NET Web Pages 动态页，您可以使用代码动态创建页面内容。

动态页，您可以执行各种操作。 您可以通过使用窗体输入请求用户，然后更改页上显示的内容或它的外观。 您可以从用户中获取信息、 将其保存在数据库中，并更高版本列出它。 你可以从您的网站发送电子邮件。 可以与 web （例如，映射服务） 上的其他服务进行交互，并生成集成来自这些源的信息的页面。

## <a name="what-is-webmatrix"></a>WebMatrix 是什么？

WebMatrix 是一个集成的网页编辑器、 数据库实用程序、 用于测试页面和用于将你的网站发布到 Internet 的功能的 web 服务器的工具。 WebMatrix 是免费的而且很容易安装且易于使用。 （它也只是普通的 HTML 页面，以及其他技术，如 PHP。）

您不会真正*具有*使用 WebMatrix 来处理使用 ASP.NET Web Pages。 您可以创建页，使用文本编辑器，例如，和测试页使用有权访问的 web 服务器。 但是，WebMatrix 得所有非常简单，因此这些教程将使用在整个的 WebMatrix。

## <a name="about-these-tutorials"></a>有关这些教程

本教程系列将介绍如何使用 ASP.NET Web Pages。 在此介绍性教程集中中共有 9 教程。 它的一系列教程的集，从 ASP.NET Web Pages 初级用户到创建实际的专业外观的网站的一部分。

第一个教程设置集中向您展示如何使用 ASP.NET Web Pages 的基础知识。 完成后，可以使用此结束，其中的更深入地浏览网页选取的其他教程集。

我们有意继续轻松进行深入的解释。 只要我们显示一些内容，对于本教程系列我们始终选择的方法，我们认为是最易于帮助理解。 更高版本的教程集转到更多深入分析和显示更高效或更灵活的方法 （也更有趣）。 但是，这些教程要求您首先了解的基本知识。

你刚刚启动教程系列介绍了这些功能的 ASP.NET Web Pages:

- 简介和获取安装的所有内容。 （这是您在阅读本教程中值。）
- ASP.NET Web Pages 编程的基础知识。
- 创建数据库。
- 创建和处理用户输入窗体。
- 添加、 更新和删除数据库中的数据。

## <a name="what-will-you-create"></a>您将创建哪些内容？

本教程中设置和后续条件围绕的网站可以在其中列出您喜欢的电影。 您可以输入电影，编辑它们，然后列出它们。 下面是一些你将创建在本教程系列中的页。 第一个显示电影列表，您将创建的页面：

![已完成的影片应用程序显示电影列表](getting-started/_static/image1.png)

而以下是可将新电影信息添加到你的站点的页面：

![显示将添加影片页的已完成的电影应用](getting-started/_static/image2.png)

后续教程集生成对此设置，并添加更多的功能，如将图片上载、 让人们登录、 发送电子邮件和与社交媒体相集成。

## <a name="see-this-app-running-on-azure"></a>请参阅在 Azure 上运行此应用程序

若要查看已完成的站点作为实时 web 应用运行吗？ 只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果你还没有帐户，你具有以下选项：

- [免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。
- [激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。

## <a name="installing-everything"></a>安装的所有内容

可以使用 microsoft Web 平台安装程序安装的所有内容。 事实上，您安装安装程序，并且然后使用它来安装其他所有内容。

若要使用 Web 页，必须至少具有 Windows XP SP3 安装或 Windows Server 2008 或更高版本。

上[Web Pages 页](../../../index.md)的 ASP.NET 网站中，单击**安装**。

![ASP.NET Web 站点显示&quot;安装 WebMatrix&quot;按钮](getting-started/_static/image3.png)

需要接受许可条款和隐私声明，然后安装 WebMatrix。

![接受条款以开始安装](getting-started/_static/image4.png)

单击**运行**以开始安装。 (如果你想要保存该安装程序，请单击**保存**，然后从保存位置的文件夹运行安装程序。)

![](getting-started/_static/image5.png)

Web 平台安装程序将显示，您可以随时安装 WebMatrix。 单击“安装” 。

![](getting-started/_static/image6.png)

安装过程计算出它具有要在计算机上安装并启动进程。 具体取决于确切的功能安装，该过程可能需要从几分钟到几分钟的时间。 选择**我接受**以接受许可条款。

## <a name="hello-webmatrix"></a>Hello WebMatrix

完成后，安装过程可以自动启动 WebMatrix。 如果没有，Windows，在从**启动**菜单，启动**Microsoft WebMatrix**。

当首次启动 WebMatrix 时，系统将提供机会与 Microsoft 帐户登录到 Microsoft Azure。 通过登录，系统会通过 Azure 的 10 个免费的 web 应用。 这些免费的 web 应用程序提供测试您的应用程序的简便方法。 如果你还没有 Azure 帐户，但有 MSDN 订阅，可以[激活 MSDN 订阅权益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。 否则，可以只需几分钟内创建一个免费试用帐户。 有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。

无需立即登录以继续学习本教程。 如果您确实不登录现在，你仍将进行更高版本登录的选项。 上次[主题](publishing.md)在本教程系列介绍了如何将你的网站部署到 Azure; 因此，您将需要登录以完成该主题。

此时，请登录你的 Microsoft 帐户或选择**不是现在**右下角中。

![登录](getting-started/_static/image7.png)

若要开始，将创建空白网站，并添加一个页面。 在此集中的下一个教程将尝试使用某个内置网站模板。

在开始窗口中，单击**新建**。

![WebMatrix 启动屏幕](getting-started/_static/image8.png)

模板是网站的预生成的文件和页面的不同类型。 若要查看所有默认提供的模板，请选择模板库选项。

![选择模板库](getting-started/_static/image9.png)

在中**快速启动**窗口中，选择**空网站**从**ASP.NET**组，并命名新的站点"WebPagesMovies"。

![WebMatrix 快速启动窗口中选择空网站模板](getting-started/_static/image10.png)

单击 **“下一步”**。

如果你已登录到你的 Microsoft 帐户，您将有机会在 Azure 上创建站点。 根据你的站点的默认名称的名称**WebPagesMovies.azurewebsites.net**建议; 但是，感叹号指示此名称不是 Windows Azure 上提供。 为简单起见，选择**跳过**绕过现在在 Azure 上创建网站。 更高版本在此系列中，我们将站点发布到 Azure。

![创建 azure 网站](getting-started/_static/image11.png)

WebMatrix 创建并打开该站点：

![在 WebMatrix 中打开新 WebPagesMovies 站点](getting-started/_static/image12.png)

在顶部，没有快速访问工具栏和一个功能区。 在左下角，你看到工作区选择器，切换任务 (**站点**，**文件**，**数据库**，**报表**)。 右侧是内容窗格中，用于在编辑器和报表。 并在底部有时您会看到消息通知栏。

您将了解有关 WebMatrix 和它的功能在完成这些教程。

## <a name="creating-a-web-page"></a>创建 Web 页

若要熟悉 WebMatrix 和 ASP.NET Web Pages，将创建一个简单的页面。

在工作区选择器中，选择**文件**工作区。 此工作区允许您使用的文件和文件夹。 左的窗格显示您的网站的文件结构。 此功能区改为显示与文件相关的任务。

![在 WebMatrix 中的文件工作区](getting-started/_static/image13.png)

在功能区中，单击下的箭头**新建**，然后单击**新文件**。

![使用&quot;新建&quot;命令在功能区中创建新文件](getting-started/_static/image14.png)

WebMatrix 显示文件类型的列表。 选择**CSHTML**，然后在**名称**框中，键入"HelloWorld"。 CSHTML 页面是 ASP.NET Web Pages 页。

![创建新的 CSHTML 页面命名 HelloWorld.cshtml](getting-started/_static/image15.png)

单击 **“确定”**。

WebMatrix 创建页，并在编辑器中打开它。

![WebMatrix 编辑器中的新 HelloWorld 页](getting-started/_static/image16.png)

正如您所看到的页面包含主要是普通的 HTML 标记，如下所示顶部块除外：

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

这将添加代码，如稍后您将看到。

请注意，页面的不同部分&mdash;元素名称、 属性和文本，以及在顶部块 — 所有位于不同的颜色。 这称为*语法突出显示*，使得更容易地将清除所有内容。 它是可以轻松地处理在 WebMatrix 中的 web 页面的功能之一。

添加的内容`<head>`和`<body>`元素类似于下面的示例。 （如果你想，您可以只需将以下块复制和使用以下代码替换整个现有页面。）

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

在快速访问工具栏或在**文件**菜单上，单击**保存**。

![在 WebMatrix 快速访问工具栏中保存按钮](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>测试页

在中**文件**工作区中，右键单击*HelloWorld.cshtml*页，然后单击**浏览器中启动**。

![运行在 WebMatrix 功能区中使用运行按钮的页](getting-started/_static/image18.png)

WebMatrix 启动内置的 web 服务器 (IIS Express)，可用于测试您的计算机上的页面。 （无需 IIS Express 在 WebMatrix 中，你将需要发布页面的 web 服务器到某个位置之前无法对其进行测试。）在默认浏览器中显示的页。

![&quot;Hello World&quot;页在浏览器中运行](getting-started/_static/image19.png)

请注意，当在 WebMatrix 中测试一个页面，在浏览器中的 URL 是类似`http://localhost:33651/HelloWorld.cshtml.`名称*localhost*指的是本地服务器，这意味着处理页面时由你自己的计算机上的 web 服务器。 如前所述，WebMatrix 将包含名为 IIS Express 运行时启动的页的 web 服务器程序。

之后的数字*localhost* (例如， *localhost:33651*) 是指*端口号*您的计算机上。 这是 IIS Express 使用为此特定网站的"通道"号。 端口号是随机选择的范围 1024 到 65536 中时创建你的站点，并为您创建的每个站点不同。 （测试自己的网站时，端口号几乎可以肯定将不同数量比 33561。）通过为每个网站使用其他端口，IIS Express 可以让保持连续的你它正在与通信的站点。

当你发布你的站点到公共 web 服务器，不会再看到时，更高版本*localhost*在 URL 中。 此时，你将看到更典型的 URL，例如`http://myhostingsite/mywebsite/HelloWorld.cshtml`或任何页。 您将了解有关稍后在本系列教程中发布站点。

## <a name="adding-some-server-side-code"></a>添加一些服务器端代码

关闭浏览器并返回到 WebMatrix 中的页。

将行添加到代码块，以便它看起来像以下代码：

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

这是很少的 Razor 代码中。 获取当前日期和时间，并将放到此值可能明确*变量*名为`currentDateTime`。 您在阅读更多有关下一教程中的 Razor 语法。

页上，在正文中后`<p>Hello World!</p>`元素中，添加以下：

[!code-html[Main](getting-started/samples/sample4.html)]

此代码获取的值放入`currentDateTime`顶部变量并将其插入到页的标记。 `@`字符将标记中页面的 ASP.NET Web Pages 代码。

运行的页再次 （WebMatrix 将保存所做的更改为你之前运行的页）。 此时会显示的日期和时间的页中。

![&quot;Hello World&quot;与动态生成的时间显示在浏览器中运行页面](getting-started/_static/image20.png)

稍等片刻，然后刷新浏览器中的页。 日期和时间显示更新。

在浏览器中，查看页面源文件。 它类似于以下标记：

[!code-html[Main](getting-started/samples/sample5.html)]

请注意，`@{ }`顶部块不存在。 另请注意，日期和时间显示会显示实际字符串的字符 (`1/18/2012 2:49:50 PM`或其他任何)，而非`@currentDateTime`像中有 *.cshtml*页。 发生了什么情况下面是当运行页面时，ASP.NET 处理的所有代码 （几乎在此情况下） 标记有`@`。 此代码生成输出，并且该输出已插入到页。

## <a name="this-is-what-aspnet-web-pages-are-about"></a>这是 ASP.NET Web Pages 的作用

当您阅读了 ASP.NET Web Pages 生成动态 web 内容时，你已了解了想法。 你只需创建的页面包含您以前看到的相同 HTML 标记。 它还可以包含可执行各种任务的代码。 在此示例中，像普通任务，将当前日期和时间。 如您所见，您可以单引号分隔文件，代码与 HTML 以在页面中生成输出。 当有人请求 *.cshtml*仍在手中的 web 服务器时，在浏览器，ASP.NET 页处理页。 ASP.NET 插入代码的输出 （如果有） 页以 html 格式。 完成代码处理后，ASP.NET 将在生成的页面发送到浏览器。 所有浏览器不断获取为 HTML。 下面是一个关系图：

![ASP.NET 动态生成 HTML 如何的概念流](getting-started/_static/image21.png)

其原理很简单，但有许多有趣的任务可执行代码，并有许多有趣的方式在其中您可以向动态添加 HTML 内容页。 和 ASP.NET *.cshtml*页面，例如从任何 HTML 页上，还可以包括在浏览器本身 （JavaScript 和 jQuery 代码） 中运行的代码。 将介绍所有这些内容在本教程系列和后续条件。

## <a name="coming-up-next"></a>即将推出下一步

在此系列中的下一教程，您了解 ASP.NET Web Pages 编程有点多。

## <a name="additional-resources"></a>其他资源

[从头开始创建一个 ASP.NET 网站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。 这是具体而言，是一个教程使用 WebMatrix (不是 ASP.NET Web Pages)。 它将进入稍有一些我们不会在本教程系列介绍 WebMatrix 的其他功能的更多详细信息。

> [!div class="step-by-step"]
> [下一篇](intro-to-web-pages-programming.md)
