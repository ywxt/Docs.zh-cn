---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第 4 部分： 模型和数据访问 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 4 部分介绍了模型和数据访问。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 6a07bf6c8a3fb926ae25fe1f6c9359e64cd7a290
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825469"
---
<a name="part-4-models-and-data-access"></a><span data-ttu-id="3bb4d-104">第 4 部分： 模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="3bb4d-104">Part 4: Models and Data Access</span></span>
====================
<span data-ttu-id="3bb4d-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="3bb4d-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3bb4d-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="3bb4d-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="3bb4d-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="3bb4d-109">第 4 部分介绍了模型和数据访问。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-109">Part 4 covers Models and Data Access.</span></span>


<span data-ttu-id="3bb4d-110">到目前为止，我们已只已传递"虚拟数据"从我们控制器到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="3bb4d-111">现在我们已准备好挂接的实际数据库。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="3bb4d-112">在本教程中我们将讨论如何使用 SQL Server Compact Edition （通常称为 SQL CE） 作为我们的数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="3bb4d-113">SQL CE 是基于的免费、 嵌入式、 文件的数据库，不需要任何安装或配置，使其真正方便本地开发。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="3bb4d-114">数据库访问使用 Entity Framework 代码优先</span><span class="sxs-lookup"><span data-stu-id="3bb4d-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="3bb4d-115">我们将使用 ASP.NET MVC 3 项目来查询和更新数据库中包含的 Entity Framework (EF) 支持。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="3bb4d-116">EF 是一个灵活的对象关系映射 (ORM) 数据的 API，使开发人员能够以一种面向对象的方式存储在数据库中的查询和更新数据。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="3bb4d-117">实体框架版本 4 支持称为代码优先开发模式。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="3bb4d-118">代码的第一个，可通过编写简单的类 (也称为 POCO 从"纯旧式"CLR 对象)，创建模型对象，甚至可以从您的类动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="3bb4d-119">对我们模型类的更改</span><span class="sxs-lookup"><span data-stu-id="3bb4d-119">Changes to our Model Classes</span></span>

<span data-ttu-id="3bb4d-120">在本教程中，我们将使用实体框架中的数据库创建功能。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="3bb4d-121">我们执行该操作之前，不过，让我们进行一些小的更改到我们模型类中我们将更高版本使用的一些事项添加。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="3bb4d-122">添加艺术家模型类</span><span class="sxs-lookup"><span data-stu-id="3bb4d-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="3bb4d-123">因此，我们将添加一个简单的模型类来描述艺术家，我们唱片集将与艺术家，相关联。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="3bb4d-124">将新类添加到模型文件夹名为 Artist.cs 使用如下所示的代码。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="3bb4d-125">更新了模型类</span><span class="sxs-lookup"><span data-stu-id="3bb4d-125">Updating our Model Classes</span></span>

<span data-ttu-id="3bb4d-126">更新唱片集类，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="3bb4d-127">接下来，对流派类进行以下更新。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a><span data-ttu-id="3bb4d-128">将应用添加\_数据文件夹</span><span class="sxs-lookup"><span data-stu-id="3bb4d-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="3bb4d-129">我们将添加应用\_到我们的项目来存放我们的 SQL Server Express 数据库文件的数据目录。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="3bb4d-130">应用\_数据是在 ASP.NET 中已有数据库访问权限的正确的安全访问权限的特殊目录。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="3bb4d-131">从项目菜单中，选择添加 ASP.NET 文件夹，然后应用\_数据。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="3bb4d-132">在 web.config 文件中创建的连接字符串</span><span class="sxs-lookup"><span data-stu-id="3bb4d-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="3bb4d-133">我们将对网站的配置文件添加几行，以便实体框架知道如何连接到我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="3bb4d-134">双击 Web.config 文件位于项目根目录中。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="3bb4d-135">滚动到此文件的底部，添加&lt;connectionStrings&gt;部分的正上方的最后一行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="3bb4d-136">添加上下文类</span><span class="sxs-lookup"><span data-stu-id="3bb4d-136">Adding a Context Class</span></span>

<span data-ttu-id="3bb4d-137">右键单击模型文件夹并添加一个名为 MusicStoreEntities.cs 的新类。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="3bb4d-138">此类将表示实体框架数据库上下文，并将处理我们创建、 读取、 更新和删除用于我们的操作。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="3bb4d-139">此类的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="3bb4d-140">就这么简单-没有任何其他配置、 特殊的接口，等等。通过扩展 DbContext 基类，我们 MusicStoreEntities 类是能够处理我们为我们的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="3bb4d-141">现在，我们已得到挂接了，让我们将多个属性添加到我们的模型类以利用我们的数据库中的一些其他信息。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="3bb4d-142">添加存储目录数据</span><span class="sxs-lookup"><span data-stu-id="3bb4d-142">Adding our store catalog data</span></span>

<span data-ttu-id="3bb4d-143">将"种子"数据添加到新创建的数据库实体框架中，我们将充分利用一项功能。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="3bb4d-144">这将预填充了存储目录，流派、 艺术家和唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="3bb4d-145">MvcMusicStore Assets.zip 下载-包含我们之前在本教程中使用的站点设计文件-具有此种子数据，位于名为代码的文件夹中的类文件。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="3bb4d-146">在代码内 / Models 文件夹中，找到 SampleData.cs 文件并将其放到我们的项目中的 Models 文件夹中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="3bb4d-147">现在，我们需要添加一行代码需要了解的有关该 SampleData 类实体框架。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="3bb4d-148">双击要打开它，并添加以下行到顶部应用程序的项目的根目录中的 Global.asax 文件\_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="3bb4d-149">此时，我们已完成为我们的项目配置实体框架所必需的工作。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="3bb4d-150">查询数据库</span><span class="sxs-lookup"><span data-stu-id="3bb4d-150">Querying the Database</span></span>

<span data-ttu-id="3bb4d-151">现在让我们更新我们 StoreController 以便而不是使用"虚拟数据"改为调用到我们的数据库来查询其所有的信息。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="3bb4d-152">我们将开始通过声明一个字段上**StoreController**来托管实例的名为 storeDB MusicStoreEntities 类：</span><span class="sxs-lookup"><span data-stu-id="3bb4d-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="3bb4d-153">正在更新存储索引查询数据库</span><span class="sxs-lookup"><span data-stu-id="3bb4d-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="3bb4d-154">MusicStoreEntities 类由实体框架维护并公开数据库中每个表的集合属性。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="3bb4d-155">让我们更新我们 StoreController 索引操作来检索所有流派在我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="3bb4d-156">以前我们是通过硬编码字符串数据。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="3bb4d-157">现在我们可以只需使用实体框架上下文 Generes 集合：</span><span class="sxs-lookup"><span data-stu-id="3bb4d-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="3bb4d-158">不需要由于仍将返回同一 StoreIndexViewModel 之前-只需将返回实时数据从我们的数据库现在我们返回到我们的视图模板会发生任何更改。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="3bb4d-159">如果我们再次运行该项目并访问 URL"/ 存储"，我们现在看到所有影片类型列表在我们的数据库：</span><span class="sxs-lookup"><span data-stu-id="3bb4d-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="3bb4d-160">更新浏览应用商店和详细信息，以使用实时数据</span><span class="sxs-lookup"><span data-stu-id="3bb4d-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="3bb4d-161">与应用商店/浏览？ genre =*[某些流派]* 操作方法中，我们要搜索的一种流派的名称。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="3bb4d-162">我们仅预期结果，因为我们不应拥有相同的类型名称的两个项目，因此我们可以使用。在 LINQ 中查询此类的适当流派对象的 single （） 扩展 （不要键入这尚未）：</span><span class="sxs-lookup"><span data-stu-id="3bb4d-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="3bb4d-163">一个方法采用 Lambda 表达式作为参数，它指定我们想单个流派对象，以便其名称不匹配，我们已定义的值。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="3bb4d-164">在上面的示例中，我们在加载单个流派对象与匹配的 Disco 名称值。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="3bb4d-165">我们将利用一 Entity Framework 功能，使我们能够指示检索流派对象时，我们希望还加载其他相关的实体。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="3bb4d-166">此功能称为查询结果调整，并且使我们能够减少我们需要访问数据库以检索所有需要的信息的次数。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="3bb4d-167">我们想要预提取相册的流派我们检索，因此我们将更新我们的查询以包含从 Genres.Include("Albums") 以指示我们要以及相关的唱片集。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="3bb4d-168">这是更高效，因为它会检索中的单个数据库请求我们的流派和唱片集数据。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="3bb4d-169">使用开的说明，下面是我们已更新的浏览控制器操作的外观：</span><span class="sxs-lookup"><span data-stu-id="3bb4d-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="3bb4d-170">我们现在可以更新应用商店浏览视图以显示每个类型中可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="3bb4d-171">打开视图模板 (在中找到 /Views/Store/Browse.cshtml) 并添加唱片集的项目符号列表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="3bb4d-172">运行我们的应用程序并浏览到/Store/浏览？ genre = Jazz 显示我们的结果现在正在从数据库中，在我们所选流派中显示的所有相册拉取。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="3bb4d-173">我们将使相同的地址更改为我们 /Store/详细信息 / [id] URL，和我们虚构数据替换为数据库查询，这将加载其 ID 与参数值匹配的相册。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="3bb4d-174">运行我们的应用程序并浏览至 /Store/Details/1 显示了我们的结果从数据库正在请求。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="3bb4d-175">现在，我们存储详细信息的页设置要显示的唱片集 ID 的唱片集，让我们更新**浏览**视图，以链接到详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="3bb4d-176">我们将使用 Html.ActionLink，我们要从存储区索引链接到应用商店浏览在上一节末尾的样子。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="3bb4d-177">浏览视图的完整源如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="3bb4d-178">我们现在能够从我们的应用商店页浏览到流派页上，其中列出了可用的唱片集，并通过单击唱片集，我们可以查看该唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3bb4d-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="3bb4d-179">[上一页](mvc-music-store-part-3.md)
> [下一页](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="3bb4d-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
