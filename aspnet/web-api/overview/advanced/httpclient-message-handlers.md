---
uid: web-api/overview/advanced/httpclient-message-handlers
title: 在 ASP.NET Web API 中的 HttpClient 消息处理程序 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2012
ms.topic: article
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 805741b0ac682b7479ce82127df48b1b9a49a427
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506786"
---
<a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="df157-102">在 ASP.NET Web API 中的 HttpClient 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="df157-102">HttpClient Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="df157-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="df157-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="df157-104">A*消息处理程序*是接收 HTTP 请求，并返回 HTTP 响应的类。</span><span class="sxs-lookup"><span data-stu-id="df157-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="df157-105">通常情况下，消息处理程序的一系列链接在一起。</span><span class="sxs-lookup"><span data-stu-id="df157-105">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="df157-106">第一个处理程序接收的 HTTP 请求，会处理，并提供请求下一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="df157-106">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="df157-107">在某些时候，响应将创建并将会再次回升链。</span><span class="sxs-lookup"><span data-stu-id="df157-107">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="df157-108">此模式称为*委派*处理程序。</span><span class="sxs-lookup"><span data-stu-id="df157-108">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="df157-109">在客户端， **HttpClient**类使用消息处理程序来处理请求。</span><span class="sxs-lookup"><span data-stu-id="df157-109">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="df157-110">默认处理程序是**HttpClientHandler**，其中通过网络发送请求，并从服务器获取的响应。</span><span class="sxs-lookup"><span data-stu-id="df157-110">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="df157-111">你可以将自定义消息处理程序插入客户端管道：</span><span class="sxs-lookup"><span data-stu-id="df157-111">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="df157-112">ASP.NET Web API 还使用在服务器端的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="df157-112">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="df157-113">有关详细信息，请参阅[HTTP 消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="df157-113">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="df157-114">自定义消息处理程序</span><span class="sxs-lookup"><span data-stu-id="df157-114">Custom Message Handlers</span></span>

<span data-ttu-id="df157-115">若要编写自定义消息处理程序，派生自**System.Net.Http.DelegatingHandler** ，并重写**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="df157-115">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="df157-116">下面是方法签名：</span><span class="sxs-lookup"><span data-stu-id="df157-116">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="df157-117">该方法采用**HttpRequestMessage**作为输入并以异步方式返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="df157-117">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="df157-118">一个典型的实现将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="df157-118">A typical implementation does the following:</span></span>

1. <span data-ttu-id="df157-119">处理请求消息。</span><span class="sxs-lookup"><span data-stu-id="df157-119">Process the request message.</span></span>
2. <span data-ttu-id="df157-120">调用`base.SendAsync`将请求发送到内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="df157-120">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="df157-121">内部处理程序返回的响应消息。</span><span class="sxs-lookup"><span data-stu-id="df157-121">The inner handler returns a response message.</span></span> <span data-ttu-id="df157-122">（此步骤是异步的。）</span><span class="sxs-lookup"><span data-stu-id="df157-122">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="df157-123">处理响应，并将其返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="df157-123">Process the response and return it to the caller.</span></span>

<span data-ttu-id="df157-124">下面的示例显示的消息处理程序将自定义标头添加到传出的请求：</span><span class="sxs-lookup"><span data-stu-id="df157-124">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="df157-125">调用`base.SendAsync`是异步的。</span><span class="sxs-lookup"><span data-stu-id="df157-125">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="df157-126">如果处理程序此调用后执行任何工作，使用**await**关键字在方法完成之后继续执行。</span><span class="sxs-lookup"><span data-stu-id="df157-126">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="df157-127">下面的示例显示的处理程序日志错误代码。</span><span class="sxs-lookup"><span data-stu-id="df157-127">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="df157-128">本身的日志记录不是很有趣，但此示例演示如何获取在处理程序内响应。</span><span class="sxs-lookup"><span data-stu-id="df157-128">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="df157-129">将消息处理程序添加到客户端管道</span><span class="sxs-lookup"><span data-stu-id="df157-129">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="df157-130">若要添加到自定义处理程序**HttpClient**，使用**HttpClientFactory.Create**方法：</span><span class="sxs-lookup"><span data-stu-id="df157-130">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="df157-131">消息处理程序调用的顺序，将它们到传递**创建**方法。</span><span class="sxs-lookup"><span data-stu-id="df157-131">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="df157-132">由于嵌套处理程序的响应消息旅行反方向。</span><span class="sxs-lookup"><span data-stu-id="df157-132">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="df157-133">即，最后一个处理程序是以获取响应消息的第一个。</span><span class="sxs-lookup"><span data-stu-id="df157-133">That is, the last handler is the first to get the response message.</span></span>
