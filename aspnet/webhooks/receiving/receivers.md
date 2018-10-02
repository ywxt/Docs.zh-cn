---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收方 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收方
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: 13940eb53c68664b11a2d685ee17c78faab1945d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860909"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Webhook 接收方

接收 Webhook 取决于发件人是谁。 有时有注册 WebHook 验证订阅服务器上实际侦听的其他步骤。 某些 Webhook 提供 HTTP POST 请求只包含对它然后将单独检索的事件信息的引用的推送与提取模型。 通常的安全模型改变了不少。

Microsoft ASP.NET Webhook 的目的是，使其更简单且更一致而无法接通你的 API，而无需花费大量时间来了解如何处理 Webhook 的任何特定变体。

WebHook 接收方负责接受和验证来自特定发件人的 Webhook。 WebHook 接收方可以支持任意数量的 Webhook，每个都有自己的配置。 例如，GitHub WebHook 接收方可以接受从任意数量的 GitHub 存储库的 Webhook。

## <a name="webhook-receiver-uris"></a>WebHook 接收方的 Uri

通过安装 Microsoft ASP.NET Webhook 可以获得常规的 WebHook 控制器，它接受从无限数量的服务的 WebHook 请求。 当请求到达时，它会选取适当的接收方已安装用于处理特定的 WebHook 发件人。

此控制器的 URI 是注册到服务的 WebHook URI，并且是窗体：

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

出于安全原因，许多 WebHook 接收方需要的 URI 是*https* URI 并在某些情况下，则还必须包含一个其他查询参数，用于强制此要求仅预定的接收方可以将 Webhook 发送到更高版本的 URI.

`<receiver>`组件是名称的接收方，例如`github`或`slack`。

*{Id}* 是用于标识特定的 WebHook 接收器配置的可选标识符。 这可以用于将注册特定的接收方的 n 个 Webhook。 例如，以下三个 Uri 可用于为三个独立的 Webhook 注册：

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>安装 WebHook 接收方

若要接收使用 Microsoft ASP.NET Webhook 的 Webhook，首先安装 Nuget 包为 WebHook 提供程序或你想要接收从 Webhook 提供程序。 名为 Nuget 包[Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中的最后一个部分指示支持的服务。 例如

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)提供支持，接收来自 GitHub 的 Webhook 和[Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)提供支持，用于接收生成的 ASP 的 Webhook。NET Webhook。

在初始状态下可以找到对 Dropbox、 GitHub、 MailChimp、 PayPal、 Pusher、 Salesforce、 Slack、 条带、 Trello 和 WordPress 的支持，但可以支持任意数量的其他提供程序。

## <a name="configuring-a-webhook-receiver"></a>配置 WebHook 接收方

通过配置的 WebHook 接收器[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)可以使用任何依赖关系注入模型已注册界面，该接口的特定实现。 默认实现使用应用程序设置可以设置 Web.config 文件中，或如果使用 Azure Web 应用，可以通过设置[Azure 门户](https://portal.azure.com/)。

![Azure 应用程序设置](_static/AzureAppSettings.png)

应用程序设置密钥的格式如下所示：

```
MS_WebHookReceiverSecret_<receiver>
```

值是以逗号分隔列表匹配的值 *{id}* 值为其 Webhook 已注册，例如：

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>初始化 WebHook 接收方

通过注册它们，通常在初始化 WebHook 接收方*WebApiConfig*静态类，例如：

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
