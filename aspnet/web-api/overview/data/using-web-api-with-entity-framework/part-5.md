---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 创建数据传输对象 (Dto) |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 6a066f1aca909afc2956e2026d9025cb87f10b1f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399920"
---
<a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="3aa73-102">创建数据传输对象 (Dto)</span><span class="sxs-lookup"><span data-stu-id="3aa73-102">Create Data Transfer Objects (DTOs)</span></span>
====================
<span data-ttu-id="3aa73-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3aa73-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3aa73-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="3aa73-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="3aa73-105">右我们的 web API 现在，公开给客户端的数据库实体。</span><span class="sxs-lookup"><span data-stu-id="3aa73-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="3aa73-106">客户端接收直接映射到数据库表的数据。</span><span class="sxs-lookup"><span data-stu-id="3aa73-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="3aa73-107">但是，，并不总是一个好主意。</span><span class="sxs-lookup"><span data-stu-id="3aa73-107">However, that's not always a good idea.</span></span> <span data-ttu-id="3aa73-108">有时你想要更改发送到客户端的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="3aa73-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="3aa73-109">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="3aa73-109">For example, you might want to:</span></span>

- <span data-ttu-id="3aa73-110">删除循环引用 （请参阅上一节）。</span><span class="sxs-lookup"><span data-stu-id="3aa73-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="3aa73-111">隐藏客户端不应查看的特定属性。</span><span class="sxs-lookup"><span data-stu-id="3aa73-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="3aa73-112">若要减小负载大小省略某些属性。</span><span class="sxs-lookup"><span data-stu-id="3aa73-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="3aa73-113">平展包含嵌套的对象，以使其更方便的客户端的对象图。</span><span class="sxs-lookup"><span data-stu-id="3aa73-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="3aa73-114">避免"过度发布"漏洞。</span><span class="sxs-lookup"><span data-stu-id="3aa73-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="3aa73-115">(请参阅[模型验证](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)有关过度发布的讨论。)</span><span class="sxs-lookup"><span data-stu-id="3aa73-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="3aa73-116">您从数据库层的服务层中分离出来。</span><span class="sxs-lookup"><span data-stu-id="3aa73-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="3aa73-117">若要实现此目的，可以定义*数据传输对象*(DTO)。</span><span class="sxs-lookup"><span data-stu-id="3aa73-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="3aa73-118">DTO 是定义将如何通过网络发送数据的对象。</span><span class="sxs-lookup"><span data-stu-id="3aa73-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="3aa73-119">我们来看，与通讯簿实体的工作方式。</span><span class="sxs-lookup"><span data-stu-id="3aa73-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="3aa73-120">在 Models 文件夹中，添加两个 DTO 类：</span><span class="sxs-lookup"><span data-stu-id="3aa73-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="3aa73-121">`BookDetailDTO`类包含的所有从通讯簿模型，不同之处在于属性`AuthorName`是一个字符串，将保存作者姓名。</span><span class="sxs-lookup"><span data-stu-id="3aa73-121">The `BookDetailDTO` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="3aa73-122">`BookDTO`类包含属性的子集`BookDetailDTO`。</span><span class="sxs-lookup"><span data-stu-id="3aa73-122">The `BookDTO` class contains a subset of properties from `BookDetailDTO`.</span></span>

<span data-ttu-id="3aa73-123">接下来，将在两个 GET 方法`BooksController`类，与返回 Dto 的版本。</span><span class="sxs-lookup"><span data-stu-id="3aa73-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="3aa73-124">我们将使用 LINQ**选择**语句将从本书实体转换为 Dto。</span><span class="sxs-lookup"><span data-stu-id="3aa73-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="3aa73-125">下面是生成新的 SQL`GetBooks`方法。</span><span class="sxs-lookup"><span data-stu-id="3aa73-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="3aa73-126">您可以看到 EF 转换 LINQ**选择**成 SQL SELECT 语句。</span><span class="sxs-lookup"><span data-stu-id="3aa73-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="3aa73-127">最后，修改`PostBook`方法以返回 DTO。</span><span class="sxs-lookup"><span data-stu-id="3aa73-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="3aa73-128">在本教程中，我们会转换为 Dto 手动在代码中。</span><span class="sxs-lookup"><span data-stu-id="3aa73-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="3aa73-129">另一种方法是使用一个库，如[AutoMapper](http://automapper.org/)用于自动处理转换。</span><span class="sxs-lookup"><span data-stu-id="3aa73-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="3aa73-130">[上一页](part-4.md)
> [下一页](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="3aa73-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
