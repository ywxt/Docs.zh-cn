---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: "第 2 部分： 创建域模型 |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2012
ms.topic: article
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: a573b47d27767dc78d557cd2b6c73714eb9e94f4
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="part-2-creating-the-domain-models"></a><span data-ttu-id="f4193-102">第 2 部分： 创建域模型</span><span class="sxs-lookup"><span data-stu-id="f4193-102">Part 2: Creating the Domain Models</span></span>
====================
<span data-ttu-id="f4193-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f4193-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f4193-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="f4193-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="f4193-105">添加模型</span><span class="sxs-lookup"><span data-stu-id="f4193-105">Add Models</span></span>

<span data-ttu-id="f4193-106">有三种方法方法实体框架：</span><span class="sxs-lookup"><span data-stu-id="f4193-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="f4193-107">数据库优先： 对于数据库，启动和实体框架生成的代码。</span><span class="sxs-lookup"><span data-stu-id="f4193-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="f4193-108">模型优先： 开头 visual 模型和实体框架生成的数据库和代码。</span><span class="sxs-lookup"><span data-stu-id="f4193-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="f4193-109">代码优先： 与代码中，启动，实体框架生成数据库。</span><span class="sxs-lookup"><span data-stu-id="f4193-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="f4193-110">我们使用代码为先的方法，因此我们首先我们域对象定义为 POCOs （纯旧式 CLR 对象）。</span><span class="sxs-lookup"><span data-stu-id="f4193-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="f4193-111">使用代码优先方法时，域对象不需要任何额外的代码，以支持数据库层，如事务或持久性。</span><span class="sxs-lookup"><span data-stu-id="f4193-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="f4193-112">(具体而言，它们不需要从继承[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)类。)你仍然可以使用数据注释控制实体框架如何创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="f4193-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="f4193-113">因为 POCOs 不执行任何额外的属性，用于描述[的数据库状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)，它们可以轻松地序列化为 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="f4193-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="f4193-114">但是，，并不意味着你始终应公开实体框架模型直接向客户端，正如我们看到在教程的后面。</span><span class="sxs-lookup"><span data-stu-id="f4193-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="f4193-115">我们将创建以下 POCOs:</span><span class="sxs-lookup"><span data-stu-id="f4193-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="f4193-116">产品</span><span class="sxs-lookup"><span data-stu-id="f4193-116">Product</span></span>
- <span data-ttu-id="f4193-117">订单</span><span class="sxs-lookup"><span data-stu-id="f4193-117">Order</span></span>
- <span data-ttu-id="f4193-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="f4193-118">OrderDetail</span></span>

<span data-ttu-id="f4193-119">若要创建每个类，右键单击解决方案资源管理器中的 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="f4193-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="f4193-120">从上下文菜单中，选择**添加**，然后选择**类。**</span><span class="sxs-lookup"><span data-stu-id="f4193-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="f4193-121">添加`Product`类具有以下实现：</span><span class="sxs-lookup"><span data-stu-id="f4193-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="f4193-122">按照约定，实体框架使用`Id`为主键的属性并将其映射到数据库表中的标识列。</span><span class="sxs-lookup"><span data-stu-id="f4193-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="f4193-123">当你创建一个新`Product`实例，不会设置的值`Id`，因为数据库将生成值。</span><span class="sxs-lookup"><span data-stu-id="f4193-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="f4193-124">**ScaffoldColumn**属性告知 ASP.NET MVC 要跳过`Id`属性生成的编辑器窗体时。</span><span class="sxs-lookup"><span data-stu-id="f4193-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="f4193-125">**所需**属性用来验证模型。</span><span class="sxs-lookup"><span data-stu-id="f4193-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="f4193-126">它指定`Name`属性必须为非空字符串。</span><span class="sxs-lookup"><span data-stu-id="f4193-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="f4193-127">添加`Order`类：</span><span class="sxs-lookup"><span data-stu-id="f4193-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="f4193-128">添加`OrderDetail`类：</span><span class="sxs-lookup"><span data-stu-id="f4193-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="f4193-129">外键关系</span><span class="sxs-lookup"><span data-stu-id="f4193-129">Foreign Key Relations</span></span>

<span data-ttu-id="f4193-130">订单包含许多订单详细信息，并且每个订单详细信息指向单个产品。</span><span class="sxs-lookup"><span data-stu-id="f4193-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="f4193-131">来表示这些关系，`OrderDetail`类定义属性名为`OrderId`和`ProductId`。</span><span class="sxs-lookup"><span data-stu-id="f4193-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="f4193-132">实体框架将推断这些属性表示外键，并会将外键约束添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="f4193-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="f4193-133">`Order`和`OrderDetail`类还包括"导航"属性，其中包含对相关对象的引用。</span><span class="sxs-lookup"><span data-stu-id="f4193-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="f4193-134">给定订单，你可以通过导航到订单中产品以下导航属性。</span><span class="sxs-lookup"><span data-stu-id="f4193-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="f4193-135">现在编译该项目。</span><span class="sxs-lookup"><span data-stu-id="f4193-135">Compile the project now.</span></span> <span data-ttu-id="f4193-136">实体框架使用反射来发现的属性的模型，因此它需要编译的程序集，若要创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="f4193-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="f4193-137">配置的媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="f4193-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="f4193-138">A[媒体类型格式化程序](../../formats-and-model-binding/media-formatters.md)是当 Web API 写入 HTTP 响应正文将你的数据序列化的对象。</span><span class="sxs-lookup"><span data-stu-id="f4193-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="f4193-139">内置的格式化程序支持的 JSON 和 XML 输出。</span><span class="sxs-lookup"><span data-stu-id="f4193-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="f4193-140">默认情况下，这两个这些格式化程序序列化的所有对象的值。</span><span class="sxs-lookup"><span data-stu-id="f4193-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="f4193-141">如果对象图包含循环引用，则按值序列化会产生问题。</span><span class="sxs-lookup"><span data-stu-id="f4193-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="f4193-142">这是完全与用例`Order`和`OrderDetail`类，因为每个保存到其他的引用。</span><span class="sxs-lookup"><span data-stu-id="f4193-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="f4193-143">格式化程序将按照编写值，每个对象的引用，并在兜圈子转。</span><span class="sxs-lookup"><span data-stu-id="f4193-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="f4193-144">因此，我们需要更改默认行为。</span><span class="sxs-lookup"><span data-stu-id="f4193-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="f4193-145">在解决方案资源管理器，展开应用程序\_启动文件夹并打开名为 WebApiConfig.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="f4193-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="f4193-146">将下面的代码添加到 `WebApiConfig` 类中:</span><span class="sxs-lookup"><span data-stu-id="f4193-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="f4193-147">此代码会设置 JSON 格式化程序来保留对象引用，并从管道中完全移除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="f4193-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="f4193-148">（你可以配置 XML 格式化程序来保留对象引用，但该稍有更多工作，并且我们只需要为此应用程序的 JSON。</span><span class="sxs-lookup"><span data-stu-id="f4193-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="f4193-149">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。)</span><span class="sxs-lookup"><span data-stu-id="f4193-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f4193-150">[上一页](using-web-api-with-entity-framework-part-1.md)
[下一页](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="f4193-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
