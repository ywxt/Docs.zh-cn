---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 处理实体关系 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: 3c82724739b8ccb7c6b13788a5420af1e61c990b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="handling-entity-relations"></a><span data-ttu-id="5bb4c-102">处理实体关系</span><span class="sxs-lookup"><span data-stu-id="5bb4c-102">Handling Entity Relations</span></span>
====================
<span data-ttu-id="5bb4c-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5bb4c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5bb4c-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="5bb4c-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="5bb4c-105">本部分介绍如何 EF 加载相关的实体，以及如何处理模型类中的循环的导航属性的某些详细信息。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="5bb4c-106">（本部分提供背景知识，并不需要完成本教程。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="5bb4c-107">如果你愿意，请跳到[第 5 部分。](part-5.md)。)</span><span class="sxs-lookup"><span data-stu-id="5bb4c-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="5bb4c-108">预先加载与延迟加载</span><span class="sxs-lookup"><span data-stu-id="5bb4c-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="5bb4c-109">使用关系数据库支持 EF，时，一定要了解如何 EF 加载相关的数据。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="5bb4c-110">它也是有用若要查看 EF 生成的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="5bb4c-111">若要跟踪 SQL，添加以下代码的行`BookServiceContext`构造函数：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="5bb4c-112">如果将 GET 请求发送到 /api/books 中时，它将返回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="5bb4c-113">你可以看到 Author 属性为 null，，即使该指南包含有效的作者 Id 也是如此。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="5bb4c-114">这是因为 EF 不在加载相关的作者实体。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="5bb4c-115">SQL 查询的跟踪日志对此进行确认：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="5bb4c-116">SELECT 语句采用丛书表中并不引用作者表。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="5bb4c-117">作为参考，下面是中的方法`BooksController`返回的书籍列表的类。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="5bb4c-118">我们来看作为 JSON 数据的一部分，我们就可以返回作者。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="5bb4c-119">有三种方法来加载相关的实体框架中的数据： 预先加载、 延迟加载和显式加载。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="5bb4c-120">有权衡与每种技术，因此务必了解它们如何工作。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="5bb4c-121">预先加载</span><span class="sxs-lookup"><span data-stu-id="5bb4c-121">Eager Loading</span></span>

<span data-ttu-id="5bb4c-122">与*预先加载*，EF 加载相关的实体作为初始数据库查询的一部分。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="5bb4c-123">若要执行预先加载，使用**System.Data.Entity.Include**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="5bb4c-124">这将告知 EF 在查询中包含作者数据。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="5bb4c-125">如果你进行此更改，并运行应用，现在的 JSON 数据如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="5bb4c-126">跟踪日志显示 EF Book 和作者表执行联接。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="5bb4c-127">延迟加载</span><span class="sxs-lookup"><span data-stu-id="5bb4c-127">Lazy Loading</span></span>

<span data-ttu-id="5bb4c-128">使用延迟加载，EF 自动加载相关的实体时该实体的导航属性取消引用。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="5bb4c-129">若要启用延迟加载，请导航属性虚拟。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="5bb4c-130">例如，在 Book 类中：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="5bb4c-131">现在请考虑下面的代码：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="5bb4c-132">启用延迟加载后，访问`Author`属性`books[0]`导致 EF 作者查询数据库。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="5bb4c-133">延迟加载需要多个数据库访问，原因是 EF 发送查询每次它检索的相关的实体。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="5bb4c-134">一般而言，你希望在序列化的对象禁用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="5bb4c-135">序列化程序具有读取所有模型，随即将会触发加载相关的实体的属性。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="5bb4c-136">例如，以下是出现 EF 使用启用的延迟加载序列化的书籍列表的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="5bb4c-137">你可以看到 EF 的三个作者使三个单独的查询。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="5bb4c-138">仍有的时候你可能想要使用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="5bb4c-139">预先加载可能会导致 EF 生成非常复杂的联接。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="5bb4c-140">或可能的数据，一小部分需要相关的实体和延迟加载将更有效。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="5bb4c-141">若要避免序列化问题的一种方法是序列化而不是实体对象的数据传输对象 (Dto)。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="5bb4c-142">在本文的后面，我将介绍这种方法。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="5bb4c-143">显式加载</span><span class="sxs-lookup"><span data-stu-id="5bb4c-143">Explicit Loading</span></span>

<span data-ttu-id="5bb4c-144">显式加载具有类似于延迟加载的只不过您显式将相关的数据进入代码;它不会发生自动访问导航属性时。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="5bb4c-145">显式加载功能允许更好地控制何时加载相关的数据，但需要额外的代码。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="5bb4c-146">有关显式加载的详细信息，请参阅[加载相关实体](https://msdn.microsoft.com/data/jj574232#explicit)。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="5bb4c-147">导航属性并循环引用</span><span class="sxs-lookup"><span data-stu-id="5bb4c-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="5bb4c-148">当定义了 Book 和作者模型时，定义一个导航属性上`Book`类对于册作者关系，但我未在另一个方向定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="5bb4c-149">如果你添加到对应的导航属性，将会发生什么情况`Author`类？</span><span class="sxs-lookup"><span data-stu-id="5bb4c-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="5bb4c-150">遗憾的是，这将创建问题在序列化模型时。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="5bb4c-151">如果你加载相关的数据，它将创建循环对象图。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="5bb4c-152">当 JSON 或 XML 格式化程序尝试序列化关系图时，它将引发异常。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="5bb4c-153">两个格式化程序引发了不同的异常消息。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="5bb4c-154">下面是一个示例，用于 JSON 格式化程序：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="5bb4c-155">下面是 XML 格式化程序：</span><span class="sxs-lookup"><span data-stu-id="5bb4c-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="5bb4c-156">一种解决方案是使用 Dto，我介绍了下一节中。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="5bb4c-157">或者，你可以配置 JSON 和 XML 格式化程序来处理 graph 周期。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="5bb4c-158">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="5bb4c-159">对于本教程中，不需要使用`Author.Book`导航属性，因此您可以忽略它。</span><span class="sxs-lookup"><span data-stu-id="5bb4c-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5bb4c-160">[上一页](part-3.md)
> [下一页](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="5bb4c-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
