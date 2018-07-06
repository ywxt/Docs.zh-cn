---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 2d99a9c553ba79922cb0c5e852709ab97ea2e22b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818458"
---
<a name="adding-a-model"></a><span data-ttu-id="8fc81-102">添加模型</span><span class="sxs-lookup"><span data-stu-id="8fc81-102">Adding a Model</span></span>
====================
<span data-ttu-id="8fc81-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="8fc81-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="8fc81-104">在本部分中将添加用于管理数据库中的电影的一些类。</span><span class="sxs-lookup"><span data-stu-id="8fc81-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="8fc81-105">这些类将是&quot;模型&quot;ASP.NET MVC 应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="8fc81-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="8fc81-106">将使用名为.NET Framework 数据访问技术[Entity Framework](https://docs.microsoft.com/ef/)来定义和使用这些模型的类。</span><span class="sxs-lookup"><span data-stu-id="8fc81-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="8fc81-107">实体框架 （通常称为 EF） 支持开发模式称为*Code First*。</span><span class="sxs-lookup"><span data-stu-id="8fc81-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="8fc81-108">代码首先允许你通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="8fc81-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="8fc81-109">(这些是也称为 POCO 类，从&quot;普通旧 CLR 对象。&quot;)然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="8fc81-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="8fc81-110">如果您需要首先创建数据库，您仍可遵循此教程，了解有关 MVC 和 EF 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="8fc81-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="8fc81-111">然后可以按照 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)教程，介绍了数据库第一种方法。</span><span class="sxs-lookup"><span data-stu-id="8fc81-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="8fc81-112">添加模型类</span><span class="sxs-lookup"><span data-stu-id="8fc81-112">Adding Model Classes</span></span>

<span data-ttu-id="8fc81-113">在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="8fc81-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="8fc81-114">输入*类*名称&quot;电影&quot;。</span><span class="sxs-lookup"><span data-stu-id="8fc81-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="8fc81-115">添加到以下五个属性`Movie`类：</span><span class="sxs-lookup"><span data-stu-id="8fc81-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="8fc81-116">我们将使用`Movie`类来表示数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="8fc81-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="8fc81-117">每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。</span><span class="sxs-lookup"><span data-stu-id="8fc81-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="8fc81-118">注意： 若要使用 system.data.entity 的引用和相关的类，您需要安装[实体框架 NuGet 包](https://www.nuget.org/packages/EntityFramework/)。</span><span class="sxs-lookup"><span data-stu-id="8fc81-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="8fc81-119">请访问有关进一步说明链接。</span><span class="sxs-lookup"><span data-stu-id="8fc81-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="8fc81-120">在同一文件中，添加以下`MovieDBContext`类：</span><span class="sxs-lookup"><span data-stu-id="8fc81-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="8fc81-121">`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="8fc81-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="8fc81-122">`MovieDBContext`派生自`DbContext`实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="8fc81-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="8fc81-123">若要引用将`DbContext`并`DbSet`，你需要添加以下`using`在文件顶部的语句：</span><span class="sxs-lookup"><span data-stu-id="8fc81-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="8fc81-124">您可以执行此操作通过手动添加 using 语句，也可以悬停在红色的波浪线，再单击`Show potential fixes`单击 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="8fc81-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="8fc81-125">注意： 多个未使用`using`语句已被删除。</span><span class="sxs-lookup"><span data-stu-id="8fc81-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="8fc81-126">Visual Studio 将显示为灰色的未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="8fc81-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="8fc81-127">可以通过将鼠标悬停的灰色的依赖项上删除未使用的依赖项，再单击`Show potential fixes`单击**删除未使用的 Using。**</span><span class="sxs-lookup"><span data-stu-id="8fc81-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="8fc81-128">最后，我们已添加模型 (在 MVC 中的 M)。</span><span class="sxs-lookup"><span data-stu-id="8fc81-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="8fc81-129">下一节中将使用数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="8fc81-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8fc81-130">[上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="8fc81-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
