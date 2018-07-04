---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证功能构建模型 |Microsoft Docs
author: microsoft
description: 步骤 3 显示了如何创建一个模型，我们可以使用这两个查询，并为 NerdDinner 应用程序更新数据库。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 8e871a8c14dce80edbddb9d87dba929bf3356895
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379016"
---
<a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="5f6b5-103">使用业务规则验证功能构建模型</span><span class="sxs-lookup"><span data-stu-id="5f6b5-103">Build a Model with Business Rule Validations</span></span>
====================
<span data-ttu-id="5f6b5-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5f6b5-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5f6b5-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="5f6b5-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5f6b5-106">这是一种免费的步骤 3 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5f6b5-107">步骤 3 显示了如何创建一个模型，我们可以使用这两个查询，并为 NerdDinner 应用程序更新数据库。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="5f6b5-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="5f6b5-109">NerdDinner 步骤 3： 生成模型</span><span class="sxs-lookup"><span data-stu-id="5f6b5-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="5f6b5-110">在一个模型-视图-控制器框架术语"模型"是指表示数据的应用程序，以及与之集成验证规则和业务规则的相应域逻辑的对象。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="5f6b5-111">模型在很多方面"核心"的基于 MVC 的应用程序，并且正如我们将看到更高版本从根本上驱动器的行为。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="5f6b5-112">ASP.NET MVC 框架支持使用任何数据访问技术和开发人员可以选择使用不同的丰富的.NET 数据选项，来实现其模型，包括： LINQ to 实体、 LINQ to SQL、 NHibernate、 LLBLGen Pro，SubSonic、 WilsonORM 或只是原始的 ADO。NET Datareader 或数据集。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="5f6b5-113">NerdDinner 应用程序，我们将使用 LINQ to SQL 创建简单的模型的方法相当接近于我们的数据库设计，并将一些自定义验证逻辑和业务规则。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="5f6b5-114">我们然后将实现存储库类，可帮助立即抽象应用程序，并允许我们轻松单元测试的其余部分的数据持久性实现。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="5f6b5-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="5f6b5-115">LINQ to SQL</span></span>

<span data-ttu-id="5f6b5-116">LINQ to SQL 是作为.NET 3.5 的一部分提供的 ORM （对象关系映射程序）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="5f6b5-117">LINQ to SQL 提供轻松地将数据库表映射到我们可以编写代码的.NET 类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="5f6b5-118">NerdDinner 应用程序我们将使用它来将 Dinners 和 RSVP 表映射到 Dinner 和 RSVP 类我们数据库中。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="5f6b5-119">Dinners 和 RSVP 表的列将相对应的 Dinner 和 RSVP 类上的属性。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="5f6b5-120">每个 Dinner 和 RSVP 对象将表示数据库中的 Dinners 或 RSVP 表内一个单独的行。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="5f6b5-121">LINQ to SQL 允许我们可以避免不得不手动构造 SQL 语句以检索和更新 Dinner 的 RSVP 数据库数据的对象。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="5f6b5-122">相反，我们将定义的 Dinner 和 RSVP 的类，它们映射到如何存储或从数据库和它们之间的关系。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="5f6b5-123">然后，LINQ to SQL 将将负责生成用于进行交互并使用它们时，在运行时使用的相应 SQL 执行逻辑。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="5f6b5-124">我们可以使用 VB 和 C# 中的 LINQ 语言支持编写检索 Dinner 和 RSVP 的表达查询数据库中的对象。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="5f6b5-125">这将减少我们需要编写，数据代码量，并让我们来构建真正清理应用程序。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="5f6b5-126">将 LINQ to SQL 类添加到我们的项目</span><span class="sxs-lookup"><span data-stu-id="5f6b5-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="5f6b5-127">我们将首先右键单击"Models"文件夹中我们的项目，并选择**Add-&gt;新项**菜单命令：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="5f6b5-128">这将显示"添加新项"对话框。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="5f6b5-129">我们将按"数据"类别筛选，并选择在其中的"LINQ to SQL Classes"模板：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="5f6b5-130">我们将命名项"NerdDinner"，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="5f6b5-131">Visual Studio 将添加我们 \Models 的目录下的 NerdDinner.dbml 文件并打开 LINQ to SQL 对象关系设计器：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="5f6b5-132">使用 LINQ to SQL 创建数据模型类</span><span class="sxs-lookup"><span data-stu-id="5f6b5-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="5f6b5-133">LINQ to SQL，我们能够快速从现有数据库架构创建数据模型类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="5f6b5-134">待办事项我们想要在其中建模的此我们将在服务器资源管理器中打开 NerdDinner 数据库并选择的表：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="5f6b5-135">然后，我们可以将表拖到 LINQ 到 SQL 设计器图面。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="5f6b5-136">当我们进行此 LINQ to SQL 将自动创建 Dinner 的 RSVP 类使用 （包括类将映射到数据库表列的属性） 的表的架构：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="5f6b5-137">默认情况下，LINQ to SQL 设计器自动"为"表名和列名时它将创建基于数据库架构的类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="5f6b5-138">例如： 在上述示例中的"Dinners"表会导致"Dinner"类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="5f6b5-139">此类命名可帮助使我们的模型与.NET 命名约定保持一致，我经常发现该具有设计器修复这向上方便 （尤其是在添加许多表）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="5f6b5-140">如果您不喜欢类或该设计器生成，但你始终可以重写它并将其更改为所需的任何名称的属性的名称。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="5f6b5-141">您可以执行此操作通过编辑实体/属性名称串联在设计器中或通过修改通过属性网格。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="5f6b5-142">默认情况下，LINQ to SQL 设计器还会检查表的主键/外键关系和自动基于它们创建默认"关系关联的的之间的不同模型类，它将创建。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="5f6b5-143">例如，当我们拖动 Dinners 和 RSVP 表到 LINQ to SQL 设计器上两者之间的一个对多关系关联推断基于的事实，RSVP 表具有外键，到 Dinners 表 (这会由中的箭头指示设计器）：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="5f6b5-144">上面的关联会导致 LINQ to SQL 将强类型化"Dinner"属性添加到开发人员可用于访问与给定的 RSVP Dinner 的 RSVP 类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="5f6b5-145">它将导致 Dinner 类具有一个"RSVPs"集合属性，使开发人员能够检索和更新关联与特定 Dinner 的 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="5f6b5-146">下面介绍 Visual Studio 中的 intellisense 的示例，当我们创建一个新的 RSVP 对象并将其添加到 Dinner 的 Rsvp 集合时。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="5f6b5-147">请注意如何 LINQ to SQL 会自动添加"Rsvp"集合上的 Dinner 对象：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="5f6b5-148">通过将 RSVP 对象添加到 Dinner 的 Rsvp 集合，我们将指示 LINQ to SQL 将 Dinner 和我们的数据库中的 RSVP 行之间的外键关系相关联：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="5f6b5-149">如果您不喜欢如何在设计器已建模或名为表关联，可以重写它。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="5f6b5-150">只需单击设计器中的关联箭头，然后访问其属性通过属性网格，若要重命名、 删除或修改它。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="5f6b5-151">我们 NerdDinner 的应用程序，不过，默认关联规则适用于我们正在创建数据模型类和我们可以直接使用的默认行为。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="5f6b5-152">NerdDinnerDataContext 类</span><span class="sxs-lookup"><span data-stu-id="5f6b5-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="5f6b5-153">Visual Studio 将自动创建表示模型和使用 LINQ to SQL 设计器定义的数据库关系的.NET 类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="5f6b5-154">LINQ to SQL DataContext 类还会为每个 LINQ to SQL 设计器文件添加到解决方案中生成。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="5f6b5-155">因为我们命名为我们 LINQ to SQL 类项"NerdDinner"，创建的 DataContext 类将名为"NerdDinnerDataContext"。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="5f6b5-156">此 NerdDinnerDataContext 类是我们将与数据库交互的主要方法。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="5f6b5-157">我们 NerdDinnerDataContext 类公开两个属性-"Dinners"和"RSVPs"-表示我们在数据库中建模的两个表。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="5f6b5-158">我们可以使用 C# 来编写 LINQ 查询对这些属性对查询和检索 Dinner 和 RSVP 对象从数据库。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="5f6b5-159">下面的代码演示如何实例化 NerdDinnerDataContext 对象并执行针对它以获取 Dinners 将来发生的一系列的 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="5f6b5-160">编写 LINQ 查询时，visual Studio 提供了完整的 intellisense 和从其返回的对象都是强类型，而且还支持 intellisense:</span><span class="sxs-lookup"><span data-stu-id="5f6b5-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="5f6b5-161">除了允许我们 Dinner 和 RSVP 对象查询，NerdDinnerDataContext 还会自动跟踪我们随后对我们通过它检索的 Dinner 和 RSVP 对象进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="5f6b5-162">我们可以使用此功能来轻松地将所做的更改保存回数据库-而无需编写任何显式的 SQL 更新代码。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="5f6b5-163">例如，下面的代码演示如何使用 LINQ 查询以从数据库中检索单个 Dinner 对象更新两个 Dinner 属性，然后将所做的更改保存回数据库：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="5f6b5-164">在上面的代码的 NerdDinnerDataContext 对象自动跟踪对我们从它检索的 Dinner 对象的属性更改。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="5f6b5-165">当我们调用"SubmitChanges()"方法时，它将执行到要保存更新后的值返回的数据库的相应 SQL"更新"语句。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="5f6b5-166">创建 DinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="5f6b5-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="5f6b5-167">对于小型应用程序是有时可以将具有控制器直接对 LINQ to SQL DataContext 类工作，并将嵌入控制器中的 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="5f6b5-168">随着应用程序变得更长，不过，这种方法变得难以维护和测试。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="5f6b5-169">它可能还会导致我们复制多个位置中的相同 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="5f6b5-170">可以使应用程序更易于维护和测试的一种方法是使用"存储库"模式。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="5f6b5-171">存储库类可帮助封装数据查询和持久性逻辑和提取了从应用程序的数据持久性的实现细节。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="5f6b5-172">除了使应用程序代码更简洁，使用存储库模式可以轻松地在将来，更改数据存储实现，它可以帮助简化单元测试的应用程序而无需实际数据库。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="5f6b5-173">NerdDinner 应用程序中，我们将定义 DinnerRepository 类具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="5f6b5-174">*注意： 更高版本在本章我们将从此类提取 IDinnerRepository 接口，使我们控制器上使用它的依赖关系注入。开始时，不过，我们将简单的开始和只需直接使用 DinnerRepository 类。*</span><span class="sxs-lookup"><span data-stu-id="5f6b5-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="5f6b5-175">若要实现此类，我们将在我们"Models"文件夹上右键单击并选择**Add-&gt;新项**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="5f6b5-176">在"添加新项"对话框中，我们将选择"类"模板，并将文件命名"DinnerRepository.cs":</span><span class="sxs-lookup"><span data-stu-id="5f6b5-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="5f6b5-177">然后，我们可以实现我们使用下面的代码的 DinnerRespository 类：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-177">We can then implement our DinnerRespository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="5f6b5-178">检索、 更新、 插入和删除使用 DinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="5f6b5-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="5f6b5-179">现在，我们已创建我们的 DinnerRepository 类，让我们看一些代码示例演示我们可以用它完成常见任务：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="5f6b5-180">查询示例</span><span class="sxs-lookup"><span data-stu-id="5f6b5-180">Querying Examples</span></span>

<span data-ttu-id="5f6b5-181">下面的代码检索单个 Dinner 使用 DinnerID 值：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="5f6b5-182">下面的代码会通过其检索所有即将推出 dinners 和循环：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="5f6b5-183">插入和更新示例</span><span class="sxs-lookup"><span data-stu-id="5f6b5-183">Insert and Update Examples</span></span>

<span data-ttu-id="5f6b5-184">下面的代码演示如何添加两个新 dinners。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="5f6b5-185">在其上调用"save （）"方法之前，对存储库中添加/修改不会提交到数据库。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="5f6b5-186">LINQ to SQL 会自动将所有更改都包装在数据库事务 – 因此发生了所有更改或其中任何一个执行时我们的存储库将保存：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="5f6b5-187">下面的代码检索现有 Dinner 对象，并修改它的两个属性。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="5f6b5-188">在我们的存储库上调用"save （）"方法时，在提交回数据库更改：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="5f6b5-189">下面的代码检索 dinner，然后向其添加 RSVP。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="5f6b5-190">这样做 （因为在数据库中两者之间没有主键键/外键关系），为我们创建 LINQ to SQL 的 Dinner 对象上使用 Rsvp 集合。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="5f6b5-191">在存储库上调用"save （）"方法时，此更改为新的 RSVP 表行保存回数据库中：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="5f6b5-192">删除示例</span><span class="sxs-lookup"><span data-stu-id="5f6b5-192">Delete Example</span></span>

<span data-ttu-id="5f6b5-193">下面的代码检索现有 Dinner 对象，并随后会被删除标记。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="5f6b5-194">在存储库上调用"save （）"方法时它将删除提交回数据库：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="5f6b5-195">将与模型类集成验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="5f6b5-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="5f6b5-196">集成验证和业务规则逻辑是适用于数据的任何应用程序的关键部分。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="5f6b5-197">架构验证</span><span class="sxs-lookup"><span data-stu-id="5f6b5-197">Schema Validation</span></span>

<span data-ttu-id="5f6b5-198">模型类定义时使用 LINQ to SQL 设计器，在数据模型类中属性的数据类型对应于数据库表的数据类型。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="5f6b5-199">例如： 如果 Dinners 表中的"EventDate"列"datetime"，创建 linq to SQL 的数据模型类将类型为"DateTime"（这是内置的.NET 数据类型）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="5f6b5-200">这意味着如果你尝试从代码中，为其分配一个整数或布尔值，并且如果尝试将隐式非有效的字符串类型转换为它在运行时，它将自动引发错误，则会收到编译错误。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="5f6b5-201">使用的字符串-它有助于保护您免受 SQL 注入攻击时使用它时，LINQ to SQL 还会自动将为你处理转义 SQL 值。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="5f6b5-202">验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="5f6b5-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="5f6b5-203">架构验证作为第一个步骤，非常有用，但很少足够。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="5f6b5-204">大多数实际情况下，需要指定更丰富的验证逻辑可以跨越多个属性、 执行代码，且通常有意识的模型的状态的功能 (例如： 它正在创建/更新/删除，或在某一特定于域的状态例如"已存档"）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="5f6b5-205">有各种不同的模式和框架，可用于定义并将验证规则应用于模型的类，并有几个基于.NET 框架有可用于帮助实现此目的。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="5f6b5-206">可以使用几乎任何这些 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="5f6b5-207">对于我们 NerdDinner 的应用程序的目的，我们将使用相对简单，简单的模式，我们会在我们 Dinner 的模型对象上公开 IsValid 属性和 GetRuleViolations() 方法。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="5f6b5-208">IsValid 属性将返回 true 或 false 具体取决于是否所有有效的验证和业务规则。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="5f6b5-209">GetRuleViolations() 方法将返回一组规则的任何错误。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="5f6b5-210">我们将实现 IsValid 和 GetRuleViolations() Dinner 模型通过将"分部类"添加到我们的项目。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="5f6b5-211">分部类可用于将方法/属性/事件添加到维护的 VS 设计器 （如 linq to SQL 设计器生成的 Dinner 类） 的类和帮助避免产生混淆，我们的代码中的工具。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="5f6b5-212">我们可以右键单击 \Models 文件夹中，将新的分部类添加到我们的项目，然后选择"添加新项"菜单命令。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="5f6b5-213">我们然后可以选择在"添加新项"对话框的"类"模板并将其命名 Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="5f6b5-214">单击"添加"按钮将 Dinner.cs 文件添加到我们的项目，并在 IDE 中打开它。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="5f6b5-215">我们然后可以实现基本的规则验证强制框架，它使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="5f6b5-216">有关上述代码中的几个注意事项：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-216">A few notes about the above code:</span></span>

- <span data-ttu-id="5f6b5-217">Dinner 类开头，但使用 partial 关键字 – 这意味着它所包含的代码将是与生成/维护的类结合使用 linq to SQL 设计器，编译到单个类。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="5f6b5-218">RuleViolation 类是一个帮助器类，我们将添加到项目，可用于提供有关规则冲突的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="5f6b5-219">Dinner.GetRuleViolations() 方法使我们验证规则和业务规则进行评估 （我们将马上要实现它们）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="5f6b5-220">然后返回一系列 RuleViolation 对象，它提供有关规则的任何错误的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="5f6b5-221">Dinner.IsValid 属性提供了一个便利的帮助器属性，指示 Dinner 对象是否具有任何活动 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="5f6b5-222">它可以主动检查由开发人员在任何时候使用 Dinner 对象 （并不会引发异常）。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="5f6b5-223">Dinner.OnValidate() 分部方法是 LINQ to SQL 提供，可用于 Dinner 对象由要保留在数据库中的任何时间收到通知的挂钩。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="5f6b5-224">上述我们 OnValidate() 实现可确保 Dinner 有没有 RuleViolations，之后再将其保存。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="5f6b5-225">如果处于无效状态，它会引发异常，这将导致 LINQ to SQL 中止事务。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="5f6b5-226">这种方法提供了一个简单的框架，我们可以将验证和到业务规则集成。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="5f6b5-227">现在让我们添加到我们的 GetRuleViolations() 方法的规则如下：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="5f6b5-228">我们将使用 C#"yield return"的功能可返回任何 RuleViolations 的序列。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="5f6b5-229">上面的第六个规则检查只是强制执行我们 Dinner 的字符串属性不能为 null 或为空。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="5f6b5-230">最后一条规则是一些更有趣，并调用 PhoneValidator.IsValidNumber() 帮助器方法，我们可以将添加到我们的项目以验证 contactphone 编号格式匹配 Dinner 国家/地区。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="5f6b5-231">我们可以使用。NET 的正则表达式支持，以实现此电话验证支持。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="5f6b5-232">下面是一个简单的 PhoneValidator 实现，我们可以添加到项目，使我们可以添加特定于国家/地区的正则表达式模式检查：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="5f6b5-233">处理验证和业务逻辑冲突</span><span class="sxs-lookup"><span data-stu-id="5f6b5-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="5f6b5-234">现在，我们已添加上述验证和业务规则代码中，我们尝试创建或更新 Dinner 任何时候，我们验证逻辑规则将进行评估和强制执行。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="5f6b5-235">开发人员可以编写的代码类似下面主动确定 Dinner 对象是否有效，并检索在其中的所有冲突，并且不会引发任何异常的列表：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="5f6b5-236">如果我们尝试在无效状态中保存 Dinner，当我们在 DinnerRepository 上调用 save （） 方法时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="5f6b5-237">这是因为 LINQ to SQL 会自动调用我们 Dinner.OnValidate() 分部方法之前它将保存 Dinner 的更改，我们将代码添加到 Dinner.OnValidate() 引发异常，如果在 Dinner 中存在任何规则冲突。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="5f6b5-238">我们可以捕获此异常和被动检索冲突后，若要修复的列表：</span><span class="sxs-lookup"><span data-stu-id="5f6b5-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="5f6b5-239">因为在我们的模型层，而不是在 UI 层，并实现我们验证和业务规则，它们将应用和我们的应用程序中的所有方案中都使用。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="5f6b5-240">我们稍后可以更改或添加业务规则，具有适用于我们的 Dinner 对象遵循它们的所有代码。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="5f6b5-241">可以灵活地更改业务规则在一个位置，而无需波及整个应用程序和 UI 逻辑，这些更改就编写良好的应用程序和的 MVC 框架可帮助支持权益的登录。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="5f6b5-242">下一步</span><span class="sxs-lookup"><span data-stu-id="5f6b5-242">Next Step</span></span>

<span data-ttu-id="5f6b5-243">我们现在有一个模型，我们可以使用查询和更新我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="5f6b5-244">现在让我们添加一些控制器和视图的项目的我们可用于构建在其周围的 HTML UI 体验。</span><span class="sxs-lookup"><span data-stu-id="5f6b5-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5f6b5-245">[上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="5f6b5-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
