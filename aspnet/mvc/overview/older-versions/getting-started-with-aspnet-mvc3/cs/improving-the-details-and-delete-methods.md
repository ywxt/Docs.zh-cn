---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
title: 改进 Details 和 Delete 方法 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 3f42edd9-c5b8-4712-9055-970f7d38e350
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 5dc786a05822328bc4317c582d135f26fb168dfb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830660"
---
<a name="improving-the-details-and-delete-methods-c"></a>改进 Details 和 Delete 方法 (C#)
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。
> 
> 
> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。


在本教程的此部分中，您将进行自动生成的一些改进`Details`和`Delete`方法。 这些更改不是必需的但有几个小位的代码，可以轻松地增强应用程序。

## <a name="improving-the-details-and-delete-methods"></a>改进 Details 和 Delete 方法

当你已搭建基架`Movie`控制器，ASP.NET MVC 生成的代码起作用的良好，但可以进行的更加强大，只需几个较小的更改。

打开`Movie`控制器并修改`Details`方法通过返回`HttpNotFound`电影时找不到。 您还应修改`Details`方法默认值设置为传递给它的 ID。 (进行类似更改`Edit`中的方法[第 6 部分](examining-the-edit-methods-and-edit-view.md)本教程。)但是，必须更改的返回类型`Details`方法从`ViewResult`到`ActionResult`，因为`HttpNotFound`方法不返回`ViewResult`对象。 下面的示例显示了已修改`Details`方法。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample1.cs)]

代码首次建立容易搜索的数据使用`Find`方法。 该代码验证的一项重要的安全功能，我们构建到方法为`Find`方法已经找到电影，该代码尝试使用它执行任何操作之前。 例如，黑客可能错误引入站点通过更改创建中的链接的 URL`http://localhost:xxxx/Movies/Details/1`为类似于`http://localhost:xxxx/Movies/Details/12345`（或不代表任何实际电影的一些其他值）。 如果没有检查有空电影，这可能导致数据库错误。

同样，更改`Delete`并`DeleteConfirmed`方法来指定 ID 参数的默认值并返回`HttpNotFound`电影时找不到。 已更新`Delete`中的方法`Movie`控制器如下所示。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample2.cs)]

请注意，`Delete`方法不会删除数据。 执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。 有关详细信息，请参阅 Stephen Walther 的博客文章[ASP.NET MVC 提示 #46 — 不使用删除链接，因为他们创建的安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。 下面显示了两个方法签名：

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample3.cs)]

公共语言运行时 (CLR) 需要重载的方法具有一个唯一的签名 （相同的名称，不同的参数列表）。 但是，在这里需要两个 Delete 方法-一个用于 GET-和另一个用于 POST 都需要相同的签名。 （它们都需要接受单个整数作为参数。）

若要对其进行扩展，可以执行一些操作。 一个是为方法提供不同的名称。 这就是我们在前面的示例中。 但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。 该示例中也提供了解决方案，即向 `DeleteConfirmed` 方法添加 `ActionName("Delete")` 属性。 这有效地执行映射为路由系统，以便某一 URL 包含<em>/Delete/</em>对于 POST 请求将发现`DeleteConfirmed`方法。

若要避免具有相同的名称和签名的方法问题的另一种方法是手动更改 POST 方法以包括未使用的参数的签名。 例如，一些开发人员添加的参数类型`FormCollection`传递给 POST 方法中，然后只需不使用参数：

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="wrapping-up"></a>总结

你现在具有一个完整的 ASP.NET MVC 应用程序在 SQL Server Compact 数据库中存储数据。 可以创建、 读取、 更新、 删除和搜索电影。

![](improving-the-details-and-delete-methods/_static/image1.png)

这一基本教程能满足你的启动使控制器，将其关联到视图，并传递硬编码数据。 然后创建并设计数据模型。 实体框架 Code First 从动态，数据模型创建数据库和 ASP.NET MVC 基架系统自动生成的操作方法和视图的基本 CRUD 操作。 然后添加搜索窗体，用户可在数据库中搜索。 更改要包括的数据，新列的数据库，然后更新两个页，以创建并显示此新数据。 通过将标记中的属性与数据模型添加验证`DataAnnotations`命名空间。 生成验证运行客户端和服务器上。

如果你想要部署你的应用程序，很有帮助首先测试你的本地 IIS 7 服务器上的应用程序。 可以使用此[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;)链接，以启用 ASP.NET 应用程序的 IIS 设置。 请参阅以下部署链接：

- [ASP.NET 部署内容映射](https://msdn.microsoft.com/library/dd394698.aspx)
- [启用 IIS 7.x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Web 应用程序项目部署](https://msdn.microsoft.com/library/dd394698.aspx)

我现在鼓励您转到我们的中级[为 ASP.NET MVC 应用程序创建实体框架数据模型](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)并[MVC Music 商店](../../mvc-music-store/mvc-music-store-part-1.md)教程，若要浏览[ASP.NETMSDN 上的文章](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)，并查看许多视频和资源，请访问[ https://asp.net/mvc ](https://asp.net/mvc)甚至更多地了解 ASP.NET MVC ！ [ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是一个很好的提出的问题。

请尽情体验吧！

-Scott Hanselman ([ http://hanselman.com ](http://hanselman.com)并[ @shanselman ](http://twitter.com/shanselman) Twitter 上) 和 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [上一篇](adding-validation-to-the-model.md)
