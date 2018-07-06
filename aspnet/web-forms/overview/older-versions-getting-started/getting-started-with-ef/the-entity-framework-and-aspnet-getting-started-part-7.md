---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 7 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: bb1abe52b913785f47b7f8ec9822ed9db5ee8a05
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823395"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a><span data-ttu-id="ffc04-104">Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 7 部分</span><span class="sxs-lookup"><span data-stu-id="ffc04-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 7</span></span>
====================
<span data-ttu-id="ffc04-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ffc04-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="ffc04-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffc04-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="ffc04-107">有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="ffc04-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="using-stored-procedures"></a><span data-ttu-id="ffc04-108">使用存储过程</span><span class="sxs-lookup"><span data-stu-id="ffc04-108">Using Stored Procedures</span></span>

<span data-ttu-id="ffc04-109">在上一教程中，您将实现的每个层次结构一个表继承模式。</span><span class="sxs-lookup"><span data-stu-id="ffc04-109">In the previous tutorial you implemented a table-per-hierarchy inheritance pattern.</span></span> <span data-ttu-id="ffc04-110">本教程将演示如何使用存储的过程来获得更好地控制数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="ffc04-110">This tutorial will show you how to use stored procedures to gain more control over database access.</span></span>

<span data-ttu-id="ffc04-111">实体框架允许你指定它应将存储的过程用于数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="ffc04-111">The Entity Framework lets you specify that it should use stored procedures for database access.</span></span> <span data-ttu-id="ffc04-112">对于任何实体类型，可以指定要用于创建、 更新或删除该类型的实体的存储的过程。</span><span class="sxs-lookup"><span data-stu-id="ffc04-112">For any entity type, you can specify a stored procedure to use for creating, updating, or deleting entities of that type.</span></span> <span data-ttu-id="ffc04-113">然后在数据模型中可以添加到存储过程可用于执行任务，例如检索实体集的引用。</span><span class="sxs-lookup"><span data-stu-id="ffc04-113">Then in the data model you can add references to stored procedures that you can use to perform tasks such as retrieving sets of entities.</span></span>

<span data-ttu-id="ffc04-114">使用存储的过程是数据库访问权限的一个常见要求。</span><span class="sxs-lookup"><span data-stu-id="ffc04-114">Using stored procedures is a common requirement for database access.</span></span> <span data-ttu-id="ffc04-115">在某些情况下的数据库管理员可能需要的所有数据库访问都经历出于安全原因的存储过程。</span><span class="sxs-lookup"><span data-stu-id="ffc04-115">In some cases a database administrator may require that all database access go through stored procedures for security reasons.</span></span> <span data-ttu-id="ffc04-116">在其他情况下您可能想要构建到实体框架在更新数据库时使用的进程的一些业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="ffc04-116">In other cases you may want to build business logic into some of the processes that the Entity Framework uses when it updates the database.</span></span> <span data-ttu-id="ffc04-117">例如，删除某个实体时您可能想要将其复制到存档数据库。</span><span class="sxs-lookup"><span data-stu-id="ffc04-117">For example, whenever an entity is deleted you might want to copy it to an archive database.</span></span> <span data-ttu-id="ffc04-118">或者，每次更新行时您可能想要一次更改该记录到日志记录表中写入行。</span><span class="sxs-lookup"><span data-stu-id="ffc04-118">Or whenever a row is updated you might want to write a row to a logging table that records who made the change.</span></span> <span data-ttu-id="ffc04-119">每当 Entity Framework 删除的实体或实体来更新实体时调用的存储过程中，可以执行这些类型的任务。</span><span class="sxs-lookup"><span data-stu-id="ffc04-119">You can perform these kinds of tasks in a stored procedure that's called whenever the Entity Framework deletes an entity or updates an entity.</span></span>

<span data-ttu-id="ffc04-120">如前面的教程，你将不创建任何新页面。</span><span class="sxs-lookup"><span data-stu-id="ffc04-120">As in the previous tutorial, you'll not create any new pages.</span></span> <span data-ttu-id="ffc04-121">相反，你将更改实体框架访问数据库，对于某些已创建的页面的方式。</span><span class="sxs-lookup"><span data-stu-id="ffc04-121">Instead, you'll change the way the Entity Framework accesses the database for some of the pages you already created.</span></span>

<span data-ttu-id="ffc04-122">在本教程中，你将创建用于插入数据库中的存储的过程`Student`和`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="ffc04-122">In this tutorial you'll create stored procedures in the database for inserting `Student` and `Instructor` entities.</span></span> <span data-ttu-id="ffc04-123">会将它们添加到数据模型中，并且你将指定实体框架应使用它们将添加`Student`和`Instructor`到数据库的实体。</span><span class="sxs-lookup"><span data-stu-id="ffc04-123">You'll add them to the data model, and you'll specify that the Entity Framework should use them for adding `Student` and `Instructor` entities to the database.</span></span> <span data-ttu-id="ffc04-124">此外将创建的存储的过程，可用于检索`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="ffc04-124">You'll also create a stored procedure that you can use to retrieve `Course` entities.</span></span>

## <a name="creating-stored-procedures-in-the-database"></a><span data-ttu-id="ffc04-125">在数据库中创建存储的过程</span><span class="sxs-lookup"><span data-stu-id="ffc04-125">Creating Stored Procedures in the Database</span></span>

<span data-ttu-id="ffc04-126">(如果您使用的*School.mdf*文件从下载本教程项目中，则可以跳过本部分因为已存在存储的过程。)</span><span class="sxs-lookup"><span data-stu-id="ffc04-126">(If you're using the *School.mdf* file from the project available for download with this tutorial, you can skip this section because the stored procedures already exist.)</span></span>

<span data-ttu-id="ffc04-127">在**服务器资源管理器**，展开*School.mdf*，右键单击**Stored Procedures**，然后选择**添加新存储过程**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-127">In **Server Explorer**, expand *School.mdf*, right-click **Stored Procedures**, and select **Add New Stored Procedure**.</span></span>

<span data-ttu-id="ffc04-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-128">[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)</span></span>

<span data-ttu-id="ffc04-129">复制以下 SQL 语句并将其粘贴到存储的过程窗口中，替换主干存储的过程。</span><span class="sxs-lookup"><span data-stu-id="ffc04-129">Copy the following SQL statements and paste them into the stored procedure window, replacing the skeleton stored procedure.</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

<span data-ttu-id="ffc04-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-130">[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)</span></span>

<span data-ttu-id="ffc04-131">`Student` 实体具有四个属性： `PersonID`， `LastName`， `FirstName`，和`EnrollmentDate`。</span><span class="sxs-lookup"><span data-stu-id="ffc04-131">`Student` entities have four properties: `PersonID`, `LastName`, `FirstName`, and `EnrollmentDate`.</span></span> <span data-ttu-id="ffc04-132">该数据库会自动生成的 ID 值和存储的过程接受其他三个参数。</span><span class="sxs-lookup"><span data-stu-id="ffc04-132">The database generates the ID value automatically, and the stored procedure accepts parameters for the other three.</span></span> <span data-ttu-id="ffc04-133">存储的过程返回的新行的记录键的值，以便实体框架可以跟踪的它在内存中保留的实体的版本中。</span><span class="sxs-lookup"><span data-stu-id="ffc04-133">The stored procedure returns the value of the new row's record key so that the Entity Framework can keep track of that in the version of the entity it keeps in memory.</span></span>

<span data-ttu-id="ffc04-134">保存并关闭存储的过程窗口中。</span><span class="sxs-lookup"><span data-stu-id="ffc04-134">Save and close the stored procedure window.</span></span>

<span data-ttu-id="ffc04-135">创建`InsertInstructor`中相同的方式，使用以下 SQL 语句的存储过程：</span><span class="sxs-lookup"><span data-stu-id="ffc04-135">Create an `InsertInstructor` stored procedure in the same manner, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

<span data-ttu-id="ffc04-136">创建`Update`存储过程`Student`和`Instructor`实体还。</span><span class="sxs-lookup"><span data-stu-id="ffc04-136">Create `Update` stored procedures for `Student` and `Instructor` entities also.</span></span> <span data-ttu-id="ffc04-137">(数据库中已经有`DeletePerson`存储过程，这将适用于两者`Instructor`和`Student`实体。)</span><span class="sxs-lookup"><span data-stu-id="ffc04-137">(The database already has a `DeletePerson` stored procedure which will work for both `Instructor` and `Student` entities.)</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

<span data-ttu-id="ffc04-138">在本教程中，您将映射所有三个函数-insert、 update 和 delete-每个实体类型。</span><span class="sxs-lookup"><span data-stu-id="ffc04-138">In this tutorial you'll map all three functions -- insert, update, and delete -- for each entity type.</span></span> <span data-ttu-id="ffc04-139">Entity Framework 版本 4，您可以将映射只是一个或两个函数到存储过程，而无需映射其他用户，有一个例外： 如果映射 update 函数，但不是删除函数，实体框架将引发异常时，尝试删除实体。</span><span class="sxs-lookup"><span data-stu-id="ffc04-139">The Entity Framework version 4 allows you to map just one or two of these functions to stored procedures without mapping the others, with one exception: if you map the update function but not the delete function, the Entity Framework will throw an exception when you attempt to delete an entity.</span></span> <span data-ttu-id="ffc04-140">在 Entity Framework 版本 3.5 中，您没有映射的存储的过程中如此大的灵活性： 如果您已映射到一个函数都需要映射所有三个。</span><span class="sxs-lookup"><span data-stu-id="ffc04-140">In the Entity Framework version 3.5, you did not have this much flexibility in mapping stored procedures: if you mapped one function you were required to map all three.</span></span>

<span data-ttu-id="ffc04-141">若要创建读取而不更新数据的存储的过程，创建一个选择所有`Course`实体，使用以下 SQL 语句：</span><span class="sxs-lookup"><span data-stu-id="ffc04-141">To create a stored procedure that reads rather than updates data, create one that selects all `Course` entities, using the following SQL statements:</span></span>

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a><span data-ttu-id="ffc04-142">将存储的过程添加到数据模型</span><span class="sxs-lookup"><span data-stu-id="ffc04-142">Adding the Stored Procedures to the Data Model</span></span>

<span data-ttu-id="ffc04-143">在数据库中，现在定义的存储的过程，但必须将它们添加到要向实体框架提供的数据模型。</span><span class="sxs-lookup"><span data-stu-id="ffc04-143">The stored procedures are now defined in the database, but they must be added to the data model to make them available to the Entity Framework.</span></span> <span data-ttu-id="ffc04-144">打开*SchoolModel.edmx*，右键单击设计图面上，然后选择**从数据库更新模型**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-144">Open *SchoolModel.edmx*, right-click the design surface, and select **Update Model from Database**.</span></span> <span data-ttu-id="ffc04-145">在**添加**选项卡**选择数据库对象**对话框中，展开**Stored Procedures**，选择新创建的存储的过程和`DeletePerson`存储过程，然后依次**完成**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-145">In the **Add** tab of the **Choose Your Database Objects** dialog box, expand **Stored Procedures**, select the newly created stored procedures and the `DeletePerson` stored procedure, and then click **Finish**.</span></span>

<span data-ttu-id="ffc04-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-146">[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)</span></span>

## <a name="mapping-the-stored-procedures"></a><span data-ttu-id="ffc04-147">映射存储的过程</span><span class="sxs-lookup"><span data-stu-id="ffc04-147">Mapping the Stored Procedures</span></span>

<span data-ttu-id="ffc04-148">在数据模型设计器中，右键单击`Student`实体，然后选择**存储过程映射**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-148">In the data model designer, right-click the `Student` entity and select **Stored Procedure Mapping**.</span></span>

<span data-ttu-id="ffc04-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-149">[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)</span></span>

<span data-ttu-id="ffc04-150">**映射详细信息**窗口随即出现，可以在其中指定实体框架应使用的插入、 更新和删除此类型的实体的存储的过程。</span><span class="sxs-lookup"><span data-stu-id="ffc04-150">The **Mapping Details** window appears, in which you can specify stored procedures that the Entity Framework should use for inserting, updating, and deleting entities of this type.</span></span>

<span data-ttu-id="ffc04-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-151">[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)</span></span>

<span data-ttu-id="ffc04-152">设置**插入**函数来**InsertStudent**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-152">Set the **Insert** function to **InsertStudent**.</span></span> <span data-ttu-id="ffc04-153">窗口显示的存储的过程参数，其中每个必须映射到实体属性的列表。</span><span class="sxs-lookup"><span data-stu-id="ffc04-153">The window shows a list of stored procedure parameters, each of which must be mapped to an entity property.</span></span> <span data-ttu-id="ffc04-154">原因是名称相同，两个都自动映射。</span><span class="sxs-lookup"><span data-stu-id="ffc04-154">Two of these are mapped automatically because the names are the same.</span></span> <span data-ttu-id="ffc04-155">不存在名为实体属性`FirstName`，因此必须手动选择`FirstMidName`从下拉列表，显示可用的实体属性。</span><span class="sxs-lookup"><span data-stu-id="ffc04-155">There's no entity property named `FirstName`, so you must manually select `FirstMidName` from a drop-down list that shows available entity properties.</span></span> <span data-ttu-id="ffc04-156">(这是因为更改的名称`FirstName`属性设置为`FirstMidName`中的第一个教程。)</span><span class="sxs-lookup"><span data-stu-id="ffc04-156">(This is because you changed the name of the `FirstName` property to `FirstMidName` in the first tutorial.)</span></span>

<span data-ttu-id="ffc04-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-157">[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)</span></span>

<span data-ttu-id="ffc04-158">在同一**映射详细信息**窗口中，映射`Update`函数来`UpdateStudent`存储过程 (请确保指定`FirstMidName`的参数值作为`FirstName`，如你对`Insert`存储过程） 和`Delete`函数来`DeletePerson`存储过程。</span><span class="sxs-lookup"><span data-stu-id="ffc04-158">In the same **Mapping Details** window, map the `Update` function to the `UpdateStudent` stored procedure (make sure you specify `FirstMidName` as the parameter value for `FirstName`, as you did for the `Insert` stored procedure) and the `Delete` function to the `DeletePerson` stored procedure.</span></span>

<span data-ttu-id="ffc04-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-159">[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)</span></span>

<span data-ttu-id="ffc04-160">请遵循相同的过程来映射 insert、 update 和 delete 存储过程用于为讲师`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="ffc04-160">Follow the same procedure to map the insert, update, and delete stored procedures for instructors to the `Instructor` entity.</span></span>

<span data-ttu-id="ffc04-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-161">[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)</span></span>

<span data-ttu-id="ffc04-162">对于读取而不是更新数据的存储过程，您使用**模型浏览器**窗口，以将存储的过程映射到实体类型将其返回。</span><span class="sxs-lookup"><span data-stu-id="ffc04-162">For stored procedures that read rather than update data, you use the **Model Browser** window to map the stored procedure to the entity type it returns.</span></span> <span data-ttu-id="ffc04-163">在数据模型设计器中，右键单击设计图面并选择**模型浏览器**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-163">In the data model designer, right-click the design surface and select **Model Browser**.</span></span> <span data-ttu-id="ffc04-164">打开**SchoolModel.Store**节点，然后打开**存储过程**节点。</span><span class="sxs-lookup"><span data-stu-id="ffc04-164">Open the **SchoolModel.Store** node and then open the **Stored Procedures** node.</span></span> <span data-ttu-id="ffc04-165">然后右键单击`GetCourses`存储过程，然后选择**添加函数导入**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-165">Then right-click the `GetCourses` stored procedure and select **Add Function Import**.</span></span>

<span data-ttu-id="ffc04-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-166">[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)</span></span>

<span data-ttu-id="ffc04-167">在中**添加函数导入**对话框中的**返回集合的**选择**实体**，然后选择`Course`作为实体类型返回。</span><span class="sxs-lookup"><span data-stu-id="ffc04-167">In the **Add Function Import** dialog box, under **Returns a Collection Of** select **Entities**, and then select `Course` as the entity type returned.</span></span> <span data-ttu-id="ffc04-168">完成后，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="ffc04-168">When you're done, click **OK**.</span></span> <span data-ttu-id="ffc04-169">保存并关闭 *.edmx*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc04-169">Save and close the *.edmx* file.</span></span>

<span data-ttu-id="ffc04-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-170">[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)</span></span>

## <a name="using-insert-update-and-delete-stored-procedures"></a><span data-ttu-id="ffc04-171">使用 Insert、 Update 和 Delete 存储的过程</span><span class="sxs-lookup"><span data-stu-id="ffc04-171">Using Insert, Update, and Delete Stored Procedures</span></span>

<span data-ttu-id="ffc04-172">存储的过程以插入、 更新和删除数据后已添加到数据模型和映射到相应的实体会自动由实体框架使用。</span><span class="sxs-lookup"><span data-stu-id="ffc04-172">Stored procedures to insert, update, and delete data are used by the Entity Framework automatically after you've added them to the data model and mapped them to the appropriate entities.</span></span> <span data-ttu-id="ffc04-173">现在可以运行*StudentsAdd.aspx*页上，并每次创建新的学生，将使用实体框架`InsertStudent`存储过程来添加新行`Student`表。</span><span class="sxs-lookup"><span data-stu-id="ffc04-173">You can now run the *StudentsAdd.aspx* page, and every time you create a new student, the Entity Framework will use the `InsertStudent` stored procedure to add the new row to the `Student` table.</span></span>

<span data-ttu-id="ffc04-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-174">[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)</span></span>

<span data-ttu-id="ffc04-175">运行*Students.aspx*页和新的学生将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="ffc04-175">Run the *Students.aspx* page and the new student appears in the list.</span></span>

<span data-ttu-id="ffc04-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-176">[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)</span></span>

<span data-ttu-id="ffc04-177">更改名称，以验证更新函数工作，然后再删除该学生验证的删除函数正常工作。</span><span class="sxs-lookup"><span data-stu-id="ffc04-177">Change the name to verify that the update function works, and then delete the student to verify that the delete function works.</span></span>

<span data-ttu-id="ffc04-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="ffc04-178">[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)</span></span>

## <a name="using-select-stored-procedures"></a><span data-ttu-id="ffc04-179">使用选择的存储的过程</span><span class="sxs-lookup"><span data-stu-id="ffc04-179">Using Select Stored Procedures</span></span>

<span data-ttu-id="ffc04-180">实体框架不会自动运行存储的过程如`GetCourses`，并不能将其用于`EntityDataSource`控件。</span><span class="sxs-lookup"><span data-stu-id="ffc04-180">The Entity Framework does not automatically run stored procedures such as `GetCourses`, and you cannot use them with the `EntityDataSource` control.</span></span> <span data-ttu-id="ffc04-181">若要使用它们，它们从代码调用。</span><span class="sxs-lookup"><span data-stu-id="ffc04-181">To use them, you call them from code.</span></span>

<span data-ttu-id="ffc04-182">打开*InstructorsCourses.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc04-182">Open the *InstructorsCourses.aspx.cs* file.</span></span> <span data-ttu-id="ffc04-183">`PopulateDropDownLists`方法使用 LINQ 到 Entities 查询来检索所有 course 实体，以便它可以循环访问列表并确定的哪些分配给讲师，哪些是未分配：</span><span class="sxs-lookup"><span data-stu-id="ffc04-183">The `PopulateDropDownLists` method uses a LINQ-to-Entities query to retrieve all course entities so that it can loop through the list and determine which ones an instructor is assigned to and which ones are unassigned:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

<span data-ttu-id="ffc04-184">将此替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="ffc04-184">Replace this with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

<span data-ttu-id="ffc04-185">页面现在使用`GetCourses`存储过程来检索所有课程的列表。</span><span class="sxs-lookup"><span data-stu-id="ffc04-185">The page now uses the `GetCourses` stored procedure to retrieve the list of all courses.</span></span> <span data-ttu-id="ffc04-186">运行页以验证它像以前一样工作。</span><span class="sxs-lookup"><span data-stu-id="ffc04-186">Run the page to verify that it works as it did before.</span></span>

<span data-ttu-id="ffc04-187">(使用与这些实体，具体取决于相关的数据，存储过程来检索的实体的导航属性可能不自动填充`ObjectContext`默认设置。</span><span class="sxs-lookup"><span data-stu-id="ffc04-187">(Navigation properties of entities retrieved by a stored procedure might not be automatically populated with the data related to those entities, depending on `ObjectContext` default settings.</span></span> <span data-ttu-id="ffc04-188">有关详细信息，请参阅[加载相关对象](https://msdn.microsoft.com/library/bb896272.aspx)MSDN 库中。)</span><span class="sxs-lookup"><span data-stu-id="ffc04-188">For more information, see [Loading Related Objects](https://msdn.microsoft.com/library/bb896272.aspx) in the MSDN Library.)</span></span>

<span data-ttu-id="ffc04-189">在下一步的教程中，您将了解如何使用动态数据功能来轻松地计划和测试数据格式设置和验证规则。</span><span class="sxs-lookup"><span data-stu-id="ffc04-189">In the next tutorial, you'll learn how to use Dynamic Data functionality to make it easier to program and test data formatting and validation rules.</span></span> <span data-ttu-id="ffc04-190">而不是指定每个网页规则，如数据格式字符串和字段是必填上，可以在数据模型元数据中指定此类规则，这些自动应用在每一页上。</span><span class="sxs-lookup"><span data-stu-id="ffc04-190">Instead of specifying on each web page rules such as data format strings and whether or not a field is required, you can specify such rules in data model metadata and they're automatically applied on every page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ffc04-191">[上一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="ffc04-191">[Previous](the-entity-framework-and-aspnet-getting-started-part-6.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-8.md)</span></span>
