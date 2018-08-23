---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第 3 部分： 视图和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 3 部分介绍 Views 和 ViewModels。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 828ff18abcc5932f82be71a45ebde589eeb051fa
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831059"
---
<a name="part-3-views-and-viewmodels"></a><span data-ttu-id="c2e7e-104">第 3 部分： 视图和 Viewmodel</span><span class="sxs-lookup"><span data-stu-id="c2e7e-104">Part 3: Views and ViewModels</span></span>
====================
<span data-ttu-id="c2e7e-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="c2e7e-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c2e7e-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c2e7e-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c2e7e-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c2e7e-109">第 3 部分介绍 Views 和 ViewModels。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-109">Part 3 covers Views and ViewModels.</span></span>


<span data-ttu-id="c2e7e-110">到目前为止我们已经就已返回字符串的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="c2e7e-111">这是一个好方法大致的控制器的工作方式，但不是将如何生成实际的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="c2e7e-112">我们要想更好的方法来生成 HTML 返回到浏览器访问我们的站点 — 一个在其中我们可以使用模板文件更轻松地自定义 HTML 内容发送回。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="c2e7e-113">这正是视图执行的操作。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="c2e7e-114">添加视图模板</span><span class="sxs-lookup"><span data-stu-id="c2e7e-114">Adding a View template</span></span>

<span data-ttu-id="c2e7e-115">若要使用视图模板，我们将更改 HomeController Index 方法，以返回一个 ActionResult，并使其返回 View()，类似如下：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="c2e7e-116">上述更改表示而不是返回一个字符串，我们改为想要使用"视图"以生成返回的结果。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="c2e7e-117">我们现在将为我们的项目中添加相应的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="c2e7e-118">为此我们将在索引操作方法中，将文本光标置于然后右键单击并选择"添加视图"。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="c2e7e-119">这将打开添加视图对话框：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="c2e7e-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c2e7e-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="c2e7e-121">"添加视图"对话框可用于快速、 轻松地生成视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="c2e7e-122">默认情况下，"添加视图"对话框预填充视图模板来创建，使其匹配将使用它的操作方法的名称。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="c2e7e-123">由于我们使用我们 HomeController 的 index （） 操作方法中的"添加视图"上下文菜单，上述"添加视图"对话框的"索引"作为视图名称默认情况下预填充。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="c2e7e-124">我们不需要更改任何在该对话框中的选项，因此请单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="c2e7e-125">当我们单击添加按钮时，Visual Web Developer 将创建新的 Index.cshtml 视图模板为我们在 \Views\Home 目录中，如果创建文件夹尚不存在。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="c2e7e-126">"Index.cshtml"文件的名称和文件夹位置是重要的是，并遵循的默认 ASP.NET MVC 命名约定。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="c2e7e-127">目录名称、 \Views\Home，匹配的控制器的名为 HomeController。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="c2e7e-128">视图模板名称，索引，匹配将显示该视图的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="c2e7e-129">ASP.NET MVC，我们可以避免不得不显式指定的名称或视图模板的位置，当我们使用此命名约定可以返回视图。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="c2e7e-130">它会默认情况下呈现 \Views\Home\Index.cshtml 视图模板时，我们编写类似下面的代码中我们 HomeController:</span><span class="sxs-lookup"><span data-stu-id="c2e7e-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="c2e7e-131">Visual Web Developer 中创建并打开"Index.cshtml"视图模板之后我们单击"添加视图"对话框中的"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="c2e7e-132">Index.cshtml 的内容如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="c2e7e-133">此视图使用 Razor 语法，这是比使用 ASP.NET Web 窗体和 ASP.NET MVC 的以前版本中的 Web 窗体视图引擎更简洁。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="c2e7e-134">Web 窗体视图引擎在 ASP.NET MVC 3 中仍然可用，但许多开发人员查找 Razor 视图引擎的确非常适合 ASP.NET MVC 开发。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="c2e7e-135">前三行设置页面标题使用 ViewBag.Title。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="c2e7e-136">我们将看看这的工作原理更详细地推出，但首先让我们更新文本标题文本，并查看该页面。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="c2e7e-137">更新&lt;h2&gt;标记可以说"这是主页上"，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="c2e7e-138">运行我们的新文本可见的主页上，应用程序所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="c2e7e-139">有关通用站点元素中使用的布局</span><span class="sxs-lookup"><span data-stu-id="c2e7e-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="c2e7e-140">大多数网站有很多页间共享的内容： 导航、 页脚、 徽标图像、 样式表的引用，等等。Razor 视图引擎使这更容易地管理使用名为页\_Layout.cshtml 自动创建的对我们在/视图/共享文件夹。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="c2e7e-141">双击此文件夹以查看内容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="c2e7e-142">我们的单个视图中的内容将显示的@RenderBody（） 命令中，我们想要出现在之外的任何公共内容可以添加到\_Layout.cshtml 标记。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="c2e7e-143">我们需要我们 MVC Music 商店到在站点中的所有页面上我们主页上和应用商店区域均具有链接的常见标头，以便我们将它添加到正上方的模板@RenderBody（） 语句。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="c2e7e-144">更新了样式表</span><span class="sxs-lookup"><span data-stu-id="c2e7e-144">Updating the StyleSheet</span></span>

<span data-ttu-id="c2e7e-145">空项目模板包含一个非常简化的 CSS 文件只包括用来显示验证消息的样式。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="c2e7e-146">我们的设计器提供了一些额外的 CSS 和图像，因此我们将添加中现在定义我们的站点，外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="c2e7e-147">可在 MvcMusicStore Assets.zip 的内容目录中包含的更新后的 CSS 文件和映像[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="c2e7e-148">我们将在 Windows 资源管理器中选择这两个文件，并将其放入在 Visual Web Developer 中，我们的解决方案的 Content 文件夹中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="c2e7e-149">您将需要确认你是否要覆盖现有 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="c2e7e-150">单击是。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="c2e7e-151">你的应用程序的 Content 文件夹现在将出现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="c2e7e-152">现在让我们运行该应用程序并查看我们更改的主页上的效果。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="c2e7e-153">让我们回顾一下会发生什么变化： HomeController 索引操作方法找到并显示 \Views\Home\Index.cshtmlView 模板，即使我们的代码称为"返回 View()"，因为我们查看模板遵循标准的命名约定。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="c2e7e-154">主页上显示 \Views\Home\Index.cshtml 视图模板中定义一个简单的欢迎使用消息。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="c2e7e-155">使用主页上我们\_Layout.cshtml 模板，因此欢迎使用消息包含在标准站点 HTML 布局。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="c2e7e-156">使用模型将信息传递到视图</span><span class="sxs-lookup"><span data-stu-id="c2e7e-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="c2e7e-157">只是显示了硬编码 HTML 的视图模板不会给非常有趣的 web 站点。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="c2e7e-158">若要创建动态网站，我们将改为想要将信息从控制器操作传递到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="c2e7e-159">在模型-视图-控制器模式中，的术语模型是指将对象表示在应用程序中的数据。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="c2e7e-160">通常情况下，模型对象对应于表在数据库中，但他们就不需要。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="c2e7e-161">返回一个 ActionResult 控制器操作方法可以将模型对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="c2e7e-162">这允许进行完全以生成响应，然后将此信息传递到视图模板所需的所有信息打包控制器用于生成相应的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="c2e7e-163">这是最容易理解通过查看运行中，让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="c2e7e-164">首先，我们将创建一些模型类来表示在我们存储的类型和唱片集。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="c2e7e-165">让我们首先创建一个类型的类。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="c2e7e-166">右键单击你的项目中的"Models"文件夹中，选择"添加类"选项，并将文件命名"Genre.cs"。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="c2e7e-167">然后将名称属性的公共字符串添加到已创建的类：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="c2e7e-168">*注意： 在您想知道的情况下 {get; 设置;} 表示法进行 C# 的自动实现的属性功能的使用。这为我们提供一个属性的优点而无需我们声明支持字段。*</span><span class="sxs-lookup"><span data-stu-id="c2e7e-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="c2e7e-169">接下来，请按照相同的步骤来创建一个具有标题和流派属性的唱片集类 （名为 Album.cs）：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="c2e7e-170">现在我们可以修改 StoreController 若要使用它显示我们的模型中的动态信息的视图。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="c2e7e-171">如果-出于演示目的-现在我们名为我们根据请求 ID 的唱片集，我们无法显示该信息，如下面的视图中所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="c2e7e-172">我们将开始通过更改存储详细信息操作，因此它显示的是一个唱片集信息。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="c2e7e-173">将"using"语句添加到顶部**StoreControllers**类，以包含 MvcMusicStore.Models 命名空间，因此我们无需键入 MvcMusicStore.Models.Album，每次我们想要使用的唱片集类。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="c2e7e-174">此类的"using"部分现在应显示如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="c2e7e-175">接下来，我们将更新的详细信息控制器操作，以便它返回 ActionResult 而不是一个字符串，正如我们做了 HomeController 的索引方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="c2e7e-176">现在我们可以修改逻辑，以返回到视图的唱片集对象。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="c2e7e-177">本教程中稍后我们将会从数据库检索数据 – 但现在我们将使用"虚拟数据"以开始。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="c2e7e-178">*注意： 如果您熟悉 C#，您可能会假定使用 var 意味着我们唱片集的变量是后期绑定。不正确-C# 编译器所使用类型推理基于什么我们要分配给该变量来确定该唱片集属于类型唱片集和编译本地唱片集变量作为唱片集类型，因此我们获得编译时检查的 Visual Studio 代码编辑器支持。*</span><span class="sxs-lookup"><span data-stu-id="c2e7e-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="c2e7e-179">让我们现在创建一个使用我们的唱片集来生成 HTML 响应的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="c2e7e-180">在此之前，我们需要生成项目，以便添加视图对话框知道我们新创建的唱片集类。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="c2e7e-181">可以生成项目通过选择 Debug⇨Build MvcMusicStore 菜单项 （for 额外信用额度，你可以使用 Ctrl-Shift-B 快捷方式以生成项目）。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="c2e7e-182">现在，我们设置了我们支持类，我们可以开始构建我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="c2e7e-183">在详细信息方法内右键单击并从上下文菜单中选择"添加视图..."。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="c2e7e-184">我们要创建新的视图模板像 HomeController 与之前执行。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="c2e7e-185">因为我们将从 StoreController 创建它将默认情况下生成 \Views\Store\Index.cshtml 文件中。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="c2e7e-186">不同于之前，我们将选中"创建强类型"视图复选框。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="c2e7e-187">然后将我们选择"视图数据类"下拉 downlist 中我们"唱片集"的类。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="c2e7e-188">这将导致"添加视图"对话框来创建视图模板所需的对象将传递给它要使用的相册。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="c2e7e-189">当我们单击"添加"按钮时将创建我们 \Views\Store\Details.cshtml 视图模板，包含以下代码。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="c2e7e-190">请注意，该值指示此视图为强类型化为我们唱片集的类的第一行。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="c2e7e-191">Razor 视图引擎能够理解，它已被传递唱片集对象，因此我们可以轻松访问模型属性，并甚至具有 Visual Web Developer 编辑器中的 IntelliSense 优势。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="c2e7e-192">更新&lt;h2&gt;标记，以便它显示的唱片集标题属性修改的行才会显示，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="c2e7e-193">请注意时输入超过这个有效期之后，会触发智能感知@Model关键字，显示的属性和唱片集类支持的方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="c2e7e-194">让我们现在重新运行我们的项目，并访问应用商店/详细信息/5 URL。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="c2e7e-195">我们将看到类似如下的相册的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="c2e7e-196">现在我们将使应用商店浏览操作方法类似的更新。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="c2e7e-197">更新的方法，使其返回一个 ActionResult，并修改方法逻辑，因此它将创建一个新的流派对象并将其返回到视图。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="c2e7e-198">浏览方法中右键单击并从上下文菜单中，选择"添加视图..."，然后添加了强类型化的视图将强类型化添加到流派类。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="c2e7e-199">更新&lt;h2&gt;视图中的元素中的代码 （/Views/Store/Browse.cshtml) 以显示类型信息。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="c2e7e-200">现在让我们重新运行我们的项目，并浏览到应用商店/浏览？Genre = Disco 的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="c2e7e-201">我们将看到浏览页显示如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="c2e7e-202">最后，让我们进行的稍微复杂更新**存储索引**操作方法和视图，以显示我们的存储区中的所有影片类型列表。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="c2e7e-203">我们将为我们的模型对象，而不只是单个流派使用流派列表来执行的操作。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="c2e7e-204">存储索引操作方法中右键单击并选择添加视图之前，选择流派作为模型类，并按添加按钮。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="c2e7e-205">首先我们将更改@model声明，以指示该视图将期望出现多个流派对象而不是只是一个。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="c2e7e-206">更改 /Store/Index.cshtml 读取，如下所示的第一行：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="c2e7e-207">这将告知 Razor 视图引擎，它将使用可以容纳多个流派对象的模型对象。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="c2e7e-208">我们使用 IEnumerable&lt;流派&gt;而不是列表&lt;流派&gt;由于它是更通用，让我们能够将我们的模型类型更高版本更改为任何支持 IEnumerable 接口的对象类型。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="c2e7e-209">接下来，我们将循环访问下面的代码已完成的视图中所示的模型中的类型对象。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="c2e7e-210">请注意，我们具有完全 IntelliSense 支持在进入此代码中，以便当我们键入"@Model。"</span><span class="sxs-lookup"><span data-stu-id="c2e7e-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="c2e7e-211">我们看到的所有方法和支持 IEnumerable of type Genre 的属性。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="c2e7e-212">在我们"foreach"循环中，Visual Web 开发人员知道，每个项的类型是类型，因此我们会看到 IntelliSense 每个流派类型。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="c2e7e-213">接下来，基架功能检查流派对象，并确定，每个将包含一个 Name 属性，因此它循环访问，并将其输出。它还会生成每个单个项目的编辑、 详细信息和删除链接。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="c2e7e-214">我们将利用这一点，更高版本中我们商店经理处，但现在我们想要改为具有一个简单的列表。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="c2e7e-215">当我们运行该应用程序，并浏览到 /Store 时，我们看到显示的计数和的类型列表。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="c2e7e-216">页之间添加链接</span><span class="sxs-lookup"><span data-stu-id="c2e7e-216">Adding Links between pages</span></span>

<span data-ttu-id="c2e7e-217">我们目前列出了流派的 /Store URL 只需以明文形式列出类型名称。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="c2e7e-218">让我们来更改这使而不是纯文本我们改为具有流派名称链接到相应的应用商店/浏览 URL，以便单击某个音乐类型，如"Disco"将导航到应用商店/浏览？ genre = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="c2e7e-219">我们无法更新 \Views\Store\Index.cshtml 视图模板为使用这些链接的代码类似如下的输出 **（不要键入考虑到这-我们将改进）**:</span><span class="sxs-lookup"><span data-stu-id="c2e7e-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="c2e7e-220">操作成功，但它可能会导致问题更高版本，因为它依赖于硬编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="c2e7e-221">例如，如果我们想要重命名控制器，我们需要我们寻找需要更新的链接的代码中进行搜索。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="c2e7e-222">我们可以使用一种替代方法是利用 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="c2e7e-223">ASP.NET MVC 包括可从我们的视图模板代码以执行各种常见任务，就像下面这样的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="c2e7e-224">Html.ActionLink() 帮助器方法是一个特别有用，并轻松地生成 HTML &lt;&gt;链接，并负责令人讨厌的详细信息，如确保 URL 路径为正确编码的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="c2e7e-225">Html.ActionLink() 有多个不同的重载，以允许指定尽可能为你的链接所需的信息。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="c2e7e-226">在最简单的情况下，将提供只是链接文本和要在客户端上单击超链接时转到的操作方法。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="c2e7e-227">例如，我们可以链接到"应用商店 /"链接文本"转到存储索引"使用以下调用存储详细信息页上的 index （） 方法：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="c2e7e-228">*注意： 在这种情况下，我们不需要指定控制器名称，因为我们只链接到同一呈现当前视图的控制器内的另一个动作。*</span><span class="sxs-lookup"><span data-stu-id="c2e7e-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="c2e7e-229">我们浏览页面的链接需要传递一个参数，不过，因此我们将使用另一个重载采用三个参数的 Html.ActionLink 方法：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="c2e7e-230">链接文本，将显示类型名称</span><span class="sxs-lookup"><span data-stu-id="c2e7e-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="c2e7e-231">控制器操作名称 （浏览）</span><span class="sxs-lookup"><span data-stu-id="c2e7e-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="c2e7e-232">路由参数值，指定的名称 （类型） 和值 （类型名称）</span><span class="sxs-lookup"><span data-stu-id="c2e7e-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="c2e7e-233">将它们组合在一起此处向存储区索引视图，我们就将编写这些链接：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="c2e7e-234">现在我们再次运行我们的项目并访问 /Store/ URL 时我们会看到影片类型列表。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="c2e7e-235">每个流派是超链接 – 单击时它会引导我们完成到我们/Store/浏览？ genre =*[类型]* URL。</span><span class="sxs-lookup"><span data-stu-id="c2e7e-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="c2e7e-236">流派列表的 HTML 如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2e7e-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> <span data-ttu-id="c2e7e-237">[上一页](mvc-music-store-part-2.md)
> [下一页](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="c2e7e-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
