---
uid: webhooks/receiving/handlers
title: ASP.NET Webhook 处理程序 |Microsoft Docs
author: rick-anderson
description: 如何处理 ASP.NET Webhook 中的请求。
ms.author: aspnetcontent
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: bc8f4ef3f4ade775b395d73dfa8d73fec92fba3f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841417"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="b0b3f-103">ASP.NET Webhook 处理程序</span><span class="sxs-lookup"><span data-stu-id="b0b3f-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="b0b3f-104">一旦 Webhook 请求验证的 WebHook 接收器通过后，就已准备好处理由用户代码。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="b0b3f-105">这就是*处理程序*进入。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-105">This is where *handlers* come in.</span></span> <span data-ttu-id="b0b3f-106">处理程序派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)而不是直接从接口派生的类。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="b0b3f-107">WebHook 请求可以由一个或多个处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="b0b3f-108">处理程序的调用顺序根据各自*顺序*属性将从最低到最高的顺序简单的整数 （建议为 1 到 100 之间）：</span><span class="sxs-lookup"><span data-stu-id="b0b3f-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 处理程序顺序属性关系图](_static/Handlers.png)

<span data-ttu-id="b0b3f-110">可以选择性地设置一个处理程序*响应*WebHookHandlerContext 这将导致处理停止和响应发送回作为对 WebHook 的 HTTP 响应上的属性。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="b0b3f-111">在上面的示例中，因为它具有更高的顺序不是 B 和 B 的响应设置不会调用处理程序 C。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="b0b3f-112">设置响应是通常仅适用于 Webhook 响应可以在其中执行信息发送回原始 API。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="b0b3f-113">例如，这是与其中响应回发到 WebHook 的来自的通道的 Slack Webhook 的情况。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="b0b3f-114">如果他们只想要接收来自该特定接收方的 Webhook，处理程序可以设置的接收方属性。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="b0b3f-115">如果它们不能设置为所有这些调用的接收方。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="b0b3f-116">响应的一个其他常见用途是使用*410 不存在*响应以指示 WebHook 不再处于活动状态，并且应提交任何后续请求。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="b0b3f-117">默认情况下将由所有 WebHook 接收方调用处理程序。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="b0b3f-118">但是，如果*接收方*属性设置为处理程序的名称，则该处理程序只会从该接收方收到 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="b0b3f-119">处理 WebHook</span><span class="sxs-lookup"><span data-stu-id="b0b3f-119">Processing a WebHook</span></span>

<span data-ttu-id="b0b3f-120">当调用处理程序时，它将获取[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)包含有关 WebHook 请求的信息。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="b0b3f-121">这些数据，通常的 HTTP 请求正文，可以从*数据*属性。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="b0b3f-122">数据类型通常是 JSON 或 HTML 窗体数据，但可以根据需要强制转换为更具体的类型。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="b0b3f-123">例如，生成的 ASP.NET Webhook 的自定义 Webhook 可以转换为类型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b0b3f-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="b0b3f-124">排队的处理</span><span class="sxs-lookup"><span data-stu-id="b0b3f-124">Queued Processing</span></span>

<span data-ttu-id="b0b3f-125">如果在几秒内未生成响应，大多数 WebHook 发件人将重新发送 WebHook。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="b0b3f-126">这意味着您的处理程序必须完成的处理在不使其再次调用该时间范围内。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="b0b3f-127">如果在处理花费的时间，或者更好地单独处理然后[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用于将 WebHook 请求提交给队列中，例如[Azure 存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b0b3f-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="b0b3f-128">大纲[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)此处提供了实现：</span><span class="sxs-lookup"><span data-stu-id="b0b3f-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
