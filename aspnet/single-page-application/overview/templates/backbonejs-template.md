---
uid: single-page-application/overview/templates/backbonejs-template
title: Backbone 模板 |Microsoft 文档
author: madskristensen
description: Backbone.js SPA 模板
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/04/2013
ms.topic: article
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 3b8eabd3cefcb96dc40bbf6cc6e3ee81accb0d7c
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26506676"
---
<a name="backbone-template"></a><span data-ttu-id="5ff15-103">Backbone 模板</span><span class="sxs-lookup"><span data-stu-id="5ff15-103">Backbone Template</span></span>
====================
<span data-ttu-id="5ff15-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="5ff15-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="5ff15-105">Backbone SPA 模板已写入 Kazi Manzur 发展的见解</span><span class="sxs-lookup"><span data-stu-id="5ff15-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="5ff15-106">下载 Backbone.js SPA 模板</span><span class="sxs-lookup"><span data-stu-id="5ff15-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)


<span data-ttu-id="5ff15-107">Backbone.js SPA 模板旨在帮助你入门快速构建客户端的交互式 web 应用程序使用[Backbone.js。](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="5ff15-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="5ff15-108">模板提供用于开发 Backbone.js ASP.NET mvc 应用程序的初始主干。</span><span class="sxs-lookup"><span data-stu-id="5ff15-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="5ff15-109">在初始状态下，它提供基本的用户登录功能，包括用户注册、 登录，密码重置，以及使用基本的电子邮件模板的用户确认。</span><span class="sxs-lookup"><span data-stu-id="5ff15-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="5ff15-110">要求：</span><span class="sxs-lookup"><span data-stu-id="5ff15-110">Requirements:</span></span>

- [<span data-ttu-id="5ff15-111">ASP.NET 和 Web Tools 2012.2 的更新</span><span class="sxs-lookup"><span data-stu-id="5ff15-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="5ff15-112">创建一个主干模板项目</span><span class="sxs-lookup"><span data-stu-id="5ff15-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="5ff15-113">下载并安装该模板通过单击上面的下载按钮。</span><span class="sxs-lookup"><span data-stu-id="5ff15-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="5ff15-114">模板被打包为 Visual Studio 扩展 (VSIX) 文件。</span><span class="sxs-lookup"><span data-stu-id="5ff15-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="5ff15-115">你可能需要重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5ff15-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="5ff15-116">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="5ff15-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="5ff15-117">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="5ff15-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="5ff15-118">在项目模板列表中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="5ff15-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="5ff15-119">命名该项目并单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="5ff15-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="5ff15-120">在**新项目**向导，选择 Backbone.js SPA 项目。</span><span class="sxs-lookup"><span data-stu-id="5ff15-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="5ff15-121">按 Ctrl + F5 生成并运行应用程序而不进行调试，或按 F5 边运行边调试。</span><span class="sxs-lookup"><span data-stu-id="5ff15-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="5ff15-122">单击"我的帐户"将打开登录页：</span><span class="sxs-lookup"><span data-stu-id="5ff15-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="5ff15-123">演练： 客户端代码</span><span class="sxs-lookup"><span data-stu-id="5ff15-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="5ff15-124">让我们开头的客户端。</span><span class="sxs-lookup"><span data-stu-id="5ff15-124">Let's starts with the client side.</span></span> <span data-ttu-id="5ff15-125">客户端应用程序脚本位于 ~/Scripts/application 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5ff15-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="5ff15-126">应用用编写[TypeScript](http://www.typescriptlang.org/) （.ts 文件） 进行编译到 JavaScript （.js 文件）。</span><span class="sxs-lookup"><span data-stu-id="5ff15-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="5ff15-127">**应用程序**</span><span class="sxs-lookup"><span data-stu-id="5ff15-127">**Application**</span></span>

<span data-ttu-id="5ff15-128">`Application` 在 application.ts 中定义。</span><span class="sxs-lookup"><span data-stu-id="5ff15-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="5ff15-129">此对象初始化应用程序，并且可作为根命名空间。</span><span class="sxs-lookup"><span data-stu-id="5ff15-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="5ff15-130">这样可保持在应用程序之间共享的配置和状态信息，如用户已登录。</span><span class="sxs-lookup"><span data-stu-id="5ff15-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="5ff15-131">`application.start`方法创建的模式视图，并将附加应用程序级事件，例如用户登录事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5ff15-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="5ff15-132">接下来，它创建的默认路由器，并检查是否指定任何客户端的 URL。</span><span class="sxs-lookup"><span data-stu-id="5ff15-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="5ff15-133">如果不是，它将重定向到默认 url (# ！ /)。</span><span class="sxs-lookup"><span data-stu-id="5ff15-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="5ff15-134">**事件**</span><span class="sxs-lookup"><span data-stu-id="5ff15-134">**Events**</span></span>

<span data-ttu-id="5ff15-135">当开发松散耦合的组件时，事件始终是非常重要。</span><span class="sxs-lookup"><span data-stu-id="5ff15-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="5ff15-136">应用程序通常可以执行多个操作以响应用户操作。</span><span class="sxs-lookup"><span data-stu-id="5ff15-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="5ff15-137">Backbone 提供内置的事件的组件，如模型、 集合和视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="5ff15-138">该模板而不是创建这些组件间的相互依赖性，使用"发布/订阅"模型： `events` events.ts，在定义的对象充当用于发布和订阅应用程序事件的事件中心。</span><span class="sxs-lookup"><span data-stu-id="5ff15-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="5ff15-139">`events`对象是单一实例。</span><span class="sxs-lookup"><span data-stu-id="5ff15-139">The `events` object is a singleton.</span></span> <span data-ttu-id="5ff15-140">下面的代码演示如何订阅事件，然后触发该事件：</span><span class="sxs-lookup"><span data-stu-id="5ff15-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="5ff15-141">**路由器**</span><span class="sxs-lookup"><span data-stu-id="5ff15-141">**Router**</span></span>

<span data-ttu-id="5ff15-142">在 Backbone.js，路由器提供方法以路由客户端页，并将它们连接到操作和事件。</span><span class="sxs-lookup"><span data-stu-id="5ff15-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="5ff15-143">模板定义中 router.ts 单一路由器。</span><span class="sxs-lookup"><span data-stu-id="5ff15-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="5ff15-144">路由器创建 activable 视图，并切换视图时维护的状态。</span><span class="sxs-lookup"><span data-stu-id="5ff15-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="5ff15-145">（activable 视图所述的下一节。）最初，该项目包含两个 dummy 视图，家庭和有关。</span><span class="sxs-lookup"><span data-stu-id="5ff15-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="5ff15-146">它还具有未找到视图，如果不知道路由才会显示。</span><span class="sxs-lookup"><span data-stu-id="5ff15-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="5ff15-147">**视图**</span><span class="sxs-lookup"><span data-stu-id="5ff15-147">**Views**</span></span>

<span data-ttu-id="5ff15-148">视图定义中 ~/Scripts/application/视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="5ff15-149">有两种类型的视图、 activable 视图和模式对话框视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="5ff15-150">Activable 视图都是通过路由器调用的。</span><span class="sxs-lookup"><span data-stu-id="5ff15-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="5ff15-151">当显示 activable 视图时，所有其他 activable 视图将变为不活动状态。</span><span class="sxs-lookup"><span data-stu-id="5ff15-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="5ff15-152">若要创建 activable 视图，请扩展与视图`Activable`对象：</span><span class="sxs-lookup"><span data-stu-id="5ff15-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="5ff15-153">使用扩展`Activable`将两个新方法添加到视图中，`activate`和`deactivate`。</span><span class="sxs-lookup"><span data-stu-id="5ff15-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="5ff15-154">路由器调用这些方法来激活和停用仍视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="5ff15-155">作为实现的模式视图[Twitter Bootstrap](http://twitter.github.com/bootstrap/)模式对话框。</span><span class="sxs-lookup"><span data-stu-id="5ff15-155">Modal views are implemented as [Twitter Bootstrap](http://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="5ff15-156">`Membership`和`Profile`视图是模式的视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="5ff15-157">可以通过任何应用程序事件中调用模型视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="5ff15-158">例如，在`Navigation`视图中，单击"我的帐户"链接显示任一`Membership`视图或`Profile`视图中的，具体取决于用户已登录。</span><span class="sxs-lookup"><span data-stu-id="5ff15-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="5ff15-159">`Navigation`附加单击事件处理程序与具有任何子元素`data-command`属性。</span><span class="sxs-lookup"><span data-stu-id="5ff15-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="5ff15-160">下面是 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="5ff15-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="5ff15-161">以下是 navigation.ts 要挂钩到事件中的代码：</span><span class="sxs-lookup"><span data-stu-id="5ff15-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="5ff15-162">**模型**</span><span class="sxs-lookup"><span data-stu-id="5ff15-162">**Models**</span></span>

<span data-ttu-id="5ff15-163">模型进行 ~/Scripts/application/模型中定义。</span><span class="sxs-lookup"><span data-stu-id="5ff15-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="5ff15-164">所有模型都具有三个基本操作： 默认属性、 验证规则和服务器端终结点。</span><span class="sxs-lookup"><span data-stu-id="5ff15-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="5ff15-165">下面是一个典型的示例：</span><span class="sxs-lookup"><span data-stu-id="5ff15-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="5ff15-166">**插件**</span><span class="sxs-lookup"><span data-stu-id="5ff15-166">**Plug-ins**</span></span>

<span data-ttu-id="5ff15-167">~/Scripts/application/lib 文件夹包含几个方便 jQuery 插件。Form.ts 文件定义插件用于使用窗体数据。</span><span class="sxs-lookup"><span data-stu-id="5ff15-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="5ff15-168">通常，你需要序列化或反序列化的表单数据并显示任何模型验证错误。</span><span class="sxs-lookup"><span data-stu-id="5ff15-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="5ff15-169">插件 form.ts 有方法，如`serializeFields`， `deserializeFields`，和`showFieldErrors`。</span><span class="sxs-lookup"><span data-stu-id="5ff15-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="5ff15-170">下面的示例演示如何序列化到模型的窗体。</span><span class="sxs-lookup"><span data-stu-id="5ff15-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="5ff15-171">插件 flashbar.ts 向用户提供的各种类型的反馈消息。</span><span class="sxs-lookup"><span data-stu-id="5ff15-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="5ff15-172">方法都是`$.showSuccessbar`，`$.showErrorbar`和`$.showInfobar`。</span><span class="sxs-lookup"><span data-stu-id="5ff15-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="5ff15-173">在后台，它将使用 Twitter Bootstrap 警报以显示可以很好地经过动画处理的消息。</span><span class="sxs-lookup"><span data-stu-id="5ff15-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="5ff15-174">插件 confirm.ts 替换浏览器的确认对话框中，虽然 API 是稍有不同：</span><span class="sxs-lookup"><span data-stu-id="5ff15-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="5ff15-175">演练： 服务器代码</span><span class="sxs-lookup"><span data-stu-id="5ff15-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="5ff15-176">现在让我们看一下服务器端。</span><span class="sxs-lookup"><span data-stu-id="5ff15-176">Now let's look at the server side.</span></span>

<span data-ttu-id="5ff15-177">**控制器**</span><span class="sxs-lookup"><span data-stu-id="5ff15-177">**Controllers**</span></span>

<span data-ttu-id="5ff15-178">在单页面应用程序中，服务器扮演仅在用户界面很小的作用。</span><span class="sxs-lookup"><span data-stu-id="5ff15-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="5ff15-179">通常情况下，服务器将呈现的初始页以及然后发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="5ff15-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="5ff15-180">该模板具有两个 MVC 控制器：`HomeController`呈现的初始页，和`SupportsController`用于确认新的用户帐户和重置密码。</span><span class="sxs-lookup"><span data-stu-id="5ff15-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="5ff15-181">在模板中的所有其他控制器都是 ASP.NET Web API 控制器，发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="5ff15-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="5ff15-182">默认情况下，控制器使用新`WebSecurity`类来执行与用户相关的任务。</span><span class="sxs-lookup"><span data-stu-id="5ff15-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="5ff15-183">但是，它们还具有可选，可以将其在委托中传递这些任务的构造函数。</span><span class="sxs-lookup"><span data-stu-id="5ff15-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="5ff15-184">这使测试更加轻松，并让您替换`WebSecurity`替换为其他的情况下，使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="5ff15-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="5ff15-185">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="5ff15-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="5ff15-186">视图</span><span class="sxs-lookup"><span data-stu-id="5ff15-186">Views</span></span>

<span data-ttu-id="5ff15-187">设计视图为模块化： 页面的每个部分都有自己专用的视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="5ff15-188">在单页面应用程序中，很普遍包括不具有任何相应的控制器的视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="5ff15-189">你可以通过调用包括视图`@Html.Partial('myView')`，但这将得到需要很长时间。</span><span class="sxs-lookup"><span data-stu-id="5ff15-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="5ff15-190">若要简化此过程，该模板定义了一个帮助器方法， `IncludeClientViews`，呈现所有指定的文件夹中的视图：</span><span class="sxs-lookup"><span data-stu-id="5ff15-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="5ff15-191">如果未指定文件夹名称，默认文件夹名称是"ClientViews"。</span><span class="sxs-lookup"><span data-stu-id="5ff15-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="5ff15-192">如果你的客户端视图还使用分部视图，名称以下划线字符分部视图 (例如， `_SignUp`)。</span><span class="sxs-lookup"><span data-stu-id="5ff15-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="5ff15-193">`IncludeClientViews`方法排除名称以下划线开头的任何视图。</span><span class="sxs-lookup"><span data-stu-id="5ff15-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="5ff15-194">若要在客户端视图中包含了分部视图，调用`Html.ClientView('SignUp')`而不是`Html.Partial('_SignUp')`。</span><span class="sxs-lookup"><span data-stu-id="5ff15-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="5ff15-195">**发送电子邮件**</span><span class="sxs-lookup"><span data-stu-id="5ff15-195">**Sending Email**</span></span>

<span data-ttu-id="5ff15-196">若要发送电子邮件，该模板使用[邮递](http://aboutcode.net/postal)。</span><span class="sxs-lookup"><span data-stu-id="5ff15-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="5ff15-197">但是，从与代码的其余部分提取邮递`IMailer`接口，所以可以轻松地将其替换另一个实现。</span><span class="sxs-lookup"><span data-stu-id="5ff15-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="5ff15-198">电子邮件模板位于视图/电子邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="5ff15-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="5ff15-199">发件人的电子邮件地址中，在 web.config 文件中，指定`sender.email`键**appSettings**部分。</span><span class="sxs-lookup"><span data-stu-id="5ff15-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="5ff15-200">此外，当`debug="true"`在 web.config 中，应用程序不需要用户电子邮件确认，以加速开发。</span><span class="sxs-lookup"><span data-stu-id="5ff15-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="5ff15-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="5ff15-201">GitHub</span></span>

<span data-ttu-id="5ff15-202">你还可以上查找 Backbone.js SPA 模板[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)。</span><span class="sxs-lookup"><span data-stu-id="5ff15-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
