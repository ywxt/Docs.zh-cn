---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: "创建数据访问层 |Microsoft 文档"
author: Erikre
description: "本系列教程将教您生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 809609155b06c4632bd4f450082d84c432c7a46f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="create-the-data-access-layer"></a><span data-ttu-id="987cb-103">创建数据访问层</span><span class="sxs-lookup"><span data-stu-id="987cb-103">Create the Data Access Layer</span></span>
====================
<span data-ttu-id="987cb-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="987cb-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="987cb-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="987cb-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="987cb-106">本系列教程将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="987cb-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="987cb-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)是可以附带本系列教程。</span><span class="sxs-lookup"><span data-stu-id="987cb-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="987cb-108">本教程介绍如何创建、 访问和查看使用 ASP.NET Web 窗体和 Entity Framework Code First 数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="987cb-109">本教程以前一教程"创建项目"上构建，并为 Wingtip 无实用价值应用商店教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="987cb-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="987cb-110">当你已完成本教程时，您便会生成的一组中的数据访问类*模型*项目文件夹中的。</span><span class="sxs-lookup"><span data-stu-id="987cb-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="987cb-111">你将学习：</span><span class="sxs-lookup"><span data-stu-id="987cb-111">What you'll learn:</span></span>

- <span data-ttu-id="987cb-112">如何创建数据模型。</span><span class="sxs-lookup"><span data-stu-id="987cb-112">How to create the data models.</span></span>
- <span data-ttu-id="987cb-113">如何初始化和植入到数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="987cb-114">如何更新和配置应用程序以支持的数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="987cb-115">以下是本教程中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="987cb-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="987cb-116">实体框架代码优先</span><span class="sxs-lookup"><span data-stu-id="987cb-116">Entity Framework Code First</span></span>
- <span data-ttu-id="987cb-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="987cb-117">LocalDB</span></span>
- <span data-ttu-id="987cb-118">数据注释</span><span class="sxs-lookup"><span data-stu-id="987cb-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="987cb-119">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="987cb-119">Creating the Data Models</span></span>

<span data-ttu-id="987cb-120">[实体框架](https://msdn.microsoft.com/data/aa937723)是一种对象关系映射 (ORM) 框架。</span><span class="sxs-lookup"><span data-stu-id="987cb-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="987cb-121">它允许你为对象，消除大部分数据访问代码，你通常需要编写处理关系数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="987cb-122">使用实体框架，你可以发出使用查询[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)，然后检索和处理数据作为强类型化的对象。</span><span class="sxs-lookup"><span data-stu-id="987cb-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="987cb-123">LINQ 提供了用于查询和更新数据的模式。</span><span class="sxs-lookup"><span data-stu-id="987cb-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="987cb-124">使用实体框架可以专注于创建你的应用程序的其余部分，而不是将重点放在数据访问基础知识。</span><span class="sxs-lookup"><span data-stu-id="987cb-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="987cb-125">稍后在本教程系列中，我们将演示如何使用数据来填充导航和产品的查询。</span><span class="sxs-lookup"><span data-stu-id="987cb-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="987cb-126">实体框架支持调用的开发范例*Code First*。</span><span class="sxs-lookup"><span data-stu-id="987cb-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="987cb-127">代码首先让你定义数据模型使用类。</span><span class="sxs-lookup"><span data-stu-id="987cb-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="987cb-128">类是一个构造，用于使您能够创建自己的自定义类型的其他类型、 方法和事件变量组合在一起。</span><span class="sxs-lookup"><span data-stu-id="987cb-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="987cb-129">你可以将类映射到现有数据库，或使用它们来生成数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="987cb-130">在本教程中，你将通过编写数据模型类来创建数据模型。</span><span class="sxs-lookup"><span data-stu-id="987cb-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="987cb-131">然后，你将让这些新类从动态创建数据库的实体框架。</span><span class="sxs-lookup"><span data-stu-id="987cb-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="987cb-132">你将首先创建定义 Web 窗体应用程序的数据模型的实体类。</span><span class="sxs-lookup"><span data-stu-id="987cb-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="987cb-133">然后你将创建一个上下文类，用于管理的实体类并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="987cb-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="987cb-134">你还将创建将用于在数据库中填充初始值设定项类。</span><span class="sxs-lookup"><span data-stu-id="987cb-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="987cb-135">实体框架和引用</span><span class="sxs-lookup"><span data-stu-id="987cb-135">Entity Framework and References</span></span>

<span data-ttu-id="987cb-136">默认情况下，实体框架时，将包括你创建一个新**ASP.NET Web 应用程序**使用**Web 窗体**模板。</span><span class="sxs-lookup"><span data-stu-id="987cb-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="987cb-137">实体框架可以安装、 卸载，并作为 NuGet 程序包更新。</span><span class="sxs-lookup"><span data-stu-id="987cb-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="987cb-138">此 NuGet 程序包包含以下**运行时**你的项目中的程序集：</span><span class="sxs-lookup"><span data-stu-id="987cb-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="987cb-139">EntityFramework.dll – 实体框架使用的所有公共运行时代码</span><span class="sxs-lookup"><span data-stu-id="987cb-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="987cb-140">EntityFramework.SqlServer.dll – 实体框架的 Microsoft SQL Server 提供程序</span><span class="sxs-lookup"><span data-stu-id="987cb-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="987cb-141">实体类</span><span class="sxs-lookup"><span data-stu-id="987cb-141">Entity Classes</span></span>

<span data-ttu-id="987cb-142">创建要定义的数据的架构的类称为实体类。</span><span class="sxs-lookup"><span data-stu-id="987cb-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="987cb-143">如果你不熟悉数据库设计，将实体类视为表定义的数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="987cb-144">在类中的每个属性指定的数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="987cb-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="987cb-145">这些类提供面向对象的代码和数据库的关系表结构之间的轻量、 对象关系接口。</span><span class="sxs-lookup"><span data-stu-id="987cb-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="987cb-146">在本教程中，您可以先通过添加简单实体类表示产品和类别的架构。</span><span class="sxs-lookup"><span data-stu-id="987cb-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="987cb-147">产品类将包含每个产品的定义。</span><span class="sxs-lookup"><span data-stu-id="987cb-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="987cb-148">每个产品类的成员的名称将`ProductID`， `ProductName`， `Description`， `ImagePath`， `UnitPrice`， `CategoryID`，和`Category`。</span><span class="sxs-lookup"><span data-stu-id="987cb-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="987cb-149">类别类将包含每个产品可以属于，如汽车、 条船或平面的类别的定义。</span><span class="sxs-lookup"><span data-stu-id="987cb-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="987cb-150">每个类别类的成员的名称将`CategoryID`， `CategoryName`， `Description`，和`Products`。</span><span class="sxs-lookup"><span data-stu-id="987cb-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="987cb-151">每个产品将属于一个类别。</span><span class="sxs-lookup"><span data-stu-id="987cb-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="987cb-152">这些实体类将添加到项目的现有*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="987cb-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="987cb-153">在**解决方案资源管理器**，右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="987cb-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![创建数据访问层-新项菜单](create_the_data_access_layer/_static/image1.png)

 <span data-ttu-id="987cb-155">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="987cb-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="987cb-156">下**Visual C#**从**已安装**左侧窗格中，选择**代码**。</span><span class="sxs-lookup"><span data-stu-id="987cb-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![创建数据访问层-新项菜单](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="987cb-158">选择**类**从中间窗格中并将此新类命名*Product.cs*。</span><span class="sxs-lookup"><span data-stu-id="987cb-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="987cb-159">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="987cb-159">Click **Add**.</span></span>  
 <span data-ttu-id="987cb-160">编辑器中将显示新的类文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="987cb-161">默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="987cb-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="987cb-162">通过重复步骤 1 至 4，但是，将新类来创建另一个类*Category.cs*和默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="987cb-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="987cb-163">如前所述，`Category`类的表示的一种应用程序的产品旨在销售 (如<a id="a"> </a>&quot;汽车&quot;，&quot;船&quot;， &quot;Rockets&quot;，依次类推)，和`Product`类表示数据库中的各个产品 (toys)。</span><span class="sxs-lookup"><span data-stu-id="987cb-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="987cb-164">每个实例`Product`对象将对应于关系数据库表中的行和产品类的每个属性将映射到关系数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="987cb-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="987cb-165">稍后在本教程中，你将查看包含在数据库中的产品数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="987cb-166">数据注释</span><span class="sxs-lookup"><span data-stu-id="987cb-166">Data Annotations</span></span>

<span data-ttu-id="987cb-167">你可能已经注意到某些类的成员具有属性指定该成员，有关详细信息，如`[ScaffoldColumn(false)]`。</span><span class="sxs-lookup"><span data-stu-id="987cb-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="987cb-168">这些是*数据注释*。</span><span class="sxs-lookup"><span data-stu-id="987cb-168">These are *data annotations*.</span></span> <span data-ttu-id="987cb-169">数据 annotation 特性可以描述如何验证该成员，以指定格式设置，并指定创建数据库时的建模方式的用户输入。</span><span class="sxs-lookup"><span data-stu-id="987cb-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="987cb-170">Context 类</span><span class="sxs-lookup"><span data-stu-id="987cb-170">Context Class</span></span>

<span data-ttu-id="987cb-171">若要开始使用这些类用于数据访问，必须定义的上下文类。</span><span class="sxs-lookup"><span data-stu-id="987cb-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="987cb-172">如前所述，上下文类所管理的实体类 (如`Product`类和`Category`类) 并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="987cb-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="987cb-173">此过程添加到的新 C# 上下文类*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="987cb-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="987cb-174">右键单击*模型*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="987cb-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
 <span data-ttu-id="987cb-175">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="987cb-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="987cb-176">选择**类**从中间窗格中，将其命名为*ProductContext.cs*单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="987cb-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="987cb-177">将替换为以下代码的类中包含的默认代码：</span><span class="sxs-lookup"><span data-stu-id="987cb-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="987cb-178">此代码将添加`System.Data.Entity`命名空间，以便有权访问的实体框架中，其中包括查询的功能，所有核心功能插入、 更新和删除通过使用强类型化对象数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="987cb-179">`ProductContext`类表示实体框架产品数据库上下文，用于处理提取、 存储和更新`Product`类数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="987cb-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="987cb-180">`ProductContext`类派生自`DbContext`由实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="987cb-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="987cb-181">初始值设定项类</span><span class="sxs-lookup"><span data-stu-id="987cb-181">Initializer Class</span></span>

<span data-ttu-id="987cb-182">你将需要运行某些自定义逻辑来初始化数据库第一个时间使用的上下文。</span><span class="sxs-lookup"><span data-stu-id="987cb-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="987cb-183">这将允许设定数据种子以添加到数据库，以使你可以立即显示产品和类别。</span><span class="sxs-lookup"><span data-stu-id="987cb-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="987cb-184">此过程添加到的新 C# 初始值设定项类*模型*文件夹。</span><span class="sxs-lookup"><span data-stu-id="987cb-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="987cb-185">创建另一个`Class`中*模型*文件夹并将其命名*ProductDatabaseInitializer.cs*。</span><span class="sxs-lookup"><span data-stu-id="987cb-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="987cb-186">将替换为以下代码的类中包含的默认代码：</span><span class="sxs-lookup"><span data-stu-id="987cb-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="987cb-187">因为时创建数据库并将其初始化，可以看到上述代码中，从`Seed`中被重写属性，将其设置。</span><span class="sxs-lookup"><span data-stu-id="987cb-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="987cb-188">当`Seed`属性设置，可使用的类别和产品中的值来填充数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="987cb-189">如果你尝试通过修改上面的代码中，创建数据库后更新种子数据，不会看到任何更新，当你运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="987cb-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="987cb-190">原因是上述代码中使用的实现`DropCreateDatabaseIfModelChanges`类，以识别在重置种子数据前是否已更改了模型 （架构）。</span><span class="sxs-lookup"><span data-stu-id="987cb-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="987cb-191">如果对不进行任何更改`Category`和`Product`实体类，数据库将不能重新初始化的种子数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="987cb-192">如果你想要重新创建每个时间的数据库运行应用程序，则可以使用`DropCreateDatabaseAlways`类而不是`DropCreateDatabaseIfModelChanges`类。</span><span class="sxs-lookup"><span data-stu-id="987cb-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="987cb-193">但是对于本教程系列中，使用`DropCreateDatabaseIfModelChanges`类。</span><span class="sxs-lookup"><span data-stu-id="987cb-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>


<span data-ttu-id="987cb-194">此时在本教程中，你将具有*模型*文件夹具有四个新类和一个默认类：</span><span class="sxs-lookup"><span data-stu-id="987cb-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![创建数据访问层中的 Models 文件夹](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="987cb-196">配置用于数据模型的应用程序</span><span class="sxs-lookup"><span data-stu-id="987cb-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="987cb-197">现在，你已创建表示数据的类，必须配置应用程序使用的类。</span><span class="sxs-lookup"><span data-stu-id="987cb-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="987cb-198">在*Global.asax*文件，你添加初始化模型的代码。</span><span class="sxs-lookup"><span data-stu-id="987cb-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="987cb-199">在*Web.config*文件添加信息，告诉应用程序内容数据库，您将使用它来存储由新的数据类表示的数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="987cb-200">*Global.asax*文件可以用于处理应用程序事件或方法。</span><span class="sxs-lookup"><span data-stu-id="987cb-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="987cb-201">*Web.config*文件可以控制 ASP.NET web 应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="987cb-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="987cb-202">正在更新的 Global.asax 文件</span><span class="sxs-lookup"><span data-stu-id="987cb-202">Updating the Global.asax file</span></span>

<span data-ttu-id="987cb-203">若要初始化的数据模型，应用程序启动时，你将更新`Application_Start`中的处理程序*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="987cb-204">在解决方案资源管理器，你可以选择*Global.asax*文件或*Global.asax.cs*文件以便进行编辑*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>


1. <span data-ttu-id="987cb-205">添加以下代码以到黄色突出显示`Application_Start`中的方法*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="987cb-206">你的浏览器必须支持 HTML5 以查看在浏览器中查看本系列教程时以黄色突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="987cb-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>


<span data-ttu-id="987cb-207">上述代码中中, 所示，应用程序启动时，应用程序指定访问数据过程中首次运行的初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="987cb-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="987cb-208">两个其他命名空间所需的访问`Database`对象和`ProductDatabaseInitializer`对象。</span><span class="sxs-lookup"><span data-stu-id="987cb-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="987cb-209">修改 Web.Config 文件</span><span class="sxs-lookup"><span data-stu-id="987cb-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="987cb-210">尽管 Entity Framework Code First 将生成数据库为你在默认位置在数据库填充了种子数据时，将你自己的连接信息添加到你的应用程序可以控制数据库位置。</span><span class="sxs-lookup"><span data-stu-id="987cb-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="987cb-211">指定此数据库连接时使用的连接字符串中应用程序的*Web.config*在项目的根目录的文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="987cb-212">你可以通过添加新的连接字符串，指示数据库的位置 (*wingtiptoys.mdf*) 若要在应用程序的数据目录中生成 (*应用\_数据*)，而不是其默认值位置。</span><span class="sxs-lookup"><span data-stu-id="987cb-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="987cb-213">进行此更改将允许你查找和在本教程后面检查数据库文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="987cb-214">在**解决方案资源管理器**，找到并打开*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="987cb-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="987cb-215">添加连接字符串以到黄色突出显示`<connectionStrings>`部分*Web.config*文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="987cb-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="987cb-216">当首次运行应用程序时，它将生成连接字符串指定的位置上的数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="987cb-217">但在运行之前应用程序，让我们来生成其第一次。</span><span class="sxs-lookup"><span data-stu-id="987cb-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="987cb-218">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="987cb-218">Building the Application</span></span>

<span data-ttu-id="987cb-219">若要确保所有的类和更改 Web 应用程序工作，应生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="987cb-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="987cb-220">从**调试**菜单上，选择**生成 WingtipToys**。</span><span class="sxs-lookup"><span data-stu-id="987cb-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="987cb-221">**输出**窗口会显示，并且所有进展良好，如果你看到*成功*消息。</span><span class="sxs-lookup"><span data-stu-id="987cb-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![创建数据访问层-输出窗口](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="987cb-223">如果在遇到错误，请重新检查上述步骤。</span><span class="sxs-lookup"><span data-stu-id="987cb-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="987cb-224">中的信息**输出**窗口将指示哪些文件遇到问题，在文件中更改要求的位置。</span><span class="sxs-lookup"><span data-stu-id="987cb-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="987cb-225">此信息将使您能够确定哪些属于上述步骤需要评审和在你的项目中修复。</span><span class="sxs-lookup"><span data-stu-id="987cb-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="987cb-226">摘要</span><span class="sxs-lookup"><span data-stu-id="987cb-226">Summary</span></span>

<span data-ttu-id="987cb-227">在本教程中的序列你已创建数据模型中，以及，添加将用于初始化和植入到数据库的代码。</span><span class="sxs-lookup"><span data-stu-id="987cb-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="987cb-228">你已配置应用程序以运行应用程序时使用的数据模型。</span><span class="sxs-lookup"><span data-stu-id="987cb-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="987cb-229">在下一步的教程中，将更新 UI、 添加导航窗格中，并从数据库中检索数据。</span><span class="sxs-lookup"><span data-stu-id="987cb-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="987cb-230">这将导致自动创建基于你在本教程中创建的实体类上的数据库。</span><span class="sxs-lookup"><span data-stu-id="987cb-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="987cb-231">其他资源</span><span class="sxs-lookup"><span data-stu-id="987cb-231">Additional Resources</span></span>

<span data-ttu-id="987cb-232">[实体框架概述](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="987cb-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="987cb-233">[ADO.NET 实体框架初学者指南](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="987cb-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="987cb-234">[代码使用实体框架的第一个开发](http://www.msteched.com/2010/Europe/DEV212)（视频）</span><span class="sxs-lookup"><span data-stu-id="987cb-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="987cb-235">[代码第一个关系 Fluent API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="987cb-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="987cb-236">Code First 数据批注</span><span class="sxs-lookup"><span data-stu-id="987cb-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="987cb-237">用于实体框架的工作效率改进</span><span class="sxs-lookup"><span data-stu-id="987cb-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

>[!div class="step-by-step"]
<span data-ttu-id="987cb-238">[上一页](create-the-project.md)
[下一页](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="987cb-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
