---
uid: single-page-application/overview/templates/breezeknockout-template
title: 轻松/Knockout 模板 |Microsoft 文档
author: madskristensen
description: 轻松/Knockout 单页面应用程序模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 07ec099a0381458fe42c1972a2554f76fd34638c
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26506696"
---
<a name="breezeknockout-template"></a><span data-ttu-id="a7859-103">轻松/Knockout 模板</span><span class="sxs-lookup"><span data-stu-id="a7859-103">Breeze/Knockout template</span></span>
====================
<span data-ttu-id="a7859-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="a7859-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="a7859-105">轻松/Knockout MVC 模板是编写的选区钟形</span><span class="sxs-lookup"><span data-stu-id="a7859-105">The Breeze/Knockout MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="a7859-106">下载轻松/Knockout MVC 模板</span><span class="sxs-lookup"><span data-stu-id="a7859-106">Download the Breeze/Knockout MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282649)


<span data-ttu-id="a7859-107">听说的"单页面应用程序"(SPA) 并想知道它是什么。</span><span class="sxs-lookup"><span data-stu-id="a7859-107">You've heard of "single page application" (SPA) and wondered what it is.</span></span> <span data-ttu-id="a7859-108">您无法阅读有关它，你将而是亲身体验。</span><span class="sxs-lookup"><span data-stu-id="a7859-108">While you could read about it, you'd rather experience it for yourself.</span></span> <span data-ttu-id="a7859-109">但有时间来下载示例的人员？</span><span class="sxs-lookup"><span data-stu-id="a7859-109">But who has time to download a sample?</span></span> <span data-ttu-id="a7859-110">如果你具有 Visual Studio，你将示例 SPA 启动并使用 ASP.NET MVC 4"轻松/Knockout 单页面应用程序"模板运行在小于 60 秒。</span><span class="sxs-lookup"><span data-stu-id="a7859-110">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds with the ASP.NET MVC 4 "Breeze/Knockout Single Page Application" template.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a><span data-ttu-id="a7859-111">什么是轻松/Knockout SPA 模板？</span><span class="sxs-lookup"><span data-stu-id="a7859-111">What is the Breeze/Knockout SPA Template?</span></span>

<span data-ttu-id="a7859-112">大多数项目模板生成应用程序框架。</span><span class="sxs-lookup"><span data-stu-id="a7859-112">Most project templates generate an application skeleton.</span></span> <span data-ttu-id="a7859-113">通过添加你的代码置于这些骨骼 flesh 和最终提供有效的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7859-113">You put flesh on those bones by adding your code and eventually deliver a working application.</span></span> <span data-ttu-id="a7859-114">轻松/Knockout SPA 模板是不同的。</span><span class="sxs-lookup"><span data-stu-id="a7859-114">The Breeze/Knockout SPA template is different.</span></span> <span data-ttu-id="a7859-115">它会生成用于你来研究的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7859-115">It generates a sample application for you to study.</span></span> <span data-ttu-id="a7859-116">它演示了 SPA 应用程序设计和许多用于生成 SPA 的技术。</span><span class="sxs-lookup"><span data-stu-id="a7859-116">It demonstrates a SPA application design and many of the techniques for building a SPA.</span></span>

<span data-ttu-id="a7859-117">轻松/Knockout 模板上是一种变体[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)包含在 ASP.NET 和 Web Tools 2012.2 更新。</span><span class="sxs-lookup"><span data-stu-id="a7859-117">The Breeze/Knockout template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="a7859-118">轻松 SPA 模板生成的应用程序相同的用户体验，但它具有不同的实现，轻松使用数据管理的。</span><span class="sxs-lookup"><span data-stu-id="a7859-118">The Breeze SPA template generates an application with the same user experience, but it has a different implementation, using Breeze for data management.</span></span>

<span data-ttu-id="a7859-119">KnockoutJS SPA 模板发出与原始 jQuery AJAX 的服务请求足以满足简单的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7859-119">The KnockoutJS SPA template makes service requests with raw jQuery AJAX, which is adequate for a simple application.</span></span> <span data-ttu-id="a7859-120">但更复杂的应用程序必须满足更加严苛的数据管理要求。</span><span class="sxs-lookup"><span data-stu-id="a7859-120">But more sophisticated apps have more demanding data management requirements.</span></span> <span data-ttu-id="a7859-121">例如，大多数应用程序：</span><span class="sxs-lookup"><span data-stu-id="a7859-121">For example, most applications:</span></span>

- <span data-ttu-id="a7859-122">查询并重新在扩展的用户会话期间查询服务器。</span><span class="sxs-lookup"><span data-stu-id="a7859-122">Query and re-query the server during an extended user session.</span></span>
- <span data-ttu-id="a7859-123">添加查询筛选器，排序和分页。</span><span class="sxs-lookup"><span data-stu-id="a7859-123">Add query filters, sorting, and paging.</span></span>
- <span data-ttu-id="a7859-124">在多个屏幕之间共享相同的数据。</span><span class="sxs-lookup"><span data-stu-id="a7859-124">Share the same data across multiple screens.</span></span>
- <span data-ttu-id="a7859-125">累积到多个对象的更改，然后将其保存为单个事务。</span><span class="sxs-lookup"><span data-stu-id="a7859-125">Accumulate changes to many objects, then save them as a single transaction.</span></span>
- <span data-ttu-id="a7859-126">验证客户端上的更改，因此用户可以更改提交到数据库之前更正错误。</span><span class="sxs-lookup"><span data-stu-id="a7859-126">Validate changes on the client, so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="a7859-127">BreezeJS 库为你，释放你开发而言最为重要的应用程序逻辑和用户体验中处理这些日常任务。</span><span class="sxs-lookup"><span data-stu-id="a7859-127">The BreezeJS library handles these chores for you, freeing you to develop the application logic and user experience that matter most.</span></span>

<span data-ttu-id="a7859-128">[**轻松**](http://www.breezejs.com/?utm_source=ms-spa)是用于构建丰富的数据应用程序中 JavaScript 和 HTML，从历史上看已传递作为独立的桌面应用程序的应用类型的一个开源库。</span><span class="sxs-lookup"><span data-stu-id="a7859-128">[**Breeze**](http://www.breezejs.com/?utm_source=ms-spa) is an open source library for building rich data applications in JavaScript and HTML, the kinds of apps that have historically been delivered as stand-alone desktop applications.</span></span>

<span data-ttu-id="a7859-129">轻松/Knockout 模板可帮助你执行的更可靠的数据管理基础结构向该第一个关键步骤。</span><span class="sxs-lookup"><span data-stu-id="a7859-129">The Breeze/Knockout template helps you take that first crucial step toward a more robust data management infrastructure.</span></span> <span data-ttu-id="a7859-130">它将生成的示例 Todo 应用程序与 KnockoutJS SPA 模板表面上是相同。</span><span class="sxs-lookup"><span data-stu-id="a7859-130">It produces a sample Todo application that is outwardly identical to the KnockoutJS SPA template.</span></span> <span data-ttu-id="a7859-131">在内部，它替换轻松 AJAX 数据层，以便你可以比较两个接近并排显示。</span><span class="sxs-lookup"><span data-stu-id="a7859-131">On the inside, it replaces the AJAX data layer with Breeze, so you can compare the two approaches side-by-side.</span></span> <span data-ttu-id="a7859-132">当然，它只是涉及轻松应用程序的可能性。</span><span class="sxs-lookup"><span data-stu-id="a7859-132">Of course, it barely touches the potential of a Breeze application.</span></span> <span data-ttu-id="a7859-133">但是，你将看到轻松的工作原理和多么少需要以使该转换。</span><span class="sxs-lookup"><span data-stu-id="a7859-133">But you'll see how Breeze works and how little is required to make that transition.</span></span>

<span data-ttu-id="a7859-134">让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="a7859-134">Let's get started.</span></span>

## <a name="create-a-breezeknockout-template-project"></a><span data-ttu-id="a7859-135">创建一个轻松/Knockout 模板项目</span><span class="sxs-lookup"><span data-stu-id="a7859-135">Create a Breeze/Knockout Template Project</span></span>

<span data-ttu-id="a7859-136">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="a7859-136">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="a7859-137">模板被打包为 Visual Studio 扩展 (VSIX) 文件。</span><span class="sxs-lookup"><span data-stu-id="a7859-137">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="a7859-138">你可能需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a7859-138">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="a7859-139">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="a7859-139">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a7859-140">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="a7859-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a7859-141">在项目模板列表中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a7859-141">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="a7859-142">命名该项目并单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a7859-142">Name the project and click **OK**.</span></span>

<span data-ttu-id="a7859-143">在**新项目**向导中，选择**轻松 Knockout SPA**。</span><span class="sxs-lookup"><span data-stu-id="a7859-143">In the **New Project** wizard, select **Breeze Knockout SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

<span data-ttu-id="a7859-144">按 Ctrl + F5 生成并运行应用程序而不进行调试，或按 F5 边运行边调试。</span><span class="sxs-lookup"><span data-stu-id="a7859-144">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

<span data-ttu-id="a7859-145">第一次运行应用程序，它会显示登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="a7859-145">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="a7859-146">单击"注册"链接和新的页种到视图中，你可以在其中输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="a7859-146">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="a7859-147">（登录名和注册页是使用 ASP.NET MVC 构建。）当提交注册表单时，服务器会生成你的帐户提供两个项目的 TodoList。</span><span class="sxs-lookup"><span data-stu-id="a7859-147">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="a7859-148">然后它将它们提供给你在上一个黄色的注释。</span><span class="sxs-lookup"><span data-stu-id="a7859-148">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="a7859-149">现在你已在上关于领土的 SPA 中。</span><span class="sxs-lookup"><span data-stu-id="a7859-149">Now you are in the land of SPA.</span></span> <span data-ttu-id="a7859-150">所有内容你看到和遇到时操作 Todos 呈现中，管理 Knockout 和轻松的帮助客户端上。</span><span class="sxs-lookup"><span data-stu-id="a7859-150">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="a7859-151">作为用户浏览应用程序...</span><span class="sxs-lookup"><span data-stu-id="a7859-151">Explore the app as a user …</span></span> <span data-ttu-id="a7859-152">但开发人员眼睛。</span><span class="sxs-lookup"><span data-stu-id="a7859-152">but with a developer's eye.</span></span> <span data-ttu-id="a7859-153">在浏览器中使用的开发人员工具来捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="a7859-153">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="a7859-154">(在 Internet Explorer： 按 f12 键，选择**网络**卡，然后单击**开始捕获**。)现在请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="a7859-154">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="a7859-155">添加新的 Todo 项。</span><span class="sxs-lookup"><span data-stu-id="a7859-155">Add a new Todo item.</span></span>
- <span data-ttu-id="a7859-156">单击标签和编辑 Todo 项标题</span><span class="sxs-lookup"><span data-stu-id="a7859-156">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="a7859-157">选中复选框以将标记项完成。</span><span class="sxs-lookup"><span data-stu-id="a7859-157">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="a7859-158">请注意已禁用文本框中，所以标题不再可编辑。</span><span class="sxs-lookup"><span data-stu-id="a7859-158">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="a7859-159">单击右侧的标签的 'x'。</span><span class="sxs-lookup"><span data-stu-id="a7859-159">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="a7859-160">该项目将消失，从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="a7859-160">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="a7859-161">选择另一个项，并清除其标题。</span><span class="sxs-lookup"><span data-stu-id="a7859-161">Pick another item and clear its title.</span></span> <span data-ttu-id="a7859-162">你将获得标题需要一个验证错误。</span><span class="sxs-lookup"><span data-stu-id="a7859-162">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="a7859-163">简要暂停后，将还原以前的标题。</span><span class="sxs-lookup"><span data-stu-id="a7859-163">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="a7859-164">键入在可以极为长标题。</span><span class="sxs-lookup"><span data-stu-id="a7859-164">Type in a ridiculously long title.</span></span> <span data-ttu-id="a7859-165">你将获得不同的验证错误的标题太长。</span><span class="sxs-lookup"><span data-stu-id="a7859-165">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="a7859-166">单击"添加 Todo 列表"按钮。</span><span class="sxs-lookup"><span data-stu-id="a7859-166">Click the "Add Todo List" button.</span></span> <span data-ttu-id="a7859-167">前面的列表左侧将显示新列表。</span><span class="sxs-lookup"><span data-stu-id="a7859-167">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="a7859-168">播放使用触发其所需的 TodoList 标题和长度验证。</span><span class="sxs-lookup"><span data-stu-id="a7859-168">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="a7859-169">单击在标题文本框中，若要清除的错误消息。</span><span class="sxs-lookup"><span data-stu-id="a7859-169">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="a7859-170">单击要删除任务列表和其 todos 右上角圆圈，圆圈中的"x"。</span><span class="sxs-lookup"><span data-stu-id="a7859-170">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>

<span data-ttu-id="a7859-171">验证逻辑是通过轻松执行的客户端。</span><span class="sxs-lookup"><span data-stu-id="a7859-171">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="a7859-172">在的服务器模型类验证特性是传播到客户端，并且自动执行之前客户端与服务器联系。</span><span class="sxs-lookup"><span data-stu-id="a7859-172">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="a7859-173">查看网络流量。</span><span class="sxs-lookup"><span data-stu-id="a7859-173">Review the network traffic.</span></span> <span data-ttu-id="a7859-174">请注意轻松检测到错误时的已连接到服务器的任何调用。</span><span class="sxs-lookup"><span data-stu-id="a7859-174">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="a7859-175">每个有效的更改导致 POST 请求为"/ api/Todo/SaveChanges"。</span><span class="sxs-lookup"><span data-stu-id="a7859-175">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="a7859-176">轻松将打包所做的更改并将其发送在一起以单个请求到 Web API 控制器`SaveChanges`方法。</span><span class="sxs-lookup"><span data-stu-id="a7859-176">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="a7859-177">这是不同于 KockoutJS SPA 模板，这使得 PUT、 POST 和单独删除每个项的请求。</span><span class="sxs-lookup"><span data-stu-id="a7859-177">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="a7859-178">在查看</span><span class="sxs-lookup"><span data-stu-id="a7859-178">Peek inside</span></span>

<span data-ttu-id="a7859-179">此应用程序具有客户端和服务器端。</span><span class="sxs-lookup"><span data-stu-id="a7859-179">This application has a client side and a server side.</span></span> <span data-ttu-id="a7859-180">客户端堆栈组成少量 HTML 和应用程序 JavaScript 模块 （在"应用"文件夹中） 的组合以及第三方 JavaScript 库 （在"脚本"文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="a7859-180">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

<span data-ttu-id="a7859-181">如果你已调查 KnockoutJS SPA 模板，这应该非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="a7859-181">If you've investigated the KnockoutJS SPA template, this should look very familiar.</span></span> <span data-ttu-id="a7859-182">专注于蓝色框。</span><span class="sxs-lookup"><span data-stu-id="a7859-182">Focus on the blue boxes.</span></span> <span data-ttu-id="a7859-183">UI 体系结构是模型-视图-视图模型 (MVVM)，在该视图的 HTML 小组件完全分隔从视图模型中支持的演示文稿代码。</span><span class="sxs-lookup"><span data-stu-id="a7859-183">The UI architecture is Model-View-ViewModel (MVVM), in which the HTML widgets of the view are cleanly separated from the supporting presentation code in the view-model.</span></span> <span data-ttu-id="a7859-184">数据绑定系统 (在此情况下 Knockout) 协调的视图和视图模型，以便每个可以完成其他直接不知情的情况下操作。</span><span class="sxs-lookup"><span data-stu-id="a7859-184">A data binding system (Knockout in this case) coordinates the view and view-model so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="a7859-185">模型封装 Todo 数据。</span><span class="sxs-lookup"><span data-stu-id="a7859-185">The model encapsulates the Todo data.</span></span> <span data-ttu-id="a7859-186">模型中的实体构造通过轻松使用 Knockout 可观察属性，以便它们可以直接绑定到视图中的小组件。</span><span class="sxs-lookup"><span data-stu-id="a7859-186">Entities in the model are constructed by Breeze with Knockout observable properties, so they can be bound directly to widgets in the view.</span></span> <span data-ttu-id="a7859-187">视图模型要求数据上下文，以获取并保存模型实体。</span><span class="sxs-lookup"><span data-stu-id="a7859-187">The view-model asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="a7859-188">数据上下文委托的大部分到轻松工作。</span><span class="sxs-lookup"><span data-stu-id="a7859-188">The data context delegates most of the work to Breeze.</span></span>

<span data-ttu-id="a7859-189">一些开发人员代码和三个原则.NET 库的服务器端堆栈组成： Web API、 实体框架和 Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="a7859-189">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="a7859-190">KockoutJS SPA 模板相同的基本体系结构。</span><span class="sxs-lookup"><span data-stu-id="a7859-190">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="a7859-191">但是，实现是要简单得多： Dto 已删除，并且大部分的实体框架的详细信息已委派给 Breeze.NET。</span><span class="sxs-lookup"><span data-stu-id="a7859-191">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7859-192">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a7859-192">Next Steps</span></span>

<span data-ttu-id="a7859-193">我们建议你浏览代码中，由指导[全面讨论](http://www.breezejs.com/spa-template?utm_source=ms-spa)的客户端和服务器堆栈轻松网站上的。</span><span class="sxs-lookup"><span data-stu-id="a7859-193">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="a7859-194">你可以尝试 playing with 轻松客户端查询; 使用添加某些筛选器和排序。</span><span class="sxs-lookup"><span data-stu-id="a7859-194">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="a7859-195">你可以添加更多的模型属性和多个实体来更好地感受用于端到端 SPA 开发。</span><span class="sxs-lookup"><span data-stu-id="a7859-195">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="a7859-196">当你确信的设计时，你可以拉出 Todo 功能并将它们替换为你自己。</span><span class="sxs-lookup"><span data-stu-id="a7859-196">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="a7859-197">很快你将准备就绪供下一大步： 添加客户端屏幕和它们之间导航。</span><span class="sxs-lookup"><span data-stu-id="a7859-197">Soon you'll be ready for the next big step: Adding client-side screens and navigating among them.</span></span> <span data-ttu-id="a7859-198">将留下此 SPA 模板并转向更完整的 SPA 堆栈，如[John 爸爸热毛巾](https://github.com/johnpapa/HotTowel#readme "热毛巾")，从而将 Durandal 添加到轻松和 Knockout 组合。</span><span class="sxs-lookup"><span data-stu-id="a7859-198">You'll leave this SPA template behind and turn to a more complete SPA stack, such as [John Papa's Hot Towel](https://github.com/johnpapa/HotTowel#readme "Hot Towel"), which adds Durandal to the Breeze and Knockout mix.</span></span>
