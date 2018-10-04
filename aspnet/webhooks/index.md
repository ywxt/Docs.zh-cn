---
uid: webhooks/index
title: ASP.NET Webhook 概述 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 简介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 702cc0bf0d0bb887c64bec19e1faf249bd96617a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "48252957"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="ed2c1-103">ASP.NET Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="ed2c1-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="ed2c1-104">Webhook 是轻量级 HTTP 模式一起编写 Web Api 和 SaaS 服务提供简单的发布/订阅模型。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="ed2c1-105">在服务中发生的事件时, 通知中的 HTTP POST 请求的形式发送到已注册的订阅。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="ed2c1-106">POST 请求包含有关事件使得接收方可以采取相应行动的信息。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="ed2c1-107">由于其简单性，Webhook 已公开的服务包括大量[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [Slack](http://www.slack.com)，[条带](http://www.stripe.com)， [Trello](http://www.trello.com/)，等等。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="ed2c1-108">例如，WebHook 可以指示文件已在进行了更改[Dropbox](http://dropbox.com/)，或在 GitHub 中，已提交代码更改或已在启动付款[PayPal](http://www.paypal.com/)，或已在中创建卡片[Trello](http://www.trello.com/)。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="ed2c1-109">一切皆有可能 ！</span><span class="sxs-lookup"><span data-stu-id="ed2c1-109">The possibilities are endless!</span></span>

<span data-ttu-id="ed2c1-110">Microsoft ASP.NET Webhook 可以更轻松地同时发送和接收 Webhook 作为 ASP.NET 应用程序的一部分：</span><span class="sxs-lookup"><span data-stu-id="ed2c1-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="ed2c1-111">在接收端，它提供一种通用模式接收和处理从任意数量的 WebHook 提供程序的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="ed2c1-112">它不再是支持与框[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [pusher](http://www.pusher.com)， [Salesforce](http://www.salesforce.com)， [Slack](http://www.slack.com)， [Stripe](http://www.stripe.com)， [Trello](http://www.trello.com/)，[WordPress](http://www.wordpress.com)并[Zendesk](https://www.zendesk.com/)但很容易地添加对的详细信息的支持。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="ed2c1-113">在发送端它进行管理和存储与将事件通知发送到一组正确的订阅服务器的订阅还提供支持。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="ed2c1-114">这允许您定义您自己的订阅者可以订阅并操作发生时通知他们的事件集。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="ed2c1-115">两个部分可以根据具体的方案在一起或分开使用。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="ed2c1-116">如果只需要接收来自其他服务的 Webhook，则可以使用只接收方部分;如果只想要公开 Webhook 为其他人使用，然后您可以进行这项操作。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="ed2c1-117">代码面向 ASP.NET Web API 2 和 ASP.NET MVC 5，可用作[GitHub 上的 OSS](https://github.com/aspnet/WebHooks)。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="ed2c1-118">Webhook 概述</span><span class="sxs-lookup"><span data-stu-id="ed2c1-118">WebHooks Overview</span></span>

<span data-ttu-id="ed2c1-119">Webhook 是表示它而异的使用方式从服务到服务，但基本理念都是相同的模式。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="ed2c1-120">可以将 Webhook 作为简单的发布/订阅模型，用户可以订阅事件发生的其他位置。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="ed2c1-121">事件通知会作为包含有关事件本身的信息的 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="ed2c1-122">通常，HTTP POST 请求包含 JSON 对象或 WebHook 发件人包括有关导致 WebHook 事件的信息确定触发 HTML 窗体数据。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="ed2c1-123">例如，从 WebHook POST 请求正文的示例[GitHub](http://www.github.com/)如下所示由于正在特定的存储库中打开一个新问题：</span><span class="sxs-lookup"><span data-stu-id="ed2c1-123">For example, an example of a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

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

<span data-ttu-id="ed2c1-124">若要确保 WebHook 确实来自预期的发送方，POST 请求被以某种方式保护，然后验证接收方。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="ed2c1-125">例如， [GitHub Webhook](https://developer.github.com/webhooks/)包括*X 的中心签名*与接收方实现通过检查，因此无需担心它的请求正文的哈希值的 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="ed2c1-126">WebHook 流通常是这样：</span><span class="sxs-lookup"><span data-stu-id="ed2c1-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="ed2c1-127">WebHook 发送方公开客户端可以订阅的事件。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="ed2c1-128">事件描述可观察更改到系统中，例如新的数据项已插入，完成后一个进程，还是其他内容。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="ed2c1-129">WebHook 接收方订阅通过注册 WebHook 包含以下四项内容：</span><span class="sxs-lookup"><span data-stu-id="ed2c1-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="ed2c1-130">URI 的 HTTP POST 请求; 形式中，其中应发布事件通知</span><span class="sxs-lookup"><span data-stu-id="ed2c1-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="ed2c1-131">一组描述为其应触发 WebHook; 的特定事件的筛选器</span><span class="sxs-lookup"><span data-stu-id="ed2c1-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="ed2c1-132">一个密钥用于对 HTTP POST 请求;</span><span class="sxs-lookup"><span data-stu-id="ed2c1-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="ed2c1-133">这是要包含在 HTTP POST 请求中附加数据。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="ed2c1-134">例如，这可以是其他 HTTP 标头字段或在 HTTP POST 请求正文中包含的属性。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="ed2c1-135">事件发生，一旦找到匹配的 WebHook 注册和提交 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="ed2c1-136">通常情况下，生成的 HTTP POST 请求的是如果出于某种原因未响应收件人或 HTTP POST 请求将导致错误响应重试几次。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="ed2c1-137">Webhook 处理管道</span><span class="sxs-lookup"><span data-stu-id="ed2c1-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="ed2c1-138">传入 Webhook 在 Microsoft ASP.NET Webhook 处理管道如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed2c1-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 处理管道](_static/WebHookReceivers.png)

<span data-ttu-id="ed2c1-140">这两个关键概念这里*接收方*并*处理程序*:</span><span class="sxs-lookup"><span data-stu-id="ed2c1-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="ed2c1-141">*接收方*负责处理从给定的发送方的特定风格的 WebHook 并强制执行安全检查，以确保 WebHook 请求实际上是从预期的发送方。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="ed2c1-142">*处理程序*通常是用户代码运行处理特定的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="ed2c1-143">在以下节点中更多详细信息描述了这些概念。</span><span class="sxs-lookup"><span data-stu-id="ed2c1-143">In the following nodes these concepts are described in more details.</span></span>
