---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收方 |Microsoft 文档
author: rick-anderson
description: ASP.NET Webhook 接收方
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.technology: ''
ms.prod: .net-framework
ms.openlocfilehash: a8e42521f201f88b0ed433550e8786411b4487b0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="951d6-103">ASP.NET Webhook 接收方</span><span class="sxs-lookup"><span data-stu-id="951d6-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="951d6-104">接收 Webhook 取决于发件人是谁。</span><span class="sxs-lookup"><span data-stu-id="951d6-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="951d6-105">有时，有注册 WebHook 验证实际上正在侦听的订阅服务器上的其他步骤。</span><span class="sxs-lookup"><span data-stu-id="951d6-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="951d6-106">某些 Webhook 提供 HTTP POST 请求仅包含对然后则需要单独检索的事件信息的引用推送到拉取模型。</span><span class="sxs-lookup"><span data-stu-id="951d6-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="951d6-107">通常的安全模型很多各不相同。</span><span class="sxs-lookup"><span data-stu-id="951d6-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="951d6-108">Microsoft ASP.NET Webhook 的用途是时间的，使其更简单且更一致，以将你的 API 而无需花费了大量了解如何处理 Webhook 任何特定变体。</span><span class="sxs-lookup"><span data-stu-id="951d6-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="951d6-109">WebHook 接收方负责接受和验证来自特定发件人的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="951d6-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="951d6-110">WebHook 接收方可以支持任何数量的 Webhook，每个都有自己的配置。</span><span class="sxs-lookup"><span data-stu-id="951d6-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="951d6-111">例如，GitHub WebHook 接收方可以接受从任意数量的 GitHub 存储库的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="951d6-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="951d6-112">WebHook 接收方 Uri</span><span class="sxs-lookup"><span data-stu-id="951d6-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="951d6-113">通过安装 Microsoft ASP.NET Webhook，你可以接受从无限数量的服务的 WebHook 请求的常规 WebHook 控制器。</span><span class="sxs-lookup"><span data-stu-id="951d6-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="951d6-114">当请求到达时，它会选取的已安装用于处理特定的 WebHook 发件人的相应接收方。</span><span class="sxs-lookup"><span data-stu-id="951d6-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="951d6-115">此控制器的 URI 是向服务注册的 WebHook URI 和形式：</span><span class="sxs-lookup"><span data-stu-id="951d6-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="951d6-116">出于安全原因，许多 WebHook 接收方需要的 URI 是*https* URI 并在某些情况下，它还必须包含一个其他查询参数用于强制此要求仅预定的接收方可以将 Webhook 发送到上面的 URI.</span><span class="sxs-lookup"><span data-stu-id="951d6-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="951d6-117"><em> <receiver> </em>组件是接收方的名称，例如<em>github</em>或<em>slack</em>。</span><span class="sxs-lookup"><span data-stu-id="951d6-117">The <em><receiver></em> component is the name of the receiver, for example <em>github</em> or <em>slack</em>.</span></span>

<span data-ttu-id="951d6-118">*{Id}*是用于标识特定的 WebHook 接收方配置的可选标识符。</span><span class="sxs-lookup"><span data-stu-id="951d6-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="951d6-119">这可以用于 N 的 Webhook 注册特定的接收方。</span><span class="sxs-lookup"><span data-stu-id="951d6-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="951d6-120">例如，以下三个 Uri 可以用于为三个独立的 Webhook 注册：</span><span class="sxs-lookup"><span data-stu-id="951d6-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="951d6-121">安装 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="951d6-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="951d6-122">若要接收使用 Microsoft ASP.NET Webhook 的 Webhook，你首先安装为 WebHook 提供程序或你想要接收从 Webhook 的提供程序 Nuget 包。</span><span class="sxs-lookup"><span data-stu-id="951d6-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="951d6-123">Nuget 包名为[Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中的最后部分表示支持的服务。</span><span class="sxs-lookup"><span data-stu-id="951d6-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="951d6-124">例如</span><span class="sxs-lookup"><span data-stu-id="951d6-124">For example</span></span>

<span data-ttu-id="951d6-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)提供用于从 GitHub 接收 Webhook 的支持和[Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)用于接收 Webhook 生成的 ASP 提供支持。NET Webhook。</span><span class="sxs-lookup"><span data-stu-id="951d6-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="951d6-126">可以在初始状态下找到对 Dropbox、 GitHub、 MailChimp、 PayPal、 Pusher、 Salesforce、 Slack、 条带、 Trello，和 WordPress 的支持，但可以支持任意数量的其他提供程序。</span><span class="sxs-lookup"><span data-stu-id="951d6-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="951d6-127">配置 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="951d6-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="951d6-128">通过配置的 WebHook 接收方[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface 特定实现该接口的来注册和使用任何依赖关系注入模型。</span><span class="sxs-lookup"><span data-stu-id="951d6-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="951d6-129">默认实现使用应用程序设置，它可设置在 Web.config 文件中，或者，如果使用 Azure Web 应用程序，可通过设置[Azure 门户](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="951d6-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 应用程序设置](_static/AzureAppSettings.png)

<span data-ttu-id="951d6-131">应用程序设置密钥的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="951d6-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="951d6-132">值是匹配的值的以逗号分隔列表*{id}*值的 Webhook 已注册，例如：</span><span class="sxs-lookup"><span data-stu-id="951d6-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="951d6-133">初始化 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="951d6-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="951d6-134">WebHook 接收方初始化通过注册它们，通常在*WebApiConfig*静态类，例如：</span><span class="sxs-lookup"><span data-stu-id="951d6-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
