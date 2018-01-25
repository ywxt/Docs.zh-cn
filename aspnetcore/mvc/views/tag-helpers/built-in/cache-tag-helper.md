---
title: "缓存 ASP.NET Core MVC 中的标记帮助器"
author: pkellner
description: "演示如何使用缓存标记帮助器"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: 10aa1b493dbd0672cac789f6e48ddf2f14ba35dc
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="5bfd1-103">缓存 ASP.NET Core MVC 中的标记帮助器</span><span class="sxs-lookup"><span data-stu-id="5bfd1-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="5bfd1-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="5bfd1-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="5bfd1-105">缓存标记帮助器提供的功能可以显著提高通过缓存其内容与内部 ASP.NET Core 缓存提供程序的 ASP.NET Core 应用的性能。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="5bfd1-106">Razor 视图引擎设置的默认`expires-after`到 20 分钟。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="5bfd1-107">以下 Razor 标记缓存日期/时间：</span><span class="sxs-lookup"><span data-stu-id="5bfd1-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="5bfd1-108">对包含的页的第一个请求`CacheTagHelper`将显示当前日期/时间。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="5bfd1-109">缓存过期 （默认值 20 分钟），或内存压力逐出之前，其他请求将显示缓存的值。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="5bfd1-110">你可以设置具有以下属性将缓存持续时间：</span><span class="sxs-lookup"><span data-stu-id="5bfd1-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="5bfd1-111">缓存标记帮助器属性</span><span class="sxs-lookup"><span data-stu-id="5bfd1-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="5bfd1-112">enabled</span><span class="sxs-lookup"><span data-stu-id="5bfd1-112">enabled</span></span>    


| <span data-ttu-id="5bfd1-113">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-113">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-114">有效值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="5bfd1-115">boolean</span><span class="sxs-lookup"><span data-stu-id="5bfd1-115">boolean</span></span>           | <span data-ttu-id="5bfd1-116">"true"（默认值）</span><span class="sxs-lookup"><span data-stu-id="5bfd1-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="5bfd1-117">“false”</span><span class="sxs-lookup"><span data-stu-id="5bfd1-117">"false"</span></span>   |


<span data-ttu-id="5bfd1-118">确定是否缓存的缓存标记帮助程序括起来的内容。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="5bfd1-119">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-119">The default is `true`.</span></span>  <span data-ttu-id="5bfd1-120">如果设置为`false`此缓存标记帮助器将不起缓存上呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="5bfd1-121">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="5bfd1-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="5bfd1-122">expires-on</span></span> 

| <span data-ttu-id="5bfd1-123">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-123">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-124">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-124">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="5bfd1-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="5bfd1-125">DateTimeOffset</span></span>    | <span data-ttu-id="5bfd1-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-126">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="5bfd1-127">设置一个绝对过期日期。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="5bfd1-128">下面的示例将之前 2025 年 1 月 29，下午 5:02 缓存的缓存标记帮助程序中的内容。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="5bfd1-129">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="5bfd1-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="5bfd1-130">expires-after</span></span>

| <span data-ttu-id="5bfd1-131">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-131">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-132">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-132">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="5bfd1-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="5bfd1-133">TimeSpan</span></span>    | <span data-ttu-id="5bfd1-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-134">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="5bfd1-135">从缓存中的内容的第一个请求时间设置时间的长度。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="5bfd1-136">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="5bfd1-137">expires-sliding</span><span class="sxs-lookup"><span data-stu-id="5bfd1-137">expires-sliding</span></span>

| <span data-ttu-id="5bfd1-138">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-138">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-139">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-139">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="5bfd1-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="5bfd1-140">TimeSpan</span></span>    | <span data-ttu-id="5bfd1-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-141">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="5bfd1-142">设置应被逐出缓存项，如果未访问的时间。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="5bfd1-143">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="5bfd1-144">不同的标题</span><span class="sxs-lookup"><span data-stu-id="5bfd1-144">vary-by-header</span></span>

| <span data-ttu-id="5bfd1-145">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-145">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-146">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-147">String</span><span class="sxs-lookup"><span data-stu-id="5bfd1-147">String</span></span>            | <span data-ttu-id="5bfd1-148">"User-Agent"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="5bfd1-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="5bfd1-150">接受的单个标头值或在更改时触发缓存刷新的标头值的以逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="5bfd1-151">下面的示例监视标头值`User-Agent`。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="5bfd1-152">该示例将缓存的内容的每个不同`User-Agent`向 web 服务器显示。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="5bfd1-153">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="5bfd1-154">vary-by-query</span><span class="sxs-lookup"><span data-stu-id="5bfd1-154">vary-by-query</span></span>

| <span data-ttu-id="5bfd1-155">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-155">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-156">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-157">String</span><span class="sxs-lookup"><span data-stu-id="5bfd1-157">String</span></span>            | <span data-ttu-id="5bfd1-158">"使"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-158">"Make"</span></span>                |
|                   | <span data-ttu-id="5bfd1-159">"生成，模型"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-159">"Make,Model"</span></span> |

<span data-ttu-id="5bfd1-160">接受的单个标头值或以逗号分隔的标头值更改时触发缓存刷新的标头值的列表。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="5bfd1-161">下面的示例查找值`Make`和`Model`。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="5bfd1-162">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="5bfd1-163">vary-by-route</span><span class="sxs-lookup"><span data-stu-id="5bfd1-163">vary-by-route</span></span>

| <span data-ttu-id="5bfd1-164">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-164">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-165">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-166">String</span><span class="sxs-lookup"><span data-stu-id="5bfd1-166">String</span></span>            | <span data-ttu-id="5bfd1-167">"使"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-167">"Make"</span></span>                |
|                   | <span data-ttu-id="5bfd1-168">"生成，模型"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-168">"Make,Model"</span></span> |

<span data-ttu-id="5bfd1-169">接受的单个标头值或路由数据参数值更改时触发缓存刷新的标头值的以逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="5bfd1-170">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-170">Example:</span></span>

<span data-ttu-id="5bfd1-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="5bfd1-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="5bfd1-172">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="5bfd1-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="5bfd1-173">vary-by-cookie</span><span class="sxs-lookup"><span data-stu-id="5bfd1-173">vary-by-cookie</span></span>

| <span data-ttu-id="5bfd1-174">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-174">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-175">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-176">String</span><span class="sxs-lookup"><span data-stu-id="5bfd1-176">String</span></span>            | <span data-ttu-id="5bfd1-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="5bfd1-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="5bfd1-179">接受的单个标头值或在标头值 (s) 更改时触发缓存刷新的标头值的以逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="5bfd1-180">下面的示例查找在与 ASP.NET 标识关联的 cookie。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-180">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="5bfd1-181">用户进行身份验证时请求 cookie 设置随即将会触发缓存刷新。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="5bfd1-182">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="5bfd1-183">vary-by-user</span><span class="sxs-lookup"><span data-stu-id="5bfd1-183">vary-by-user</span></span>

| <span data-ttu-id="5bfd1-184">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-184">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-185">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-186">Boolean</span><span class="sxs-lookup"><span data-stu-id="5bfd1-186">Boolean</span></span>             | <span data-ttu-id="5bfd1-187">“true”</span><span class="sxs-lookup"><span data-stu-id="5bfd1-187">"true"</span></span>                  |
|                     | <span data-ttu-id="5bfd1-188">"false"（默认值）</span><span class="sxs-lookup"><span data-stu-id="5bfd1-188">"false" (default)</span></span> |

<span data-ttu-id="5bfd1-189">指定的登录的用户 （或上下文主体） 更改时，缓存应重置。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="5bfd1-190">当前用户是也称为请求上下文主体和可以在 Razor 视图中查看通过引用`@User.Identity.Name`。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="5bfd1-191">下面的示例查找在当前登录用户。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="5bfd1-192">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="5bfd1-193">使用此属性可保持缓存通过日志和日志打卡周期中的内容。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="5bfd1-194">使用时`vary-by-user="true"`，身份验证的用户的缓存失效的登录和注销操作。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="5bfd1-195">因为在登录时会生成新的唯一的 cookie 值，缓存会失效。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="5bfd1-196">在任何 cookie 或已过期时，缓存将保留匿名的状态。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="5bfd1-197">这意味着如果没有用户登录，将维护缓存。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="5bfd1-198">vary-by</span><span class="sxs-lookup"><span data-stu-id="5bfd1-198">vary-by</span></span>

| <span data-ttu-id="5bfd1-199">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-199">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-200">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-200">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-201">String</span><span class="sxs-lookup"><span data-stu-id="5bfd1-201">String</span></span>             | <span data-ttu-id="5bfd1-202">“@Model”</span><span class="sxs-lookup"><span data-stu-id="5bfd1-202">"@Model"</span></span>                 |


<span data-ttu-id="5bfd1-203">允许获取缓存哪些数据的自定义项。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="5bfd1-204">当更新属性的字符串值发生更改，缓存标记帮助器的内容所引用的对象。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="5bfd1-205">通常模型值字符串串联分配给此属性。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="5bfd1-206">实际上，这意味着对任何的串连值的更新令缓存失效。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="5bfd1-207">下面的示例假定呈现的两个的路由参数的整数值的视图和控制器方法`myParam1`和`myParam2`，并作为单个模型属性返回的。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="5bfd1-208">当此总和更改时，呈现和再次缓存的缓存标记帮助程序的内容。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="5bfd1-209">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-209">Example:</span></span>

<span data-ttu-id="5bfd1-210">操作：</span><span class="sxs-lookup"><span data-stu-id="5bfd1-210">Action:</span></span>

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

<span data-ttu-id="5bfd1-211">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="5bfd1-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="5bfd1-212">priority</span><span class="sxs-lookup"><span data-stu-id="5bfd1-212">priority</span></span>

| <span data-ttu-id="5bfd1-213">特性类型</span><span class="sxs-lookup"><span data-stu-id="5bfd1-213">Attribute Type</span></span>    | <span data-ttu-id="5bfd1-214">示例值</span><span class="sxs-lookup"><span data-stu-id="5bfd1-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="5bfd1-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="5bfd1-215">CacheItemPriority</span></span>  | <span data-ttu-id="5bfd1-216">"高"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-216">"High"</span></span>                   |
|                    | <span data-ttu-id="5bfd1-217">"低"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-217">"Low"</span></span> |
|                    | <span data-ttu-id="5bfd1-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="5bfd1-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="5bfd1-219">"Normal"</span></span> |

<span data-ttu-id="5bfd1-220">提供内置的缓存提供程序的缓存逐出指导。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="5bfd1-221">Web 服务器将逐出`Low`处于内存压力下时，第一次缓存条目。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="5bfd1-222">示例:</span><span class="sxs-lookup"><span data-stu-id="5bfd1-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="5bfd1-223">`priority`属性并不能保证特定级别的缓存保留。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-223">The `priority` attribute doesn't guarantee a specific level of cache retention.</span></span> <span data-ttu-id="5bfd1-224">`CacheItemPriority`是只是建议。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="5bfd1-225">此属性设置为`NeverRemove`并不能保证始终将保留缓存。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-225">Setting this attribute to `NeverRemove` doesn't guarantee that the cache will always be retained.</span></span> <span data-ttu-id="5bfd1-226">请参阅[其他资源](#additional-resources)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="5bfd1-227">缓存标记帮助程序是依赖于[内存缓存服务](xref:performance/caching/memory)。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="5bfd1-228">如果尚未添加，缓存标记帮助器将服务添加。</span><span class="sxs-lookup"><span data-stu-id="5bfd1-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bfd1-229">其他资源</span><span class="sxs-lookup"><span data-stu-id="5bfd1-229">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
