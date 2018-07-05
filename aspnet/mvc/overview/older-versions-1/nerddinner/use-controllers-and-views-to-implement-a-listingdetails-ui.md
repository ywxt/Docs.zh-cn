---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |Microsoft Docs
author: microsoft
description: 步骤 4 显示了如何将控制器添加到应用程序充分利用我们的模型为用户提供对数据的列表/详细信息导航体验...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 4fe065e29950a076de07d73205a97399f82f07d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377871"
---
<a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="e0eb2-103">使用控制器和视图实现列表/详细信息 UI</span><span class="sxs-lookup"><span data-stu-id="e0eb2-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>
====================
<span data-ttu-id="e0eb2-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e0eb2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e0eb2-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e0eb2-106">这是一种免费的第 4 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e0eb2-107">步骤 4 显示了如何将控制器添加到应用程序充分利用我们的模型为用户提供 dinners 我们 NerdDinner 的网站上的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="e0eb2-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="e0eb2-109">NerdDinner 步骤 4： 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="e0eb2-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="e0eb2-110">与传统的 web 框架 （经典 ASP、 PHP、 ASP.NET Web 窗体等），传入的 Url 通常映射到磁盘上的文件中。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="e0eb2-111">例如： 所示的请求 url"/ Products.aspx"或"/ Products.php"可能会处理由"Products.aspx"或"Products.php"文件。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="e0eb2-112">基于 web 的 MVC 框架将 Url 映射到服务器代码中以略有不同的方式。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="e0eb2-113">而不是将传入 Url 映射到文件，它们而是将 Url 映射到类上的方法。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="e0eb2-114">这些类称为"控制器"和要负责处理传入的 HTTP 请求，处理用户输入、 检索和保存数据，并确定要发送的响应返回给客户端 （显示 HTML、 下载文件，将重定向到不同URL，等等）。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="e0eb2-115">现在，我们已为 NerdDinner 应用程序生成基本模型，我们下一步将是将控制器添加到应用程序充分利用它来向用户提供 Dinners 我们的网站上的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="e0eb2-116">添加 DinnersController 控制器</span><span class="sxs-lookup"><span data-stu-id="e0eb2-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="e0eb2-117">我们将首先右键单击"控制器"文件夹中的 web 项目，并选择**Add-&gt;控制器**菜单命令 （您还可以执行此命令通过键入 Ctrl M、 Ctrl + C）：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="e0eb2-118">这将显示"添加控制器"对话框：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="e0eb2-119">我们将命名的新控制器"DinnersController"，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="e0eb2-120">然后，visual Studio 将添加我们 \Controllers 目录下的 DinnersController.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="e0eb2-121">它还会打开代码编辑器内的新 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="e0eb2-122">向 DinnersController 类添加 index （） 和 Details() 操作方法</span><span class="sxs-lookup"><span data-stu-id="e0eb2-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="e0eb2-123">我们想要启用访问者使用我们的应用程序以浏览即将发布 dinners 的列表，使他们可以单击列表中的任何 Dinner，若要查看其特定详细信息。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="e0eb2-124">我们将发布我们的应用程序从以下 Url 来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="e0eb2-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-125">**URL**</span></span> | <span data-ttu-id="e0eb2-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="e0eb2-127">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-127">*/Dinners/*</span></span> | <span data-ttu-id="e0eb2-128">显示即将到来的 dinners 的 HTML 列表</span><span class="sxs-lookup"><span data-stu-id="e0eb2-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="e0eb2-129">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="e0eb2-130">显示有关特定 dinner 嵌入到 URL – 将匹配的数据库中 dinner DinnerID 中"id"参数指示的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="e0eb2-131">例如： /Dinners/Details/2 将显示有关 Dinner DinnerID 值为 2 的详细信息的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="e0eb2-132">通过将两个公共"操作方法"添加到我们 DinnersController 类，如下面，我们将发布这些 Url 的初始实现：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="e0eb2-133">然后，我们将运行 NerdDinner 应用程序，并使用浏览器来调用它们。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="e0eb2-134">在中键入 *"/ Dinners /"* 的 URL 将导致我们*index （)* 方法运行，然后它将发送回以下响应：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="e0eb2-135">在中键入 *"/ Dinners/详细信息/2"* 的 URL 将导致我们*Details()* 方法来运行，并发送回以下响应：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="e0eb2-136">您可能想知道-ASP.NET MVC 是如何知道要创建我们的 DinnersController 类和调用这些方法？</span><span class="sxs-lookup"><span data-stu-id="e0eb2-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="e0eb2-137">若要了解，让我们快速看一下如何路由的工作原理。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="e0eb2-138">了解 ASP.NET MVC 路由</span><span class="sxs-lookup"><span data-stu-id="e0eb2-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="e0eb2-139">ASP.NET MVC 包括一个功能强大的 URL 路由引擎，提供大量灵活地控制如何将 Url 映射到 controller 类。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="e0eb2-140">它允许我们完全自定义 ASP.NET MVC 如何选择要创建哪种方法来调用它，以及配置不同的方式，变量可以自动分析从 URL/查询字符串和传递给形式参数的方法的控制器类自变量。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="e0eb2-141">它提供灵活地完全针对 SEO （搜索引擎优化） 进行优化站点以及发布任何我们想从应用程序的 URL 结构。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="e0eb2-142">默认情况下，新的 ASP.NET MVC 项目附带了已注册的 URL 路由规则的预配置集。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="e0eb2-143">这使我们能够轻松地开始使用应用程序而无需显式配置的任何内容。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="e0eb2-144">我们的项目 – 我们可以通过双击"Global.asax"文件的我们的项目根目录中打开的"应用程序"类中找不到默认路由规则注册：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="e0eb2-145">此类的"RegisterRoutes"方法中注册的默认 ASP.NET MVC 路由规则：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="e0eb2-146">"路由。MapRoute()"上面的方法调用注册的默认路由规则将传入 Url 映射到 controller 类使用的 URL 格式:"/ {controller} / {action} / {id}"– 其中"controller"是要实例化，控制器类的名称"action"是的名称公共方法来调用它，然后"id"是嵌入到该方法可以作为参数传递到 URL 中的一个可选参数。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="e0eb2-147">传递给"MapRoute()"方法调用的第三个参数是一组的默认值，以便使用它们不存在在 URL 中进行的控制器/操作/id 值 (控制器 ="主页"，操作 ="Index"，Id ="")。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="e0eb2-148">下面是一个表，其中演示如何各种 Url 使用默认值映射"<em>/ {控制器} / {action} / {id}"</em>路由规则：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="e0eb2-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-149">**URL**</span></span> | <span data-ttu-id="e0eb2-150">**控制器类**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-150">**Controller Class**</span></span> | <span data-ttu-id="e0eb2-151">**操作方法**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-151">**Action Method**</span></span> | <span data-ttu-id="e0eb2-152">**传递的参数**</span><span class="sxs-lookup"><span data-stu-id="e0eb2-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e0eb2-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="e0eb2-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-154">DinnersController</span></span> | <span data-ttu-id="e0eb2-155">Details(id)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-155">Details(id)</span></span> | <span data-ttu-id="e0eb2-156">id=2</span><span class="sxs-lookup"><span data-stu-id="e0eb2-156">id=2</span></span> |
| <span data-ttu-id="e0eb2-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="e0eb2-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-158">DinnersController</span></span> | <span data-ttu-id="e0eb2-159">Edit(id)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-159">Edit(id)</span></span> | <span data-ttu-id="e0eb2-160">id=5</span><span class="sxs-lookup"><span data-stu-id="e0eb2-160">id=5</span></span> |
| <span data-ttu-id="e0eb2-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-161">*/Dinners/Create*</span></span> | <span data-ttu-id="e0eb2-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-162">DinnersController</span></span> | <span data-ttu-id="e0eb2-163">Create （)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-163">Create()</span></span> | <span data-ttu-id="e0eb2-164">不可用</span><span class="sxs-lookup"><span data-stu-id="e0eb2-164">N/A</span></span> |
| <span data-ttu-id="e0eb2-165">*/ Dinners*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-165">*/Dinners*</span></span> | <span data-ttu-id="e0eb2-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-166">DinnersController</span></span> | <span data-ttu-id="e0eb2-167">Index （)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-167">Index()</span></span> | <span data-ttu-id="e0eb2-168">不可用</span><span class="sxs-lookup"><span data-stu-id="e0eb2-168">N/A</span></span> |
| <span data-ttu-id="e0eb2-169">*/ 主页*</span><span class="sxs-lookup"><span data-stu-id="e0eb2-169">*/Home*</span></span> | <span data-ttu-id="e0eb2-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-170">HomeController</span></span> | <span data-ttu-id="e0eb2-171">Index （)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-171">Index()</span></span> | <span data-ttu-id="e0eb2-172">不可用</span><span class="sxs-lookup"><span data-stu-id="e0eb2-172">N/A</span></span> |
| */* | <span data-ttu-id="e0eb2-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="e0eb2-173">HomeController</span></span> | <span data-ttu-id="e0eb2-174">Index （)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-174">Index()</span></span> | <span data-ttu-id="e0eb2-175">不可用</span><span class="sxs-lookup"><span data-stu-id="e0eb2-175">N/A</span></span> |

<span data-ttu-id="e0eb2-176">最后三行显示的默认值 (控制器 = 主页，操作 = 索引，Id ="") 正在使用。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="e0eb2-177">因为如果未指定，"Index"方法注册为默认操作名称"/ Dinners"和"/home"Url 原因 index （） 操作方法及其控制器类上调用。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="e0eb2-178">因为如果未指定，"Home"控制器已注册为默认控制器，"/"URL 使 HomeController 要创建和 index （） 操作方法来调用它。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="e0eb2-179">如果您不喜欢这些默认 URL 路由规则，好消息是它们很容易更改-只需在上面的 RegisterRoutes 方法中对其进行编辑。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="e0eb2-180">NerdDinner 应用程序，不过，我们不打算更改任何默认 URL 路由规则 – 我们将只需使用它们作为-是。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="e0eb2-181">使用从我们 DinnersController DinnerRepository</span><span class="sxs-lookup"><span data-stu-id="e0eb2-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="e0eb2-182">让我们现在将为我们的 DinnersController 的当前实现 index （） 和 Details() 操作方法与使用我们的模型的实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="e0eb2-183">我们将使用我们之前生成以实现行为的 DinnerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="e0eb2-184">我们将首先添加引用"NerdDinner.Models"命名空间的"using"语句，然后作为字段，在我们的 DinnerController 类声明的我们 DinnerRepository 实例。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="e0eb2-185">本章稍后我们将介绍"依赖关系注入"的概念并展示控制器能够获取对启用更好单元 DinnerRepository 引用另一种方法，测试 – 但右侧的现在只需创建我们 DinnerRepository 实例如下面的内联。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="e0eb2-186">现在我们已准备好生成 HTML 响应使用我们检索到的数据模型对象。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="e0eb2-187">使用视图和控制器</span><span class="sxs-lookup"><span data-stu-id="e0eb2-187">Using Views with our Controller</span></span>

<span data-ttu-id="e0eb2-188">虽然可以编写在组装 HTML，然后使用我们操作方法中的代码*response.write （)* 帮助器方法来将其发送回客户端，该方法变得相当不便于快速。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="e0eb2-189">更好的方法是为我们只能执行应用程序和数据逻辑内我们 DinnersController 的操作方法，并将然后传递要呈现到单独的"视图"模板，它负责将输出 HTML 形式呈现的 HTML 响应所需的数据它。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="e0eb2-190">正如我们稍后将看到，"查看"模板是文本文件，通常包含 HTML 标记和嵌入的呈现代码的组合。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="e0eb2-191">我们的控制器逻辑分开我们视图呈现带来了几大好处。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="e0eb2-192">特别是它可帮助应用程序代码和 UI 设置的格式呈现代码之间强制清除"关注点分离"。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="e0eb2-193">这样，可以更容易地中隔离单元测试应用程序逻辑与 UI 呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="e0eb2-194">它可以更轻松地更高版本修改 UI 呈现模板，而无需更改应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="e0eb2-195">它可以方便开发人员和设计人员共同协作的项目。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="e0eb2-196">我们可以更新我们 DinnersController 类，以指示我们想要查看模板用于通过更改我们的两个操作方法的方法签名中具有返回类型为"void"改为具有返回类型为"ActionResult"发回 HTML UI 响应。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="e0eb2-197">然后，我们可以调用*View()* 控制器基类要返回上的帮助器方法"ViewResult"对象如下所示：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="e0eb2-198">签名*View()* 我们使用上面的帮助器方法类似于下面：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="e0eb2-199">第一个参数*View()* 帮助器方法是我们想要用于呈现 HTML 响应的视图模板文件的名称。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="e0eb2-200">第二个参数是包含在视图模板呈现的 HTML 响应所需的数据的模型对象。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="e0eb2-201">我们 index （） 操作方法中，我们将调用*View()* 帮助器方法并指示我们想要呈现的 HTML 列表的 dinners 使用"索引"视图模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="e0eb2-202">我们要传递视图模板 Dinner 对象生成的列表中的序列：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="e0eb2-203">我们 Details() 操作方法中，我们尝试检索 Dinner 对象使用的 URL 中提供的 id。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="e0eb2-204">如果我们调用找到有效的 Dinner *View()* 帮助器方法，指明我们想要使用"详细信息"视图模板来呈现检索到的 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="e0eb2-205">如果请求无效 dinner，则我们呈现有用的错误消息，指示 Dinner 不存在使用"NotFound"视图模板 (和重载的版本*View()* 帮助器方法，只需将模板名称):</span><span class="sxs-lookup"><span data-stu-id="e0eb2-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="e0eb2-206">现在让我们来实现"NotFound"、"详细信息"和"索引"视图模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="e0eb2-207">实现"NotFound"查看模板</span><span class="sxs-lookup"><span data-stu-id="e0eb2-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="e0eb2-208">我们将开始通过实现"NotFound"视图模板-其中显示了一个友好的错误消息，表明找不到请求的 dinner。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="e0eb2-209">我们将通过定位在控制器操作方法中，我们文本光标创建新的视图模板，然后右键单击并选择"添加视图"菜单命令 （我们还可以执行此命令通过键入 Ctrl-M，Ctrl + V）：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="e0eb2-210">此时会弹出如下面的"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="e0eb2-211">默认情况下该对话框将预填充要创建的视图的名称以与操作方法的名称匹配光标时所在对话框启动 （在本例中"的详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="e0eb2-212">由于我们想要首先实现"NotFound"模板，我们将重写此视图的名称，并将其改为"找不到"设置为：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="e0eb2-213">当我们单击"添加"按钮时，Visual Studio 将创建一个新"NotFound.aspx"视图模板为我们中的"\Views\Dinners"目录 （它还将创建如果目录尚不存在）：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="e0eb2-214">它还将打开代码编辑器内我们新"NotFound.aspx"查看模板：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="e0eb2-215">默认情况下的视图模板有两个"内容区域"我们可以在其中添加内容和代码。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="e0eb2-216">第一个可用于自定义"title"的 HTML 页发回。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="e0eb2-217">第二个可用于自定义的"主要内容"HTML 页发回。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="e0eb2-218">若要实现"NotFound"视图模板，我们将添加一些基本内容：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="e0eb2-219">我们可以再尝试在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-219">We can then try it out within the browser.</span></span> <span data-ttu-id="e0eb2-220">若要执行此操作让我们请求 *"/ Dinners/详细信息/9999"* URL。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="e0eb2-221">这将引用 dinner，当前不存在在数据库中，并将导致我们 DinnersController.Details() 操作方法以呈现我们"NotFound"查看模板：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="e0eb2-222">您会注意到在上面的屏幕截图中的一件事是我们的基本视图模板已继承了一系列 HTML 围绕在屏幕上的主要内容。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="e0eb2-223">这是因为我们视图模板使用的使我们能够一致布局适用于站点上的所有视图的"母版页"模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="e0eb2-224">我们将讨论如何母版页的工作原理的本教程后面部分中提供了更多。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="e0eb2-225">实现"详细信息"视图模板</span><span class="sxs-lookup"><span data-stu-id="e0eb2-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="e0eb2-226">现在让我们来实现的"详细信息"视图模板-将单个 Dinner 模型生成的 HTML。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="e0eb2-227">我们将执行此操作通过定位在详细信息操作方法中，我们文本光标然后右键单击并选择"添加视图"菜单命令 （或按 Ctrl-M、 Ctrl + V）：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="e0eb2-228">这将显示"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="e0eb2-229">我们将保留的默认视图名称 （"详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="e0eb2-230">我们还将在对话框中选择"创建强类型视图"复选框，然后选择 （使用组合框下拉列表中） 到该视图从控制器传入的模型类型的名称。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="e0eb2-231">此视图的传入 Dinner 对象 (此类型的完全限定的名称是:"NerdDinner.Models.Dinner"):</span><span class="sxs-lookup"><span data-stu-id="e0eb2-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="e0eb2-232">与上面的模板，其中我们选择创建"空视图"，的此时我们将自动选择"创建基架"视图使用"详细信息"的模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="e0eb2-233">我们可以通过更改"视图内容"下拉列表中上述对话框指示这一点。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="e0eb2-234">"基架"将生成基于我们要将它们传递给它的 Dinner 对象详细信息视图模板的初始实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="e0eb2-235">这提供了用于轻松对我们能够快速开始我们的视图模板实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="e0eb2-236">当我们单击"添加"按钮时，Visual Studio 将创建一个新"Details.aspx"视图模板文件为我们我们"\Views\Dinners"目录中：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="e0eb2-237">它还会打开代码编辑器内我们新的"Details.aspx"视图模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="e0eb2-238">它将包含基于 Dinner 模型的详细信息视图的初始基架实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="e0eb2-239">基架引擎使用.NET 反射来看看传递，在类上公开的公共属性，并将添加基于找到每种类型的相应内容：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="e0eb2-240">我们可以请求 *"/ Dinners/详细信息/1"* URL 即可查看此"详细信息"基架实现在浏览器中的样子。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="e0eb2-241">使用此 URL 将显示我们手动添加到我们的数据库时我们首次创建的 dinners 之一：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="e0eb2-242">这很快就会变我们启动并运行，并为我们提供了我们 Details.aspx 视图的初始实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="e0eb2-243">我们然后可以转到并进行调整，以自定义用户界面，以我们的满意度。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="e0eb2-244">当我们更紧密地查看 Details.aspx 模板时，我们会发现，它包含静态 HTML，以及嵌入呈现代码。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="e0eb2-245">&lt;%%&gt;代码片段执行代码时呈现的视图模板，并&lt;%= %&gt;代码片段执行其中所包含的代码，并随后呈现到输出流的模板的结果。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="e0eb2-246">我们可以访问的"Dinner"模型对象，我们使用从控制器的强类型化"模型"属性传递我们视图内编写代码。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="e0eb2-247">Visual Studio 为我们提供了在具有完整的代码 intellisense 时访问此"模型"属性编辑器中：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="e0eb2-248">让我们进行一些调整，以便我们最终的详细信息视图模板的源类似于下面：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="e0eb2-249">当我们访问 *"/ Dinners/详细信息/1"* URL 再次它现在将呈现如下所示：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="e0eb2-250">实现"索引"视图模板</span><span class="sxs-lookup"><span data-stu-id="e0eb2-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="e0eb2-251">现在让我们来实现"索引"视图模板-这会导致生成即将推出 Dinners 的列表。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="e0eb2-252">待办事项这我们在索引操作方法中，我们文本光标的位置，然后右键单击并选择"添加视图"菜单命令 （或按 Ctrl-M，Ctrl + V）。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="e0eb2-253">在"添加视图"对话框中，我们将保留视图模板名为"Index"，并选择"创建强类型视图"复选框。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="e0eb2-254">这次我们将选择自动生成"列表"视图模板，然后选择"NerdDinner.Models.Dinner"作为模型类型传递给视图 (其中因为我们已表明我们要创建基架将导致假定我们添加视图对话框的"列表"Dinner 对象的序列将从传递控制器到视图）：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="e0eb2-255">当我们单击"添加"按钮时，Visual Studio 将新的"Index.aspx"视图模板文件为我们创建我们"\Views\Dinners"目录中。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="e0eb2-256">它将"搭建基架"提供了我们向视图传递的 Dinners HTML 表列表中的初始实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="e0eb2-257">当我们运行的应用程序和访问权限 *"/ Dinners /"* 它会呈现我们 dinners 的列表的 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="e0eb2-258">上面的表解决方案为我们提供了我们的 Dinner 数据 – 这并不完全是我们希望我们消费型 Dinner 列表类似于网格的布局。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="e0eb2-259">我们可以更新 Index.aspx 视图模板并修改它以列表更少的数据列，并使用&lt;ul&gt;元素来呈现它们而不是使用下面的代码对表：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="e0eb2-260">如我们循环访问每个 dinner 在我们的模型中，我们将使用在上面的 foreach 语句中的"var"关键字。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="e0eb2-261">熟悉 C# 3.0 的那些可能会认为，使用"var"意味着 dinner 对象是后期绑定。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="e0eb2-262">而是意味着编译器所使用类型推理针对强类型化的"模型"属性 (它属于类型"IEnumerable&lt;Dinner&gt;") 和编译为 Dinner 类型 – 这意味着我们获得完整的本地"dinner"变量intellisense 和编译时在代码块内检查：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="e0eb2-263">当我们点击刷新 */Dinners*我们更新的视图现在看起来像下面我们浏览器中的 URL:</span><span class="sxs-lookup"><span data-stu-id="e0eb2-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="e0eb2-264">这查找更好，但尚未完全到位。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="e0eb2-265">我们最后一步是启用最终用户可以单击列表中的单个 Dinners，看到它们的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="e0eb2-266">我们将呈现链接到我们 DinnersController 的详细信息操作方法的 HTML 超链接元素进行实现。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="e0eb2-267">我们中有两种，索引视图中，我们可以生成这些超链接。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="e0eb2-268">第一种是手动创建的 HTML &lt;&gt;元素类似下面，我们将嵌入&lt;%%&gt;内阻止&lt;&gt; HTML 元素：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="e0eb2-269">我们可以使用一种替代方法是利用在 ASP.NET MVC 支持以编程方式创建 HTML 中的内置"Html.ActionLink()"帮助程序方法&lt;&gt;链接到另一个操作方法的元素控制器：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="e0eb2-270">Html.ActionLink() 帮助器方法的第一个参数是要显示的链接文本 （在本例中标题的 dinner），第二个参数是我们想要生成的链接 （在本例中的详细信息的方法），控制器操作名称，第三个参数是要将发送到 （实现为具有属性名称/值的匿名类型） 的操作的参数集。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="e0eb2-271">我们在这种情况下指定的 dinner 我们想要链接到，并且由于 ASP.NET MVC 中的默认 URL 路由规则的"id"参数"{Controller} / {Action} / {id}"Html.ActionLink() 帮助器方法将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="e0eb2-272">Index.aspx 视图中，我们将使用 Html.ActionLink() 帮助器方法的方法，并具有指向适当的详细信息 URL 的列表中的每个 dinner:</span><span class="sxs-lookup"><span data-stu-id="e0eb2-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="e0eb2-273">和现在当我们点击 */Dinners* dinner 列表类似于下面的 URL:</span><span class="sxs-lookup"><span data-stu-id="e0eb2-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="e0eb2-274">当我们单击任一列表中 Dinners 我们导航以查看其详细信息：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="e0eb2-275">基于约定的命名和 \Views 目录结构</span><span class="sxs-lookup"><span data-stu-id="e0eb2-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="e0eb2-276">默认情况下的 ASP.NET MVC 应用程序使用基于约定的目录解析视图模板时命名结构。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="e0eb2-277">这允许开发人员无需完全限定位置路径引用从控制器类中的视图时。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="e0eb2-278">默认情况下 ASP.NET MVC 将查找视图模板文件内 * \Views\[ControllerName]\*应用程序下面的目录。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-278">By default ASP.NET MVC will look for the view template file within the *\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="e0eb2-279">例如，我们一直在努力 DinnersController 类 – 它显式引用三个视图模板:"索引"、"详细信息"和"NotFound"。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="e0eb2-280">ASP.NET MVC 将默认情况下查找中的这些视图*\Views\Dinners*目录下我们应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="e0eb2-281">请注意上面这里是当前项目中的三个控制器类 (DinnersController、 HomeController 和 AccountController – 最后两个默认情况下我们在创建项目时添加)，并且有三个子目录 （一个用于每个控制器） \Views 目录中。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="e0eb2-282">从主页和帐户控制器中引用的视图将自动解析及其各自的视图模板*\Views\Home*并*\Views\Account*目录。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="e0eb2-283">*\Views\Shared*子目录提供了一种方法来存储跨多个控制器应用程序中重复使用的视图模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="e0eb2-284">当 ASP.NET MVC 尝试解析视图模板时，它将首先检查内*\Views\[控制器]* 特定目录，并且如果它找不到视图模板那里它看起来将中*\Views\共享*目录。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="e0eb2-285">命名单个视图模板时，推荐的指导是已导致要呈现的操作方法同名的视图模板。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="e0eb2-286">例如，以上我们的"索引"操作方法使用"索引"视图来呈现视图结果，而"详细信息"操作方法使用"详细信息"视图来呈现其结果。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="e0eb2-287">这样，可以轻松快速查看哪些模板是与每个操作相关联。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="e0eb2-288">开发人员不需要显式指定视图模板名称，当视图模板具有与所调用的控制器上的操作方法相同的名称。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="e0eb2-289">我们可以改为只是该模型对象传递给"View()"帮助器方法 （如果不指定视图名称），和 ASP.NET MVC 将自动推断我们想要使用*\Views\[ControllerName]\[ActionName]* 视图模板来呈现它的磁盘上。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="e0eb2-290">这样，我们有点，清理我们的控制器代码并避免重复两次在代码中的名称：</span><span class="sxs-lookup"><span data-stu-id="e0eb2-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="e0eb2-291">上面的代码是实现很好 Dinner 列表/详细信息所需的所有站点体验。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="e0eb2-292">下一步</span><span class="sxs-lookup"><span data-stu-id="e0eb2-292">Next Step</span></span>

<span data-ttu-id="e0eb2-293">现在，我们有很好的 Dinner 浏览生成的体验。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="e0eb2-294">让我们现在启用 CRUD （创建、 读取、 更新、 删除） 数据窗体编辑支持。</span><span class="sxs-lookup"><span data-stu-id="e0eb2-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e0eb2-295">[上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="e0eb2-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
