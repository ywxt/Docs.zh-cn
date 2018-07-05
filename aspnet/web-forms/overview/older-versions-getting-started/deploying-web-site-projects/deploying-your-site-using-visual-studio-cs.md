---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
title: 部署你的网站使用 Visual Studio (C#) |Microsoft Docs
author: rick-anderson
description: Visual Studio 包含用于部署网站的工具。 在本教程中了解有关这些工具的详细信息。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2009
ms.topic: article
ms.assetid: cde4ee53-a5d0-4937-a54b-67877e8266c3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
msc.type: authoredcontent
ms.openlocfilehash: d549c615ea822d58ae71876ff3acd28c5f773d8a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399755"
---
<a name="deploying-your-site-using-visual-studio-c"></a>使用 Visual Studio (C#) 部署站点
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_CS.zip)或[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_cs.pdf)

> Visual Studio 包含用于部署网站的工具。 在本教程中了解有关这些工具的详细信息。


## <a name="introduction"></a>介绍

前面的教程介绍了如何部署到 web 宿主提供程序的简单 ASP.NET web 应用程序。 具体而言，本教程说明了如何使用 FileZilla 等 FTP 客户端可以将所需的文件从开发环境转移到生产环境。 Visual Studio 还提供了内置工具可简化部署到 web 宿主提供程序。 本教程探讨这些工具的两个: 复制网站工具，其中您可以将文件移到和从远程 web 服务器使用 FTP 或服务器管理员联系。和发布工具，将整个网站复制到指定位置。


> [!NOTE]
> Visual Studio 提供其他与部署相关的工具包括[Web 安装项目](https://msdn.microsoft.com/library/wx3b589t.aspx)并[Web 部署项目](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en)外接程序。 Web 安装项目包网站的内容和配置信息导出成一个 MSI 文件。 此选项是最有用的 intranet 内部署的网站或公司的销售客户自己的 web 服务器安装的预打包的 web 应用程序。 Web 部署项目外接程序是 Visual Studio 外接程序可帮助之间的指定配置差异生成为开发环境和生产环境。 本系列教程; 不讨论 web 安装项目Web 部署项目进行了总结[*常见配置差异之间开发和生产*](common-configuration-differences-between-development-and-production-cs.md)教程。


## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>使用复制网站工具部署站点

Visual Studio 的复制网站工具是在功能上类似于独立 FTP 客户端。 简单地说，复制网站工具，可连接到远程网站通过 FTP 或 FrontPage 服务器扩展。 类似于 FileZilla 的用户界面，复制网站用户界面包含两个窗格： 左窗格中列出的本地文件，而右侧窗格列出了这些文件在目标服务器上的。

> [!NOTE]
> 复制网站工具才可用于网站项目。 使用 Web 应用程序项目时，visual Studio 确实提供了此工具。

让我们看一看使用复制网站工具发布到生产环境书评应用程序。 因为复制网站工具仅适用于使用网站项目模型的项目，我们只能检查与 BookReviewsWSP 项目配合使用此工具。 打开该项目。

通过单击解决方案资源管理器 （图 1 中有此图标圆圈）; 复制网站图标启动复制网站工具项目或者，您可以从网站菜单上选择复制网站选项。 这两种方法启动图 1; 中所示的复制网站用户界面图 1 中的，左窗格中仅被填充，因为我们尚未连接到远程服务器。


[![复制网站工具的用户界面是划分到两个窗格](deploying-your-site-using-visual-studio-cs/_static/image2.png)](deploying-your-site-using-visual-studio-cs/_static/image1.png)

**图 1**: 复制网站工具的用户界面是划分到两个窗格 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image3.png))


若要部署我们的站点，我们需要先将连接到 web 宿主提供程序。 单击顶部的复制网站用户界面连接按钮。 这将显示在图 2 所示的打开网站对话框。

可以通过从左侧选择四个选项之一来连接到目标网站：

- **文件系统**-选择此选项可从您的计算机将您的网站部署到可访问的文件夹或网络共享。
- **本地 IIS** -使用此选项可将站点部署到您的计算机上安装的 IIS web 服务器。
- **FTP 站点**-连接到远程网站上使用 FTP。
- **远程站点**-连接到远程网站使用 FrontPage 服务器扩展。

大多数 web 宿主提供程序支持 FTP，但更少提供 FrontPage 服务器扩展插件的支持。 为此，我已选择了 FTP 站点的选项，然后输入连接信息，如图 2 中所示。


[![指定目标网站](deploying-your-site-using-visual-studio-cs/_static/image5.png)](deploying-your-site-using-visual-studio-cs/_static/image4.png)

**图 2**： 指定目标网站 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image6.png))


连接后，复制网站工具加载在右窗格中的远程站点的文件，并指示每个文件的状态： 新的、 已删除、 已更改或未更改。 可以将文件从本地站点复制到远程站点或进行相反的转换。

让我们添加一个新页到 BookReviewsWSP 项目，然后将其部署，以便我们可以看到操作中的复制网站工具。 Visual Studio 中名为的根目录中创建一个新的 ASP.NET 页面`Privacy.aspx`。 已使用的母版页的页`Site.master`并将站点的隐私策略添加到此页。 创建此页后，图 3 显示了 Visual Studio。


[![添加新的页名为&lt;代码&gt;Privacy.aspx&lt;o&gt;到网站的根文件夹](deploying-your-site-using-visual-studio-cs/_static/image8.png)](deploying-your-site-using-visual-studio-cs/_static/image7.png)

**图 3**： 添加新的页名为`Privacy.aspx`网站的根文件夹 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image9.png))


接下来，返回到复制网站用户界面。 如图 4 所示，左窗格中现在包括新的文件-`Policy.aspx`和`Policy.aspx.cs`。 更重要的是，这些文件用箭头图标和状态的新，指示它们存在本地站点上但不是在远程站点进行标记。


[![复制网站工具包括新建&lt;代码&gt;Privacy.aspx&lt;o&gt;其左侧窗格中的页面](deploying-your-site-using-visual-studio-cs/_static/image11.png)](deploying-your-site-using-visual-studio-cs/_static/image10.png)

**图 4**： 复制网站工具包括新建`Privacy.aspx`在其左侧窗格中的页 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image12.png))


若要部署的新文件选择它们，然后单击箭头图标以将其传输到远程站点。 在传输完成后`Policy.aspx`和`Policy.aspx.cs`状态未更改本地和远程站点上的文件存在。

列出新的文件，以及复制网站工具突出显示了不同本地和远程站点之间的任何文件。 若要了解此操作，请返回到`Privacy.aspx`页上，并将几个更多的单词添加到的隐私策略。 保存页面，然后返回到复制网站工具。 如图 5 所示，`Privacy.aspx`左侧窗格中的状态为已更改，指示它已与远程站点不同步。


[![复制网站工具指示&lt;代码&gt;Privacy.aspx&lt;o&gt;页已更改](deploying-your-site-using-visual-studio-cs/_static/image14.png)](deploying-your-site-using-visual-studio-cs/_static/image13.png)

**图 5**： 复制网站工具指示`Privacy.aspx`页已更改 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image15.png))


复制网站工具也指示文件是否已删除自上次复制操作。 删除`Privacy.aspx`从本地项目和刷新复制网站工具。 `Privacy.aspx`和`Privacy.aspx.cs`文件保持在左窗格中列出，但其已删除状态指示，它们已被删除自上次复制操作。

## <a name="publishing-a-web-application"></a>Web 应用程序发布

若要部署 web 应用程序从 Visual Studio 中的另一种方法是使用发布选项，这是可通过生成菜单访问。 发布选项显式编译应用程序，然后将复制到指定的远程站点所需的文件的所有。 我们稍后将看到，发布选项是更钝比复制网站工具。 复制网站工具，您可以检查本地和远程站点上的文件，并允许您在上传或下载单个文件，根据需要而发布选项部署整个 web 应用程序。


除了将所有所需的文件复制到指定的远程站点，发布选项还显式编译应用程序。 考虑到 Web 应用程序项目需要显式编译应该会在为发布选项仅适用于 Web 应用程序项目不令人惊讶。 什么可能有点令人惊讶的是发布选项也是适用于网站项目。 如中所述[*确定哪些文件需要将部署到*](determining-what-files-need-to-be-deployed-cs.md)教程中，网站项目都可通过称为过程显式编译*预编译*。 本教程重点介绍使用 Web 应用程序项目中; 的发布选项以后的教程将探讨预编译，此时我们将返回以查看与网站项目一起使用的发布选项。

> [!NOTE]
> 对于网站项目和 Web 应用程序项目的 Visual Studio 中提供的发布选项时，Visual Web Developer 仅提供 Web 应用程序项目的发布选项。


让我们看看部署书评应用程序使用发布选项。 首先在 Visual Studio 中打开 BookReviewsWAP （Web 应用程序项目）。 从发布菜单上选择生成 BookReviewsWAP 项目。 此时会打开一个对话框，提示输入目标位置，以及其他配置选项 （请参阅图 6）。 更像使用复制网站工具可以输入到本地文件夹，在 IIS 上的本地网站，支持 FrontPage 服务器扩展或 FTP 服务器地址的远程网站点的位置。 您可以选择是否在远程 web 服务器上的文件替换为已部署的文件或删除所有发布前在远程站点上的内容。 此外可以指定是否将复制：

- 仅在项目中运行应用程序，省略不必要的源代码和项目相关的文件所需文件。
- 所有项目文件，其中包括源代码文件和 Visual Studio 项目文件，都如解决方案文件。
- 在源项目文件夹中，将所有文件都复制源项目文件夹，而不考虑是否要包含在项目中的所有文件。

此外，还有一个上载的内容选项`App_Data`文件夹。


[![指定目标网站](deploying-your-site-using-visual-studio-cs/_static/image17.png)](deploying-your-site-using-visual-studio-cs/_static/image16.png)

**图 6**： 指定目标网站 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image18.png))


书评应用程序的远程站点包含复制复制网站工具通过 BookReviewsWSP 项目时，部署的文件。 因此，让我们首先删除所有现有内容的发布选项。 此外，让我们只需复制所需的文件，而不是使用不需要的源代码和项目文件会干扰生产环境。 指定后这些选项，单击发布按钮。 接下来的几秒内通过 Visual Studio 将部署所需的文件到目标站点中，在输出窗口中显示其进度。

发布操作完成后，图 7 显示了 FTP 站点上的文件。 请注意，只有标记页和需要服务器端和客户端的支持文件已上传。


[![仅将所需的文件发布到生产环境](deploying-your-site-using-visual-studio-cs/_static/image20.png)](deploying-your-site-using-visual-studio-cs/_static/image19.png)

**图 7**： 仅需要文件发布到生产环境 ([单击以查看实际尺寸的图像](deploying-your-site-using-visual-studio-cs/_static/image21.png))


发布选项是一个不太能体现细微差别的工具比复制网站工具。 复制网站工具允许您以检查本地和远程站点上的文件会发现它们之间的差异，而发布选项提供了任何此类接口。 此外，复制网站工具，可进行一次性更改上, 传或删除单个文件。 发布选项不允许此类精细控制;相反，它将发布*整个*应用程序。 此行为有其优点和缺点。 好的方面，你知道何时使用您不会忘记将重要文件上传的发布选项。 但是，如果在进行少量更改到非常大的网站的发布选项不能更新该页面或两个已修改，但必须等待时 Visual Studio 将部署的整个站点，而是会发生什么情况，请考虑。

不需要某些文件之间的生产和开发环境不同，其内容不常见。 主要示例是应用程序的配置文件， `Web.config`。 因为发布选项会盲目地将复制的 web 应用程序文件时，它会与开发环境中的版本覆盖生产环境中的自定义的配置文件。 后续教程探讨了本主题进一步，并提供了用于部署 web 应用程序时存在此类差异的提示。

## <a name="summary"></a>总结

部署网站涉及将开发环境中的所需的文件复制到生产环境。 在上一教程介绍了如何使用 FileZilla 等 FTP 客户端传输文件。 本教程中检查 Visual Studio 中的两个部署工具: 复制网站工具和发布选项。 复制网站工具相当于 FTP 客户端，因为它可以列出本地计算机和指定的远程计算机，以便轻松上传或下载两台计算机之间的文件上的文件的双窗格界面。 发布选项是一个更钝工具，显式编译项目，然后再部署到指定的目标的整个应用程序。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [使用复制网站工具复制网站](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [实现： 如何部署网站的网站使用复制网站工具](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md)（视频）
- [如何： 发布 Web 应用程序项目](https://msdn.microsoft.com/library/aa983453.aspx)
- [如何： 发布网站](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [安装和部署项目在 Visual Studio 中](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-your-site-using-an-ftp-client-cs.md)
> [下一页](common-configuration-differences-between-development-and-production-cs.md)
