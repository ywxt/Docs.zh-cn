---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: "添加模型 |Microsoft 文档"
author: Rick-Anderson
description: "注意： 本教程的更新的版本此处提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全，请按照和演示要简单得多..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 304c428b0d787e902f30c1989471c476f54d3b39
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-model"></a><span data-ttu-id="db0b4-104">添加模型</span><span class="sxs-lookup"><span data-stu-id="db0b4-104">Adding a Model</span></span>
====================
<span data-ttu-id="db0b4-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="db0b4-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="db0b4-106">本教程的更新的版本可[此处](../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="db0b4-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="db0b4-107">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="db0b4-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="db0b4-108">在本部分中，你将添加用于管理数据库中的电影某些类。</span><span class="sxs-lookup"><span data-stu-id="db0b4-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="db0b4-109">这些类将&quot;模型&quot;ASP.NET MVC 应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="db0b4-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="db0b4-110">你将使用名为的.NET Framework 数据访问技术[实体框架](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="db0b4-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="db0b4-111">开发范例调用 （通常称为 EF） 的实体框架支持*Code First*。</span><span class="sxs-lookup"><span data-stu-id="db0b4-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="db0b4-112">代码首先，可通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="db0b4-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="db0b4-113">(这些是也称为 POCO 类，从&quot;纯旧式 CLR 对象。&quot;)然后，你可以这样非常干净且快速开发工作流从您的类，动态创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="db0b4-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="db0b4-114">添加模型类</span><span class="sxs-lookup"><span data-stu-id="db0b4-114">Adding Model Classes</span></span>

<span data-ttu-id="db0b4-115">在**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="db0b4-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="db0b4-116">输入*类*名称&quot;电影&quot;。</span><span class="sxs-lookup"><span data-stu-id="db0b4-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="db0b4-117">添加到以下五种属性`Movie`类：</span><span class="sxs-lookup"><span data-stu-id="db0b4-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="db0b4-118">我们将使用`Movie`类来表示数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="db0b4-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="db0b4-119">每个实例`Movie`对象将对应于数据库表中，并的每个属性中的行`Movie`类将映射到表中的列。</span><span class="sxs-lookup"><span data-stu-id="db0b4-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="db0b4-120">在同一文件中，添加以下`MovieDBContext`类：</span><span class="sxs-lookup"><span data-stu-id="db0b4-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="db0b4-121">`MovieDBContext`类表示的实体框架的电影数据库上下文，用于处理提取、 存储和更新`Movie`类数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="db0b4-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="db0b4-122">`MovieDBContext`派生自`DbContext`由实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="db0b4-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="db0b4-123">若要引用`DbContext`和`DbSet`，你需要添加以下`using`语句文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="db0b4-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="db0b4-124">完整*Movie.cs*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="db0b4-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="db0b4-125">(多个使用不是语句需要已删除。)</span><span class="sxs-lookup"><span data-stu-id="db0b4-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="db0b4-126">创建连接字符串和使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="db0b4-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="db0b4-127">`MovieDBContext`你创建的类处理任务连接到数据库并映射`Movie`数据库记录的对象。</span><span class="sxs-lookup"><span data-stu-id="db0b4-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="db0b4-128">一个问题可能会问，不过，是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="db0b4-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="db0b4-129">将执行该操作通过添加中的连接信息*Web.config*应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="db0b4-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="db0b4-130">打开应用程序根目录*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="db0b4-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="db0b4-131">(不*Web.config*文件中*视图*文件夹。)打开*Web.config*用红色的文件。</span><span class="sxs-lookup"><span data-stu-id="db0b4-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="db0b4-132">添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="db0b4-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="db0b4-133">下面的示例显示的一部分*Web.config*文件以添加新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="db0b4-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="db0b4-134">这种少量的代码和 XML 是你需要编写以便表示，并将影片数据存储在数据库中的所有内容。</span><span class="sxs-lookup"><span data-stu-id="db0b4-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="db0b4-135">接下来，你将生成一个新`MoviesController`类，该类可以用于显示影片数据，并允许用户创建新的影片列表。</span><span class="sxs-lookup"><span data-stu-id="db0b4-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="db0b4-136">[上一页](adding-a-view.md)
[下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="db0b4-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
