---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 了解 ASP.NET MVC 的执行流程 |Microsoft Docs
author: microsoft
description: 了解 ASP.NET MVC framework 如何处理分步的浏览器请求。
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 34699c314eb862e91ecba8831c5092af9d47dc70
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823730"
---
<a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="af2e2-103">了解 ASP.NET MVC 的执行流程</span><span class="sxs-lookup"><span data-stu-id="af2e2-103">Understanding the ASP.NET MVC Execution Process</span></span>
====================
<span data-ttu-id="af2e2-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="af2e2-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="af2e2-105">了解 ASP.NET MVC framework 如何处理分步的浏览器请求。</span><span class="sxs-lookup"><span data-stu-id="af2e2-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>


<span data-ttu-id="af2e2-106">对基于 ASP.NET MVC 的 Web 应用程序请求首先穿过**UrlRoutingModule**对象，它是一个 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="af2e2-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="af2e2-107">此模块将分析请求并执行路由选择。</span><span class="sxs-lookup"><span data-stu-id="af2e2-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="af2e2-108">**UrlRoutingModule**对象将选择与当前请求匹配的第一个路由对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="af2e2-109">(路由对象是实现的类**RouteBase**，并且通常是实例**路由**类。)如果任何路由都不匹配， **UrlRoutingModule**对象不执行任何操作，并允许请求回退到常规的 ASP.NET 或 IIS 请求处理。</span><span class="sxs-lookup"><span data-stu-id="af2e2-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="af2e2-110">从所选**路由**对象， **UrlRoutingModule**对象获取**IRouteHandler**与关联的对象**路由**对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="af2e2-111">通常情况下，在 MVC 应用程序，这将的实例**MvcRouteHandler**。</span><span class="sxs-lookup"><span data-stu-id="af2e2-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="af2e2-112">**IRouteHandler**实例创建**IHttpHandler**对象，并将其传递**IHttpContext**对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="af2e2-113">默认情况下**IHttpHandler**实例为 MVC **MvcHandler**对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="af2e2-114">**MvcHandler**对象然后选择将最终处理该请求的控制器。</span><span class="sxs-lookup"><span data-stu-id="af2e2-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="af2e2-115">在 IIS 7.0 中运行的 ASP.NET MVC Web 应用程序，没有文件扩展名时，对于 MVC 项目所需。</span><span class="sxs-lookup"><span data-stu-id="af2e2-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="af2e2-116">但是，在 IIS 6.0 中，处理程序要求将.mvc 文件扩展名映射到 ASP.NET ISAPI DLL。</span><span class="sxs-lookup"><span data-stu-id="af2e2-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>


<span data-ttu-id="af2e2-117">模块和处理程序是 ASP.NET MVC 框架的入口点。</span><span class="sxs-lookup"><span data-stu-id="af2e2-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="af2e2-118">它们执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="af2e2-118">They perform the following actions:</span></span>

- <span data-ttu-id="af2e2-119">MVC Web 应用程序中选择相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="af2e2-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="af2e2-120">获取特定的控制器实例。</span><span class="sxs-lookup"><span data-stu-id="af2e2-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="af2e2-121">调用控制器的**Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="af2e2-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="af2e2-122">下面列出了 MVC Web 项目的执行阶段：</span><span class="sxs-lookup"><span data-stu-id="af2e2-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="af2e2-123">接收应用程序的第一个请求</span><span class="sxs-lookup"><span data-stu-id="af2e2-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="af2e2-124">在 Global.asax 文件中，**路由**对象添加到**RouteTable**对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="af2e2-125">执行的路由</span><span class="sxs-lookup"><span data-stu-id="af2e2-125">Perform routing</span></span> 

    - <span data-ttu-id="af2e2-126">**UrlRoutingModule**模块使用的第一个匹配**路由**对象中**RouteTable**集合创建**RouteData**对象，然后用来创建**RequestContext** (**IHttpContext**) 对象。</span><span class="sxs-lookup"><span data-stu-id="af2e2-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="af2e2-127">创建 MVC 请求处理程序</span><span class="sxs-lookup"><span data-stu-id="af2e2-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="af2e2-128">**MvcRouteHandler**对象创建的实例**MvcHandler**类，并将其传递**RequestContext**实例。</span><span class="sxs-lookup"><span data-stu-id="af2e2-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="af2e2-129">创建控制器</span><span class="sxs-lookup"><span data-stu-id="af2e2-129">Create controller</span></span> 

    - <span data-ttu-id="af2e2-130">**MvcHandler**对象使用**RequestContext**实例，以识别**IControllerFactory**对象 (通常的实例**借助于 DefaultControllerFactory**类) 来创建控制器实例。</span><span class="sxs-lookup"><span data-stu-id="af2e2-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="af2e2-131">执行控制器- **MvcHandler**实例调用控制器 s **Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="af2e2-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="af2e2-132">调用操作</span><span class="sxs-lookup"><span data-stu-id="af2e2-132">Invoke action</span></span> 

    - <span data-ttu-id="af2e2-133">大多数控制器均继承**控制器**基类。</span><span class="sxs-lookup"><span data-stu-id="af2e2-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="af2e2-134">为此，请控制器**ControllerActionInvoker**与控制器关联的对象将决定哪些操作方法的控制器类来调用，然后调用该方法。</span><span class="sxs-lookup"><span data-stu-id="af2e2-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="af2e2-135">执行结果</span><span class="sxs-lookup"><span data-stu-id="af2e2-135">Execute result</span></span> 

    - <span data-ttu-id="af2e2-136">典型操作方法可能会接收用户输入，准备合适的响应数据，并通过返回的结果类型执行结果。</span><span class="sxs-lookup"><span data-stu-id="af2e2-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="af2e2-137">可以执行的内置结果类型包括以下： **ViewResult** （其中一个将视图呈现和是最常用的结果类型）， **RedirectToRouteResult**， **RedirectResult**， **ContentResult**， **JsonResult**，并且**EmptyResult**。</span><span class="sxs-lookup"><span data-stu-id="af2e2-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
