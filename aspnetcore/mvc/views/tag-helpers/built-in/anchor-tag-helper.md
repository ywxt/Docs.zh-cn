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
# <a name="anchor-tag-helper"></a>定位点标记帮助程序

作者：[Peter Kellner](http://peterkellner.net) 

定位点标记帮助程序可通过添加新属性来增强 HTML 定位点 (`<a ... ></a>`) 标记。 生成的链接（在 `href` 标记上）使用新属性创建。 该 URL 可以包括可选协议（如 https）。

本文档中的示例均以下面的发言人控制器为例。

**SpeakerController.cs** 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a>定位点标记帮助程序属性

### <a name="asp-controller"></a>asp-controller

`asp-controller` 用于关联将用于生成 URL 的控制器。 当前项目中必须存在指定的控制器。 下面的代码列出了所有发言人： 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

生成的标记将为：

```html
<a href="/Speaker">All Speakers</a>
```

如果指定了 `asp-controller`，但未指定 `asp-action`，则默认的 `asp-action` 将为当前正在执行的视图的默认控制器方法。 也就是说，在上面的示例中，如果忽略 `asp-action`，并且此定位点标记帮助程序从 *HomeController* 的 `Index` 视图 (**/Home**) 生成，则生成的标记将为：

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a>asp-action

`asp-action` 是要包含在生成的 `href` 中的控制器操作方法的名称。 例如，下面的代码将生成的 `href` 设置为指向发言人详细信息页面：

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

生成的标记将为：

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

如果未指定 `asp-controller` 属性，则使用默认控制器，该控制器调用执行当前视图的视图。  
 
如果 `asp-action` 属性为 `Index`，则不向 URL 追加任何操作，从而导致调用默认的 `Index` 方法。 `asp-controller` 引用的控制器中必须存在指定的（或默认的）操作。

### <a name="asp-page"></a>asp-page

使用定位点标记中的 `asp-page` 属性将其 URL 设置为指向特定页。 通过在页面名称前面使用正斜杠“/”作为前缀，可创建 URL。 以下示例中的 URL 指向当前目录中的“发言人”页。

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

上一个代码示例中的 `asp-page` 属性在视图中呈现类似于以下代码片段的 HTML 输出：

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
```

`asp-page` 属性与 `asp-route`、`asp-controller` 和 `asp-action` 属性互斥。 但是，`asp-page` 可与 `asp-route-id` 结合使用以控制路由，如以下代码示例所示：

```cshtml
<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a>
```

`asp-route-id` 生成以下输出：

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```

> [!NOTE]
> 若要在 Razor 页面中使用 `asp-page` 属性，URL 必须为相对路径，例如 `"./Speaker"`。 `asp-page` 属性中的相对路径在 MVC 视图中不可用。 对 MVC 视图应改用“/”语法。

### <a name="asp-route-value"></a>asp-route-{value}

`asp-route-` 是一个通配符路由前缀。 放在尾部短划线后面的所有值都将解释为可能的路由参数。 如果找不到默认路由，则将此路由前缀作为请求参数和值追加到生成的 href。 否则，将在路由模板中替换它。

假设定义了一个控制器方法，如下所示：

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

并在 *Startup.cs* 中定义了默认路由模板，如下所示：

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

**cshtml** 文件包含定位点标记帮助程序，后者是在使用从控制器传递到视图的 **speaker** 模型参数时所必需的，如下所示：

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

则生成的 HTML 将如下所示，因为在默认路由中找到了 **id**。

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

如果路由前缀不是已找到的路由模板的一部分，如以下 **cshtml** 文件中所示：

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

则生成的 HTML 将如下所示，因为在匹配的路由中找不到 **speakerid**：

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

如果 `asp-controller` 或 `asp-action` 均未指定，则会执行与 `asp-route` 属性中相同的默认处理。

### <a name="asp-route"></a>asp-route

`asp-route` 可用于创建直接链接到命名路由的 URL。 使用路由属性，路由可以按 `SpeakerController` 中所示进行命名并用于其 `Evaluations` 方法。

`Name = "speakerevals"` 指示定位点标记帮助程序使用 URL `/Speaker/Evaluations`生成直接指向该控制器方法的路由。 如果除了 `asp-route`，还指定了 `asp-controller` 或 `asp-action`，则可能不会生成预期的路由。 不能将 `asp-route` 与 `asp-controller` 或 `asp-action` 属性结合使用，以免发生路由冲突。

### <a name="asp-all-route-data"></a>asp-all-route-data

`asp-all-route-data` 允许创建键值对字典，其中，键是参数名称，值是与该键关联的值。

如以下示例所示，创建一个内联字典并将数据传递到 Razor 视图。 作为替代方法，也可以使用模型传递数据。

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

以上代码生成以下 URL：http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true

单击该链接时，会调用控制器方法 `EvaluationsCurrent`。 之所以调用它是因为该控制器具有两个字符串参数，它们与从 `asp-all-route-data` 字典创建的键匹配。

如果字典中的任意键与路由参数匹配，则将在路由中相应地替换这些值，其他不匹配的值则生成为请求参数。

### <a name="asp-fragment"></a>asp-fragment

`asp-fragment` 定义要追加到 URL 的 URL 片段。 定位点标记帮助程序将添加哈希字符 (#)。 如果创建标记：

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

生成的 URL 将为：http://localhost/Speaker/Evaluations#SpeakerEvaluations

生成客户端应用程序时，哈希标记很有用。 它们可用于在 JavaScript 中轻松地执行标记和搜索等操作。

### <a name="asp-area"></a>asp-area

`asp-area` 设置区域名称，ASP.NET Core 使用该名称设置适当的路由。 以下示例展示了区域属性如何导致重新映射路由。 如果将 `asp-area` 设置为 Blogs，则会为此定位点标记的关联控制器和视图的路由添加目录 `Areas/Blogs` 作为前缀。

* 项目名称
  * wwwroot
  * 区域
    * 博客
      * Controllers
        * HomeController.cs
      * 视图
        * 主页
          * Index.cshtml
          * AboutBlog.cshtml
  * Controllers

使用定位点标记帮助程序指定一个有效的区域标记（比如，引用 ```AboutBlog.cshtml``` 文件时使用的 ```area="Blogs"```），如下所示。

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

生成的 HTML 将包括区域段，并将如下所示：

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> 若要使 MVC 区域在 Web 应用程序中正常工作，路由模板必须包含对该区域（如果存在）的引用。 该模板（`routes.MapRoute` 方法调用的第二个参数）将显示为：`template: '"{area:exists}/{controller=Home}/{action=Index}"'`

### <a name="asp-protocol"></a>asp-protocol

`asp-protocol` 用于在 URL 中指定协议（比如 `https`）。 包含协议的定位点标记帮助程序示例如下所示：

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

将生成如下所示的 HTML：

```<a href="https://localhost/Home/About">About</a>```

示例中的域为 localhost，但在生成 URL 时，定位点标记帮助程序会使用网站的公共域。

## <a name="additional-resources"></a>其他资源

* [区域](xref:mvc/controllers/areas)
