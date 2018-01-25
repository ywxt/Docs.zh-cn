---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: "配置 ASP.NET Web API 2 |Microsoft 文档"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2014
ms.topic: article
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f9b471fe2afdce278869a2e4d9b693a78030324b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="d0a76-102">配置 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="d0a76-102">Configuring ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="d0a76-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d0a76-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d0a76-104">本主题介绍如何配置 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="d0a76-104">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="d0a76-105">配置设置</span><span class="sxs-lookup"><span data-stu-id="d0a76-105">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="d0a76-106">使用 ASP.NET 宿主配置 Web API</span><span class="sxs-lookup"><span data-stu-id="d0a76-106">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="d0a76-107">配置带 OWIN 自承载的 Web API</span><span class="sxs-lookup"><span data-stu-id="d0a76-107">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="d0a76-108">全局 Web API 服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-108">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="d0a76-109">每个控制器配置</span><span class="sxs-lookup"><span data-stu-id="d0a76-109">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="d0a76-110">配置设置</span><span class="sxs-lookup"><span data-stu-id="d0a76-110">Configuration Settings</span></span>

<span data-ttu-id="d0a76-111">在中定义的配置设置，web API [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx)类。</span><span class="sxs-lookup"><span data-stu-id="d0a76-111">Web API configuration setttings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="d0a76-112">成员</span><span class="sxs-lookup"><span data-stu-id="d0a76-112">Member</span></span> | <span data-ttu-id="d0a76-113">描述</span><span class="sxs-lookup"><span data-stu-id="d0a76-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0a76-114">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="d0a76-114">**DependencyResolver**</span></span> | <span data-ttu-id="d0a76-115">使控制器的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="d0a76-115">Enables dependency injection for controllers.</span></span> <span data-ttu-id="d0a76-116">请参阅[使用 Web API 依赖项解析程序](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-116">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="d0a76-117">**筛选器**</span><span class="sxs-lookup"><span data-stu-id="d0a76-117">**Filters**</span></span> | <span data-ttu-id="d0a76-118">操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-118">Action filters.</span></span> |
| <span data-ttu-id="d0a76-119">**格式化程序**</span><span class="sxs-lookup"><span data-stu-id="d0a76-119">**Formatters**</span></span> | <span data-ttu-id="d0a76-120">[媒体类型格式化程序](../formats-and-model-binding/media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-120">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="d0a76-121">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="d0a76-121">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="d0a76-122">指定服务器是否应在 HTTP 响应消息中包含错误详细信息，例如异常消息和堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="d0a76-122">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="d0a76-123">请参阅[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))。</span><span class="sxs-lookup"><span data-stu-id="d0a76-123">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="d0a76-124">**Initializer**</span><span class="sxs-lookup"><span data-stu-id="d0a76-124">**Initializer**</span></span> | <span data-ttu-id="d0a76-125">执行最终的初始化函数**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="d0a76-125">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="d0a76-126">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="d0a76-126">**MessageHandlers**</span></span> | <span data-ttu-id="d0a76-127">[HTTP 消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-127">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="d0a76-128">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="d0a76-128">**ParameterBindingRules**</span></span> | <span data-ttu-id="d0a76-129">用于在控制器操作绑定参数的规则的集合。</span><span class="sxs-lookup"><span data-stu-id="d0a76-129">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="d0a76-130">**属性**</span><span class="sxs-lookup"><span data-stu-id="d0a76-130">**Properties**</span></span> | <span data-ttu-id="d0a76-131">一个泛型属性包。</span><span class="sxs-lookup"><span data-stu-id="d0a76-131">A generic property bag.</span></span> |
| <span data-ttu-id="d0a76-132">**路由**</span><span class="sxs-lookup"><span data-stu-id="d0a76-132">**Routes**</span></span> | <span data-ttu-id="d0a76-133">路由的集合。</span><span class="sxs-lookup"><span data-stu-id="d0a76-133">The collection of routes.</span></span> <span data-ttu-id="d0a76-134">请参阅[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-134">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="d0a76-135">**服务**</span><span class="sxs-lookup"><span data-stu-id="d0a76-135">**Services**</span></span> | <span data-ttu-id="d0a76-136">服务集合。</span><span class="sxs-lookup"><span data-stu-id="d0a76-136">The collection of services.</span></span> <span data-ttu-id="d0a76-137">请参阅[服务](#services)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-137">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="d0a76-138">系统必备</span><span class="sxs-lookup"><span data-stu-id="d0a76-138">Prerequisites</span></span>

<span data-ttu-id="d0a76-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community、 Professional 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="d0a76-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional, or Enterprise Edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="d0a76-140">使用 ASP.NET 宿主配置 Web API</span><span class="sxs-lookup"><span data-stu-id="d0a76-140">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="d0a76-141">在 ASP.NET 应用程序，通过调用来配置 Web API [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx)中**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="d0a76-141">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="d0a76-142">**配置**方法采用单个参数的类型的委托**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="d0a76-142">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="d0a76-143">执行所有委托内你配置。</span><span class="sxs-lookup"><span data-stu-id="d0a76-143">Perform all of your configuation inside the delegate.</span></span>

<span data-ttu-id="d0a76-144">下面是使用匿名委托的示例：</span><span class="sxs-lookup"><span data-stu-id="d0a76-144">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="d0a76-145">在 Visual Studio 2017，"ASP.NET Web 应用程序"项目模板会自动设置的配置代码，如果在中选择"Web API"**新建 ASP.NET 项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="d0a76-145">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="d0a76-146">项目模板创建一个名为应用程序在 WebApiConfig.cs 文件\_开始文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0a76-146">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="d0a76-147">此代码文件定义应放置 Web API 配置代码的委托。</span><span class="sxs-lookup"><span data-stu-id="d0a76-147">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="d0a76-148">项目模板还添加调用从委托的代码，**应用程序\_启动**。</span><span class="sxs-lookup"><span data-stu-id="d0a76-148">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="d0a76-149">配置带 OWIN 自承载的 Web API</span><span class="sxs-lookup"><span data-stu-id="d0a76-149">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="d0a76-150">如果你是带 OWIN 自承载，创建一个新**HttpConfiguration**实例。</span><span class="sxs-lookup"><span data-stu-id="d0a76-150">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="d0a76-151">在此实例上执行任何配置，然后将传递到实例**Owin.UseWebApi**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="d0a76-151">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="d0a76-152">本教程[使用 OWIN 自承载 ASP.NET Web API 2 来](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)显示的完整步骤。</span><span class="sxs-lookup"><span data-stu-id="d0a76-152">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="d0a76-153">全局 Web API 服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-153">Global Web API Services</span></span>

<span data-ttu-id="d0a76-154">**HttpConfiguration.Services**集合包含一组 Web API 用于执行各种任务，如控制器所选内容和内容协商的全局服务。</span><span class="sxs-lookup"><span data-stu-id="d0a76-154">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a76-155">**服务**集合不是用于服务发现或依赖关系注入的通用机制。</span><span class="sxs-lookup"><span data-stu-id="d0a76-155">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="d0a76-156">它只存储到 Web API 框架已知的服务类型。</span><span class="sxs-lookup"><span data-stu-id="d0a76-156">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="d0a76-157">**服务**使用一组默认的服务，初始化集合，你可以提供你自己的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="d0a76-157">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="d0a76-158">某些服务支持多个实例，而其他人可以只有一个实例。</span><span class="sxs-lookup"><span data-stu-id="d0a76-158">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="d0a76-159">(但是，还可以在控制器级别的服务提供; 请参阅[-控制器配置](#percontrollerconfig)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-159">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="d0a76-160">单实例服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-160">Single-Instance Services</span></span>


| <span data-ttu-id="d0a76-161">服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-161">Service</span></span> | <span data-ttu-id="d0a76-162">描述</span><span class="sxs-lookup"><span data-stu-id="d0a76-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0a76-163">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="d0a76-163">**IActionValueBinder**</span></span> | <span data-ttu-id="d0a76-164">获取参数绑定。</span><span class="sxs-lookup"><span data-stu-id="d0a76-164">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="d0a76-165">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="d0a76-165">**IApiExplorer**</span></span> | <span data-ttu-id="d0a76-166">获取应用程序公开的 api 的说明。</span><span class="sxs-lookup"><span data-stu-id="d0a76-166">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="d0a76-167">请参阅[创建一个 Web API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-167">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="d0a76-168">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="d0a76-168">**IAssembliesResolver**</span></span> | <span data-ttu-id="d0a76-169">获取应用程序的程序集的列表。</span><span class="sxs-lookup"><span data-stu-id="d0a76-169">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="d0a76-170">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-170">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-171">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="d0a76-171">**IBodyModelValidator**</span></span> | <span data-ttu-id="d0a76-172">验证从请求正文中的媒体类型格式化程序读取的模型。</span><span class="sxs-lookup"><span data-stu-id="d0a76-172">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="d0a76-173">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="d0a76-173">**IContentNegotiator**</span></span> | <span data-ttu-id="d0a76-174">执行内容协商。</span><span class="sxs-lookup"><span data-stu-id="d0a76-174">Performs content negotiation.</span></span> |
| <span data-ttu-id="d0a76-175">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="d0a76-175">**IDocumentationProvider**</span></span> | <span data-ttu-id="d0a76-176">提供有关 Api 的文档。</span><span class="sxs-lookup"><span data-stu-id="d0a76-176">Provides documentation for APIs.</span></span> <span data-ttu-id="d0a76-177">默认值是**null**。</span><span class="sxs-lookup"><span data-stu-id="d0a76-177">The default is **null**.</span></span> <span data-ttu-id="d0a76-178">请参阅[创建一个 Web API 的帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-178">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="d0a76-179">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="d0a76-179">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="d0a76-180">指示主机是否应缓冲 HTTP 消息实体正文。</span><span class="sxs-lookup"><span data-stu-id="d0a76-180">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="d0a76-181">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="d0a76-181">**IHttpActionInvoker**</span></span> | <span data-ttu-id="d0a76-182">调用的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d0a76-182">Invokes a controller action.</span></span> <span data-ttu-id="d0a76-183">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-183">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-184">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="d0a76-184">**IHttpActionSelector**</span></span> | <span data-ttu-id="d0a76-185">选择的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d0a76-185">Selects a controller action.</span></span> <span data-ttu-id="d0a76-186">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-186">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-187">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="d0a76-187">**IHttpControllerActivator**</span></span> | <span data-ttu-id="d0a76-188">激活一个控制器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-188">Activates a controller.</span></span> <span data-ttu-id="d0a76-189">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-189">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-190">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="d0a76-190">**IHttpControllerSelector**</span></span> | <span data-ttu-id="d0a76-191">选择一个控制器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-191">Selects a controller.</span></span> <span data-ttu-id="d0a76-192">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-192">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-193">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="d0a76-193">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="d0a76-194">提供应用程序中的 Web API 控制器类型的列表。</span><span class="sxs-lookup"><span data-stu-id="d0a76-194">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="d0a76-195">请参阅[路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-195">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="d0a76-196">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="d0a76-196">**ITraceManager**</span></span> | <span data-ttu-id="d0a76-197">初始化跟踪 framework。</span><span class="sxs-lookup"><span data-stu-id="d0a76-197">Initializes the tracing framework.</span></span> <span data-ttu-id="d0a76-198">请参阅[在 ASP.NET Web API 中进行跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-198">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="d0a76-199">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="d0a76-199">**ITraceWriter**</span></span> | <span data-ttu-id="d0a76-200">提供的跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-200">Provides a trace writer.</span></span> <span data-ttu-id="d0a76-201">默认值为"无操作"跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-201">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="d0a76-202">请参阅[在 ASP.NET Web API 中进行跟踪](../testing-and-debugging/tracing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d0a76-202">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="d0a76-203">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="d0a76-203">**IModelValidatorCache**</span></span> | <span data-ttu-id="d0a76-204">提供的模型验证程序的缓存。</span><span class="sxs-lookup"><span data-stu-id="d0a76-204">Provides a cache of model validators.</span></span> |

<span data-ttu-id="d0a76-205">多实例服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-205">Multiple-Instance Services</span></span>


| <span data-ttu-id="d0a76-206">服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-206">Service</span></span> | <span data-ttu-id="d0a76-207">描述</span><span class="sxs-lookup"><span data-stu-id="d0a76-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0a76-208">**IFilterProvider**</span><span class="sxs-lookup"><span data-stu-id="d0a76-208">**IFilterProvider**</span></span> | <span data-ttu-id="d0a76-209">返回的控制器操作的筛选器的列表。</span><span class="sxs-lookup"><span data-stu-id="d0a76-209">Returns a list of filters for a controller action.</span></span> |
| <span data-ttu-id="d0a76-210">**ModelBinderProvider**</span><span class="sxs-lookup"><span data-stu-id="d0a76-210">**ModelBinderProvider**</span></span> | <span data-ttu-id="d0a76-211">返回给定类型的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="d0a76-211">Returns a model binder for a given type.</span></span> |
| <span data-ttu-id="d0a76-212">**ModelMetadataProvider**</span><span class="sxs-lookup"><span data-stu-id="d0a76-212">**ModelMetadataProvider**</span></span> | <span data-ttu-id="d0a76-213">模型可提供元数据。</span><span class="sxs-lookup"><span data-stu-id="d0a76-213">Provides metadata for a model.</span></span> |
| <span data-ttu-id="d0a76-214">**ModelValidatorProvider**</span><span class="sxs-lookup"><span data-stu-id="d0a76-214">**ModelValidatorProvider**</span></span> | <span data-ttu-id="d0a76-215">为模型提供一个验证程序。</span><span class="sxs-lookup"><span data-stu-id="d0a76-215">Provides a validator for a model.</span></span> |
| <span data-ttu-id="d0a76-216">**ValueProviderFactory**</span><span class="sxs-lookup"><span data-stu-id="d0a76-216">**ValueProviderFactory**</span></span> | <span data-ttu-id="d0a76-217">创建值提供程序。</span><span class="sxs-lookup"><span data-stu-id="d0a76-217">Creates a value provider.</span></span> <span data-ttu-id="d0a76-218">有关详细信息，请参阅 Mike 停止的博客文章[如何在 WebAPI 中创建自定义值提供程序](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="d0a76-218">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |<span data-ttu-id="d0a76-219">.</span><span class="sxs-lookup"><span data-stu-id="d0a76-219">.</span></span>

<span data-ttu-id="d0a76-220">若要添加到多实例服务的自定义实现，调用**添加**或**插入**上**服务**集合：</span><span class="sxs-lookup"><span data-stu-id="d0a76-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="d0a76-221">若要替换的自定义实现单实例服务，请调用**替换**上**服务**集合：</span><span class="sxs-lookup"><span data-stu-id="d0a76-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="d0a76-222">每个控制器配置</span><span class="sxs-lookup"><span data-stu-id="d0a76-222">Per-Controller Configuration</span></span>

<span data-ttu-id="d0a76-223">您可以重写每个控制器基础上的以下设置：</span><span class="sxs-lookup"><span data-stu-id="d0a76-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="d0a76-224">媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="d0a76-224">Media-type formatters</span></span>
- <span data-ttu-id="d0a76-225">参数绑定规则</span><span class="sxs-lookup"><span data-stu-id="d0a76-225">Parameter binding rules</span></span>
- <span data-ttu-id="d0a76-226">服务</span><span class="sxs-lookup"><span data-stu-id="d0a76-226">Services</span></span>

<span data-ttu-id="d0a76-227">为此，请定义实现的自定义特性**IControllerConfiguration**接口。</span><span class="sxs-lookup"><span data-stu-id="d0a76-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="d0a76-228">然后，将特性应用到控制器。</span><span class="sxs-lookup"><span data-stu-id="d0a76-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="d0a76-229">下面的示例将默认媒体类型格式化程序替换为自定义格式化程序。</span><span class="sxs-lookup"><span data-stu-id="d0a76-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="d0a76-230">**IControllerConfiguration.Initialize**方法采用两个参数：</span><span class="sxs-lookup"><span data-stu-id="d0a76-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="d0a76-231">**HttpControllerSettings**对象</span><span class="sxs-lookup"><span data-stu-id="d0a76-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="d0a76-232">**HttpControllerDescriptor**对象</span><span class="sxs-lookup"><span data-stu-id="d0a76-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="d0a76-233">**HttpControllerDescriptor**包含控制器，它可以检查用于信息说明 （例如，若要区分两个控制器） 的说明。</span><span class="sxs-lookup"><span data-stu-id="d0a76-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="d0a76-234">使用**HttpControllerSettings**要配置控制器对象。</span><span class="sxs-lookup"><span data-stu-id="d0a76-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="d0a76-235">此对象包含你可以基于每个控制器重写的配置参数的子集。</span><span class="sxs-lookup"><span data-stu-id="d0a76-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="d0a76-236">不要更改任何设置默认为全局**HttpConfiguration**对象。</span><span class="sxs-lookup"><span data-stu-id="d0a76-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
