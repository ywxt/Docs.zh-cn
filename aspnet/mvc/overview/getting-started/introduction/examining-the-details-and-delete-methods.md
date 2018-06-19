---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: 检查的详细信息和删除方法 |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: f534080fe9aa22eb9092932babc74c5ab96aabbf
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "33962423"
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="c1e18-102">检查的详细信息和删除方法</span><span class="sxs-lookup"><span data-stu-id="c1e18-102">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="c1e18-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="c1e18-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="c1e18-104">在本教程的此部分中，你将检查自动生成`Details`和`Delete`方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-104">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="c1e18-105">检查的详细信息和删除方法</span><span class="sxs-lookup"><span data-stu-id="c1e18-105">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="c1e18-106">打开`Movie`控制器并检查`Details`方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-106">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="c1e18-107">MVC 基架引擎，可用于创建此操作添加注释，显示调用方法的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c1e18-107">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="c1e18-108">在这种情况下它是`GET`请求包含三个 URL 段，`Movies`控制器，`Details`方法和一个`ID`值。</span><span class="sxs-lookup"><span data-stu-id="c1e18-108">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="c1e18-109">代码首先可以轻松地搜索数据使用`Find`方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-109">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="c1e18-110">生成到方法的一个重要的安全功能是代码验证`Find`代码尝试使用它执行任何操作之前，已找到一部电影方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-110">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="c1e18-111">例如，黑客无法将错误引入到站点通过更改由来自链接的 URL`http://localhost:xxxx/Movies/Details/1`为类似于`http://localhost:xxxx/Movies/Details/12345`（或不表示实际的电影的一些其他值）。</span><span class="sxs-lookup"><span data-stu-id="c1e18-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="c1e18-112">如果你没有检查 null 电影，null 电影将导致数据库错误。</span><span class="sxs-lookup"><span data-stu-id="c1e18-112">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="c1e18-113">检查 `Delete` 和 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="c1e18-114">请注意，HTTP GET`Delete`方法不会删除指定的电影，则返回其中可以提交电影的视图 (`HttpPost`) 删除。</span><span class="sxs-lookup"><span data-stu-id="c1e18-114">Note that the HTTP GET `Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion.</span></span> <span data-ttu-id="c1e18-115">执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="c1e18-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="c1e18-116">有关此的详细信息，请参阅博客条目，Stephen Walther [ASP.NET MVC 提示 #46-不要使用删除的链接，因为他们创建的安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c1e18-116">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="c1e18-117">删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。</span><span class="sxs-lookup"><span data-stu-id="c1e18-117">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="c1e18-118">下面显示了两个方法签名：</span><span class="sxs-lookup"><span data-stu-id="c1e18-118">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="c1e18-119">公共语言运行时 (CLR) 需要重载方法拥有唯一的参数签名（相同的方法名称但不同的参数列表）。</span><span class="sxs-lookup"><span data-stu-id="c1e18-119">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="c1e18-120">但是，此处你需要两个删除方法-一个 get-，一个用于 POST 都具有相同的参数签名。</span><span class="sxs-lookup"><span data-stu-id="c1e18-120">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="c1e18-121">（它们都需要接受单个整数作为参数。）</span><span class="sxs-lookup"><span data-stu-id="c1e18-121">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="c1e18-122">若要对此项进行排序，你可以执行几个事项。</span><span class="sxs-lookup"><span data-stu-id="c1e18-122">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="c1e18-123">之一是为方法提供不同的名称。</span><span class="sxs-lookup"><span data-stu-id="c1e18-123">One is to give the methods different names.</span></span> <span data-ttu-id="c1e18-124">这正是前面的示例中的基架机制进行的操作。</span><span class="sxs-lookup"><span data-stu-id="c1e18-124">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="c1e18-125">但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-125">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="c1e18-126">该示例中也提供了解决方案，即向 `DeleteConfirmed` 方法添加 `ActionName("Delete")` 属性。</span><span class="sxs-lookup"><span data-stu-id="c1e18-126">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="c1e18-127">这有效地执行映射路由的系统，以使 URL，包括 */Delete/* 的 post 请求将查找`DeleteConfirmed`方法。</span><span class="sxs-lookup"><span data-stu-id="c1e18-127">This effectively performs mapping for the routing system so that a URL that includes */Delete/* for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="c1e18-128">另一种常见的方法以避免问题具有相同的名称和签名的方法是人为地更改要包括未使用的参数的 POST 方法的签名。</span><span class="sxs-lookup"><span data-stu-id="c1e18-128">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="c1e18-129">例如，一些开发人员添加的参数类型`FormCollection`传递给 POST 方法中，然后只需不使用参数：</span><span class="sxs-lookup"><span data-stu-id="c1e18-129">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="c1e18-130">总结</span><span class="sxs-lookup"><span data-stu-id="c1e18-130">Summary</span></span>

<span data-ttu-id="c1e18-131">你现在具有一个完整的 ASP.NET MVC 应用程序在本地的 DB 数据库中存储数据。</span><span class="sxs-lookup"><span data-stu-id="c1e18-131">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="c1e18-132">你可以创建、 读取、 更新、 删除和搜索电影。</span><span class="sxs-lookup"><span data-stu-id="c1e18-132">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="c1e18-133">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c1e18-133">Next Steps</span></span>

<span data-ttu-id="c1e18-134">已生成和测试 web 应用程序后下, 一步是将其提供给其他人通过 Internet 使用。</span><span class="sxs-lookup"><span data-stu-id="c1e18-134">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="c1e18-135">若要做到这一点，你必须将其部署到 web 宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="c1e18-135">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="c1e18-136">Microsoft 提供了可用的 web 宿主中的最多 10 个网站[免费 Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="c1e18-136">Microsoft offers free web hosting for up to 10 web sites in a [free Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="c1e18-137">我建议你接下来请按照我的教程[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用程序部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="c1e18-137">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="c1e18-138">绝佳教程是 Tom Dykstra 的中间级[为 ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="c1e18-138">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="c1e18-139">[Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是出色放置询问的问题。</span><span class="sxs-lookup"><span data-stu-id="c1e18-139">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="c1e18-140">请按照[我](https://twitter.com/RickAndMSFT)以便您可以获取我的最新教程上的更新在 twitter 上。</span><span class="sxs-lookup"><span data-stu-id="c1e18-140">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="c1e18-141">反馈是受欢迎。</span><span class="sxs-lookup"><span data-stu-id="c1e18-141">Feedback is welcome.</span></span>

<span data-ttu-id="c1e18-142">- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c1e18-142">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="c1e18-143">- [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c1e18-143">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c1e18-144">上一篇</span><span class="sxs-lookup"><span data-stu-id="c1e18-144">Previous</span></span>](adding-validation.md)
