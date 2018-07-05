---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 处理实体关系 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: 7759b828068d99f9975d56671e427ccf6e94aef6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400948"
---
<a name="handling-entity-relations"></a><span data-ttu-id="8db4a-102">处理实体关系</span><span class="sxs-lookup"><span data-stu-id="8db4a-102">Handling Entity Relations</span></span>
====================
<span data-ttu-id="8db4a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8db4a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="8db4a-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="8db4a-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="8db4a-105">本部分介绍 EF 加载相关的实体的方式以及如何处理循环的导航属性在模型类中的一些详细信息。</span><span class="sxs-lookup"><span data-stu-id="8db4a-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="8db4a-106">（本部分提供了背景知识，并不需要完成本教程。</span><span class="sxs-lookup"><span data-stu-id="8db4a-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="8db4a-107">如果您愿意，请跳到[第 5 部分。](part-5.md)。)</span><span class="sxs-lookup"><span data-stu-id="8db4a-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="8db4a-108">预先加载与延迟加载</span><span class="sxs-lookup"><span data-stu-id="8db4a-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="8db4a-109">当使用 EF 关系数据库时，务必了解 EF 加载相关的数据的方式。</span><span class="sxs-lookup"><span data-stu-id="8db4a-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="8db4a-110">也很有用，若要查看 EF 生成的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="8db4a-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="8db4a-111">若要跟踪 SQL，请添加以下代码行`BookServiceContext`构造函数：</span><span class="sxs-lookup"><span data-stu-id="8db4a-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="8db4a-112">如果向 /api/books 发送 GET 请求，它将返回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8db4a-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="8db4a-113">您可以看到 Author 属性是 null，即使该指南包含有效的作者 Id。</span><span class="sxs-lookup"><span data-stu-id="8db4a-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="8db4a-114">这是因为 EF 不加载相关的作者实体。</span><span class="sxs-lookup"><span data-stu-id="8db4a-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="8db4a-115">SQL 查询的跟踪日志对此进行确认：</span><span class="sxs-lookup"><span data-stu-id="8db4a-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="8db4a-116">SELECT 语句从书表中获取并不引用作者表。</span><span class="sxs-lookup"><span data-stu-id="8db4a-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="8db4a-117">有关参考，下面是在方法`BooksController`返回书籍列表的类。</span><span class="sxs-lookup"><span data-stu-id="8db4a-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="8db4a-118">我们来看作为 JSON 数据的一部分，我们就可以返回作者。</span><span class="sxs-lookup"><span data-stu-id="8db4a-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="8db4a-119">有三种方法来加载相关的实体框架中的数据： 预先加载、 延迟加载和显式加载。</span><span class="sxs-lookup"><span data-stu-id="8db4a-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="8db4a-120">有权衡与每种技术，因此务必要了解它们如何工作。</span><span class="sxs-lookup"><span data-stu-id="8db4a-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="8db4a-121">预先加载</span><span class="sxs-lookup"><span data-stu-id="8db4a-121">Eager Loading</span></span>

<span data-ttu-id="8db4a-122">与*预先加载*，EF 加载相关的实体作为初始数据库查询的一部分。</span><span class="sxs-lookup"><span data-stu-id="8db4a-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="8db4a-123">若要执行预先加载，请使用**System.Data.Entity.Include**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="8db4a-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="8db4a-124">这将告知 EF 在查询中包括创作数据。</span><span class="sxs-lookup"><span data-stu-id="8db4a-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="8db4a-125">如果你进行此更改，并运行应用，现在的 JSON 数据如下所示：</span><span class="sxs-lookup"><span data-stu-id="8db4a-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="8db4a-126">跟踪日志显示了 EF 的书籍和作者表执行联接。</span><span class="sxs-lookup"><span data-stu-id="8db4a-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="8db4a-127">延迟加载</span><span class="sxs-lookup"><span data-stu-id="8db4a-127">Lazy Loading</span></span>

<span data-ttu-id="8db4a-128">使用延迟加载，EF 会自动加载相关的实体时取消引用该实体的导航属性。</span><span class="sxs-lookup"><span data-stu-id="8db4a-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="8db4a-129">若要启用延迟加载，使导航属性虚拟方法。</span><span class="sxs-lookup"><span data-stu-id="8db4a-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="8db4a-130">例如，在 Book 类中：</span><span class="sxs-lookup"><span data-stu-id="8db4a-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="8db4a-131">现在请考虑以下代码：</span><span class="sxs-lookup"><span data-stu-id="8db4a-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="8db4a-132">启用延迟加载后，访问`Author`属性上的`books[0]`促使 EF 查询作者的数据库。</span><span class="sxs-lookup"><span data-stu-id="8db4a-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="8db4a-133">延迟加载需要多个数据库访问，原因是 EF 将发送每次它检索相关的实体的查询。</span><span class="sxs-lookup"><span data-stu-id="8db4a-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="8db4a-134">通常，您希望序列化的对象禁用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="8db4a-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="8db4a-135">序列化程序具有读取所有模型，这将触发加载相关的实体的属性。</span><span class="sxs-lookup"><span data-stu-id="8db4a-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="8db4a-136">例如，下面是出现 EF 将启用延迟加载序列化的书籍列表的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="8db4a-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="8db4a-137">您可以看到 EF 的三个作者可以三个单独的查询。</span><span class="sxs-lookup"><span data-stu-id="8db4a-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="8db4a-138">仍有可能的希望使用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="8db4a-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="8db4a-139">预先加载可能会导致 EF 生成非常复杂的联接。</span><span class="sxs-lookup"><span data-stu-id="8db4a-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="8db4a-140">或您可能需要相关的实体的少量数据，并延迟加载会更高效。</span><span class="sxs-lookup"><span data-stu-id="8db4a-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="8db4a-141">若要避免序列化问题的一种方法是序列化而不是实体对象的数据传输对象 (Dto)。</span><span class="sxs-lookup"><span data-stu-id="8db4a-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="8db4a-142">在本文的后面，我将介绍这种方法。</span><span class="sxs-lookup"><span data-stu-id="8db4a-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="8db4a-143">显式加载</span><span class="sxs-lookup"><span data-stu-id="8db4a-143">Explicit Loading</span></span>

<span data-ttu-id="8db4a-144">显式加载是类似于延迟加载，只是显式代码; 中有相关的数据它不会自动发生时您访问导航属性。</span><span class="sxs-lookup"><span data-stu-id="8db4a-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="8db4a-145">显式加载可提供更好地控制何时加载相关的数据，但需要额外的代码。</span><span class="sxs-lookup"><span data-stu-id="8db4a-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="8db4a-146">有关显式加载的详细信息，请参阅[加载相关实体](https://msdn.microsoft.com/data/jj574232#explicit)。</span><span class="sxs-lookup"><span data-stu-id="8db4a-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="8db4a-147">导航属性和循环引用</span><span class="sxs-lookup"><span data-stu-id="8db4a-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="8db4a-148">当我定义的书籍和作者模型时，我定义一个导航属性上`Book`类书籍作者关系，但我没有在另一个方向定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="8db4a-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="8db4a-149">如果您将添加到相应的导航属性，会发生什么情况`Author`类？</span><span class="sxs-lookup"><span data-stu-id="8db4a-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="8db4a-150">遗憾的是，这会产生问题时序列化模型。</span><span class="sxs-lookup"><span data-stu-id="8db4a-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="8db4a-151">如果在加载相关的数据，它将创建循环对象图。</span><span class="sxs-lookup"><span data-stu-id="8db4a-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="8db4a-152">当 JSON 或 XML 格式化程序尝试序列化关系图时，它将引发异常。</span><span class="sxs-lookup"><span data-stu-id="8db4a-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="8db4a-153">两个格式化程序会引发其他异常消息。</span><span class="sxs-lookup"><span data-stu-id="8db4a-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="8db4a-154">下面是 JSON 格式化程序的示例：</span><span class="sxs-lookup"><span data-stu-id="8db4a-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="8db4a-155">下面是 XML 格式化程序：</span><span class="sxs-lookup"><span data-stu-id="8db4a-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="8db4a-156">一种解决方案是使用 Dto，我在下一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="8db4a-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="8db4a-157">或者，可以配置 JSON 和 XML 格式化程序用于处理关系图周期。</span><span class="sxs-lookup"><span data-stu-id="8db4a-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="8db4a-158">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。</span><span class="sxs-lookup"><span data-stu-id="8db4a-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="8db4a-159">对于本教程中，不需要`Author.Book`导航属性，因此可以省略。</span><span class="sxs-lookup"><span data-stu-id="8db4a-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8db4a-160">[上一页](part-3.md)
> [下一页](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="8db4a-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
