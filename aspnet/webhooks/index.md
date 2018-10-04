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
# <a name="aspnet-webhooks-overview"></a>ASP.NET Webhook 概述

Webhook 是轻量级 HTTP 模式一起编写 Web Api 和 SaaS 服务提供简单的发布/订阅模型。 在服务中发生的事件时, 通知中的 HTTP POST 请求的形式发送到已注册的订阅。 POST 请求包含有关事件使得接收方可以采取相应行动的信息。

由于其简单性，Webhook 已公开的服务包括大量[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [Slack](http://www.slack.com)，[条带](http://www.stripe.com)， [Trello](http://www.trello.com/)，等等。 例如，WebHook 可以指示文件已在进行了更改[Dropbox](http://dropbox.com/)，或在 GitHub 中，已提交代码更改或已在启动付款[PayPal](http://www.paypal.com/)，或已在中创建卡片[Trello](http://www.trello.com/)。 一切皆有可能 ！

Microsoft ASP.NET Webhook 可以更轻松地同时发送和接收 Webhook 作为 ASP.NET 应用程序的一部分：

* 在接收端，它提供一种通用模式接收和处理从任意数量的 WebHook 提供程序的 Webhook。 它不再是支持与框[Dropbox](http://dropbox.com/)， [GitHub](http://www.github.com/)， [Bitbucket](https://bitbucket.org/)， [MailChimp](http://www.mailchimp.com/)， [PayPal](http://www.paypal.com/)， [pusher](http://www.pusher.com)， [Salesforce](http://www.salesforce.com)， [Slack](http://www.slack.com)， [Stripe](http://www.stripe.com)， [Trello](http://www.trello.com/)，[WordPress](http://www.wordpress.com)并[Zendesk](https://www.zendesk.com/)但很容易地添加对的详细信息的支持。

* 在发送端它进行管理和存储与将事件通知发送到一组正确的订阅服务器的订阅还提供支持。 这允许您定义您自己的订阅者可以订阅并操作发生时通知他们的事件集。

两个部分可以根据具体的方案在一起或分开使用。 如果只需要接收来自其他服务的 Webhook，则可以使用只接收方部分;如果只想要公开 Webhook 为其他人使用，然后您可以进行这项操作。

代码面向 ASP.NET Web API 2 和 ASP.NET MVC 5，可用作[GitHub 上的 OSS](https://github.com/aspnet/WebHooks)。

## <a name="webhooks-overview"></a>Webhook 概述

Webhook 是表示它而异的使用方式从服务到服务，但基本理念都是相同的模式。 可以将 Webhook 作为简单的发布/订阅模型，用户可以订阅事件发生的其他位置。 事件通知会作为包含有关事件本身的信息的 HTTP POST 请求。

通常，HTTP POST 请求包含 JSON 对象或 WebHook 发件人包括有关导致 WebHook 事件的信息确定触发 HTML 窗体数据。 例如，从 WebHook POST 请求正文的示例[GitHub](http://www.github.com/)如下所示由于正在特定的存储库中打开一个新问题：

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

若要确保 WebHook 确实来自预期的发送方，POST 请求被以某种方式保护，然后验证接收方。 例如， [GitHub Webhook](https://developer.github.com/webhooks/)包括*X 的中心签名*与接收方实现通过检查，因此无需担心它的请求正文的哈希值的 HTTP 标头。

WebHook 流通常是这样：

* WebHook 发送方公开客户端可以订阅的事件。 事件描述可观察更改到系统中，例如新的数据项已插入，完成后一个进程，还是其他内容。

* WebHook 接收方订阅通过注册 WebHook 包含以下四项内容：

     1. URI 的 HTTP POST 请求; 形式中，其中应发布事件通知

     2. 一组描述为其应触发 WebHook; 的特定事件的筛选器

     3. 一个密钥用于对 HTTP POST 请求;

     4. 这是要包含在 HTTP POST 请求中附加数据。 例如，这可以是其他 HTTP 标头字段或在 HTTP POST 请求正文中包含的属性。

* 事件发生，一旦找到匹配的 WebHook 注册和提交 HTTP POST 请求。 通常情况下，生成的 HTTP POST 请求的是如果出于某种原因未响应收件人或 HTTP POST 请求将导致错误响应重试几次。

## <a name="webhooks-processing-pipeline"></a>Webhook 处理管道

传入 Webhook 在 Microsoft ASP.NET Webhook 处理管道如下所示：

![ASP.NET Webhook 处理管道](_static/WebHookReceivers.png)

这两个关键概念这里*接收方*并*处理程序*:

* *接收方*负责处理从给定的发送方的特定风格的 WebHook 并强制执行安全检查，以确保 WebHook 请求实际上是从预期的发送方。

* *处理程序*通常是用户代码运行处理特定的 WebHook。

在以下节点中更多详细信息描述了这些概念。
