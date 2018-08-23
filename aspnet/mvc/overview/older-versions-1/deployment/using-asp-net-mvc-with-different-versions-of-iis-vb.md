---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: ASP.NET MVC 中使用不同版本的 IIS (VB) |Microsoft Docs
author: microsoft
description: 在本教程中，您将学习如何使用 ASP.NET MVC 中，并且 URL 路由，使用不同版本的 Internet Information Services。 了解不同的策略...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: e83a5f8e5d1726dc2f39a9aee6515995ce0ed157
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833114"
---
<a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>ASP.NET MVC 中使用不同版本的 IIS (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 在本教程中，您将学习如何使用 ASP.NET MVC 中，并且 URL 路由，使用不同版本的 Internet Information Services。 了解 ASP.NET MVC 中使用的 IIS 7.0 （经典模式）、 IIS 6.0 和 IIS 的早期版本不同的策略。


ASP.NET MVC 框架会在 ASP.NET 路由取决于浏览器请求路由到控制器操作。 为了充分利用 ASP.NET 路由，您可能需要在 web 服务器上执行其他配置步骤。 这完全取决于 Internet 信息服务 (IIS) 和请求处理你的应用程序的模式下的版本。

下面是不同版本的 IIS 的摘要：

- IIS 7.0 （集成模式）-使用 ASP.NET 路由所需任何特殊配置。
- IIS 7.0 （经典模式）-你需要执行特殊的配置以使用 ASP.NET 路由。
- IIS 6.0 或下面-你需要执行特殊的配置以使用 ASP.NET 路由。

IIS 的最新版本是版本 7.5 （在 Win7)。 IIS 7 的 IIS 是包含 Windows Server 2008 和 VISTA/SP1 和更高版本。 也可以安装任意版本的 Vista 操作系统，除 Home Basic 上的 IIS 7.0 (请参阅[ https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx ](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx))。

IIS 7.0 支持两种模式，用于处理请求。 可以使用集成模式下或经典模式。 您不必执行任何特殊配置步骤，使用 IIS 7.0 集成模式下时。 但是，您确实需要在经典模式下使用 IIS 7.0 时执行其他配置。

Microsoft Windows Server 2003 包括 IIS 6.0。 使用 Windows Server 2003 操作系统时，您不能升级到 IIS 7.0 IIS 6.0。 使用 IIS 6.0 时，必须执行其他配置步骤。

Microsoft Windows XP Professional 包括 IIS 5.1。 使用 IIS 5.1 时，必须执行其他配置步骤。

最后，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包括 IIS 5.0。 使用 IIS 5.0 时，必须执行其他配置步骤。

## <a name="integrated-versus-classic-mode"></a>与经典模式集成

IIS 7.0 可以处理请求使用两种不同的请求处理模式： 集成和经典。 集成模式下提供更好的性能和更多的功能。 经典模式下所包含的向后与 IIS 的早期版本的兼容性。

请求处理模式取决于应用程序池。 您可以确定特定的 web 应用程序通过确定与应用程序相关联的应用程序池使用的处理模式。 请执行这些步骤：

1. 启动 Internet 信息服务管理器
2. 在连接窗口中，选择一个应用程序
3. 在操作窗口中，单击**基本设置**链接以打开编辑应用程序对话框 （请参见图 1）
4. 记下所选的应用程序池。

默认情况下，IIS 配置为支持两个应用程序池： **DefaultAppPool**并**Classic.NET AppPool**。 如果选择了 DefaultAppPool，然后在集成的请求处理模式下运行你的应用程序。 如果选择了经典的.NET 应用程序池，你的应用程序在经典的请求处理模式下运行。


[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**图 1**： 检测请求处理模式 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))


请注意，您可以修改在编辑应用程序对话框中的请求处理模式。 单击选择按钮，并将更改应用程序与关联的应用程序池。 认识到从经典部署模型的 ASP.NET 应用程序更改为集成模式下时有兼容性问题。 有关详细信息，请参阅以下文章：

- 升级到 Windows Vista 和 Windows Server 2008--上的 IIS 7.0 的 ASP.NET 1.1 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- 使用 IIS 7.0 的 ASP.NET 集成 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)


如果 ASP.NET 应用程序使用 DefaultAppPool，您不需要执行任何其他步骤以获得 ASP.NET 路由 （以及因此 ASP.NET MVC） 工作。 但是，如果 ASP.NET 应用程序配置为使用 Classic.NET AppPool 然后往下读，则必须多工作要做。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>通过较旧版本的 IIS 使用 ASP.NET MVC

如果您需要使用 IIS 7.0 比旧版本的 IIS 使用 ASP.NET MVC 或需要在经典模式下使用 IIS 7.0，则必须使用两个选项。 首先，您可以修改要使用文件扩展名的路由表。 例如，而不是请求的 URL，如 /Store/Details，将请求的 URL，如 /Store.aspx/Details。

第二个选项是创建所谓*通配符脚本映射*。 通配符脚本映射，可将每个请求映射到 ASP.NET 框架。

如果你无权访问你的 web 服务器 (例如，应用程序托管的 Internet 服务提供商在 ASP.NET MVC) 到你将需要使用第一个选项。 如果不想要修改的 Url 中，外观，并且可以访问你的 web 服务器，您可以使用第二个选项。

我们将探讨以下各节详细地每个选项。

## <a name="adding-extensions-to-the-route-table"></a>将扩展添加到路由表

若要获取 ASP.NET 路由，以使用较旧版本的 IIS 的最简单方法是修改您在 Global.asax 文件中的路由表。 默认值，并在列表 1 中的未修改的 Global.asax 文件将配置一个名为默认路由的路由。

**代码清单 1-Global.asax （未修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

在列表 1 中配置的默认路由，可以如下所示的路由 Url:

/ Home/Index

/ 产品/详细信息/3

/ 产品

遗憾的是，较旧版本的 IIS 不会将这些请求传递给 ASP.NET 框架。 因此，不会将这些请求路由到控制器。 例如，如果浏览器请求进行 URL /Home/索引然后将图 2 中显示错误页。


[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**图 2**： 接收到 404 找不到错误 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))


较旧版本的 IIS 只能映射到 ASP.NET 框架的某些请求。 对于带有正确的文件扩展名的 URL 必须为该请求。 例如，对于 /SomePage.aspx 请求获取映射到 ASP.NET 框架。 但是，对于 /SomePage.htm 请求却没有。

因此，若要获取以便使用 ASP.NET 路由，我们必须修改默认路由，使之包含映射到 ASP.NET 框架的文件扩展名。

这是使用名为的脚本`registermvc.wsf`。 它是 ASP.NET MVC 1 版本中附带`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`，但自 ASP.NET 2 起此脚本已被移动到 ASP.NET Futures，网址[ http://aspnet.codeplex.com/releases/view/39978 ](http://aspnet.codeplex.com/releases/view/39978)。

执行此脚本向 IIS 注册一个新的.mvc 扩展。 注册.mvc 扩展后，可以修改路由在 Global.asax 文件中的，以便路由使用.mvc 扩展。

列表 2 中已修改的 Global.asax 文件适用于较旧版本的 IIS。

**代码清单 2-Global.asax （修改与扩展）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]


重要提示： 请记住要更改的 Global.asax 文件后，再次构建 ASP.NET MVC 应用程序。


有两个代码清单 2 中的 Global.asax 文件的重要更改。 现在有两个路由在 Global.asax 中定义。 现在，默认路由，第一个路由的 URL 模式如下所示：

{controller}.mvc/{action}/{id}

.Mvc 扩展添加更改的 ASP.NET 路由模块截获的文件的类型。 进行此更改后，ASP.NET MVC 应用程序现在将如下所示的请求路由：

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

第二个路由，根路由是新增的。 根路由此 URL 模式是空字符串。 此路由是必需的匹配对应用程序的根目录发出的请求。 例如，根路由将匹配的请求，如下所示：

[http://www.YourApplication.com/](http://www.YourApplication.com/)

路由表对这些修改后，将需要确保所有应用程序中的链接是使用这些新的 URL 模式兼容。 换而言之，请确保您的所有链接包含.mvc 扩展。 如果您使用 Html.ActionLink() 帮助器方法生成你的链接，然后不应需要进行任何更改。


而不是使用 registermvc.wcf 脚本，可以将一个新的扩展添加到手动映射到 ASP.NET 框架的 IIS。 在自行添加一个新的扩展，请确保相应的复选框标记为**验证该文件是否存在**未选中。


## <a name="hosted-server"></a>托管的服务器

您始终没有访问你的 web 服务器。 例如，如果托管的 ASP.NET MVC 应用程序中使用的 Internet 托管提供者，然后将不一定可以访问到 IIS。

在这种情况下，应使用一个映射到 ASP.NET framework 的现有文件扩展名。 文件扩展名映射到 ASP.NET 的示例包括.aspx、.axd 和.ashx 扩展。

例如，修改后的 Global.asax 文件中列出的 3 使用.aspx 扩展名而不是.mvc 扩展。

**代码清单 3-Global.asax （使用.aspx 扩展修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

列表 3 中的 Global.asax 文件正是除外，它使用.aspx 扩展名而非.mvc 扩展这一事实的上一个 Global.asax 文件同名。 您无需使用.aspx 扩展名在远程 web 服务器上执行任何设置。

## <a name="creating-a-wildcard-script-map"></a>创建通配符脚本映射

如果不想要修改 ASP.NET MVC 应用程序的 Url，并且可以访问你的 web 服务器，则必须使用一个附加选项。 可以创建映射到 ASP.NET 框架的 web 服务器的所有请求的通配符脚本映射。 这样一来，您可以使用默认 ASP.NET MVC 路由表与 IIS 7.0 （在经典模式下） 或 IIS 6.0。

请注意，此选项会导致 IIS 以截获对 web 服务器发出的每个请求。 这包括图像、 经典 ASP 页中和 HTML 页面的请求。 因此，启用通配符脚本映射到 ASP.NET does 会影响性能。

下面是如何为 IIS 7.0 中启用通配符脚本映射：

1. 在连接窗口中选择你的应用程序
2. 请确保**功能**选择视图
3. 双击**处理程序映射**按钮
4. 单击**添加通配符脚本映射**链接 （请参见图 3）
5. 将路径输入到 aspnet\_isapi.dll 文件 （这可以从 PageHandlerFactory 脚本映射中复制此路径）
6. 输入名称 MVC
7. 单击**确定**按钮


[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**图 3**： 使用 IIS 7.0 创建通配符脚本映射 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))


请按照以下步骤来使用 IIS 6.0 创建通配符脚本映射操作：

1. 右键单击网站，然后选择属性
2. 选择**主目录**选项卡
3. 单击**配置**按钮
4. 选择**映射**选项卡
5. 单击**插入**按钮 （请参见图 4）
6. 粘贴到 aspnet 路径\_isapi.dll 到可执行文件的字段 （.aspx 文件的脚本映射可将此路径的复制）
7. 取消选中复选框标记为**验证该文件是否存在**
8. 单击**确定**按钮


[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**图 4**： 使用 IIS 6.0 创建通配符脚本映射 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))


启用通配符脚本映射后，您需要修改 Global.asax 文件中的路由表，以使其包括根路由。 否则，您将收到错误页图 5 中，为你的应用程序的根页面请求时。 可以使用列表 4 中修改后的 Global.asax 文件。


[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**图 5**： 缺少根路由错误 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))


**列表 4-Global.asax （修改根路由的情况）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

为 IIS 7.0 或 IIS 6.0 中启用通配符脚本映射后，可以发出使用默认路由表，如下所示的请求：

/

/ Home/Index

/ 产品/详细信息/3

/ 产品

## <a name="summary"></a>总结

本教程的目的是说明如何使用 ASP.NET MVC 使用的较旧版本的 IIS （或在经典模式下的 IIS 7.0） 时。 我们讨论了获取以便使用较旧版本的 IIS 使用 ASP.NET 路由的两个方法： 修改默认路由表，或者创建一个通配符脚本映射。

第一个选项要求您修改 ASP.NET MVC 应用程序中使用的 Url。 此第一个选项的其中一个显著优点是您无需访问 web 服务器即可修改路由表。 这意味着您可以使用此第一个选项，即使承载在 ASP.NET MVC 应用程序的 Internet 托管公司。

第二个选项是创建通配符脚本映射。 此第二个选项的优点是不需要修改你的 Url。 此第二个选项的缺点是它可以对 ASP.NET MVC 应用程序的性能影响。

> [!div class="step-by-step"]
> [上一篇](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
