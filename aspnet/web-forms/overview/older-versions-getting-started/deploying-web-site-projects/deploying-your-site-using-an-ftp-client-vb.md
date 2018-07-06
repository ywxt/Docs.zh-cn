---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
title: 使用 FTP 客户端 (VB) 部署站点 |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET 应用程序的最简单方法是手动将从开发环境所需的文件复制到生产环境。 此应用程序...
ms.author: aspnetcontent
ms.date: 04/01/2009
ms.assetid: 09279194-bcf9-4b59-a09d-c68e5926a758
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b4d39ceb19e1a916775948c531c3e017e2d1a2d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835983"
---
<a name="deploying-your-site-using-an-ftp-client-vb"></a>使用 FTP 客户端 (VB) 部署站点
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_VB.zip)或[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_vb.pdf)

> 部署 ASP.NET 应用程序的最简单方法是手动将从开发环境所需的文件复制到生产环境。 本教程演示如何使用 FTP 客户端到 web 主机提供商从桌面上获取文件。


## <a name="introduction"></a>介绍

上一个教程介绍了组成少量的 ASP.NET 页、 母版页、 自定义库一个简单书籍查看 ASP.NET web 应用`Page`类，许多映像，并且三个 CSS 样式表。 我们现已准备好部署到 web 主机提供商，此时，该应用程序将连接到 Internet，与任何人都可访问此应用程序 ！


从我们中的讨论[*确定哪些文件需要将部署到*](determining-what-files-need-to-be-deployed-vb.md)教程，我们知道需要复制到 web 宿主提供程序的文件。 （回想一下，哪些文件复制取决于是否在编译应用程序显式或自动。）但是，我们如何才能让文件从开发环境 （我们的桌面） 到生产环境 （由 web 主机提供商托管的 web 服务器）？ [ **F** ile **T** ransfer **P**协议 (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol)是常用的协议将文件从一台计算机复制到另一个，通过网络。 另一个选项是 FrontPage 服务器扩展 (FPSE)。 本教程重点介绍使用独立 FTP 客户端软件部署到生产环境的必要文件从开发环境。

> [!NOTE]
> Visual Studio 包含用于通过 FTP; 发布网站工具下一教程中介绍了这些工具，以及看使用 FPSE 的工具。


若要使用的 FTP，我们需要复制文件*FTP 客户端*开发环境。 FTP 客户端是用于将文件从安装到正在运行的计算机的计算机复制的应用程序*FTP 服务器*。 （如果大多数一样，web 宿主提供程序支持通过 FTP，文件传输，则在其 web 服务器上运行的 FTP 服务器。）有大量的 FTP 客户端应用程序。 在 web 浏览器可以为 FTP 客户端甚至两倍。 我最喜欢的 FTP 客户端，我将用于本教程中，一个是[FileZilla](http://filezilla-project.org/)，免费的开源 FTP 客户端适用于 Windows、 Linux 和 Mac。 但是，任何 FTP 客户端将工作，请使用在最熟悉的任何客户端。

在您按照沿你将需要使用 web 宿主提供程序之前创建一个帐户可以完成本教程或后续条件。 上一教程中所述，有许多 web 宿主提供程序公司使用了范围广泛的价格、 功能和服务质量。 我将使用本教程系列[折扣 ASP.NET](http://discountasp.net)作为我的 web 宿主提供程序，但你可以遵循任何 web 宿主提供程序，只要它们支持您的网站开发中的 ASP.NET 版本。 （这些教程中创建使用 ASP.NET 3.5。）此外，由于我们会将文件复制到 web 宿主提供程序使用在本教程中，并且在将来的 FTP 它是命令性 web 宿主提供程序支持对 web 服务器的 FTP 访问。 几乎所有的 web 主机提供商提供此功能，但在注册之前，您应仔细检查。

## <a name="deploying-the-book-review-web-application-project"></a>部署书籍查看 Web 应用程序项目

请记住，书评 web 应用程序的两个版本： 一个使用 Web 应用程序项目模型 (BookReviewsWAP) 和另一个使用网站项目模型 (BookReviewsWSP) 实现。 项目类型会影响是否自动或显式编译站点时，该编译模式决定了需要部署的文件。 我们将说明分别部署 BookReviewsWAP 和 BookReviewsWSP 项目从 BookReviewsWAP 开始。 请花费片刻时间来下载这些两个 ASP.NET 应用程序，如果你尚未这样做已经。

通过导航到启动 BookReviewsWAP 项目`BookReviewsWAP`文件夹，然后双击`BookReviewsWAP.sln`文件。 部署项目之前务必生成它以确保对源代码的任何更改都包含在编译的程序集。 若要生成项目转到生成菜单并选择生成 BookReviewsWAP 菜单选项。 这将在项目中的源代码编译到单个程序集， `BookReviewsWAP.dll`，这放置在`Bin`文件夹。

我们现已准备好部署所需的文件 ！ 启动 FTP 客户端并连接到 web 主机提供商的 web 服务器。 （与 web 托管公司的名义注册时它们将通过电子邮件发送您如何连接到 FTP 服务器的信息; 这包括 FTP 服务器，以及用户名和密码的地址。）

从您的桌面的以下文件复制到 web 宿主提供程序上的根网站文件夹中。 当您为 web 服务器的 FTP 在 web 承载提供程序时您很可能在网站根目录。 但是，某些 web 宿主提供程序具有一个名为子`www`或`wwwroot`可用作你的网站文件的根文件夹。 最后，当 FTPing 文件时您可能需要在生产环境中的上创建相应的文件夹结构`Bin`文件夹中，`Fiction`文件夹中，`Images`文件夹中，依次类推。

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- 完整内容`Styles`文件夹
- 完整内容`Images`文件夹 (及其子文件夹， `BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

图 1 显示了 FileZilla 后已复制所需的文件。 FileZilla 显示在左侧和右侧的远程计算机上的文件在本地计算机上的文件。 如图 1 所示，ASP.NET 源代码文件，如`About.aspx.vb`，位于本地计算机 （开发环境），但未被其因为无需使用时部署代码文件复制到 web 宿主提供程序 （在生产环境）显式编译。

> [!NOTE]
> 具有源代码文件在生产服务器上，没有什么坏处它们将被忽略。 ASP.NET，以便即使生产服务器上存在的源代码文件将无法访问它们对你的网站的访客，默认情况下禁止对源代码文件的 HTTP 请求。 (即，如果用户尝试访问`http://www.yoursite.com/Default.aspx.vb`他们将得到一个错误页面，介绍的这些类型的文件-`.vb`文件-被禁止。)


[![使用 FTP 客户端将从您的桌面的所需的文件复制到 Web 主机提供商的 Web 服务器。](deploying-your-site-using-an-ftp-client-vb/_static/image2.png)](deploying-your-site-using-an-ftp-client-vb/_static/image1.png)

**图 1**： 使用 FTP 客户端将从你的桌面的所需的文件复制到 Web 主机提供商的 Web 服务器 ([单击以查看实际尺寸的图像](deploying-your-site-using-an-ftp-client-vb/_static/image3.png))


在部署你的站点后请花费片刻时间以测试网站。 如果你只购买一个域名并配置 DNS 设置正确，可以通过输入你的域名访问你的站点。 或者，您的 web 主机提供商应提供你指向你的站点的 url 这看起来好像*accountname*。*webhostprovider*.com 或*webhostprovider*.com /*accountname*。 例如，我在折扣 ASP.NET 上的帐户的 URL 是： `http://httpruntime.web703.discountasp.net`。

图 2 显示了已部署的书评站点。 请注意，我将折扣 ASP 上查看它。NET 的服务器在`http://httpruntime.web703.discountasp.net`。 在此时间点与 Internet 建立连接的任何人都无法查看我的网站 ！ 如我们所料，该站点的外观和行为就像它未在开发环境中测试它时。

> [!NOTE]
> 如果遇到错误时查看你的应用程序需要一段时间来确保您部署正确的文件集。 接下来，检查错误消息，请参阅是否它将显示有关该问题有什么解决办法。 接下来，转到 web 主机公司的支持人员或将问题发布到相应论坛[ASP.NET 论坛](https://forums.asp.net/)。


[![通讯簿评审站点是在具有 Internet 连接的任何人都现在可访问。](deploying-your-site-using-an-ftp-client-vb/_static/image5.png)](deploying-your-site-using-an-ftp-client-vb/_static/image4.png)

**图 2**: 通讯簿评审站点是现在可以访问在具有 Internet 连接的任何人 ([单击以查看实际尺寸的图像](deploying-your-site-using-an-ftp-client-vb/_static/image6.png))


## <a name="deploying-the-book-review-web-site-project"></a>部署书籍检查网站项目

使用自动编译，如 BookReviewsWSP 网站项目，将 ASP.NET 应用程序部署时在无编译的程序集`Bin`文件夹。 因此，web 应用程序的源代码文件必须部署到生产环境。 让我们完成此过程。

为与 Web 应用程序项目是明智的第一次生成前将其部署应用程序。 而构建的网站项目不会创建程序集，它会检查页中的任何编译时错误。 若要查找这些错误现在使用效果更佳而不是让你的站点访问者发现它们为你 ！

一旦您已成功生成项目，使用 FTP 客户端将以下文件复制到 web 宿主提供程序上的根网站文件夹。 您可能需要在生产环境中创建相应的文件夹结构。

> [!NOTE]
> 如果已部署项目但仍想要尝试部署 BookReviewsWSP 项目的 BookReviewsWAP，首先删除所有部署 BookReviewsWAP 时已上传 web 服务器上的文件，然后为 BookReviewsWSP 部署文件。


- `~/Default.aspx`
- `~/Default.aspx.vb`
- `~/About.aspx`
- `~/About.aspx.vb`
- `~/Site.master`
- `~/Site.master.vb`
- `~/Web.config`
- `~/Web.sitemap`
- 完整内容`Styles`文件夹
- 完整内容`Images`文件夹 (及其子文件夹， `BookCovers`)
- `~/App_Code/BasePage.vb`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.vb`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.vb`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.vb`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.vb`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.vb`

图 3 显示了所需的文件复制后 FileZilla。 正如您所看到的 ASP.NET 源代码文件，如`About.aspx.vb`，因为需要时使用自动部署代码文件均存在于本地计算机 （开发环境） 和 web 宿主提供程序 （在生产环境）编译。


[![使用 FTP 客户端将从您的桌面的所需的文件复制到 Web 主机提供商的 Web 服务器](deploying-your-site-using-an-ftp-client-vb/_static/image8.png)](deploying-your-site-using-an-ftp-client-vb/_static/image7.png)

**图 3**： 使用 FTP 客户端将从你的桌面的所需的文件复制到 Web 主机提供商的 Web 服务器 ([单击以查看实际尺寸的图像](deploying-your-site-using-an-ftp-client-vb/_static/image9.png))


应用程序的编译模式不影响用户体验。 相同的 ASP.NET 页面访问，它们的外观和是否已创建网站，使用 Web 应用程序项目模型或网站项目模型的行为相同。

## <a name="updating-a-web-application-on-production"></a>更新生产上的 Web 应用程序

Web 应用程序开发和部署不是一次性的过程。 例如，创建书籍评论网站时我构建了的各个页面，并在我的个人计算机 （开发环境） 编写的随附的代码。 达到稳定状态之后, 我部署我的应用程序，以便其他人可以访问该站点并阅读我的评审。 但部署不会将结束此站点上我开发。 可能会添加更多书籍评审或实现新功能，例如允许我的访客率书籍或保留他们自己的意见。 此类增强功能将在开发环境中开发和完成后，可能需要进行部署。 开发和部署，因此，在循环。 开发的应用程序，然后将其部署。 同时站点是实时和生产环境中，添加新功能，并随着时间推移，这使得需要重新部署应用程序修复 bug。 等，依此类推。

正如您所料，重新部署 web 应用程序只需复制新的和已更改文件时。 无需重新部署不变的页或服务器或客户端支持文件 （尽管这样做会造成任何伤害）。

> [!NOTE]
> 使用显式编译是无论何时向项目添加新的 ASP.NET 页面或进行任何与代码相关的更改，您需要重新生成项目，这会更新中的程序集时，需要注意的一点`Bin`文件夹。 因此，您将需要更新生产 （以及其他新的和更新内容） 上的 web 应用程序时，将此更新的程序集复制到生产环境。


此外了解到的任何更改`Web.config`中的文件或`Bin`目录停止并重新启动该网站的应用程序池。 如果使用存储会话状态`InProc`模式 （默认值），然后你网站的访问者将会丢失其会话状态时修改这些密钥文件。 若要避免这种问题，请考虑将存储会话使用`StateServer`或`SQLServer`模式。 有关本主题的详细信息请阅读[会话状态模式](https://msdn.microsoft.com/library/ms178586.aspx)。

最后，请记住，重新部署应用程序可能需要几秒钟到几分钟，具体取决于的数量和复制到生产环境所需的文件的大小。 在此期间用户访问您的网站可能会遇到错误或异常行为。 你可以"禁用"将整个应用程序通过添加一个名为页`App_Offline.htm`介绍给您的用户的应用程序的根目录到该站点已关闭进行维护 （或任何内容），并且会是备份很快。 当`App_Offline.htm`文件存在，则 ASP.NET 运行时将所有传入请求重定向到该页面。

## <a name="summary"></a>总结

Web 应用程序部署时，需要将所需的文件从开发环境复制到生产环境。 按其通过网络传输文件的最常见方式是文件传输协议 (FTP) 和大多数 web 宿主提供程序支持对 web 服务器的 FTP 访问。 在本教程中我们已了解如何使用 FTP 客户端将所需的文件部署到 web 服务器。 部署完成后，该网站可访问的任何人使用连接到 Internet ！

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [应用\_Offline.htm 和解决"IE 友好错误"功能](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [会话状态模式](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [上一页](determining-what-files-need-to-be-deployed-vb.md)
> [下一页](deploying-your-site-using-visual-studio-vb.md)
