---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 第 2 部分： 创建域模型 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: cb98f42df411a7ba12ff4566c30ddfbf253253d4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834274"
---
<a name="part-2-creating-the-domain-models"></a><span data-ttu-id="96f85-102">第 2 部分： 创建域模型</span><span class="sxs-lookup"><span data-stu-id="96f85-102">Part 2: Creating the Domain Models</span></span>
====================
<span data-ttu-id="96f85-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="96f85-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="96f85-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="96f85-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="96f85-105">添加模型</span><span class="sxs-lookup"><span data-stu-id="96f85-105">Add Models</span></span>

<span data-ttu-id="96f85-106">有三种方式来实体框架的方法：</span><span class="sxs-lookup"><span data-stu-id="96f85-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="96f85-107">数据库优先： 对于数据库，启动和实体框架生成的代码。</span><span class="sxs-lookup"><span data-stu-id="96f85-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="96f85-108">实体数据模型： 开始从可视模型和实体框架生成的数据库和代码。</span><span class="sxs-lookup"><span data-stu-id="96f85-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="96f85-109">代码优先： 开头的代码中，并且实体框架生成数据库。</span><span class="sxs-lookup"><span data-stu-id="96f85-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="96f85-110">我们将使用代码优先方法中，因此我们首先定义我们的域对象为 Poco （普通旧 CLR 对象）。</span><span class="sxs-lookup"><span data-stu-id="96f85-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="96f85-111">使用代码优先方法时，域对象不需要任何额外的代码，以支持数据库层，例如事务或持久性。</span><span class="sxs-lookup"><span data-stu-id="96f85-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="96f85-112">(具体而言，它们不需要从继承[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)类。)仍然可以使用数据注释来控制如何 Entity Framework 创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="96f85-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="96f85-113">因为 Poco 不传送任何额外的属性描述[的数据库状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)，他们可以轻松地序列化为 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="96f85-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="96f85-114">但是，这不表示您应始终公开实体框架模型直接向客户端，正如我们将看到在本教程后面。</span><span class="sxs-lookup"><span data-stu-id="96f85-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="96f85-115">我们将创建以下 Poco:</span><span class="sxs-lookup"><span data-stu-id="96f85-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="96f85-116">产品</span><span class="sxs-lookup"><span data-stu-id="96f85-116">Product</span></span>
- <span data-ttu-id="96f85-117">顺序</span><span class="sxs-lookup"><span data-stu-id="96f85-117">Order</span></span>
- <span data-ttu-id="96f85-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="96f85-118">OrderDetail</span></span>

<span data-ttu-id="96f85-119">若要创建的每个类，请右键单击解决方案资源管理器中的 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="96f85-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="96f85-120">从上下文菜单中，选择**外**，然后选择**类。**</span><span class="sxs-lookup"><span data-stu-id="96f85-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="96f85-121">添加`Product`类具有以下实现：</span><span class="sxs-lookup"><span data-stu-id="96f85-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="96f85-122">按照约定，Entity Framework 使用`Id`为主键的属性并将其映射到数据库表中的标识列。</span><span class="sxs-lookup"><span data-stu-id="96f85-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="96f85-123">当您创建一个新`Product`实例中，不会设置一个值`Id`，因为该数据库生成值。</span><span class="sxs-lookup"><span data-stu-id="96f85-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="96f85-124">**ScaffoldColumn**特性告诉 ASP.NET MVC 跳过`Id`属性生成编辑器窗体时。</span><span class="sxs-lookup"><span data-stu-id="96f85-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="96f85-125">**所需**特性用于验证模型。</span><span class="sxs-lookup"><span data-stu-id="96f85-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="96f85-126">它指定`Name`属性必须为非空字符串。</span><span class="sxs-lookup"><span data-stu-id="96f85-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="96f85-127">添加`Order`类：</span><span class="sxs-lookup"><span data-stu-id="96f85-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="96f85-128">添加`OrderDetail`类：</span><span class="sxs-lookup"><span data-stu-id="96f85-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="96f85-129">外键关系</span><span class="sxs-lookup"><span data-stu-id="96f85-129">Foreign Key Relations</span></span>

<span data-ttu-id="96f85-130">订单包含多个订单详细信息，以及每个订单详细信息是指一个产品。</span><span class="sxs-lookup"><span data-stu-id="96f85-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="96f85-131">来表示这些关系`OrderDetail`类定义了名为的属性`OrderId`和`ProductId`。</span><span class="sxs-lookup"><span data-stu-id="96f85-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="96f85-132">实体框架将推断这些属性表示外键，并将向数据库添加 foreign key 约束。</span><span class="sxs-lookup"><span data-stu-id="96f85-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="96f85-133">`Order`和`OrderDetail`类还包括"导航"属性，其中包含对相关对象的引用。</span><span class="sxs-lookup"><span data-stu-id="96f85-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="96f85-134">给定订单，您可以导航到的产品的顺序由以下导航属性。</span><span class="sxs-lookup"><span data-stu-id="96f85-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="96f85-135">现在来编译项目。</span><span class="sxs-lookup"><span data-stu-id="96f85-135">Compile the project now.</span></span> <span data-ttu-id="96f85-136">实体框架使用反射来发现模型的属性，因此它需要一个已编译的程序集，以创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="96f85-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="96f85-137">配置媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="96f85-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="96f85-138">一个[媒体类型格式化程序](../../formats-and-model-binding/media-formatters.md)是当 Web API 将 HTTP 响应正文将你的数据序列化的对象。</span><span class="sxs-lookup"><span data-stu-id="96f85-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="96f85-139">内置格式化程序支持 JSON 和 XML 输出。</span><span class="sxs-lookup"><span data-stu-id="96f85-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="96f85-140">默认情况下，这两个这些格式化程序序列化的所有对象的值。</span><span class="sxs-lookup"><span data-stu-id="96f85-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="96f85-141">如果对象图包含循环引用，则按值序列化会产生问题。</span><span class="sxs-lookup"><span data-stu-id="96f85-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="96f85-142">这是完全与用例`Order`和`OrderDetail`类，因为每个保存到其他的引用。</span><span class="sxs-lookup"><span data-stu-id="96f85-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="96f85-143">格式化程序将按照值，通过编写每个对象引用，并在兜圈子转。</span><span class="sxs-lookup"><span data-stu-id="96f85-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="96f85-144">因此，我们需要更改默认行为。</span><span class="sxs-lookup"><span data-stu-id="96f85-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="96f85-145">在解决方案资源管理器，展开应用\_启动文件夹并打开名为 WebApiConfig.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="96f85-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="96f85-146">将下面的代码添加到 `WebApiConfig` 类中:</span><span class="sxs-lookup"><span data-stu-id="96f85-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="96f85-147">此代码设置 JSON 格式化程序来保留对象引用，并从管道中完全删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="96f85-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="96f85-148">（你可以配置要保留对象引用的 XML 格式化程序，但它是需要执行一些操作，和我们只需为此应用程序的 JSON。</span><span class="sxs-lookup"><span data-stu-id="96f85-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="96f85-149">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。)</span><span class="sxs-lookup"><span data-stu-id="96f85-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96f85-150">[上一页](using-web-api-with-entity-framework-part-1.md)
> [下一页](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="96f85-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
