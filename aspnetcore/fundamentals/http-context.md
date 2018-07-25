---
title: 在 ASP.NET Core 中访问 HttpContext
author: coderandhiker
description: 了解如何在 ASP.NET Core 中访问 HttpContext。
ms.author: riande
ms.custom: mvc
ms.date: 07/20/2018
uid: fundamentals/httpcontext
ms.openlocfilehash: b1ff80943db1788b465accd51c70a3c3a3462d5c
ms.sourcegitcommit: a3675f9704e4e73ecc7cbbbf016a13d2a5c4d725
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2018
ms.locfileid: "39202701"
---
# <a name="access-httpcontext-in-aspnet-core"></a><span data-ttu-id="9eac5-103">在 ASP.NET Core 中访问 HttpContext</span><span class="sxs-lookup"><span data-stu-id="9eac5-103">Access HttpContext in ASP.NET Core</span></span>

<span data-ttu-id="9eac5-104">ASP.NET Core 应用通过 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 接口及其默认实现 [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor) 来访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="9eac5-104">ASP.NET Core apps access the `HttpContext` through the [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) interface and its default implementation [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor).</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="use-httpcontext-from-razor-pages"></a><span data-ttu-id="9eac5-105">通过 Razor Pages 使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="9eac5-105">Use HttpContext from Razor Pages</span></span>

<span data-ttu-id="9eac5-106">Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 公开 [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) 属性：</span><span class="sxs-lookup"><span data-stu-id="9eac5-106">The Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) exposes the [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) property:</span></span>

```csharp
public class AboutModel : PageModel
{
    public string Message { get; set; }

    public void OnGet()
    {
        Message = HttpContext.Request.PathBase;
    }
}
```

::: moniker-end

## <a name="use-httpcontext-from-a-controller"></a><span data-ttu-id="9eac5-107">通过控制器使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="9eac5-107">Use HttpContext from a controller</span></span>

<span data-ttu-id="9eac5-108">控制器公开 [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) 属性：</span><span class="sxs-lookup"><span data-stu-id="9eac5-108">Controllers expose the [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) property:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult About()
    {
        var pathBase = HttpContext.Request.PathBase;
        // Do something with the PathBase.

        return View();
    }
}
```

## <a name="use-httpcontext-from-middleware"></a><span data-ttu-id="9eac5-109">通过中间件使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="9eac5-109">Use HttpContext from middleware</span></span>

<span data-ttu-id="9eac5-110">使用自定义中间件组件时，`HttpContext` 传递到 `Invoke` 或 `InvokeAsync` 方法，在中间件配置后可供访问：</span><span class="sxs-lookup"><span data-stu-id="9eac5-110">When working with custom middleware components, `HttpContext` is passed into the `Invoke` or `InvokeAsync` method and can be accessed when the middleware is configured:</span></span>

```csharp
public class MyCustomMiddleware
{
    public Task InvokeAsync(HttpContext context)
    {
        // Middleware initialization optionally using HttpContext
    }
}
```

## <a name="use-httpcontext-from-custom-components"></a><span data-ttu-id="9eac5-111">通过自定义组件使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="9eac5-111">Use HttpContext from custom components</span></span>

<span data-ttu-id="9eac5-112">对于需要访问 `HttpContext` 的其他框架和自定义组件，建议使用内置的[依赖项注入](xref:fundamentals/dependency-injection)容器来注册依赖项。</span><span class="sxs-lookup"><span data-stu-id="9eac5-112">For other framework and custom components that require access to `HttpContext`, the recommended approach is to register a dependency using the built-in [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="9eac5-113">依赖项注入容器向任意类提供 `IHttpContextAccessor`，以供类在自己的构造函数中将它声明为依赖项。</span><span class="sxs-lookup"><span data-stu-id="9eac5-113">The dependency injection container supplies the `IHttpContextAccessor` to any classes that declare it as a dependency in their constructors.</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc()
         .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
     services.AddHttpContextAccessor();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc();
     services.AddSingleton<IHttpContextAccessor, HttpContextAccessor>();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

<span data-ttu-id="9eac5-114">在上面的示例中：</span><span class="sxs-lookup"><span data-stu-id="9eac5-114">In the preceding example:</span></span>

* <span data-ttu-id="9eac5-115">`UserRepository` 声明自己对 `IHttpContextAccessor` 的依赖。</span><span class="sxs-lookup"><span data-stu-id="9eac5-115">`UserRepository` declares its dependency on `IHttpContextAccessor`.</span></span>
* <span data-ttu-id="9eac5-116">当依赖项注入容器解析依赖链并创建 `UserRepository` 实例时，就会注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="9eac5-116">The dependency is supplied when dependency injection resolves the dependency chain and creates an instance of `UserRepository`.</span></span>

```csharp
public class UserRepository : IUserRepository
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserRepository(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public void LogCurrentUser()
    {
        var username = _httpContextAccessor.HttpContext.User.Identity.Name;
        service.LogAccessRequest(username);
    }
}
```
