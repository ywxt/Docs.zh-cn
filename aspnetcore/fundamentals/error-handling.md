---
title: "ASP.NET Core 中的错误处理"
author: ardalis
description: "了解如何处理 ASP.NET Core 应用程序中的错误。"
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 11/30/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/error-handling
ms.openlocfilehash: 5b0cda7b79b8a9523d1ba6a9b321d22d3ccc753a
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-error-handling-in-aspnet-core"></a>ASP.NET Core 中的错误处理简介

作者：[Steve Smith](https://ardalis.com/) 和 [Tom Dykstra](https://github.com/tdykstra/)

本文介绍了在 ASP.NET Core 应用中处理错误的常见方法。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="the-developer-exception-page"></a>开发人员异常页

若要配置应用以显示有关异常的详细信息页面，请安装 `Microsoft.AspNetCore.Diagnostics` NuGet 包并将行添加到 [Startup 类中的 Configure 方法](startup.md)：

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

将 `UseDeveloperExceptionPage` 放在想要捕获异常的任何中间件之前，如 `app.UseMvc`。

>[!WARNING]
> 仅当应用在开发环境中运行时，才启用开发人员异常页。 在生产环境中运行应用时，无需公开详细的异常信息。 [了解有关配置环境的详细信息](environments.md)。

若要查看开发人员异常页，请运行环境设置为 `Development` 的示例应用程序，并将 `?throw=true` 添加到应用的基本 URL。 该页包含几个有关异常和请求的信息的选项卡。 第一个选项卡包括堆栈跟踪。 

![堆栈跟踪](error-handling/_static/developer-exception-page.png)

下一个选项卡显示查询字符串参数（若有）。

![查询字符串参数](error-handling/_static/developer-exception-page-query.png)

此请求没有任何 cookie，但是如果有，会显示在“Cookie”选项卡上。可看到最后一个选项卡中传递的标头。

![标头](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a>配置自定义异常处理页

最好配置一个异常处理程序页，可在应用未在 `Development` 环境中运行时使用。

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

在 MVC 应用中，请勿使用 HTTP 方法属性（如 `HttpGet`）显式修饰错误处理程序操作方法。 使用显式动词可防止某些请求访问该方法。

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a>配置状态代码页

默认情况下，应用不会为 HTTP 状态代码（如 500（内部服务器错误）或 404（未找到））提供丰富的状态代码页。 可通过将行添加到 `Configure` 方法来配置 `StatusCodePagesMiddleware`：

```csharp
app.UseStatusCodePages();
```

默认情况下，该中间件为常见的状态代码添加简单的纯文本处理程序（如 404）：

![404 页面](error-handling/_static/default-404-status-code.png)

中间件支持几种不同的扩展方法。 一种采用 Lambda 表达式，另一种采用内容类型和格式字符串。

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

还有重定向扩展方法。 一种向客户端发送 302 状态代码，另一种将原始状态代码返回到客户端，同时执行重定向 URL 的处理程序。

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

如果需要为某些请求禁用状态代码页，可执行如下操作：

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
  statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a>异常处理代码

异常处理页中的代码可能会引发异常。 建议在生产错误页面中包含纯静态内容。

此外，请注意，一旦发送了响应标头，便不能更改响应的状态代码，也不能运行任何异常页或处理程序。 响应必须完成，否则连接中止。

## <a name="server-exception-handling"></a>服务器异常处理

除了应用中的异常处理逻辑之外，托管应用的[服务器](servers/index.md)还会执行某些异常处理。 如果服务器在发送标头之前捕获到异常，服务器将发送无正文的 500 内部服务器错误响应。 如果服务器在发送标头之后捕获到异常，服务器将关闭连接。 应用不处理的请求由服务器处理。 发生的任何异常都由服务器的异常处理来处理。 任何配置的自定义错误页或异常处理中间件或筛选器都不会影响此行为。

## <a name="startup-exception-handling"></a>启动异常处理

只有承载层才能处理应用启动过程中发生的异常。 可使用 `captureStartupErrors` 和 `detailedErrors` 键[配置主机在启动期间响应错误的行为方式](hosting.md#detailed-errors)。

如果在主机地址/端口绑定之后发生错误，承载只能显示捕获的启动错误的错误页。 如果任何绑定由于任何原因失败，承载层记录一个关键异常，dotnet 进程故障，并且不显示错误页。

## <a name="aspnet-mvc-error-handling"></a>ASP.NET MVC 错误处理

[MVC](xref:mvc/overview) 应用有处理错误的某些其他选项，如配置异常筛选器和执行模型验证。

### <a name="exception-filters"></a>异常筛选器

在 MVC 应用中，可全局配置异常筛选器，也可根据每个控制器或每个操作配置异常筛选器。 这些筛选器处理在执行控制器操作或其他筛选器期间发生的任何未处理的异常，在其他情况下并不调用。 了解[筛选器](../mvc/controllers/filters.md)中有关异常筛选器的详细信息。

>[!TIP]
> 异常筛选器适合捕获 MVC 操作内发生的异常，但它们不如错误处理中间件灵活。 一般情况下建议使用中间件；仅在需要根据所选 MVC 操作以不同方式执行错误处理时，才使用筛选器。

### <a name="handling-model-state-errors"></a>处理模型状态错误

在调用每个控制器操作前进行[模型验证](../mvc/models/validation.md)，操作方法负责检查 `ModelState.IsValid` 并作出正确反应。

某些应用会选择遵循标准约定来处理模型验证错误，在这种情况下，可以在[筛选器](../mvc/controllers/filters.md)中实现此类策略。 应测试操作在无效模型状态下的行为方式。 在[测试控制器逻辑](../mvc/controllers/testing.md)中了解详细信息。



