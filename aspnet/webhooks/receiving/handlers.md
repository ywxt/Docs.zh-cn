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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET Webhook 处理程序

一旦 Webhook 请求验证的 WebHook 接收器通过后，就已准备好处理由用户代码。 这就是*处理程序*进入。 处理程序派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)而不是直接从接口派生的类。

WebHook 请求可以由一个或多个处理程序处理。 处理程序的调用顺序根据各自*顺序*属性将从最低到最高的顺序简单的整数 （建议为 1 到 100 之间）：

![WebHook 处理程序顺序属性关系图](_static/Handlers.png)

可以选择性地设置一个处理程序*响应*WebHookHandlerContext 这将导致处理停止和响应发送回作为对 WebHook 的 HTTP 响应上的属性。 在上面的示例中，因为它具有更高的顺序不是 B 和 B 的响应设置不会调用处理程序 C。

设置响应是通常仅适用于 Webhook 响应可以在其中执行信息发送回原始 API。 例如，这是与其中响应回发到 WebHook 的来自的通道的 Slack Webhook 的情况。 如果他们只想要接收来自该特定接收方的 Webhook，处理程序可以设置的接收方属性。 如果它们不能设置为所有这些调用的接收方。

响应的一个其他常见用途是使用*410 不存在*响应以指示 WebHook 不再处于活动状态，并且应提交任何后续请求。

默认情况下将由所有 WebHook 接收方调用处理程序。 但是，如果*接收方*属性设置为处理程序的名称，则该处理程序只会从该接收方收到 WebHook 请求。

## <a name="processing-a-webhook"></a>处理 WebHook

当调用处理程序时，它将获取[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)包含有关 WebHook 请求的信息。 这些数据，通常的 HTTP 请求正文，可以从*数据*属性。

数据类型通常是 JSON 或 HTML 窗体数据，但可以根据需要强制转换为更具体的类型。 例如，生成的 ASP.NET Webhook 的自定义 Webhook 可以转换为类型[CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) ，如下所示：

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

  ## <a name="queued-processing"></a>排队的处理

如果在几秒内未生成响应，大多数 WebHook 发件人将重新发送 WebHook。 这意味着您的处理程序必须完成的处理在不使其再次调用该时间范围内。

如果在处理花费的时间，或者更好地单独处理然后[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用于将 WebHook 请求提交给队列中，例如[Azure 存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。

大纲[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)此处提供了实现：

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
