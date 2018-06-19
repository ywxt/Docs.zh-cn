---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第 5 部分： 编辑窗体和模板化 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 5 部分介绍如何编辑窗体和模板化。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: d584e614b5a4124044cd9decd2272192ca164643
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874907"
---
<a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="e43b6-104">第 5 部分： 编辑窗体和模板化</span><span class="sxs-lookup"><span data-stu-id="e43b6-104">Part 5: Edit Forms and Templating</span></span>
====================
<span data-ttu-id="e43b6-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="e43b6-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="e43b6-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="e43b6-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="e43b6-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="e43b6-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="e43b6-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="e43b6-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="e43b6-109">第 5 部分介绍如何编辑窗体和模板化。</span><span class="sxs-lookup"><span data-stu-id="e43b6-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="e43b6-110">在过去的章中，我们已将数据从我们的数据库加载并显示它。</span><span class="sxs-lookup"><span data-stu-id="e43b6-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="e43b6-111">在本章中，我们将启用编辑数据。</span><span class="sxs-lookup"><span data-stu-id="e43b6-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="e43b6-112">创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="e43b6-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="e43b6-113">我们将首先通过创建新的控制器调用**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="e43b6-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="e43b6-114">此控制器中，我们将充分利用 ASP.NET MVC 3 Tools 更新中提供的基架功能。</span><span class="sxs-lookup"><span data-stu-id="e43b6-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="e43b6-115">设置添加控制器对话框中的选项，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e43b6-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="e43b6-116">单击添加按钮时，你将看到的 ASP.NET MVC 3 基架机制为你进行大量工作：</span><span class="sxs-lookup"><span data-stu-id="e43b6-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="e43b6-117">它创建新的 StoreManagerController 与本地的实体框架变量</span><span class="sxs-lookup"><span data-stu-id="e43b6-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="e43b6-118">它将 StoreManager 文件夹添加到项目的 Views 文件夹</span><span class="sxs-lookup"><span data-stu-id="e43b6-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="e43b6-119">它将添加 Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml 和 Index.cshtml 视图中，强类型化为唱片集类</span><span class="sxs-lookup"><span data-stu-id="e43b6-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="e43b6-120">新的 StoreManager 控制器类包括 CRUD （创建、 读取、 更新、 删除） 知道如何处理与唱片集的控制器操作模型类，并使用我们的实体框架上下文来数据库访问。</span><span class="sxs-lookup"><span data-stu-id="e43b6-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="e43b6-121">修改基架的视图</span><span class="sxs-lookup"><span data-stu-id="e43b6-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="e43b6-122">请务必记住，虽然我们已生成此代码，它是标准的 ASP.NET MVC 代码，就像我们已在本指南中已编写一样。</span><span class="sxs-lookup"><span data-stu-id="e43b6-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="e43b6-123">它具有为了节省你将会花费的时间编写样本控制器代码和手动创建强类型化的视图，但这不是您可能会看到的前面加上在注释中有关如何不得更改导致可怕警告的生成代码的类型代码。</span><span class="sxs-lookup"><span data-stu-id="e43b6-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="e43b6-124">这是你的代码，并且希望您来对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="e43b6-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="e43b6-125">因此，让我们开始到 StoreManager 索引视图快速编辑 (/ Views/StoreManager/Index.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="e43b6-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="e43b6-126">此视图将显示一个表，该表列出了在我们的存储与编辑唱片集 / 删除的链接，和的详细信息包括唱片集的公共属性。</span><span class="sxs-lookup"><span data-stu-id="e43b6-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="e43b6-127">我们将删除 AlbumArtUrl 字段中，因为它不是在此显示中非常有用。</span><span class="sxs-lookup"><span data-stu-id="e43b6-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="e43b6-128">在&lt;表&gt;部分的查看代码中，删除&lt;th&gt;和&lt;td&gt;元素周围 AlbumArtUrl 引用，如下面突出显示的行所示：</span><span class="sxs-lookup"><span data-stu-id="e43b6-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="e43b6-129">修改的视图代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="e43b6-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="e43b6-130">首先查看一下商店经理</span><span class="sxs-lookup"><span data-stu-id="e43b6-130">A first look at the Store Manager</span></span>

<span data-ttu-id="e43b6-131">现在运行应用程序，并浏览到/StoreManager /。</span><span class="sxs-lookup"><span data-stu-id="e43b6-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="e43b6-132">此时将显示存储管理器索引我们刚修改，在具有编辑详细信息，以及删除链接的存储区中显示的唱片集的列表。</span><span class="sxs-lookup"><span data-stu-id="e43b6-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="e43b6-133">单击编辑链接唱片集，包括 Genre 和艺术家下拉列表中显示与字段的编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="e43b6-134">单击"返回到列表中"链接，在底部，然后单击唱片集的详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="e43b6-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="e43b6-135">此时将显示各个唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e43b6-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="e43b6-136">同样，单击列表链接回，然后单击删除链接。</span><span class="sxs-lookup"><span data-stu-id="e43b6-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="e43b6-137">此时将显示确认对话框中，显示唱片集详细信息，并询问我们是否确保我们想要将其删除。</span><span class="sxs-lookup"><span data-stu-id="e43b6-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="e43b6-138">单击底部的删除按钮，将删除唱片集，并使你返回到显示删除唱片集的索引页。</span><span class="sxs-lookup"><span data-stu-id="e43b6-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="e43b6-139">我们还没有完成与存储管理器，但我们无控制器和查看代码的 CRUD 操作从启动。</span><span class="sxs-lookup"><span data-stu-id="e43b6-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="e43b6-140">查看存储管理器控制器代码</span><span class="sxs-lookup"><span data-stu-id="e43b6-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="e43b6-141">存储管理器控制器包含大量的代码。</span><span class="sxs-lookup"><span data-stu-id="e43b6-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="e43b6-142">让我们看一下这从上到下。</span><span class="sxs-lookup"><span data-stu-id="e43b6-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="e43b6-143">控制器包含一个 MVC 控制器，以及对我们的模型命名空间的引用的某些标准命名空间。</span><span class="sxs-lookup"><span data-stu-id="e43b6-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="e43b6-144">控制器有 MusicStoreEntities，由每个控制器操作用于数据访问的专用实例。</span><span class="sxs-lookup"><span data-stu-id="e43b6-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="e43b6-145">存储管理器 Index 和 Details 操作</span><span class="sxs-lookup"><span data-stu-id="e43b6-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="e43b6-146">索引视图检索的专辑，包括每个唱片集的引用的流派和艺术家信息，正如我们以前看到的应用商店浏览方法上工作时的列表。</span><span class="sxs-lookup"><span data-stu-id="e43b6-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="e43b6-147">索引视图是以下对链接的对象的引用，以便它可以显示每个唱片集的流派名称和艺术家名称，以便在控制器正在高效且查询在原始请求此信息。</span><span class="sxs-lookup"><span data-stu-id="e43b6-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="e43b6-148">StoreManager 控制器的详细信息控制器操作起作用，我们编写了以前为-它会询问是否唱片集的存储控制器的详细信息操作完全相同通过使用 find （） 方法的 ID，然后将其返回到视图。</span><span class="sxs-lookup"><span data-stu-id="e43b6-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="e43b6-149">创建操作方法</span><span class="sxs-lookup"><span data-stu-id="e43b6-149">The Create Action Methods</span></span>

<span data-ttu-id="e43b6-150">创建操作方法是从大到目前为止，我们已了解稍有不同的因为它们处理窗体输入。</span><span class="sxs-lookup"><span data-stu-id="e43b6-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="e43b6-151">当用户第一次访问时 /StoreManager/创建/他们将看到一个空白的表单。</span><span class="sxs-lookup"><span data-stu-id="e43b6-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="e43b6-152">此 HTML 页将包含&lt;窗体&gt;元素包含下拉列表中和文本框中输入它们可以在其中输入唱片集的详细信息的元素。</span><span class="sxs-lookup"><span data-stu-id="e43b6-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="e43b6-153">用户填写唱片集窗体值后，他们可以按"保存"按钮以提交这些更改发回应用程序以保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="e43b6-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="e43b6-154">当用户按"保存"按钮&lt;窗体&gt;将执行回 /StoreManager/创建/URL HTTP POST 和提交&lt;窗体&gt;HTTP POST 的一部分的值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="e43b6-155">ASP.NET MVC 使我们能够轻松地通过使我们能够实现两个不同的"创建"操作方法在我们 StoreManagerController 类 – 另一个用于处理初始的 HTTP GET 浏览到 /StoreManager/Create 拆分这两个 URL 调用方案的逻辑/ URL 和其他处理提交的更改 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="e43b6-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="e43b6-156">将信息传递给使用 ViewBag 的视图</span><span class="sxs-lookup"><span data-stu-id="e43b6-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="e43b6-157">我们之前在本教程中中, 已使用 ViewBag，但尚未讨论太了解它。</span><span class="sxs-lookup"><span data-stu-id="e43b6-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="e43b6-158">ViewBag 使得我们可以将信息传递给视图，而无需使用强类型化的模型对象。</span><span class="sxs-lookup"><span data-stu-id="e43b6-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="e43b6-159">在这种情况下，我们编辑 HTTP GET 控制器操作需要将这两种风格和专业人员的列表传递到窗体来填充下拉列表，并执行该操作的最简单方法是以使其恢复为 ViewBag 项。</span><span class="sxs-lookup"><span data-stu-id="e43b6-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="e43b6-160">ViewBag 是动态对象，这意味着你可以无需编写代码来定义这些属性键入 ViewBag.Foo 或 ViewBag.YourNameHere。</span><span class="sxs-lookup"><span data-stu-id="e43b6-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="e43b6-161">在这种情况下，控制器代码使用 ViewBag.GenreId 和 ViewBag.ArtistId 以便提交处理该窗体的下拉列表中值将 GenreId 和 ArtistId，是将设置它们的唱片集属性。</span><span class="sxs-lookup"><span data-stu-id="e43b6-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="e43b6-162">这些下拉列表中值返回到使用此时对象，它只需为该目的构建窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="e43b6-163">这是使用如下代码：</span><span class="sxs-lookup"><span data-stu-id="e43b6-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="e43b6-164">如你所见操作方法代码中，三个参数用于创建此对象：</span><span class="sxs-lookup"><span data-stu-id="e43b6-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="e43b6-165">将显示下拉列表中的项的列表。</span><span class="sxs-lookup"><span data-stu-id="e43b6-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="e43b6-166">请注意，这不是仅仅是一个字符串-我们正在传递风格的列表。</span><span class="sxs-lookup"><span data-stu-id="e43b6-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="e43b6-167">下一个参数传递给此时是选择值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="e43b6-168">此此时如何知道如何预选择列表中的项。</span><span class="sxs-lookup"><span data-stu-id="e43b6-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="e43b6-169">这将会更容易了解何时我们了解一下编辑窗体中，这是非常类似。</span><span class="sxs-lookup"><span data-stu-id="e43b6-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="e43b6-170">最后一个参数是要显示的属性。</span><span class="sxs-lookup"><span data-stu-id="e43b6-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="e43b6-171">在这种情况下，这指示该 Genre.Name 属性什么将向用户显示。</span><span class="sxs-lookup"><span data-stu-id="e43b6-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="e43b6-172">这一点，然后，创建 HTTP GET 操作是非常简单-两个 SelectLists 添加到 ViewBag，并没有任何模型对象传递到窗体 （因为它尚未尚未创建）。</span><span class="sxs-lookup"><span data-stu-id="e43b6-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="e43b6-173">HTML 帮助器，在创建视图中显示相应的删除列表</span><span class="sxs-lookup"><span data-stu-id="e43b6-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="e43b6-174">由于我们已讨论的下拉列表值传递到该视图的方式，让我们快速了解一下视图以查看显示这些值的方式。</span><span class="sxs-lookup"><span data-stu-id="e43b6-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="e43b6-175">在查看代码 (/ Views/StoreManager/Create.cshtml)，你将看到进行以下调用以显示流派放下。</span><span class="sxs-lookup"><span data-stu-id="e43b6-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="e43b6-176">这称为的 HTML 帮助器的实用工具方法，后者将执行一项常见视图任务。</span><span class="sxs-lookup"><span data-stu-id="e43b6-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="e43b6-177">HTML 帮助程序是在使我们视图代码保持简洁、 更具可读性中非常有用。</span><span class="sxs-lookup"><span data-stu-id="e43b6-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="e43b6-178">Html.DropDownList 帮助器提供的 ASP.NET MVC，但正如我们看到更高版本是可以创建我们自己帮助器查看代码，我们将在我们的应用程序中重复使用。</span><span class="sxs-lookup"><span data-stu-id="e43b6-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="e43b6-179">只需会告知其中到 get 列表后，若要显示，和哪些值 （如果有） 应预先选择的两部分内容-Html.DropDownList 调用。</span><span class="sxs-lookup"><span data-stu-id="e43b6-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="e43b6-180">第一个参数，GenreId，指示下拉列表来查找名 GenreId 为模型或 ViewBag 中的值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="e43b6-181">第二个参数用于指示要显示的值为最初在下拉列表中选择。</span><span class="sxs-lookup"><span data-stu-id="e43b6-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="e43b6-182">由于此窗体是创建窗体，没有要预先选择的值和传递 String.Empty。</span><span class="sxs-lookup"><span data-stu-id="e43b6-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="e43b6-183">处理发布窗体值</span><span class="sxs-lookup"><span data-stu-id="e43b6-183">Handling the Posted Form values</span></span>

<span data-ttu-id="e43b6-184">如之前所述，有两个与每个窗体关联的操作方法。</span><span class="sxs-lookup"><span data-stu-id="e43b6-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="e43b6-185">第一个处理 HTTP GET 请求，并显示窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="e43b6-186">第二个处理 HTTP POST 请求，将包含提交窗体值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="e43b6-187">请注意，控制器操作 [HttpPost] 属性，它指示 ASP.NET MVC 它应仅响应 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="e43b6-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="e43b6-188">此操作具有四个职责：</span><span class="sxs-lookup"><span data-stu-id="e43b6-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="e43b6-189">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="e43b6-189">Read the form values</span></span>
- 2. <span data-ttu-id="e43b6-190">检查是否窗体值传递的任何验证规则</span><span class="sxs-lookup"><span data-stu-id="e43b6-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="e43b6-191">如果表单提交有效，保存数据并显示更新的列表</span><span class="sxs-lookup"><span data-stu-id="e43b6-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="e43b6-192">如果表单提交不是有效的则重新显示具有验证错误的窗体</span><span class="sxs-lookup"><span data-stu-id="e43b6-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="e43b6-193">使用模型绑定的读取窗体值</span><span class="sxs-lookup"><span data-stu-id="e43b6-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="e43b6-194">控制器操作正在处理包括标题、 价格和 AlbumArtUrl GenreId 和 ArtistId 值 （从下拉列表） 和文本框中值的表单提交。</span><span class="sxs-lookup"><span data-stu-id="e43b6-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="e43b6-195">可以直接访问窗体值时，更好的方法是使用内置于 ASP.NET MVC 的模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="e43b6-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="e43b6-196">当控制器操作所需模型类型作为参数时，则 ASP.NET MVC 将尝试填充该类型使用窗体输入 （以及路由和查询字符串值） 的对象。</span><span class="sxs-lookup"><span data-stu-id="e43b6-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="e43b6-197">这是通过寻找的值名称匹配的模型对象的属性，例如当设置新唱片集对象的 GenreId 值时，它会查找 GenreId 同名的输入。</span><span class="sxs-lookup"><span data-stu-id="e43b6-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="e43b6-198">创建视图使用 ASP.NET MVC 中的标准方法时，将始终使用属性名称作为输入的字段名称，因此这字段名称将仅匹配呈现窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="e43b6-199">验证模型</span><span class="sxs-lookup"><span data-stu-id="e43b6-199">Validating the Model</span></span>

<span data-ttu-id="e43b6-200">通过简单调用 ModelState.IsValid 验证模型。</span><span class="sxs-lookup"><span data-stu-id="e43b6-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="e43b6-201">我们尚未将任何验证规则添加到我们唱片集的类，但-我们将执行在某种程度-因此现在此检查没有太多工作要做。</span><span class="sxs-lookup"><span data-stu-id="e43b6-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="e43b6-202">重要的是此 ModelStat.IsValid 检查将适应我们置于我们的模型，以便将来对验证规则的更改将不需要任何更新到的控制器操作代码的验证规则。</span><span class="sxs-lookup"><span data-stu-id="e43b6-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="e43b6-203">保存的已提交的值</span><span class="sxs-lookup"><span data-stu-id="e43b6-203">Saving the submitted values</span></span>

<span data-ttu-id="e43b6-204">如果表单提交通过验证后，就可以将值保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="e43b6-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="e43b6-205">使用实体框架，只需将模型添加到专辑集合并调用 SaveChanges。</span><span class="sxs-lookup"><span data-stu-id="e43b6-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="e43b6-206">实体框架生成合适的 SQL 命令，来保留的值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="e43b6-207">在保存后的数据，我们将重定向回唱片集的列表，我们可以看到我们的更新。</span><span class="sxs-lookup"><span data-stu-id="e43b6-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="e43b6-208">这是通过返回 RedirectToAction 具有我们要显示执行的控制器操作的名称。</span><span class="sxs-lookup"><span data-stu-id="e43b6-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="e43b6-209">在这种情况下，这是 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="e43b6-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="e43b6-210">显示具有验证错误的无效的窗体提交</span><span class="sxs-lookup"><span data-stu-id="e43b6-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="e43b6-211">在无效的窗体输入的情况下的下拉列表中值添加到 ViewBag （如 HTTP GET） 和绑定的模型值会传递回视图以显示。</span><span class="sxs-lookup"><span data-stu-id="e43b6-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="e43b6-212">验证错误将自动显示使用@Html.ValidationMessageFor的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="e43b6-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="e43b6-213">测试创建窗体</span><span class="sxs-lookup"><span data-stu-id="e43b6-213">Testing the Create Form</span></span>

<span data-ttu-id="e43b6-214">若要测试这 out，运行的应用程序和浏览到 /StoreManager/创建 /-这将显示返回的 StoreController 创建 HTTP GET 方法的空白窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="e43b6-215">填写一些值，并单击创建按钮以提交该表单。</span><span class="sxs-lookup"><span data-stu-id="e43b6-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="e43b6-216">处理编辑</span><span class="sxs-lookup"><span data-stu-id="e43b6-216">Handling Edits</span></span>

<span data-ttu-id="e43b6-217">编辑操作对 （HTTP GET 和 HTTP POST） 都非常类似于我们刚刚在查看过的创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="e43b6-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="e43b6-218">由于编辑方案涉及使用现有的唱片集，编辑 HTTP GET 方法将加载唱片集基于"id"参数传入通过路由。</span><span class="sxs-lookup"><span data-stu-id="e43b6-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="e43b6-219">如我们之前介绍了中的详细信息的控制器操作，这段代码用于检索通过 AlbumId 唱片集都是相同的。</span><span class="sxs-lookup"><span data-stu-id="e43b6-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="e43b6-220">创建与 / HTTP GET 方法，通过 ViewBag 将返回的下拉列表值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="e43b6-221">这使得我们可以将唱片集作为我们模型对象返回到视图 （其中强类型化为唱片集类） 同时通过 ViewBag 传递其他数据 （例如风格的列表）。</span><span class="sxs-lookup"><span data-stu-id="e43b6-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="e43b6-222">编辑 HTTP POST 操作是非常类似于创建的 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="e43b6-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="e43b6-223">唯一的区别是而不是将新唱片集添加到数据库。唱片集集合中，我们发现唱片集的当前实例使用 db。Entry(album) 并将其状态设置为已修改。</span><span class="sxs-lookup"><span data-stu-id="e43b6-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="e43b6-224">这将告知我们正在修改现有唱片集而不是创建一个新实体框架。</span><span class="sxs-lookup"><span data-stu-id="e43b6-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="e43b6-225">我们可以通过运行应用程序并浏览到/StoreManger/，然后单击唱片集的编辑链接来测试此项。</span><span class="sxs-lookup"><span data-stu-id="e43b6-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="e43b6-226">此时将显示通过编辑 HTTP GET 方法显示的编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="e43b6-227">填写一些值，并单击保存按钮。</span><span class="sxs-lookup"><span data-stu-id="e43b6-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="e43b6-228">这将窗体发送、 保存值，并返回我们到唱片集列表中，显示已更新值。</span><span class="sxs-lookup"><span data-stu-id="e43b6-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="e43b6-229">处理删除</span><span class="sxs-lookup"><span data-stu-id="e43b6-229">Handling Deletion</span></span>

<span data-ttu-id="e43b6-230">删除遵循同一模式，编辑以及创建、 使用一个控制器操作以显示确认窗体中，以及另一个控制器操作处理提交窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="e43b6-231">HTTP GET 删除控制器操作正是我们之前的存储管理器详细信息控制器操作相同。</span><span class="sxs-lookup"><span data-stu-id="e43b6-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="e43b6-232">我们为唱片集类型，使用删除视图内容模板显示了一个强类型的窗体。</span><span class="sxs-lookup"><span data-stu-id="e43b6-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="e43b6-233">删除模板显示所有字段的模型，但我们可以很多简化该列表。</span><span class="sxs-lookup"><span data-stu-id="e43b6-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="e43b6-234">将在 /Views/StoreManager/Delete.cshtml 中的查看代码更改为以下。</span><span class="sxs-lookup"><span data-stu-id="e43b6-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="e43b6-235">此时将显示一条简化的删除确认消息。</span><span class="sxs-lookup"><span data-stu-id="e43b6-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="e43b6-236">单击删除按钮使窗体发布回执行 DeleteConfirmed 操作的服务器。</span><span class="sxs-lookup"><span data-stu-id="e43b6-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="e43b6-237">我们 HTTP POST 删除控制器操作将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e43b6-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="e43b6-238">加载按 ID 唱片集</span><span class="sxs-lookup"><span data-stu-id="e43b6-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="e43b6-239">将其删除唱片集并保存更改</span><span class="sxs-lookup"><span data-stu-id="e43b6-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="e43b6-240">重定向到索引中，显示唱片集已从列表中删除</span><span class="sxs-lookup"><span data-stu-id="e43b6-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="e43b6-241">若要测试这一点，运行应用程序，并浏览到 /StoreManager。</span><span class="sxs-lookup"><span data-stu-id="e43b6-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="e43b6-242">从列表中选择唱片集，然后单击删除链接。</span><span class="sxs-lookup"><span data-stu-id="e43b6-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="e43b6-243">此时将显示我们删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="e43b6-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="e43b6-244">单击删除按钮移除唱片集，并返回我们为存储管理器索引页，可显示唱片集已被删除。</span><span class="sxs-lookup"><span data-stu-id="e43b6-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="e43b6-245">使用自定义 HTML 帮助程序进行截断操作文本</span><span class="sxs-lookup"><span data-stu-id="e43b6-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="e43b6-246">我们与我们的存储管理器索引页面提供一个潜在问题。</span><span class="sxs-lookup"><span data-stu-id="e43b6-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="e43b6-247">我们唱片集的标题和艺术家名称的属性都可以是足够长，无法引发关闭我们表格式设置。</span><span class="sxs-lookup"><span data-stu-id="e43b6-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="e43b6-248">我们将创建用于使我们能够轻松地截断这些属性和我们的视图中的其他属性的自定义 HTML 帮助。</span><span class="sxs-lookup"><span data-stu-id="e43b6-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="e43b6-249">Razor 的@helper语法变得很容易在您的视图中创建您自己使用的帮助器函数。</span><span class="sxs-lookup"><span data-stu-id="e43b6-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="e43b6-250">打开 /Views/StoreManager/Index.cshtml 视图并添加以下代码直接@model行。</span><span class="sxs-lookup"><span data-stu-id="e43b6-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="e43b6-251">此帮助程序方法采用一个字符串，以允许的最大长度。</span><span class="sxs-lookup"><span data-stu-id="e43b6-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="e43b6-252">帮助器提供的文本短于指定的长度时，将其作为输出-是。</span><span class="sxs-lookup"><span data-stu-id="e43b6-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="e43b6-253">如果它的长度，然后它将截断的文本，并且"..."剩余时间内呈现。</span><span class="sxs-lookup"><span data-stu-id="e43b6-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="e43b6-254">现在我们可以使用我们截断的帮助器以确保唱片集标题和艺术家名称属性不超过 25 个字符。</span><span class="sxs-lookup"><span data-stu-id="e43b6-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="e43b6-255">使用我们新截断帮助器的完整视图代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="e43b6-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="e43b6-256">现在我们浏览 /StoreManager/ URL，专辑和标题将保留下面我们最大长度。</span><span class="sxs-lookup"><span data-stu-id="e43b6-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="e43b6-257">注意： 这将显示简单的情况下的创建和使用程序的帮助程序在一个视图中。</span><span class="sxs-lookup"><span data-stu-id="e43b6-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="e43b6-258">若要了解有关创建可以在整个站点使用的帮助器的详细信息，请参阅我的博客文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="e43b6-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="e43b6-259">[上一页](mvc-music-store-part-4.md)
> [下一页](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="e43b6-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
