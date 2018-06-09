---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 模板 |Microsoft 文档
author: xqiu
description: EmberJS 模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1fb7633aee288be648d4f9681b43c8911b7dbab9
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26506796"
---
<a name="emberjs-template"></a><span data-ttu-id="e422f-103">EmberJS 模板</span><span class="sxs-lookup"><span data-stu-id="e422f-103">EmberJS template</span></span>
====================
<span data-ttu-id="e422f-104">通过[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="e422f-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="e422f-105">EmberJS MVC 模板是由 Nathan totten 所写、 Thiago Santos 和 Xinyang Qiu 写入。</span><span class="sxs-lookup"><span data-stu-id="e422f-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="e422f-106">下载 EmberJS MVC 模板</span><span class="sxs-lookup"><span data-stu-id="e422f-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="e422f-107">EmberJS SPA 模板旨在让您快速构建使用 EmberJS 的客户端的交互式 web 应用。</span><span class="sxs-lookup"><span data-stu-id="e422f-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="e422f-108">"单页面应用程序"(SPA) 是常规的 web 应用程序加载单个 HTML 页，然后而不是加载新页面，动态地更新页术语。</span><span class="sxs-lookup"><span data-stu-id="e422f-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="e422f-109">初始页加载后, SPA 介绍与通过 AJAX 请求服务器。</span><span class="sxs-lookup"><span data-stu-id="e422f-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="e422f-110">AJAX 已是老生常谈，但目前有更加轻松地生成和维护一个大型的复杂的 SPA 应用程序的 JavaScript 框架。</span><span class="sxs-lookup"><span data-stu-id="e422f-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="e422f-111">此外，html5 和 CSS3 使其更方便地创建丰富的用户界面。</span><span class="sxs-lookup"><span data-stu-id="e422f-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="e422f-112">EmberJS SPA 模板使用[Ember](http://emberjs.com/) JavaScript 库来处理从 AJAX 请求的页更新。</span><span class="sxs-lookup"><span data-stu-id="e422f-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="e422f-113">Ember.js 使用数据绑定来使用最新的数据同步页。</span><span class="sxs-lookup"><span data-stu-id="e422f-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="e422f-114">这样一来，你无需编写任何代码，它将指导完成的 JSON 数据并更新 DOM</span><span class="sxs-lookup"><span data-stu-id="e422f-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="e422f-115">相反，你可以声明性属性置于告诉 Ember.js 如何将数据呈现的 HTML。</span><span class="sxs-lookup"><span data-stu-id="e422f-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="e422f-116">在服务器端，EmberJS 模板是几乎与[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)。</span><span class="sxs-lookup"><span data-stu-id="e422f-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="e422f-117">它使用 ASP.NET MVC 为 HTML 文档和 ASP.NET Web API，以处理来自客户端 AJAX 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="e422f-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="e422f-118">有关模板的这些方面的问题的详细信息，请参阅[KnockoutJS 模板](../introduction/knockoutjs-template.md)文档。</span><span class="sxs-lookup"><span data-stu-id="e422f-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="e422f-119">本主题重点介绍 Knockout 模板和 EmberJS 模板之间的差异。</span><span class="sxs-lookup"><span data-stu-id="e422f-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="e422f-120">创建 EmberJS SPA 模板项目</span><span class="sxs-lookup"><span data-stu-id="e422f-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="e422f-121">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="e422f-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="e422f-122">你可能需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e422f-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="e422f-123">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="e422f-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="e422f-124">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="e422f-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="e422f-125">在项目模板列表中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="e422f-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="e422f-126">命名该项目并单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="e422f-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="e422f-127">在**新项目**向导中，选择**Ember.js SPA 项目**。</span><span class="sxs-lookup"><span data-stu-id="e422f-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="e422f-128">EmberJS SPA 模板概述</span><span class="sxs-lookup"><span data-stu-id="e422f-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="e422f-129">EmberJS 模板使用 jQuery，Ember.js，Handlebars.js 创建平滑的交互式 UI 的组合。</span><span class="sxs-lookup"><span data-stu-id="e422f-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="e422f-130">Ember.js 是一个 JavaScript 库，使用客户端 MVC 模式。</span><span class="sxs-lookup"><span data-stu-id="e422f-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="e422f-131">A*模板*、 在车模板化语言中，写入描述应用程序用户界面。</span><span class="sxs-lookup"><span data-stu-id="e422f-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="e422f-132">在发布模式下，[车编译器](https://github.com/Myslik/csharp-ember-handlebars)用于捆绑在一起并编译车模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="e422f-133">A*模型*将它从 （ToDo 列表和 ToDo 项） 的服务器获取的应用程序数据存储。</span><span class="sxs-lookup"><span data-stu-id="e422f-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="e422f-134">A*控制器*存储应用程序状态。</span><span class="sxs-lookup"><span data-stu-id="e422f-134">A *controller* stores application state.</span></span> <span data-ttu-id="e422f-135">控制器通常存在模型数据复制到相应的模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="e422f-136">A*视图*转换从应用程序的基元事件并将传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="e422f-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="e422f-137">A*路由器*管理应用程序状态，从而 Url 和模板同步。</span><span class="sxs-lookup"><span data-stu-id="e422f-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="e422f-138">此外，Ember 数据库可用于同步 （通过 RESTful API 从服务器获取） 的 JSON 对象和客户端模型。</span><span class="sxs-lookup"><span data-stu-id="e422f-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="e422f-139">EmberJS SPA 模板将脚本整理为八个层：</span><span class="sxs-lookup"><span data-stu-id="e422f-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="e422f-140">webapi\_adapter.js、 webapi\_serializer.js： 扩展 Ember 数据库为使用 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="e422f-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="e422f-141">Scripts/helpers.js： 定义新 Ember 车帮助器。</span><span class="sxs-lookup"><span data-stu-id="e422f-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="e422f-142">Scripts/app.js： 创建应用程序，并配置适配器和序列化程序。</span><span class="sxs-lookup"><span data-stu-id="e422f-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="e422f-143">脚本/应用/模型/\*.js： 定义模型。</span><span class="sxs-lookup"><span data-stu-id="e422f-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="e422f-144">脚本/应用程序/视图/\*.js： 定义的视图。</span><span class="sxs-lookup"><span data-stu-id="e422f-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="e422f-145">脚本/应用程序/控制器/\*.js： 定义控制器。</span><span class="sxs-lookup"><span data-stu-id="e422f-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="e422f-146">脚本/应用程序/routes，Scripts/app/router.js： 定义路由。</span><span class="sxs-lookup"><span data-stu-id="e422f-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="e422f-147">模板 /\*.hbs： 定义车模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="e422f-148">让我们看看其中一些更详细地这些脚本。</span><span class="sxs-lookup"><span data-stu-id="e422f-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="e422f-149">模型</span><span class="sxs-lookup"><span data-stu-id="e422f-149">Models</span></span>

<span data-ttu-id="e422f-150">在脚本 / 应用 / 模型文件夹中定义模型。</span><span class="sxs-lookup"><span data-stu-id="e422f-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="e422f-151">有两个模型文件： todoItem.js 和 todoList.js。</span><span class="sxs-lookup"><span data-stu-id="e422f-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="e422f-152">**todo.model.js**定义待办事项列表客户端 （浏览器） 模型。</span><span class="sxs-lookup"><span data-stu-id="e422f-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="e422f-153">有两个模型类： todoItem 和 todoList。</span><span class="sxs-lookup"><span data-stu-id="e422f-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="e422f-154">在 Ember，模型是 DS 的子类。模型。</span><span class="sxs-lookup"><span data-stu-id="e422f-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="e422f-155">模型可以具有属性的属性：</span><span class="sxs-lookup"><span data-stu-id="e422f-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="e422f-156">模型可以与其他模型中定义的关系：</span><span class="sxs-lookup"><span data-stu-id="e422f-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="e422f-157">模型可以都计算将绑定到其他属性的属性：</span><span class="sxs-lookup"><span data-stu-id="e422f-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="e422f-158">模型可以观察到的属性更改时调用的观察程序函数：</span><span class="sxs-lookup"><span data-stu-id="e422f-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="e422f-159">视图</span><span class="sxs-lookup"><span data-stu-id="e422f-159">Views</span></span>

<span data-ttu-id="e422f-160">视图定义中的脚本/应用程序/views 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e422f-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="e422f-161">视图将应用程序 UI 中的事件。</span><span class="sxs-lookup"><span data-stu-id="e422f-161">A view translates events from the application UI.</span></span> <span data-ttu-id="e422f-162">事件处理程序可以回叫控制器函数，或只需直接调用的数据上下文。</span><span class="sxs-lookup"><span data-stu-id="e422f-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="e422f-163">例如，下面的代码是从 views/TodoItemEditView.js。</span><span class="sxs-lookup"><span data-stu-id="e422f-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="e422f-164">它定义的事件处理的输入的文本字段。</span><span class="sxs-lookup"><span data-stu-id="e422f-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="e422f-165">控制器</span><span class="sxs-lookup"><span data-stu-id="e422f-165">Controller</span></span>

<span data-ttu-id="e422f-166">控制器定义脚本/应用程序/controllers 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e422f-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="e422f-167">若要表示的一个模型，扩展`Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="e422f-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="e422f-168">控制器还可以通过扩展表示的模型集合`Ember.ArrayController`。</span><span class="sxs-lookup"><span data-stu-id="e422f-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="e422f-169">例如，TodoListController 表示数组的`todoList`对象。</span><span class="sxs-lookup"><span data-stu-id="e422f-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="e422f-170">控制器按 todoList ID，按降序进行排序：</span><span class="sxs-lookup"><span data-stu-id="e422f-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="e422f-171">控制器定义一个名为函数`addTodoList`，它创建新的 todoList 并将其添加到数组。</span><span class="sxs-lookup"><span data-stu-id="e422f-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="e422f-172">若要查看如何调用此函数获取，打开名为 todoListTemplate.html，模板文件夹中的模板文件。</span><span class="sxs-lookup"><span data-stu-id="e422f-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="e422f-173">下面的模板代码将绑定到按钮`addTodoList`函数：</span><span class="sxs-lookup"><span data-stu-id="e422f-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="e422f-174">控制器还包含`error`属性，其中包含一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="e422f-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="e422f-175">下面是要显示错误消息 （也在 todoListTemplate.html) 的模板代码：</span><span class="sxs-lookup"><span data-stu-id="e422f-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="e422f-176">路由</span><span class="sxs-lookup"><span data-stu-id="e422f-176">Routes</span></span>

<span data-ttu-id="e422f-177">Router.js 定义路由和默认模板，以显示，设置应用程序状态，并为路由匹配 Url:</span><span class="sxs-lookup"><span data-stu-id="e422f-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="e422f-178">TodoListRoute.js 为 TodoListRoute 中加载数据，通过重写 setupController 函数：</span><span class="sxs-lookup"><span data-stu-id="e422f-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="e422f-179">Ember 使用命名约定来匹配 Url、 路由名称、 控制器和模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="e422f-180">有关详细信息，请参阅[ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/)在 EmberJS 文档。</span><span class="sxs-lookup"><span data-stu-id="e422f-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="e422f-181">模板</span><span class="sxs-lookup"><span data-stu-id="e422f-181">Templates</span></span>

<span data-ttu-id="e422f-182">模板文件夹包含四个模板：</span><span class="sxs-lookup"><span data-stu-id="e422f-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="e422f-183">application.hbs： 时启动应用程序呈现的默认模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="e422f-184">about.hbs:"/ 关于"路由的模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="e422f-185">index.hbs： 根模板"/"的路由。</span><span class="sxs-lookup"><span data-stu-id="e422f-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="e422f-186">todoList.hbs： 的模板"/ todo"路由。</span><span class="sxs-lookup"><span data-stu-id="e422f-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="e422f-187">\_navbar.hbs: 模板定义导航菜单。</span><span class="sxs-lookup"><span data-stu-id="e422f-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="e422f-188">应用程序模板的作用类似母版页。</span><span class="sxs-lookup"><span data-stu-id="e422f-188">The application template acts like a master page.</span></span> <span data-ttu-id="e422f-189">它包含页眉、 页脚和"{{插座}}"可插入具体取决于路由中的其他模板。</span><span class="sxs-lookup"><span data-stu-id="e422f-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="e422f-190">有关 Ember 中的应用程序模板的详细信息，请参阅[ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)。</span><span class="sxs-lookup"><span data-stu-id="e422f-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="e422f-191">"/ TodoList"模板包含两个循环表达式。</span><span class="sxs-lookup"><span data-stu-id="e422f-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="e422f-192">外部循环是`{{#each controller}}`，与内部循环是`{{#each todos}}`。</span><span class="sxs-lookup"><span data-stu-id="e422f-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="e422f-193">下面的代码演示内置`Ember.Checkbox`查看，自定义`App.TodoItemEditView`，以及使用的链接`deleteTodo`操作。</span><span class="sxs-lookup"><span data-stu-id="e422f-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="e422f-194">`HtmlHelperExtensions` Controllers/HtmlHelperExensions.cs 中, 定义的类定义一个帮助器函数以缓存和插入模板文件时**调试**设置为**true** Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="e422f-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="e422f-195">从 Views/Home/App.cshtml 中定义的 ASP.NET MVC 视图文件调用此函数：</span><span class="sxs-lookup"><span data-stu-id="e422f-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="e422f-196">调用不带任何参数，该函数将呈现所有模板文件夹中的模板文件。</span><span class="sxs-lookup"><span data-stu-id="e422f-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="e422f-197">你还可以指定一个子文件夹或特定的模板文件。</span><span class="sxs-lookup"><span data-stu-id="e422f-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="e422f-198">当**调试**是**false**在 Web.config 中，该应用程序包括捆绑项"~/bundles/templates"。</span><span class="sxs-lookup"><span data-stu-id="e422f-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="e422f-199">BundleConfig.cs，使用车编译器库中添加此捆绑包项目：</span><span class="sxs-lookup"><span data-stu-id="e422f-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
