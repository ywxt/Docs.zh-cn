---
title: "ASP.NET Core 中间件"
author: rick-anderson
description: "了解有关 ASP.NET Core 中间件和请求管道。"
keywords: "ASP.NET Core，中间件，管道、 委托"
ms.author: riande
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.assetid: db9a86ab-46c2-40e0-baed-86e38c16af1f
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/middleware
ms.openlocfilehash: ad8d207b1e6de396f16d098fb07ddc89bea2c520
ms.sourcegitcommit: 8f4d4fad1ca27adf9e396f5c205c9875a3963664
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2017
---
# <a name="aspnet-core-middleware-fundamentals"></a>ASP.NET 核心中间件基础知识

<a name="fundamentals-middleware"></a>

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)和[Steve Smith](https://ardalis.com/)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-is-middleware"></a>什么是中间件

中间件是装配到应用程序管道中以处理请求和响应的软件。 每个组件：

* 可以选择是否要将请求传递到管道中的下一个组件。
* 可以在调用管道中的下一个组件之前和之后执行工作。 

请求委托用于构建请求管道，并处理每个 HTTP 请求。

请求委托使用[Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions)，[Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)，和[Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)扩展方法进行配置。 一个单独的请求委托可以指定为一个内联的匿名方法（称为内联中间件），也可以在可重用类中定义它。 这些可重用的类和内联匿名方法即*中间件*或*中间件组件*。 请求管道中的每个中间件组件负责调用管道中的下一个组件，或者在适当的情况下将链路短路。

[将HTTP模块迁移到中间件](../migration/http-modules.md)解释了ASP.NET Core和早期版本中的请求管道之间的区别，并提供了更多的中间件示例。

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a>使用 IApplicationBuilder 创建中间件管道

ASP.NET Core 请求管道由一系列请求委托组成，依次调用，如图所示（执行线程遵循黑色箭头）：

![请求处理模式显示请求到达，通过三个中间件处理，以及离开应用程序的响应。 每个中间件都运行其逻辑，并在 next() 语句中将请求交给下一个中间件。 在第三个中间件处理完请求之后，在离开应用程序作为对客户端的响应之前，通过之前的两个中间件在每个 next() 语句之后依次进行额外的处理。](middleware/_static/request-delegate-pipeline.png)

每个委托可以在下一个委托之前和之后执行操作。 委托也可以决定不将请求传递给下一个委托，这被称为将请求管道短路。 短路往往是必要的，因为它避免了不必要的工作。 例如，静态文件中间件可以返回一个静态文件的请求，并将管道的其余部分短路。 异常处理委托需要在管道的早期调用，因此它们可以捕获在管道后期发生的异常。

最简单的 ASP.NET Core 应用程序可以设置一个处理所有请求的单一请求委托。 这个例子不包括实际的请求管道。 相反，只调用一个匿名函数来响应每个HTTP请求。

[!code-csharp[Main](middleware/sample/Middleware/Startup.cs)]

第一个[app.Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions)委托终止管道。

你可以使用[app.Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)链接多个请求委托。 `next`参数表示管道中的下一步委托。 (请记住，你可以通过*不*调用*next*参数来使管道短路。)通常你可以在下一步委托之前和之后执行操作，如本示例所示：

[!code-csharp[Main](middleware/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> 不要在响应发送到客户端之后调用`next.Invoke`。 在响应已经启动后更改`HttpResponse`将引发异常。 例如，设置标头、 状态代码等变化将引发异常。 在调用`next`之后写入响应正文:
> - 可能会导致违反协议。 例如，写入超过规定`content-length`的内容。
> - 可能会损坏正文格式。 例如，向 CSS 文件中写入一个 HTML 页脚。
>
> [HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted)是一个有用的提示，以指示标头是否已被发送和/或正文已经写入。

## <a name="ordering"></a>顺序

中间件组件在`Configure`方法中添加的顺序定义了它们在请求中被调用的顺序，以及相对的响应顺序。 此顺序对于安全性，性能和功能至关重要。

Configure 方法 （如下所示） 将添加以下的中间件组件：

1. 异常/错误处理
2. 静态文件服务
3. 身份验证
4. MVC

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)


```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseAuthentication();               // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseIdentity();                     // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

-----------

在上面的代码中，`UseExceptionHandler`是第一个添加到管道的中间件组件，因此它捕获了之后调用中发生的任何异常。

静态文件中间件在管道的早期被调用，因此它无需通过其余的组件就可以处理请求并短路。 静态文件中间件**不**提供授权检查。 它所提供的任何文件，包括*wwwroot*下的文件都是可以公开访问的。 请参阅[使用静态文件](xref:fundamentals/static-files)了解保护静态文件的方法。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)


如果请求不是由静态文件中间件处理的，则将其传递到身份验证中间件（`app.UseAuthentication`），来执行身份验证。 身份验证中间件不会短路未经身份验证的请求。 尽管身份验证中间件会认证请求，但只有在MVC选择一个特定的 Razor 页面或控制器和动作后，才会触发授权（和拒绝）。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

如果请求不是由静态文件中间件处理的，则将其传递到 身份验证中间件中间件（`app.UseIdentity`），来执行身份验证。 身份验证中间件不会短路未经身份验证的请求。 尽管身份验证中间件会认证请求，但只有在MVC选择一个特定的 Razor 页面或控制器和动作后，才会触发授权（和拒绝）。

-----------

下面的示例演示了一个中间件的排序，静态文件中间件在响应压缩中间件之前处理静态文件的请求。根据此中间件顺序，静态文件不会进行压缩。 来自[UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)的 MVC 响应可以被压缩。

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();         // Static files not compressed
                                  // by middleware.
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

<a name="middleware-run-map-use"></a>

### <a name="use-run-and-map"></a>Use、 Run 和 Map

使用`Use`，`Run`和`Map`来配置HTTP管道。 `Use`方法可以使管道短路（也就是说，如果它不调用`next`请求委托的话）。 `Run`是一种约定，一些中间件组件可能暴露`Run[Middleware]`方法，其在管道结束时运行。

`Map`扩展用作分支管道的约定。 [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)根据给定请求路径的匹配来对请求管道进行分支。 如果请求路径以给定的路径开始，则执行分支。

[!code-csharp[Main](middleware/sample/Chain/StartupMap.cs?name=snippet1)]

下表使用前面的代码显示了来自`http://localhost:1234`的请求和响应：

| 请求 | 响应 |
| --- | --- |
| localhost:1234 | Hello from non-Map delegate.  |
| localhost:1234/map1 | Map Test 1 |
| localhost:1234/map2 | Map Test 2 |
| localhost:1234/map3 | Hello from non-Map delegate.  |

使用`Map`时，将从`HttpRequest.Path`中删除匹配的路径片段，并将其附加到每个请求的`HttpRequest.PathBase`。

[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions)根据给定谓词的结果对请求管道进行分支。 任何类型为`Func <HttpContext，bool>`的谓词都可用于将请求映射到管道的新分支。 在以下示例中，谓词用于检测查询字符串变量`branch`的存在：

[!code-csharp[Main](middleware/sample/Chain/StartupMapWhen.cs?name=snippet1)]

下表使用前面的代码显示了来自`http://localhost:1234`的请求和响应：

| 请求 | 响应 |
| --- | --- |
| localhost:1234 | Hello from non-Map delegate.  |
| localhost:1234/?branch=master | Branch used = master |

`Map`支持嵌套，例如：

```csharp
app.Map("/level1", level1App => {
       level1App.Map("/level2a", level2AApp => {
           // "/level1/level2a"
           //...
       });
       level1App.Map("/level2b", level2BApp => {
           // "/level1/level2b"
           //...
       });
   });
   ```

`Map`也可以同时匹配多个片段，例如：

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a>内置中间件

ASP.NET Core 附带以下的中间件组件：

| 中间件 | 描述 |
| ----- | ------- |
| [Authentication(身份验证)](xref:security/authentication/identity) | 提供身份验证支持。 |
| [CORS](xref:security/cors) | 配置跨域资源共享。 |
| [Response Caching(响应缓存)](xref:performance/caching/middleware) | 提供对缓存响应的支持。 |
| [Response Compression(响应压缩)](xref:performance/response-compression) | 提供对压缩响应的支持。 |
| [Routing(路由)](xref:fundamentals/routing) | 定义和约束请求路由。 |
| [Session(会话)](xref:fundamentals/app-state) | 提供用于管理用户会话的支持。 |
| [Static Files(静态文件)](xref:fundamentals/static-files) | 为静态文件和目录浏览提供支持。 |
| [URL Rewriting Middleware(URL 重写中间件)](xref:fundamentals/url-rewriting) | 为Url重写和请求重定向提供支持。 |

<a name="middleware-writing-middleware"></a>

## <a name="writing-middleware"></a>编写中间件

中间件通常封装在一个类中，并使用扩展方法公开。 考虑以下中间件，它从查询字符串中设置当前请求的区域性：

[!code-csharp[Main](middleware/sample/Culture/StartupCulture.cs?name=snippet1)]

注意：上面的示例代码用于演示创建中间件组件。 请参阅[全球化和本地化](xref:fundamentals/localization)了解ASP.NET Core 内置的本地化支持。

您可以通过传入culture参数来测试该中间件，例如`http://localhost:7997/?culture=no`。

以下代码将中间件委托移动到一个类中：

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddleware.cs)]

下面的扩展方法通过[IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder)公开中间件:

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

下面的代码从`Configure`调用中间件:

[!code-csharp[Main](middleware/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

中间件应该通过在其构造函数中暴露其依赖项来遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。 中间件在每个*应用程序生命周期*中仅构造一次。 如果您需要在一个请求中与中间件共享服务，请参阅下面的*每个请求的依赖关系*。

中间件组件可以通过构造函数参数从依赖注入来解析它们的依赖项。 [`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary)也可以直接接受其他参数。

### <a name="per-request-dependencies"></a>每个请求的依赖关系

由于中间件是在应用程序启动时构建的，而不是在每个请求中构建，所以在每个请求期间，中间件构造函数使用的*作用域*生命周期服务不会与其他依赖注入类型共享。 如果您必须在中间件和其他类型之间共享一个*作用域*服务，请将这些服务添加到`Invoke`方法的签名中。 `Invoke`方法可以接受由依赖注入生成的其他参数。 例如：

```c#
public class MyMiddleware
{
    private readonly RequestDelegate _next;

    public MyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="resources"></a>资源

* [在本文档中使用的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample)
* [将 HTTP 模块迁移到中间件](../migration/http-modules.md)
* [应用程序启动](startup.md)
* [请求功能](request-features.md)
