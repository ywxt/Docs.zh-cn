---
title: "ASP.NET Core 中的定位点标记帮助程序"
author: pkellner
description: "演示如何使用定位点标记帮助程序"
manager: wpickett
ms.author: riande
ms.date: 12/20/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 404fc7bc3b35114066f035e1ac28d10a8279ccbc
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="anchor-tag-helper"></a><span data-ttu-id="f9e72-103">定位点标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="f9e72-103">Anchor Tag Helper</span></span>

<span data-ttu-id="f9e72-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="f9e72-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="f9e72-105">定位点标记帮助程序可通过添加新属性来增强 HTML 定位点 (`<a ... ></a>`) 标记。</span><span class="sxs-lookup"><span data-stu-id="f9e72-105">The Anchor Tag Helper enhances the HTML anchor (`<a ... ></a>`) tag by adding new attributes.</span></span> <span data-ttu-id="f9e72-106">生成的链接（在 `href` 标记上）使用新属性创建。</span><span class="sxs-lookup"><span data-stu-id="f9e72-106">The link generated (on the `href` tag) is created using the new attributes.</span></span> <span data-ttu-id="f9e72-107">该 URL 可以包括可选协议（如 https）。</span><span class="sxs-lookup"><span data-stu-id="f9e72-107">That URL can include an optional protocol such as https.</span></span>

<span data-ttu-id="f9e72-108">本文档中的示例均以下面的发言人控制器为例。</span><span class="sxs-lookup"><span data-stu-id="f9e72-108">The speaker controller below is used in samples in this document.</span></span>

<span data-ttu-id="f9e72-109">**SpeakerController.cs**</span><span class="sxs-lookup"><span data-stu-id="f9e72-109">**SpeakerController.cs**</span></span> 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a><span data-ttu-id="f9e72-110">定位点标记帮助程序属性</span><span class="sxs-lookup"><span data-stu-id="f9e72-110">Anchor Tag Helper Attributes</span></span>

### <a name="asp-controller"></a><span data-ttu-id="f9e72-111">asp-controller</span><span class="sxs-lookup"><span data-stu-id="f9e72-111">asp-controller</span></span>

<span data-ttu-id="f9e72-112">`asp-controller` 用于关联将用于生成 URL 的控制器。</span><span class="sxs-lookup"><span data-stu-id="f9e72-112">`asp-controller` is used to associate which controller will be used to generate the URL.</span></span> <span data-ttu-id="f9e72-113">当前项目中必须存在指定的控制器。</span><span class="sxs-lookup"><span data-stu-id="f9e72-113">The controllers specified must exist in the current project.</span></span> <span data-ttu-id="f9e72-114">下面的代码列出了所有发言人：</span><span class="sxs-lookup"><span data-stu-id="f9e72-114">The following code lists all speakers:</span></span> 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

<span data-ttu-id="f9e72-115">生成的标记将为：</span><span class="sxs-lookup"><span data-stu-id="f9e72-115">The generated markup will be:</span></span>

```html
<a href="/Speaker">All Speakers</a>
```

<span data-ttu-id="f9e72-116">如果指定了 `asp-controller`，但未指定 `asp-action`，则默认的 `asp-action` 将为当前正在执行的视图的默认控制器方法。</span><span class="sxs-lookup"><span data-stu-id="f9e72-116">If the `asp-controller` is specified and `asp-action` isn't, the default `asp-action` will be the default controller method of the currently executing view.</span></span> <span data-ttu-id="f9e72-117">也就是说，在上面的示例中，如果忽略 `asp-action`，并且此定位点标记帮助程序从 *HomeController* 的 `Index` 视图 (**/Home**) 生成，则生成的标记将为：</span><span class="sxs-lookup"><span data-stu-id="f9e72-117">That is, in the above example, if `asp-action` is left out, and this Anchor Tag Helper is generated from *HomeController*'s `Index` view (**/Home**), the generated markup will be:</span></span>

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a><span data-ttu-id="f9e72-118">asp-action</span><span class="sxs-lookup"><span data-stu-id="f9e72-118">asp-action</span></span>

<span data-ttu-id="f9e72-119">`asp-action` 是要包含在生成的 `href` 中的控制器操作方法的名称。</span><span class="sxs-lookup"><span data-stu-id="f9e72-119">`asp-action` is the name of the action method in the controller that will be included in the generated `href`.</span></span> <span data-ttu-id="f9e72-120">例如，下面的代码将生成的 `href` 设置为指向发言人详细信息页面：</span><span class="sxs-lookup"><span data-stu-id="f9e72-120">For example, the following code set the generated `href` to point to the speaker detail page:</span></span>

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

<span data-ttu-id="f9e72-121">生成的标记将为：</span><span class="sxs-lookup"><span data-stu-id="f9e72-121">The generated markup will be:</span></span>

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

<span data-ttu-id="f9e72-122">如果未指定 `asp-controller` 属性，则使用默认控制器，该控制器调用执行当前视图的视图。</span><span class="sxs-lookup"><span data-stu-id="f9e72-122">If no `asp-controller` attribute is specified, the default controller calling the view executing the current view will be used.</span></span>  
 
<span data-ttu-id="f9e72-123">如果 `asp-action` 属性为 `Index`，则不向 URL 追加任何操作，从而导致调用默认的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="f9e72-123">If the attribute `asp-action` is `Index`, then no action is appended to the URL, leading to the default `Index` method being called.</span></span> <span data-ttu-id="f9e72-124">`asp-controller` 引用的控制器中必须存在指定的（或默认的）操作。</span><span class="sxs-lookup"><span data-stu-id="f9e72-124">The action specified (or defaulted), must exist in the controller referenced in `asp-controller`.</span></span>

### <a name="asp-page"></a><span data-ttu-id="f9e72-125">asp-page</span><span class="sxs-lookup"><span data-stu-id="f9e72-125">asp-page</span></span>

<span data-ttu-id="f9e72-126">使用定位点标记中的 `asp-page` 属性将其 URL 设置为指向特定页。</span><span class="sxs-lookup"><span data-stu-id="f9e72-126">Use the `asp-page` attribute in an anchor tag to set its URL to point to a specific page.</span></span> <span data-ttu-id="f9e72-127">通过在页面名称前面使用正斜杠“/”作为前缀，可创建 URL。</span><span class="sxs-lookup"><span data-stu-id="f9e72-127">Prefixing the page name with a forward slash "/" creates the URL.</span></span> <span data-ttu-id="f9e72-128">以下示例中的 URL 指向当前目录中的“发言人”页。</span><span class="sxs-lookup"><span data-stu-id="f9e72-128">The URL in the sample below points to the "Speaker" page in the current directory.</span></span>

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

<span data-ttu-id="f9e72-129">上一个代码示例中的 `asp-page` 属性在视图中呈现类似于以下代码片段的 HTML 输出：</span><span class="sxs-lookup"><span data-stu-id="f9e72-129">The `asp-page` attribute in the previous code sample renders HTML output in the view that's similar to the following snippet:</span></span>

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
```

<span data-ttu-id="f9e72-130">`asp-page` 属性与 `asp-route`、`asp-controller` 和 `asp-action` 属性互斥。</span><span class="sxs-lookup"><span data-stu-id="f9e72-130">The `asp-page` attribute is mutually exclusive with the `asp-route`, `asp-controller`, and `asp-action` attributes.</span></span> <span data-ttu-id="f9e72-131">但是，`asp-page` 可与 `asp-route-id` 结合使用以控制路由，如以下代码示例所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-131">However, `asp-page` can be used with `asp-route-id` to control routing, as the following code sample demonstrates:</span></span>

```cshtml
<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a>
```

<span data-ttu-id="f9e72-132">`asp-route-id` 生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="f9e72-132">The `asp-route-id` produces the following output:</span></span>

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```

> [!NOTE]
> <span data-ttu-id="f9e72-133">若要在 Razor 页面中使用 `asp-page` 属性，URL 必须为相对路径，例如 `"./Speaker"`。</span><span class="sxs-lookup"><span data-stu-id="f9e72-133">To use the `asp-page` attribute in Razor Pages, the URLs must be a relative path, for example `"./Speaker"`.</span></span> <span data-ttu-id="f9e72-134">`asp-page` 属性中的相对路径在 MVC 视图中不可用。</span><span class="sxs-lookup"><span data-stu-id="f9e72-134">Relative paths in the `asp-page` attribute are not available in MVC views.</span></span> <span data-ttu-id="f9e72-135">对 MVC 视图应改用“/”语法。</span><span class="sxs-lookup"><span data-stu-id="f9e72-135">Use the "/" syntax for MVC views instead.</span></span>

### <a name="asp-route-value"></a><span data-ttu-id="f9e72-136">asp-route-{value}</span><span class="sxs-lookup"><span data-stu-id="f9e72-136">asp-route-{value}</span></span>

<span data-ttu-id="f9e72-137">`asp-route-` 是一个通配符路由前缀。</span><span class="sxs-lookup"><span data-stu-id="f9e72-137">`asp-route-` is a wild card route prefix.</span></span> <span data-ttu-id="f9e72-138">放在尾部短划线后面的所有值都将解释为可能的路由参数。</span><span class="sxs-lookup"><span data-stu-id="f9e72-138">Any value you put after the trailing dash will be interpreted as a potential route parameter.</span></span> <span data-ttu-id="f9e72-139">如果找不到默认路由，则将此路由前缀作为请求参数和值追加到生成的 href。</span><span class="sxs-lookup"><span data-stu-id="f9e72-139">If a default route isn't found, this route prefix will be appended to the generated href as a request parameter and value.</span></span> <span data-ttu-id="f9e72-140">否则，将在路由模板中替换它。</span><span class="sxs-lookup"><span data-stu-id="f9e72-140">Otherwise it will be substituted in the route template.</span></span>

<span data-ttu-id="f9e72-141">假设定义了一个控制器方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-141">Assuming you have a controller method defined as follows:</span></span>

```csharp
public IActionResult AnchorTagHelper(string id)
{
    var speaker = new SpeakerData()
    {
        SpeakerId = 12
    };
    return View(viewName, speaker);
}
```

<span data-ttu-id="f9e72-142">并在 *Startup.cs* 中定义了默认路由模板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-142">And have the default route template defined in your *Startup.cs* as follows:</span></span>

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

<span data-ttu-id="f9e72-143">**cshtml** 文件包含定位点标记帮助程序，后者是在使用从控制器传递到视图的 **speaker** 模型参数时所必需的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-143">The **cshtml** file that contains the Anchor Tag Helper necessary to use the **speaker** model parameter passed in from the controller to the view is as follows:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="f9e72-144">则生成的 HTML 将如下所示，因为在默认路由中找到了 **id**。</span><span class="sxs-lookup"><span data-stu-id="f9e72-144">The generated HTML will then be as follows because **id** was found in the default route.</span></span>

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

<span data-ttu-id="f9e72-145">如果路由前缀不是已找到的路由模板的一部分，如以下 **cshtml** 文件中所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-145">If the route prefix isn't part of the routing template found, which is the case with the following **cshtml** file:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="f9e72-146">则生成的 HTML 将如下所示，因为在匹配的路由中找不到 **speakerid**：</span><span class="sxs-lookup"><span data-stu-id="f9e72-146">The generated HTML will then be as follows because **speakerid** wasn't found in the route matched:</span></span>

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

<span data-ttu-id="f9e72-147">如果 `asp-controller` 或 `asp-action` 均未指定，则会执行与 `asp-route` 属性中相同的默认处理。</span><span class="sxs-lookup"><span data-stu-id="f9e72-147">If either `asp-controller` or `asp-action` are not specified, then the same default processing is followed as is in the `asp-route` attribute.</span></span>

### <a name="asp-route"></a><span data-ttu-id="f9e72-148">asp-route</span><span class="sxs-lookup"><span data-stu-id="f9e72-148">asp-route</span></span>

<span data-ttu-id="f9e72-149">`asp-route` 可用于创建直接链接到命名路由的 URL。</span><span class="sxs-lookup"><span data-stu-id="f9e72-149">`asp-route` provides a way to create a URL that links directly to a named route.</span></span> <span data-ttu-id="f9e72-150">使用路由属性，路由可以按 `SpeakerController` 中所示进行命名并用于其 `Evaluations` 方法。</span><span class="sxs-lookup"><span data-stu-id="f9e72-150">Using routing attributes, a route can be named as shown in the `SpeakerController` and used in its `Evaluations` method.</span></span>

<span data-ttu-id="f9e72-151">`Name = "speakerevals"` 指示定位点标记帮助程序使用 URL `/Speaker/Evaluations`生成直接指向该控制器方法的路由。</span><span class="sxs-lookup"><span data-stu-id="f9e72-151">`Name = "speakerevals"` tells the Anchor Tag Helper to generate a route directly to that controller method using the URL `/Speaker/Evaluations`.</span></span> <span data-ttu-id="f9e72-152">如果除了 `asp-route`，还指定了 `asp-controller` 或 `asp-action`，则可能不会生成预期的路由。</span><span class="sxs-lookup"><span data-stu-id="f9e72-152">If `asp-controller` or `asp-action` is specified in addition to `asp-route`, the route generated may not be what you expect.</span></span> <span data-ttu-id="f9e72-153">不能将 `asp-route` 与 `asp-controller` 或 `asp-action` 属性结合使用，以免发生路由冲突。</span><span class="sxs-lookup"><span data-stu-id="f9e72-153">`asp-route` shouldn't be used with either of the attributes `asp-controller` or `asp-action` to avoid a route conflict.</span></span>

### <a name="asp-all-route-data"></a><span data-ttu-id="f9e72-154">asp-all-route-data</span><span class="sxs-lookup"><span data-stu-id="f9e72-154">asp-all-route-data</span></span>

<span data-ttu-id="f9e72-155">`asp-all-route-data` 允许创建键值对字典，其中，键是参数名称，值是与该键关联的值。</span><span class="sxs-lookup"><span data-stu-id="f9e72-155">`asp-all-route-data` allows creating a dictionary of key value pairs where the key is the parameter name and the value is the value associated with that key.</span></span>

<span data-ttu-id="f9e72-156">如以下示例所示，创建一个内联字典并将数据传递到 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="f9e72-156">As the example below shows, an inline dictionary is created and the data is passed to the razor view.</span></span> <span data-ttu-id="f9e72-157">作为替代方法，也可以使用模型传递数据。</span><span class="sxs-lookup"><span data-stu-id="f9e72-157">As an alternative, the data could also be passed in with your model.</span></span>

```cshtml
@{
    var dict =
        new Dictionary<string, string>
        {
            {"speakerId", "11"},
            {"currentYear", "true"}
        };
}
<a asp-route="speakerevalscurrent"
asp-all-route-data="dict">SpeakerEvals</a>
```

<span data-ttu-id="f9e72-158">以上代码生成以下 URL：http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true</span><span class="sxs-lookup"><span data-stu-id="f9e72-158">The code above generates the following URL: http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true</span></span>

<span data-ttu-id="f9e72-159">单击该链接时，会调用控制器方法 `EvaluationsCurrent`。</span><span class="sxs-lookup"><span data-stu-id="f9e72-159">When the link is clicked, the controller method `EvaluationsCurrent` is called.</span></span> <span data-ttu-id="f9e72-160">之所以调用它是因为该控制器具有两个字符串参数，它们与从 `asp-all-route-data` 字典创建的键匹配。</span><span class="sxs-lookup"><span data-stu-id="f9e72-160">It's called because that controller has two string parameters that match what has been created from the `asp-all-route-data` dictionary.</span></span>

<span data-ttu-id="f9e72-161">如果字典中的任意键与路由参数匹配，则将在路由中相应地替换这些值，其他不匹配的值则生成为请求参数。</span><span class="sxs-lookup"><span data-stu-id="f9e72-161">If any keys in the dictionary match route parameters, those values will be substituted in the route as appropriate and the other non-matching values will be generated as request parameters.</span></span>

### <a name="asp-fragment"></a><span data-ttu-id="f9e72-162">asp-fragment</span><span class="sxs-lookup"><span data-stu-id="f9e72-162">asp-fragment</span></span>

<span data-ttu-id="f9e72-163">`asp-fragment` 定义要追加到 URL 的 URL 片段。</span><span class="sxs-lookup"><span data-stu-id="f9e72-163">`asp-fragment` defines a URL fragment to append to the URL.</span></span> <span data-ttu-id="f9e72-164">定位点标记帮助程序将添加哈希字符 (#)。</span><span class="sxs-lookup"><span data-stu-id="f9e72-164">The Anchor Tag Helper will add the hash character (#).</span></span> <span data-ttu-id="f9e72-165">如果创建标记：</span><span class="sxs-lookup"><span data-stu-id="f9e72-165">If you create a tag:</span></span>

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

<span data-ttu-id="f9e72-166">生成的 URL 将为：http://localhost/Speaker/Evaluations#SpeakerEvaluations</span><span class="sxs-lookup"><span data-stu-id="f9e72-166">The generated URL will be: http://localhost/Speaker/Evaluations#SpeakerEvaluations</span></span>

<span data-ttu-id="f9e72-167">生成客户端应用程序时，哈希标记很有用。</span><span class="sxs-lookup"><span data-stu-id="f9e72-167">Hash tags are useful when building client-side applications.</span></span> <span data-ttu-id="f9e72-168">它们可用于在 JavaScript 中轻松地执行标记和搜索等操作。</span><span class="sxs-lookup"><span data-stu-id="f9e72-168">They can be used for easy marking and searching in JavaScript, for example.</span></span>

### <a name="asp-area"></a><span data-ttu-id="f9e72-169">asp-area</span><span class="sxs-lookup"><span data-stu-id="f9e72-169">asp-area</span></span>

<span data-ttu-id="f9e72-170">`asp-area` 设置区域名称，ASP.NET Core 使用该名称设置适当的路由。</span><span class="sxs-lookup"><span data-stu-id="f9e72-170">`asp-area` sets the area name that ASP.NET Core uses to set the appropriate route.</span></span> <span data-ttu-id="f9e72-171">以下示例展示了区域属性如何导致重新映射路由。</span><span class="sxs-lookup"><span data-stu-id="f9e72-171">Below are examples of how the area attribute causes a remapping of routes.</span></span> <span data-ttu-id="f9e72-172">如果将 `asp-area` 设置为 Blogs，则会为此定位点标记的关联控制器和视图的路由添加目录 `Areas/Blogs` 作为前缀。</span><span class="sxs-lookup"><span data-stu-id="f9e72-172">Setting `asp-area` to Blogs prefixes the directory `Areas/Blogs` to the routes of the associated controllers and views for this anchor tag.</span></span>

* <span data-ttu-id="f9e72-173">项目名称</span><span class="sxs-lookup"><span data-stu-id="f9e72-173">Project name</span></span>
  * <span data-ttu-id="f9e72-174">wwwroot</span><span class="sxs-lookup"><span data-stu-id="f9e72-174">wwwroot</span></span>
  * <span data-ttu-id="f9e72-175">区域</span><span class="sxs-lookup"><span data-stu-id="f9e72-175">Areas</span></span>
    * <span data-ttu-id="f9e72-176">博客</span><span class="sxs-lookup"><span data-stu-id="f9e72-176">Blogs</span></span>
      * <span data-ttu-id="f9e72-177">Controllers</span><span class="sxs-lookup"><span data-stu-id="f9e72-177">Controllers</span></span>
        * <span data-ttu-id="f9e72-178">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="f9e72-178">HomeController.cs</span></span>
      * <span data-ttu-id="f9e72-179">视图</span><span class="sxs-lookup"><span data-stu-id="f9e72-179">Views</span></span>
        * <span data-ttu-id="f9e72-180">主页</span><span class="sxs-lookup"><span data-stu-id="f9e72-180">Home</span></span>
          * <span data-ttu-id="f9e72-181">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="f9e72-181">Index.cshtml</span></span>
          * <span data-ttu-id="f9e72-182">AboutBlog.cshtml</span><span class="sxs-lookup"><span data-stu-id="f9e72-182">AboutBlog.cshtml</span></span>
  * <span data-ttu-id="f9e72-183">Controllers</span><span class="sxs-lookup"><span data-stu-id="f9e72-183">Controllers</span></span>

<span data-ttu-id="f9e72-184">使用定位点标记帮助程序指定一个有效的区域标记（比如，引用 ```AboutBlog.cshtml``` 文件时使用的 ```area="Blogs"```），如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9e72-184">Specifying an area tag that's valid, such as ```area="Blogs"``` when referencing the ```AboutBlog.cshtml``` file will look like the following using the Anchor Tag Helper.</span></span>

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

<span data-ttu-id="f9e72-185">生成的 HTML 将包括区域段，并将如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-185">The generated HTML will include the areas segment and will be as follows:</span></span>

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> <span data-ttu-id="f9e72-186">若要使 MVC 区域在 Web 应用程序中正常工作，路由模板必须包含对该区域（如果存在）的引用。</span><span class="sxs-lookup"><span data-stu-id="f9e72-186">For MVC areas to work in a web application, the route template must include a reference to the area if it exists.</span></span> <span data-ttu-id="f9e72-187">该模板（`routes.MapRoute` 方法调用的第二个参数）将显示为：`template: '"{area:exists}/{controller=Home}/{action=Index}"'`</span><span class="sxs-lookup"><span data-stu-id="f9e72-187">That template, which is the second parameter of the `routes.MapRoute` method call, will appear as: `template: '"{area:exists}/{controller=Home}/{action=Index}"'`</span></span>

### <a name="asp-protocol"></a><span data-ttu-id="f9e72-188">asp-protocol</span><span class="sxs-lookup"><span data-stu-id="f9e72-188">asp-protocol</span></span>

<span data-ttu-id="f9e72-189">`asp-protocol` 用于在 URL 中指定协议（比如 `https`）。</span><span class="sxs-lookup"><span data-stu-id="f9e72-189">The `asp-protocol` is for specifying a protocol (such as `https`) in your URL.</span></span> <span data-ttu-id="f9e72-190">包含协议的定位点标记帮助程序示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9e72-190">An example Anchor Tag Helper that includes the protocol will look as follows:</span></span>

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

<span data-ttu-id="f9e72-191">将生成如下所示的 HTML：</span><span class="sxs-lookup"><span data-stu-id="f9e72-191">and will generate HTML as follows:</span></span>

```<a href="https://localhost/Home/About">About</a>```

<span data-ttu-id="f9e72-192">示例中的域为 localhost，但在生成 URL 时，定位点标记帮助程序会使用网站的公共域。</span><span class="sxs-lookup"><span data-stu-id="f9e72-192">The domain in the example is localhost, but the Anchor Tag Helper uses the website's public domain when generating the URL.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9e72-193">其他资源</span><span class="sxs-lookup"><span data-stu-id="f9e72-193">Additional resources</span></span>

* [<span data-ttu-id="f9e72-194">区域</span><span class="sxs-lookup"><span data-stu-id="f9e72-194">Areas</span></span>](xref:mvc/controllers/areas)
