---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET 网页 (Razor) API 快速参考 |Microsoft Docs
author: tfitzmac
description: 此页列出了最常用的对象、 属性和方法的 ASP.NET Web Pages 编程使用 Razor 语法的简短示例。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: 3bf706cefe5302cf1085e0f814dc6654e42ae917
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378658"
---
<a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="1da76-103">ASP.NET 网页 (Razor) API 快速参考</span><span class="sxs-lookup"><span data-stu-id="1da76-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>
====================
<span data-ttu-id="1da76-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1da76-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1da76-105">此页列出了最常用的对象、 属性和方法的 ASP.NET Web Pages 编程使用 Razor 语法的简短示例。</span><span class="sxs-lookup"><span data-stu-id="1da76-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="1da76-106">在 ASP.NET Web Pages 版本 2 引入了标有"(v2)"的说明。</span><span class="sxs-lookup"><span data-stu-id="1da76-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="1da76-107">API 参考文档，请参阅[ASP.NET Web Pages 的参考文档](https://go.microsoft.com/fwlink/?LinkId=208659)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="1da76-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="1da76-108">软件版本</span><span class="sxs-lookup"><span data-stu-id="1da76-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="1da76-109">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1da76-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1da76-110">本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0 （除了标记 v2 的功能）。</span><span class="sxs-lookup"><span data-stu-id="1da76-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>


<span data-ttu-id="1da76-111">此页包含有关以下参考信息：</span><span class="sxs-lookup"><span data-stu-id="1da76-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="1da76-112">类</span><span class="sxs-lookup"><span data-stu-id="1da76-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="1da76-113">Data</span><span class="sxs-lookup"><span data-stu-id="1da76-113">Data</span></span>](#Data)
- [<span data-ttu-id="1da76-114">帮助程序</span><span class="sxs-lookup"><span data-stu-id="1da76-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="1da76-115">验证</span><span class="sxs-lookup"><span data-stu-id="1da76-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="1da76-116">类</span><span class="sxs-lookup"><span data-stu-id="1da76-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="1da76-117">包含可由任何页面共享应用程序中的数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="1da76-118">可以使用动态`App`属性来访问相同的数据，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="1da76-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="1da76-119">将一个字符串值转换为布尔值 (true/false)。</span><span class="sxs-lookup"><span data-stu-id="1da76-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="1da76-120">返回 false 或如果字符串不表示 true/false，则指定的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="1da76-121">将转换为日期/时间字符串值。</span><span class="sxs-lookup"><span data-stu-id="1da76-121">Converts a string value to date/time.</span></span> <span data-ttu-id="1da76-122">返回`DateTime.MinValue`或如果字符串不表示日期/时间指定的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="1da76-123">将一个字符串值转换为十进制值。</span><span class="sxs-lookup"><span data-stu-id="1da76-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="1da76-124">返回介于 0.0 或如果字符串不表示一个十进制值，则指定的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="1da76-125">将一个字符串值转换为浮点数。</span><span class="sxs-lookup"><span data-stu-id="1da76-125">Converts a string value to a float.</span></span> <span data-ttu-id="1da76-126">返回介于 0.0 或如果字符串不表示一个十进制值，则指定的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="1da76-127">将一个字符串值转换为整数。</span><span class="sxs-lookup"><span data-stu-id="1da76-127">Converts a string value to an integer.</span></span> <span data-ttu-id="1da76-128">返回 0 或如果字符串不表示一个整数，指定的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="1da76-129">从本地文件路径，包含可选的附加路径部分创建一个与浏览器兼容的 URL。</span><span class="sxs-lookup"><span data-stu-id="1da76-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="1da76-130">呈现*值*为 HTML 标记，而不是它呈现为 HTML 编码的输出。</span><span class="sxs-lookup"><span data-stu-id="1da76-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="1da76-131">如果可以将值从字符串转换为指定的类型，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="1da76-132">如果对象或变量不具有任何值，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="1da76-133">如果请求为 POST，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="1da76-134">（初始请求通常是 GET。）</span><span class="sxs-lookup"><span data-stu-id="1da76-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="1da76-135">指定要应用到此页所需的布局页的路径。</span><span class="sxs-lookup"><span data-stu-id="1da76-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="1da76-136">包含在当前请求的页面、 布局页和分页之间共享的数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="1da76-137">可以使用动态`Page`属性来访问相同的数据，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="1da76-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="1da76-138">（布局页）呈现内容页不在任何命名的节的内容。</span><span class="sxs-lookup"><span data-stu-id="1da76-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="1da76-139">呈现内容页使用指定的路径和可选的额外数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="1da76-140">可以获取来自的额外参数的值`PageData`的位置 （例如 1） 或键 （示例 2）。</span><span class="sxs-lookup"><span data-stu-id="1da76-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="1da76-141">（布局页）呈现内容部分具有名称。</span><span class="sxs-lookup"><span data-stu-id="1da76-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="1da76-142">设置*需*为 false，以使部分可选。</span><span class="sxs-lookup"><span data-stu-id="1da76-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="1da76-143">获取或设置 HTTP cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="1da76-144">获取当前请求中上传的文件。</span><span class="sxs-lookup"><span data-stu-id="1da76-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="1da76-145">获取在窗体发布 （作为字符串） 的数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="1da76-146">`Request[key]` 检查这两`Request.Form`和`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="1da76-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="1da76-147">获取指定的 URL 查询字符串中的数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="1da76-148">`Request[key]` 检查这两`Request.Form`和`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="1da76-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="1da76-149">有选择地禁用请求验证的窗体元素、 查询字符串值、 cookie 或标头值。</span><span class="sxs-lookup"><span data-stu-id="1da76-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="1da76-150">请求验证默认情况下启用，并防止用户将发布标记或其他潜在的危险的内容。</span><span class="sxs-lookup"><span data-stu-id="1da76-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="1da76-151">将 HTTP 服务器标头添加到响应。</span><span class="sxs-lookup"><span data-stu-id="1da76-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="1da76-152">将页面输出缓存指定的时间。</span><span class="sxs-lookup"><span data-stu-id="1da76-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="1da76-153">（可选） 设置*滑动*重置访问每个页上的超时值以及*varyByParams*来缓存不同版本的页的页请求中的每个不同的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="1da76-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="1da76-154">浏览器请求重定向到新位置。</span><span class="sxs-lookup"><span data-stu-id="1da76-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="1da76-155">设置发送到浏览器的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="1da76-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="1da76-156">内容写入*数据*到具有可选 MIME 类型响应。</span><span class="sxs-lookup"><span data-stu-id="1da76-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="1da76-157">写入响应文件的内容。</span><span class="sxs-lookup"><span data-stu-id="1da76-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="1da76-158">（布局页）定义一个内容部分，其中有一个名称。</span><span class="sxs-lookup"><span data-stu-id="1da76-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="1da76-159">解码是 HTML 编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="1da76-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="1da76-160">在 HTML 标记中呈现的字符串进行编码。</span><span class="sxs-lookup"><span data-stu-id="1da76-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="1da76-161">返回指定的虚拟路径的服务器物理路径。</span><span class="sxs-lookup"><span data-stu-id="1da76-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="1da76-162">解码 URL 中的文本。</span><span class="sxs-lookup"><span data-stu-id="1da76-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="1da76-163">将文本放在 URL 中编码。</span><span class="sxs-lookup"><span data-stu-id="1da76-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="1da76-164">获取或设置一个值，存在，直到用户关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="1da76-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="1da76-165">显示对象的值的字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="1da76-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="1da76-166">从 URL 中获取其他数据 (例如， */MyPage/ExtraData*)。</span><span class="sxs-lookup"><span data-stu-id="1da76-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="1da76-167">更改为指定的用户的密码。</span><span class="sxs-lookup"><span data-stu-id="1da76-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="1da76-168">确认使用帐户确认令牌的帐户。</span><span class="sxs-lookup"><span data-stu-id="1da76-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="1da76-169">使用指定的用户名和密码创建新的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="1da76-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="1da76-170">如果需要确认令牌，请传递 true 为*requireConfirmationToken。*</span><span class="sxs-lookup"><span data-stu-id="1da76-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="1da76-171">获取当前登录的用户的整数标识符。</span><span class="sxs-lookup"><span data-stu-id="1da76-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="1da76-172">获取当前登录的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="1da76-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="1da76-173">生成可以在电子邮件中向用户发送，以便用户可以重置密码的密码重置令牌。</span><span class="sxs-lookup"><span data-stu-id="1da76-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="1da76-174">从用户名返回用户 ID。</span><span class="sxs-lookup"><span data-stu-id="1da76-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="1da76-175">如果当前用户登录，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="1da76-176">如果已确认用户 （例如，通过确认电子邮件），则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="1da76-177">如果当前用户的名称与指定的用户名相匹配，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="1da76-178">通过在 cookie 中设置身份验证令牌记录中的用户。</span><span class="sxs-lookup"><span data-stu-id="1da76-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="1da76-179">删除身份验证令牌 cookie 使用户登录超时。</span><span class="sxs-lookup"><span data-stu-id="1da76-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="1da76-180">如果用户未经过身份验证，请将 HTTP 状态设置为 401 （未经授权）。</span><span class="sxs-lookup"><span data-stu-id="1da76-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="1da76-181">如果当前用户不是指定角色之一的成员，请将 HTTP 状态设置为 401 （未经授权）。</span><span class="sxs-lookup"><span data-stu-id="1da76-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="1da76-182">如果当前用户不是指定的用户*用户名*，HTTP 状态设置为 401 （未经授权）。</span><span class="sxs-lookup"><span data-stu-id="1da76-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="1da76-183">如果密码重置令牌有效，为新密码更改用户的密码。</span><span class="sxs-lookup"><span data-stu-id="1da76-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="1da76-184">数据</span><span class="sxs-lookup"><span data-stu-id="1da76-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="1da76-185">执行*SQLstatement* （包含可选参数） 如 INSERT、 DELETE 或 UPDATE，并返回受影响的记录的计数。</span><span class="sxs-lookup"><span data-stu-id="1da76-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="1da76-186">从最近插入的行返回标识列。</span><span class="sxs-lookup"><span data-stu-id="1da76-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="1da76-187">打开指定的数据库文件或使用已命名的连接字符串中指定的数据库*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="1da76-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="1da76-188">打开数据库使用连接字符串。</span><span class="sxs-lookup"><span data-stu-id="1da76-188">Opens a database using the connection string.</span></span> <span data-ttu-id="1da76-189">(这与完全不同`Database.Open`，它使用连接字符串名称。)</span><span class="sxs-lookup"><span data-stu-id="1da76-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="1da76-190">数据库使用的查询*SQLstatement* （根据需要传递参数） 并将结果返回为一个集合。</span><span class="sxs-lookup"><span data-stu-id="1da76-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="1da76-191">执行*SQLstatement* （包含可选参数），并返回一条记录。</span><span class="sxs-lookup"><span data-stu-id="1da76-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="1da76-192">执行*SQLstatement* （包含可选参数），并返回单个值。</span><span class="sxs-lookup"><span data-stu-id="1da76-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="1da76-193">帮助程序</span><span class="sxs-lookup"><span data-stu-id="1da76-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="1da76-194">将 Google 分析 JavaScript 代码呈现为指定的 id。</span><span class="sxs-lookup"><span data-stu-id="1da76-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="1da76-195">呈现指定的项目的 StatCounter 分析 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="1da76-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="1da76-196">呈现指定的帐户的 Yahoo 分析 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="1da76-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="1da76-197">传递到必应搜索。</span><span class="sxs-lookup"><span data-stu-id="1da76-197">Passes a search to Bing.</span></span> <span data-ttu-id="1da76-198">若要指定站点到搜索和搜索框的标题，可以设置`Bing.SiteUrl`和`Bing.SiteTitle`属性。</span><span class="sxs-lookup"><span data-stu-id="1da76-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="1da76-199">在设置这些属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="1da76-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="1da76-200">初始化一个图表。</span><span class="sxs-lookup"><span data-stu-id="1da76-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="1da76-201">向图表添加图例。</span><span class="sxs-lookup"><span data-stu-id="1da76-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="1da76-202">向图表添加一系列的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="1da76-203">返回指定的数据的哈希值。</span><span class="sxs-lookup"><span data-stu-id="1da76-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="1da76-204">默认的算法是`sha256`。</span><span class="sxs-lookup"><span data-stu-id="1da76-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="1da76-205">允许建立到页面的 Facebook 用户。</span><span class="sxs-lookup"><span data-stu-id="1da76-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="1da76-206">上传的文件中呈现的 UI。</span><span class="sxs-lookup"><span data-stu-id="1da76-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="1da76-207">呈现指定的 Xbox 玩家标记。</span><span class="sxs-lookup"><span data-stu-id="1da76-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="1da76-208">呈现指定的电子邮件地址的 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="1da76-209">将数据对象转换为 JavaScript 对象表示法 (JSON) 格式的字符串。</span><span class="sxs-lookup"><span data-stu-id="1da76-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="1da76-210">将 JSON 编码的输入的字符串转换为可以循环访问，也可以向数据库中插入的数据对象。</span><span class="sxs-lookup"><span data-stu-id="1da76-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="1da76-211">呈现社交网络的链接使用指定的标题和可选的 URL。</span><span class="sxs-lookup"><span data-stu-id="1da76-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="1da76-212">将一条错误消息与窗体字段关联。</span><span class="sxs-lookup"><span data-stu-id="1da76-212">Associates an error message with a form field.</span></span> <span data-ttu-id="1da76-213">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="1da76-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="1da76-214">将一条错误消息与窗体相关联。</span><span class="sxs-lookup"><span data-stu-id="1da76-214">Associates an error message with a form.</span></span> <span data-ttu-id="1da76-215">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="1da76-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="1da76-216">如果没有任何验证错误，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="1da76-217">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="1da76-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="1da76-218">呈现的属性和值的对象和任何子对象。</span><span class="sxs-lookup"><span data-stu-id="1da76-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="1da76-219">呈现 reCAPTCHA 验证测试。</span><span class="sxs-lookup"><span data-stu-id="1da76-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="1da76-220">设置 reCAPTCHA 服务的公共和私有密钥。</span><span class="sxs-lookup"><span data-stu-id="1da76-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="1da76-221">在设置这些属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="1da76-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="1da76-222">返回 reCAPTCHA 测试的结果。</span><span class="sxs-lookup"><span data-stu-id="1da76-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="1da76-223">呈现有关 ASP.NET Web Pages 的状态信息。</span><span class="sxs-lookup"><span data-stu-id="1da76-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="1da76-224">呈现指定的用户的 Twitter 流。</span><span class="sxs-lookup"><span data-stu-id="1da76-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="1da76-225">呈现指定的搜索文本的 Twitter 流。</span><span class="sxs-lookup"><span data-stu-id="1da76-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="1da76-226">呈现可选宽度和高度指定的文件的闪存视频播放器。</span><span class="sxs-lookup"><span data-stu-id="1da76-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="1da76-227">呈现可选宽度和高度指定的文件的 Windows 媒体播放器。</span><span class="sxs-lookup"><span data-stu-id="1da76-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="1da76-228">呈现指定的 Silverlight 播放器 *.xap*文件所需的宽度和高度。</span><span class="sxs-lookup"><span data-stu-id="1da76-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="1da76-229">返回由指定的对象*密钥*，或如果未找到该对象，则为 null。</span><span class="sxs-lookup"><span data-stu-id="1da76-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="1da76-230">删除指定的对象*密钥*缓存中。</span><span class="sxs-lookup"><span data-stu-id="1da76-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="1da76-231">将放*值*导入到指定的名称下缓存*密钥*。</span><span class="sxs-lookup"><span data-stu-id="1da76-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="1da76-232">创建一个新`WebGrid`对象使用查询中的数据。</span><span class="sxs-lookup"><span data-stu-id="1da76-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="1da76-233">呈现 HTML 表中显示数据标记。</span><span class="sxs-lookup"><span data-stu-id="1da76-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="1da76-234">呈现页导航`WebGrid`对象。</span><span class="sxs-lookup"><span data-stu-id="1da76-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="1da76-235">从指定的路径加载图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="1da76-236">将指定的映像添加为水印。</span><span class="sxs-lookup"><span data-stu-id="1da76-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="1da76-237">将指定的文本添加到映像。</span><span class="sxs-lookup"><span data-stu-id="1da76-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="1da76-238">水平或垂直翻转图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="1da76-239">在文件上传的映像发布到页面时，请加载图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="1da76-240">调整图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="1da76-241">旋转到左侧或右侧图像。</span><span class="sxs-lookup"><span data-stu-id="1da76-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="1da76-242">将图像保存到指定的路径。</span><span class="sxs-lookup"><span data-stu-id="1da76-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="1da76-243">设置 SMTP 服务器的密码。</span><span class="sxs-lookup"><span data-stu-id="1da76-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="1da76-244">在中设置此属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="1da76-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="1da76-245">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1da76-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="1da76-246">设置 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="1da76-246">Sets the SMTP server name.</span></span> <span data-ttu-id="1da76-247">在中设置此属性通常<em>\_AppStart</em>页。</span><span class="sxs-lookup"><span data-stu-id="1da76-247">Normally you set this property in the<em>\_AppStart</em> page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="1da76-248">设置 SMTP 服务器的用户名。</span><span class="sxs-lookup"><span data-stu-id="1da76-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="1da76-249">通常应将此属性 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="1da76-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="1da76-250">验证</span><span class="sxs-lookup"><span data-stu-id="1da76-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="1da76-251">(v2)呈现指定字段的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="1da76-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="1da76-252">(v2)显示所有验证错误的列表。</span><span class="sxs-lookup"><span data-stu-id="1da76-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="1da76-253">(v2)注册指定类型的验证用户输入的元素。</span><span class="sxs-lookup"><span data-stu-id="1da76-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="1da76-254">(v2)动态呈现客户端验证的 CSS 类的特性，以便您可以设置验证错误消息的格式。</span><span class="sxs-lookup"><span data-stu-id="1da76-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="1da76-255">（需要引用相应的客户端脚本库和定义 CSS 类。）</span><span class="sxs-lookup"><span data-stu-id="1da76-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="1da76-256">(v2)启用客户端验证用户输入字段。</span><span class="sxs-lookup"><span data-stu-id="1da76-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="1da76-257">（需要引用相应的客户端脚本库。）</span><span class="sxs-lookup"><span data-stu-id="1da76-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="1da76-258">(v2)如果是用于验证注册的所有用户输入的元素都包含有效的值，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="1da76-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="1da76-259">(v2)指定用户必须为用户输入元素提供一个值。</span><span class="sxs-lookup"><span data-stu-id="1da76-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="1da76-260">(v2)指定用户必须提供的每个用户输入元素的值。</span><span class="sxs-lookup"><span data-stu-id="1da76-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="1da76-261">此方法不允许你指定自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="1da76-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="1da76-262">(v2)指定一个验证测试，当您使用`Validation.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="1da76-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
