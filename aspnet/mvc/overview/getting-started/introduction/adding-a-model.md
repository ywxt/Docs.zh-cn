---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 添加模型 |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: b3ef871c4d7627a03c8f0fd8cce9d3e97fc1a4ba
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-model"></a><span data-ttu-id="fd443-102">添加模型</span><span class="sxs-lookup"><span data-stu-id="fd443-102">Adding a Model</span></span>
====================
<span data-ttu-id="fd443-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="fd443-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="fd443-104">在本部分中，你将添加用于管理数据库中的电影某些类。</span><span class="sxs-lookup"><span data-stu-id="fd443-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="fd443-105">这些类将&quot;模型&quot;ASP.NET MVC 应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="fd443-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="fd443-106">你将使用名为的.NET Framework 数据访问技术[实体框架](https://docs.microsoft.com/ef/)定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="fd443-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="fd443-107">开发范例调用 （通常称为 EF） 的实体框架支持*Code First*。</span><span class="sxs-lookup"><span data-stu-id="fd443-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="fd443-108">代码首先，可通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="fd443-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="fd443-109">(这些是也称为 POCO 类，从&quot;纯旧式 CLR 对象。&quot;)然后，你可以这样非常干净且快速开发工作流从您的类，动态创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="fd443-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="fd443-110">如果你需要首先创建数据库，则仍可按照本教程，若要了解有关 MVC 和 EF 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="fd443-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="fd443-111">然后，你可以按照 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)教程，介绍数据库第一种方法。</span><span class="sxs-lookup"><span data-stu-id="fd443-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="fd443-112">添加模型类</span><span class="sxs-lookup"><span data-stu-id="fd443-112">Adding Model Classes</span></span>

<span data-ttu-id="fd443-113">在**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="fd443-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="fd443-114">输入*类*名称&quot;电影&quot;。</span><span class="sxs-lookup"><span data-stu-id="fd443-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="fd443-115">添加到以下五种属性`Movie`类：</span><span class="sxs-lookup"><span data-stu-id="fd443-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="fd443-116">我们将使用`Movie`类来表示数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="fd443-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="fd443-117">每个实例`Movie`对象将对应于数据库表中，并的每个属性中的行`Movie`类将映射到表中的列。</span><span class="sxs-lookup"><span data-stu-id="fd443-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="fd443-118">注意： 若要使用 System.Data.Entity 和相关的类，你需要安装[实体 Framework NuGet 包](https://www.nuget.org/packages/EntityFramework/)。</span><span class="sxs-lookup"><span data-stu-id="fd443-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="fd443-119">按链接进行进一步的说明。</span><span class="sxs-lookup"><span data-stu-id="fd443-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="fd443-120">在同一文件中，添加以下`MovieDBContext`类：</span><span class="sxs-lookup"><span data-stu-id="fd443-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="fd443-121">`MovieDBContext`类表示的实体框架的电影数据库上下文，用于处理提取、 存储和更新`Movie`类数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="fd443-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="fd443-122">`MovieDBContext`派生自`DbContext`由实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="fd443-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="fd443-123">若要引用`DbContext`和`DbSet`，你需要添加以下`using`语句文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="fd443-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="fd443-124">你可以执行此操作通过手动添加 using 语句，也可以将鼠标悬停在红色波浪线，请单击`Show potential fixes`单击 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="fd443-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="fd443-125">注意： 多个未使用`using`语句已删除。</span><span class="sxs-lookup"><span data-stu-id="fd443-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="fd443-126">Visual Studio 将显示为灰色的未使用的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="fd443-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="fd443-127">你可以通过将鼠标悬停在灰色的依赖关系中删除未使用的依赖关系，请单击`Show potential fixes`单击**删除未使用的 Using。**</span><span class="sxs-lookup"><span data-stu-id="fd443-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="fd443-128">最后，我们添加了模型 (MVC 中的 M) 上。</span><span class="sxs-lookup"><span data-stu-id="fd443-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="fd443-129">在下一部分中你将使用的数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fd443-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fd443-130">[上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="fd443-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
