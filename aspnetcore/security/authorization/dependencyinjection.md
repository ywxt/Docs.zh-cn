---
title: "要求处理程序中的依赖关系注入"
author: rick-anderson
description: "本文档概述了如何插入到 ASP.NET Core 应用使用依赖关系注入的授权要求处理程序。"
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 1b7506b49109264a8c628ea2e39ded9f5ace95d3
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="dependency-injection-in-requirement-handlers"></a><span data-ttu-id="1515c-103">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="1515c-103">Dependency Injection in requirement handlers</span></span>

<a name="security-authorization-di"></a>

<span data-ttu-id="1515c-104">[必须注册授权处理程序](policies.md#handler-registration)在配置期间服务集合中 (使用[依赖关系注入](../../fundamentals/dependency-injection.md#fundamentals-dependency-injection))。</span><span class="sxs-lookup"><span data-stu-id="1515c-104">[Authorization handlers must be registered](policies.md#handler-registration) in the service collection during configuration (using [dependency injection](../../fundamentals/dependency-injection.md#fundamentals-dependency-injection)).</span></span>

<span data-ttu-id="1515c-105">假设您有你想要评估的授权处理程序内的规则的存储库和服务集合中注册了该存储库。</span><span class="sxs-lookup"><span data-stu-id="1515c-105">Suppose you had a repository of rules you wanted to evaluate inside an authorization handler and that repository was registered in the service collection.</span></span> <span data-ttu-id="1515c-106">授权将解析和您的构造函数中的插入。</span><span class="sxs-lookup"><span data-stu-id="1515c-106">Authorization will resolve and inject that into your constructor.</span></span>

<span data-ttu-id="1515c-107">例如，如果你想要使用 ASP。NET 的日志记录你想要插入的基础结构`ILoggerFactory`到您的处理程序。</span><span class="sxs-lookup"><span data-stu-id="1515c-107">For example, if you wanted to use ASP.NET's logging infrastructure you would want to inject `ILoggerFactory` into your handler.</span></span> <span data-ttu-id="1515c-108">此类处理可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="1515c-108">Such a handler might look like:</span></span>

```csharp
public class LoggingAuthorizationHandler : AuthorizationHandler<MyRequirement>
   {
       ILogger _logger;

       public LoggingAuthorizationHandler(ILoggerFactory loggerFactory)
       {
           _logger = loggerFactory.CreateLogger(this.GetType().FullName);
       }

       protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MyRequirement requirement)
       {
           _logger.LogInformation("Inside my handler");
           // Check if the requirement is fulfilled.
           return Task.CompletedTask;
       }
   }
   ```

<span data-ttu-id="1515c-109">将注册处理程序替换`services.AddSingleton()`:</span><span class="sxs-lookup"><span data-stu-id="1515c-109">You would register the handler with `services.AddSingleton()`:</span></span>

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

<span data-ttu-id="1515c-110">实例的处理程序将你的应用程序启动时，创建和插入的已注册的 DI 将`ILoggerFactory`到您的构造函数。</span><span class="sxs-lookup"><span data-stu-id="1515c-110">An instance of the handler will be created when your application starts, and DI will inject the registered `ILoggerFactory` into your constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="1515c-111">使用实体框架的处理程序不应注册为单一实例。</span><span class="sxs-lookup"><span data-stu-id="1515c-111">Handlers that use Entity Framework shouldn't be registered as singletons.</span></span>
