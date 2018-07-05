---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收方 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收方
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.technology: ''
ms.openlocfilehash: be1f7dcef60642231af9c593eb7329ede7c2094f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374738"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="0c183-103">ASP.NET Webhook 接收方</span><span class="sxs-lookup"><span data-stu-id="0c183-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="0c183-104">接收 Webhook 取决于发件人是谁。</span><span class="sxs-lookup"><span data-stu-id="0c183-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="0c183-105">有时有注册 WebHook 验证订阅服务器上实际侦听的其他步骤。</span><span class="sxs-lookup"><span data-stu-id="0c183-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="0c183-106">某些 Webhook 提供 HTTP POST 请求只包含对它然后将单独检索的事件信息的引用的推送与提取模型。</span><span class="sxs-lookup"><span data-stu-id="0c183-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="0c183-107">通常的安全模型改变了不少。</span><span class="sxs-lookup"><span data-stu-id="0c183-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="0c183-108">Microsoft ASP.NET Webhook 的目的是，使其更简单且更一致而无法接通你的 API，而无需花费大量时间来了解如何处理 Webhook 的任何特定变体。</span><span class="sxs-lookup"><span data-stu-id="0c183-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="0c183-109">WebHook 接收方负责接受和验证来自特定发件人的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="0c183-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="0c183-110">WebHook 接收方可以支持任意数量的 Webhook，每个都有自己的配置。</span><span class="sxs-lookup"><span data-stu-id="0c183-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="0c183-111">例如，GitHub WebHook 接收方可以接受从任意数量的 GitHub 存储库的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="0c183-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="0c183-112">WebHook 接收方的 Uri</span><span class="sxs-lookup"><span data-stu-id="0c183-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="0c183-113">通过安装 Microsoft ASP.NET Webhook 可以获得常规的 WebHook 控制器，它接受从无限数量的服务的 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="0c183-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="0c183-114">当请求到达时，它会选取适当的接收方已安装用于处理特定的 WebHook 发件人。</span><span class="sxs-lookup"><span data-stu-id="0c183-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="0c183-115">此控制器的 URI 是注册到服务的 WebHook URI，并且是窗体：</span><span class="sxs-lookup"><span data-stu-id="0c183-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="0c183-116">出于安全原因，许多 WebHook 接收方需要的 URI 是*https* URI 并在某些情况下，则还必须包含一个其他查询参数，用于强制此要求仅预定的接收方可以将 Webhook 发送到更高版本的 URI.</span><span class="sxs-lookup"><span data-stu-id="0c183-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="0c183-117"><em> <receiver> </em>组件是名称的接收方，例如<em>github</em>或<em>slack</em>。</span><span class="sxs-lookup"><span data-stu-id="0c183-117">The <em><receiver></em> component is the name of the receiver, for example <em>github</em> or <em>slack</em>.</span></span>

<span data-ttu-id="0c183-118">*{Id}* 是用于标识特定的 WebHook 接收器配置的可选标识符。</span><span class="sxs-lookup"><span data-stu-id="0c183-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="0c183-119">这可以用于将注册特定的接收方的 n 个 Webhook。</span><span class="sxs-lookup"><span data-stu-id="0c183-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="0c183-120">例如，以下三个 Uri 可用于为三个独立的 Webhook 注册：</span><span class="sxs-lookup"><span data-stu-id="0c183-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="0c183-121">安装 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="0c183-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="0c183-122">若要接收使用 Microsoft ASP.NET Webhook 的 Webhook，首先安装 Nuget 包为 WebHook 提供程序或你想要接收从 Webhook 提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c183-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="0c183-123">名为 Nuget 包[Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中的最后一个部分指示支持的服务。</span><span class="sxs-lookup"><span data-stu-id="0c183-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="0c183-124">例如</span><span class="sxs-lookup"><span data-stu-id="0c183-124">For example</span></span>

<span data-ttu-id="0c183-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)提供支持，接收来自 GitHub 的 Webhook 和[Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)提供支持，用于接收生成的 ASP 的 Webhook。NET Webhook。</span><span class="sxs-lookup"><span data-stu-id="0c183-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="0c183-126">在初始状态下可以找到对 Dropbox、 GitHub、 MailChimp、 PayPal、 Pusher、 Salesforce、 Slack、 条带、 Trello 和 WordPress 的支持，但可以支持任意数量的其他提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c183-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="0c183-127">配置 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="0c183-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="0c183-128">通过配置的 WebHook 接收器[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)可以使用任何依赖关系注入模型已注册界面，该接口的特定实现。</span><span class="sxs-lookup"><span data-stu-id="0c183-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="0c183-129">默认实现使用应用程序设置可以设置 Web.config 文件中，或如果使用 Azure Web 应用，可以通过设置[Azure 门户](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0c183-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 应用程序设置](_static/AzureAppSettings.png)

<span data-ttu-id="0c183-131">应用程序设置密钥的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c183-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="0c183-132">值是以逗号分隔列表匹配的值 *{id}* 值为其 Webhook 已注册，例如：</span><span class="sxs-lookup"><span data-stu-id="0c183-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="0c183-133">初始化 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="0c183-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="0c183-134">通过注册它们，通常在初始化 WebHook 接收方*WebApiConfig*静态类，例如：</span><span class="sxs-lookup"><span data-stu-id="0c183-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
