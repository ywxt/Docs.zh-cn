---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 应用程序生命周期 |Microsoft Docs
author: cephalin
description: 下载 PDF 文档绘制图表的一个 ASP.NET MVC 5 应用程序生命周期。 此生命周期文档提供 MVC 生命周期的高级视图...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/28/2014
ms.topic: article
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 98735f2e04bdd0f2fec19524e59f6272dbc4ca57
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393910"
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a><span data-ttu-id="d530e-104">ASP.NET MVC 5 应用程序生命周期</span><span class="sxs-lookup"><span data-stu-id="d530e-104">Lifecycle of an ASP.NET MVC 5 Application</span></span>
====================
<span data-ttu-id="d530e-105">通过[Cephas Lin](https://github.com/cephalin)</span><span class="sxs-lookup"><span data-stu-id="d530e-105">by [Cephas Lin](https://github.com/cephalin)</span></span>

[<span data-ttu-id="d530e-106">下载 PDF 文档</span><span class="sxs-lookup"><span data-stu-id="d530e-106">Download PDF Document</span></span>](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

<span data-ttu-id="d530e-107">此处，您可以下载 PDF 文档的图表的生命周期的每个 ASP.NET MVC 5 应用程序，接收 HTTP 请求发送的 HTTP 响应回客户端。</span><span class="sxs-lookup"><span data-stu-id="d530e-107">Here you can download a PDF document that charts the lifecycle of every ASP.NET MVC 5 application, from receiving the HTTP request to sending the HTTP response back to the client.</span></span> <span data-ttu-id="d530e-108">它旨在为那些不熟悉 ASP.NET MVC 的学习工具，而且还为那些需要深入了解应用程序的特定方面的参考。</span><span class="sxs-lookup"><span data-stu-id="d530e-108">It is designed both as an educational tool for those who are new to ASP.NET MVC and also as a reference for those who need to drill into specific aspects of the application.</span></span> <span data-ttu-id="d530e-109">PDF 文档具有以下功能：</span><span class="sxs-lookup"><span data-stu-id="d530e-109">The PDF document has the following features:</span></span>

- <span data-ttu-id="d530e-110">相关[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)阶段以帮助您了解 MVC 生地[ASP.NET 应用程序生命周期](https://msdn.microsoft.com/library/bb470252.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d530e-110">Relevant [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) stages to help you understand where MVC integrates into the [ASP.NET application lifecycle](https://msdn.microsoft.com/library/bb470252.aspx).</span></span>
- <span data-ttu-id="d530e-111">在 MVC 应用程序生命周期，其中您可以了解每个 MVC 应用程序通过在请求处理管道中的主要阶段的高级视图。</span><span class="sxs-lookup"><span data-stu-id="d530e-111">A high-level view of the MVC application lifecycle, where you can understand the major stages that every MVC application passes through in the request processing pipeline.</span></span>  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- <span data-ttu-id="d530e-112">显示向下钻取，请求处理管道的详细信息的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="d530e-112">A detail view that shows drills down into the details of the request processing pipeline.</span></span> <span data-ttu-id="d530e-113">您可以比较高级的视图和详细信息视图以查看如何生命周期的详细信息将收集到的各个阶段。</span><span class="sxs-lookup"><span data-stu-id="d530e-113">You can compare the high-level view and the detail view to see how the lifecycles details are collected into the various stages.</span></span> <span data-ttu-id="d530e-114">[下载 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)若要查看可查看大图。</span><span class="sxs-lookup"><span data-stu-id="d530e-114">[Download PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) to see a larger view.</span></span>
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- <span data-ttu-id="d530e-115">定位以及所有可重写方法的目的[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)请求处理管道中的对象。</span><span class="sxs-lookup"><span data-stu-id="d530e-115">Placement and purpose of all overridable methods on the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) object in the request processing pipeline.</span></span> <span data-ttu-id="d530e-116">您可能会或可能需要重写任何一种方法，但很重要，以便了解在应用程序生命周期中的角色，使您可以在适当的生命周期阶段的预期的效果编写代码。</span><span class="sxs-lookup"><span data-stu-id="d530e-116">You may or may not have the need to override any one method, but it is important for you to understand their role in the application lifecycle so that you can write code at the appropriate life cycle stage for the effect you intend.</span></span>
- <span data-ttu-id="d530e-117">解决问题向上关系图显示每个筛选器类型 （身份验证、 授权、 操作和结果） 的调用方式。</span><span class="sxs-lookup"><span data-stu-id="d530e-117">Blown-up diagrams showing how each of the filter types (authentication, authorization, action, and result) is invoked.</span></span>
- <span data-ttu-id="d530e-118">从每个点的详细信息视图中的相关链接到帮助性文章或博客。</span><span class="sxs-lookup"><span data-stu-id="d530e-118">Link to a useful article or blog from each point of interest in the detail view.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d530e-119">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d530e-119">Next Steps</span></span>

<span data-ttu-id="d530e-120">本文档是否满足您的需求？</span><span class="sxs-lookup"><span data-stu-id="d530e-120">Does this document meet your need?</span></span> <span data-ttu-id="d530e-121">我们将不胜感激您的反馈。</span><span class="sxs-lookup"><span data-stu-id="d530e-121">We'd appreciate your feedback.</span></span> <span data-ttu-id="d530e-122">如果你在应用程序中有任何问题的 ASP.NET MVC 生命周期[Stackoverflow](http://stackoverflow.com/help)并[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)所提出的好地方。</span><span class="sxs-lookup"><span data-stu-id="d530e-122">If you have any question on the ASP.NET MVC lifecycle in your application, [Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are great places to ask.</span></span> <span data-ttu-id="d530e-123">请按照[我](https://twitter.com/Cephas_MSFT)twitter 这样您就获得更新的我最新教程。</span><span class="sxs-lookup"><span data-stu-id="d530e-123">Follow [me](https://twitter.com/Cephas_MSFT) on twitter so you can get updates on my latest tutorials.</span></span>
