---
uid: single-page-application/overview/templates/breezeangular-template
title: 轻松/角模板 |Microsoft 文档
author: madskristensen
description: 轻松/角单页面应用程序模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/08/2013
ms.topic: article
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: faf28a510a83b7fa07585904344176601c2e1f34
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26506686"
---
<a name="breezeangular-template"></a><span data-ttu-id="2c812-103">轻松/角模板</span><span class="sxs-lookup"><span data-stu-id="2c812-103">Breeze/Angular template</span></span>
====================
<span data-ttu-id="2c812-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="2c812-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="2c812-105">轻松/角 MVC 模板是编写的选区钟形</span><span class="sxs-lookup"><span data-stu-id="2c812-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="2c812-106">下载轻松/角度 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="2c812-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)


<span data-ttu-id="2c812-107">[AngularJS](http://angularjs.org)用于构建单页面应用程序 (Spa) 是从 Google 一个开放源代码库。</span><span class="sxs-lookup"><span data-stu-id="2c812-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="2c812-108">它提供数据绑定、 依赖关系注入和屏幕管理。</span><span class="sxs-lookup"><span data-stu-id="2c812-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="2c812-109">将其与结合[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)，数据建模和数据管理，并且你的另一个开放源代码库具有很好的 HTML/JavaScript 客户端应用程序的基本成分。</span><span class="sxs-lookup"><span data-stu-id="2c812-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="2c812-110">轻松/角 SPA 模板上是一种变体[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)包含在 ASP.NET 和 Web Tools 2012.2 更新。</span><span class="sxs-lookup"><span data-stu-id="2c812-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="2c812-111">如果您有 Visual Studio，则必须示例 SPA 启动并正在运行 60 秒内。</span><span class="sxs-lookup"><span data-stu-id="2c812-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="2c812-112">表面上是，应用程序看起来非常相似 KnockoutJS SPA 模板。</span><span class="sxs-lookup"><span data-stu-id="2c812-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="2c812-113">但它是实质上却大不相同。</span><span class="sxs-lookup"><span data-stu-id="2c812-113">But it's quite different under the hood.</span></span> <span data-ttu-id="2c812-114">KnockoutJS 模板用于数据绑定和数据访问的原始 AJAX Knockout。</span><span class="sxs-lookup"><span data-stu-id="2c812-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="2c812-115">轻松/角模板使用角进行数据绑定和轻松进行数据访问。</span><span class="sxs-lookup"><span data-stu-id="2c812-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="2c812-116">这些库启用其他功能，包括页面导航和历史记录。</span><span class="sxs-lookup"><span data-stu-id="2c812-116">These libaries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="2c812-117">下面是应用程序的关于页上：</span><span class="sxs-lookup"><span data-stu-id="2c812-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="2c812-118">此页当前用户会话期间，将显示一份运行日志的事件包括：</span><span class="sxs-lookup"><span data-stu-id="2c812-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="2c812-119">分页。</span><span class="sxs-lookup"><span data-stu-id="2c812-119">Paging.</span></span> <span data-ttu-id="2c812-120">请注意在 #2 和快照 #7 在 Todo 控制器创建。</span><span class="sxs-lookup"><span data-stu-id="2c812-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="2c812-121">远程查询 (#3) 和本地缓存查询 (#7)。</span><span class="sxs-lookup"><span data-stu-id="2c812-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="2c812-122">保存新 （#5，6） 和修改 (#4) 实体。</span><span class="sxs-lookup"><span data-stu-id="2c812-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="2c812-123">在上验证客户端 (#9)，以便用户可以在提交更改之前更正错误到数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="2c812-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="2c812-124">多个要在此模板中，浏览包括：</span><span class="sxs-lookup"><span data-stu-id="2c812-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="2c812-125">动态加载的 HTML 视图模板。</span><span class="sxs-lookup"><span data-stu-id="2c812-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="2c812-126">通过角"指令。"的自定义数据绑定</span><span class="sxs-lookup"><span data-stu-id="2c812-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="2c812-127">模块性和依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="2c812-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="2c812-128">查询筛选器、 排序、 分页、 投影和包含相关实体。</span><span class="sxs-lookup"><span data-stu-id="2c812-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="2c812-129">跨多个屏幕共享数据。</span><span class="sxs-lookup"><span data-stu-id="2c812-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="2c812-130">作为单个事务中保存多个更改。</span><span class="sxs-lookup"><span data-stu-id="2c812-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="2c812-131">验证规则传播自动从服务器到 JavaScript 客户端。</span><span class="sxs-lookup"><span data-stu-id="2c812-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="2c812-132">让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="2c812-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="2c812-133">创建一个角度轻松/模板项目</span><span class="sxs-lookup"><span data-stu-id="2c812-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="2c812-134">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="2c812-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="2c812-135">模板被打包为 Visual Studio 扩展 (VSIX) 文件。</span><span class="sxs-lookup"><span data-stu-id="2c812-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="2c812-136">你可能需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2c812-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="2c812-137">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="2c812-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="2c812-138">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="2c812-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2c812-139">在项目模板列表中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="2c812-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="2c812-140">命名该项目并单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="2c812-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="2c812-141">在**新项目**向导中，选择**轻松角度 SPA**。</span><span class="sxs-lookup"><span data-stu-id="2c812-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="2c812-142">按 Ctrl + F5 生成并运行应用程序而不进行调试，或按 F5 边运行边调试。</span><span class="sxs-lookup"><span data-stu-id="2c812-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="2c812-143">第一次运行应用程序，它会显示登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="2c812-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="2c812-144">单击"注册"链接和新的页种到视图中，你可以在其中输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="2c812-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="2c812-145">（登录名和注册页是使用 ASP.NET MVC 构建。）当提交注册表单时，服务器会生成你的帐户提供两个项目的 TodoList。</span><span class="sxs-lookup"><span data-stu-id="2c812-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="2c812-146">然后它将它们提供给你在上一个黄色的注释。</span><span class="sxs-lookup"><span data-stu-id="2c812-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="2c812-147">现在你已在上关于领土的 SPA 中。</span><span class="sxs-lookup"><span data-stu-id="2c812-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="2c812-148">所有内容你看到和遇到时操作 Todos 呈现中，管理 Knockout 和轻松的帮助客户端上。</span><span class="sxs-lookup"><span data-stu-id="2c812-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="2c812-149">作为用户浏览应用程序...</span><span class="sxs-lookup"><span data-stu-id="2c812-149">Explore the app as a user …</span></span> <span data-ttu-id="2c812-150">但开发人员眼睛。</span><span class="sxs-lookup"><span data-stu-id="2c812-150">but with a developer's eye.</span></span> <span data-ttu-id="2c812-151">在浏览器中使用的开发人员工具来捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="2c812-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="2c812-152">(在 Internet Explorer： 按 f12 键，选择**网络**卡，然后单击**开始捕获**。)现在请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="2c812-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="2c812-153">添加新的 Todo 项。</span><span class="sxs-lookup"><span data-stu-id="2c812-153">Add a new Todo item.</span></span>
- <span data-ttu-id="2c812-154">单击标签和编辑 Todo 项标题</span><span class="sxs-lookup"><span data-stu-id="2c812-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="2c812-155">选中复选框以将标记项完成。</span><span class="sxs-lookup"><span data-stu-id="2c812-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="2c812-156">请注意已禁用文本框中，所以标题不再可编辑。</span><span class="sxs-lookup"><span data-stu-id="2c812-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="2c812-157">单击右侧的标签的 'x'。</span><span class="sxs-lookup"><span data-stu-id="2c812-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="2c812-158">该项目将消失，从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="2c812-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="2c812-159">选择另一个项，并清除其标题。</span><span class="sxs-lookup"><span data-stu-id="2c812-159">Pick another item and clear its title.</span></span> <span data-ttu-id="2c812-160">你将获得标题需要一个验证错误。</span><span class="sxs-lookup"><span data-stu-id="2c812-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="2c812-161">简要暂停后，将还原以前的标题。</span><span class="sxs-lookup"><span data-stu-id="2c812-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="2c812-162">键入在可以极为长标题。</span><span class="sxs-lookup"><span data-stu-id="2c812-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="2c812-163">你将获得不同的验证错误的标题太长。</span><span class="sxs-lookup"><span data-stu-id="2c812-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="2c812-164">单击"添加 Todo 列表"按钮。</span><span class="sxs-lookup"><span data-stu-id="2c812-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="2c812-165">前面的列表左侧将显示新列表。</span><span class="sxs-lookup"><span data-stu-id="2c812-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="2c812-166">播放使用触发其所需的 TodoList 标题和长度验证。</span><span class="sxs-lookup"><span data-stu-id="2c812-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="2c812-167">单击在标题文本框中，若要清除的错误消息。</span><span class="sxs-lookup"><span data-stu-id="2c812-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="2c812-168">单击要删除任务列表和其 todos 右上角圆圈，圆圈中的"x"。</span><span class="sxs-lookup"><span data-stu-id="2c812-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="2c812-169">单击右上角，若要查看这些活动日志中的"关于"链接。</span><span class="sxs-lookup"><span data-stu-id="2c812-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="2c812-170">验证逻辑是通过轻松执行的客户端。</span><span class="sxs-lookup"><span data-stu-id="2c812-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="2c812-171">在的服务器模型类验证特性是传播到客户端，并且自动执行之前客户端与服务器联系。</span><span class="sxs-lookup"><span data-stu-id="2c812-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="2c812-172">查看网络流量。</span><span class="sxs-lookup"><span data-stu-id="2c812-172">Review the network traffic.</span></span> <span data-ttu-id="2c812-173">请注意轻松检测到错误时的已连接到服务器的任何调用。</span><span class="sxs-lookup"><span data-stu-id="2c812-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="2c812-174">每个有效的更改导致 POST 请求为"/ api/Todo/SaveChanges"。</span><span class="sxs-lookup"><span data-stu-id="2c812-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="2c812-175">轻松将打包所做的更改并将其发送在一起以单个请求到 Web API 控制器`SaveChanges`方法。</span><span class="sxs-lookup"><span data-stu-id="2c812-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="2c812-176">这是不同于 KockoutJS SPA 模板，这使得 PUT、 POST 和单独删除每个项的请求。</span><span class="sxs-lookup"><span data-stu-id="2c812-176">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="2c812-177">此外，请注意没有任何网络流量时切换之间任务列表和有关页。</span><span class="sxs-lookup"><span data-stu-id="2c812-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="2c812-178">这是因为已到本地缓存中轻松约束查询。</span><span class="sxs-lookup"><span data-stu-id="2c812-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="2c812-179">在查看</span><span class="sxs-lookup"><span data-stu-id="2c812-179">Peek inside</span></span>

<span data-ttu-id="2c812-180">此应用程序具有客户端和服务器端。</span><span class="sxs-lookup"><span data-stu-id="2c812-180">This application has a client side and a server side.</span></span> <span data-ttu-id="2c812-181">客户端堆栈组成少量 HTML 和应用程序 JavaScript 模块 （在"应用"文件夹中） 的组合以及第三方 JavaScript 库 （在"脚本"文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="2c812-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="2c812-182">UI 体系结构控制器中的支持演示文稿代码分离开来的视图的 HTML 小组件。</span><span class="sxs-lookup"><span data-stu-id="2c812-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="2c812-183">角度的数据绑定系统协调视图和控制器，以便每个可以完成其他直接不知情的情况下操作。</span><span class="sxs-lookup"><span data-stu-id="2c812-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="2c812-184">控制器要求的数据上下文，以获取并保存模型实体。</span><span class="sxs-lookup"><span data-stu-id="2c812-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="2c812-185">数据上下文委托的大部分工作到轻松，构造自跟踪模型对象从 JSON 查询结果。</span><span class="sxs-lookup"><span data-stu-id="2c812-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="2c812-186">一些开发人员代码和三个原则.NET 库的服务器端堆栈组成： Web API、 实体框架和 Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="2c812-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="2c812-187">KockoutJS SPA 模板相同的基本体系结构。</span><span class="sxs-lookup"><span data-stu-id="2c812-187">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="2c812-188">但是，实现是要简单得多： Dto 已删除，并且大部分的实体框架的详细信息已委派给 Breeze.NET。</span><span class="sxs-lookup"><span data-stu-id="2c812-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c812-189">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2c812-189">Next Steps</span></span>

<span data-ttu-id="2c812-190">我们建议你浏览代码中，由指导[全面讨论](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)的客户端和服务器堆栈轻松网站上的。</span><span class="sxs-lookup"><span data-stu-id="2c812-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="2c812-191">你可以尝试 playing with 轻松客户端查询; 使用添加某些筛选器和排序。</span><span class="sxs-lookup"><span data-stu-id="2c812-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="2c812-192">你可以添加更多的模型属性和多个实体来更好地感受用于端到端 SPA 开发。</span><span class="sxs-lookup"><span data-stu-id="2c812-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="2c812-193">当你确信的设计时，你可以拉出 Todo 功能并将它们替换为你自己。</span><span class="sxs-lookup"><span data-stu-id="2c812-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="2c812-194">祝你编码愉快！</span><span class="sxs-lookup"><span data-stu-id="2c812-194">Happy coding!</span></span>
