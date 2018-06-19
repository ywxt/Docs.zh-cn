---
uid: webhooks/index
title: ASP.NET Webhook 概述 |Microsoft 文档
author: rick-anderson
description: ASP.NET Webhook 简介。
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.technology: ''
ms.prod: .net-framework
ms.openlocfilehash: 52399c23cdf393a2f7f94661fd48098ced65948c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26530046"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="e0628-103">ASP.NET Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="e0628-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="e0628-104">Webhook 是一种轻型的 HTTP 模式，为连接在一起的 Web Api 和 SaaS 服务提供简单的发布/订阅模型。</span><span class="sxs-lookup"><span data-stu-id="e0628-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="e0628-105">时事件发生在服务中，通知形式的 HTTP POST 请求发送到已注册的订阅服务器。</span><span class="sxs-lookup"><span data-stu-id="e0628-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="e0628-106">POST 请求包含有关事件这样就可以接收方可以采取相应行动的信息。</span><span class="sxs-lookup"><span data-stu-id="e0628-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="e0628-107">由于其简单起见，Webhook 已公开的大量服务包括[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [Slack](http://www.slack.com)，[条带](http://www.stripe.com)， [Trello](http://www.trello.com/)，以及更多。</span><span class="sxs-lookup"><span data-stu-id="e0628-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="e0628-108">例如，WebHook 可以指示文件已在进行了更改[Dropbox](http://dropbox.com/)，或代码更改已提交在 GitHub 中，或在已启动付款[PayPal](http://www.paypal.com/)，或已在中创建了卡[Trello](http://www.trello.com/)。</span><span class="sxs-lookup"><span data-stu-id="e0628-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="e0628-109">可能的匹配项是无限的 ！</span><span class="sxs-lookup"><span data-stu-id="e0628-109">The possibilities are endless!</span></span>

<span data-ttu-id="e0628-110">Microsoft ASP.NET Webhook 容易地同时发送和接收 Webhook ASP.NET 应用程序的一部分：</span><span class="sxs-lookup"><span data-stu-id="e0628-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="e0628-111">在接收端，它用于接收和处理从任意数量的 WebHook 提供程序的 Webhook 提供一个通用模型。</span><span class="sxs-lookup"><span data-stu-id="e0628-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="e0628-112">就支持现成[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [pusher](http://www.pusher.com)， [Salesforce](http://www.salesforce.com)， [Slack](http://www.slack.com)，[条带](http://www.stripe.com)， [Trello](http://www.trello.com/)，[WordPress](http://www.wordpress.com)和[Zendesk](https://www.zendesk.com/)但很容易添加支持的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e0628-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="e0628-113">在发送端为管理和存储用于将事件通知发送到正确的一组订阅服务器的订阅也提供支持。</span><span class="sxs-lookup"><span data-stu-id="e0628-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="e0628-114">这允许你定义自己的事件订阅服务器只能订阅和在操作发生时通知他们集。</span><span class="sxs-lookup"><span data-stu-id="e0628-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="e0628-115">两个部分可以根据你的方案拆分或一起使用。</span><span class="sxs-lookup"><span data-stu-id="e0628-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="e0628-116">如果你只需从其他服务接收 Webhook，则你可以使用只需的接收方部分;如果你只想要公开其他人的 Webhook 来使用，你可以做到这。</span><span class="sxs-lookup"><span data-stu-id="e0628-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="e0628-117">代码以 ASP.NET Web API 2 和 ASP.NET MVC 5 为目标，可用作[GitHub 上的 OSS](https://github.com/aspnet/WebHooks)。</span><span class="sxs-lookup"><span data-stu-id="e0628-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="e0628-118">Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="e0628-118">WebHooks Overview</span></span>

<span data-ttu-id="e0628-119">Webhook 是一种模式，这意味着，可变及其使用方式从服务到服务，但基本要旨是相同。</span><span class="sxs-lookup"><span data-stu-id="e0628-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="e0628-120">可以将 Webhook 视为简单的发布/订阅模型其中用户可以在其他位置发生的事件订阅。</span><span class="sxs-lookup"><span data-stu-id="e0628-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="e0628-121">事件通知作为 HTTP POST 请求包含有关事件本身的信息会传播。</span><span class="sxs-lookup"><span data-stu-id="e0628-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="e0628-122">通常 HTTP POST 请求包含 JSON 对象或由 WebHook 发件人包括有关导致 WebHook 事件的信息来触发的 HTML 窗体数据。</span><span class="sxs-lookup"><span data-stu-id="e0628-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="e0628-123">例如，从 WebHook POST 请求正文的示例[GitHub](http://www.github.com/)如下所示由于特定的存储库中打开一个新问题：</span><span class="sxs-lookup"><span data-stu-id="e0628-123">For example, an example of a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="e0628-124">若要确保 WebHook 确实是预期的发件人发，POST 请求被以某种方式保护，然后验证接收方。</span><span class="sxs-lookup"><span data-stu-id="e0628-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="e0628-125">例如， [GitHub Webhook](https://developer.github.com/webhooks/)包括*X 中心签名*与它使你不必担心由接收方实现检查请求正文的哈希的 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="e0628-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="e0628-126">WebHook 流通常将类似如下内容：</span><span class="sxs-lookup"><span data-stu-id="e0628-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="e0628-127">WebHook 发件人公开客户端可以订阅的事件。</span><span class="sxs-lookup"><span data-stu-id="e0628-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="e0628-128">事件描述可观察更改到系统，例如新的数据项已插入，完成后进程，或其他内容。</span><span class="sxs-lookup"><span data-stu-id="e0628-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="e0628-129">WebHook 接收方订阅注册 WebHook 包含四件事：</span><span class="sxs-lookup"><span data-stu-id="e0628-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="e0628-130">针对事件通知应其中发布在 HTTP POST 请求; 形式的 URI</span><span class="sxs-lookup"><span data-stu-id="e0628-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="e0628-131">一组描述为其应激发 WebHook; 的特定事件的筛选器</span><span class="sxs-lookup"><span data-stu-id="e0628-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="e0628-132">用于对 HTTP POST 请求中; 签名密钥</span><span class="sxs-lookup"><span data-stu-id="e0628-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="e0628-133">这是要包含在 HTTP POST 请求中的其他数据。</span><span class="sxs-lookup"><span data-stu-id="e0628-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="e0628-134">例如，这可以是其他 HTTP 标头字段或在 HTTP POST 请求正文中包含的属性。</span><span class="sxs-lookup"><span data-stu-id="e0628-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="e0628-135">一旦事件发生，找到匹配的 WebHook 注册并提交 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="e0628-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="e0628-136">通常情况下，HTTP POST 请求的生成是如果出于某种原因未响应收件人或 HTTP POST 请求将导致错误响应重试几次。</span><span class="sxs-lookup"><span data-stu-id="e0628-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="e0628-137">Webhook 处理管道</span><span class="sxs-lookup"><span data-stu-id="e0628-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="e0628-138">传入的 Webhook 的 Microsoft ASP.NET Webhook 处理管道类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="e0628-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 处理管道](_static/WebHookReceivers.png)

<span data-ttu-id="e0628-140">这两个关键概念此处*接收方*和*处理程序*:</span><span class="sxs-lookup"><span data-stu-id="e0628-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="e0628-141">*接收方*负责处理来自给定发件人的 WebHook 的特定风格和强制实施安全性检查，以确保确实是预期的发件人发 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="e0628-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="e0628-142">*处理程序*通常是用户代码运行处理特定的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="e0628-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="e0628-143">在以下节点中更多详细信息描述了这些概念。</span><span class="sxs-lookup"><span data-stu-id="e0628-143">In the following nodes these concepts are described in more details.</span></span>
