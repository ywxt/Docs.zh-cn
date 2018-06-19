---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 应用程序生命周期 |Microsoft 文档
author: cephalin
description: 下载 PDF 文档绘制图表的 ASP.NET MVC 5 应用程序生命周期。 此生命周期文档提供的 MVC 生命周期的高级视图...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/28/2014
ms.topic: article
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 50d58d10c11677fa72ede6a03e686cbde4cbae1d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28036487"
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="db27a-104">ASP.NET MVC 5 应用程序生命周期</span><span class="sxs-lookup"><span data-stu-id="db27a-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>
====================
<span data-ttu-id="db27a-105">通过[Cephas Lin](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="db27a-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="db27a-106">下载 PDF 文档</span><span class="sxs-lookup"><span data-stu-id="db27a-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="db27a-107">此处你可以下载的图表的生命周期的每个 ASP.NET MVC 5 应用程序，接收 HTTP 请求发送的 HTTP 响应回客户端的 PDF 文档。</span><span class="sxs-lookup"><span data-stu-id="db27a-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="db27a-108">它旨在为那些不熟悉 ASP.NET MVC 的教学工具，而且还作为那些需要深入了解应用程序的特定方面的参考。</span><span class="sxs-lookup"><span data-stu-id="db27a-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="db27a-109">PDF 文档具有以下功能：</span><span class="sxs-lookup"><span data-stu-id="db27a-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="db27a-110">相关[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)阶段以帮助你了解 MVC 集成到[ASP.NET 应用程序生命周期](https://msdn.microsoft.com/library/bb470252.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db27a-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="db27a-111">MVC 应用程序生命周期，，您可以从中了解每个 MVC 应用程序通过在请求处理管道中的主要阶段的高级视图。</span><span class="sxs-lookup"><span data-stu-id="db27a-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="db27a-112">显示向下钻取，到请求处理管道的详细信息的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="db27a-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="db27a-113">你可以比较高级视图和详细信息视图以查看如何生命周期的详细信息将收集到的各个阶段。</span><span class="sxs-lookup"><span data-stu-id="db27a-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="db27a-114">[下载 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)若要查看更大的视图。</span><span class="sxs-lookup"><span data-stu-id="db27a-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="db27a-115">放置和用途的所有可重写方法[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)请求处理管道中的对象。</span><span class="sxs-lookup"><span data-stu-id="db27a-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="db27a-116">你可能或可能不需要重写任何一种方法，但务必要了解应用程序生命周期中的其角色，以便你可以在适当的生命周期阶段的预期的效果编写代码。</span><span class="sxs-lookup"><span data-stu-id="db27a-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="db27a-117">断了向上关系图显示如何调用每个筛选器类型 （身份验证、 授权、 操作和结果）。</span><span class="sxs-lookup"><span data-stu-id="db27a-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="db27a-118">链接到有用的文章或博客与感兴趣的详细信息视图的每个点。</span><span class="sxs-lookup"><span data-stu-id="db27a-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>


## <a name="next-steps"></a><span data-ttu-id="db27a-119">后续步骤</span><span class="sxs-lookup"><span data-stu-id="db27a-119">Next Steps</span></span>

<span data-ttu-id="db27a-120">本文档是否满足您的需求？</span><span class="sxs-lookup"><span data-stu-id="db27a-120">Does this document meet your need?</span></span> <span data-ttu-id="db27a-121">我们会十分感激你的反馈。</span><span class="sxs-lookup"><span data-stu-id="db27a-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="db27a-122">如果你有任何问题的 ASP.NET MVC 生命周期中你的应用程序， [Stackoverflow](http://stackoverflow.com/help)和[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)是可以提出的极佳位置。</span><span class="sxs-lookup"><span data-stu-id="db27a-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="db27a-123">请按照[我](https://twitter.com/Cephas_MSFT)以便您可以获取我的最新教程上的更新在 twitter 上。</span><span class="sxs-lookup"><span data-stu-id="db27a-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
