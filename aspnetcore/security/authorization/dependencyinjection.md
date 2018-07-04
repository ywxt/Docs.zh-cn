---
title: 在 ASP.NET Core 要求处理程序中的依赖关系注入
author: rick-anderson
description: 了解如何插入到 ASP.NET Core 应用使用依赖关系注入的授权要求处理程序。
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/dependencyinjection
ms.openlocfilehash: c6bb2589c6fef9f4586e6f4ddbb574866e6c48ab
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273717"
---
# <a name="dependency-injection-in-requirement-handlers-in-aspnet-core"></a>在 ASP.NET Core 要求处理程序中的依赖关系注入

<a name="security-authorization-di"></a>

[必须注册授权处理程序](xref:security/authorization/policies#handler-registration)在配置期间服务集合中 (使用[依赖关系注入](xref:fundamentals/dependency-injection#fundamentals-dependency-injection))。

假设您有你想要评估的授权处理程序内的规则的存储库和服务集合中注册了该存储库。 授权将解析和您的构造函数中的插入。

例如，如果你想要使用 ASP。NET 的日志记录你想要插入的基础结构`ILoggerFactory`到您的处理程序。 此类处理可能如下所示：

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

将注册处理程序替换`services.AddSingleton()`:

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

实例的处理程序将你的应用程序启动时，创建和插入的已注册的 DI 将`ILoggerFactory`到您的构造函数。

> [!NOTE]
> 使用实体框架的处理程序不应注册为单一实例。
