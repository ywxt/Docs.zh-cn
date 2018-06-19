---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第 3 部分： 视图和 Viewmodel |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 3 部分介绍视图和 Viewmodel。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 497c2898db2e03b0650982c3ad1e6b5ac5ca639d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874845"
---
<a name="part-3-views-and-viewmodels"></a><span data-ttu-id="73b8e-104">第 3 部分： 视图和 Viewmodel</span><span class="sxs-lookup"><span data-stu-id="73b8e-104">Part 3: Views and ViewModels</span></span>
====================
<span data-ttu-id="73b8e-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="73b8e-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="73b8e-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="73b8e-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="73b8e-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="73b8e-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="73b8e-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="73b8e-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="73b8e-109">第 3 部分介绍视图和 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="73b8e-109">Part 3 covers Views and ViewModels.</span></span>


<span data-ttu-id="73b8e-110">到目前为止我们已刚刚已返回字符串的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="73b8e-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="73b8e-111">可以很好地了解如何控制器工作，但不是如何你想要构建实际的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="73b8e-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="73b8e-112">我们将需要一种更好的方式，来返回到浏览器访问我们的站点生成 HTML – 其中我们可以用模板文件要更轻松地自定义的 HTML 内容的一种发回。</span><span class="sxs-lookup"><span data-stu-id="73b8e-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="73b8e-113">这正是视图执行的操作。</span><span class="sxs-lookup"><span data-stu-id="73b8e-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="73b8e-114">添加视图模板</span><span class="sxs-lookup"><span data-stu-id="73b8e-114">Adding a View template</span></span>

<span data-ttu-id="73b8e-115">若要使用视图模板，我们将更改 HomeController 索引方法，以便返回 ActionResult，并将其返回 View()，如下面：</span><span class="sxs-lookup"><span data-stu-id="73b8e-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="73b8e-116">上述更改表示而不是返回一个字符串，我们改为想要使用"视图"来生成结果返回。</span><span class="sxs-lookup"><span data-stu-id="73b8e-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="73b8e-117">我们现在将添加到我们的项目中的适当的视图模板。</span><span class="sxs-lookup"><span data-stu-id="73b8e-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="73b8e-118">若要这样做我们将在索引操作方法中，将文本光标的位置，然后右键单击并选择"添加视图"。</span><span class="sxs-lookup"><span data-stu-id="73b8e-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="73b8e-119">此时将显示添加视图对话框：</span><span class="sxs-lookup"><span data-stu-id="73b8e-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="73b8e-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="73b8e-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="73b8e-121">"添加视图"对话框，我们可以快速轻松地生成查看模板文件。</span><span class="sxs-lookup"><span data-stu-id="73b8e-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="73b8e-122">默认情况下，"添加视图"对话框将预先填充视图模板创建，以便它与匹配将使用它的操作方法的名称。</span><span class="sxs-lookup"><span data-stu-id="73b8e-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="73b8e-123">由于我们使用我们 HomeController index （） 操作方法内的"添加视图"上下文菜单，上面的"添加视图"对话框为默认情况下预填充的视图名称具有"索引"。</span><span class="sxs-lookup"><span data-stu-id="73b8e-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="73b8e-124">我们无需更改任何在该对话框中的选项，因此单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="73b8e-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="73b8e-125">当我们单击添加按钮时，Visual Web Developer 将创建新 Index.cshtml 为我们在 \Views\Home 目录中，如果创建文件夹的视图模板尚不存在。</span><span class="sxs-lookup"><span data-stu-id="73b8e-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="73b8e-126">"Index.cshtml"文件的名称和文件夹位置是重要的是，并遵循的默认 ASP.NET MVC 命名约定。</span><span class="sxs-lookup"><span data-stu-id="73b8e-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="73b8e-127">目录名称、 \Views\Home，匹配的控制器的名为 HomeController。</span><span class="sxs-lookup"><span data-stu-id="73b8e-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="73b8e-128">视图模板名称，索引，匹配的控制器操作方法，这将会显示该视图。</span><span class="sxs-lookup"><span data-stu-id="73b8e-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="73b8e-129">ASP.NET MVC 允许我们以避免让我们使用此命名约定来返回的视图时显式指定的名称或视图模板的位置。</span><span class="sxs-lookup"><span data-stu-id="73b8e-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="73b8e-130">它会默认情况下呈现 \Views\Home\Index.cshtml 视图模板当我们在我们 HomeController 内编写类似下面的代码：</span><span class="sxs-lookup"><span data-stu-id="73b8e-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="73b8e-131">Visual Web Developer 中创建并打开"Index.cshtml"查看模板之后我们单击"添加视图"对话框中的"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="73b8e-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="73b8e-132">Index.cshtml 的内容如下所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="73b8e-133">此视图使用 Razor 语法，这是比使用 ASP.NET Web 窗体和以前版本的 ASP.NET MVC 中的 Web 窗体视图引擎更加简洁。</span><span class="sxs-lookup"><span data-stu-id="73b8e-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="73b8e-134">Web 窗体视图引擎在 ASP.NET MVC 3 中仍然可用，但许多开发人员查找 Razor 视图引擎很好地符合 ASP.NET MVC 开发。</span><span class="sxs-lookup"><span data-stu-id="73b8e-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="73b8e-135">前三行设置使用 ViewBag.Title 页面标题。</span><span class="sxs-lookup"><span data-stu-id="73b8e-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="73b8e-136">我们将查看原理更详细地很快，但首先让我们更新文本标题文本，并查看该页面。</span><span class="sxs-lookup"><span data-stu-id="73b8e-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="73b8e-137">更新&lt;h2&gt;标记说"此是 Home Page"，如下所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="73b8e-138">运行应用程序显示我们的新文本是在主页页上可见。</span><span class="sxs-lookup"><span data-stu-id="73b8e-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="73b8e-139">有关通用站点元素中使用的布局</span><span class="sxs-lookup"><span data-stu-id="73b8e-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="73b8e-140">大多数网站具有多个页间共享的内容： 导航、 页脚、 徽标图像、 样式表的引用，等等。Razor 视图引擎使此更容易地管理使用页调用\_Layout.cshtml 其中已自动为创建我们在/视图/共享文件夹。</span><span class="sxs-lookup"><span data-stu-id="73b8e-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="73b8e-141">双击此文件夹以查看该内容，其如下所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="73b8e-142">我们单个视图中的内容将显示的@RenderBody（） 的命令，并且我们想要显示之外的任何公共内容可以添加到\_Layout.cshtml 标记。</span><span class="sxs-lookup"><span data-stu-id="73b8e-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="73b8e-143">我们将需要拥有对我们主页上和存储的区域，在站点中，所有页面上的具有链接的常见标头，因此我们将添加到正上方的模板我们 MVC 音乐商店@RenderBody（） 语句。</span><span class="sxs-lookup"><span data-stu-id="73b8e-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="73b8e-144">更新样式表</span><span class="sxs-lookup"><span data-stu-id="73b8e-144">Updating the StyleSheet</span></span>

<span data-ttu-id="73b8e-145">空项目模板包括非常简化的 CSS 文件，其中只包含用于显示验证消息的样式。</span><span class="sxs-lookup"><span data-stu-id="73b8e-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="73b8e-146">一些其他的 CSS 和映像，以定义我们的站点，外观和感觉，使我们将添加中现在提供了我们设计器。</span><span class="sxs-lookup"><span data-stu-id="73b8e-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="73b8e-147">这是在可用的 MvcMusicStore Assets.zip 的内容目录中包括的更新的 CSS 文件和映像[MVC 音乐商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="73b8e-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="73b8e-148">我们将在 Windows 资源管理器中选择这两个，并将其放入在 Visual Web Developer 中，我们的解决方案的内容文件夹中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="73b8e-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="73b8e-149">你将需要确认你是否要覆盖现有的 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="73b8e-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="73b8e-150">单击是。</span><span class="sxs-lookup"><span data-stu-id="73b8e-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="73b8e-151">你的应用程序的内容文件夹将现在显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="73b8e-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="73b8e-152">现在让我们运行应用程序并查看我们更改在主页上的效果。</span><span class="sxs-lookup"><span data-stu-id="73b8e-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="73b8e-153">让我们回顾一下会发生什么变化： HomeController 的索引操作方法找到，并且显示 \Views\Home\Index.cshtmlView 模板中，即使我们的代码称为"返回 View()"，因为我们查看模板遵循标准的命名约定。</span><span class="sxs-lookup"><span data-stu-id="73b8e-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="73b8e-154">主页上显示在 \Views\Home\Index.cshtml 视图模板中定义的简单欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="73b8e-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="73b8e-155">使用主页页面我们\_Layout.cshtml 模板，因此在欢迎消息包含在标准站点 HTML 布局。</span><span class="sxs-lookup"><span data-stu-id="73b8e-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="73b8e-156">使用模型将信息传递给我们视图</span><span class="sxs-lookup"><span data-stu-id="73b8e-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="73b8e-157">只是显示了硬编码 HTML 视图模板并不会使很感兴趣的 web 站点。</span><span class="sxs-lookup"><span data-stu-id="73b8e-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="73b8e-158">若要创建动态网站，我们将改为想要将信息从我们的控制器操作传递到我们查看模板。</span><span class="sxs-lookup"><span data-stu-id="73b8e-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="73b8e-159">在模型-视图-控制器模式中，的术语模型是指对象表示应用程序中的数据。</span><span class="sxs-lookup"><span data-stu-id="73b8e-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="73b8e-160">通常情况下，模型对象对应于表在数据库中，但它们并非一定。</span><span class="sxs-lookup"><span data-stu-id="73b8e-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="73b8e-161">返回 ActionResult 控制器操作方法可以将模型对象传递给该视图。</span><span class="sxs-lookup"><span data-stu-id="73b8e-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="73b8e-162">这样，到完全包生成响应，，然后将此信息传递到视图模板所需的所有信息的控制器用来生成相应的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="73b8e-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="73b8e-163">这是最简单方法是查看在操作中了解，因此让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="73b8e-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="73b8e-164">首先我们将创建用于在我们存储表示风格和专辑某些模型类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="73b8e-165">让我们开始通过创建流派类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="73b8e-166">右键单击你的项目中的"模型"文件夹中，选择"添加类"选项，并将文件"Genre.cs"。</span><span class="sxs-lookup"><span data-stu-id="73b8e-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="73b8e-167">然后添加到已创建的类的公共字符串名称属性：</span><span class="sxs-lookup"><span data-stu-id="73b8e-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="73b8e-168">*注意： 在您想知道的情况下 {获取; 设置;} 表示法正在使用 C# 的自动实现的属性功能。这为我们提供一个属性的优点而无需我们可以声明一个后备字段。*</span><span class="sxs-lookup"><span data-stu-id="73b8e-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="73b8e-169">接下来，请按照相同的步骤来创建一个具有标题和风格属性的唱片集类 （名为 Album.cs）：</span><span class="sxs-lookup"><span data-stu-id="73b8e-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="73b8e-170">现在我们可以修改 StoreController 用于显示我们的模型中的动态信息的视图。</span><span class="sxs-lookup"><span data-stu-id="73b8e-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="73b8e-171">如果-出于演示目的现在-我们名为基于的请求 ID 我们专辑，我们无法显示该信息，如下面的视图中所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="73b8e-172">我们将开始通过更改存储详细信息操作，以便其显示单个唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="73b8e-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="73b8e-173">将"using"语句添加到顶部**StoreControllers**类，以包含 MvcMusicStore.Models 命名空间，因此我们不需要键入 MvcMusicStore.Models.Album，每次我们想要使用唱片集类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="73b8e-174">此类的"using"部分现在应显示如下。</span><span class="sxs-lookup"><span data-stu-id="73b8e-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="73b8e-175">接下来，我们将更新的详细信息的控制器操作，以便它返回 ActionResult 而不是一个字符串，正如我们做与 HomeController 的 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="73b8e-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="73b8e-176">现在我们可以修改逻辑，以返回到视图的唱片集对象。</span><span class="sxs-lookup"><span data-stu-id="73b8e-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="73b8e-177">本教程中稍后我们将检索数据从数据库 – 但对于现在我们将使用"虚拟数据"以开始。</span><span class="sxs-lookup"><span data-stu-id="73b8e-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="73b8e-178">*注意： 如果你熟悉 C#，你可能会假定使用 var 意味着我们唱片集变量是后期绑定。不正确-C# 编译器使用类型推理基于什么我们要为变量分配以确定该唱片集属于类型唱片集和编译本地唱片集变量用作唱片集类型，因此我们获取编译时检查和 Visual Studio 代码编辑器支持。*</span><span class="sxs-lookup"><span data-stu-id="73b8e-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="73b8e-179">让我们现在创建一个视图模板，它使用我们唱片集来生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="73b8e-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="73b8e-180">我们执行此操作之前，我们需要生成项目，以便添加视图对话框就会了解有关我们新创建的唱片集类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="73b8e-181">可以生成项目时通过选择 Debug⇨Build MvcMusicStore 菜单项 （对于额外信用，你可以使用 Ctrl Shift B 快捷方式以生成项目）。</span><span class="sxs-lookup"><span data-stu-id="73b8e-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="73b8e-182">现在，我们已设置了我们支持的类，我们已准备好生成我们查看模板。</span><span class="sxs-lookup"><span data-stu-id="73b8e-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="73b8e-183">在详细信息方法内右键单击并选择"添加视图..."</span><span class="sxs-lookup"><span data-stu-id="73b8e-183">Right-click within the Details method and select "Add View…"</span></span> <span data-ttu-id="73b8e-184">从上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="73b8e-184">from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="73b8e-185">我们将创建一个新的视图模板像我们之前使用 HomeController。</span><span class="sxs-lookup"><span data-stu-id="73b8e-185">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="73b8e-186">因为我们将从 StoreController 创建它将默认情况下生成 \Views\Store\Index.cshtml 文件中。</span><span class="sxs-lookup"><span data-stu-id="73b8e-186">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="73b8e-187">与不同之前，我们将选中"创建强类型"视图复选框。</span><span class="sxs-lookup"><span data-stu-id="73b8e-187">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="73b8e-188">然后，我们将选择"视图数据的类"放-downlist 中我们"唱片集"的类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-188">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="73b8e-189">这将导致创建唱片集将传递给其使用的对象的视图模板所需的"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="73b8e-189">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="73b8e-190">当单击"添加"按钮时，我们将创建我们 \Views\Store\Details.cshtml 查看模板，包含以下代码。</span><span class="sxs-lookup"><span data-stu-id="73b8e-190">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="73b8e-191">请注意第一行，该值指示此视图为强类型化为我们唱片集的类。</span><span class="sxs-lookup"><span data-stu-id="73b8e-191">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="73b8e-192">Razor 视图引擎能够理解，它已被传递唱片集对象，以便我们可以轻松地访问模型属性，甚至可以安排在 Visual Web Developer 编辑器中 IntelliSense 的好处。</span><span class="sxs-lookup"><span data-stu-id="73b8e-192">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="73b8e-193">更新&lt;h2&gt;标记以便它显示唱片集的 Title 属性通过修改该行起来，如下所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-193">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="73b8e-194">请注意当你输入后的期间触发时 IntelliSense@Model关键字，显示的属性和唱片集类支持的方法。</span><span class="sxs-lookup"><span data-stu-id="73b8e-194">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="73b8e-195">让我们现在重新运行我们的项目，并访问应用商店/详细信息/5 URL。</span><span class="sxs-lookup"><span data-stu-id="73b8e-195">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="73b8e-196">我们将看到类似下面唱片集的详细信息。</span><span class="sxs-lookup"><span data-stu-id="73b8e-196">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="73b8e-197">现在我们将使应用商店浏览操作方法类似的更新。</span><span class="sxs-lookup"><span data-stu-id="73b8e-197">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="73b8e-198">更新方法，使其返回 ActionResult 和修改的方法的逻辑，以使它创建一个新的流派对象并将其返回到视图。</span><span class="sxs-lookup"><span data-stu-id="73b8e-198">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="73b8e-199">浏览方法中右键单击并选择"添加视图..."</span><span class="sxs-lookup"><span data-stu-id="73b8e-199">Right-click in the Browse method and select "Add View…"</span></span> <span data-ttu-id="73b8e-200">从上下文菜单，然后添加是强类型的视图类中添加强类型化风格。</span><span class="sxs-lookup"><span data-stu-id="73b8e-200">from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="73b8e-201">更新&lt;h2&gt;视图中的元素内的代码 （/Views/Store/Browse.cshtml) 以显示流派信息。</span><span class="sxs-lookup"><span data-stu-id="73b8e-201">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="73b8e-202">现在让我们重新运行我们的项目，并浏览到应用商店/浏览？流派 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="73b8e-202">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="73b8e-203">我们将看到浏览页显示如下所示。</span><span class="sxs-lookup"><span data-stu-id="73b8e-203">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="73b8e-204">最后，让我们进行到稍微更复杂的更新**存储索引**操作方法以及要在我们的存储区中显示的所有风格列表视图。</span><span class="sxs-lookup"><span data-stu-id="73b8e-204">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="73b8e-205">我们将为我们的模型对象，而不是单个流派，只需使用风格列表来执行该操作。</span><span class="sxs-lookup"><span data-stu-id="73b8e-205">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="73b8e-206">存储索引操作方法中右键单击，然后选择添加视图之前，选择 Genre 作为模型类，以及按添加按钮。</span><span class="sxs-lookup"><span data-stu-id="73b8e-206">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="73b8e-207">首先我们将更改@model声明，以指示该视图将需要几个流派对象而不是仅仅一个。</span><span class="sxs-lookup"><span data-stu-id="73b8e-207">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="73b8e-208">更改 /Store/Index.cshtml 读取，如下所示的第一行：</span><span class="sxs-lookup"><span data-stu-id="73b8e-208">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="73b8e-209">这将告知 Razor 视图引擎，它将使用可以容纳多个流派对象模型对象。</span><span class="sxs-lookup"><span data-stu-id="73b8e-209">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="73b8e-210">我们将使用 IEnumerable&lt;流派&gt;而不是列表&lt;流派&gt;由于这是更通用的使我们能够将我们的模型类型更高版本更改为支持 IEnumerable 接口的任何对象类型。</span><span class="sxs-lookup"><span data-stu-id="73b8e-210">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="73b8e-211">接下来，我们将循环访问中的模型，如下面的已完成的视图代码中所示的流派对象。</span><span class="sxs-lookup"><span data-stu-id="73b8e-211">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="73b8e-212">请注意，我们具有完整的 IntelliSense 支持我们输入此代码，以便当我们键入"@Model。"</span><span class="sxs-lookup"><span data-stu-id="73b8e-212">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="73b8e-213">我们看到所有方法和支持的类型流派 IEnumerable 的属性。</span><span class="sxs-lookup"><span data-stu-id="73b8e-213">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="73b8e-214">在我们"foreach"循环中，Visual Web Developer 知道，每个项的类型是流派，我们看到 IntelliSence 每个风格类型。</span><span class="sxs-lookup"><span data-stu-id="73b8e-214">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSence for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="73b8e-215">接下来，基架功能检查流派对象，并确定，每个将包含一个 Name 属性，因此它循环访问并写出。它还将生成的每个项的编辑、 详细信息，并删除链接。</span><span class="sxs-lookup"><span data-stu-id="73b8e-215">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="73b8e-216">我们将利用这一点，更高版本中我们存储管理器中，但现在我们想要改为具有一个简单的列表。</span><span class="sxs-lookup"><span data-stu-id="73b8e-216">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="73b8e-217">当我们运行该应用程序和浏览到 /Store 时，我们看到显示的计数和风格的列表。</span><span class="sxs-lookup"><span data-stu-id="73b8e-217">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="73b8e-218">页之间添加链接</span><span class="sxs-lookup"><span data-stu-id="73b8e-218">Adding Links between pages</span></span>

<span data-ttu-id="73b8e-219">当前列出风格我们 /Store URL 只需以纯文本形式列出流派名称。</span><span class="sxs-lookup"><span data-stu-id="73b8e-219">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="73b8e-220">让我们更改这，以便而不是纯文本我们改为具有流派名称链接到相应的应用商店/浏览 URL，以便单击音乐流派，如"Disco"将导航到 / 存储/浏览？ 流派 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="73b8e-220">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="73b8e-221">我们无法更新我们 \Views\Store\Index.cshtml 视图模板使用这些链接的代码类似下面的输出到 **（不键入此中-我们将在其上改进）**:</span><span class="sxs-lookup"><span data-stu-id="73b8e-221">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="73b8e-222">操作成功，但它可能会导致更高版本问题，因为它依赖于硬编码字符串。</span><span class="sxs-lookup"><span data-stu-id="73b8e-222">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="73b8e-223">例如，如果我们想要重命名控制器，我们需要我们寻找需要更新的链接的代码中进行搜索。</span><span class="sxs-lookup"><span data-stu-id="73b8e-223">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="73b8e-224">我们可以使用另一种方法是利用一个 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="73b8e-224">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="73b8e-225">ASP.NET MVC 包括 HTML 帮助器方法，可从我们查看模板代码可执行各种就像下面这样的常见任务。</span><span class="sxs-lookup"><span data-stu-id="73b8e-225">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="73b8e-226">Html.ActionLink() 帮助器方法是一个特别有用，并可以轻松地生成 HTML &lt;&gt;链接，并负责令人讨厌的详细信息，如确保 URL 路径正确进行 URL 编码。</span><span class="sxs-lookup"><span data-stu-id="73b8e-226">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="73b8e-227">Html.ActionLink() 有几个不同的重载来允许指定尽可能多的信息，根据需要为你的链接。</span><span class="sxs-lookup"><span data-stu-id="73b8e-227">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="73b8e-228">在最简单的情况下，你将提供不仅仅是链接文本和客户端上单击超链接时转到的操作方法。</span><span class="sxs-lookup"><span data-stu-id="73b8e-228">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="73b8e-229">例如，我们可以将链接到"应用商店 /"链接文本"转到存储索引"使用以下调用存储详细信息页面上的 index （） 方法：</span><span class="sxs-lookup"><span data-stu-id="73b8e-229">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="73b8e-230">*注意： 在这种情况下，我们不需要指定控制器名称，因为我们只需链接到同一个呈现当前视图的控制器中的另一个操作。*</span><span class="sxs-lookup"><span data-stu-id="73b8e-230">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="73b8e-231">我们指向浏览页上的将需要传递参数，不过，因此我们将使用另一个重载采用三个参数的次 Html.ActionLink 方法：</span><span class="sxs-lookup"><span data-stu-id="73b8e-231">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="73b8e-232">链接文本，将显示流派名称</span><span class="sxs-lookup"><span data-stu-id="73b8e-232">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="73b8e-233">控制器操作名称 （浏览）</span><span class="sxs-lookup"><span data-stu-id="73b8e-233">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="73b8e-234">路由参数值，指定的名称 （流派） 和值 （流派名称）</span><span class="sxs-lookup"><span data-stu-id="73b8e-234">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="73b8e-235">将放在一起，此处我们如何将写存储索引视图这些链接：</span><span class="sxs-lookup"><span data-stu-id="73b8e-235">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="73b8e-236">现在我们再次运行我们的项目并访问 /Store/ URL 时我们将看到风格的列表。</span><span class="sxs-lookup"><span data-stu-id="73b8e-236">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="73b8e-237">单击时，每个风格是一个超链接 – 它将给我们讲到我们/存储/浏览？ 流派 =*[流派]* URL。</span><span class="sxs-lookup"><span data-stu-id="73b8e-237">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="73b8e-238">有关风格列表 HTML 类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="73b8e-238">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> <span data-ttu-id="73b8e-239">[上一页](mvc-music-store-part-2.md)
> [下一页](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="73b8e-239">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
