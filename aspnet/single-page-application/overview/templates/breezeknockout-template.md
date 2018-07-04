---
uid: single-page-application/overview/templates/breezeknockout-template
title: Breeze/Knockout 模版 |Microsoft Docs
author: madskristensen
description: Breeze/Knockout 单页面应用程序模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 48ee0463fe950c28832523986a2242417411c96a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376859"
---
<a name="breezeknockout-template"></a><span data-ttu-id="f39fd-103">Breeze/Knockout 模版</span><span class="sxs-lookup"><span data-stu-id="f39fd-103">Breeze/Knockout template</span></span>
====================
<span data-ttu-id="f39fd-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="f39fd-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="f39fd-105">Breeze/Knockout MVC 模板是编写的 Ward Bell</span><span class="sxs-lookup"><span data-stu-id="f39fd-105">The Breeze/Knockout MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="f39fd-106">下载 Breeze/Knockout MVC 模板</span><span class="sxs-lookup"><span data-stu-id="f39fd-106">Download the Breeze/Knockout MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282649)


<span data-ttu-id="f39fd-107">您听说过"单页面应用程序"(SPA) 并想知道它是什么。</span><span class="sxs-lookup"><span data-stu-id="f39fd-107">You've heard of "single page application" (SPA) and wondered what it is.</span></span> <span data-ttu-id="f39fd-108">虽然无法了解它，而不是与它自己。</span><span class="sxs-lookup"><span data-stu-id="f39fd-108">While you could read about it, you'd rather experience it for yourself.</span></span> <span data-ttu-id="f39fd-109">但谁还有时间来下载示例？</span><span class="sxs-lookup"><span data-stu-id="f39fd-109">But who has time to download a sample?</span></span> <span data-ttu-id="f39fd-110">如果您有 Visual Studio，将包含最多的示例 SPA 和 ASP.NET mvc 4"Breeze/Knockout 单页面应用程序"模板运行在不会早于 60 秒。</span><span class="sxs-lookup"><span data-stu-id="f39fd-110">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds with the ASP.NET MVC 4 "Breeze/Knockout Single Page Application" template.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a><span data-ttu-id="f39fd-111">什么是 Breeze/Knockout SPA 模板？</span><span class="sxs-lookup"><span data-stu-id="f39fd-111">What is the Breeze/Knockout SPA Template?</span></span>

<span data-ttu-id="f39fd-112">大多数项目模板生成应用程序框架。</span><span class="sxs-lookup"><span data-stu-id="f39fd-112">Most project templates generate an application skeleton.</span></span> <span data-ttu-id="f39fd-113">通过添加你的代码置于这些基本加点料和最终交付的工作应用程序。</span><span class="sxs-lookup"><span data-stu-id="f39fd-113">You put flesh on those bones by adding your code and eventually deliver a working application.</span></span> <span data-ttu-id="f39fd-114">Breeze/Knockout SPA 模板是不同的。</span><span class="sxs-lookup"><span data-stu-id="f39fd-114">The Breeze/Knockout SPA template is different.</span></span> <span data-ttu-id="f39fd-115">它会生成示例应用程序，以便研究。</span><span class="sxs-lookup"><span data-stu-id="f39fd-115">It generates a sample application for you to study.</span></span> <span data-ttu-id="f39fd-116">它演示了 SPA 应用程序设计和许多用于构建 SPA 的技术。</span><span class="sxs-lookup"><span data-stu-id="f39fd-116">It demonstrates a SPA application design and many of the techniques for building a SPA.</span></span>

<span data-ttu-id="f39fd-117">Breeze/Knockout 模版上是一种变体[KnockoutJS SPA 模板](../introduction/knockoutjs-template.md)包含在 ASP.NET 和 Web Tools 2012.2 更新。</span><span class="sxs-lookup"><span data-stu-id="f39fd-117">The Breeze/Knockout template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="f39fd-118">Breeze SPA 模板生成具有相同的用户体验的应用程序，但它具有不同的实现，使用数据管理变得轻而易举。</span><span class="sxs-lookup"><span data-stu-id="f39fd-118">The Breeze SPA template generates an application with the same user experience, but it has a different implementation, using Breeze for data management.</span></span>

<span data-ttu-id="f39fd-119">KnockoutJS SPA 模板，可使用原始 jQuery AJAX 中，服务请求足以满足简单的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f39fd-119">The KnockoutJS SPA template makes service requests with raw jQuery AJAX, which is adequate for a simple application.</span></span> <span data-ttu-id="f39fd-120">但更复杂的应用具有满足更加严苛的数据管理要求。</span><span class="sxs-lookup"><span data-stu-id="f39fd-120">But more sophisticated apps have more demanding data management requirements.</span></span> <span data-ttu-id="f39fd-121">例如，大多数应用程序：</span><span class="sxs-lookup"><span data-stu-id="f39fd-121">For example, most applications:</span></span>

- <span data-ttu-id="f39fd-122">查询和扩展的用户会话期间重新查询服务器。</span><span class="sxs-lookup"><span data-stu-id="f39fd-122">Query and re-query the server during an extended user session.</span></span>
- <span data-ttu-id="f39fd-123">添加查询筛选器、 排序和分页。</span><span class="sxs-lookup"><span data-stu-id="f39fd-123">Add query filters, sorting, and paging.</span></span>
- <span data-ttu-id="f39fd-124">在多个屏幕之间共享相同的数据。</span><span class="sxs-lookup"><span data-stu-id="f39fd-124">Share the same data across multiple screens.</span></span>
- <span data-ttu-id="f39fd-125">累积更改向很多对象，然后将其保存为一个事务。</span><span class="sxs-lookup"><span data-stu-id="f39fd-125">Accumulate changes to many objects, then save them as a single transaction.</span></span>
- <span data-ttu-id="f39fd-126">验证在客户端上的更改，因此，用户可以将更改提交到数据库之前更正错误。</span><span class="sxs-lookup"><span data-stu-id="f39fd-126">Validate changes on the client, so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="f39fd-127">BreezeJS 库处理这些繁琐的事务，使你能开发最重要的应用程序逻辑和用户体验。</span><span class="sxs-lookup"><span data-stu-id="f39fd-127">The BreezeJS library handles these chores for you, freeing you to develop the application logic and user experience that matter most.</span></span>

<span data-ttu-id="f39fd-128">[**Breeze** ](http://www.breezejs.com/?utm_source=ms-spa)是用于构建丰富的数据应用程序中 JavaScript 和 HTML 的以前已作为独立桌面应用程序传递的应用类型的开放源代码库。</span><span class="sxs-lookup"><span data-stu-id="f39fd-128">[**Breeze**](http://www.breezejs.com/?utm_source=ms-spa) is an open source library for building rich data applications in JavaScript and HTML, the kinds of apps that have historically been delivered as stand-alone desktop applications.</span></span>

<span data-ttu-id="f39fd-129">Breeze/Knockout 模板可帮助你执行向更可靠的数据管理基础结构的第一个关键步骤。</span><span class="sxs-lookup"><span data-stu-id="f39fd-129">The Breeze/Knockout template helps you take that first crucial step toward a more robust data management infrastructure.</span></span> <span data-ttu-id="f39fd-130">它将生成与 KnockoutJS SPA 模板表面上是相同的示例待办事项应用程序。</span><span class="sxs-lookup"><span data-stu-id="f39fd-130">It produces a sample Todo application that is outwardly identical to the KnockoutJS SPA template.</span></span> <span data-ttu-id="f39fd-131">在内部，它替换 Breeze 的 AJAX 数据层，以便可以比较两个方法，通过并行。</span><span class="sxs-lookup"><span data-stu-id="f39fd-131">On the inside, it replaces the AJAX data layer with Breeze, so you can compare the two approaches side-by-side.</span></span> <span data-ttu-id="f39fd-132">当然，它几乎不能涉及到 Breeze 应用程序的可能性。</span><span class="sxs-lookup"><span data-stu-id="f39fd-132">Of course, it barely touches the potential of a Breeze application.</span></span> <span data-ttu-id="f39fd-133">但您会看到 Breeze 的工作原理和如何稍有需要进行这种转换。</span><span class="sxs-lookup"><span data-stu-id="f39fd-133">But you'll see how Breeze works and how little is required to make that transition.</span></span>

<span data-ttu-id="f39fd-134">让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="f39fd-134">Let's get started.</span></span>

## <a name="create-a-breezeknockout-template-project"></a><span data-ttu-id="f39fd-135">创建一个 Breeze/Knockout 模板项目</span><span class="sxs-lookup"><span data-stu-id="f39fd-135">Create a Breeze/Knockout Template Project</span></span>

<span data-ttu-id="f39fd-136">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="f39fd-136">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="f39fd-137">该模板打包为 Visual Studio 扩展 (VSIX) 文件。</span><span class="sxs-lookup"><span data-stu-id="f39fd-137">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="f39fd-138">您可能需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f39fd-138">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="f39fd-139">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="f39fd-139">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="f39fd-140">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="f39fd-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="f39fd-141">在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="f39fd-141">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="f39fd-142">命名项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="f39fd-142">Name the project and click **OK**.</span></span>

<span data-ttu-id="f39fd-143">在中**新的项目**向导中，选择**Breeze Knockout SPA**。</span><span class="sxs-lookup"><span data-stu-id="f39fd-143">In the **New Project** wizard, select **Breeze Knockout SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

<span data-ttu-id="f39fd-144">按 Ctrl-F5 生成并运行应用程序而不进行调试，或按 f5 边运行边调试。</span><span class="sxs-lookup"><span data-stu-id="f39fd-144">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

<span data-ttu-id="f39fd-145">当首次运行该应用程序时，它显示登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="f39fd-145">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="f39fd-146">单击"注册"链接，一个新页面种到视图中，您可以在其中输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="f39fd-146">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="f39fd-147">（登录名和注册页使用构建 ASP.NET MVC。）当您提交注册表单时，服务器会生成 TodoList 以下两个项为您的帐户。</span><span class="sxs-lookup"><span data-stu-id="f39fd-147">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="f39fd-148">其呈现给你在上一个黄色的注释。</span><span class="sxs-lookup"><span data-stu-id="f39fd-148">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="f39fd-149">现在，已在 SPA 土地。</span><span class="sxs-lookup"><span data-stu-id="f39fd-149">Now you are in the land of SPA.</span></span> <span data-ttu-id="f39fd-150">所有内容您看到和体验时操作 Todo 呈现和管理的 Knockout 和 Breeze 帮助客户端上。</span><span class="sxs-lookup"><span data-stu-id="f39fd-150">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="f39fd-151">以用户身份浏览应用程序...</span><span class="sxs-lookup"><span data-stu-id="f39fd-151">Explore the app as a user …</span></span> <span data-ttu-id="f39fd-152">但与开发人员的关注。</span><span class="sxs-lookup"><span data-stu-id="f39fd-152">but with a developer's eye.</span></span> <span data-ttu-id="f39fd-153">在浏览器中使用的开发人员工具来捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="f39fd-153">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="f39fd-154">(在 Internet Explorer： 按 f12 键，选择**网络**选项卡，然后单击**开始捕获**。)现在请尝试以下方法：</span><span class="sxs-lookup"><span data-stu-id="f39fd-154">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="f39fd-155">添加新的 Todo 项。</span><span class="sxs-lookup"><span data-stu-id="f39fd-155">Add a new Todo item.</span></span>
- <span data-ttu-id="f39fd-156">单击标签和编辑 Todo 项标题</span><span class="sxs-lookup"><span data-stu-id="f39fd-156">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="f39fd-157">选中复选框以将标记项已完成。</span><span class="sxs-lookup"><span data-stu-id="f39fd-157">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="f39fd-158">请注意，文本框被禁用，因此是不再可编辑的标题。</span><span class="sxs-lookup"><span data-stu-id="f39fd-158">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="f39fd-159">单击右侧的标签的 x。</span><span class="sxs-lookup"><span data-stu-id="f39fd-159">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="f39fd-160">项目将消失，并从数据库删除。</span><span class="sxs-lookup"><span data-stu-id="f39fd-160">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="f39fd-161">选择另一个项，并清除其标题。</span><span class="sxs-lookup"><span data-stu-id="f39fd-161">Pick another item and clear its title.</span></span> <span data-ttu-id="f39fd-162">您将有标题是必需的验证错误。</span><span class="sxs-lookup"><span data-stu-id="f39fd-162">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="f39fd-163">短暂暂停之后还原上一个标题。</span><span class="sxs-lookup"><span data-stu-id="f39fd-163">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="f39fd-164">键入可笑长标题中。</span><span class="sxs-lookup"><span data-stu-id="f39fd-164">Type in a ridiculously long title.</span></span> <span data-ttu-id="f39fd-165">你将收到不同的验证错误的标题是太长。</span><span class="sxs-lookup"><span data-stu-id="f39fd-165">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="f39fd-166">单击"添加待办事项列表"按钮。</span><span class="sxs-lookup"><span data-stu-id="f39fd-166">Click the "Add Todo List" button.</span></span> <span data-ttu-id="f39fd-167">上一列表的左侧将显示新列表。</span><span class="sxs-lookup"><span data-stu-id="f39fd-167">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="f39fd-168">播放使用触发其所需的 TodoList 标题和长度验证。</span><span class="sxs-lookup"><span data-stu-id="f39fd-168">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="f39fd-169">单击以清除错误消息的标题文本框中。</span><span class="sxs-lookup"><span data-stu-id="f39fd-169">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="f39fd-170">单击右上角以删除任务列表和其 todo 圆圈中的"x"。</span><span class="sxs-lookup"><span data-stu-id="f39fd-170">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>

<span data-ttu-id="f39fd-171">验证逻辑是通过 Breeze 的执行的客户端。</span><span class="sxs-lookup"><span data-stu-id="f39fd-171">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="f39fd-172">服务器模型类上的验证特性是传播到客户端，并自动执行之前客户端与服务器联系。</span><span class="sxs-lookup"><span data-stu-id="f39fd-172">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="f39fd-173">查看网络流量。</span><span class="sxs-lookup"><span data-stu-id="f39fd-173">Review the network traffic.</span></span> <span data-ttu-id="f39fd-174">请注意，Breeze 检测到错误时，已连接到服务器的任何调用。</span><span class="sxs-lookup"><span data-stu-id="f39fd-174">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="f39fd-175">每个有效的更改时为"/ api/Todo/SaveChanges"的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="f39fd-175">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="f39fd-176">Breeze 捆绑包所做的更改并将其发送到一起以单个请求到 Web API 控制器`SaveChanges`方法。</span><span class="sxs-lookup"><span data-stu-id="f39fd-176">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="f39fd-177">这就是不同于 KockoutJS SPA 模板，这使得 PUT、 POST 和 DELETE 分别为每个项的请求。</span><span class="sxs-lookup"><span data-stu-id="f39fd-177">That's different from KockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="f39fd-178">在查看</span><span class="sxs-lookup"><span data-stu-id="f39fd-178">Peek inside</span></span>

<span data-ttu-id="f39fd-179">此应用程序具有一个客户端和服务器端。</span><span class="sxs-lookup"><span data-stu-id="f39fd-179">This application has a client side and a server side.</span></span> <span data-ttu-id="f39fd-180">客户端堆栈组成一个小的 HTML 和应用程序 JavaScript 模块 （在"应用"文件夹中） 的组合以及第三方 JavaScript 库 （在"脚本"文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="f39fd-180">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

<span data-ttu-id="f39fd-181">如果您研究 KnockoutJS SPA 模板，这应该很熟悉。</span><span class="sxs-lookup"><span data-stu-id="f39fd-181">If you've investigated the KnockoutJS SPA template, this should look very familiar.</span></span> <span data-ttu-id="f39fd-182">重点放在蓝色框。</span><span class="sxs-lookup"><span data-stu-id="f39fd-182">Focus on the blue boxes.</span></span> <span data-ttu-id="f39fd-183">UI 体系结构是视图的模型-视图-视图模型 (MVVM)，其中的 HTML 小组件视图的完全分隔从视图模型中支持的演示文稿代码。</span><span class="sxs-lookup"><span data-stu-id="f39fd-183">The UI architecture is Model-View-ViewModel (MVVM), in which the HTML widgets of the view are cleanly separated from the supporting presentation code in the view-model.</span></span> <span data-ttu-id="f39fd-184">数据绑定系统 (Knockout 在此情况下) 协调的视图和视图模型，这样，每个可以执行其作业而无需其他精通。</span><span class="sxs-lookup"><span data-stu-id="f39fd-184">A data binding system (Knockout in this case) coordinates the view and view-model so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="f39fd-185">模型封装 Todo 数据。</span><span class="sxs-lookup"><span data-stu-id="f39fd-185">The model encapsulates the Todo data.</span></span> <span data-ttu-id="f39fd-186">模型中的实体都由构造通过 Breeze Knockout 可观察量属性，以便它们可以直接绑定到视图中的小组件。</span><span class="sxs-lookup"><span data-stu-id="f39fd-186">Entities in the model are constructed by Breeze with Knockout observable properties, so they can be bound directly to widgets in the view.</span></span> <span data-ttu-id="f39fd-187">视图模型要求数据上下文来获取和保存模型实体。</span><span class="sxs-lookup"><span data-stu-id="f39fd-187">The view-model asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="f39fd-188">数据上下文委托的大部分 breeze 工作。</span><span class="sxs-lookup"><span data-stu-id="f39fd-188">The data context delegates most of the work to Breeze.</span></span>

<span data-ttu-id="f39fd-189">一些开发人员代码和三个原则.NET 库的服务器端堆栈组成： Web API、 实体框架和 Breeze.NET:</span><span class="sxs-lookup"><span data-stu-id="f39fd-189">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="f39fd-190">KockoutJS SPA 模板相同的基本体系结构。</span><span class="sxs-lookup"><span data-stu-id="f39fd-190">The basic architecture is the same as the KockoutJS SPA template.</span></span> <span data-ttu-id="f39fd-191">但是，实现是要简单得多： Dto 已删除，并且已到 Breeze.NET 委派大多数实体框架的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f39fd-191">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39fd-192">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f39fd-192">Next Steps</span></span>

<span data-ttu-id="f39fd-193">我们建议您浏览代码，由引导[广泛的讨论](http://www.breezejs.com/spa-template?utm_source=ms-spa)的客户端和服务器堆栈 Breeze 网站上的。</span><span class="sxs-lookup"><span data-stu-id="f39fd-193">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="f39fd-194">您可以尝试播放使用 Breeze 客户端的查询的灵活性。添加一些筛选器和排序。</span><span class="sxs-lookup"><span data-stu-id="f39fd-194">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="f39fd-195">你可以添加多个模型的属性和多个实体以更好地了解端到端 SPA 开发的。</span><span class="sxs-lookup"><span data-stu-id="f39fd-195">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="f39fd-196">当你确信该设计的时你可以断开 Todo 功能并替换为您自己。</span><span class="sxs-lookup"><span data-stu-id="f39fd-196">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="f39fd-197">很快您就可以大的下一步： 添加客户端屏幕并在它们之间导航。</span><span class="sxs-lookup"><span data-stu-id="f39fd-197">Soon you'll be ready for the next big step: Adding client-side screens and navigating among them.</span></span> <span data-ttu-id="f39fd-198">将留下此 SPA 模板和转向更完整的 SPA 堆栈，如[John Papa 热总是随身携带毛巾](https://github.com/johnpapa/HotTowel#readme "热总是随身携带毛巾")，从而将 Durandal 添加到 Breeze 和 Knockout 组合。</span><span class="sxs-lookup"><span data-stu-id="f39fd-198">You'll leave this SPA template behind and turn to a more complete SPA stack, such as [John Papa's Hot Towel](https://github.com/johnpapa/HotTowel#readme "Hot Towel"), which adds Durandal to the Breeze and Knockout mix.</span></span>
