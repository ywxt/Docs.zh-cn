---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 模板 |Microsoft Docs
author: xqiu
description: EmberJS 模板
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: fbc3b1d299ace27d38d895e42b8e3bb3b51b36f8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825660"
---
<a name="emberjs-template"></a><span data-ttu-id="0a5eb-103">EmberJS 模板</span><span class="sxs-lookup"><span data-stu-id="0a5eb-103">EmberJS template</span></span>
====================
<span data-ttu-id="0a5eb-104">通过[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="0a5eb-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="0a5eb-105">EmberJS MVC 模板是由 Nathan Totten、 Thiago Santos 和 Xinyang Qiu 编写的。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="0a5eb-106">下载 EmberJS MVC 模板</span><span class="sxs-lookup"><span data-stu-id="0a5eb-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="0a5eb-107">EmberJS SPA 模板是为帮助你开始快速构建交互式客户端的 web 应用使用 EmberJS 而设计的。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="0a5eb-108">"单页面应用程序"(SPA) 是加载单个 HTML 页面，然后页面动态更新，而不是加载新页面的 web 应用程序的常规术语。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="0a5eb-109">初始页面加载后 SPA 通过 AJAX 请求与服务器通信。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="0a5eb-110">AJAX 是什么新鲜事物，但如今有更加轻松地构建和维护大型复杂的 SPA 应用程序的 JavaScript 框架。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="0a5eb-111">此外，html5 和 CSS3 轻松地创建丰富的 Ui。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="0a5eb-112">EmberJS SPA 模板使用[Ember](http://emberjs.com/) JavaScript 库来处理从 AJAX 请求的页面更新。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="0a5eb-113">Ember.js 使用数据绑定与最新的数据同步页。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="0a5eb-114">这样一来，您无需编写任何代码，它将指导完成的 JSON 数据并更新 DOM</span><span class="sxs-lookup"><span data-stu-id="0a5eb-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="0a5eb-115">相反，你可以声明性属性置于告诉 Ember.js 如何呈现数据的 HTML。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="0a5eb-116">在服务器端 EmberJS 模板是几乎完全相同[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="0a5eb-117">它使用 ASP.NET MVC 为 HTML 文档和 ASP.NET Web API，以处理来自客户端 AJAX 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="0a5eb-118">有关模板的这些方面的详细信息，请参阅[KnockoutJS 模板](../introduction/knockoutjs-template.md)文档。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="0a5eb-119">本主题重点介绍 Knockout 模板和 EmberJS 模板之间的差异。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="0a5eb-120">创建 EmberJS SPA 模板项目</span><span class="sxs-lookup"><span data-stu-id="0a5eb-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="0a5eb-121">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="0a5eb-122">您可能需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="0a5eb-123">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="0a5eb-124">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="0a5eb-125">在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="0a5eb-126">命名项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="0a5eb-127">在中**新的项目**向导中，选择**Ember.js SPA 项目**。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="0a5eb-128">EmberJS SPA 模板概述</span><span class="sxs-lookup"><span data-stu-id="0a5eb-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="0a5eb-129">EmberJS 模板使用 jQuery、 Ember.js、 Handlebars.js 创建平滑的交互式用户界面的组合。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="0a5eb-130">Ember.js 是一个 JavaScript 库，使用客户端的 MVC 模式。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="0a5eb-131">一个*模板*、 书面 Handlebars 模板化语言，描述的应用程序用户界面。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="0a5eb-132">在发布模式下[Handlebars 编译器](https://github.com/Myslik/csharp-ember-handlebars)用于捆绑包和编译 handlebars 模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="0a5eb-133">一个*模型*将它从服务器 （待办事项列表和 ToDo 项） 中获取的应用程序数据存储。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="0a5eb-134">一个*控制器*存储应用程序状态。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-134">A *controller* stores application state.</span></span> <span data-ttu-id="0a5eb-135">控制器通常存在模型数据复制到相应的模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="0a5eb-136">一个*视图*将转换应用程序中的基元事件，并将传递给控制器。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="0a5eb-137">一个*路由器*管理应用程序状态，保持 Url 和模板的同步。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="0a5eb-138">此外，Ember 数据库可用于同步 （通过 RESTful API 从服务器获取） 的 JSON 对象和客户端模型。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="0a5eb-139">EmberJS SPA 模板将脚本组织到八个层：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="0a5eb-140">webapi\_adapter.js、 webapi\_serializer.js： 扩展了 Ember 数据库以使用 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="0a5eb-141">Scripts/helpers.js： 定义新的 Ember Handlebars 帮助器。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="0a5eb-142">Scripts/app.js： 创建应用程序，并配置适配器和序列化程序。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="0a5eb-143">脚本/应用/模型/\*.js： 定义模型。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="0a5eb-144">脚本/应用/视图/\*.js： 定义的视图。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="0a5eb-145">脚本/应用/控制器/\*.js： 定义控制器。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="0a5eb-146">脚本/应用/routes、 Scripts/app/router.js： 定义了路由。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="0a5eb-147">模板 /\*.hbs： 定义 handlebars 模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="0a5eb-148">让我们看一些更详细地这些脚本。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="0a5eb-149">模型</span><span class="sxs-lookup"><span data-stu-id="0a5eb-149">Models</span></span>

<span data-ttu-id="0a5eb-150">模型进行定义的脚本/应用/models 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="0a5eb-151">有两个模型文件： 将 todoitem.js 文件和 todoList.js。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="0a5eb-152">**todo.model.js**定义待办事项列表客户端 （浏览器） 模型。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="0a5eb-153">有两个模型类： todoItem 和 todoList。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="0a5eb-154">在 Ember 中，模型是 DS 子类。模型。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="0a5eb-155">一个模型可以有属性具有属性：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="0a5eb-156">模型可以与其他模型定义的关系：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="0a5eb-157">模型可以计算出绑定到其他属性的属性：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="0a5eb-158">模型可以具有一个观察到的属性更改时调用的观察者函数：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="0a5eb-159">视图</span><span class="sxs-lookup"><span data-stu-id="0a5eb-159">Views</span></span>

<span data-ttu-id="0a5eb-160">在脚本/app/views 文件夹中定义这些视图。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="0a5eb-161">视图将转换应用程序 UI 中的事件。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-161">A view translates events from the application UI.</span></span> <span data-ttu-id="0a5eb-162">事件处理程序可以调用返回控制器的功能，或只需直接调用数据上下文。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="0a5eb-163">例如，以下代码是从 views/TodoItemEditView.js。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="0a5eb-164">它定义的事件处理为输入的文本字段。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="0a5eb-165">控制器</span><span class="sxs-lookup"><span data-stu-id="0a5eb-165">Controller</span></span>

<span data-ttu-id="0a5eb-166">控制器定义的脚本/应用/controllers 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="0a5eb-167">若要表示单个模型，扩展`Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="0a5eb-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="0a5eb-168">在控制器还可以通过扩展表示的模型集合`Ember.ArrayController`。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="0a5eb-169">例如，TodoListController 表示数组的`todoList`对象。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="0a5eb-170">控制器按 todoList ID 以降序进行排序：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="0a5eb-171">控制器定义了一个名为函数`addTodoList`，它创建新的 todoList 并将其添加到数组。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="0a5eb-172">若要查看如何调用此函数，请打开名为 todoListTemplate.html，在模板文件夹中的模板文件。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="0a5eb-173">以下模板代码绑定到按钮`addTodoList`函数：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="0a5eb-174">该控制器还包含`error`属性，其中包含一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="0a5eb-175">下面是用于显示错误消息 （也在 todoListTemplate.html) 的模板代码：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="0a5eb-176">路由</span><span class="sxs-lookup"><span data-stu-id="0a5eb-176">Routes</span></span>

<span data-ttu-id="0a5eb-177">Router.js 定义的路由和默认模板，以显示，还设置了应用程序状态，并与 Url 匹配的路由：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="0a5eb-178">TodoListRoute.js 加载通过重写 setupController 函数 TodoListRoute 的数据：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="0a5eb-179">Ember 使用命名约定来匹配 Url、 路由名称、 控制器和模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="0a5eb-180">有关详细信息，请参阅[ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) EmberJS 文档。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="0a5eb-181">模板</span><span class="sxs-lookup"><span data-stu-id="0a5eb-181">Templates</span></span>

<span data-ttu-id="0a5eb-182">模板文件夹包含四个模板：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="0a5eb-183">application.hbs： 启动应用程序时呈现的默认模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="0a5eb-184">about.hbs:"/ 关于"路由模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="0a5eb-185">index.hbs： 根模板"/"的路由。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="0a5eb-186">todoList.hbs： 的模板"/ todo"路由。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="0a5eb-187">\_navbar.hbs: 模板定义导航菜单。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="0a5eb-188">应用程序模板的作用类似于主页面。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-188">The application template acts like a master page.</span></span> <span data-ttu-id="0a5eb-189">它包含一个标头、 页脚和"{{outlet}}"要插入的路由中的其他模板。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="0a5eb-190">有关在 Ember 中的应用程序模板的详细信息，请参阅[ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="0a5eb-191">"/ TodoList"模板包含两个循环表达式。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="0a5eb-192">外部循环是`{{#each controller}}`，并内部循环是`{{#each todos}}`。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="0a5eb-193">以下代码显示了内置`Ember.Checkbox`查看，以自定义`App.TodoItemEditView`，并使用链接`deleteTodo`操作。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="0a5eb-194">`HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs 中, 定义的类定义一个帮助程序函数来缓存，并插入模板文件时**调试**设置为**true** Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="0a5eb-195">从 Views/Home/App.cshtml 中定义的 ASP.NET MVC 视图文件调用此函数：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="0a5eb-196">调用不带任何参数，该函数将呈现的所有模板文件的模板文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="0a5eb-197">此外可以指定一个子文件夹或特定的模板文件。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="0a5eb-198">当**调试**是**false**在 Web.config 中，该应用程序包括绑定项"~/bundles/templates"。</span><span class="sxs-lookup"><span data-stu-id="0a5eb-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="0a5eb-199">此捆绑包项将添加在 BundleConfig.cs，使用 Handlebars 编译器库：</span><span class="sxs-lookup"><span data-stu-id="0a5eb-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
