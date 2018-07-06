---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第 5 部分： 编辑窗体和模板化 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 5 部分介绍如何编辑窗体和模板化。
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: acb4a4c427870e375ff19823f0bdfa208438e899
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835996"
---
<a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="e3e97-104">第 5 部分： 编辑窗体和模板化</span><span class="sxs-lookup"><span data-stu-id="e3e97-104">Part 5: Edit Forms and Templating</span></span>
====================
<span data-ttu-id="e3e97-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="e3e97-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="e3e97-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3e97-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="e3e97-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="e3e97-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="e3e97-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="e3e97-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="e3e97-109">第 5 部分介绍如何编辑窗体和模板化。</span><span class="sxs-lookup"><span data-stu-id="e3e97-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="e3e97-110">在过去的章中，我们已从数据库加载数据并显示它。</span><span class="sxs-lookup"><span data-stu-id="e3e97-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="e3e97-111">在本章中，我们还将启用编辑数据。</span><span class="sxs-lookup"><span data-stu-id="e3e97-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="e3e97-112">创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="e3e97-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="e3e97-113">我们将首先创建名为的新控制器**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="e3e97-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="e3e97-114">此控制器中，我们将充分利用 ASP.NET MVC 3 Tools Update 中提供的基架功能。</span><span class="sxs-lookup"><span data-stu-id="e3e97-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="e3e97-115">设置添加控制器对话框的选项，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3e97-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="e3e97-116">当你单击添加按钮时，会看到 ASP.NET MVC 3 基架机制为您完成大量的工作：</span><span class="sxs-lookup"><span data-stu-id="e3e97-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="e3e97-117">它使用实体框架局部变量创建新 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="e3e97-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="e3e97-118">它将 StoreManager 文件夹添加到项目的 Views 文件夹</span><span class="sxs-lookup"><span data-stu-id="e3e97-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="e3e97-119">它将添加 Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml 和 Index.cshtml 视图中，强类型化为唱片集类</span><span class="sxs-lookup"><span data-stu-id="e3e97-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="e3e97-120">新 StoreManager 控制器类包括 CRUD （创建、 读取、 更新、 删除） 控制器操作在其知道如何处理与唱片集的模型和我们的 Entity Framework 上下文用于数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="e3e97-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="e3e97-121">修改基架生成的视图</span><span class="sxs-lookup"><span data-stu-id="e3e97-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="e3e97-122">请务必记住，虽然我们已生成此代码，这是标准的 ASP.NET MVC 代码，就像已在本教程中，我们已编写的一样。</span><span class="sxs-lookup"><span data-stu-id="e3e97-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="e3e97-123">它可用于为你节省将会花费的时间编写样板控制器代码和手动创建强类型化的视图，但这不是生成的代码可能会看到前面加上有关如何不能更改的注释中的可怕警告类型代码。</span><span class="sxs-lookup"><span data-stu-id="e3e97-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="e3e97-124">这是你的代码，并且你应将其更改。</span><span class="sxs-lookup"><span data-stu-id="e3e97-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="e3e97-125">因此，让我们先快速编辑到 StoreManager 索引视图 (/ Views/StoreManager/Index.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="e3e97-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="e3e97-126">此视图将显示一个表，该表列出了在我们的存储与编辑相册 / 详细信息 / 删除的链接，并包含唱片集的公共属性。</span><span class="sxs-lookup"><span data-stu-id="e3e97-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="e3e97-127">我们将删除 AlbumArtUrl 字段，因为它不是在此显示中非常有用。</span><span class="sxs-lookup"><span data-stu-id="e3e97-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="e3e97-128">中&lt;表&gt;部分的查看代码中，删除&lt;th&gt;并&lt;td&gt;元素周围 AlbumArtUrl 引用，如以下突出显示的行所示：</span><span class="sxs-lookup"><span data-stu-id="e3e97-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="e3e97-129">经过修改的视图代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="e3e97-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="e3e97-130">初步了解存储管理器</span><span class="sxs-lookup"><span data-stu-id="e3e97-130">A first look at the Store Manager</span></span>

<span data-ttu-id="e3e97-131">现在运行应用程序并浏览到/StoreManager /。</span><span class="sxs-lookup"><span data-stu-id="e3e97-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="e3e97-132">此时将显示存储管理器我们只需修改索引，其中包含用于编辑的详细信息，和删除链接的存储中显示的唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="e3e97-133">单击编辑链接显示的唱片集、 流派和艺术家包括下拉列表的字段的编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="e3e97-134">单击"返回到列表"链接，在底部，然后单击唱片集的详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="e3e97-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="e3e97-135">这将显示单个唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e3e97-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="e3e97-136">同样，单击列表链接回，然后单击删除链接。</span><span class="sxs-lookup"><span data-stu-id="e3e97-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="e3e97-137">此时将显示确认对话框中，显示的唱片集详细信息并询问我们要确保我们想要将其删除。</span><span class="sxs-lookup"><span data-stu-id="e3e97-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="e3e97-138">单击底部的删除按钮，将删除唱片集，并使你返回到索引页，其中显示了已删除的唱片集。</span><span class="sxs-lookup"><span data-stu-id="e3e97-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="e3e97-139">我们还没有完成与存储管理器，但我们具有有效的控制器和视图的 CRUD 操作从启动代码。</span><span class="sxs-lookup"><span data-stu-id="e3e97-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="e3e97-140">查看存储管理器控制器代码</span><span class="sxs-lookup"><span data-stu-id="e3e97-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="e3e97-141">存储管理器控制器包含大量的代码。</span><span class="sxs-lookup"><span data-stu-id="e3e97-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="e3e97-142">让我们通过此从上到下。</span><span class="sxs-lookup"><span data-stu-id="e3e97-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="e3e97-143">该控制器包含一个 MVC 控制器，以及对我们的模型命名空间的引用的某些标准命名空间。</span><span class="sxs-lookup"><span data-stu-id="e3e97-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="e3e97-144">控制器有 MusicStoreEntities，使用每个控制器操作进行数据访问的专用实例。</span><span class="sxs-lookup"><span data-stu-id="e3e97-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="e3e97-145">存储管理器索引和详细信息操作</span><span class="sxs-lookup"><span data-stu-id="e3e97-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="e3e97-146">索引视图中检索唱片集，包括每个唱片集的被引用的流派和艺术家信息，正如我们以前看到的应用商店浏览方法上工作时的列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="e3e97-147">索引视图，以便它可以使控制器进行高效的查询的原始请求中的此信息显示每个唱片集的类型名称和艺术家姓名关注对所链接的对象的引用。</span><span class="sxs-lookup"><span data-stu-id="e3e97-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="e3e97-148">StoreManager 控制器的详细信息控制器操作的工作方式，我们编写了以前为-它会询问是否唱片集的存储控制器的详细信息操作完全相同的 ID 使用 find （） 方法，然后将其返回到视图。</span><span class="sxs-lookup"><span data-stu-id="e3e97-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="e3e97-149">创建操作方法</span><span class="sxs-lookup"><span data-stu-id="e3e97-149">The Create Action Methods</span></span>

<span data-ttu-id="e3e97-150">创建操作方法是稍有不同的为止，我们所看到的因为它们处理窗体输入。</span><span class="sxs-lookup"><span data-stu-id="e3e97-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="e3e97-151">当用户首次访问时 /StoreManager/创建/他们将看到一个空窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="e3e97-152">此 HTML 页将包含&lt;窗体&gt;元素，其中包含下拉列表中，文本框中输入的元素可在其中输入唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e3e97-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="e3e97-153">唱片集窗体值中填充用户后，他们可以按"保存"按钮提交这些更改回我们的应用程序保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="e3e97-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="e3e97-154">当用户按"保存"按钮&lt;窗体&gt;将执行 HTTP POST 回 /StoreManager/创建/URL，并提交&lt;窗体&gt;作为 HTTP POST 的一部分的值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="e3e97-155">ASP.NET MVC 使我们能够轻松地通过使我们能够实现两个单独的"创建"操作方法中我们 StoreManagerController 类-另一个用于处理初始的 HTTP GET 浏览到 /StoreManager/Create 拆分这两个 URL 调用方案的逻辑/ URL 和其他处理 HTTP POST 提交的更改。</span><span class="sxs-lookup"><span data-stu-id="e3e97-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="e3e97-156">将信息传递给视图使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="e3e97-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="e3e97-157">我们之前在本教程中已使用 ViewBag 但探讨它得还不够。</span><span class="sxs-lookup"><span data-stu-id="e3e97-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="e3e97-158">ViewBag 使我们能够将信息传递给视图，而无需使用强类型化的模型对象。</span><span class="sxs-lookup"><span data-stu-id="e3e97-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="e3e97-159">在这种情况下，需要将这两个流派和艺术家的列表传递给窗体来填充下拉列表中，我们编辑 HTTP-GET 控制器操作和执行此操作的最简单方法是将其返回作为 ViewBag 项。</span><span class="sxs-lookup"><span data-stu-id="e3e97-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="e3e97-160">ViewBag 是动态对象，这意味着你可以无需编写代码来定义这些属性键入 ViewBag.Foo 或 ViewBag.YourNameHere。</span><span class="sxs-lookup"><span data-stu-id="e3e97-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="e3e97-161">在这种情况下，控制器代码使用 ViewBag.GenreId 和 ViewBag.ArtistId，以便处理该窗体提交的下拉列表中值将 GenreId 和 ArtistId，即会设置它们的唱片集属性。</span><span class="sxs-lookup"><span data-stu-id="e3e97-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="e3e97-162">这些下拉列表中的值返回到窗体使用 SelectList 对象，它专门为此目的。</span><span class="sxs-lookup"><span data-stu-id="e3e97-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="e3e97-163">这是使用如下代码：</span><span class="sxs-lookup"><span data-stu-id="e3e97-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="e3e97-164">您可以看到从操作方法代码，三个参数是要用于创建此对象：</span><span class="sxs-lookup"><span data-stu-id="e3e97-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="e3e97-165">将显示在下拉列表中的项的列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="e3e97-166">请注意，这并不只是一个字符串-我们传入影片类型列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="e3e97-167">下一个参数传递给 SelectList 是所选的值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="e3e97-168">此 SelectList 如何知道如何预选择列表中的项。</span><span class="sxs-lookup"><span data-stu-id="e3e97-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="e3e97-169">这将是更易于理解时我们了解一下编辑窗体，这是非常相似。</span><span class="sxs-lookup"><span data-stu-id="e3e97-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="e3e97-170">最后一个参数是要显示的属性。</span><span class="sxs-lookup"><span data-stu-id="e3e97-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="e3e97-171">在这种情况下，这指示 Genre.Name 属性什么将向用户显示。</span><span class="sxs-lookup"><span data-stu-id="e3e97-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="e3e97-172">这一点后，然后，创建 HTTP GET 操作是非常简单-两个 SelectLists 添加到 ViewBag，并没有模型对象传递给窗体 （因为它尚未创建）。</span><span class="sxs-lookup"><span data-stu-id="e3e97-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="e3e97-173">若要在创建视图中显示在删除列表的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="e3e97-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="e3e97-174">由于我们已经讨论过的下拉列表值传递到视图的方式，让我们快速看一下视图以查看这些值的显示方式。</span><span class="sxs-lookup"><span data-stu-id="e3e97-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="e3e97-175">查看代码中 (/ Views/StoreManager/Create.cshtml)，可以看到进行以下调用以显示流派下拉列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="e3e97-176">这被称为 HTML 帮助器的实用工具方法，后者将执行一项常见视图任务。</span><span class="sxs-lookup"><span data-stu-id="e3e97-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="e3e97-177">HTML 帮助程序是在保持简洁和可读的我们查看代码中非常有用。</span><span class="sxs-lookup"><span data-stu-id="e3e97-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="e3e97-178">Html.DropDownList 帮助程序提供的 ASP.NET MVC 中，但我们稍后会看到它是可以创建适用于查看代码，我们将在我们的应用程序中重复使用我们的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="e3e97-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="e3e97-179">Html.DropDownList 调用只需告知两件事-何处进行 get 列表后，若要显示，和哪些值 （如果有） 应预先选择。</span><span class="sxs-lookup"><span data-stu-id="e3e97-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="e3e97-180">第一个参数，GenreId，告知 DropDownList 以寻找名 GenreId 为模型或 ViewBag 中的值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="e3e97-181">第二个参数用于指示要显示的值最初在下拉列表中选择。</span><span class="sxs-lookup"><span data-stu-id="e3e97-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="e3e97-182">由于此窗体是创建窗体，因此没有要预先选择的值，并传递 String.Empty。</span><span class="sxs-lookup"><span data-stu-id="e3e97-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="e3e97-183">处理发布窗体值</span><span class="sxs-lookup"><span data-stu-id="e3e97-183">Handling the Posted Form values</span></span>

<span data-ttu-id="e3e97-184">如之前所述，有两个操作方法与每个窗体相关联。</span><span class="sxs-lookup"><span data-stu-id="e3e97-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="e3e97-185">第一个处理 HTTP GET 请求，并显示该窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="e3e97-186">第二个处理 HTTP POST 请求，其中包含的提交的窗体值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="e3e97-187">请注意控制器操作具有 [HttpPost] 属性，它将告诉 ASP.NET MVC 它只应响应 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="e3e97-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="e3e97-188">此操作有四个职责：</span><span class="sxs-lookup"><span data-stu-id="e3e97-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="e3e97-189">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="e3e97-189">Read the form values</span></span>
- 2. <span data-ttu-id="e3e97-190">检查窗体值是否传递的任何验证规则</span><span class="sxs-lookup"><span data-stu-id="e3e97-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="e3e97-191">如果表单提交有效，将数据保存并显示更新的列表</span><span class="sxs-lookup"><span data-stu-id="e3e97-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="e3e97-192">如果提交窗体不是有效的重新显示具有验证错误的窗体</span><span class="sxs-lookup"><span data-stu-id="e3e97-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="e3e97-193">使用模型绑定的读取窗体值</span><span class="sxs-lookup"><span data-stu-id="e3e97-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="e3e97-194">控制器操作正在处理包括用于标题、 价格和 AlbumArtUrl GenreId 和 ArtistId 值 （从下拉列表） 和文本框值的窗体提交。</span><span class="sxs-lookup"><span data-stu-id="e3e97-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="e3e97-195">可以直接访问窗体值时，更好的方法是使用内置到 ASP.NET MVC 模型绑定功能。</span><span class="sxs-lookup"><span data-stu-id="e3e97-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="e3e97-196">模型类型作为参数的控制器操作时，ASP.NET MVC 将尝试填充该类型使用窗体输入 （以及路由和查询字符串值） 的对象。</span><span class="sxs-lookup"><span data-stu-id="e3e97-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="e3e97-197">此查找的值名称匹配的模型对象的属性，例如，它会设置新的唱片集对象的 GenreId 值时，它会查找与名称 GenreId 的输入。</span><span class="sxs-lookup"><span data-stu-id="e3e97-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="e3e97-198">创建 ASP.NET MVC 中使用的标准方法的视图时，将始终为输入的字段名称，使用属性名称，因此此字段名称将只匹配呈现窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="e3e97-199">验证模型</span><span class="sxs-lookup"><span data-stu-id="e3e97-199">Validating the Model</span></span>

<span data-ttu-id="e3e97-200">通过简单调用 ModelState.IsValid 验证模型。</span><span class="sxs-lookup"><span data-stu-id="e3e97-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="e3e97-201">我们尚未向我们唱片集的类添加任何验证规则，但-我们将执行在位-好了，现在这一检查没有太大关系。</span><span class="sxs-lookup"><span data-stu-id="e3e97-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="e3e97-202">重要的是此 ModelStat.IsValid 检查将适应，我们在我们的模型，以便将来对验证规则的更改将不需要任何更新到控制器操作代码的验证规则。</span><span class="sxs-lookup"><span data-stu-id="e3e97-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="e3e97-203">保存已提交的值</span><span class="sxs-lookup"><span data-stu-id="e3e97-203">Saving the submitted values</span></span>

<span data-ttu-id="e3e97-204">如果提交窗体通过验证，就可以将值保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="e3e97-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="e3e97-205">使用实体框架，只需将模型添加到唱片集集合并调用 SaveChanges。</span><span class="sxs-lookup"><span data-stu-id="e3e97-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="e3e97-206">实体框架生成相应的 SQL 命令，以保留的值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="e3e97-207">在保存后的数据，我们将重定向回唱片集的列表，我们可以看到我们的更新。</span><span class="sxs-lookup"><span data-stu-id="e3e97-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="e3e97-208">这是通过返回 RedirectToAction 与我们要显示的控制器操作的名称。</span><span class="sxs-lookup"><span data-stu-id="e3e97-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="e3e97-209">在这种情况下，这是 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="e3e97-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="e3e97-210">显示无效的窗体提交带有验证错误</span><span class="sxs-lookup"><span data-stu-id="e3e97-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="e3e97-211">在无效的窗体输入的情况下的下拉列表中值添加到 ViewBag （如 HTTP GET） 和绑定的模型值传递回视图进行显示。</span><span class="sxs-lookup"><span data-stu-id="e3e97-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="e3e97-212">验证错误将自动显示使用@Html.ValidationMessageFor的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="e3e97-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="e3e97-213">测试创建窗体</span><span class="sxs-lookup"><span data-stu-id="e3e97-213">Testing the Create Form</span></span>

<span data-ttu-id="e3e97-214">若要测试此扩展，运行的应用程序和浏览到 /StoreManager/创建 /-这将显示您 StoreController 创建 HTTP GET 方法返回的空白表单。</span><span class="sxs-lookup"><span data-stu-id="e3e97-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="e3e97-215">填写一些值并单击创建按钮提交窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="e3e97-216">处理编辑</span><span class="sxs-lookup"><span data-stu-id="e3e97-216">Handling Edits</span></span>

<span data-ttu-id="e3e97-217">编辑操作对 （HTTP GET 和 HTTP POST） 都非常类似于我们刚了解的创建操作方法。</span><span class="sxs-lookup"><span data-stu-id="e3e97-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="e3e97-218">由于编辑方案涉及使用现有的相册，编辑 HTTP-GET 方法加载的唱片集基于"id"参数传递通过路由中。</span><span class="sxs-lookup"><span data-stu-id="e3e97-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="e3e97-219">如我们以前介绍了中的详细信息控制器操作，这段代码用于检索通过 AlbumId 唱片集都是相同的。</span><span class="sxs-lookup"><span data-stu-id="e3e97-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="e3e97-220">创建与 / HTTP GET 方法，通过 ViewBag 返回的下拉列表值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="e3e97-221">这使得我们可以将唱片集作为我们的模型对象返回到视图 （这强类型化的唱片集类） 时通过 ViewBag 传递其他数据 （例如影片类型列表）。</span><span class="sxs-lookup"><span data-stu-id="e3e97-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="e3e97-222">编辑 HTTP POST 操作是非常类似于创建 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="e3e97-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="e3e97-223">唯一的区别是，而不是向数据库添加新唱片集。唱片集集合中，我们要查找唱片集的当前实例使用 db。Entry(album) 并将其状态设置为已修改。</span><span class="sxs-lookup"><span data-stu-id="e3e97-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="e3e97-224">这会告诉实体框架，我们正在修改现有而不是创建一个新的相册。</span><span class="sxs-lookup"><span data-stu-id="e3e97-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="e3e97-225">我们可以通过运行应用程序并浏览到/StoreManger/，然后单击唱片集的编辑链接它进行测试。</span><span class="sxs-lookup"><span data-stu-id="e3e97-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="e3e97-226">此时将显示所示编辑 HTTP GET 方法的编辑表单。</span><span class="sxs-lookup"><span data-stu-id="e3e97-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="e3e97-227">填写一些值并单击保存按钮。</span><span class="sxs-lookup"><span data-stu-id="e3e97-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="e3e97-228">此发布窗体、 保存值，并返回我们到唱片集列表中，显示已更新值。</span><span class="sxs-lookup"><span data-stu-id="e3e97-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="e3e97-229">处理删除</span><span class="sxs-lookup"><span data-stu-id="e3e97-229">Handling Deletion</span></span>

<span data-ttu-id="e3e97-230">删除遵循与编辑和创建，使用一个控制器操作可以确认窗体，显示和另一个控制器操作来处理提交窗体相同的模式。</span><span class="sxs-lookup"><span data-stu-id="e3e97-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="e3e97-231">HTTP GET 删除控制器操作正是我们之前的存储管理器详细信息控制器操作相同。</span><span class="sxs-lookup"><span data-stu-id="e3e97-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="e3e97-232">我们显示为唱片集类型，使用 Delete 视图内容模板的强类型化的窗体。</span><span class="sxs-lookup"><span data-stu-id="e3e97-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="e3e97-233">删除模板显示所有字段的模型，但我们可以相当简化该列表。</span><span class="sxs-lookup"><span data-stu-id="e3e97-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="e3e97-234">更改为以下 /Views/StoreManager/Delete.cshtml 中的查看代码。</span><span class="sxs-lookup"><span data-stu-id="e3e97-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="e3e97-235">此时将显示简化的删除确认。</span><span class="sxs-lookup"><span data-stu-id="e3e97-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="e3e97-236">单击删除按钮后，窗体会回发到服务器，执行 DeleteConfirmed 操作。</span><span class="sxs-lookup"><span data-stu-id="e3e97-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="e3e97-237">我们 HTTP POST 删除控制器操作将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e3e97-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="e3e97-238">加载的唱片集的 ID</span><span class="sxs-lookup"><span data-stu-id="e3e97-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="e3e97-239">将其删除唱片集并保存更改</span><span class="sxs-lookup"><span data-stu-id="e3e97-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="e3e97-240">重定向到显示唱片集已从列表中删除的索引</span><span class="sxs-lookup"><span data-stu-id="e3e97-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="e3e97-241">若要测试这一点，运行该应用程序，并浏览到 /StoreManager。</span><span class="sxs-lookup"><span data-stu-id="e3e97-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="e3e97-242">从列表中选择唱片集，然后单击删除链接。</span><span class="sxs-lookup"><span data-stu-id="e3e97-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="e3e97-243">此时会显示我们删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="e3e97-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="e3e97-244">单击删除按钮移除唱片集，并返回我们为存储管理器索引页，其中显示了已删除的唱片集。</span><span class="sxs-lookup"><span data-stu-id="e3e97-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="e3e97-245">使用自定义 HTML 帮助器要截断的文本</span><span class="sxs-lookup"><span data-stu-id="e3e97-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="e3e97-246">我们有一个潜在的问题与我们的存储管理器索引页。</span><span class="sxs-lookup"><span data-stu-id="e3e97-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="e3e97-247">唱片集标题和艺术家姓名属性都可以是时间足够长，它们可能会引发关闭我们表格的格式。</span><span class="sxs-lookup"><span data-stu-id="e3e97-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="e3e97-248">我们将创建自定义的 HTML 帮助程序，以便我们能够轻松地截断这些和我们的视图中的其他属性。</span><span class="sxs-lookup"><span data-stu-id="e3e97-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="e3e97-249">Razor 的@helper语法变得很容易在视图中创建您自己使用的帮助器函数。</span><span class="sxs-lookup"><span data-stu-id="e3e97-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="e3e97-250">打开 /Views/StoreManager/Index.cshtml 视图，并添加以下代码直接后的@model行。</span><span class="sxs-lookup"><span data-stu-id="e3e97-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="e3e97-251">此帮助程序方法采用一个字符串，以允许的最大长度。</span><span class="sxs-lookup"><span data-stu-id="e3e97-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="e3e97-252">帮助程序提供的文本是短于指定的长度，如果将其作为输出的是。</span><span class="sxs-lookup"><span data-stu-id="e3e97-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="e3e97-253">如果长度，然后它将截断的文本，并且"..."剩余时间内呈现。</span><span class="sxs-lookup"><span data-stu-id="e3e97-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="e3e97-254">现在我们可以使用我们截断的帮助器以确保不超过 25 个字符的唱片集标题和艺术家姓名的属性。</span><span class="sxs-lookup"><span data-stu-id="e3e97-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="e3e97-255">使用我们新的截断帮助程序的完整视图代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3e97-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="e3e97-256">现在当我们浏览 /StoreManager/ URL 时，唱片集和标题保留下面我们最大长度。</span><span class="sxs-lookup"><span data-stu-id="e3e97-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="e3e97-257">注意： 这将显示创建和使用一个帮助程序在一个视图中的简单情况。</span><span class="sxs-lookup"><span data-stu-id="e3e97-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="e3e97-258">若要了解有关创建可在整个站点的帮助程序的详细信息，请参阅我的博客文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="e3e97-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="e3e97-259">[上一页](mvc-music-store-part-4.md)
> [下一页](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="e3e97-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
