---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: 检查 Details 和 Delete 方法 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: e28a901fec66f03321dd94b6938f12d7ed84d1f9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833742"
---
<a name="examining-the-details-and-delete-methods"></a>检查 Details 和 Delete 方法
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本教程的此部分中，您将查看自动生成`Details`和`Delete`方法。

## <a name="examining-the-details-and-delete-methods"></a>检查 Details 和 Delete 方法

打开`Movie`控制器并检查`Details`方法。

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

创建此操作方法的 MVC 基架引擎添加显示调用方法的 HTTP 请求的注释。 在这种情况下它是`GET`包含三个 URL 段，请求`Movies`控制器`Details`方法和一个`ID`值。

代码首次建立容易搜索的数据使用`Find`方法。 该代码验证的一项重要的安全功能内置于该方法是`Find`方法已经找到电影，该代码尝试使用它执行任何操作之前。 例如，黑客可能错误引入站点通过更改创建中的链接的 URL`http://localhost:xxxx/Movies/Details/1`为类似于`http://localhost:xxxx/Movies/Details/12345`（或不代表任何实际电影的一些其他值）。 如果您没有检查是否有空电影，有空电影将导致数据库错误。

检查 `Delete` 和 `DeleteConfirmed` 方法。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

请注意，`HTTP Get``Delete`方法不会删除指定的电影，则返回的电影视图可在其中提交 (`HttpPost`) 删除... 执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。 有关详细信息，请参阅 Stephen Walther 的博客文章[ASP.NET MVC 提示 #46 — 不使用删除链接，因为他们创建的安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。 下面显示了两个方法签名：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

公共语言运行时 (CLR) 需要重载方法拥有唯一的参数签名（相同的方法名称但不同的参数列表）。 但是，在这里需要两个 Delete 方法-一个用于 GET-和另一个用于 POST 都有相同的参数签名。 （它们都需要接受单个整数作为参数。）

若要对其进行扩展，可以执行一些操作。 一个是为方法提供不同的名称。 这正是前面的示例中的基架机制进行的操作。 但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。 该示例中也提供了解决方案，即向 `DeleteConfirmed` 方法添加 `ActionName("Delete")` 属性。 这有效地执行映射为路由系统，以便某一 URL 包含<em>/Delete/</em>对于 POST 请求将发现`DeleteConfirmed`方法。

另一种常见的方法来避免问题具有相同的名称和签名的方法是手动更改 POST 方法以包括未使用的参数的签名。 例如，一些开发人员添加的参数类型`FormCollection`传递给 POST 方法中，然后只需不使用参数：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>总结

你现在具有一个完整的 ASP.NET MVC 应用程序在本地 DB 数据库中存储数据。 可以创建、 读取、 更新、 删除和搜索电影。

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>后续步骤

生成并测试 web 应用程序后下, 一步是使其可供其他人通过 Internet 使用。 为此，必须将其部署到 web 宿主提供程序。 Microsoft 提供了免费的 web 托管最多 10 个网站中有关[免费 Windows Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)。 我建议你接下来请按照我的教程[包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 精彩教程是 Tom Dykstra 中级[为 ASP.NET MVC 应用程序创建实体框架数据模型](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 [Stackoverflow](http://stackoverflow.com/help)并[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是非常棒放置提出的问题。 请按照[我](https://twitter.com/RickAndMSFT)twitter 这样您就获得更新的我最新教程。

反馈是欢迎使用。

— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [上一篇](adding-validation-to-the-model.md)
