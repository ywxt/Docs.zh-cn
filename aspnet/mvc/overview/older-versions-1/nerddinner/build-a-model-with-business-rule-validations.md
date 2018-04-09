---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 生成一个具有业务规则验证模型 |Microsoft 文档
author: microsoft
description: 第 3 步演示如何创建模型，我们可以使用这两个查询，并且我们 NerdDinner 为应用程序更新数据库。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: c5a482474fd2f41836f70952306ada5cd9136455
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="07386-103">生成一个具有业务规则验证模型</span><span class="sxs-lookup"><span data-stu-id="07386-103">Build a Model with Business Rule Validations</span></span>
====================
<span data-ttu-id="07386-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="07386-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="07386-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="07386-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="07386-106">这是一个免费的第 3 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07386-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="07386-107">第 3 步演示如何创建模型，我们可以使用这两个查询，并且我们 NerdDinner 为应用程序更新数据库。</span><span class="sxs-lookup"><span data-stu-id="07386-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="07386-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="07386-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="07386-109">NerdDinner 步骤 3： 构建模型</span><span class="sxs-lookup"><span data-stu-id="07386-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="07386-110">模型-视图-控制器框架中的术语"模型"是指表示应用程序，以及与之集成验证和业务规则的相应域逻辑数据的对象。</span><span class="sxs-lookup"><span data-stu-id="07386-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="07386-111">模型在基于 MVC 的应用程序的许多方面"核心"是和正如我们看到更高版本从根本上驱动器的行为。</span><span class="sxs-lookup"><span data-stu-id="07386-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="07386-112">ASP.NET MVC framework 支持使用任何数据访问技术，开发人员可以选择使用不同的丰富的.NET 数据选项，来实现其模型，包括： LINQ to 实体、 LINQ to SQL、 NHibernate、 LLBLGen Pro、 SubSonic、 WilsonORM 或只是原始 ADO。NET DataReaders 或数据集。</span><span class="sxs-lookup"><span data-stu-id="07386-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="07386-113">我们 NerdDinner 为应用程序，我们将以使用 LINQ to SQL 来创建一个简单的模型的方法相当接近于我们的数据库设计，并将一些自定义验证逻辑和业务规则添加。</span><span class="sxs-lookup"><span data-stu-id="07386-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="07386-114">我们然后将实现存储库类，可帮助消失抽象应用程序，并启用我们到轻松单元测试的其余部分的数据持久性实现。</span><span class="sxs-lookup"><span data-stu-id="07386-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="07386-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="07386-115">LINQ to SQL</span></span>

<span data-ttu-id="07386-116">LINQ to SQL 是作为.NET 3.5 的一部分附带的 ORM （对象关系映射器）。</span><span class="sxs-lookup"><span data-stu-id="07386-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="07386-117">LINQ to SQL 提供将数据库表映射到我们可以编写代码，针对的.NET 类的简单办法。</span><span class="sxs-lookup"><span data-stu-id="07386-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="07386-118">我们 NerdDinner 为应用程序我们将使用它来将晚餐和回复表映射到 Dinner 和回复类我们数据库中。</span><span class="sxs-lookup"><span data-stu-id="07386-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="07386-119">晚餐和回复表的列将对应于 Dinner 和回复类上的属性。</span><span class="sxs-lookup"><span data-stu-id="07386-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="07386-120">每个 Dinner 和回复对象将表示数据库中的晚餐或的回复表中的单独行。</span><span class="sxs-lookup"><span data-stu-id="07386-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="07386-121">LINQ to SQL 允许我们避免不得不手动构造 SQL 语句以便检索和更新 Dinner 以及回复处理数据库数据的对象。</span><span class="sxs-lookup"><span data-stu-id="07386-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="07386-122">相反，我们将定义 Dinner 和回复类中，如何它们映射到/从该数据库，以及它们之间的关系。</span><span class="sxs-lookup"><span data-stu-id="07386-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="07386-123">然后，LINQ to SQL 将采用负责生成相应的 SQL 执行逻辑，当我们进行交互，并使用它们时，在运行时使用。</span><span class="sxs-lookup"><span data-stu-id="07386-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="07386-124">我们可以使用 VB 和 C# 中的 LINQ 语言支持可以编写可表达查询来检索 Dinner 和回复从数据库对象。</span><span class="sxs-lookup"><span data-stu-id="07386-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="07386-125">这将减少量数据我们编写的代码，并允许我们构建真正干净的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07386-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="07386-126">将 LINQ to SQL 类添加到我们的项目</span><span class="sxs-lookup"><span data-stu-id="07386-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="07386-127">我们将开始通过我们的项目中的"模型"文件夹中右键单击并选择**添加-&gt;新项**菜单命令：</span><span class="sxs-lookup"><span data-stu-id="07386-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="07386-128">这将显示"添加新项"对话框。</span><span class="sxs-lookup"><span data-stu-id="07386-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="07386-129">我们将按"数据"类别筛选，并选择在其中的"LINQ 到 SQL 类"模板：</span><span class="sxs-lookup"><span data-stu-id="07386-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="07386-130">我们将命名的项"NerdDinner"，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="07386-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="07386-131">Visual Studio 将添加一个 NerdDinner.dbml 文件我们 \Models 目录下的，然后打开 LINQ to SQL 对象关系设计器：</span><span class="sxs-lookup"><span data-stu-id="07386-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="07386-132">使用 LINQ to SQL 创建数据模型类</span><span class="sxs-lookup"><span data-stu-id="07386-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="07386-133">LINQ to SQL，我们可以快速从现有数据库架构创建数据模型类。</span><span class="sxs-lookup"><span data-stu-id="07386-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="07386-134">待办事项我们想要在其中进行建模的此处我们将在服务器资源管理器中打开 NerdDinner 数据库并选择的表：</span><span class="sxs-lookup"><span data-stu-id="07386-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="07386-135">然后，我们可以将表拖到 LINQ 到 SQL 设计器图面。</span><span class="sxs-lookup"><span data-stu-id="07386-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="07386-136">此 LINQ to SQL 执行时将自动创建 Dinner 和使用 （包括映射到数据库表中各列的类属性） 表的架构的回复类：</span><span class="sxs-lookup"><span data-stu-id="07386-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="07386-137">默认情况下，LINQ to SQL 设计器自动"以复数形式表示"表名和列名时它创建基于数据库架构的类。</span><span class="sxs-lookup"><span data-stu-id="07386-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="07386-138">例如： 在上述示例中的"晚餐"表导致"Dinner"类。</span><span class="sxs-lookup"><span data-stu-id="07386-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="07386-139">此类命名可帮助使我们的模型与.NET 命名约定保持一致和通常找到该设计器修复这向上方便 （尤其是时遇到添加大量表）。</span><span class="sxs-lookup"><span data-stu-id="07386-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="07386-140">如果你不喜欢的类或设计器生成，但始终可以重写此方法，并将其更改为所需的任何名称的属性的名称。</span><span class="sxs-lookup"><span data-stu-id="07386-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="07386-141">你可以执行此操作通过编辑实体/属性名称中，线设计器中或通过修改通过属性网格。</span><span class="sxs-lookup"><span data-stu-id="07386-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="07386-142">默认情况下，LINQ to SQL 设计器还检查表，主键/外的键关系，并自动基于它们创建默认"关系关联"的它将创建不同的模型类之间。</span><span class="sxs-lookup"><span data-stu-id="07386-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="07386-143">例如，当我们拖动晚餐和回复表到 LINQ to SQL 设计器两者之间的一对多关系关联已推断出基于这一事实的回复表具有外键，到晚餐表 (这由中的箭头指示设计器）：</span><span class="sxs-lookup"><span data-stu-id="07386-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="07386-144">上面的关联将导致 LINQ to SQL 将强类型化"Dinner"属性添加到开发人员可以使用访问 Dinner 与给定的回复关联的回复类。</span><span class="sxs-lookup"><span data-stu-id="07386-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="07386-145">它将导致 Dinner 该类具有一个"RSVPs"集合属性，使开发人员能够检索和更新与特定 Dinner 关联的回复对象。</span><span class="sxs-lookup"><span data-stu-id="07386-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="07386-146">下面可以看到举例说明了 Visual Studio 中的 intellisense，当我们创建一个新的回复对象并将其添加到 Dinner RSVPs 集合。</span><span class="sxs-lookup"><span data-stu-id="07386-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="07386-147">请注意如何 LINQ to SQL 会自动添加"RSVPs"集合上的 Dinner 对象：</span><span class="sxs-lookup"><span data-stu-id="07386-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="07386-148">将回复对象添加到 Dinner RSVPs 集合我们相当于告诉 LINQ to SQL 将 Dinner 和我们的数据库中的回复行之间的外键关系相关联：</span><span class="sxs-lookup"><span data-stu-id="07386-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="07386-149">如果你不喜欢如何在设计器具有建模或名为表关联，则可以重写它。</span><span class="sxs-lookup"><span data-stu-id="07386-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="07386-150">只需单击设计器中的关联箭头，然后访问通过属性网格重命名、 删除或对其进行修改其属性。</span><span class="sxs-lookup"><span data-stu-id="07386-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="07386-151">我们 NerdDinner 的应用程序，不过，默认关联规则适用于我们要生成的数据模型类和我们只需使用的默认行为。</span><span class="sxs-lookup"><span data-stu-id="07386-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="07386-152">NerdDinnerDataContext 类</span><span class="sxs-lookup"><span data-stu-id="07386-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="07386-153">Visual Studio 将自动创建表示的模型和使用 LINQ to SQL 设计器定义的数据库关系的.NET 类。</span><span class="sxs-lookup"><span data-stu-id="07386-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="07386-154">LINQ to SQL DataContext 类还会为每个 LINQ to SQL 设计器文件添加到解决方案中生成。</span><span class="sxs-lookup"><span data-stu-id="07386-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="07386-155">由于我们命名我们 LINQ to SQL 类项"NerdDinner"，创建的 DataContext 类将调用"NerdDinnerDataContext"。</span><span class="sxs-lookup"><span data-stu-id="07386-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="07386-156">此 NerdDinnerDataContext 类是我们将与数据库交互的主要方法。</span><span class="sxs-lookup"><span data-stu-id="07386-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="07386-157">我们 NerdDinnerDataContext 该类会公开两个属性-"晚餐"和"RSVPs"-表示我们建模数据库中的两个表。</span><span class="sxs-lookup"><span data-stu-id="07386-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="07386-158">我们可以使用 C# 来编写针对这些属性的 LINQ 查询的查询和检索 Dinner 和回复对象从数据库。</span><span class="sxs-lookup"><span data-stu-id="07386-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="07386-159">下面的代码演示如何实例化 NerdDinnerDataContext 对象和执行 LINQ 查询来获取晚餐将来发生的序列。</span><span class="sxs-lookup"><span data-stu-id="07386-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="07386-160">Visual Studio 提供了完整的 intellisense，当编写 LINQ 查询，并从它返回的对象都是强类型，而且还支持 intellisense:</span><span class="sxs-lookup"><span data-stu-id="07386-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="07386-161">除了使我们能够 Dinner 和回复对象查询，NerdDinnerDataContext 还自动跟踪我们随后对我们通过它检索的 Dinner 和回复对象进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="07386-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="07386-162">我们可以使用此功能来轻松地将所做的更改保存回数据库-无需编写任何显式的 SQL 更新代码。</span><span class="sxs-lookup"><span data-stu-id="07386-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="07386-163">例如，下面的代码演示如何使用 LINQ 查询以从数据库中检索单个 Dinner 对象更新两个 Dinner 属性，然后将所做的更改保存回数据库：</span><span class="sxs-lookup"><span data-stu-id="07386-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="07386-164">在上面的代码的 NerdDinnerDataContext 对象自动跟踪对我们从它检索的 Dinner 对象的属性更改。</span><span class="sxs-lookup"><span data-stu-id="07386-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="07386-165">当我们调用"SubmitChanges()"方法时，它将执行到要保存更新后的值返回的数据库的相应 SQL"更新"语句。</span><span class="sxs-lookup"><span data-stu-id="07386-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="07386-166">创建 DinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="07386-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="07386-167">对于小型应用程序是有时可以将具有控制器直接针对 LINQ to SQL DataContext 类，并将嵌入在控制器中的 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="07386-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="07386-168">随着应用程序变得更长，不过，这种方法变得难以维护和测试。</span><span class="sxs-lookup"><span data-stu-id="07386-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="07386-169">此外可能导致我们复制多个位置中的同一个 LINQ 查询导致。</span><span class="sxs-lookup"><span data-stu-id="07386-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="07386-170">可以使应用程序更易于维护和测试的一种方法是使用"存储库"模式。</span><span class="sxs-lookup"><span data-stu-id="07386-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="07386-171">存储库类可帮助将数据查询和持久性逻辑和摘要消失封装从应用程序的数据持久性的实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="07386-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="07386-172">除了让应用程序代码更简洁，使用的存储库模式会导致更轻松地在将来，更改数据存储实现，并且它可以帮助实现单元测试应用程序，而无需实际的数据库。</span><span class="sxs-lookup"><span data-stu-id="07386-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="07386-173">对于我们 NerdDinner 的应用程序中，我们将定义具有的 DinnerRepository 类以下签名：</span><span class="sxs-lookup"><span data-stu-id="07386-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="07386-174">*注意： 本章后面我们从此类提取 IDinnerRepository 接口，启用与之我们控制器上的依赖关系注入。开始时，不过，我们将启动简单和直接与 DinnerRepository 类正常工作。*</span><span class="sxs-lookup"><span data-stu-id="07386-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="07386-175">若要实现此类，我们将在我们"Models"文件夹上右键单击并选择**添加-&gt;新项**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="07386-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="07386-176">在"添加新项"对话框中，我们将选择"类"模板，并将文件命名为"DinnerRepository.cs":</span><span class="sxs-lookup"><span data-stu-id="07386-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="07386-177">然后，我们可以实现下面的代码使用我们 DinnerRespository 类：</span><span class="sxs-lookup"><span data-stu-id="07386-177">We can then implement our DinnerRespository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="07386-178">检索、 更新、 插入和删除使用 DinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="07386-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="07386-179">现在，我们已创建我们 DinnerRepository 类，让我们看一些演示我们可以使用它执行操作的常见任务的代码示例：</span><span class="sxs-lookup"><span data-stu-id="07386-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="07386-180">查询示例</span><span class="sxs-lookup"><span data-stu-id="07386-180">Querying Examples</span></span>

<span data-ttu-id="07386-181">下面的代码检索单个 Dinner 使用 DinnerID 值：</span><span class="sxs-lookup"><span data-stu-id="07386-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="07386-182">下面的代码检索在其所有即将发布晚餐和循环：</span><span class="sxs-lookup"><span data-stu-id="07386-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="07386-183">插入和更新示例</span><span class="sxs-lookup"><span data-stu-id="07386-183">Insert and Update Examples</span></span>

<span data-ttu-id="07386-184">下面的代码演示如何添加两个新晚餐。</span><span class="sxs-lookup"><span data-stu-id="07386-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="07386-185">添加/修改存储库不提交到数据库，直到对它调用了"save （）"方法。</span><span class="sxs-lookup"><span data-stu-id="07386-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="07386-186">LINQ to SQL 会自动将所有更改都包装在一项数据库事务 – 因此发生了所有更改或其中任何一个执行我们的存储库保存时：</span><span class="sxs-lookup"><span data-stu-id="07386-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="07386-187">下面的代码检索现有 Dinner 对象，并修改它的两个属性。</span><span class="sxs-lookup"><span data-stu-id="07386-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="07386-188">在我们的存储库上调用"save （）"方法时，在提交回数据库更改：</span><span class="sxs-lookup"><span data-stu-id="07386-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="07386-189">下面的代码检索 dinner，，然后向其添加回复。</span><span class="sxs-lookup"><span data-stu-id="07386-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="07386-190">不过这将为我们创建 LINQ to SQL （因为在数据库中这两者之间没有主键/外键关系） 的 Dinner 对象上使用 RSVPs 集合。</span><span class="sxs-lookup"><span data-stu-id="07386-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="07386-191">存储库上调用"save （）"方法时，此更改为新的回复表行保存回数据库中：</span><span class="sxs-lookup"><span data-stu-id="07386-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="07386-192">删除示例</span><span class="sxs-lookup"><span data-stu-id="07386-192">Delete Example</span></span>

<span data-ttu-id="07386-193">下面的代码检索现有 Dinner 对象，然后将其标记为要删除。</span><span class="sxs-lookup"><span data-stu-id="07386-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="07386-194">存储库上调用"save （）"方法时它将提交回数据库的删除：</span><span class="sxs-lookup"><span data-stu-id="07386-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="07386-195">将与模型类集成验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="07386-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="07386-196">集成验证和业务规则逻辑是任何可使用应用程序数据的重要组成部分。</span><span class="sxs-lookup"><span data-stu-id="07386-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="07386-197">架构验证</span><span class="sxs-lookup"><span data-stu-id="07386-197">Schema Validation</span></span>

<span data-ttu-id="07386-198">如果使用 LINQ to SQL 设计器定义模型类中的数据模型类的属性的数据类型对应于数据库表的数据类型。</span><span class="sxs-lookup"><span data-stu-id="07386-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="07386-199">例如： 如果晚餐表中的"EventDate"列是"datetime"，创建 LINQ to SQL 的数据模型类将是类型"DateTime"（这是内置的.NET 数据类型）。</span><span class="sxs-lookup"><span data-stu-id="07386-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="07386-200">这意味着如果你尝试从代码中，为其指定的整数或布尔值，并且如果你尝试隐式将非有效的字符串类型转换为它在运行时，它将自动引发错误，则将收到编译错误。</span><span class="sxs-lookup"><span data-stu-id="07386-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="07386-201">使用的字符串-这有助于帮助你抵御 SQL 注入式攻击时使用它时，LINQ to SQL 还会自动将为你处理转义 SQL 值。</span><span class="sxs-lookup"><span data-stu-id="07386-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="07386-202">验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="07386-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="07386-203">架构验证是作为第一个步骤中，有用，但很少足够。</span><span class="sxs-lookup"><span data-stu-id="07386-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="07386-204">大多数实际情况下，需要指定更丰富的验证逻辑，可以跨多个属性、 执行代码，并且通常具有感知的模型的状态的功能 (例如： 它正在创建/更新/删除，或在某一特定于域的状态如"存档"）。</span><span class="sxs-lookup"><span data-stu-id="07386-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="07386-205">有各种不同的模式和可用来定义和将验证规则应用于模型类的框架和几个基于.NET 框架现成可用来帮助实现这一点。</span><span class="sxs-lookup"><span data-stu-id="07386-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="07386-206">你可以使用 ASP.NET MVC 应用程序中的其中几乎任何。</span><span class="sxs-lookup"><span data-stu-id="07386-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="07386-207">对于我们 NerdDinner 的应用程序的目的，我们将使用一种相对简单和直接模式其中我们会在我们 Dinner 模型对象上公开 IsValid 属性和 GetRuleViolations() 方法。</span><span class="sxs-lookup"><span data-stu-id="07386-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="07386-208">IsValid 属性将返回 true 或 false，具体取决于是否验证和业务规则均有效。</span><span class="sxs-lookup"><span data-stu-id="07386-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="07386-209">GetRuleViolations() 方法将返回任何规则错误的列表。</span><span class="sxs-lookup"><span data-stu-id="07386-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="07386-210">我们将实现 IsValid 和 GetRuleViolations() 为我们 Dinner 模型通过向我们的项目中添加"分部类"。</span><span class="sxs-lookup"><span data-stu-id="07386-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="07386-211">分部类可以用来将方法/属性/事件添加到类 （如 linq to SQL 设计器生成的 Dinner 类） 的 VS 设计器由维护，并且有助于避免混乱与我们的代码中的工具。</span><span class="sxs-lookup"><span data-stu-id="07386-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="07386-212">我们可以右键单击 \Models 文件夹中，将新的分部类添加到我们的项目，然后选择"添加新项"菜单命令。</span><span class="sxs-lookup"><span data-stu-id="07386-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="07386-213">然后，我们可以选择在"添加新项"对话框的"类"模板，并将其命名 Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="07386-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="07386-214">单击"添加"按钮将将 Dinner.cs 文件添加到我们的项目，并在 IDE 中打开它。</span><span class="sxs-lookup"><span data-stu-id="07386-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="07386-215">我们然后实现基本的规则验证强制 framework 使用下面的代码：</span><span class="sxs-lookup"><span data-stu-id="07386-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="07386-216">有关上面的代码的几个注意事项：</span><span class="sxs-lookup"><span data-stu-id="07386-216">A few notes about the above code:</span></span>

- <span data-ttu-id="07386-217">Dinner 类开头为"partial"关键字 – 这意味着将与生成/维护类结合使用 linq to SQL 设计器中包含的代码，并将其编译成一个类。</span><span class="sxs-lookup"><span data-stu-id="07386-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="07386-218">RuleViolation 类是我们将添加到项目，我们提供有关某一规则冲突的更多详细信息的帮助程序类。</span><span class="sxs-lookup"><span data-stu-id="07386-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="07386-219">Dinner.GetRuleViolations() 方法使我们验证规则和业务规则要进行求值 （我们将实现它们很快）。</span><span class="sxs-lookup"><span data-stu-id="07386-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="07386-220">它然后返回 RuleViolation 对象，它提供有关任何规则错误的更多详细信息的序列。</span><span class="sxs-lookup"><span data-stu-id="07386-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="07386-221">Dinner.IsValid 属性提供了一个便利的帮助器属性，指示 Dinner 对象是否具有任何活动 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="07386-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="07386-222">它可以在任何时候使用 Dinner 对象的开发人员通过主动检查 （并不会引发异常）。</span><span class="sxs-lookup"><span data-stu-id="07386-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="07386-223">Dinner.OnValidate() 分部方法是提供 LINQ to SQL 允许我们 Dinner 对象将保留在数据库中的任何时候要通知的挂钩。</span><span class="sxs-lookup"><span data-stu-id="07386-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="07386-224">上述我们 OnValidate() 实现可确保 Dinner 具有任何 RuleViolations，则在保存前。</span><span class="sxs-lookup"><span data-stu-id="07386-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="07386-225">如果它处于无效状态，因此它会引发异常，这将导致 LINQ to SQL 中止事务。</span><span class="sxs-lookup"><span data-stu-id="07386-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="07386-226">此方法提供一个简单的框架，我们可以将验证和业务规则到集成。</span><span class="sxs-lookup"><span data-stu-id="07386-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="07386-227">现在让我们添加以下规则到我们 GetRuleViolations() 方法：</span><span class="sxs-lookup"><span data-stu-id="07386-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="07386-228">我们将使用 C# 的"产量返回"的功能来返回任何 RuleViolations 的序列。</span><span class="sxs-lookup"><span data-stu-id="07386-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="07386-229">上面的第一个六个规则检查只是强制执行我们 Dinner 的字符串属性不能为 null 或为空。</span><span class="sxs-lookup"><span data-stu-id="07386-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="07386-230">最后一条规则很变得更加有趣，而且调用 PhoneValidator.IsValidNumber() 帮助器方法，我们可以将添加到我们的项目，以便确认 ContactPhone 数字格式匹配 Dinner 国家/地区。</span><span class="sxs-lookup"><span data-stu-id="07386-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="07386-231">我们可以使用。若要实现此电话验证支持的 NET 的正则表达式支持。</span><span class="sxs-lookup"><span data-stu-id="07386-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="07386-232">下面是一个简单的 PhoneValidator 实现，我们可以添加到我们使我们能够添加特定于国家/地区的正则表达式模式检查的项目：</span><span class="sxs-lookup"><span data-stu-id="07386-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="07386-233">处理验证和业务逻辑冲突</span><span class="sxs-lookup"><span data-stu-id="07386-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="07386-234">现在，我们已添加上述验证和业务规则代码中，我们尝试创建或更新 Dinner 任何时间，将评估和强制执行我们的验证逻辑规则。</span><span class="sxs-lookup"><span data-stu-id="07386-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="07386-235">开发人员可以编写代码类似下面主动确定 Dinner 对象是否有效，并检索中它的所有冲突，而不会引发任何异常的列表：</span><span class="sxs-lookup"><span data-stu-id="07386-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="07386-236">如果我们尝试保存 Dinner 处于无效状态，当我们调用 DinnerRepository save （） 方法时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="07386-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="07386-237">这是因为它将保存 Dinner 的更改，然后我们将代码添加到 Dinner.OnValidate() 以引发异常时如果 Dinner 中不存在任何规则冲突后，LINQ to SQL 将自动调用我们 Dinner.OnValidate() 分部方法。</span><span class="sxs-lookup"><span data-stu-id="07386-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="07386-238">我们可以捕获此异常，并可以被动检索冲突后，若要解决问题的列表：</span><span class="sxs-lookup"><span data-stu-id="07386-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="07386-239">因为我们验证规则和业务规则并实现在我们的模型层，以及不中的 UI 层，它们将应用并在我们的应用程序内的所有方案中都使用。</span><span class="sxs-lookup"><span data-stu-id="07386-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="07386-240">我们可以稍后更改或添加业务规则并具有适用于我们 Dinner 对象遵循它们的所有代码。</span><span class="sxs-lookup"><span data-stu-id="07386-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="07386-241">具有灵活地更改业务规则在一个位置，而无 ripple 在整个应用程序和用户界面逻辑，这些更改是正确编写的应用程序，和的 MVC 框架可帮助鼓励权益的符号。</span><span class="sxs-lookup"><span data-stu-id="07386-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="07386-242">下一步</span><span class="sxs-lookup"><span data-stu-id="07386-242">Next Step</span></span>

<span data-ttu-id="07386-243">我们现在我们可以使用查询和更新我们的数据库的模型。</span><span class="sxs-lookup"><span data-stu-id="07386-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="07386-244">让我们现在将添加一些控制器和视图到我们可以使用生成在其周围的 HTML UI 体验的项目。</span><span class="sxs-lookup"><span data-stu-id="07386-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="07386-245">[上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="07386-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
