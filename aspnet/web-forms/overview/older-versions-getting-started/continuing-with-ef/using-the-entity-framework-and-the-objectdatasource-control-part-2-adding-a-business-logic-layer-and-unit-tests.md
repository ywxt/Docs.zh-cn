---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: "使用 Entity Framework 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试 |Microsoft 文档"
author: tdykstra
description: "本教程系列上的 Contoso 大学 web 应用程序创建的 Getting Started with 实体 Framework 4.0 教程系列生成。 I..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: df37acd8901b457f7887afe767d42d53e45e4815
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a><span data-ttu-id="2992d-104">使用 Entity Framework 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试</span><span class="sxs-lookup"><span data-stu-id="2992d-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 2: Adding a Business Logic Layer and Unit Tests</span></span>
====================
<span data-ttu-id="2992d-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2992d-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="2992d-106">本教程系列上的 Contoso 大学 web 应用程序创建的生成[Getting Started with 实体 Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教程系列。</span><span class="sxs-lookup"><span data-stu-id="2992d-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="2992d-107">如果未完成前面的教程，作为一个起始点本教程，你可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，你应已创建。</span><span class="sxs-lookup"><span data-stu-id="2992d-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="2992d-108">你还可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)，它由完整教程系列创建。</span><span class="sxs-lookup"><span data-stu-id="2992d-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="2992d-109">如果你有疑问的教程，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2992d-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="2992d-110">在前面的教程中创建使用实体框架的 n 层 web 应用程序和`ObjectDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="2992d-110">In the previous tutorial you created an n-tier web application using the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="2992d-111">本教程演示如何添加业务逻辑，同时保持业务逻辑层 (BLL) 和数据访问层 (DAL) 是独立的并显示如何为 BLL 创建自动的单元测试。</span><span class="sxs-lookup"><span data-stu-id="2992d-111">This tutorial shows how to add business logic while keeping the business-logic layer (BLL) and the data-access layer (DAL) separate, and it shows how to create automated unit tests for the BLL.</span></span>

<span data-ttu-id="2992d-112">在本教程中，你将完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="2992d-112">In this tutorial you'll complete the following tasks:</span></span>

- <span data-ttu-id="2992d-113">创建存储库声明接口，你需要的数据访问方法。</span><span class="sxs-lookup"><span data-stu-id="2992d-113">Create a repository interface that declares the data-access methods you need.</span></span>
- <span data-ttu-id="2992d-114">存储库类中实现存储库的接口。</span><span class="sxs-lookup"><span data-stu-id="2992d-114">Implement the repository interface in the repository class.</span></span>
- <span data-ttu-id="2992d-115">创建调用存储库类以执行数据访问功能的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="2992d-115">Create a business-logic class that calls the repository class to perform data-access functions.</span></span>
- <span data-ttu-id="2992d-116">连接`ObjectDataSource`控件添加到存储库类而不是业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="2992d-116">Connect the `ObjectDataSource` control to the business-logic class instead of to the repository class.</span></span>
- <span data-ttu-id="2992d-117">创建单元测试项目和为其数据存储区使用内存中集合的存储库类。</span><span class="sxs-lookup"><span data-stu-id="2992d-117">Create a unit-test project and a repository class that uses in-memory collections for its data store.</span></span>
- <span data-ttu-id="2992d-118">创建你想要将添加到业务逻辑类，则运行测试并查看其失败的业务逻辑的单元测试。</span><span class="sxs-lookup"><span data-stu-id="2992d-118">Create a unit test for business logic that you want to add to the business-logic class, then run the test and see it fail.</span></span>
- <span data-ttu-id="2992d-119">实现业务逻辑在业务逻辑类中，然后重新运行单元测试并查看之通过。</span><span class="sxs-lookup"><span data-stu-id="2992d-119">Implement the business logic in the business-logic class, then re-run the unit test and see it pass.</span></span>

<span data-ttu-id="2992d-120">您将使用*Departments.aspx*和*DepartmentsAdd.aspx*你在前面的教程中创建的页。</span><span class="sxs-lookup"><span data-stu-id="2992d-120">You'll work with the *Departments.aspx* and *DepartmentsAdd.aspx* pages that you created in the previous tutorial.</span></span>

## <a name="creating-a-repository-interface"></a><span data-ttu-id="2992d-121">创建存储库接口</span><span class="sxs-lookup"><span data-stu-id="2992d-121">Creating a Repository Interface</span></span>

<span data-ttu-id="2992d-122">你将首先创建存储库接口。</span><span class="sxs-lookup"><span data-stu-id="2992d-122">You'll begin by creating the repository interface.</span></span>

<span data-ttu-id="2992d-123">[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-123">[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)</span></span>

<span data-ttu-id="2992d-124">在*DAL*文件夹中，创建一个新的类文件，将其命名为*ISchoolRepository.cs*，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2992d-124">In the *DAL* folder, create a new class file, name it *ISchoolRepository.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

<span data-ttu-id="2992d-125">该接口定义一种方法为每个 CRUD （创建、 读取、 更新、 删除） 存储库类中创建的方法。</span><span class="sxs-lookup"><span data-stu-id="2992d-125">The interface defines one method for each of the CRUD (create, read, update, delete) methods that you created in the repository class.</span></span>

<span data-ttu-id="2992d-126">在`SchoolRepository`类*SchoolRepository.cs*，指示此类实现`ISchoolRepository`接口：</span><span class="sxs-lookup"><span data-stu-id="2992d-126">In the `SchoolRepository` class in *SchoolRepository.cs*, indicate that this class implements the `ISchoolRepository` interface:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a><span data-ttu-id="2992d-127">创建业务逻辑类</span><span class="sxs-lookup"><span data-stu-id="2992d-127">Creating a Business-Logic Class</span></span>

<span data-ttu-id="2992d-128">接下来，你将创建业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="2992d-128">Next, you'll create the business-logic class.</span></span> <span data-ttu-id="2992d-129">执行此操作，以便您可以添加将由执行的业务逻辑`ObjectDataSource`控件，但不会尚未执行的。</span><span class="sxs-lookup"><span data-stu-id="2992d-129">You do this so that you can add business logic that will be executed by the `ObjectDataSource` control, although you will not do that yet.</span></span> <span data-ttu-id="2992d-130">现在，新的业务逻辑类将仅执行相同的 CRUD 操作执行存储库。</span><span class="sxs-lookup"><span data-stu-id="2992d-130">For now, the new business-logic class will only perform the same CRUD operations that the repository does.</span></span>

<span data-ttu-id="2992d-131">[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-131">[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)</span></span>

<span data-ttu-id="2992d-132">创建一个新文件夹并将其命名*BLL*。</span><span class="sxs-lookup"><span data-stu-id="2992d-132">Create a new folder and name it *BLL*.</span></span> <span data-ttu-id="2992d-133">(在实际应用中，业务逻辑层通常的实现为类库 — 一个单独的项目，但为了简化本教程，BLL 类将保留在项目文件夹。)</span><span class="sxs-lookup"><span data-stu-id="2992d-133">(In a real-world application, the business-logic layer would typically be implemented as a class library — a separate project — but to keep this tutorial simple, BLL classes will be kept in a project folder.)</span></span>

<span data-ttu-id="2992d-134">在*BLL*文件夹中，创建一个新的类文件，将其命名为*SchoolBL.cs*，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2992d-134">In the *BLL* folder, create a new class file, name it *SchoolBL.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

<span data-ttu-id="2992d-135">此代码将创建之前在存储库类中，你看到的相同 CRUD 方法但而不是直接访问的实体框架方法，它调用的存储库类方法。</span><span class="sxs-lookup"><span data-stu-id="2992d-135">This code creates the same CRUD methods you saw earlier in the repository class, but instead of accessing the Entity Framework methods directly, it calls the repository class methods.</span></span>

<span data-ttu-id="2992d-136">保存对存储库类的引用类变量定义为接口类型，并且实例化的存储库类的代码包含在两个构造函数。</span><span class="sxs-lookup"><span data-stu-id="2992d-136">The class variable that holds a reference to the repository class is defined as an interface type, and the code that instantiates the repository class is contained in two constructors.</span></span> <span data-ttu-id="2992d-137">无参数构造函数将由`ObjectDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="2992d-137">The parameterless constructor will be used by the `ObjectDataSource` control.</span></span> <span data-ttu-id="2992d-138">它创建的实例`SchoolRepository`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="2992d-138">It creates an instance of the `SchoolRepository` class that you created earlier.</span></span> <span data-ttu-id="2992d-139">另一个构造函数允许实例化的业务逻辑类以实现存储库接口的任何对象中传递的任何代码。</span><span class="sxs-lookup"><span data-stu-id="2992d-139">The other constructor allows whatever code that instantiates the business-logic class to pass in any object that implements the repository interface.</span></span>

<span data-ttu-id="2992d-140">调用存储库类和两个构造函数的 CRUD 方法，使其可以与你选择任何后端数据存储区中使用业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="2992d-140">The CRUD methods that call the repository class and the two constructors make it possible to use the business-logic class with whatever back-end data store you choose.</span></span> <span data-ttu-id="2992d-141">业务逻辑类不必注意它所调用类如何保持数据。</span><span class="sxs-lookup"><span data-stu-id="2992d-141">The business-logic class does not need to be aware of how the class that it's calling persists the data.</span></span> <span data-ttu-id="2992d-142">(此情况通常称作*持久性无感知*。)因为你可以连接到使用的内容作为一种简单的存储库实现的业务逻辑类来帮助进行单元测试，内存中作为`List`来存储数据的集合。</span><span class="sxs-lookup"><span data-stu-id="2992d-142">(This is often called *persistence ignorance*.) This facilitates unit testing, because you can connect the business-logic class to a repository implementation that uses something as simple as in-memory `List` collections to store data.</span></span>

> [!NOTE]
> <span data-ttu-id="2992d-143">从技术上讲，实体对象不仍不持久性未知，因为它们正在从实体框架的继承的类实例化`EntityObject`类。</span><span class="sxs-lookup"><span data-stu-id="2992d-143">Technically, the entity objects are still not persistence-ignorant, because they're instantiated from classes that inherit from the Entity Framework's `EntityObject` class.</span></span> <span data-ttu-id="2992d-144">对于完整持久性无感知，你可以使用*纯旧 CLR 对象*，或*POCOs*，来从继承的对象代替`EntityObject`类。</span><span class="sxs-lookup"><span data-stu-id="2992d-144">For complete persistence ignorance, you can use *plain old CLR objects*, or *POCOs*, in place of objects that inherit from the `EntityObject` class.</span></span> <span data-ttu-id="2992d-145">使用 POCOs 不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="2992d-145">Using POCOs is beyond the scope of this tutorial.</span></span> <span data-ttu-id="2992d-146">有关详细信息，请参阅[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) MSDN 网站上。)</span><span class="sxs-lookup"><span data-stu-id="2992d-146">For more information, see [Testability and Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) on the MSDN website.)</span></span>


<span data-ttu-id="2992d-147">现在你可以连接`ObjectDataSource`业务逻辑的控件类而不是到存储库并验证一切就绪像以前一样。</span><span class="sxs-lookup"><span data-stu-id="2992d-147">Now you can connect the `ObjectDataSource` controls to the business-logic class instead of to the repository and verify that everything works as it did before.</span></span>

<span data-ttu-id="2992d-148">在*Departments.aspx*和*DepartmentsAdd.aspx*，更改每个匹配项`TypeName="ContosoUniversity.DAL.SchoolRepository"`到`TypeName="ContosoUniversity.BLL.SchoolBL`"。</span><span class="sxs-lookup"><span data-stu-id="2992d-148">In *Departments.aspx* and *DepartmentsAdd.aspx*, change each occurrence of `TypeName="ContosoUniversity.DAL.SchoolRepository"` to `TypeName="ContosoUniversity.BLL.SchoolBL`".</span></span> <span data-ttu-id="2992d-149">有四个实例中所有。）</span><span class="sxs-lookup"><span data-stu-id="2992d-149">(There are four instances in all.)</span></span>

<span data-ttu-id="2992d-150">运行*Departments.aspx*和*DepartmentsAdd.aspx*页以验证它们仍工作以前一样。</span><span class="sxs-lookup"><span data-stu-id="2992d-150">Run the *Departments.aspx* and *DepartmentsAdd.aspx* pages to verify that they still work as they did before.</span></span>

<span data-ttu-id="2992d-151">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-151">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)</span></span>

<span data-ttu-id="2992d-152">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-152">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)</span></span>

## <a name="creating-a-unit-test-project-and-repository-implementation"></a><span data-ttu-id="2992d-153">创建单元测试项目和存储库实现</span><span class="sxs-lookup"><span data-stu-id="2992d-153">Creating a Unit-Test Project and Repository Implementation</span></span>

<span data-ttu-id="2992d-154">将新项目添加到解决方案使用**测试项目**模板，并将其命名`ContosoUniversity.Tests`。</span><span class="sxs-lookup"><span data-stu-id="2992d-154">Add a new project to the solution using the **Test Project** template, and name it `ContosoUniversity.Tests`.</span></span>

<span data-ttu-id="2992d-155">在测试项目中，添加对的引用`System.Data.Entity`并添加到项目引用`ContosoUniversity`项目。</span><span class="sxs-lookup"><span data-stu-id="2992d-155">In the test project, add a reference to `System.Data.Entity` and add a project reference to the `ContosoUniversity` project.</span></span>

<span data-ttu-id="2992d-156">你现在可以创建将用于单元测试的存储库类。</span><span class="sxs-lookup"><span data-stu-id="2992d-156">You can now create the repository class that you'll use with unit tests.</span></span> <span data-ttu-id="2992d-157">此存储库的数据存储将在类中。</span><span class="sxs-lookup"><span data-stu-id="2992d-157">The data store for this repository will be within the class.</span></span>

<span data-ttu-id="2992d-158">[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-158">[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)</span></span>

<span data-ttu-id="2992d-159">在测试项目中，创建一个新的类文件，将其*MockSchoolRepository.cs*，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2992d-159">In the test project, create a new class file, name it *MockSchoolRepository.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

<span data-ttu-id="2992d-160">此存储库类具有相同的 CRUD 方法与直接访问实体框架，但它们适用于的`List`而不是与数据库的内存中集合。</span><span class="sxs-lookup"><span data-stu-id="2992d-160">This repository class has the same CRUD methods as the one that accesses the Entity Framework directly, but they work with `List` collections in memory instead of with a database.</span></span> <span data-ttu-id="2992d-161">这样会对测试类来设置和验证业务逻辑类的单元测试更容易。</span><span class="sxs-lookup"><span data-stu-id="2992d-161">This makes it easier for a test class to set up and validate unit tests for the business-logic class.</span></span>

## <a name="creating-unit-tests"></a><span data-ttu-id="2992d-162">创建单元测试</span><span class="sxs-lookup"><span data-stu-id="2992d-162">Creating Unit Tests</span></span>

<span data-ttu-id="2992d-163">**测试**项目模板创建一个存根 （stub） 单元测试类，并且下一个任务是通过向其添加单元测试方法，你想要将添加到业务逻辑类的业务逻辑中修改此类。</span><span class="sxs-lookup"><span data-stu-id="2992d-163">The **Test** project template created a stub unit test class for you, and your next task is to modify this class by adding unit test methods to it for business logic that you want to add to the business-logic class.</span></span>

<span data-ttu-id="2992d-164">[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-164">[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)</span></span>

<span data-ttu-id="2992d-165">Contoso 大学，任何单个教师只能是单个部门的管理员，你需要添加业务逻辑来强制执行此规则。</span><span class="sxs-lookup"><span data-stu-id="2992d-165">At Contoso University, any individual instructor can only be the administrator of a single department, and you need to add business logic to enforce this rule.</span></span> <span data-ttu-id="2992d-166">首先，将通过添加测试和运行测试后，若要查看这些失败。</span><span class="sxs-lookup"><span data-stu-id="2992d-166">You will start by adding tests and running the tests to see them fail.</span></span> <span data-ttu-id="2992d-167">然后，你将添加代码并重新运行测试，预期会看到它们通过。</span><span class="sxs-lookup"><span data-stu-id="2992d-167">You'll then add the code and rerun the tests, expecting to see them pass.</span></span>

<span data-ttu-id="2992d-168">打开*UnitTest1.cs*文件并添加`using`ContosoUniversity 项目中创建业务逻辑和数据访问层的语句：</span><span class="sxs-lookup"><span data-stu-id="2992d-168">Open the *UnitTest1.cs* file and add `using` statements for the business logic and data-access layers that you created in the ContosoUniversity project:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

<span data-ttu-id="2992d-169">替换`TestMethod1`方法使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="2992d-169">Replace the `TestMethod1` method with the following methods:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

<span data-ttu-id="2992d-170">`CreateSchoolBL`方法创建的存储库类创建单元测试项目，然后将其传递到业务逻辑类的新实例的一个实例。</span><span class="sxs-lookup"><span data-stu-id="2992d-170">The `CreateSchoolBL` method creates an instance of the repository class that you created for the unit test project, which it then passes to a new instance of the business-logic class.</span></span> <span data-ttu-id="2992d-171">然后，该方法使用业务逻辑类来在测试方法中插入三个您可以使用的部门。</span><span class="sxs-lookup"><span data-stu-id="2992d-171">The method then uses the business-logic class to insert three departments that you can use in test methods.</span></span>

<span data-ttu-id="2992d-172">测试方法可以验证业务逻辑类引发异常，如果有人试图插入一个新部门有相同的管理员为现有的部门，或如果有人试图通过将其设置为个人的 ID 更新部门的管理员谁已经是另一个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="2992d-172">The test methods verify that the business-logic class throws an exception if someone tries to insert a new department with the same administrator as an existing department, or if someone tries to update a department's administrator by setting it to the ID of a person who is already the administrator of another department.</span></span>

<span data-ttu-id="2992d-173">你尚未创建异常类，因此将不会编译此代码。</span><span class="sxs-lookup"><span data-stu-id="2992d-173">You haven't created the exception class yet, so this code will not compile.</span></span> <span data-ttu-id="2992d-174">若要获取编译它，右键单击`DuplicateAdministratorException`和选择**生成**，，然后**类**。</span><span class="sxs-lookup"><span data-stu-id="2992d-174">To get it to compile, right-click `DuplicateAdministratorException` and select **Generate**, and then **Class**.</span></span>

<span data-ttu-id="2992d-175">[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-175">[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)</span></span>

<span data-ttu-id="2992d-176">这可以删除其中的测试项目中创建一个类主项目中创建的异常类后。</span><span class="sxs-lookup"><span data-stu-id="2992d-176">This creates a class in the test project which you can delete after you've created the exception class in the main project.</span></span> <span data-ttu-id="2992d-177">实现业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="2992d-177">and implemented the business logic.</span></span>

<span data-ttu-id="2992d-178">运行该测试项目。</span><span class="sxs-lookup"><span data-stu-id="2992d-178">Run the test project.</span></span> <span data-ttu-id="2992d-179">按预期方式运行测试将失败。</span><span class="sxs-lookup"><span data-stu-id="2992d-179">As expected, the tests fail.</span></span>

<span data-ttu-id="2992d-180">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-180">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)</span></span>

## <a name="adding-business-logic-to-make-a-test-pass"></a><span data-ttu-id="2992d-181">添加业务逻辑，以使测试通过</span><span class="sxs-lookup"><span data-stu-id="2992d-181">Adding Business Logic to Make a Test Pass</span></span>

<span data-ttu-id="2992d-182">接下来，你将实施使得无法设置为部门的管理员已经是另一个部门的管理员的人员的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="2992d-182">Next, you'll implement the business logic that makes it impossible to set as the administrator of a department someone who is already administrator of another department.</span></span> <span data-ttu-id="2992d-183">你将从业务逻辑层中，引发异常并将然后将其表示层中捕获如果用户编辑一个部门，并单击**更新**选择已经是管理员的任何人后。</span><span class="sxs-lookup"><span data-stu-id="2992d-183">You'll throw an exception from the business-logic layer, and then catch it in the presentation layer if a user edits a department and clicks **Update** after selecting someone who is already an administrator.</span></span> <span data-ttu-id="2992d-184">（你还可以从下拉列表中的用户已是管理员之前呈现页上，, 删除教师，但此处的目的是要使用业务逻辑层）。</span><span class="sxs-lookup"><span data-stu-id="2992d-184">(You could also remove instructors from the drop-down list who are already administrators before you render the page, but the purpose here is to work with the business-logic layer.)</span></span>

<span data-ttu-id="2992d-185">首先，创建在用户尝试使多个部门的管理员的一个教师时将引发的异常类。</span><span class="sxs-lookup"><span data-stu-id="2992d-185">Start by creating the exception class that you'll throw when a user tries to make an instructor the administrator of more than one department.</span></span> <span data-ttu-id="2992d-186">在主项目中，在其中创建新类文件*BLL*文件夹中，将其命名为*DuplicateAdministratorException.cs*，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2992d-186">In the main project, create a new class file in the *BLL* folder, name it *DuplicateAdministratorException.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

<span data-ttu-id="2992d-187">现在删除该临时*DuplicateAdministratorException.cs*你测试项目中创建更早版本以便能够编译的文件。</span><span class="sxs-lookup"><span data-stu-id="2992d-187">Now delete the temporary *DuplicateAdministratorException.cs* file that you created in the test project earlier in order to be able to compile.</span></span>

<span data-ttu-id="2992d-188">在主项目中，打开*SchoolBL.cs*文件并添加以下包含验证逻辑的方法。</span><span class="sxs-lookup"><span data-stu-id="2992d-188">In the main project, open the *SchoolBL.cs* file and add the following method that contains the validation logic.</span></span> <span data-ttu-id="2992d-189">（代码是指将更高版本创建的方法。）</span><span class="sxs-lookup"><span data-stu-id="2992d-189">(The code refers to a method that you'll create later.)</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

<span data-ttu-id="2992d-190">要插入或更新时，将调用此方法`Department`以便检查是否另一个部门已有相同的管理员的实体。</span><span class="sxs-lookup"><span data-stu-id="2992d-190">You'll call this method when you're inserting or updating `Department` entities in order to check whether another department already has the same administrator.</span></span>

<span data-ttu-id="2992d-191">该代码调用方法要搜索的数据库`Department`具有相同的实体`Administrator`作为实体的属性值正在被插入或更新。</span><span class="sxs-lookup"><span data-stu-id="2992d-191">The code calls a method to search the database for a `Department` entity that has the same `Administrator` property value as the entity being inserted or updated.</span></span> <span data-ttu-id="2992d-192">如果找到一个对象，该代码将引发异常。</span><span class="sxs-lookup"><span data-stu-id="2992d-192">If one is found, the code throws an exception.</span></span> <span data-ttu-id="2992d-193">不进行验证检查是必需的如果正在插入或更新的实体未包含任何`Administrator`如果在更新过程中调用该方法引发值和任何异常和`Department`找到匹配项的实体`Department`正在更新的实体。</span><span class="sxs-lookup"><span data-stu-id="2992d-193">No validation check is required if the entity being inserted or updated has no `Administrator` value, and no exception is thrown if the method is called during an update and the `Department` entity found matches the `Department` entity being updated.</span></span>

<span data-ttu-id="2992d-194">调用中的新方法`Insert`和`Update`方法：</span><span class="sxs-lookup"><span data-stu-id="2992d-194">Call the new method from the `Insert` and `Update` methods:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

<span data-ttu-id="2992d-195">在*ISchoolRepository.cs*，添加新的数据访问方法的以下声明：</span><span class="sxs-lookup"><span data-stu-id="2992d-195">In *ISchoolRepository.cs*, add the following declaration for the new data-access method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

<span data-ttu-id="2992d-196">在*SchoolRepository.cs*，添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="2992d-196">In *SchoolRepository.cs*, add the following `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

<span data-ttu-id="2992d-197">在*SchoolRepository.cs*，添加以下新的数据访问方法：</span><span class="sxs-lookup"><span data-stu-id="2992d-197">In *SchoolRepository.cs*, add the following new data-access method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

<span data-ttu-id="2992d-198">此代码检索`Department`具有指定的管理员的实体。</span><span class="sxs-lookup"><span data-stu-id="2992d-198">This code retrieves `Department` entities that have a specified administrator.</span></span> <span data-ttu-id="2992d-199">（如果有），则应找到只有一个部门。</span><span class="sxs-lookup"><span data-stu-id="2992d-199">Only one department should be found (if any).</span></span> <span data-ttu-id="2992d-200">但是，由于没有约束构建在数据库中，返回类型是一个集合，如果找到多个部门。</span><span class="sxs-lookup"><span data-stu-id="2992d-200">However, because no constraint is built into the database, the return type is a collection in case multiple departments are found.</span></span>

<span data-ttu-id="2992d-201">默认情况下，当对象上下文中从数据库中检索实体时它将跟踪的它们在其对象状态管理器中。</span><span class="sxs-lookup"><span data-stu-id="2992d-201">By default, when the object context retrieves entities from the database, it keeps track of them in its object state manager.</span></span> <span data-ttu-id="2992d-202">`MergeOption.NoTracking`参数指定此查询将不完成此跟踪。</span><span class="sxs-lookup"><span data-stu-id="2992d-202">The `MergeOption.NoTracking` parameter specifies that this tracking will not be done for this query.</span></span> <span data-ttu-id="2992d-203">这是必需的因为查询可能返回您正在尝试进行更新，确切实体，然后你将无法附加该实体。</span><span class="sxs-lookup"><span data-stu-id="2992d-203">This is necessary because the query might return the exact entity that you're trying to update, and then you would not be able to attach that entity.</span></span> <span data-ttu-id="2992d-204">例如，如果编辑中的历史记录部门*Departments.aspx*页和将管理员保留不变，此查询将返回历史系。</span><span class="sxs-lookup"><span data-stu-id="2992d-204">For example, if you edit the History department in the *Departments.aspx* page and leave the administrator unchanged, this query will return the History department.</span></span> <span data-ttu-id="2992d-205">如果`NoTracking`未设置，在其对象状态管理器中的对象上下文将已有历史记录部门实体。</span><span class="sxs-lookup"><span data-stu-id="2992d-205">If `NoTracking` is not set, the object context would already have the History department entity in its object state manager.</span></span> <span data-ttu-id="2992d-206">然后对象上下文附加重新创建从视图状态的历史记录部门实体时，会引发异常，指出`"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`。</span><span class="sxs-lookup"><span data-stu-id="2992d-206">Then when you attach the History department entity that's re-created from view state, the object context would throw an exception that says `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`.</span></span>

<span data-ttu-id="2992d-207">(作为指定的替代方法`MergeOption.NoTracking`，你可以创建新的对象上下文只需为此查询。</span><span class="sxs-lookup"><span data-stu-id="2992d-207">(As an alternative to specifying `MergeOption.NoTracking`, you could create a new object context just for this query.</span></span> <span data-ttu-id="2992d-208">因为新的对象上下文应具有其自己的对象状态管理器，有可能会不会发生冲突时调用`Attach`方法。</span><span class="sxs-lookup"><span data-stu-id="2992d-208">Because the new object context would have its own object state manager, there would be no conflict when you call the `Attach` method.</span></span> <span data-ttu-id="2992d-209">新的对象上下文将与原始对象上下文中，共享元数据和数据库连接，因此此另一种方法对性能的影响将最小。</span><span class="sxs-lookup"><span data-stu-id="2992d-209">The new object context would share metadata and database connection with the original object context, so the performance penalty of this alternate approach would be minimal.</span></span> <span data-ttu-id="2992d-210">在这里，显示的方法，但是，引入了`NoTracking`选项，你将找到在其他上下文中有用。</span><span class="sxs-lookup"><span data-stu-id="2992d-210">The approach shown here, however, introduces the `NoTracking` option, which you'll find useful in other contexts.</span></span> <span data-ttu-id="2992d-211">`NoTracking`讨论选项进一步在本系列后面的教程。)</span><span class="sxs-lookup"><span data-stu-id="2992d-211">The `NoTracking` option is discussed further in a later tutorial in this series.)</span></span>

<span data-ttu-id="2992d-212">在测试项目中，添加新数据访问方法*MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="2992d-212">In the test project, add the new data-access method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

<span data-ttu-id="2992d-213">此代码使用 LINQ 来执行相同的数据选择，`ContosoUniversity`项目存储库使用 LINQ to Entities 有关。</span><span class="sxs-lookup"><span data-stu-id="2992d-213">This code uses LINQ to perform the same data selection that the `ContosoUniversity` project repository uses LINQ to Entities for.</span></span>

<span data-ttu-id="2992d-214">再次运行测试项目。</span><span class="sxs-lookup"><span data-stu-id="2992d-214">Run the test project again.</span></span> <span data-ttu-id="2992d-215">这次测试通过了。</span><span class="sxs-lookup"><span data-stu-id="2992d-215">This time the tests pass.</span></span>

<span data-ttu-id="2992d-216">[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-216">[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)</span></span>

## <a name="handling-objectdatasource-exceptions"></a><span data-ttu-id="2992d-217">处理 ObjectDataSource 异常</span><span class="sxs-lookup"><span data-stu-id="2992d-217">Handling ObjectDataSource Exceptions</span></span>

<span data-ttu-id="2992d-218">在`ContosoUniversity`项目中，运行*Departments.aspx*页上，尝试将某个部门管理员更改为人已经是另一个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="2992d-218">In the `ContosoUniversity` project, run the *Departments.aspx* page and try to change the administrator for a department to someone who is already administrator for another department.</span></span> <span data-ttu-id="2992d-219">（记住，你只能编辑在本教程中，过程中添加的部门因为数据库将具有无效数据预加载）。获取以下服务器错误页面：</span><span class="sxs-lookup"><span data-stu-id="2992d-219">(Remember that you can only edit departments that you added during this tutorial, because the database comes preloaded with invalid data.) You get the following server error page:</span></span>

<span data-ttu-id="2992d-220">[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-220">[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)</span></span>

<span data-ttu-id="2992d-221">你不希望用户看到的错误页面，此类型，因此，你需要添加错误处理代码。</span><span class="sxs-lookup"><span data-stu-id="2992d-221">You don't want users to see this kind of error page, so you need to add error-handling code.</span></span> <span data-ttu-id="2992d-222">打开*Departments.aspx*和指定的处理程序`OnUpdated`事件`DepartmentsObjectDataSource`。</span><span class="sxs-lookup"><span data-stu-id="2992d-222">Open *Departments.aspx* and specify a handler for the `OnUpdated` event of the `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="2992d-223">`ObjectDataSource`现在开始标记类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="2992d-223">The `ObjectDataSource` opening tag now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

<span data-ttu-id="2992d-224">在*Departments.aspx.cs*，添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="2992d-224">In *Departments.aspx.cs*, add the following `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

<span data-ttu-id="2992d-225">添加以下处理程序`Updated`事件：</span><span class="sxs-lookup"><span data-stu-id="2992d-225">Add the following handler for the `Updated` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

<span data-ttu-id="2992d-226">如果`ObjectDataSource`控件捕获异常，它尝试执行更新时，它将异常传递中的事件自变量 (`e`) 到此处理程序。</span><span class="sxs-lookup"><span data-stu-id="2992d-226">If the `ObjectDataSource` control catches an exception when it tries to perform the update, it passes the exception in the event argument (`e`) to this handler.</span></span> <span data-ttu-id="2992d-227">处理程序中的代码检查该异常是否是重复管理员异常。</span><span class="sxs-lookup"><span data-stu-id="2992d-227">The code in the handler checks to see if the exception is the duplicate administrator exception.</span></span> <span data-ttu-id="2992d-228">如果是，代码将创建包含的错误消息的验证程序控件`ValidationSummary`控件来显示。</span><span class="sxs-lookup"><span data-stu-id="2992d-228">If it is, the code creates a validator control that contains an error message for the `ValidationSummary` control to display.</span></span>

<span data-ttu-id="2992d-229">运行页面，并尝试再次使人成为两个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="2992d-229">Run the page and attempt to make someone the administrator of two departments again.</span></span> <span data-ttu-id="2992d-230">这一次`ValidationSummary`控件将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="2992d-230">This time the `ValidationSummary` control displays an error message.</span></span>

<span data-ttu-id="2992d-231">[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="2992d-231">[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)</span></span>

<span data-ttu-id="2992d-232">进行类似更改到*DepartmentsAdd.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="2992d-232">Make similar changes to the *DepartmentsAdd.aspx* page.</span></span> <span data-ttu-id="2992d-233">在*DepartmentsAdd.aspx*，指定的处理程序`OnInserted`事件`DepartmentsObjectDataSource`。</span><span class="sxs-lookup"><span data-stu-id="2992d-233">In *DepartmentsAdd.aspx*, specify a handler for the `OnInserted` event of the `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="2992d-234">生成的标记将类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="2992d-234">The resulting markup will resemble the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

<span data-ttu-id="2992d-235">在*DepartmentsAdd.aspx.cs*，将同一`using`语句：</span><span class="sxs-lookup"><span data-stu-id="2992d-235">In *DepartmentsAdd.aspx.cs*, add the same `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

<span data-ttu-id="2992d-236">添加以下事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="2992d-236">Add the following event handler:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

<span data-ttu-id="2992d-237">你现在可以测试*DepartmentsAdd.aspx.cs*页以验证它还能正确地处理尝试使多个部门的管理员的人。</span><span class="sxs-lookup"><span data-stu-id="2992d-237">You can now test the *DepartmentsAdd.aspx.cs* page to verify that it also correctly handles attempts to make one person the administrator of more than one department.</span></span>

<span data-ttu-id="2992d-238">这将完成实现使用的存储库模式简介`ObjectDataSource`与实体框架的控件。</span><span class="sxs-lookup"><span data-stu-id="2992d-238">This completes the introduction to implementing the repository pattern for using the `ObjectDataSource` control with the Entity Framework.</span></span> <span data-ttu-id="2992d-239">有关存储库模式和可测试性的详细信息，请参阅 MSDN 白皮书[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2992d-239">For more information about the repository pattern and testability, see the MSDN whitepaper [Testability and Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx).</span></span>

<span data-ttu-id="2992d-240">在以下教程中，你将看到如何添加排序和筛选到应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="2992d-240">In the following tutorial you'll see how to add sorting and filtering functionality to the application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2992d-241">[上一页](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
[下一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)</span><span class="sxs-lookup"><span data-stu-id="2992d-241">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
[Next](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)</span></span>
