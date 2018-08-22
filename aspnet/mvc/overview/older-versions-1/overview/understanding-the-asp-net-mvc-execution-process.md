---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 了解 ASP.NET MVC 的执行流程 |Microsoft Docs
author: microsoft
description: 了解 ASP.NET MVC framework 如何处理分步的浏览器请求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 3a3bcf4b78e3b19fb4d293f67b68c3a790d05221
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830054"
---
<a name="understanding-the-aspnet-mvc-execution-process"></a>了解 ASP.NET MVC 的执行流程
====================
by [Microsoft](https://github.com/microsoft)

> 了解 ASP.NET MVC framework 如何处理分步的浏览器请求。


对基于 ASP.NET MVC 的 Web 应用程序请求首先穿过**UrlRoutingModule**对象，它是一个 HTTP 模块。 此模块将分析请求并执行路由选择。 **UrlRoutingModule**对象将选择与当前请求匹配的第一个路由对象。 (路由对象是实现的类**RouteBase**，并且通常是实例**路由**类。)如果任何路由都不匹配， **UrlRoutingModule**对象不执行任何操作，并允许请求回退到常规的 ASP.NET 或 IIS 请求处理。

从所选**路由**对象， **UrlRoutingModule**对象获取**IRouteHandler**与关联的对象**路由**对象。 通常情况下，在 MVC 应用程序，这将的实例**MvcRouteHandler**。 **IRouteHandler**实例创建**IHttpHandler**对象，并将其传递**IHttpContext**对象。 默认情况下**IHttpHandler**实例为 MVC **MvcHandler**对象。 **MvcHandler**对象然后选择将最终处理该请求的控制器。

> [!NOTE]
> 在 IIS 7.0 中运行的 ASP.NET MVC Web 应用程序，没有文件扩展名时，对于 MVC 项目所需。 但是，在 IIS 6.0 中，处理程序要求将.mvc 文件扩展名映射到 ASP.NET ISAPI DLL。


模块和处理程序是 ASP.NET MVC 框架的入口点。 它们执行以下操作：

- MVC Web 应用程序中选择相应的控制器。
- 获取特定的控制器实例。
- 调用控制器的**Execute**方法。

下面列出了 MVC Web 项目的执行阶段：

- 接收应用程序的第一个请求 

    - 在 Global.asax 文件中，**路由**对象添加到**RouteTable**对象。
- 执行的路由 

    - **UrlRoutingModule**模块使用的第一个匹配**路由**对象中**RouteTable**集合创建**RouteData**对象，然后用来创建**RequestContext** (**IHttpContext**) 对象。
- 创建 MVC 请求处理程序 

    - **MvcRouteHandler**对象创建的实例**MvcHandler**类，并将其传递**RequestContext**实例。
- 创建控制器 

    - **MvcHandler**对象使用**RequestContext**实例，以识别**IControllerFactory**对象 (通常的实例**借助于 DefaultControllerFactory**类) 来创建控制器实例。
- 执行控制器- **MvcHandler**实例调用控制器 s **Execute**方法。 |
- 调用操作 

    - 大多数控制器均继承**控制器**基类。 为此，请控制器**ControllerActionInvoker**与控制器关联的对象将决定哪些操作方法的控制器类来调用，然后调用该方法。
- 执行结果 

    - 典型操作方法可能会接收用户输入，准备合适的响应数据，并通过返回的结果类型执行结果。 可以执行的内置结果类型包括以下： **ViewResult** （其中一个将视图呈现和是最常用的结果类型）， **RedirectToRouteResult**， **RedirectResult**， **ContentResult**， **JsonResult**，并且**EmptyResult**。
