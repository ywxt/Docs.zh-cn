---
title: ASP.NET Core MVC 中的缓存标记帮助程序
author: pkellner
description: 演示如何使用缓存标记帮助程序
ms.author: riande
ms.date: 02/14/2017
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: 969716e21211513053f52049368a0a7190ffba47
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276547"
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="d94b4-103">ASP.NET Core MVC 中的缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="d94b4-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="d94b4-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="d94b4-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="d94b4-105">缓存标记帮助程序通过将其内容缓存到内部 ASP.NET Core 缓存提供程序中，可极大地提高 ASP.NET Core 应用的性能。</span><span class="sxs-lookup"><span data-stu-id="d94b4-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="d94b4-106">Razor 视图引擎将默认的 `expires-after` 设置为 20 分钟。</span><span class="sxs-lookup"><span data-stu-id="d94b4-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="d94b4-107">以下 Razor 标记将缓存日期/时间：</span><span class="sxs-lookup"><span data-stu-id="d94b4-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="d94b4-108">针对包含 `CacheTagHelper` 页面的第一个请求将显示当前的日期/时间。</span><span class="sxs-lookup"><span data-stu-id="d94b4-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="d94b4-109">其他请求将显示已缓存的值，直到缓存过期（默认 20 分钟）或被内存压力逐出。</span><span class="sxs-lookup"><span data-stu-id="d94b4-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="d94b4-110">可使用以下属性设置缓存持续时间：</span><span class="sxs-lookup"><span data-stu-id="d94b4-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="d94b4-111">缓存标记帮助程序属性</span><span class="sxs-lookup"><span data-stu-id="d94b4-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="d94b4-112">enabled</span><span class="sxs-lookup"><span data-stu-id="d94b4-112">enabled</span></span>    


| <span data-ttu-id="d94b4-113">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-113">Attribute Type</span></span>    | <span data-ttu-id="d94b4-114">有效值</span><span class="sxs-lookup"><span data-stu-id="d94b4-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="d94b4-115">boolean</span><span class="sxs-lookup"><span data-stu-id="d94b4-115">boolean</span></span>           | <span data-ttu-id="d94b4-116">“true”（默认值）</span><span class="sxs-lookup"><span data-stu-id="d94b4-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="d94b4-117">“false”</span><span class="sxs-lookup"><span data-stu-id="d94b4-117">"false"</span></span>   |


<span data-ttu-id="d94b4-118">确定是否缓存了缓存标记帮助程序所包含的内容。</span><span class="sxs-lookup"><span data-stu-id="d94b4-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="d94b4-119">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="d94b4-119">The default is `true`.</span></span>  <span data-ttu-id="d94b4-120">如果设置为 `false`，则此缓存标记帮助程序对于呈现的输出没有缓存效果。</span><span class="sxs-lookup"><span data-stu-id="d94b4-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="d94b4-121">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="d94b4-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="d94b4-122">expires-on</span></span> 

| <span data-ttu-id="d94b4-123">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-123">Attribute Type</span></span> |           <span data-ttu-id="d94b4-124">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-124">Example Value</span></span>            |
|----------------|------------------------------------|
| <span data-ttu-id="d94b4-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d94b4-125">DateTimeOffset</span></span> | <span data-ttu-id="d94b4-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="d94b4-126">"@new DateTime(2025,1,29,17,02,0)"</span></span> |

<span data-ttu-id="d94b4-127">设置一个绝对到期日期。</span><span class="sxs-lookup"><span data-stu-id="d94b4-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="d94b4-128">以下示例将在 2025 年 1 月 29 日下午 5:02 之前缓存缓存标记帮助程序的内容。</span><span class="sxs-lookup"><span data-stu-id="d94b4-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="d94b4-129">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="d94b4-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="d94b4-130">expires-after</span></span>

| <span data-ttu-id="d94b4-131">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-131">Attribute Type</span></span> |        <span data-ttu-id="d94b4-132">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-132">Example Value</span></span>         |
|----------------|------------------------------|
|    <span data-ttu-id="d94b4-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d94b4-133">TimeSpan</span></span>    | <span data-ttu-id="d94b4-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="d94b4-134">"@TimeSpan.FromSeconds(120)"</span></span> |

<span data-ttu-id="d94b4-135">设置从第一个请求时间到缓存内容的时间长度。</span><span class="sxs-lookup"><span data-stu-id="d94b4-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="d94b4-136">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="d94b4-137">expires-sliding</span><span class="sxs-lookup"><span data-stu-id="d94b4-137">expires-sliding</span></span>

| <span data-ttu-id="d94b4-138">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-138">Attribute Type</span></span> |        <span data-ttu-id="d94b4-139">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-139">Example Value</span></span>        |
|----------------|-----------------------------|
|    <span data-ttu-id="d94b4-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d94b4-140">TimeSpan</span></span>    | <span data-ttu-id="d94b4-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="d94b4-141">"@TimeSpan.FromSeconds(60)"</span></span> |

<span data-ttu-id="d94b4-142">设置缓存条目在未被访问时应被逐出的时间。</span><span class="sxs-lookup"><span data-stu-id="d94b4-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="d94b4-143">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="d94b4-144">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="d94b4-144">vary-by-header</span></span>

| <span data-ttu-id="d94b4-145">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-145">Attribute Type</span></span>    | <span data-ttu-id="d94b4-146">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-147">String</span><span class="sxs-lookup"><span data-stu-id="d94b4-147">String</span></span>            | <span data-ttu-id="d94b4-148">"User-Agent"</span><span class="sxs-lookup"><span data-stu-id="d94b4-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="d94b4-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="d94b4-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="d94b4-150">接受单个标头值或逗号分隔的标头值列表，在更改时触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="d94b4-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="d94b4-151">以下示例监视标头值 `User-Agent`。</span><span class="sxs-lookup"><span data-stu-id="d94b4-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="d94b4-152">该示例将缓存提供给 Web 服务器的每个不同 `User-Agent` 的内容。</span><span class="sxs-lookup"><span data-stu-id="d94b4-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="d94b4-153">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="d94b4-154">vary-by-query</span><span class="sxs-lookup"><span data-stu-id="d94b4-154">vary-by-query</span></span>

| <span data-ttu-id="d94b4-155">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-155">Attribute Type</span></span>    | <span data-ttu-id="d94b4-156">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-157">String</span><span class="sxs-lookup"><span data-stu-id="d94b4-157">String</span></span>            | <span data-ttu-id="d94b4-158">"Make"</span><span class="sxs-lookup"><span data-stu-id="d94b4-158">"Make"</span></span>                |
|                   | <span data-ttu-id="d94b4-159">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="d94b4-159">"Make,Model"</span></span> |

<span data-ttu-id="d94b4-160">接受单个标头值或逗号分隔的标头值列表，当标头值更改时触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="d94b4-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="d94b4-161">以下示例查看 `Make` 和 `Model` 的值。</span><span class="sxs-lookup"><span data-stu-id="d94b4-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="d94b4-162">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="d94b4-163">vary-by-route</span><span class="sxs-lookup"><span data-stu-id="d94b4-163">vary-by-route</span></span>

| <span data-ttu-id="d94b4-164">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-164">Attribute Type</span></span>    | <span data-ttu-id="d94b4-165">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-166">String</span><span class="sxs-lookup"><span data-stu-id="d94b4-166">String</span></span>            | <span data-ttu-id="d94b4-167">"Make"</span><span class="sxs-lookup"><span data-stu-id="d94b4-167">"Make"</span></span>                |
|                   | <span data-ttu-id="d94b4-168">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="d94b4-168">"Make,Model"</span></span> |

<span data-ttu-id="d94b4-169">接受单个标头值或逗号分隔的标头值列表，当路由数据参数值更改时触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="d94b4-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="d94b4-170">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-170">Example:</span></span>

<span data-ttu-id="d94b4-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="d94b4-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```

<span data-ttu-id="d94b4-172">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d94b4-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="d94b4-173">vary-by-cookie</span><span class="sxs-lookup"><span data-stu-id="d94b4-173">vary-by-cookie</span></span>

| <span data-ttu-id="d94b4-174">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-174">Attribute Type</span></span>    | <span data-ttu-id="d94b4-175">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-176">String</span><span class="sxs-lookup"><span data-stu-id="d94b4-176">String</span></span>            | <span data-ttu-id="d94b4-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="d94b4-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="d94b4-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="d94b4-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="d94b4-179">接受单个标头值或逗号分隔的标头值列表，当标头值更改时触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="d94b4-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="d94b4-180">以下示例查看与ASP.NET Identity 相关联的 cookie。</span><span class="sxs-lookup"><span data-stu-id="d94b4-180">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="d94b4-181">当用户经过身份验证时，要设置的请求 cookie 将触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="d94b4-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="d94b4-182">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="d94b4-183">vary-by-user</span><span class="sxs-lookup"><span data-stu-id="d94b4-183">vary-by-user</span></span>

| <span data-ttu-id="d94b4-184">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-184">Attribute Type</span></span>    | <span data-ttu-id="d94b4-185">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-186">Boolean</span><span class="sxs-lookup"><span data-stu-id="d94b4-186">Boolean</span></span>             | <span data-ttu-id="d94b4-187">“true”</span><span class="sxs-lookup"><span data-stu-id="d94b4-187">"true"</span></span>                  |
|                     | <span data-ttu-id="d94b4-188">“false”（默认值）</span><span class="sxs-lookup"><span data-stu-id="d94b4-188">"false" (default)</span></span> |

<span data-ttu-id="d94b4-189">指定当已登录用户（或上下文主体）更改时是否应该重置缓存。</span><span class="sxs-lookup"><span data-stu-id="d94b4-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="d94b4-190">当前用户也称为请求上下文主体，可通过引用 `@User.Identity.Name` 在 Razor 视图中查看。</span><span class="sxs-lookup"><span data-stu-id="d94b4-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="d94b4-191">以下示例查看当前登录的用户。</span><span class="sxs-lookup"><span data-stu-id="d94b4-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="d94b4-192">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="d94b4-193">通过登录和注销周期，使用此属性将内容维护在缓存中。</span><span class="sxs-lookup"><span data-stu-id="d94b4-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="d94b4-194">使用 `vary-by-user="true"` 时，登录和注销操作会使经过身份验证的用户的缓存无效。</span><span class="sxs-lookup"><span data-stu-id="d94b4-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="d94b4-195">缓存无效，因为登录时会生成一个新的唯一 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="d94b4-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="d94b4-196">当 cookie 不存在或已过期时，则维持缓存以呈现匿名状态。</span><span class="sxs-lookup"><span data-stu-id="d94b4-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="d94b4-197">这意味着如果没有用户登录，将维持缓存。</span><span class="sxs-lookup"><span data-stu-id="d94b4-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="d94b4-198">vary-by</span><span class="sxs-lookup"><span data-stu-id="d94b4-198">vary-by</span></span>

| <span data-ttu-id="d94b4-199">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-199">Attribute Type</span></span> | <span data-ttu-id="d94b4-200">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-200">Example Values</span></span> |
|----------------|----------------|
|     <span data-ttu-id="d94b4-201">String</span><span class="sxs-lookup"><span data-stu-id="d94b4-201">String</span></span>     |    <span data-ttu-id="d94b4-202">“@Model”</span><span class="sxs-lookup"><span data-stu-id="d94b4-202">"@Model"</span></span>    |

<span data-ttu-id="d94b4-203">允许自定义缓存的数据。</span><span class="sxs-lookup"><span data-stu-id="d94b4-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="d94b4-204">当属性的字符串值引用的对象发生更改时，会更新缓存标记帮助程序的内容。</span><span class="sxs-lookup"><span data-stu-id="d94b4-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="d94b4-205">通常将模型值的字符串串联分配给此属性。</span><span class="sxs-lookup"><span data-stu-id="d94b4-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="d94b4-206">从效果上看，这意味着更新任何已连接的值都会使缓存无效。</span><span class="sxs-lookup"><span data-stu-id="d94b4-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="d94b4-207">以下示例假定视图的控制器方法将两个路由参数 `myParam1` 和 `myParam2` 的整数值相加，并将其作为单个模型属性返回。</span><span class="sxs-lookup"><span data-stu-id="d94b4-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="d94b4-208">当此总和更改时，会再次呈现并缓存缓存标记帮助程序的内容。</span><span class="sxs-lookup"><span data-stu-id="d94b4-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="d94b4-209">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-209">Example:</span></span>

<span data-ttu-id="d94b4-210">操作：</span><span class="sxs-lookup"><span data-stu-id="d94b4-210">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="d94b4-211">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d94b4-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="d94b4-212">priority</span><span class="sxs-lookup"><span data-stu-id="d94b4-212">priority</span></span>

| <span data-ttu-id="d94b4-213">属性类型</span><span class="sxs-lookup"><span data-stu-id="d94b4-213">Attribute Type</span></span>    | <span data-ttu-id="d94b4-214">示例值</span><span class="sxs-lookup"><span data-stu-id="d94b4-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="d94b4-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="d94b4-215">CacheItemPriority</span></span>  | <span data-ttu-id="d94b4-216">"High"</span><span class="sxs-lookup"><span data-stu-id="d94b4-216">"High"</span></span>                   |
|                    | <span data-ttu-id="d94b4-217">"Low"</span><span class="sxs-lookup"><span data-stu-id="d94b4-217">"Low"</span></span> |
|                    | <span data-ttu-id="d94b4-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="d94b4-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="d94b4-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="d94b4-219">"Normal"</span></span> |

<span data-ttu-id="d94b4-220">为内置缓存提供程序提供缓存逐出指导。</span><span class="sxs-lookup"><span data-stu-id="d94b4-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="d94b4-221">在内存压力下，Web 服务器将首先逐出 `Low` 缓存条目。</span><span class="sxs-lookup"><span data-stu-id="d94b4-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="d94b4-222">示例:</span><span class="sxs-lookup"><span data-stu-id="d94b4-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="d94b4-223">`priority` 属性并不能保证特定级别的缓存保留。</span><span class="sxs-lookup"><span data-stu-id="d94b4-223">The `priority` attribute doesn't guarantee a specific level of cache retention.</span></span> <span data-ttu-id="d94b4-224">`CacheItemPriority` 仅供参考。</span><span class="sxs-lookup"><span data-stu-id="d94b4-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="d94b4-225">将此属性设置为 `NeverRemove` 并不能保证缓存将始终保留。</span><span class="sxs-lookup"><span data-stu-id="d94b4-225">Setting this attribute to `NeverRemove` doesn't guarantee that the cache will always be retained.</span></span> <span data-ttu-id="d94b4-226">有关详细信息，请参阅[其他资源](#additional-resources)。</span><span class="sxs-lookup"><span data-stu-id="d94b4-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="d94b4-227">缓存标记帮助程序依赖于[内存缓存服务](xref:performance/caching/memory)。</span><span class="sxs-lookup"><span data-stu-id="d94b4-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="d94b4-228">如果尚未添加该服务，缓存标记帮助程序将添加。</span><span class="sxs-lookup"><span data-stu-id="d94b4-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d94b4-229">其他资源</span><span class="sxs-lookup"><span data-stu-id="d94b4-229">Additional resources</span></span>

* [<span data-ttu-id="d94b4-230">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="d94b4-230">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="d94b4-231">标识简介</span><span class="sxs-lookup"><span data-stu-id="d94b4-231">Introduction to Identity</span></span>](xref:security/authentication/identity)
