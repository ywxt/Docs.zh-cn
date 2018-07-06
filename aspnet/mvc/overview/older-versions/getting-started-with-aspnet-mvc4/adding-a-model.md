---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e68b6d41c7880fb849bbefbedd4c4e25c6f47b0e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837754"
---
<a name="adding-a-model"></a><span data-ttu-id="575d0-104">添加模型</span><span class="sxs-lookup"><span data-stu-id="575d0-104">Adding a Model</span></span>
====================
<span data-ttu-id="575d0-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="575d0-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="575d0-106">本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="575d0-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="575d0-107">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="575d0-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="575d0-108">在本部分中将添加用于管理数据库中的电影的一些类。</span><span class="sxs-lookup"><span data-stu-id="575d0-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="575d0-109">这些类将是&quot;模型&quot;ASP.NET MVC 应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="575d0-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="575d0-110">将使用名为.NET Framework 数据访问技术[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)来定义和使用这些模型的类。</span><span class="sxs-lookup"><span data-stu-id="575d0-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="575d0-111">实体框架 （通常称为 EF） 支持开发模式称为*Code First*。</span><span class="sxs-lookup"><span data-stu-id="575d0-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="575d0-112">代码首先允许你通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="575d0-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="575d0-113">(这些是也称为 POCO 类，从&quot;普通旧 CLR 对象。&quot;)然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="575d0-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="575d0-114">添加模型类</span><span class="sxs-lookup"><span data-stu-id="575d0-114">Adding Model Classes</span></span>

<span data-ttu-id="575d0-115">在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="575d0-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="575d0-116">输入*类*名称&quot;电影&quot;。</span><span class="sxs-lookup"><span data-stu-id="575d0-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="575d0-117">添加到以下五个属性`Movie`类：</span><span class="sxs-lookup"><span data-stu-id="575d0-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="575d0-118">我们将使用`Movie`类来表示数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="575d0-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="575d0-119">每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。</span><span class="sxs-lookup"><span data-stu-id="575d0-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="575d0-120">在同一文件中，添加以下`MovieDBContext`类：</span><span class="sxs-lookup"><span data-stu-id="575d0-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="575d0-121">`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="575d0-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="575d0-122">`MovieDBContext`派生自`DbContext`实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="575d0-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="575d0-123">若要引用将`DbContext`并`DbSet`，你需要添加以下`using`在文件顶部的语句：</span><span class="sxs-lookup"><span data-stu-id="575d0-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="575d0-124">完整*Movie.cs*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="575d0-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="575d0-125">(多个 using 语句不需要已被删除。)</span><span class="sxs-lookup"><span data-stu-id="575d0-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="575d0-126">创建的连接字符串和使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="575d0-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="575d0-127">`MovieDBContext`创建的类处理连接到数据库以及映射任务`Movie`数据库记录的对象。</span><span class="sxs-lookup"><span data-stu-id="575d0-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="575d0-128">您可能会问的一个问题，是如何指定将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="575d0-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="575d0-129">您将通过添加中的连接信息来实现*Web.config*应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="575d0-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="575d0-130">打开应用程序根目录*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="575d0-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="575d0-131">(未*Web.config*中的文件*视图*文件夹。)打开*Web.config*以红色标出的文件。</span><span class="sxs-lookup"><span data-stu-id="575d0-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="575d0-132">添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="575d0-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="575d0-133">下面的示例显示了一部分*Web.config*文件添加的新连接字符串：</span><span class="sxs-lookup"><span data-stu-id="575d0-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="575d0-134">这种少量的代码和 XML 是为了表示，并将影片数据存储在数据库中编写所需的一切。</span><span class="sxs-lookup"><span data-stu-id="575d0-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="575d0-135">接下来，你将生成一个新`MoviesController`类，该类可以用于显示电影数据并允许用户创建新的影片列表。</span><span class="sxs-lookup"><span data-stu-id="575d0-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="575d0-136">[上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="575d0-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
