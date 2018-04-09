---
title: 在 ASP.NET Core 防止跨站点请求伪造 (XSRF/CSRF) 攻击
author: steve-smith
description: 了解如何防止对恶意网站可能会影响客户端浏览器和应用程序之间的交互的 web 应用的攻击。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/19/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: ad50f8b261447d40ccc24c0ee006239aa976bf20
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2018
---
# <a name="prevent-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a>在 ASP.NET Core 防止跨站点请求伪造 (XSRF/CSRF) 攻击

通过[Steve Smith](https://ardalis.com/)， [Fiyaz Hasan](https://twitter.com/FiyazBinHasan)，和[Rick Anderson](https://twitter.com/RickAndMSFT)

跨站点请求伪造 (也称为 XSRF 或 CSRF，发音*，请参阅冲浪*) 是针对恶意网站凭此可以影响客户端浏览器和信任，一个 web 应用程序之间的交互的 web 承载的应用程序的攻击浏览器。 这些攻击是可能的因为 web 浏览器将自动与每个请求某些类型的身份验证令牌发送到网站。 这种形式的攻击也称为是*一键式攻击*或*会话乘坐*因为攻击充分利用用户的先前进行身份验证会话。

CSRF 攻击的示例：

1. 用户登录到`www.good-banking-site.com`使用窗体身份验证。 服务器对用户进行身份验证，并发出包含身份验证 cookie 的响应。 该站点处于易受到攻击，因为它信任的任何请求都收到与有效的身份验证 cookie。
1. 用户访问恶意站点， `www.bad-crook-site.com`。

   恶意站点， `www.bad-crook-site.com`，包含类似于以下的 HTML 窗体：

   ```html
   <h1>Congratulations! You're a Winner!</h1>
   <form action="http://good-banking-site.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw">
       <input type="hidden" name="Amount" value="1000000">
       <input type="submit" value="Click to collect your prize!">
   </form>
   ```

   请注意，窗体的`action`文章到易受攻击的站点上，而不是恶意的站点。 这是 CSRF 的"跨站点"部分。

1. 用户选择提交按钮。 浏览器发出请求，并自动将请求的域中，身份验证 cookie `www.good-banking-site.com`。
1. 在上运行的请求`www.good-banking-site.com`与用户的身份验证上下文的服务器，并且可以执行允许经过身份验证的用户执行任何操作。

当用户选择按钮以提交表单时，将无法恶意站点：

* 运行自动提交该表单的脚本。
* 将窗体提交作为 AJAX 请求中发送。 
* 使用 CSS 的隐藏的表单。 

使用 HTTPS，则不会阻止 CSRF 攻击。 恶意站点可以将发送`https://www.good-banking-site.com/`请求一样轻松它可发送的不安全的请求。

一些攻击目标响应 GET 请求的终结点，在这种情况下使用的图像标记要执行的操作。 允许映像但阻止 JavaScript 的论坛站点上，这种攻击十分常见。 应用程序更改的状态 GET 请求中，在其中修改变量或资源，就很容易遭受恶意攻击。 **更改状态的 GET 请求是不安全的。最佳做法是永远不会更改在 GET 请求的状态。**

针对 web 应用可用于身份验证的 cookie，因为可能会出现 CSRF 攻击：

* 浏览器存储颁发的 web 应用的 cookie。
* 存储的 cookie 包括用于身份验证的用户的会话 cookie。
* 浏览器发送的所有 cookie 与域关联到 web 应用程序而不考虑如何向应用程序请求生成浏览器中的每个请求。

但是，CSRF 攻击不局限于利用 cookie。 例如，基本和摘要式身份验证也是易受攻击的。 浏览器使用基本或摘要式身份验证的用户登录后，直到会话才会自动发送凭据&dagger;结束。

&dagger;在此上下文中，*会话*指的是在此期间用户进行身份验证的客户端会话。 它是与服务器端会话无关或[ASP.NET 核心会话中间件](xref:fundamentals/app-state)。

用户可以通过采取预防措施来防止 CSRF 漏洞：

* 从 web 应用程序在完成后使用这些签名。
* 定期清除浏览器 cookie。

但是，CSRF 漏洞基本上是 web 应用，而不是最终用户有问题。

## <a name="authentication-fundamentals"></a>身份验证基础知识

基于 cookie 的身份验证是一种身份验证的常用形式。 基于令牌的身份验证系统中受欢迎程度，特别是对于单页面应用程序 (Spa) 增长。

### <a name="cookie-based-authentication"></a>基于 cookie 的身份验证

当用户身份验证使用其用户名和密码时，它们被颁发一个令牌，包含可以用于身份验证和授权的身份验证票证。 随着工作的附带的每个请求客户端的 cookie 的令牌存储。 生成和验证此 cookie 的 Cookie 身份验证中间件执行。 [中间件](xref:fundamentals/middleware/index)的加密 cookie 序列化为一个用户主体。 在后续请求，该中间件将验证 cookie，重新创建主体，并将分配到主体[用户](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)属性[HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)。

### <a name="token-based-authentication"></a>基于令牌的身份验证

当用户进行身份验证时，它们被颁发一个令牌 （不 antiforgery 令牌）。 令牌包含用户信息的形式[声明](/dotnet/framework/security/claims-based-identity-model)或指向维护应用程序中的用户状态的应用程序的引用令牌。 当用户尝试访问要求进行身份验证的资源时，令牌将发送到使用的其他授权标头中的持有者令牌的窗体应用程序。 这使得应用程序无状态。 在每个后续请求中，令牌请求中传递进行服务器端验证。 此令牌不*加密*; 它具有*编码*。 在服务器上，将解码令牌来访问其信息。 若要在后续请求中发送令牌，请在浏览器的本地存储中存储令牌。 如果该令牌存储在浏览器的本地存储，则不会关心 CSRF 漏洞。 CSRF 是一个问题时的令牌存储在一个 cookie。

### <a name="multiple-apps-hosted-at-one-domain"></a>在一个域托管的多个应用程序

共享宿主环境包括易受到会话劫持、 登录 CSRF 和其他的攻击。

尽管`example1.contoso.net`和`example2.contoso.net`是不同的主机下的主机之间没有隐式信任关系`*.contoso.net`域。 此隐式信任关系允许影响对方的 cookie （控制 AJAX 请求的同源策略不一定适用于 HTTP cookie） 可能不受信任的主机。

可以通过不能共享域防止利用在同一个域上托管的应用程序之间的受信任的 cookie 的攻击。 当每个应用程序托管在自身域中时，没有任何隐式 cookie 信任关系，以便利用。

## <a name="aspnet-core-antiforgery-configuration"></a>ASP.NET 核心 antiforgery 配置

> [!WARNING]
> ASP.NET 核心实现 antiforgery 使用[ASP.NET 核心数据保护](xref:security/data-protection/introduction)。 数据保护堆栈必须配置为在服务器场中正常工作。 请参阅[配置数据保护](xref:security/data-protection/configuration/overview)有关详细信息。

在 ASP.NET 核心 2.0 或更高版本， [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) antiforgery 令牌注入 HTML 窗体元素。 Razor 文件中的以下标记将自动生成 antiforgery 令牌：

```cshtml
<form method="post">
    ...
</form>
```

类似地， [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) antiforgery 令牌生成默认情况下，如果窗体的方法不 GET。

自动生成的 antiforgery 令牌 HTML 窗体元素发生时`<form>`标记包含`method="post"`属性和以下任一条件：

  * 操作属性为空 (`action=""`)。
  * 操作属性不提供 (`<form method="post">`)。

可以禁用自动生成的 antiforgery 令牌 HTML 窗体元素：

* 显式禁用 antiforgery 令牌`asp-antiforgery`属性：

  ```cshtml
  <form method="post" asp-antiforgery="false">
      ...
  </form>
  ```

* Form 元素是已选择扩展的标记帮助程序通过使用标记帮助器[！ 选择退出符号](xref:mvc/views/tag-helpers/intro#opt-out):

  ```cshtml
  <!form method="post">
      ...
  </!form>
  ```

* 删除`FormTagHelper`从视图。 `FormTagHelper`可以通过将以下指令添加到 Razor 视图从视图中删除：

  ```cshtml
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> [Razor 页](xref:mvc/razor-pages/index)会自动防范 XSRF/CSRF。 有关详细信息，请参阅[XSRF/CSRF 和 Razor 页](xref:mvc/razor-pages/index#xsrf)。

防御 CSRF 攻击的最常见方法是使用*同步器令牌模式*(STP)。 在用户请求具有窗体数据的页时，使用 STP:

1. 服务器将发送到客户端的当前用户的标识与关联的令牌。
1. 客户端返回将令牌发送到服务器以进行验证。
1. 如果服务器收到与经过身份验证的用户的标识不匹配的令牌，而拒绝该请求。

该令牌的唯一且不可预测。 此外可以使用令牌以确保正确地执行序列化的一系列请求 (例如，确保请求序列的： 第 1 页&ndash;页上 2&ndash;第 3 页)。 ASP.NET 核心 MVC 和 Razor 页模板中的窗体的所有生成 antiforgery 令牌。 以下两个视图的示例生成 antiforgery 令牌：

```cshtml
<form asp-controller="Manage" asp-action="ChangePassword" method="post">
    ...
</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    ...
}
```

显式添加到 antiforgery 令牌`<form>`没有标记帮助程序使用的 HTML 帮助程序元素[ @Html.AntiForgeryToken ](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):

```cshtml
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

在每个前面的情况下，ASP.NET Core 添加类似于以下一个隐藏的表单字段：

```cshtml
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkS ... s2-m9Yw">
```

ASP.NET 核心包括三个[筛选器](xref:mvc/controllers/filters)来处理 antiforgery 令牌：

* [ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)
* [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)
* [IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)

## <a name="antiforgery-options"></a>Antiforgery 选项

自定义[antiforgery 选项](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions)中`Startup.ConfigureServices`:

```csharp
services.AddAntiforgery(options => 
{
    options.CookieDomain = "contoso.com";
    options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
    options.CookiePath = "Path";
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.RequireSsl = false;
    options.SuppressXFrameOptionsHeader = false;
});
```

| 选项 | 描述 |
| ------ | ----------- |
| [Cookie](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookie) | 确定用于创建 antiforgery cookie 的设置。 |
| [CookieDomain](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiedomain) | Cookie 的域。 默认为 `null`。 此属性已过时，并在未来版本中将删除。 建议的替代项是 Cookie.Domain。 |
| [CookieName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiename) | Cookie 的名称。 如果未设置，则系统会生成一个唯一的名称开头[DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) ("。AspNetCore.Antiforgery。") 下。 此属性已过时，并在未来版本中将删除。 建议的替代项是 Cookie.Name。 |
| [CookiePath](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiepath) | 在 cookie 上设置的路径。 此属性已过时，并在未来版本中将删除。 建议的替代项是 Cookie.Path。 |
| [FormFieldName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.formfieldname) | Antiforgery 系统用于呈现 antiforgery 令牌在视图中的隐藏的表单字段的名称。 |
| [HeaderName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.headername) | Antiforgery 系统使用的标头的名称。 如果`null`，系统会考虑仅窗体数据。 |
| [RequireSsl](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.requiressl) | 指定是否由 antiforgery 系统需要 SSL。 如果`true`，非 SSL 请求将失败。 默认为 `false`。 此属性已过时，并在未来版本中将删除。 建议的替代项是设置 Cookie.SecurePolicy。 |
| [SuppressXFrameOptionsHeader](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.suppressxframeoptionsheader) | 指定是否禁止生成`X-Frame-Options`标头。 默认情况下，值为"SAMEORIGIN"生成标头。 默认为 `false`。 |

有关详细信息，请参阅[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions)。

## <a name="configure-antiforgery-features-with-iantiforgery"></a>使用 IAntiforgery 配置 antiforgery 功能

[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery)提供 API 来配置 antiforgery 功能。 `IAntiforgery` 可以在请求`Configure`方法`Startup`类。 下面的示例使用从应用程序的主页上的中间件生成 antiforgery 令牌并将其发送响应中将其作为 cookie （使用在本主题后面所述的默认角度命名约定）：

```csharp
public void Configure(IApplicationBuilder app, IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;

        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // The request token can be sent as a JavaScript-readable cookie, 
            // and Angular uses it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
}
```

### <a name="require-antiforgery-validation"></a>要求 antiforgery 验证

[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)是操作筛选器，可以应用于单个操作，一个控制器或全局范围内。 除非请求包含有效的 antiforgery 令牌，将阻止对已应用此筛选器的操作发出的请求。

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();

    if (user != null)
    {
        var result = 
            await _userManager.RemoveLoginAsync(
                user, account.LoginProvider, account.ProviderKey);

        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }

    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

`ValidateAntiForgeryToken`属性修饰，包括 HTTP GET 请求对操作方法的请求要求令牌。 如果`ValidateAntiForgeryToken`属性应用跨应用程序的控制器，则可以重写与`IgnoreAntiforgeryToken`属性。

> [!NOTE]
> ASP.NET Core 不支持自动将 antiforgery 令牌添加到 GET 请求。

### <a name="automatically-validate-antiforgery-tokens-for-unsafe-http-methods-only"></a>自动验证 antiforgery 令牌仅不安全的 HTTP 方法

ASP.NET Core 应用不生成 antiforgery 令牌进行安全的 HTTP 方法 （GET、 HEAD、 选项和跟踪）。 而不是广泛应用`ValidateAntiForgeryToken`属性，然后重写它与`IgnoreAntiforgeryToken`特性， [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)可以使用属性。 此属性适用类似`ValidateAntiForgeryToken`特性，只不过它不需要使用以下的 HTTP 方法发出的请求令牌：

* GET
* HEAD
* 选项
* TRACE

我们建议使用`AutoValidateAntiforgeryToken`广泛的非 API 方案。 这可确保默认情况下保护 POST 操作。 替代项是默认情况下，将忽略 antiforgery 令牌除非`ValidateAntiForgeryToken`应用于单个操作方法。 它更有可能在此方案中保留的 POST 操作方法不受保护错误地使应用程序容易受到 CSRF 攻击。 所有文章应都发送 antiforgery 令牌。

Api 没有一种用于发送令牌的非 cookie 一部分的自动机制。 实现可能取决于客户端代码实现。 一些示例如下所示：

类级别示例：

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

全局示例：

```csharp
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

### <a name="override-global-or-controller-antiforgery-attributes"></a>替代全局或控制器 antiforgery 属性

[IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)筛选器用于消除对给定操作 （或控制器） 的 antiforgery 令牌的需要。 当应用时，此筛选器将重写`ValidateAntiForgeryToken`和`AutoValidateAntiforgeryToken`（全局或在控制器上） 在高级别指定筛选器。

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
    [HttpPost]
    [IgnoreAntiforgeryToken]
    public async Task<IActionResult> DoSomethingSafe(SomeViewModel model)
    {
        // no antiforgery token required
    }
}
```

## <a name="refresh-tokens-after-authentication"></a>身份验证后刷新令牌

用户进行身份验证通过将用户重定向到一个视图或 Razor 页页后，应刷新令牌。

## <a name="javascript-ajax-and-spas"></a>JavaScript、 AJAX 和 Spa

在传统的基于 HTML 的应用，antiforgery 令牌将传递到使用隐藏的表单域的服务器。 在基于 JavaScript 的现代应用和 Spa 中，以编程方式进行多请求。 这些 AJAX 请求可能使用其他方法 （如请求标头或 cookie） 将该令牌发送。

如果使用 cookie 来存储身份验证令牌，并在服务器上的 API 请求进行身份验证，CSRF 是一个潜在的问题。 如果本地存储用于存储令牌，因为从本地存储的值不会自动发送到每个请求的服务器可能会缓解 CSRF 漏洞。 因此，使用本地存储来存储客户端和发送令牌，因为请求标头是建议的方法上的 antiforgery 令牌。

### <a name="javascript"></a>JavaScript

使用视图支持 JavaScript，令牌可以创建使用从视图中的服务。 注入[Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery)到视图并调用服务[GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):

[!code-csharp[](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,12-13,35-36)]

此方法不需要直接处理从服务器设置 cookie 或从客户端读取它们。

前面的示例使用 JavaScript 的 AJAX POST 标头中读取的隐藏的字段值。

JavaScript 还可以访问在 cookie 令牌并使用 cookie 的内容与令牌的值创建的标头。

```csharp
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
    new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

假设脚本请求将该令牌发送调用标头中`X-CSRF-TOKEN`，配置 antiforgery 服务以查找`X-CSRF-TOKEN`标头：

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

下面的示例使用 JavaScript 进行了相应的标头使用的 AJAX 请求：

```javascript
function getCookie(cname) {
    var name = cname + "=";
    var decodedCookie = decodeURIComponent(document.cookie);
    var ca = decodedCookie.split(';');
    for(var i = 0; i <ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

var csrfToken = getCookie("CSRF-TOKEN");

var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (xhttp.readyState == XMLHttpRequest.DONE) {
        if (xhttp.status == 200) {
            alert(xhttp.responseText);
        } else {
            alert('There was an error processing the AJAX request.');
        }
    }
};
xhttp.open('POST', '/api/password/changepassword', true);
xhttp.setRequestHeader("Content-type", "application/json");
xhttp.setRequestHeader("X-CSRF-TOKEN", csrfToken);
xhttp.send(JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }));
```

### <a name="angularjs"></a>AngularJS

AngularJS 使用到地址 CSRF 的约定。 如果服务器发送具有该名称的 cookie `XSRF-TOKEN`，AngularJS`$http`服务将 cookie 值添加到标头时它将请求发送到服务器。 此过程是自动进行。 标头不需要显式设置。 标头名称是`X-XSRF-TOKEN`。 服务器应检测此标头，并验证其内容。

有关 ASP.NET 核心 API 使用此约定：

* 配置你的应用程序提供在调用 cookie 令牌`XSRF-TOKEN`。
* 将查找名为的标头 antiforgery 服务配置为`X-XSRF-TOKEN`。

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="extend-antiforgery"></a>扩展 antiforgery

[IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider)类型允许开发人员通过往返中每个令牌的其他数据扩展的反 CSRF 系统行为。 [GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata)每次调用方法生成的字段标记，和在生成的标记内嵌入的返回值。 实施者无法返回时间戳、 nonce 或任何其他值，然后调用[ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata)时验证令牌验证此数据。 客户端的用户名已嵌入在生成的令牌中，因此无需包括此信息。 如果令牌包括补充数据但不是`IAntiForgeryAdditionalDataProvider`是配置，不验证补充数据。

## <a name="additional-resources"></a>其他资源

* [CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))上[打开 Web 应用程序安全项目](https://www.owasp.org/index.php/Main_Page)(OWASP)。
