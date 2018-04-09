---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第 4 部分： 模型和数据访问 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 4 部分介绍模型和数据访问。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 76671bbc7050d111b4d156c45584ba5aa4f1ea8f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="part-4-models-and-data-access"></a><span data-ttu-id="bbb12-104">第 4 部分： 模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="bbb12-104">Part 4: Models and Data Access</span></span>
====================
<span data-ttu-id="bbb12-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="bbb12-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="bbb12-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="bbb12-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="bbb12-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="bbb12-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="bbb12-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="bbb12-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="bbb12-109">第 4 部分介绍模型和数据访问。</span><span class="sxs-lookup"><span data-stu-id="bbb12-109">Part 4 covers Models and Data Access.</span></span>


<span data-ttu-id="bbb12-110">到目前为止，我们已刚刚已"dummy 数据"将从传递我们控制器到我们查看模板。</span><span class="sxs-lookup"><span data-stu-id="bbb12-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="bbb12-111">现在我们已准备好挂钩实际的数据库。</span><span class="sxs-lookup"><span data-stu-id="bbb12-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="bbb12-112">在本教程中我们将讨论如何使用 SQL Server Compact Edition （通常称为 SQL CE） 作为我们数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="bbb12-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="bbb12-113">SQL CE 是基于的免费、 嵌入式、 文件的数据库不需要任何安装或配置，这样，就以进行本地开发真正方便。</span><span class="sxs-lookup"><span data-stu-id="bbb12-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="bbb12-114">数据库访问与实体框架代码的第一个</span><span class="sxs-lookup"><span data-stu-id="bbb12-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="bbb12-115">我们将使用 ASP.NET MVC 3 项目，以便查询和更新数据库中包含的 Entity Framework (EF) 支持。</span><span class="sxs-lookup"><span data-stu-id="bbb12-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="bbb12-116">EF 是一个灵活的对象关系映射 (ORM) 数据的 API，使开发人员能够以一种面向对象的方式存储在数据库中的查询和更新数据。</span><span class="sxs-lookup"><span data-stu-id="bbb12-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="bbb12-117">实体框架版本 4 支持调用的代码优先的开发范例。</span><span class="sxs-lookup"><span data-stu-id="bbb12-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="bbb12-118">代码的第一个选项，可以通过编写简单的类 (也称为 POCO 从"纯旧式"CLR 对象)，创建模型对象，甚至可以从您的类动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="bbb12-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="bbb12-119">对我们的模型类的更改</span><span class="sxs-lookup"><span data-stu-id="bbb12-119">Changes to our Model Classes</span></span>

<span data-ttu-id="bbb12-120">我们将利用实体框架中的数据库创建功能在本教程中。</span><span class="sxs-lookup"><span data-stu-id="bbb12-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="bbb12-121">我们在此之前，不过，让我们进行一些次要更改到我们在我们将更高版本使用的事件中添加的模型类。</span><span class="sxs-lookup"><span data-stu-id="bbb12-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="bbb12-122">添加艺术家模型类</span><span class="sxs-lookup"><span data-stu-id="bbb12-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="bbb12-123">因此，我们将添加一个简单的模型类来描述艺术家，我们专辑将与艺术家，相关联。</span><span class="sxs-lookup"><span data-stu-id="bbb12-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="bbb12-124">将新类添加到名为 Artist.cs 使用下面所示的代码的 Models 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bbb12-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="bbb12-125">更新我们模型类</span><span class="sxs-lookup"><span data-stu-id="bbb12-125">Updating our Model Classes</span></span>

<span data-ttu-id="bbb12-126">更新唱片集类，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="bbb12-127">接下来，对流派类进行下列更新。</span><span class="sxs-lookup"><span data-stu-id="bbb12-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a><span data-ttu-id="bbb12-128">添加应用程序\_数据文件夹</span><span class="sxs-lookup"><span data-stu-id="bbb12-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="bbb12-129">我们将添加应用程序\_到我们的项目以保存我们 SQL Server Express 数据库文件的数据目录。</span><span class="sxs-lookup"><span data-stu-id="bbb12-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="bbb12-130">应用\_数据是已具有正确的安全访问权限来访问数据库的 ASP.NET 中的特殊目录。</span><span class="sxs-lookup"><span data-stu-id="bbb12-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="bbb12-131">从项目菜单中，选择添加 ASP.NET 文件夹，然后应用\_数据。</span><span class="sxs-lookup"><span data-stu-id="bbb12-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="bbb12-132">在 web.config 文件中创建连接字符串</span><span class="sxs-lookup"><span data-stu-id="bbb12-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="bbb12-133">以便实体框架知道如何连接到我们的数据库，我们将向网站的配置文件添加几行。</span><span class="sxs-lookup"><span data-stu-id="bbb12-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="bbb12-134">双击位于项目根目录中的 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="bbb12-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="bbb12-135">滚动到此文件的底部并添加&lt;connectionStrings&gt;部分的正上方的最后一行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="bbb12-136">添加上下文类</span><span class="sxs-lookup"><span data-stu-id="bbb12-136">Adding a Context Class</span></span>

<span data-ttu-id="bbb12-137">右键单击 Models 文件夹，并添加一个名为 MusicStoreEntities.cs 的新类。</span><span class="sxs-lookup"><span data-stu-id="bbb12-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="bbb12-138">此类将表示实体框架数据库上下文，并将处理我们创建、 读取、 更新和删除为我们的操作。</span><span class="sxs-lookup"><span data-stu-id="bbb12-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="bbb12-139">此类的代码所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="bbb12-140">就这么简单-没有任何其他配置、 特殊的接口，等等。通过扩展 DbContext 基类，我们 MusicStoreEntities 类是能够处理我们为我们的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="bbb12-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="bbb12-141">现在，我们提供的挂钩，让我们将几个更多属性添加到我们的模型类来利用我们的数据库中的某些其他信息。</span><span class="sxs-lookup"><span data-stu-id="bbb12-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="bbb12-142">添加我们存储目录数据</span><span class="sxs-lookup"><span data-stu-id="bbb12-142">Adding our store catalog data</span></span>

<span data-ttu-id="bbb12-143">将"种子"数据添加到新创建的数据库实体框架中，我们将充分利用一项功能。</span><span class="sxs-lookup"><span data-stu-id="bbb12-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="bbb12-144">这将预先填充我们应用商店目录的风格、 艺术家和唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="bbb12-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="bbb12-145">MvcMusicStore Assets.zip 下载-包含我们之前在本教程中使用的站点设计文件-已具有此种子数据，位于名为代码的文件夹中的类文件。</span><span class="sxs-lookup"><span data-stu-id="bbb12-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="bbb12-146">在代码中 / Models 文件夹中，找到 SampleData.cs 文件并将其放到我们的项目中的 Models 文件夹中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="bbb12-147">现在，我们需要添加一行代码需要了解的有关 SampleData 该类实体框架。</span><span class="sxs-lookup"><span data-stu-id="bbb12-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="bbb12-148">双击以打开它并添加以下行到顶部应用程序项目的根目录中的 Global.asax 文件\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="bbb12-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="bbb12-149">此时，我们已经完成为我们的项目配置实体框架所必需的工作。</span><span class="sxs-lookup"><span data-stu-id="bbb12-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="bbb12-150">查询数据库</span><span class="sxs-lookup"><span data-stu-id="bbb12-150">Querying the Database</span></span>

<span data-ttu-id="bbb12-151">现在让我们更新我们 StoreController 以便而不是使用"虚拟数据"它改为调用到我们的数据库以查询其所有的信息。</span><span class="sxs-lookup"><span data-stu-id="bbb12-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="bbb12-152">我们将开始通过将字段声明上**StoreController**来托管实例的名为 storeDB 的 MusicStoreEntities 类：</span><span class="sxs-lookup"><span data-stu-id="bbb12-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="bbb12-153">更新存储索引来查询数据库</span><span class="sxs-lookup"><span data-stu-id="bbb12-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="bbb12-154">MusicStoreEntities 类由实体框架维护，并公开每个表中我们的数据库使用的集合属性。</span><span class="sxs-lookup"><span data-stu-id="bbb12-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="bbb12-155">让我们更新我们 StoreController 索引操作，以检索在我们的数据库中的所有风格。</span><span class="sxs-lookup"><span data-stu-id="bbb12-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="bbb12-156">以前我们执行此操作的硬编码字符串数据。</span><span class="sxs-lookup"><span data-stu-id="bbb12-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="bbb12-157">现在我们可以只需使用实体框架上下文 Generes 集合：</span><span class="sxs-lookup"><span data-stu-id="bbb12-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="bbb12-158">发生到我们的视图模板，因为我们仍在返回之前-我们要仅返回实时数据从我们的数据库现在我们返回相同 StoreIndexViewModel 所不需要的任何更改。</span><span class="sxs-lookup"><span data-stu-id="bbb12-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="bbb12-159">当我们试运行项目和访问"/ 存储"URL 时，我们现在将我们的数据库中看到所有风格的列表：</span><span class="sxs-lookup"><span data-stu-id="bbb12-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="bbb12-160">更新存储浏览和详细信息，若要使用实时数据</span><span class="sxs-lookup"><span data-stu-id="bbb12-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="bbb12-161">与应用商店/浏览？ 流派 =*[某些流派]*操作方法，我们要搜索的一种风格的名称。</span><span class="sxs-lookup"><span data-stu-id="bbb12-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="bbb12-162">我们仅预期结果，因为我们不应永远都不会为流派同名的两个条目，因此我们可以使用。在 LINQ 查询为适当的流派对象如下的 Single() 扩展 （不要键入这尚未）：</span><span class="sxs-lookup"><span data-stu-id="bbb12-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="bbb12-163">单个方法采用 Lambda 表达式作为一个参数，它指定我们希望单个流派对象，以便其名称与我们已定义的值相匹配。</span><span class="sxs-lookup"><span data-stu-id="bbb12-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="bbb12-164">在上面的示例中，我们会匹配 Disco 为名称值中加载单个流派对象。</span><span class="sxs-lookup"><span data-stu-id="bbb12-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="bbb12-165">我们将充分利用一实体框架功能，使我们可以指示检索流派对象时，我们想加载以及其他相关的实体。</span><span class="sxs-lookup"><span data-stu-id="bbb12-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="bbb12-166">此功能称为查询结果调整，并使我们能够减少我们需要用于访问数据库来检索所有我们需要的信息的次数。</span><span class="sxs-lookup"><span data-stu-id="bbb12-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="bbb12-167">我们想要预提取的流派我们检索唱片集，因此我们将更新我们的查询以从 Genres.Include("Albums") 以指示我们要以及相关唱片集都有。</span><span class="sxs-lookup"><span data-stu-id="bbb12-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="bbb12-168">这是更高效，因为它将检索单个数据库请求中我们 Genre 和唱片集的数据。</span><span class="sxs-lookup"><span data-stu-id="bbb12-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="bbb12-169">说明开，下面是我们更新的浏览控制器操作的外观：</span><span class="sxs-lookup"><span data-stu-id="bbb12-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="bbb12-170">我们现在可以更新存储浏览视图以显示专辑中每个风格。</span><span class="sxs-lookup"><span data-stu-id="bbb12-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="bbb12-171">打开视图模板 (在中找到 /Views/Store/Browse.cshtml) 并添加唱片集的项目符号列表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="bbb12-172">运行我们的应用程序，并浏览至/存储/浏览？ 流派 = 爵士乐表明，从数据库中，在我们所选风格中显示所有专辑现在拉出我们的结果。</span><span class="sxs-lookup"><span data-stu-id="bbb12-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="bbb12-173">我们将使将更改为我们 /Store/详细信息 / [id] URL，并将我们 dummy 数据替换为数据库查询，后者将加载唱片集的 ID 匹配的参数值相同。</span><span class="sxs-lookup"><span data-stu-id="bbb12-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="bbb12-174">运行我们的应用程序和浏览到 /Store/Details/1 演示了我们的结果从数据库正在请求。</span><span class="sxs-lookup"><span data-stu-id="bbb12-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="bbb12-175">现在，我们存储详细信息页面设置为按唱片集 ID 显示唱片集，让我们更新**浏览**视图以链接到详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="bbb12-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="bbb12-176">我们将使用次 Html.ActionLink，严格按照我们未从应用商店索引链接到应用商店浏览在上一节的末尾。</span><span class="sxs-lookup"><span data-stu-id="bbb12-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="bbb12-177">浏览视图的完整源如下所示。</span><span class="sxs-lookup"><span data-stu-id="bbb12-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="bbb12-178">我们现在能够从我们的应用商店页面浏览到流派页，其中列出了可用的专辑，并通过单击唱片集，我们可以查看该唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bbb12-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="bbb12-179">[上一页](mvc-music-store-part-3.md)
> [下一页](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="bbb12-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
