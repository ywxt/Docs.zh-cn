---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 添加模型 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0c846d31fb6b24ad964d69d0f81858c87305d68c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826633"
---
<a name="adding-a-model-vb"></a><span data-ttu-id="56bcf-103">添加模型 (VB)</span><span class="sxs-lookup"><span data-stu-id="56bcf-103">Adding a Model (VB)</span></span>
====================
<span data-ttu-id="56bcf-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="56bcf-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="56bcf-105">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="56bcf-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="56bcf-106">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="56bcf-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="56bcf-107">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="56bcf-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="56bcf-108">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="56bcf-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="56bcf-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="56bcf-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="56bcf-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="56bcf-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="56bcf-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="56bcf-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="56bcf-112">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="56bcf-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="56bcf-113">可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="56bcf-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="56bcf-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="56bcf-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="56bcf-115">如果您愿意 C#，切换到[C# 版本](../cs/adding-a-model.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="56bcf-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="56bcf-116">添加模型</span><span class="sxs-lookup"><span data-stu-id="56bcf-116">Adding a Model</span></span>

<span data-ttu-id="56bcf-117">在本部分中将添加用于管理数据库中的电影的一些类。</span><span class="sxs-lookup"><span data-stu-id="56bcf-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="56bcf-118">这些类将 ASP.NET MVC 应用程序的"模型"部分。</span><span class="sxs-lookup"><span data-stu-id="56bcf-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="56bcf-119">将使用名为实体框架的.NET Framework 数据访问技术来定义和使用这些模型的类。</span><span class="sxs-lookup"><span data-stu-id="56bcf-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="56bcf-120">实体框架 （通常称为 EF） 支持开发模式称为*Code First*。</span><span class="sxs-lookup"><span data-stu-id="56bcf-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="56bcf-121">代码首先允许你通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="56bcf-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="56bcf-122">（这些也称为是 POCO 类，从"纯旧式 CLR 对象"。）然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="56bcf-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="56bcf-123">添加模型类</span><span class="sxs-lookup"><span data-stu-id="56bcf-123">Adding Model Classes</span></span>

<span data-ttu-id="56bcf-124">在中**解决方案资源管理器**，右键单击 *模型* 文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="56bcf-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="56bcf-125">命名类"电影"。</span><span class="sxs-lookup"><span data-stu-id="56bcf-125">Name the class "Movie".</span></span>

<span data-ttu-id="56bcf-126">添加到以下五个属性`Movie`类：</span><span class="sxs-lookup"><span data-stu-id="56bcf-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="56bcf-127">我们将使用`Movie`类来表示数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="56bcf-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="56bcf-128">每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。</span><span class="sxs-lookup"><span data-stu-id="56bcf-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="56bcf-129">在同一文件中，添加以下`MovieDBContext`类：</span><span class="sxs-lookup"><span data-stu-id="56bcf-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="56bcf-130">`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。</span><span class="sxs-lookup"><span data-stu-id="56bcf-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="56bcf-131">`MovieDBContext`派生自`DbContext`实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="56bcf-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="56bcf-132">有关详细信息`DbContext`并`DbSet`，请参阅[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。</span><span class="sxs-lookup"><span data-stu-id="56bcf-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="56bcf-133">若要引用将`DbContext`并`DbSet`，你需要添加以下`imports`在文件顶部的语句：</span><span class="sxs-lookup"><span data-stu-id="56bcf-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="56bcf-134">完整*Movie.vb*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="56bcf-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="56bcf-135">创建的连接字符串和使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="56bcf-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="56bcf-136">`MovieDBContext`创建的类处理连接到数据库以及映射任务`Movie`数据库记录的对象。</span><span class="sxs-lookup"><span data-stu-id="56bcf-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="56bcf-137">您可能会问的一个问题，是如何指定将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="56bcf-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="56bcf-138">您将通过添加中的连接信息来实现*Web.config*应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="56bcf-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="56bcf-139">打开应用程序根目录*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="56bcf-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="56bcf-140">(未*Web.config*中的文件*视图*文件夹。)下图显示两者*Web.config*文件; 打开*Web.config*用红线圈出文件。</span><span class="sxs-lookup"><span data-stu-id="56bcf-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

## 

<span data-ttu-id="56bcf-141">添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="56bcf-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="56bcf-142">下面的示例显示了一部分*Web.config*文件添加的新连接字符串：</span><span class="sxs-lookup"><span data-stu-id="56bcf-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="56bcf-143">这种少量的代码和 XML 是为了表示，并将影片数据存储在数据库中编写所需的一切。</span><span class="sxs-lookup"><span data-stu-id="56bcf-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="56bcf-144">接下来，你将生成一个新`MoviesController`类，该类可以用于显示电影数据并允许用户创建新的影片列表。</span><span class="sxs-lookup"><span data-stu-id="56bcf-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56bcf-145">[上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="56bcf-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
