---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 使用实体框架 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 02f0b86203eb879ca618655b8956f22dc67858cd
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394237"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a><span data-ttu-id="5b1f0-104">使用实体框架 4.0 和 ObjectDataSource 控件，第 2 部分： 添加业务逻辑层和单元测试</span><span class="sxs-lookup"><span data-stu-id="5b1f0-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 2: Adding a Business Logic Layer and Unit Tests</span></span>
====================
<span data-ttu-id="5b1f0-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="5b1f0-106">本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="5b1f0-107">如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="5b1f0-108">此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="5b1f0-109">如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="5b1f0-110">在上一教程中创建使用实体框架的 n 层 web 应用程序和`ObjectDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-110">In the previous tutorial you created an n-tier web application using the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="5b1f0-111">本教程演示如何添加业务逻辑，同时保持业务逻辑层 (BLL) 和数据访问层 (DAL) 是独立的以及如何为 BLL 创建自动化的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-111">This tutorial shows how to add business logic while keeping the business-logic layer (BLL) and the data-access layer (DAL) separate, and it shows how to create automated unit tests for the BLL.</span></span>

<span data-ttu-id="5b1f0-112">在本教程中将完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-112">In this tutorial you'll complete the following tasks:</span></span>

- <span data-ttu-id="5b1f0-113">创建存储库接口声明所需的数据访问方法。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-113">Create a repository interface that declares the data-access methods you need.</span></span>
- <span data-ttu-id="5b1f0-114">存储库类中实现存储库的接口。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-114">Implement the repository interface in the repository class.</span></span>
- <span data-ttu-id="5b1f0-115">创建调用存储库类以执行数据访问功能的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-115">Create a business-logic class that calls the repository class to perform data-access functions.</span></span>
- <span data-ttu-id="5b1f0-116">连接`ObjectDataSource`业务逻辑类而不是存储库类的控件。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-116">Connect the `ObjectDataSource` control to the business-logic class instead of to the repository class.</span></span>
- <span data-ttu-id="5b1f0-117">创建单元测试项目和使用内存中集合来存储其数据的存储库类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-117">Create a unit-test project and a repository class that uses in-memory collections for its data store.</span></span>
- <span data-ttu-id="5b1f0-118">创建你想要添加到业务逻辑类，然后运行测试并查看其失败的业务逻辑的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-118">Create a unit test for business logic that you want to add to the business-logic class, then run the test and see it fail.</span></span>
- <span data-ttu-id="5b1f0-119">在业务逻辑类中，实现业务逻辑，然后重新运行单元测试并查看它的传递。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-119">Implement the business logic in the business-logic class, then re-run the unit test and see it pass.</span></span>

<span data-ttu-id="5b1f0-120">您将使用*Departments.aspx*并*DepartmentsAdd.aspx*在上一教程中创建的页。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-120">You'll work with the *Departments.aspx* and *DepartmentsAdd.aspx* pages that you created in the previous tutorial.</span></span>

## <a name="creating-a-repository-interface"></a><span data-ttu-id="5b1f0-121">创建存储库接口</span><span class="sxs-lookup"><span data-stu-id="5b1f0-121">Creating a Repository Interface</span></span>

<span data-ttu-id="5b1f0-122">您将首先创建存储库接口。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-122">You'll begin by creating the repository interface.</span></span>

<span data-ttu-id="5b1f0-123">[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-123">[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)</span></span>

<span data-ttu-id="5b1f0-124">在中*DAL*文件夹中，创建一个新类文件，将其命名*ISchoolRepository.cs*，和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-124">In the *DAL* folder, create a new class file, name it *ISchoolRepository.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

<span data-ttu-id="5b1f0-125">该接口定义的一种方法为每个 CRUD （创建、 读取、 更新、 删除） 存储库类中创建的方法。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-125">The interface defines one method for each of the CRUD (create, read, update, delete) methods that you created in the repository class.</span></span>

<span data-ttu-id="5b1f0-126">在中`SchoolRepository`类中*SchoolRepository.cs*，指示此类实现`ISchoolRepository`接口：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-126">In the `SchoolRepository` class in *SchoolRepository.cs*, indicate that this class implements the `ISchoolRepository` interface:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a><span data-ttu-id="5b1f0-127">创建业务逻辑类</span><span class="sxs-lookup"><span data-stu-id="5b1f0-127">Creating a Business-Logic Class</span></span>

<span data-ttu-id="5b1f0-128">接下来，你将创建业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-128">Next, you'll create the business-logic class.</span></span> <span data-ttu-id="5b1f0-129">执行此操作，以便可以添加将由执行的业务逻辑`ObjectDataSource`控件，但不会尚未执行的。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-129">You do this so that you can add business logic that will be executed by the `ObjectDataSource` control, although you will not do that yet.</span></span> <span data-ttu-id="5b1f0-130">现在，新的业务逻辑类将仅执行相同的 CRUD 操作的存储库。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-130">For now, the new business-logic class will only perform the same CRUD operations that the repository does.</span></span>

<span data-ttu-id="5b1f0-131">[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-131">[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)</span></span>

<span data-ttu-id="5b1f0-132">创建一个新文件夹并将其命名*BLL*。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-132">Create a new folder and name it *BLL*.</span></span> <span data-ttu-id="5b1f0-133">(在实际应用程序中，业务逻辑层将通常作为实现的类库，一个单独的项目，但为了简化本教程中，BLL 类将保留在项目文件夹中。)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-133">(In a real-world application, the business-logic layer would typically be implemented as a class library — a separate project — but to keep this tutorial simple, BLL classes will be kept in a project folder.)</span></span>

<span data-ttu-id="5b1f0-134">在中*BLL*文件夹中，创建一个新类文件，将其命名*SchoolBL.cs*，和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-134">In the *BLL* folder, create a new class file, name it *SchoolBL.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

<span data-ttu-id="5b1f0-135">此代码将创建前面在存储库类中，您看到的相同的 CRUD 方法，但调用而不是直接访问的实体框架方法，它在存储库类方法。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-135">This code creates the same CRUD methods you saw earlier in the repository class, but instead of accessing the Entity Framework methods directly, it calls the repository class methods.</span></span>

<span data-ttu-id="5b1f0-136">保存对存储库类的引用的类变量定义为接口类型，并实例化存储库类的代码包含在两个构造函数。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-136">The class variable that holds a reference to the repository class is defined as an interface type, and the code that instantiates the repository class is contained in two constructors.</span></span> <span data-ttu-id="5b1f0-137">无参数构造函数将由`ObjectDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-137">The parameterless constructor will be used by the `ObjectDataSource` control.</span></span> <span data-ttu-id="5b1f0-138">它创建的实例`SchoolRepository`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-138">It creates an instance of the `SchoolRepository` class that you created earlier.</span></span> <span data-ttu-id="5b1f0-139">另一个构造函数允许实例化业务逻辑类将实现存储库接口的任何对象中传递的任何代码。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-139">The other constructor allows whatever code that instantiates the business-logic class to pass in any object that implements the repository interface.</span></span>

<span data-ttu-id="5b1f0-140">调用存储库类和两个构造函数的 CRUD 方法，使其可以与您选择任何后端数据存储区一起使用的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-140">The CRUD methods that call the repository class and the two constructors make it possible to use the business-logic class with whatever back-end data store you choose.</span></span> <span data-ttu-id="5b1f0-141">业务逻辑类不需要，需要注意的调用类如何持久保存数据。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-141">The business-logic class does not need to be aware of how the class that it's calling persists the data.</span></span> <span data-ttu-id="5b1f0-142">(此情况通常称作*持久性无感知*。)这有利于进行单元测试，因为你可以连接到使用的内容作为一种简单的存储库实现的业务逻辑类作为内存中`List`集合来存储数据。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-142">(This is often called *persistence ignorance*.) This facilitates unit testing, because you can connect the business-logic class to a repository implementation that uses something as simple as in-memory `List` collections to store data.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1f0-143">从技术上讲，实体对象是仍不持久性未知，因为它们从实体框架的继承的类实例化`EntityObject`类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-143">Technically, the entity objects are still not persistence-ignorant, because they're instantiated from classes that inherit from the Entity Framework's `EntityObject` class.</span></span> <span data-ttu-id="5b1f0-144">可以使用完整的持久性无感知*普通旧 CLR 对象*，或*Poco*，来替代继承的对象`EntityObject`类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-144">For complete persistence ignorance, you can use *plain old CLR objects*, or *POCOs*, in place of objects that inherit from the `EntityObject` class.</span></span> <span data-ttu-id="5b1f0-145">使用 Poco 不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-145">Using POCOs is beyond the scope of this tutorial.</span></span> <span data-ttu-id="5b1f0-146">有关详细信息，请参阅[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) MSDN 网站上。)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-146">For more information, see [Testability and Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) on the MSDN website.)</span></span>


<span data-ttu-id="5b1f0-147">现在可以连接`ObjectDataSource`控件添加到业务逻辑类而不是到存储库并验证一切正常就像以前一样。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-147">Now you can connect the `ObjectDataSource` controls to the business-logic class instead of to the repository and verify that everything works as it did before.</span></span>

<span data-ttu-id="5b1f0-148">在中*Departments.aspx*并*DepartmentsAdd.aspx*，更改每个匹配项`TypeName="ContosoUniversity.DAL.SchoolRepository"`到`TypeName="ContosoUniversity.BLL.SchoolBL`"。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-148">In *Departments.aspx* and *DepartmentsAdd.aspx*, change each occurrence of `TypeName="ContosoUniversity.DAL.SchoolRepository"` to `TypeName="ContosoUniversity.BLL.SchoolBL`".</span></span> <span data-ttu-id="5b1f0-149">(有四个实例中所有。）</span><span class="sxs-lookup"><span data-stu-id="5b1f0-149">(There are four instances in all.)</span></span>

<span data-ttu-id="5b1f0-150">运行*Departments.aspx*并*DepartmentsAdd.aspx*页以验证它们仍能够与以前一样。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-150">Run the *Departments.aspx* and *DepartmentsAdd.aspx* pages to verify that they still work as they did before.</span></span>

<span data-ttu-id="5b1f0-151">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-151">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)</span></span>

<span data-ttu-id="5b1f0-152">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-152">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)</span></span>

## <a name="creating-a-unit-test-project-and-repository-implementation"></a><span data-ttu-id="5b1f0-153">创建单元测试项目和存储库实现</span><span class="sxs-lookup"><span data-stu-id="5b1f0-153">Creating a Unit-Test Project and Repository Implementation</span></span>

<span data-ttu-id="5b1f0-154">将新项目添加到解决方案： 使用**测试项目**模板，并将其命名`ContosoUniversity.Tests`。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-154">Add a new project to the solution using the **Test Project** template, and name it `ContosoUniversity.Tests`.</span></span>

<span data-ttu-id="5b1f0-155">在测试项目中，添加对的引用`System.Data.Entity`并添加到项目引用`ContosoUniversity`项目。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-155">In the test project, add a reference to `System.Data.Entity` and add a project reference to the `ContosoUniversity` project.</span></span>

<span data-ttu-id="5b1f0-156">现在可以创建将用于单元测试的存储库类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-156">You can now create the repository class that you'll use with unit tests.</span></span> <span data-ttu-id="5b1f0-157">此存储库的数据存储将在类中。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-157">The data store for this repository will be within the class.</span></span>

<span data-ttu-id="5b1f0-158">[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-158">[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)</span></span>

<span data-ttu-id="5b1f0-159">在测试项目中，创建一个新类文件，将其命名*MockSchoolRepository.cs*，和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-159">In the test project, create a new class file, name it *MockSchoolRepository.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

<span data-ttu-id="5b1f0-160">此存储库类将具有与直接访问 Entity Framework 相同的 CRUD 方法，但它们适用于`List`内存而不是与数据库中的集合。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-160">This repository class has the same CRUD methods as the one that accesses the Entity Framework directly, but they work with `List` collections in memory instead of with a database.</span></span> <span data-ttu-id="5b1f0-161">这简化了安装和验证业务逻辑类的单元测试的测试类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-161">This makes it easier for a test class to set up and validate unit tests for the business-logic class.</span></span>

## <a name="creating-unit-tests"></a><span data-ttu-id="5b1f0-162">创建单元测试</span><span class="sxs-lookup"><span data-stu-id="5b1f0-162">Creating Unit Tests</span></span>

<span data-ttu-id="5b1f0-163">**测试**项目模板创建存根 （stub） 单元测试类，并将下一个任务是通过的业务逻辑的你想要添加到业务逻辑类向其添加单元测试方法中修改此类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-163">The **Test** project template created a stub unit test class for you, and your next task is to modify this class by adding unit test methods to it for business logic that you want to add to the business-logic class.</span></span>

<span data-ttu-id="5b1f0-164">[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-164">[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)</span></span>

<span data-ttu-id="5b1f0-165">Contoso 大学，任何单个 instructor 只能单个部门的管理员，您需要添加业务逻辑以强制实施此规则。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-165">At Contoso University, any individual instructor can only be the administrator of a single department, and you need to add business logic to enforce this rule.</span></span> <span data-ttu-id="5b1f0-166">首先，将通过添加测试和运行测试后，若要查看这些失败。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-166">You will start by adding tests and running the tests to see them fail.</span></span> <span data-ttu-id="5b1f0-167">然后，将添加代码，并重新运行测试，预期会看到它们通过。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-167">You'll then add the code and rerun the tests, expecting to see them pass.</span></span>

<span data-ttu-id="5b1f0-168">打开*UnitTest1.cs*文件，并添加`using`ContosoUniversity 项目中创建业务逻辑和数据访问层的语句：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-168">Open the *UnitTest1.cs* file and add `using` statements for the business logic and data-access layers that you created in the ContosoUniversity project:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

<span data-ttu-id="5b1f0-169">替换为`TestMethod1`方法使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-169">Replace the `TestMethod1` method with the following methods:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

<span data-ttu-id="5b1f0-170">`CreateSchoolBL`方法创建的存储库类创建的单元测试项目，然后将其传递到业务逻辑类的新实例的一个实例。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-170">The `CreateSchoolBL` method creates an instance of the repository class that you created for the unit test project, which it then passes to a new instance of the business-logic class.</span></span> <span data-ttu-id="5b1f0-171">然后，该方法使用业务逻辑类在测试方法中插入三个可以使用的部门。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-171">The method then uses the business-logic class to insert three departments that you can use in test methods.</span></span>

<span data-ttu-id="5b1f0-172">测试方法验证业务逻辑类引发异常，如果有人试图插入新系与现有院系，作为同一管理员或者有人尝试通过将其设置为一个人的 ID 来更新部门的管理员谁已经是另一部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-172">The test methods verify that the business-logic class throws an exception if someone tries to insert a new department with the same administrator as an existing department, or if someone tries to update a department's administrator by setting it to the ID of a person who is already the administrator of another department.</span></span>

<span data-ttu-id="5b1f0-173">你尚未创建异常类，因此此代码将不进行编译。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-173">You haven't created the exception class yet, so this code will not compile.</span></span> <span data-ttu-id="5b1f0-174">若要获取其进行编译，请右键单击`DuplicateAdministratorException`，然后选择**生成**，然后**类**。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-174">To get it to compile, right-click `DuplicateAdministratorException` and select **Generate**, and then **Class**.</span></span>

<span data-ttu-id="5b1f0-175">[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-175">[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)</span></span>

<span data-ttu-id="5b1f0-176">这将创建一个类中的测试项目，您可以删除在主项目中创建的异常类后。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-176">This creates a class in the test project which you can delete after you've created the exception class in the main project.</span></span> <span data-ttu-id="5b1f0-177">和实现业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-177">and implemented the business logic.</span></span>

<span data-ttu-id="5b1f0-178">运行测试项目。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-178">Run the test project.</span></span> <span data-ttu-id="5b1f0-179">按预期运行，则测试失败。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-179">As expected, the tests fail.</span></span>

<span data-ttu-id="5b1f0-180">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-180">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)</span></span>

## <a name="adding-business-logic-to-make-a-test-pass"></a><span data-ttu-id="5b1f0-181">添加业务逻辑，以使测试通过</span><span class="sxs-lookup"><span data-stu-id="5b1f0-181">Adding Business Logic to Make a Test Pass</span></span>

<span data-ttu-id="5b1f0-182">接下来，将实现使我们无法设置为某个部门的管理员已经是另一部门的管理员的人员的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-182">Next, you'll implement the business logic that makes it impossible to set as the administrator of a department someone who is already administrator of another department.</span></span> <span data-ttu-id="5b1f0-183">将业务逻辑层中，从引发异常，然后将其表示层中捕获如果用户编辑院系，并单击**更新**选择已是管理员的人后。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-183">You'll throw an exception from the business-logic layer, and then catch it in the presentation layer if a user edits a department and clicks **Update** after selecting someone who is already an administrator.</span></span> <span data-ttu-id="5b1f0-184">（你还可以从下拉列表中的用户已是管理员之前呈现页上，, 删除教师，但此处的目的是要使用业务逻辑层。)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-184">(You could also remove instructors from the drop-down list who are already administrators before you render the page, but the purpose here is to work with the business-logic layer.)</span></span>

<span data-ttu-id="5b1f0-185">首先创建在用户尝试使多个部门的管理员的一名讲师时将引发的异常类。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-185">Start by creating the exception class that you'll throw when a user tries to make an instructor the administrator of more than one department.</span></span> <span data-ttu-id="5b1f0-186">在主项目中，创建新的类文件中*BLL*文件夹中，其命名*DuplicateAdministratorException.cs*，和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-186">In the main project, create a new class file in the *BLL* folder, name it *DuplicateAdministratorException.cs*, and replace the existing code with the following code:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

<span data-ttu-id="5b1f0-187">现在，删除临时*DuplicateAdministratorException.cs*中创建测试项目之前为了能够编译的文件。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-187">Now delete the temporary *DuplicateAdministratorException.cs* file that you created in the test project earlier in order to be able to compile.</span></span>

<span data-ttu-id="5b1f0-188">在主项目中，打开*SchoolBL.cs*文件，并添加以下方法，以便包含验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-188">In the main project, open the *SchoolBL.cs* file and add the following method that contains the validation logic.</span></span> <span data-ttu-id="5b1f0-189">（代码将引用你将更高版本创建的方法。）</span><span class="sxs-lookup"><span data-stu-id="5b1f0-189">(The code refers to a method that you'll create later.)</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

<span data-ttu-id="5b1f0-190">要插入或更新时，将调用此方法`Department`以检查另一部门是否已具有相同的管理员的实体。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-190">You'll call this method when you're inserting or updating `Department` entities in order to check whether another department already has the same administrator.</span></span>

<span data-ttu-id="5b1f0-191">该代码调用方法要搜索的数据库`Department`具有相同的实体`Administrator`作为正在插入或更新的实体的属性值。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-191">The code calls a method to search the database for a `Department` entity that has the same `Administrator` property value as the entity being inserted or updated.</span></span> <span data-ttu-id="5b1f0-192">如果找到一个对象，该代码将引发异常。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-192">If one is found, the code throws an exception.</span></span> <span data-ttu-id="5b1f0-193">不进行验证检查是必需的如果正在插入或更新的实体不具有`Administrator`如果在更新过程中调用该方法，将引发值和任何异常并`Department`找到匹配项的实体`Department`实体正在更新。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-193">No validation check is required if the entity being inserted or updated has no `Administrator` value, and no exception is thrown if the method is called during an update and the `Department` entity found matches the `Department` entity being updated.</span></span>

<span data-ttu-id="5b1f0-194">调用中的新方法`Insert`和`Update`方法：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-194">Call the new method from the `Insert` and `Update` methods:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

<span data-ttu-id="5b1f0-195">在中*ISchoolRepository.cs*，添加新的数据访问方法的以下声明：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-195">In *ISchoolRepository.cs*, add the following declaration for the new data-access method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

<span data-ttu-id="5b1f0-196">在中*SchoolRepository.cs*，添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-196">In *SchoolRepository.cs*, add the following `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

<span data-ttu-id="5b1f0-197">在中*SchoolRepository.cs*，添加以下新的数据访问方法：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-197">In *SchoolRepository.cs*, add the following new data-access method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

<span data-ttu-id="5b1f0-198">此代码检索`Department`具有指定的管理员的实体。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-198">This code retrieves `Department` entities that have a specified administrator.</span></span> <span data-ttu-id="5b1f0-199">可以看到只有一个部门和 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-199">Only one department should be found (if any).</span></span> <span data-ttu-id="5b1f0-200">但是，由于没有约束内置到数据库中，返回类型是集合找到多个部门的情况下。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-200">However, because no constraint is built into the database, the return type is a collection in case multiple departments are found.</span></span>

<span data-ttu-id="5b1f0-201">默认情况下，对象上下文从数据库检索实体时，它跟踪的它们在其对象状态管理器中。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-201">By default, when the object context retrieves entities from the database, it keeps track of them in its object state manager.</span></span> <span data-ttu-id="5b1f0-202">`MergeOption.NoTracking`参数指定此查询将无法完成此跟踪。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-202">The `MergeOption.NoTracking` parameter specifies that this tracking will not be done for this query.</span></span> <span data-ttu-id="5b1f0-203">这是必需的因为查询可能返回确切想要更新的实体，然后您就会无法附加该实体。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-203">This is necessary because the query might return the exact entity that you're trying to update, and then you would not be able to attach that entity.</span></span> <span data-ttu-id="5b1f0-204">例如，如果您编辑在历史记录院系*Departments.aspx*页并将管理员保留不变，此查询将返回历史系。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-204">For example, if you edit the History department in the *Departments.aspx* page and leave the administrator unchanged, this query will return the History department.</span></span> <span data-ttu-id="5b1f0-205">如果`NoTracking`未设置，对象上下文将其对象状态管理器中已有的历史记录 department 实体。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-205">If `NoTracking` is not set, the object context would already have the History department entity in its object state manager.</span></span> <span data-ttu-id="5b1f0-206">对象上下文附加时重新创建从视图状态的历史记录 department 实体，将引发异常，指示`"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-206">Then when you attach the History department entity that's re-created from view state, the object context would throw an exception that says `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`.</span></span>

<span data-ttu-id="5b1f0-207">(为指定的替代方法`MergeOption.NoTracking`，可以创建新的对象上下文只需为此查询。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-207">(As an alternative to specifying `MergeOption.NoTracking`, you could create a new object context just for this query.</span></span> <span data-ttu-id="5b1f0-208">因为新的对象上下文会有其自己的对象状态管理器，会有不会发生冲突时调用`Attach`方法。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-208">Because the new object context would have its own object state manager, there would be no conflict when you call the `Attach` method.</span></span> <span data-ttu-id="5b1f0-209">新的对象上下文将与原始对象上下文中，共享元数据和数据库连接，因此此备用方法的性能损失最少。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-209">The new object context would share metadata and database connection with the original object context, so the performance penalty of this alternate approach would be minimal.</span></span> <span data-ttu-id="5b1f0-210">但是，会在这里，所示的方法引入`NoTracking`选项，您会发现在其他上下文中非常有用。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-210">The approach shown here, however, introduces the `NoTracking` option, which you'll find useful in other contexts.</span></span> <span data-ttu-id="5b1f0-211">`NoTracking`讨论选项进一步在本系列中下一个教程。)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-211">The `NoTracking` option is discussed further in a later tutorial in this series.)</span></span>

<span data-ttu-id="5b1f0-212">在测试项目中，将添加到新的数据访问方法*MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="5b1f0-212">In the test project, add the new data-access method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

<span data-ttu-id="5b1f0-213">此代码使用 LINQ 来执行相同的数据选择的`ContosoUniversity`项目存储库使用 LINQ to Entities 的。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-213">This code uses LINQ to perform the same data selection that the `ContosoUniversity` project repository uses LINQ to Entities for.</span></span>

<span data-ttu-id="5b1f0-214">再次运行测试项目。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-214">Run the test project again.</span></span> <span data-ttu-id="5b1f0-215">这次测试通过了。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-215">This time the tests pass.</span></span>

<span data-ttu-id="5b1f0-216">[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-216">[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)</span></span>

## <a name="handling-objectdatasource-exceptions"></a><span data-ttu-id="5b1f0-217">处理的异常对象数据源</span><span class="sxs-lookup"><span data-stu-id="5b1f0-217">Handling ObjectDataSource Exceptions</span></span>

<span data-ttu-id="5b1f0-218">在中`ContosoUniversity`项目中，运行*Departments.aspx*页上，并尝试将某个部门的管理员更改的人已经是另一部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-218">In the `ContosoUniversity` project, run the *Departments.aspx* page and try to change the administrator for a department to someone who is already administrator for another department.</span></span> <span data-ttu-id="5b1f0-219">（请记住，你只能编辑部门添加在本教程中，因为在数据库恢复包含无效的数据预加载。）获取以下服务器错误页：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-219">(Remember that you can only edit departments that you added during this tutorial, because the database comes preloaded with invalid data.) You get the following server error page:</span></span>

<span data-ttu-id="5b1f0-220">[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-220">[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)</span></span>

<span data-ttu-id="5b1f0-221">您不希望用户看到错误页上，此类，因此需要添加错误处理代码。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-221">You don't want users to see this kind of error page, so you need to add error-handling code.</span></span> <span data-ttu-id="5b1f0-222">打开*Departments.aspx*并指定的处理程序`OnUpdated`事件的`DepartmentsObjectDataSource`。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-222">Open *Departments.aspx* and specify a handler for the `OnUpdated` event of the `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="5b1f0-223">`ObjectDataSource`现在开始标记类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-223">The `ObjectDataSource` opening tag now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

<span data-ttu-id="5b1f0-224">在中*Departments.aspx.cs*，添加以下`using`语句：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-224">In *Departments.aspx.cs*, add the following `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

<span data-ttu-id="5b1f0-225">添加以下处理程序`Updated`事件：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-225">Add the following handler for the `Updated` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

<span data-ttu-id="5b1f0-226">如果`ObjectDataSource`控制捕获异常，当其尝试执行更新时，它将异常传递事件参数中 (`e`) 向此处理程序。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-226">If the `ObjectDataSource` control catches an exception when it tries to perform the update, it passes the exception in the event argument (`e`) to this handler.</span></span> <span data-ttu-id="5b1f0-227">在处理程序中的代码检查异常是否重复管理员异常。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-227">The code in the handler checks to see if the exception is the duplicate administrator exception.</span></span> <span data-ttu-id="5b1f0-228">如果是，代码将创建包含的错误消息的验证程序控件`ValidationSummary`控件来显示。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-228">If it is, the code creates a validator control that contains an error message for the `ValidationSummary` control to display.</span></span>

<span data-ttu-id="5b1f0-229">运行页面并尝试再次使人成为两个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-229">Run the page and attempt to make someone the administrator of two departments again.</span></span> <span data-ttu-id="5b1f0-230">这一次`ValidationSummary`控件将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-230">This time the `ValidationSummary` control displays an error message.</span></span>

<span data-ttu-id="5b1f0-231">[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-231">[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)</span></span>

<span data-ttu-id="5b1f0-232">进行到类似的更改*DepartmentsAdd.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-232">Make similar changes to the *DepartmentsAdd.aspx* page.</span></span> <span data-ttu-id="5b1f0-233">在中*DepartmentsAdd.aspx*，指定的处理程序`OnInserted`事件的`DepartmentsObjectDataSource`。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-233">In *DepartmentsAdd.aspx*, specify a handler for the `OnInserted` event of the `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="5b1f0-234">所得的标记将类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-234">The resulting markup will resemble the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

<span data-ttu-id="5b1f0-235">在中*DepartmentsAdd.aspx.cs*，将同一`using`语句：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-235">In *DepartmentsAdd.aspx.cs*, add the same `using` statement:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

<span data-ttu-id="5b1f0-236">添加以下事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="5b1f0-236">Add the following event handler:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

<span data-ttu-id="5b1f0-237">现在可以测试*DepartmentsAdd.aspx.cs*页以验证它也可以正确处理尝试使多个部门的管理员的人。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-237">You can now test the *DepartmentsAdd.aspx.cs* page to verify that it also correctly handles attempts to make one person the administrator of more than one department.</span></span>

<span data-ttu-id="5b1f0-238">这将完成对实现使用的存储库模式引入`ObjectDataSource`使用实体框架的控件。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-238">This completes the introduction to implementing the repository pattern for using the `ObjectDataSource` control with the Entity Framework.</span></span> <span data-ttu-id="5b1f0-239">有关存储库模式和可测试性的详细信息，请参阅 MSDN 白皮书[可测试性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-239">For more information about the repository pattern and testability, see the MSDN whitepaper [Testability and Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx).</span></span>

<span data-ttu-id="5b1f0-240">以下教程中你将了解如何添加排序和筛选的应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="5b1f0-240">In the following tutorial you'll see how to add sorting and filtering functionality to the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5b1f0-241">[上一页](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [下一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)</span><span class="sxs-lookup"><span data-stu-id="5b1f0-241">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
[Next](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)</span></span>
