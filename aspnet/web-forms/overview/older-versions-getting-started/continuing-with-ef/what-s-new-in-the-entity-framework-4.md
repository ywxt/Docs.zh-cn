---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 什么是实体框架 4.0 中的新增功能 |Microsoft 文档
author: tdykstra
description: 本教程系列上的 Contoso 大学 web 应用程序创建的 Getting Started with 实体 Framework 4.0 教程系列生成。 I...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 04444ce98fa60045cf617a6c518dd55677258148
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889181"
---
<a name="whats-new-in-the-entity-framework-40"></a><span data-ttu-id="adc85-104">什么是实体框架 4.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="adc85-104">What's New in the Entity Framework 4.0</span></span>
====================
<span data-ttu-id="adc85-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="adc85-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="adc85-106">本教程系列上的 Contoso 大学 web 应用程序创建的生成[Getting Started with 实体框架](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程系列。</span><span class="sxs-lookup"><span data-stu-id="adc85-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) tutorial series.</span></span> <span data-ttu-id="adc85-107">如果未完成前面的教程，作为一个起始点本教程，你可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，你应已创建。</span><span class="sxs-lookup"><span data-stu-id="adc85-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="adc85-108">你还可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)，它由完整教程系列创建。</span><span class="sxs-lookup"><span data-stu-id="adc85-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="adc85-109">如果你有疑问的教程，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="adc85-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="adc85-110">在前面的教程中，您将了解一些方法用于最大程度地使用实体框架的 web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="adc85-110">In the previous tutorial you saw some methods for maximizing the performance of a web application that uses the Entity Framework.</span></span> <span data-ttu-id="adc85-111">本教程中查看的一些最重要新功能在版本 4 的实体框架中，而且它链接到提供的所有新功能的更完整介绍的资源。</span><span class="sxs-lookup"><span data-stu-id="adc85-111">This tutorial reviews some of the most important new features in version 4 of the Entity Framework, and it links to resources that provide a more complete introduction to all of the new features.</span></span> <span data-ttu-id="adc85-112">在本教程中突出显示的功能包括：</span><span class="sxs-lookup"><span data-stu-id="adc85-112">The features highlighted in this tutorial include the following:</span></span>

- <span data-ttu-id="adc85-113">外键关联。</span><span class="sxs-lookup"><span data-stu-id="adc85-113">Foreign-key associations.</span></span>
- <span data-ttu-id="adc85-114">执行用户定义的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="adc85-114">Executing user-defined SQL commands.</span></span>
- <span data-ttu-id="adc85-115">模型优先开发。</span><span class="sxs-lookup"><span data-stu-id="adc85-115">Model-first development.</span></span>
- <span data-ttu-id="adc85-116">POCO 支持。</span><span class="sxs-lookup"><span data-stu-id="adc85-116">POCO support.</span></span>

<span data-ttu-id="adc85-117">此外，本教程将简要介绍*代码优先的开发*，即将推出的实体框架的下一个版本中的功能。</span><span class="sxs-lookup"><span data-stu-id="adc85-117">In addition, the tutorial will briefly introduce *code-first development*, a feature that's coming in the next release of the Entity Framework.</span></span>

<span data-ttu-id="adc85-118">若要开始本教程，请启动 Visual Studio 并打开与你共事中以前的教程，Contoso 大学 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="adc85-118">To start the tutorial, start Visual Studio and open the Contoso University web application that you were working with in the previous tutorial.</span></span>

## <a name="foreign-key-associations"></a><span data-ttu-id="adc85-119">外键关联</span><span class="sxs-lookup"><span data-stu-id="adc85-119">Foreign-Key Associations</span></span>

<span data-ttu-id="adc85-120">包含实体框架版本 3.5 的导航属性，但它没有数据模型中包括外键属性。</span><span class="sxs-lookup"><span data-stu-id="adc85-120">Version 3.5 of the Entity Framework included navigation properties, but it didn't include foreign-key properties in the data model.</span></span> <span data-ttu-id="adc85-121">例如，`CourseID`和`StudentID`列`StudentGrade`表将省略从`StudentGrade`实体。</span><span class="sxs-lookup"><span data-stu-id="adc85-121">For example, the `CourseID` and `StudentID` columns of the `StudentGrade` table would be omitted from the `StudentGrade` entity.</span></span>

<span data-ttu-id="adc85-122">[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-122">[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)</span></span>

<span data-ttu-id="adc85-123">此方法的原因时，严格地说外, 键是物理实现详细信息且不属于概念数据模型中。</span><span class="sxs-lookup"><span data-stu-id="adc85-123">The reason for this approach was that, strictly speaking, foreign keys are a physical implementation detail and don't belong in a conceptual data model.</span></span> <span data-ttu-id="adc85-124">但是，在实践中，通常很容易地使用代码中的实体时可以直接访问的外键。</span><span class="sxs-lookup"><span data-stu-id="adc85-124">However, as a practical matter, it's often easier to work with entities in code when you have direct access to the foreign keys.</span></span>

<span data-ttu-id="adc85-125">为数据模型中的方式外键的一个示例可以简化你的代码，请考虑如何你将获得了对代码*DepartmentsAdd.aspx*页，不需要它们。</span><span class="sxs-lookup"><span data-stu-id="adc85-125">For an example of how foreign keys in the data model can simplify your code, consider how you would have had to code the *DepartmentsAdd.aspx* page without them.</span></span> <span data-ttu-id="adc85-126">在`Department`实体，`Administrator`属性是对应的外键`PersonID`中`Person`实体。</span><span class="sxs-lookup"><span data-stu-id="adc85-126">In the `Department` entity, the `Administrator` property is a foreign key that corresponds to `PersonID` in the `Person` entity.</span></span> <span data-ttu-id="adc85-127">为了建立新部门和其管理员之间的关联，你所要做已设置的值`Administrator`中的属性`ItemInserting`的数据绑定控件的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="adc85-127">In order to establish the association between a new department and its administrator, all you had to do was set the value for the `Administrator` property in the `ItemInserting` event handler of the databound control:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

<span data-ttu-id="adc85-128">如果数据模型中的外键，没有将处理`Inserting`而不是数据源控件的事件`ItemInserting`的数据绑定控件，以获取对该实体本身的引用，该实体添加到实体集之前的事件。</span><span class="sxs-lookup"><span data-stu-id="adc85-128">Without foreign keys in the data model, you'd handle the `Inserting` event of the data source control instead of the `ItemInserting` event of the databound control, in order to get a reference to the entity itself before the entity is added to the entity set.</span></span> <span data-ttu-id="adc85-129">该引用后，你建立使用类似于下面的示例中的代码的关联：</span><span class="sxs-lookup"><span data-stu-id="adc85-129">When you have that reference, you establish the association using code like that in the following examples:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

<span data-ttu-id="adc85-130">在实体框架团队中可以看到[在外键关联上的博客文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)，有其他情况下，在代码复杂性方面的差异是大得多。</span><span class="sxs-lookup"><span data-stu-id="adc85-130">As you can see in the Entity Framework team's [blog post on Foreign Key associations](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), there are other cases where the difference in code complexity is much greater.</span></span> <span data-ttu-id="adc85-131">若要满足的要求的那些人员更愿意接受更简易的代码为概念数据模型中的实现详细信息，实体框架将会提供数据模型中包括外键的选项。</span><span class="sxs-lookup"><span data-stu-id="adc85-131">To meet the needs of those who prefer to live with implementation details in the conceptual data model for the sake of simpler code, the Entity Framework now gives you the option of including foreign keys in the data model.</span></span>

<span data-ttu-id="adc85-132">在实体框架术语中，如果数据模型中包括外键您正使用*外键关联*，并且如果你正在使用的外键中排除*独立关联*。</span><span class="sxs-lookup"><span data-stu-id="adc85-132">In Entity Framework terminology, if you include foreign keys in the data model you're using *foreign key associations*, and if you exclude foreign keys you're using *independent associations*.</span></span>

## <a name="executing-user-defined-sql-commands"></a><span data-ttu-id="adc85-133">执行用户定义的 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="adc85-133">Executing User-Defined SQL Commands</span></span>

<span data-ttu-id="adc85-134">在早期版本的实体框架中，没有简单方法来动态创建你自己的 SQL 命令，然后运行这些。</span><span class="sxs-lookup"><span data-stu-id="adc85-134">In earlier versions of the Entity Framework, there was no easy way to create your own SQL commands on the fly and run them.</span></span> <span data-ttu-id="adc85-135">实体框架动态生成为你的 SQL 命令，或者您必须创建存储的过程并将其作为函数导入。</span><span class="sxs-lookup"><span data-stu-id="adc85-135">Either the Entity Framework dynamically generated SQL commands for you, or you had to create a stored procedure and import it as a function.</span></span> <span data-ttu-id="adc85-136">版本 4 添加`ExecuteStoreQuery`和`ExecuteStoreCommand`方法`ObjectContext`使其更轻松地任何查询将直接传递到数据库的类。</span><span class="sxs-lookup"><span data-stu-id="adc85-136">Version 4 adds `ExecuteStoreQuery` and `ExecuteStoreCommand` methods the `ObjectContext` class that make it easier for you to pass any query directly to the database.</span></span>

<span data-ttu-id="adc85-137">假设 Contoso 大学管理员想要能够对数据库中执行大容量更改，而无需经历创建存储的过程和导入数据模型的过程。</span><span class="sxs-lookup"><span data-stu-id="adc85-137">Suppose Contoso University administrators want to be able to perform bulk changes in the database without having to go through the process of creating a stored procedure and importing it into the data model.</span></span> <span data-ttu-id="adc85-138">页，以便他们更改用于在数据库中的所有课程的信用额度数可以是其第一个请求。</span><span class="sxs-lookup"><span data-stu-id="adc85-138">Their first request is for a page that lets them change the number of credits for all courses in the database.</span></span> <span data-ttu-id="adc85-139">他们想要能够输入要使用的值相乘的数字在网页上，每个`Course`行的`Credits`列。</span><span class="sxs-lookup"><span data-stu-id="adc85-139">On the web page, they want to be able to enter a number to use to multiply the value of every `Course` row's `Credits` column.</span></span>

<span data-ttu-id="adc85-140">创建新的页使用*Site.Master*母版页并将其命名*UpdateCredits.aspx*。</span><span class="sxs-lookup"><span data-stu-id="adc85-140">Create a new page that uses the *Site.Master* master page and name it *UpdateCredits.aspx*.</span></span> <span data-ttu-id="adc85-141">然后添加以下标记到`Content`控件名为`Content2`:</span><span class="sxs-lookup"><span data-stu-id="adc85-141">Then add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

<span data-ttu-id="adc85-142">此标记将创建`TextBox`控制用户可以在其中输入乘数值，`Button`控件若要执行该命令，请单击和`Label`，该值指示受影响的行数的控件。</span><span class="sxs-lookup"><span data-stu-id="adc85-142">This markup creates a `TextBox` control in which the user can enter the multiplier value, a `Button` control to click in order to execute the command, and a `Label` control for indicating the number of rows affected.</span></span>

<span data-ttu-id="adc85-143">打开*UpdateCredits.aspx.cs*，并添加以下`using`语句和为按钮的处理程序`Click`事件：</span><span class="sxs-lookup"><span data-stu-id="adc85-143">Open *UpdateCredits.aspx.cs*, and add the following `using` statement and a handler for the button's `Click` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

<span data-ttu-id="adc85-144">此代码执行 SQL`Update`命令在文本框中使用的值，并使用标签来显示受影响的行数。</span><span class="sxs-lookup"><span data-stu-id="adc85-144">This code executes the SQL `Update` command using the value in the text box and uses the label to display the number of rows affected.</span></span> <span data-ttu-id="adc85-145">运行页面之前，运行*Courses.aspx*页后，可以获取一些数据的"之前"图片。</span><span class="sxs-lookup"><span data-stu-id="adc85-145">Before you run the page, run the *Courses.aspx* page to get a "before" picture of some data.</span></span>

<span data-ttu-id="adc85-146">[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-146">[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)</span></span>

<span data-ttu-id="adc85-147">运行*UpdateCredits.aspx*，作为乘数中，输入"10"，然后单击**执行**。</span><span class="sxs-lookup"><span data-stu-id="adc85-147">Run *UpdateCredits.aspx*, enter "10" as the multiplier, and then click **Execute**.</span></span>

<span data-ttu-id="adc85-148">[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-148">[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)</span></span>

<span data-ttu-id="adc85-149">运行*Courses.aspx*页上再次查看已更改的数据。</span><span class="sxs-lookup"><span data-stu-id="adc85-149">Run the *Courses.aspx* page again to see the changed data.</span></span>

<span data-ttu-id="adc85-150">[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-150">[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)</span></span>

<span data-ttu-id="adc85-151">(如果你想要在将信用额度数设置回其原始值， *UpdateCredits.aspx.cs*更改`Credits * {0}`到`Credits / {0}`，然后重新运行页上，输入 10 作为除数。)</span><span class="sxs-lookup"><span data-stu-id="adc85-151">(If you want to set the number of credits back to their original values, in *UpdateCredits.aspx.cs* change `Credits * {0}` to `Credits / {0}` and re-run the page, entering 10 as the divisor.)</span></span>

<span data-ttu-id="adc85-152">有关执行查询，以在代码中定义的详细信息，请参阅[如何： 直接执行命令针对数据源](https://msdn.microsoft.com/library/ee358769.aspx)。</span><span class="sxs-lookup"><span data-stu-id="adc85-152">For more information about executing queries that you define in code, see [How to: Directly Execute Commands Against the Data Source](https://msdn.microsoft.com/library/ee358769.aspx).</span></span>

## <a name="model-first-development"></a><span data-ttu-id="adc85-153">模型优先开发</span><span class="sxs-lookup"><span data-stu-id="adc85-153">Model-First Development</span></span>

<span data-ttu-id="adc85-154">这些演练中，你首先创建数据库，然后生成基于数据库结构的数据模型。</span><span class="sxs-lookup"><span data-stu-id="adc85-154">In these walkthroughs you created the database first and then generated the data model based on the database structure.</span></span> <span data-ttu-id="adc85-155">Entity Framework 4 中你可以改为启动与数据模型，并生成基于数据模型结构的数据库。</span><span class="sxs-lookup"><span data-stu-id="adc85-155">In the Entity Framework 4 you can start with the data model instead and generate the database based on the data model structure.</span></span> <span data-ttu-id="adc85-156">如果你要创建应用程序为其数据库尚不存在，模型为先的方法使你可以创建实体和关系从概念上讲对应用程序，并不需考虑如何物理实现详细信息的意义.</span><span class="sxs-lookup"><span data-stu-id="adc85-156">If you're creating an application for which the database doesn't already exist, the model-first approach enables you to create entities and relationships that make sense conceptually for the application, while not worrying about physical implementation details.</span></span> <span data-ttu-id="adc85-157">（情况都是如此只能通过初始阶段的开发，但是。</span><span class="sxs-lookup"><span data-stu-id="adc85-157">(This remains true only through the initial stages of development, however.</span></span> <span data-ttu-id="adc85-158">最终将创建和中，必须将具有生产数据的数据库，重新创建它从模型将不再是实际可行的;此时，你将准备回数据库为先的方法。）</span><span class="sxs-lookup"><span data-stu-id="adc85-158">Eventually the database will be created and will have production data in it, and recreating it from the model will no longer be practical; at that point you'll be back to the database-first approach.)</span></span>

<span data-ttu-id="adc85-159">在本教程的此部分中，你将创建简单的数据模型，并从它生成数据库。</span><span class="sxs-lookup"><span data-stu-id="adc85-159">In this section of the tutorial, you'll create a simple data model and generate the database from it.</span></span>

<span data-ttu-id="adc85-160">在**解决方案资源管理器**，右键单击*DAL*文件夹，然后选择**添加新项**。</span><span class="sxs-lookup"><span data-stu-id="adc85-160">In **Solution Explorer**, right-click the *DAL* folder and select **Add New Item**.</span></span> <span data-ttu-id="adc85-161">在**添加新项**对话框中，在**已安装的模板**选择**数据**，然后选择**ADO.NET 实体数据模型**模板.</span><span class="sxs-lookup"><span data-stu-id="adc85-161">In the **Add New Item** dialog box, under **Installed Templates** select **Data** and then select the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="adc85-162">将新文件命名*AlumniAssociationModel.edmx*单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="adc85-162">Name the new file *AlumniAssociationModel.edmx* and click **Add**.</span></span>

<span data-ttu-id="adc85-163">[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-163">[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)</span></span>

<span data-ttu-id="adc85-164">这将启动实体数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="adc85-164">This launches the Entity Data Model Wizard.</span></span> <span data-ttu-id="adc85-165">在**选择模型内容**步骤中，选择**空模型**，然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="adc85-165">In the **Choose Model Contents** step, select **Empty Model** and then click **Finish**.</span></span>

<span data-ttu-id="adc85-166">[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-166">[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)</span></span>

<span data-ttu-id="adc85-167">**Entity Data Model Designer**打开与空白设计图面。</span><span class="sxs-lookup"><span data-stu-id="adc85-167">The **Entity Data Model Designer** opens with a blank design surface.</span></span> <span data-ttu-id="adc85-168">拖动**实体**项从**工具箱**拖到设计图面。</span><span class="sxs-lookup"><span data-stu-id="adc85-168">Drag an **Entity** item from the **Toolbox** onto the design surface.</span></span>

<span data-ttu-id="adc85-169">[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-169">[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)</span></span>

<span data-ttu-id="adc85-170">更改从实体名称`Entity1`到`Alumnus`，更改`Id`属性名称设置为`AlumnusId`，并添加名为的新标量属性`Name`。</span><span class="sxs-lookup"><span data-stu-id="adc85-170">Change the entity name from `Entity1` to `Alumnus`, change the `Id` property name to `AlumnusId`, and add a new scalar property named `Name`.</span></span> <span data-ttu-id="adc85-171">若要将新属性添加你可以更改的名称后按 Enter`Id`列，或者右键单击该实体，然后选择**添加标量属性**。</span><span class="sxs-lookup"><span data-stu-id="adc85-171">To add new properties you can press Enter after changing the name of the `Id` column, or right-click the entity and select **Add Scalar Property**.</span></span> <span data-ttu-id="adc85-172">新属性的默认类型是`String`，这样做也可以为此简单演示中，但这是当然你可以更改等中的数据类型**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="adc85-172">The default type for new properties is `String`, which is fine for this simple demonstration, but of course you can change things like data type in the **Properties** window.</span></span>

<span data-ttu-id="adc85-173">创建相同的方式的另一个实体并将其命名`Donation`。</span><span class="sxs-lookup"><span data-stu-id="adc85-173">Create another entity the same way and name it `Donation`.</span></span> <span data-ttu-id="adc85-174">更改`Id`属性`DonationId`并添加名为的标量属性`DateAndAmount`。</span><span class="sxs-lookup"><span data-stu-id="adc85-174">Change the `Id` property to `DonationId` and add a scalar property named `DateAndAmount`.</span></span>

<span data-ttu-id="adc85-175">[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-175">[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)</span></span>

<span data-ttu-id="adc85-176">若要添加这两个实体之间的关联，右键单击`Alumnus`实体中，选择**添加**，然后选择**关联**。</span><span class="sxs-lookup"><span data-stu-id="adc85-176">To add an association between these two entities, right-click the `Alumnus` entity, select **Add**, and then select **Association**.</span></span>

<span data-ttu-id="adc85-177">[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-177">[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)</span></span>

<span data-ttu-id="adc85-178">中的默认值**添加关联**对话框是所需 （一到多包括导航属性，包括外键），因此只需单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="adc85-178">The default values in the **Add Association** dialog box are what you want (one-to-many, include navigation properties, include foreign keys), so just click **OK**.</span></span>

<span data-ttu-id="adc85-179">[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-179">[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)</span></span>

<span data-ttu-id="adc85-180">设计器添加一条关联连线和外键属性。</span><span class="sxs-lookup"><span data-stu-id="adc85-180">The designer adds an association line and a foreign-key property.</span></span>

<span data-ttu-id="adc85-181">[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-181">[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)</span></span>

<span data-ttu-id="adc85-182">现在你已准备好创建数据库。</span><span class="sxs-lookup"><span data-stu-id="adc85-182">Now you're ready to create the database.</span></span> <span data-ttu-id="adc85-183">右键单击设计图面并选择**根据模型生成数据库**。</span><span class="sxs-lookup"><span data-stu-id="adc85-183">Right-click the design surface and select **Generate Database from Model**.</span></span>

<span data-ttu-id="adc85-184">[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-184">[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)</span></span>

<span data-ttu-id="adc85-185">这将启动生成数据库向导。</span><span class="sxs-lookup"><span data-stu-id="adc85-185">This launches the Generate Database Wizard.</span></span> <span data-ttu-id="adc85-186">（如果您看到指示实体未映射的警告，则可以忽略这些暂时。）</span><span class="sxs-lookup"><span data-stu-id="adc85-186">(If you see warnings that indicate that the entities aren't mapped, you can ignore those for the time being.)</span></span>

<span data-ttu-id="adc85-187">在**选择你的数据连接**步骤中，单击**新连接**。</span><span class="sxs-lookup"><span data-stu-id="adc85-187">In the **Choose Your Data Connection** step, click **New Connection**.</span></span>

<span data-ttu-id="adc85-188">[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-188">[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)</span></span>

<span data-ttu-id="adc85-189">在**连接属性**对话框中，选择 SQL Server Express 的本地实例并将数据库命名`AlumniAsssociation`。</span><span class="sxs-lookup"><span data-stu-id="adc85-189">In the **Connection Properties** dialog box, select the local SQL Server Express instance and name the database `AlumniAsssociation`.</span></span>

<span data-ttu-id="adc85-190">[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-190">[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)</span></span>

<span data-ttu-id="adc85-191">单击**是**当系统询问你是否是否想要创建数据库。</span><span class="sxs-lookup"><span data-stu-id="adc85-191">Click **Yes** when you're asked if you want to create the database.</span></span> <span data-ttu-id="adc85-192">当**选择你的数据连接**再次显示步骤，请单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="adc85-192">When the **Choose Your Data Connection** step is displayed again, click **Next**.</span></span>

<span data-ttu-id="adc85-193">在**摘要和设置**步骤中，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="adc85-193">In the **Summary and Settings** step, click **Finish**.</span></span>

<span data-ttu-id="adc85-194">[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-194">[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)</span></span>

<span data-ttu-id="adc85-195">A *.sql*将创建与数据定义语言 (DDL) 命令的文件，但尚未运行命令。</span><span class="sxs-lookup"><span data-stu-id="adc85-195">A *.sql* file with the data definition language (DDL) commands is created, but the commands haven't been run yet.</span></span>

<span data-ttu-id="adc85-196">[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-196">[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)</span></span>

<span data-ttu-id="adc85-197">使用一种工具，如**SQL Server Management Studio**来运行脚本并创建表，因为可能在执行了你在创建时`School`数据库[入门教程系列中的第一个教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="adc85-197">Use a tool such as **SQL Server Management Studio** to run the script and create the tables, as you might have done when you created the `School` database for [the first tutorial in the Getting Started tutorial series](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span></span> <span data-ttu-id="adc85-198">（除非你下载此数据库）。</span><span class="sxs-lookup"><span data-stu-id="adc85-198">(Unless you downloaded the database.)</span></span>

<span data-ttu-id="adc85-199">你现在可以使用`AlumniAssociation`数据模型中你的 web 页你所用的相同方式`School`模型。</span><span class="sxs-lookup"><span data-stu-id="adc85-199">You can now use the `AlumniAssociation` data model in your web pages the same way you've been using the `School` model.</span></span> <span data-ttu-id="adc85-200">若要试用此项，对表中添加一些数据，并创建网页上显示的数据。</span><span class="sxs-lookup"><span data-stu-id="adc85-200">To try this out, add some data to the tables and create a web page that displays the data.</span></span>

<span data-ttu-id="adc85-201">使用**服务器资源管理器**，添加以下行到`Alumnus`和`Donation`表。</span><span class="sxs-lookup"><span data-stu-id="adc85-201">Using **Server Explorer**, add the following rows to the `Alumnus` and `Donation` tables.</span></span>

<span data-ttu-id="adc85-202">[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-202">[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)</span></span>

<span data-ttu-id="adc85-203">创建一个名为的新 web 页*Alumni.aspx*使用*Site.Master*母版页。</span><span class="sxs-lookup"><span data-stu-id="adc85-203">Create a new web page named *Alumni.aspx* that uses the *Site.Master* master page.</span></span> <span data-ttu-id="adc85-204">添加到以下标记`Content`控件名为`Content2`:</span><span class="sxs-lookup"><span data-stu-id="adc85-204">Add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

<span data-ttu-id="adc85-205">此标记将创建嵌套`GridView`控制，外部的一个，若要显示校友名称，内部的一个，以显示捐赠日期和金额。</span><span class="sxs-lookup"><span data-stu-id="adc85-205">This markup creates nested `GridView` controls, the outer one to display alumni names and the inner one to display donation dates and amounts.</span></span>

<span data-ttu-id="adc85-206">打开*Alumni.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="adc85-206">Open *Alumni.aspx.cs*.</span></span> <span data-ttu-id="adc85-207">添加`using`语句的数据访问层和的处理程序外部`GridView`控件的`RowDataBound`事件：</span><span class="sxs-lookup"><span data-stu-id="adc85-207">Add a `using` statement for the data access layer and a handler for the outer `GridView` control's `RowDataBound` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

<span data-ttu-id="adc85-208">此代码 databinds 内部`GridView`控制使用`Donations`的当前行的导航属性`Alumnus`实体。</span><span class="sxs-lookup"><span data-stu-id="adc85-208">This code databinds the inner `GridView` control using the `Donations` navigation property of the current row's `Alumnus` entity.</span></span>

<span data-ttu-id="adc85-209">运行页面。</span><span class="sxs-lookup"><span data-stu-id="adc85-209">Run the page.</span></span>

<span data-ttu-id="adc85-210">[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="adc85-210">[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)</span></span>

<span data-ttu-id="adc85-211">(注意： 此页包含在可下载的项目中，但若要使它起作用，您必须创建数据库在本地 SQL Server Express 实例; 数据库中不包含作为 *.mdf*文件中*应用\_数据*文件夹。)</span><span class="sxs-lookup"><span data-stu-id="adc85-211">(Note: This page is included in the downloadable project, but to make it work you must create the database in your local SQL Server Express instance; the database isn't included as an *.mdf* file in the *App\_Data* folder.)</span></span>

<span data-ttu-id="adc85-212">有关使用实体框架的第一个模型的功能的详细信息，请参阅[实体 Framework 4 中的模型的第一个](https://msdn.microsoft.com/data/ff830362.aspx)。</span><span class="sxs-lookup"><span data-stu-id="adc85-212">For more information about using the model-first feature of the Entity Framework, see [Model-First in the Entity Framework 4](https://msdn.microsoft.com/data/ff830362.aspx).</span></span>

## <a name="poco-support"></a><span data-ttu-id="adc85-213">POCO 支持</span><span class="sxs-lookup"><span data-stu-id="adc85-213">POCO Support</span></span>

<span data-ttu-id="adc85-214">当使用域驱动的设计方法时，您设计数据类表示数据和与业务领域相关的行为。</span><span class="sxs-lookup"><span data-stu-id="adc85-214">When you use domain-driven design methodology, you design data classes that represent data and behavior that's relevant to the business domain.</span></span> <span data-ttu-id="adc85-215">这些类就能独立于任何特定的技术，用于存储 （保留） 数据;换而言之，应将它们*持久性未知*。</span><span class="sxs-lookup"><span data-stu-id="adc85-215">These classes should be independent of any specific technology used to store (persist) the data; in other words, they should be *persistence ignorant*.</span></span> <span data-ttu-id="adc85-216">此外可持久性无感知可以使一个类简单到单元测试，因为单元测试项目可以使用任何持久性技术是最方便的测试。</span><span class="sxs-lookup"><span data-stu-id="adc85-216">Persistence ignorance can also make a class easier to unit test because the unit test project can use whatever persistence technology is most convenient for testing.</span></span> <span data-ttu-id="adc85-217">早期版本的实体框架提供对持久性无感知的支持有限，因为实体类必须继承自`EntityObject`类，因此包含大量实体框架特有的功能。</span><span class="sxs-lookup"><span data-stu-id="adc85-217">Earlier versions of the Entity Framework offered limited support for persistence ignorance because entity classes had to inherit from the `EntityObject` class and thus included a great deal of Entity Framework-specific functionality.</span></span>

<span data-ttu-id="adc85-218">实体框架 4 引入了使用不继承的实体类的能力`EntityObject`类，因此可以在持久性未知。</span><span class="sxs-lookup"><span data-stu-id="adc85-218">The Entity Framework 4 introduces the ability to use entity classes that don't inherit from the `EntityObject` class and therefore are persistence ignorant.</span></span> <span data-ttu-id="adc85-219">在实体框架的上下文中，通常称为的类，如这*纯旧式 CLR 对象*（POCO 或 POCOs）。</span><span class="sxs-lookup"><span data-stu-id="adc85-219">In the context of the Entity Framework, classes like this are typically called *plain-old CLR objects* (POCO, or POCOs).</span></span> <span data-ttu-id="adc85-220">你可以手动编写 POCO 类也可以自动生成基于使用实体框架提供的文本模板转换工具包 (T4) 模板的现有数据模型。</span><span class="sxs-lookup"><span data-stu-id="adc85-220">You can write POCO classes manually, or you can automatically generate them based on an existing data model using Text Template Transformation Toolkit (T4) templates provided by the Entity Framework.</span></span>

<span data-ttu-id="adc85-221">有关在实体框架中使用 POCOs 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="adc85-221">For more information about using POCOs in the Entity Framework, see the following resources:</span></span>

- <span data-ttu-id="adc85-222">[使用 POCO 实体](https://msdn.microsoft.com/library/dd456853.aspx)。</span><span class="sxs-lookup"><span data-stu-id="adc85-222">[Working with POCO Entities](https://msdn.microsoft.com/library/dd456853.aspx).</span></span> <span data-ttu-id="adc85-223">这是概述 POCOs，其中包含指向具有更多详细信息的其他文档的 MSDN 文档。</span><span class="sxs-lookup"><span data-stu-id="adc85-223">This is an MSDN document that's an overview of POCOs, with links to other documents that have more detailed information.</span></span>
- <span data-ttu-id="adc85-224">[演练： POCO 实体框架的模板](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)这是实体框架开发团队，以链接到有关 POCOs 其他博客文章的博客文章。</span><span class="sxs-lookup"><span data-stu-id="adc85-224">[Walkthrough: POCO Template for the Entity Framework](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) This is a blog post from the Entity Framework development team, with links to other blog posts about POCOs.</span></span>

## <a name="code-first-development"></a><span data-ttu-id="adc85-225">代码优先开发</span><span class="sxs-lookup"><span data-stu-id="adc85-225">Code-First Development</span></span>

<span data-ttu-id="adc85-226">POCO 支持 Entity Framework 4 中的仍然需要你创建数据模型，并链接到数据模型的实体类。</span><span class="sxs-lookup"><span data-stu-id="adc85-226">POCO support in the Entity Framework 4 still requires that you create a data model and link your entity classes to the data model.</span></span> <span data-ttu-id="adc85-227">实体框架的下一个版本将包含一个称为功能*代码优先的开发*。</span><span class="sxs-lookup"><span data-stu-id="adc85-227">The next release of the Entity Framework will include a feature called *code-first development*.</span></span> <span data-ttu-id="adc85-228">此功能，可用于实体框架使用您自己的 POCO 类而无需使用数据模型设计器或数据模型 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="adc85-228">This feature enables you to use the Entity Framework with your own POCO classes without needing to use either the data model designer or a data model XML file.</span></span> <span data-ttu-id="adc85-229">(因此，此选项也已调用*仅限代码的*;*代码优先*和*仅限代码的*都是指同一实体框架功能。)</span><span class="sxs-lookup"><span data-stu-id="adc85-229">(Therefore, this option has also been called *code-only*; *code-first* and *code-only* both refer to the same Entity Framework feature.)</span></span>

<span data-ttu-id="adc85-230">有关使用开发的代码优先方法的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="adc85-230">For more information about using the code-first approach to development, see the following resources:</span></span>

- <span data-ttu-id="adc85-231">[代码优先的开发使用实体框架 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="adc85-231">[Code-First Development with Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx).</span></span> <span data-ttu-id="adc85-232">这是由 Scott Guthrie 简介代码优先开发博客文章。</span><span class="sxs-lookup"><span data-stu-id="adc85-232">This is a blog post by Scott Guthrie introducing code-first development.</span></span>
- [<span data-ttu-id="adc85-233">实体框架开发团队博客-文章标记的 CodeOnly</span><span class="sxs-lookup"><span data-stu-id="adc85-233">Entity Framework Development Team Blog - posts tagged CodeOnly</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [<span data-ttu-id="adc85-234">实体框架开发团队博客-文章标记 Code First</span><span class="sxs-lookup"><span data-stu-id="adc85-234">Entity Framework Development Team Blog - posts tagged Code First</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [<span data-ttu-id="adc85-235">MVC 音乐商店教程-第 4 部分： 模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="adc85-235">MVC Music Store tutorial - Part 4: Models and Data Access</span></span>](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [<span data-ttu-id="adc85-236">Getting Started with MVC 3-第 4 部分： 实体框架代码优先开发</span><span class="sxs-lookup"><span data-stu-id="adc85-236">Getting Started with MVC 3 - Part 4: Entity Framework Code-First Development</span></span>](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

<span data-ttu-id="adc85-237">此外，生成类似于 Contoso 大学应用程序的应用程序的新 MVC 代码的第一个教程预计在 2011 年春季发布 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span><span class="sxs-lookup"><span data-stu-id="adc85-237">In addition, a new MVC Code-First tutorial that builds an application similar to the Contoso University application is projected to be published in the spring of 2011 at [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span></span>

## <a name="more-information"></a><span data-ttu-id="adc85-238">详细信息</span><span class="sxs-lookup"><span data-stu-id="adc85-238">More Information</span></span>

<span data-ttu-id="adc85-239">这将完成将新实体框架和此继续实体框架教程系列中的概述。</span><span class="sxs-lookup"><span data-stu-id="adc85-239">This completes the overview to what's new in the Entity Framework and this Continuing with the Entity Framework tutorial series.</span></span> <span data-ttu-id="adc85-240">有关实体框架 4 所未涵盖的新功能的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="adc85-240">For more information about new features in the Entity Framework 4 that aren't covered here, see the following resources:</span></span>

- <span data-ttu-id="adc85-241">[什么是 ADO.NET 中的新增功能](https://msdn.microsoft.com/library/ex6y04yf.aspx)MSDN 主题中的实体框架版本 4 的新功能。</span><span class="sxs-lookup"><span data-stu-id="adc85-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN topic on new features in version 4 of the Entity Framework.</span></span>
- <span data-ttu-id="adc85-242">[宣布推出新版实体框架 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)版本 4 中的新增功能有关实体框架开发团队的博客文章。</span><span class="sxs-lookup"><span data-stu-id="adc85-242">[Announcing the release of Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) The Entity Framework development team's blog post about new features in version 4.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="adc85-243">上一篇</span><span class="sxs-lookup"><span data-stu-id="adc85-243">Previous</span></span>](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
