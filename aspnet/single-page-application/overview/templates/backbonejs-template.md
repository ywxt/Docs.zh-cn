---
uid: single-page-application/overview/templates/backbonejs-template
title: Backbone 模板 |Microsoft Docs
author: madskristensen
description: Backbone.js SPA 模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/04/2013
ms.topic: article
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 641e149155fbee2655024bec3b76dce5243e7d59
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362500"
---
<a name="backbone-template"></a><span data-ttu-id="4731d-103">Backbone 模板</span><span class="sxs-lookup"><span data-stu-id="4731d-103">Backbone Template</span></span>
====================
<span data-ttu-id="4731d-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="4731d-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="4731d-105">是由 Kazi Manzur Rashid 编写的主干 SPA 模板</span><span class="sxs-lookup"><span data-stu-id="4731d-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="4731d-106">下载 Backbone.js SPA 模板</span><span class="sxs-lookup"><span data-stu-id="4731d-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)


<span data-ttu-id="4731d-107">Backbone.js SPA 模板旨在帮助你开始快速构建交互式客户端的 web 应用使用[Backbone.js。](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="4731d-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="4731d-108">该模板用于开发 ASP.NET MVC 中的 Backbone.js 应用程序提供初始的主干。</span><span class="sxs-lookup"><span data-stu-id="4731d-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="4731d-109">在初始状态下，它提供基本的用户登录功能，包括用户注册、 登录、 密码重置，并使用基本电子邮件模板的用户确认。</span><span class="sxs-lookup"><span data-stu-id="4731d-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="4731d-110">要求：</span><span class="sxs-lookup"><span data-stu-id="4731d-110">Requirements:</span></span>

- [<span data-ttu-id="4731d-111">ASP.NET 和 Web Tools 2012.2 更新</span><span class="sxs-lookup"><span data-stu-id="4731d-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="4731d-112">创建一个主干模板项目</span><span class="sxs-lookup"><span data-stu-id="4731d-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="4731d-113">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="4731d-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="4731d-114">该模板打包为 Visual Studio 扩展 (VSIX) 文件。</span><span class="sxs-lookup"><span data-stu-id="4731d-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="4731d-115">您可能需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4731d-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="4731d-116">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="4731d-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="4731d-117">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="4731d-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="4731d-118">在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="4731d-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="4731d-119">命名项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="4731d-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="4731d-120">在中**新的项目**向导，选择 Backbone.js SPA 项目。</span><span class="sxs-lookup"><span data-stu-id="4731d-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="4731d-121">按 Ctrl-F5 生成并运行应用程序而不进行调试，或按 f5 边运行边调试。</span><span class="sxs-lookup"><span data-stu-id="4731d-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="4731d-122">单击"我的帐户"将显示登录页：</span><span class="sxs-lookup"><span data-stu-id="4731d-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="4731d-123">演练： 客户端代码</span><span class="sxs-lookup"><span data-stu-id="4731d-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="4731d-124">让我们开始在客户端。</span><span class="sxs-lookup"><span data-stu-id="4731d-124">Let's starts with the client side.</span></span> <span data-ttu-id="4731d-125">客户端应用程序脚本位于 ~/Scripts/application 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4731d-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="4731d-126">编写的应用程序[TypeScript](http://www.typescriptlang.org/) （.ts 文件） 进行编译为 JavaScript （.js 文件）。</span><span class="sxs-lookup"><span data-stu-id="4731d-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="4731d-127">**应用程序**</span><span class="sxs-lookup"><span data-stu-id="4731d-127">**Application**</span></span>

<span data-ttu-id="4731d-128">`Application` application.ts 中定义。</span><span class="sxs-lookup"><span data-stu-id="4731d-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="4731d-129">此对象初始化应用程序，并且可作为根命名空间。</span><span class="sxs-lookup"><span data-stu-id="4731d-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="4731d-130">例如，用户已登录，它维护在该应用程序之间共享的配置和状态信息。</span><span class="sxs-lookup"><span data-stu-id="4731d-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="4731d-131">`application.start`方法创建模式的视图，并将附加事件处理程序应用程序级事件，例如用户登录。</span><span class="sxs-lookup"><span data-stu-id="4731d-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="4731d-132">接下来，它将创建默认路由器，并检查是否指定了任何客户端的 URL。</span><span class="sxs-lookup"><span data-stu-id="4731d-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="4731d-133">如果不是，它将重定向到默认 url (# ！ /)。</span><span class="sxs-lookup"><span data-stu-id="4731d-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="4731d-134">**事件**</span><span class="sxs-lookup"><span data-stu-id="4731d-134">**Events**</span></span>

<span data-ttu-id="4731d-135">当开发松散耦合组件时，事件始终是非常重要。</span><span class="sxs-lookup"><span data-stu-id="4731d-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="4731d-136">通常，应用程序以响应用户操作执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="4731d-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="4731d-137">主干提供内置事件与组件，如模型、 集合和视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="4731d-138">而不是创建这些组件间的相互依赖关系，该模板使用"发布/订阅"模式： `events` events.ts 中, 定义的对象充当用于发布和订阅的应用程序事件的事件中心。</span><span class="sxs-lookup"><span data-stu-id="4731d-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="4731d-139">`events`对象是单一实例。</span><span class="sxs-lookup"><span data-stu-id="4731d-139">The `events` object is a singleton.</span></span> <span data-ttu-id="4731d-140">下面的代码演示如何订阅事件，然后触发该事件：</span><span class="sxs-lookup"><span data-stu-id="4731d-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="4731d-141">**路由器**</span><span class="sxs-lookup"><span data-stu-id="4731d-141">**Router**</span></span>

<span data-ttu-id="4731d-142">在 Backbone.js，路由器提供路由客户端的页面并将其连接到操作和事件的方法。</span><span class="sxs-lookup"><span data-stu-id="4731d-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="4731d-143">该模板定义中 router.ts 单一路由器。</span><span class="sxs-lookup"><span data-stu-id="4731d-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="4731d-144">路由器创建 activable 视图，并切换视图时维护状态。</span><span class="sxs-lookup"><span data-stu-id="4731d-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="4731d-145">（下一节描述了 activable 视图）。最初，该项目包含两个虚拟视图，家庭和有关。</span><span class="sxs-lookup"><span data-stu-id="4731d-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="4731d-146">它还具有找不到视图，如果不知道路由，则显示。</span><span class="sxs-lookup"><span data-stu-id="4731d-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="4731d-147">**视图**</span><span class="sxs-lookup"><span data-stu-id="4731d-147">**Views**</span></span>

<span data-ttu-id="4731d-148">~/Scripts/application/视图中定义这些视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="4731d-149">有两种类型的视图、 activable 视图和模式对话框视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="4731d-150">由路由器调用 activable 视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="4731d-151">Activable 视图显示时，所有其他 activable 视图变为非活动状态。</span><span class="sxs-lookup"><span data-stu-id="4731d-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="4731d-152">若要创建 activable 视图，扩展视图提供`Activable`对象：</span><span class="sxs-lookup"><span data-stu-id="4731d-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="4731d-153">使用扩展`Activable`将两个新方法添加到视图中，`activate`和`deactivate`。</span><span class="sxs-lookup"><span data-stu-id="4731d-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="4731d-154">路由器调用这些方法来激活和停用仍视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="4731d-155">作为实现模式视图[Twitter Bootstrap](http://twitter.github.com/bootstrap/)模式对话框。</span><span class="sxs-lookup"><span data-stu-id="4731d-155">Modal views are implemented as [Twitter Bootstrap](http://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="4731d-156">`Membership`和`Profile`视图是模式视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="4731d-157">模型视图可由任何应用程序事件调用。</span><span class="sxs-lookup"><span data-stu-id="4731d-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="4731d-158">例如，在`Navigation`视图中，单击"我的帐户"链接显示任一`Membership`视图或`Profile`视图中的，具体取决于用户已登录。</span><span class="sxs-lookup"><span data-stu-id="4731d-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="4731d-159">`Navigation`附加 click 事件处理程序的具有任何子元素`data-command`属性。</span><span class="sxs-lookup"><span data-stu-id="4731d-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="4731d-160">以下是 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="4731d-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="4731d-161">此处是 navigation.ts 要挂钩到事件中的代码：</span><span class="sxs-lookup"><span data-stu-id="4731d-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="4731d-162">**模型**</span><span class="sxs-lookup"><span data-stu-id="4731d-162">**Models**</span></span>

<span data-ttu-id="4731d-163">模型 ~/Scripts/application/模型中进行定义。</span><span class="sxs-lookup"><span data-stu-id="4731d-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="4731d-164">所有模型都具有三个基本操作： 默认属性、 验证规则和服务器端的终结点。</span><span class="sxs-lookup"><span data-stu-id="4731d-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="4731d-165">下面是一个典型示例：</span><span class="sxs-lookup"><span data-stu-id="4731d-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="4731d-166">**插件**</span><span class="sxs-lookup"><span data-stu-id="4731d-166">**Plug-ins**</span></span>

<span data-ttu-id="4731d-167">~/Scripts/application/lib 文件夹包含一些便利的 jQuery 插件。Form.ts 文件定义的插件使用窗体数据。</span><span class="sxs-lookup"><span data-stu-id="4731d-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="4731d-168">通常，您需要进行序列化或反序列化窗体数据和显示的任何模型验证错误。</span><span class="sxs-lookup"><span data-stu-id="4731d-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="4731d-169">插件 form.ts 有方法，如`serializeFields`， `deserializeFields`，和`showFieldErrors`。</span><span class="sxs-lookup"><span data-stu-id="4731d-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="4731d-170">下面的示例演示如何序列化模型的窗体。</span><span class="sxs-lookup"><span data-stu-id="4731d-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="4731d-171">插件 flashbar.ts 分配给用户的各种类型的反馈消息。</span><span class="sxs-lookup"><span data-stu-id="4731d-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="4731d-172">方法是`$.showSuccessbar`，`$.showErrorbar`和`$.showInfobar`。</span><span class="sxs-lookup"><span data-stu-id="4731d-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="4731d-173">在后台，它使用 Twitter Bootstrap 警报显示可以很好地经过动画处理的消息。</span><span class="sxs-lookup"><span data-stu-id="4731d-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="4731d-174">插件 confirm.ts 替换浏览器的确认对话框中，尽管该 API 是略有不同：</span><span class="sxs-lookup"><span data-stu-id="4731d-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="4731d-175">演练： 服务器代码</span><span class="sxs-lookup"><span data-stu-id="4731d-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="4731d-176">现在让我们看一下在服务器端。</span><span class="sxs-lookup"><span data-stu-id="4731d-176">Now let's look at the server side.</span></span>

<span data-ttu-id="4731d-177">**控制器**</span><span class="sxs-lookup"><span data-stu-id="4731d-177">**Controllers**</span></span>

<span data-ttu-id="4731d-178">在单页面应用程序中，服务器播放用户界面中只有很小的作用。</span><span class="sxs-lookup"><span data-stu-id="4731d-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="4731d-179">通常情况下，服务器将呈现的初始页面，然后发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="4731d-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="4731d-180">该模板具有两个 MVC 控制器：`HomeController`呈现的初始页，并`SupportsController`用于确认新的用户帐户和重置密码。</span><span class="sxs-lookup"><span data-stu-id="4731d-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="4731d-181">在模板中的所有其他控制器是 ASP.NET Web API 控制器，发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="4731d-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="4731d-182">默认情况下，控制器都使用新`WebSecurity`类来执行与用户相关的任务。</span><span class="sxs-lookup"><span data-stu-id="4731d-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="4731d-183">但是，它们还具有可选的构造函数，让你将传递委托中对这些任务。</span><span class="sxs-lookup"><span data-stu-id="4731d-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="4731d-184">这简化了测试，并让您替换`WebSecurity`与其他事情，请使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="4731d-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="4731d-185">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="4731d-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="4731d-186">视图</span><span class="sxs-lookup"><span data-stu-id="4731d-186">Views</span></span>

<span data-ttu-id="4731d-187">设计视图为模块化： 页面的每个部分都有自己专用的视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="4731d-188">单页面应用程序中很常见包括不具有任何相应的控制器的视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="4731d-189">可以通过调用包括一个视图`@Html.Partial('myView')`，但是这会变得枯燥乏味。</span><span class="sxs-lookup"><span data-stu-id="4731d-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="4731d-190">若要简化此过程，该模板定义一个帮助器方法， `IncludeClientViews`，呈现的所有指定的文件夹视图：</span><span class="sxs-lookup"><span data-stu-id="4731d-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="4731d-191">如果未指定文件夹名称，默认文件夹名称是"ClientViews"。</span><span class="sxs-lookup"><span data-stu-id="4731d-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="4731d-192">如果客户端视图也使用分部视图，名称以下划线字符的分部视图 (例如， `_SignUp`)。</span><span class="sxs-lookup"><span data-stu-id="4731d-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="4731d-193">`IncludeClientViews`方法不包括其名称以下划线开头的任何视图。</span><span class="sxs-lookup"><span data-stu-id="4731d-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="4731d-194">若要包括在客户端视图的分部视图，请调用`Html.ClientView('SignUp')`而不是`Html.Partial('_SignUp')`。</span><span class="sxs-lookup"><span data-stu-id="4731d-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="4731d-195">**发送电子邮件**</span><span class="sxs-lookup"><span data-stu-id="4731d-195">**Sending Email**</span></span>

<span data-ttu-id="4731d-196">若要发送电子邮件，该模板，请使用[邮政](http://aboutcode.net/postal)。</span><span class="sxs-lookup"><span data-stu-id="4731d-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="4731d-197">邮政抽象的与代码的其余部分，但是，`IMailer`接口，所以您可以轻松地将其替换为另一个实现。</span><span class="sxs-lookup"><span data-stu-id="4731d-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="4731d-198">电子邮件模板位于视图/电子邮件文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4731d-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="4731d-199">发件人的电子邮件地址中，在 web.config 文件中，指定`sender.email`的关键**appSettings**部分。</span><span class="sxs-lookup"><span data-stu-id="4731d-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="4731d-200">此外，当`debug="true"`在 web.config 中，应用程序不需要用户电子邮件确认可加速开发。</span><span class="sxs-lookup"><span data-stu-id="4731d-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="4731d-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="4731d-201">GitHub</span></span>

<span data-ttu-id="4731d-202">您还可以在找到 Backbone.js SPA 模板[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)。</span><span class="sxs-lookup"><span data-stu-id="4731d-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
