---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 入门 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本是可以在此处使用 Visual Studio 2015。 新教程使用 ASP.NET Core MVC 6，它提供许多 improvem...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 8417be945e16ed99e655f628134c9190429f1d67
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825279"
---
<a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 入门
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

 本教程将介绍构建 ASP.NET MVC 5 web 应用程序使用的基础知识[Visual Studio 2017](https://www.visualstudio.com/)。 有关教程的最后一个源位于[GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)


 本教程由编写[Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) )， [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) )并[Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )

 需要一个 Azure 帐户才能将此应用程序部署到 Azure:

 - 你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。
 - 你可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。


## <a name="getting-started"></a>入门

首先，安装并运行[Visual Studio 2017](https://www.visualstudio.com/)。

Visual Studio 是一个 IDE 或集成的开发环境。 就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。 在 Visual Studio 中没有向您显示各种可用选项，底部的列表。 此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。 (例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)


![](getting-started/_static/image1.png)  


## <a name="creating-your-first-application"></a>创建第一个应用程序

单击**新的项目**，然后选择 Visual C# 在左侧，然后**Web** ，然后选择**ASP.NET Web 应用程序 (.NET Framework)**。 命名你的项目"MvcMovie"，然后单击**确定**。

![](getting-started/_static/image2.png)

在中**新建 ASP.NET 项目**对话框中，单击**MVC** ，然后单击**确定**。

![](getting-started/_static/image3.png)

Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！ 这是简单"Hello World ！" 项目和它的启动应用程序的好时机。

![](getting-started/_static/image4.png)

单击 F5 启动调试。 F5 会导致 Visual Studio 启动[IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)和运行 web 应用。 然后，visual Studio 启动浏览器并打开应用程序的主页。 请注意，在浏览器地址栏将显示`localhost:port#`并不是类似于`example.com`。 这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。 Visual Studio 运行时 web 项目，一个随机端口用于 web 服务器。 下图中的端口号是 1234年。 当您运行该应用程序时，您将看到不同的端口号。

![](getting-started/_static/image5.png)

即时可用的此默认模板也提供家庭、 联系人以及有关页面。 上面的图像不会显示**主页**，**有关**并**联系人**链接。 具体取决于浏览器窗口的大小，可能需要单击导航图标可查看下面的链接。

![](getting-started/_static/image6.png)  

应用程序还提供支持注册和登录。 下一步是要更改此应用程序的工作方式有点了解 ASP.NET MVC。 关闭 ASP.NET MVC 应用程序，让我们将一些代码。

当前教程的列表，请参阅[MVC 建议文章](../mvc-learning-sequence.md)。

## <a name="see-this-app-running-on-azure"></a>请参阅在 Azure 上运行此应用程序

若要查看已完成的站点作为实时 web 应用运行吗？ 只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果你还没有帐户，你具有以下选项：

- [免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。
- [激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。

> [!div class="step-by-step"]
> [下一篇](adding-a-controller.md)
