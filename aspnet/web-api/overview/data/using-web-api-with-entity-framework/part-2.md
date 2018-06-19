---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 添加模型和控制器 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 015bb9698d81387d03ea8f9629316fb53232e708
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879577"
---
<a name="add-models-and-controllers"></a><span data-ttu-id="0e81b-102">添加模型和控制器</span><span class="sxs-lookup"><span data-stu-id="0e81b-102">Add Models and Controllers</span></span>
====================
<span data-ttu-id="0e81b-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0e81b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0e81b-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="0e81b-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="0e81b-105">在本部分中，你将添加定义数据库实体的模型类。</span><span class="sxs-lookup"><span data-stu-id="0e81b-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="0e81b-106">然后你将添加执行对这些实体的 CRUD 操作的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="0e81b-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="0e81b-107">添加模型类</span><span class="sxs-lookup"><span data-stu-id="0e81b-107">Add Model Classes</span></span>

<span data-ttu-id="0e81b-108">在本教程中，我们将通过使用"代码优先"方法到 Entity Framework (EF) 创建数据库。</span><span class="sxs-lookup"><span data-stu-id="0e81b-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="0e81b-109">使用 Code First 数据库表中写入对应的 C# 类和 EF 创建数据库。</span><span class="sxs-lookup"><span data-stu-id="0e81b-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="0e81b-110">(有关详细信息，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)。)</span><span class="sxs-lookup"><span data-stu-id="0e81b-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="0e81b-111">我们首先我们域对象定义为 POCOs （纯旧式 CLR 对象）。</span><span class="sxs-lookup"><span data-stu-id="0e81b-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="0e81b-112">我们将创建以下 POCOs:</span><span class="sxs-lookup"><span data-stu-id="0e81b-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="0e81b-113">作者</span><span class="sxs-lookup"><span data-stu-id="0e81b-113">Author</span></span>
- <span data-ttu-id="0e81b-114">书籍</span><span class="sxs-lookup"><span data-stu-id="0e81b-114">Book</span></span>

<span data-ttu-id="0e81b-115">在解决方案资源管理器，右键单击模型文件夹。</span><span class="sxs-lookup"><span data-stu-id="0e81b-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="0e81b-116">选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="0e81b-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="0e81b-117">将此类命名为 `Author`。</span><span class="sxs-lookup"><span data-stu-id="0e81b-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="0e81b-118">将所有中 Author.cs 的样板文件代码替换下面的代码。</span><span class="sxs-lookup"><span data-stu-id="0e81b-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="0e81b-119">添加名为的另一个类`Book`，替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="0e81b-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="0e81b-120">实体框架将使用这些模型创建数据库表。</span><span class="sxs-lookup"><span data-stu-id="0e81b-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="0e81b-121">对于每个模型，`Id`属性将成为数据库表的主键列。</span><span class="sxs-lookup"><span data-stu-id="0e81b-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="0e81b-122">在簿类中，`AuthorId`定义外的键到`Author`表。</span><span class="sxs-lookup"><span data-stu-id="0e81b-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="0e81b-123">（为简单起见，我将假定每本书具有单个作者。）Book 类还包含指向相关的导航属性`Author`。</span><span class="sxs-lookup"><span data-stu-id="0e81b-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="0e81b-124">你可以使用导航属性访问相关`Author`在代码中。</span><span class="sxs-lookup"><span data-stu-id="0e81b-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="0e81b-125">我说第 4，部分中的导航属性有关的详细信息[处理实体关系](part-4.md)。</span><span class="sxs-lookup"><span data-stu-id="0e81b-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="0e81b-126">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="0e81b-126">Add Web API Controllers</span></span>

<span data-ttu-id="0e81b-127">在本部分中，我们将添加 Web API 控制器支持 CRUD 操作 （创建、 读取、 更新和删除）。</span><span class="sxs-lookup"><span data-stu-id="0e81b-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="0e81b-128">控制器将使用实体框架与数据库层进行通信。</span><span class="sxs-lookup"><span data-stu-id="0e81b-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="0e81b-129">首先，你可以删除文件 Controllers/ValuesController.cs。</span><span class="sxs-lookup"><span data-stu-id="0e81b-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="0e81b-130">此文件所包含的示例 Web API 控制器，但你不在本教程需要它。</span><span class="sxs-lookup"><span data-stu-id="0e81b-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="0e81b-131">接下来，生成项目。</span><span class="sxs-lookup"><span data-stu-id="0e81b-131">Next, build the project.</span></span> <span data-ttu-id="0e81b-132">Web API 基架使用反射来查找模型类，因此它需要编译的程序集。</span><span class="sxs-lookup"><span data-stu-id="0e81b-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="0e81b-133">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="0e81b-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="0e81b-134">选择**添加**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="0e81b-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="0e81b-135">在**添加基架**对话框中，选择"Web API 2 控制器其操作使用 Entity Framework"。</span><span class="sxs-lookup"><span data-stu-id="0e81b-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="0e81b-136">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="0e81b-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="0e81b-137">在**添加控制器**对话框中，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0e81b-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="0e81b-138">在**模型类**下拉列表中，选择`Author`类。</span><span class="sxs-lookup"><span data-stu-id="0e81b-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="0e81b-139">（如果你未看到它在下拉列表中列出，请确保生成项目。）</span><span class="sxs-lookup"><span data-stu-id="0e81b-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="0e81b-140">检查"使用异步控制器操作"。</span><span class="sxs-lookup"><span data-stu-id="0e81b-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="0e81b-141">将作为控制器名称&quot;AuthorsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="0e81b-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="0e81b-142">单击加号 （+） 按钮旁边**数据上下文类**。</span><span class="sxs-lookup"><span data-stu-id="0e81b-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="0e81b-143">在**新建数据上下文**对话框中，保留默认名称，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="0e81b-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="0e81b-144">单击**添加**完成**添加控制器**对话框。</span><span class="sxs-lookup"><span data-stu-id="0e81b-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="0e81b-145">该对话框将添加到你的项目的两个类：</span><span class="sxs-lookup"><span data-stu-id="0e81b-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="0e81b-146">`AuthorsController` 定义一个 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="0e81b-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="0e81b-147">控制器实现 REST API 客户端用来执行 CRUD 操作列表上的作者。</span><span class="sxs-lookup"><span data-stu-id="0e81b-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="0e81b-148">`BookServiceContext` 在运行期间，其中包括填充对象具有从数据库、 更改跟踪和将数据永久保存到数据库的数据管理实体对象。</span><span class="sxs-lookup"><span data-stu-id="0e81b-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="0e81b-149">它继承自`DbContext`。</span><span class="sxs-lookup"><span data-stu-id="0e81b-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="0e81b-150">此时，重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="0e81b-150">At this point, build the project again.</span></span> <span data-ttu-id="0e81b-151">现在，通过添加为一个 API 控制器的相同步骤转`Book`实体。</span><span class="sxs-lookup"><span data-stu-id="0e81b-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="0e81b-152">此时，选择`Book`模型类，然后选择现有`BookServiceContext`数据上下文类的类。</span><span class="sxs-lookup"><span data-stu-id="0e81b-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="0e81b-153">（不创建新的数据上下文）。单击**添加**将控制器添加。</span><span class="sxs-lookup"><span data-stu-id="0e81b-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="0e81b-154">[上一页](part-1.md)
> [下一页](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="0e81b-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
