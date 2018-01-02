---
title: "定位点标记帮助器 |Microsoft 文档"
author: pkellner
description: "演示如何使用定位点标记帮助器"
keywords: "ASP.NET Core, 标记帮助程序"
ms.author: riande
manager: wpickett
ms.date: 12/20/2017
ms.topic: article
ms.assetid: c045d485-d1dc-4cea-a675-46be83b7a011
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 503ad7c4ce8c4f08b2a06dbe9f985566f54d3ca2
ms.sourcegitcommit: 44a62f59d4db39d685c4487a0345a486be18d7c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="anchor-tag-helper"></a><span data-ttu-id="1d6b2-104">定位点标记帮助器</span><span class="sxs-lookup"><span data-stu-id="1d6b2-104">Anchor Tag Helper</span></span>

<span data-ttu-id="1d6b2-105">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="1d6b2-105">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="1d6b2-106">定位点标记帮助程序增强了 HTML 定位点 (`<a ... ></a>`) 通过添加新属性的标记。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-106">The Anchor Tag Helper enhances the HTML anchor (`<a ... ></a>`) tag by adding new attributes.</span></span> <span data-ttu-id="1d6b2-107">生成的链接 (上`href`标记) 创建使用新的属性。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-107">The link generated (on the `href` tag) is created using the new attributes.</span></span> <span data-ttu-id="1d6b2-108">该 URL 可以包括可选的协议 （如 https)。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-108">That URL can include an optional protocol such as https.</span></span>

<span data-ttu-id="1d6b2-109">下面的扬声器控制器是本文档中的示例中使用。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-109">The speaker controller below is used in samples in this document.</span></span>

<span data-ttu-id="1d6b2-110">**SpeakerController.cs**</span><span class="sxs-lookup"><span data-stu-id="1d6b2-110">**SpeakerController.cs**</span></span> 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a><span data-ttu-id="1d6b2-111">定位点标记帮助器属性</span><span class="sxs-lookup"><span data-stu-id="1d6b2-111">Anchor Tag Helper Attributes</span></span>

### <a name="asp-controller"></a><span data-ttu-id="1d6b2-112">asp 控制器</span><span class="sxs-lookup"><span data-stu-id="1d6b2-112">asp-controller</span></span>

<span data-ttu-id="1d6b2-113">`asp-controller`用于将相关联的控制器将用于生成 URL。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-113">`asp-controller` is used to associate which controller will be used to generate the URL.</span></span> <span data-ttu-id="1d6b2-114">指定的控制器必须存在于当前项目。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-114">The controllers specified must exist in the current project.</span></span> <span data-ttu-id="1d6b2-115">下面的代码列出所有发言人：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-115">The following code lists all speakers:</span></span> 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

<span data-ttu-id="1d6b2-116">将生成的标记：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-116">The generated markup will be:</span></span>

```html
<a href="/Speaker">All Speakers</a>
```

<span data-ttu-id="1d6b2-117">如果`asp-controller`指定和`asp-action`不是默认`asp-action`将当前正在执行的视图的默认控制器方法。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-117">If the `asp-controller` is specified and `asp-action` is not, the default `asp-action` will be the default controller method of the currently executing view.</span></span> <span data-ttu-id="1d6b2-118">即，在上面的示例中，如果`asp-action`留出，和从生成此定位点标记帮助器*HomeController*的`Index`视图 (**/主页**)，将生成的标记：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-118">That is, in the above example, if `asp-action` is left out, and this Anchor Tag Helper is generated from *HomeController*'s `Index` view (**/Home**), the generated markup will be:</span></span>

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a><span data-ttu-id="1d6b2-119">asp 操作</span><span class="sxs-lookup"><span data-stu-id="1d6b2-119">asp-action</span></span>

<span data-ttu-id="1d6b2-120">`asp-action`是将包含控制器中的操作方法的名称在生成`href`。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-120">`asp-action` is the name of the action method in the controller that will be included in the generated `href`.</span></span> <span data-ttu-id="1d6b2-121">例如，下面的代码将设置生成`href`以指向扬声器详细信息页：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-121">For example, the following code set the generated `href` to point to the speaker detail page:</span></span>

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

<span data-ttu-id="1d6b2-122">将生成的标记：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-122">The generated markup will be:</span></span>

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

<span data-ttu-id="1d6b2-123">如果没有`asp-controller`指定特性时，将使用默认控制器调用执行当前视图的视图。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-123">If no `asp-controller` attribute is specified, the default controller calling the view executing the current view will be used.</span></span>  
 
<span data-ttu-id="1d6b2-124">如果该属性`asp-action`是`Index`，则任何操作不追加到的 URL，从而导致默认`Index`所调用方法。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-124">If the attribute `asp-action` is `Index`, then no action is appended to the URL, leading to the default `Index` method being called.</span></span> <span data-ttu-id="1d6b2-125">指定的操作 （或默认），必须存在于中引用的控制器`asp-controller`。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-125">The action specified (or defaulted), must exist in the controller referenced in `asp-controller`.</span></span>

### <a name="asp-page"></a><span data-ttu-id="1d6b2-126">asp 页面</span><span class="sxs-lookup"><span data-stu-id="1d6b2-126">asp-page</span></span>

<span data-ttu-id="1d6b2-127">使用`asp-page`中的定位点标记，若要设置其 URL 为指向特定页属性。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-127">Use the `asp-page` attribute in an anchor tag to set its URL to point to a specific page.</span></span> <span data-ttu-id="1d6b2-128">前缀的页名称以正斜杠"/"创建 URL。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-128">Prefixing the page name with a forward slash "/" creates the URL.</span></span> <span data-ttu-id="1d6b2-129">下面的示例中的 URL 指向的当前目录中的"发言人"页。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-129">The URL in the sample below points to the "Speaker" page in the current directory.</span></span>

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

<span data-ttu-id="1d6b2-130">`asp-page`中前面的代码示例属性呈现在类似于下面的代码段的视图中的 HTML 输出：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-130">The `asp-page` attribute in the previous code sample renders HTML output in the view that is similar to the following snippet:</span></span>

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
``

The `asp-page` attribute is mutually exclusive with the `asp-route`, `asp-controller`, and `asp-action` attributes. However, `asp-page` can be used with `asp-route-id` to control routing, as the following code sample demonstrates:

```
<span data-ttu-id="1d6b2-131">cshtml<a asp-page="/Speaker" asp-route-id="@speaker.Id">视图扬声器</a></span><span class="sxs-lookup"><span data-stu-id="1d6b2-131">cshtml<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a></span></span>
```

The `asp-route-id` produces the following output:

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```


### <a name="asp-route-value"></a><span data-ttu-id="1d6b2-132">asp 的路由的 {value}</span><span class="sxs-lookup"><span data-stu-id="1d6b2-132">asp-route-{value}</span></span>

<span data-ttu-id="1d6b2-133">`asp-route-`是一个通配符路由前缀。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-133">`asp-route-` is a wild card route prefix.</span></span> <span data-ttu-id="1d6b2-134">任何 put 后尾随 dash 将解释为潜在的路由参数值。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-134">Any value you put after the trailing dash will be interpreted as a potential route parameter.</span></span> <span data-ttu-id="1d6b2-135">如果未找到默认路由，则此路由前缀将追加到为请求参数和值生成的 href。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-135">If a default route is not found, this route prefix will be appended to the generated href as a request parameter and value.</span></span> <span data-ttu-id="1d6b2-136">否则它将在路由模板中进行替换。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-136">Otherwise it will be substituted in the route template.</span></span>

<span data-ttu-id="1d6b2-137">假设您有一个控制器方法定义，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-137">Assuming you have a controller method defined as follows:</span></span>

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

<span data-ttu-id="1d6b2-138">并且具有默认路由模板中定义你*Startup.cs* ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-138">And have the default route template defined in your *Startup.cs* as follows:</span></span>

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

<span data-ttu-id="1d6b2-139">**Cshtml**文件，其中包含有必要将使用定位点标记帮助器**扬声器**从控制器中传递到视图的模型参数是，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-139">The **cshtml** file that contains the Anchor Tag Helper necessary to use the **speaker** model parameter passed in from the controller to the view is as follows:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="1d6b2-140">生成的 HTML 将然后是，如下所示，因为**id**位于默认路由。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-140">The generated HTML will then be as follows because **id** was found in the default route.</span></span>

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

<span data-ttu-id="1d6b2-141">如果路由前缀不找到路由模板的一部分，这是替换为以下这种情况**cshtml**文件：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-141">If the route prefix is not part of the routing template found, which is the case with the following **cshtml** file:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="1d6b2-142">生成的 HTML 将然后是，如下所示，因为**speakerid**匹配的路由中未找到：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-142">The generated HTML will then be as follows because **speakerid** was not found in the route matched:</span></span>

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

<span data-ttu-id="1d6b2-143">如果任一`asp-controller`或`asp-action`未指定，则相同的默认处理后面，如在`asp-route`属性。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-143">If either `asp-controller` or `asp-action` are not specified, then the same default processing is followed as is in the `asp-route` attribute.</span></span>

### <a name="asp-route"></a><span data-ttu-id="1d6b2-144">asp 路由</span><span class="sxs-lookup"><span data-stu-id="1d6b2-144">asp-route</span></span>

<span data-ttu-id="1d6b2-145">`asp-route`使您能够创建链接直接到命名路由的 URL。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-145">`asp-route` provides a way to create a URL that links directly to a named route.</span></span> <span data-ttu-id="1d6b2-146">使用路由特性，路由可以命名为中所示`SpeakerController`和中使用其`Evaluations`方法。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-146">Using routing attributes, a route can be named as shown in the `SpeakerController` and used in its `Evaluations` method.</span></span>

<span data-ttu-id="1d6b2-147">`Name = "speakerevals"`告知定位点标记帮助器以生成直接指向该控制器方法使用的 URL 的路由`/Speaker/Evaluations`。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-147">`Name = "speakerevals"` tells the Anchor Tag Helper to generate a route directly to that controller method using the URL `/Speaker/Evaluations`.</span></span> <span data-ttu-id="1d6b2-148">如果`asp-controller`或`asp-action`指定除了`asp-route`，生成的路由可能不是你的预期。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-148">If `asp-controller` or `asp-action` is specified in addition to `asp-route`, the route generated may not be what you expect.</span></span> <span data-ttu-id="1d6b2-149">`asp-route`不应与属性任一使用`asp-controller`或`asp-action`以避免路由冲突。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-149">`asp-route` should not be used with either of the attributes `asp-controller` or `asp-action` to avoid a route conflict.</span></span>

### <a name="asp-all-route-data"></a><span data-ttu-id="1d6b2-150">asp 所有路线数据</span><span class="sxs-lookup"><span data-stu-id="1d6b2-150">asp-all-route-data</span></span>

<span data-ttu-id="1d6b2-151">`asp-all-route-data`可以创建的字典的键/值对，其中键是参数名称，值是与该项关联的值。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-151">`asp-all-route-data` allows creating a dictionary of key value pairs where the key is the parameter name and the value is the value associated with that key.</span></span>

<span data-ttu-id="1d6b2-152">如以下示例所示，创建一个内联字典和数据传递到 razor 视图。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-152">As the example below shows, an inline dictionary is created and the data is passed to the razor view.</span></span> <span data-ttu-id="1d6b2-153">作为替代方法，还可以使用您的模型传递数据。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-153">As an alternative, the data could also be passed in with your model.</span></span>

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

<span data-ttu-id="1d6b2-154">上面的代码生成以下 URL: http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true</span><span class="sxs-lookup"><span data-stu-id="1d6b2-154">The code above generates the following URL: http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true</span></span>

<span data-ttu-id="1d6b2-155">单击该链接后，控制器方法`EvaluationsCurrent`调用。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-155">When the link is clicked, the controller method `EvaluationsCurrent` is called.</span></span> <span data-ttu-id="1d6b2-156">因为该控制器具有匹配什么从已创建的两个字符串参数调用`asp-all-route-data`字典。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-156">It is called because that controller has two string parameters that match what has been created from the `asp-all-route-data` dictionary.</span></span>

<span data-ttu-id="1d6b2-157">如果字典匹配项中的任何密钥传送参数，这些值将替换为相应的路由中和其他的不匹配的值会转换为请求参数。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-157">If any keys in the dictionary match route parameters, those values will be substituted in the route as appropriate and the other non-matching values will be generated as request parameters.</span></span>

### <a name="asp-fragment"></a><span data-ttu-id="1d6b2-158">asp 片段</span><span class="sxs-lookup"><span data-stu-id="1d6b2-158">asp-fragment</span></span>

<span data-ttu-id="1d6b2-159">`asp-fragment`定义要追加到 URL 的 URL 片段。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-159">`asp-fragment` defines a URL fragment to append to the URL.</span></span> <span data-ttu-id="1d6b2-160">定位点标记帮助程序将添加的哈希字符 （#）。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-160">The Anchor Tag Helper will add the hash character (#).</span></span> <span data-ttu-id="1d6b2-161">如果要创建一个标记：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-161">If you create a tag:</span></span>

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

<span data-ttu-id="1d6b2-162">生成的 URL 将是： http://localhost/Speaker/Evaluations#SpeakerEvaluations</span><span class="sxs-lookup"><span data-stu-id="1d6b2-162">The generated URL will be: http://localhost/Speaker/Evaluations#SpeakerEvaluations</span></span>

<span data-ttu-id="1d6b2-163">构建客户端应用程序时，哈希标记很有用。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-163">Hash tags are useful when building client-side applications.</span></span> <span data-ttu-id="1d6b2-164">它们可用于轻松的标记和在 JavaScript 中，例如搜索。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-164">They can be used for easy marking and searching in JavaScript, for example.</span></span>

### <a name="asp-area"></a><span data-ttu-id="1d6b2-165">asp 区域</span><span class="sxs-lookup"><span data-stu-id="1d6b2-165">asp-area</span></span>

<span data-ttu-id="1d6b2-166">`asp-area`设置 ASP.NET Core 使用设置适当的路由的区域名称。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-166">`asp-area` sets the area name that ASP.NET Core uses to set the appropriate route.</span></span> <span data-ttu-id="1d6b2-167">下面是如何区域属性将导致重新路由映射的示例。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-167">Below are examples of how the area attribute causes a remapping of routes.</span></span> <span data-ttu-id="1d6b2-168">设置`asp-area`博客前缀目录`Areas/Blogs`到关联的控制器和视图此定位点标记的路由。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-168">Setting `asp-area` to Blogs prefixes the directory `Areas/Blogs` to the routes of the associated controllers and views for this anchor tag.</span></span>

* <span data-ttu-id="1d6b2-169">项目名称</span><span class="sxs-lookup"><span data-stu-id="1d6b2-169">Project name</span></span>
  * <span data-ttu-id="1d6b2-170">wwwroot</span><span class="sxs-lookup"><span data-stu-id="1d6b2-170">wwwroot</span></span>
  * <span data-ttu-id="1d6b2-171">区域</span><span class="sxs-lookup"><span data-stu-id="1d6b2-171">Areas</span></span>
    * <span data-ttu-id="1d6b2-172">博客</span><span class="sxs-lookup"><span data-stu-id="1d6b2-172">Blogs</span></span>
      * <span data-ttu-id="1d6b2-173">控制器</span><span class="sxs-lookup"><span data-stu-id="1d6b2-173">Controllers</span></span>
        * <span data-ttu-id="1d6b2-174">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="1d6b2-174">HomeController.cs</span></span>
      * <span data-ttu-id="1d6b2-175">视图</span><span class="sxs-lookup"><span data-stu-id="1d6b2-175">Views</span></span>
        * <span data-ttu-id="1d6b2-176">主页</span><span class="sxs-lookup"><span data-stu-id="1d6b2-176">Home</span></span>
          * <span data-ttu-id="1d6b2-177">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="1d6b2-177">Index.cshtml</span></span>
          * <span data-ttu-id="1d6b2-178">AboutBlog.cshtml</span><span class="sxs-lookup"><span data-stu-id="1d6b2-178">AboutBlog.cshtml</span></span>
  * <span data-ttu-id="1d6b2-179">控制器</span><span class="sxs-lookup"><span data-stu-id="1d6b2-179">Controllers</span></span>

<span data-ttu-id="1d6b2-180">指定一个区域标记，它是有效的如```area="Blogs"```引用时```AboutBlog.cshtml```文件将如下所示使用定位点标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-180">Specifying an area tag that is valid, such as ```area="Blogs"``` when referencing the ```AboutBlog.cshtml``` file will look like the following using the Anchor Tag Helper.</span></span>

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

<span data-ttu-id="1d6b2-181">生成的 HTML 将包括区域段，并将如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-181">The generated HTML will include the areas segment and will be as follows:</span></span>

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> <span data-ttu-id="1d6b2-182">Web 应用程序中的工作的 MVC 区域，路由模板必须包括如果它存在到区域的引用。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-182">For MVC areas to work in a web application, the route template must include a reference to the area if it exists.</span></span> <span data-ttu-id="1d6b2-183">该模板，这是第二个参数的`routes.MapRoute`方法调用中，将显示为：`template: '"{area:exists}/{controller=Home}/{action=Index}"'`</span><span class="sxs-lookup"><span data-stu-id="1d6b2-183">That template, which is the second parameter of the `routes.MapRoute` method call, will appear as: `template: '"{area:exists}/{controller=Home}/{action=Index}"'`</span></span>

### <a name="asp-protocol"></a><span data-ttu-id="1d6b2-184">asp 协议</span><span class="sxs-lookup"><span data-stu-id="1d6b2-184">asp-protocol</span></span>

<span data-ttu-id="1d6b2-185">`asp-protocol`可用于指定一种协议 (如`https`) 在你的 URL。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-185">The `asp-protocol` is for specifying a protocol (such as `https`) in your URL.</span></span> <span data-ttu-id="1d6b2-186">示例包括协议的定位点标记帮助器将如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-186">An example Anchor Tag Helper that includes the protocol will look as follows:</span></span>

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

<span data-ttu-id="1d6b2-187">并将生成 HTML，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d6b2-187">and will generate HTML as follows:</span></span>

```<a href="https://localhost/Home/About">About</a>```

<span data-ttu-id="1d6b2-188">在示例中的域是 localhost，但定位点标记帮助程序生成 URL 时使用网站的公共域。</span><span class="sxs-lookup"><span data-stu-id="1d6b2-188">The domain in the example is localhost, but the Anchor Tag Helper uses the website's public domain when generating the URL.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d6b2-189">其他资源</span><span class="sxs-lookup"><span data-stu-id="1d6b2-189">Additional resources</span></span>

* [<span data-ttu-id="1d6b2-190">区域</span><span class="sxs-lookup"><span data-stu-id="1d6b2-190">Areas</span></span>](xref:mvc/controllers/areas)
