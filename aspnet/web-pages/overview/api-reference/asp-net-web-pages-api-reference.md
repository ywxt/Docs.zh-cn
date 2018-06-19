---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET 网页 (Razor) API 快速参考 |Microsoft 文档
author: tfitzmac
description: 此页包含的最常用的对象、 属性和方法进行编程的 ASP.NET Web Pages 使用 Razor 语法的简短示例的列表。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: 5f9d84f4d453583d7d4eae12e4fc510275255616
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30897579"
---
<a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="0049e-103">ASP.NET 网页 (Razor) API 快速参考</span><span class="sxs-lookup"><span data-stu-id="0049e-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>
====================
<span data-ttu-id="0049e-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0049e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0049e-105">此页包含的最常用的对象、 属性和方法进行编程的 ASP.NET Web Pages 使用 Razor 语法的简短示例的列表。</span><span class="sxs-lookup"><span data-stu-id="0049e-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="0049e-106">标记为"(v2)"的说明引入了在 ASP.NET Web Pages 版本 2。</span><span class="sxs-lookup"><span data-stu-id="0049e-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="0049e-107">API 参考文档，请参阅[ASP.NET 网页参考文档](https://go.microsoft.com/fwlink/?LinkId=208659)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="0049e-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="0049e-108">软件版本</span><span class="sxs-lookup"><span data-stu-id="0049e-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0049e-109">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0049e-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0049e-110">本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0 （除外标记 v2 的功能）。</span><span class="sxs-lookup"><span data-stu-id="0049e-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>


<span data-ttu-id="0049e-111">此页包含有关以下参考信息：</span><span class="sxs-lookup"><span data-stu-id="0049e-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="0049e-112">类</span><span class="sxs-lookup"><span data-stu-id="0049e-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="0049e-113">Data</span><span class="sxs-lookup"><span data-stu-id="0049e-113">Data</span></span>](#Data)
- [<span data-ttu-id="0049e-114">帮助器</span><span class="sxs-lookup"><span data-stu-id="0049e-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="0049e-115">验证</span><span class="sxs-lookup"><span data-stu-id="0049e-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="0049e-116">类</span><span class="sxs-lookup"><span data-stu-id="0049e-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="0049e-117">包含可由任何页共享应用程序中的数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="0049e-118">你可以使用动态`App`属性来访问相同的数据，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="0049e-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="0049e-119">将一个字符串值转换为布尔值 (true/false)。</span><span class="sxs-lookup"><span data-stu-id="0049e-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="0049e-120">返回 false 或指定的值如果字符串不表示 true/false。</span><span class="sxs-lookup"><span data-stu-id="0049e-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="0049e-121">将转换日期/时间的字符串值。</span><span class="sxs-lookup"><span data-stu-id="0049e-121">Converts a string value to date/time.</span></span> <span data-ttu-id="0049e-122">返回`DateTime.MinValue`或如果字符串不表示为日期/时间的指定的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="0049e-123">将一个字符串值转换为十进制值。</span><span class="sxs-lookup"><span data-stu-id="0049e-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="0049e-124">返回 0.0 或如果字符串不表示一个十进制值的指定的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="0049e-125">将一个字符串值转换为浮点数。</span><span class="sxs-lookup"><span data-stu-id="0049e-125">Converts a string value to a float.</span></span> <span data-ttu-id="0049e-126">返回 0.0 或如果字符串不表示一个十进制值的指定的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="0049e-127">将一个字符串值转换为整数。</span><span class="sxs-lookup"><span data-stu-id="0049e-127">Converts a string value to an integer.</span></span> <span data-ttu-id="0049e-128">返回 0 或如果字符串不表示一个整数，指定的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="0049e-129">从本地文件路径，具有可选的附加路径部分创建一个与浏览器兼容的 URL。</span><span class="sxs-lookup"><span data-stu-id="0049e-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="0049e-130">呈现*值*作为 HTML 标记，而不是呈现为 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="0049e-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="0049e-131">如果可以将值从字符串转换为指定的类型，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="0049e-132">如果该对象或变量不具有任何值，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="0049e-133">如果请求是 POST，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="0049e-134">（初始请求通常是 GET。）</span><span class="sxs-lookup"><span data-stu-id="0049e-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="0049e-135">指定要应用于此页所需的布局页的路径。</span><span class="sxs-lookup"><span data-stu-id="0049e-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="0049e-136">包含在当前请求中的页、 布局页和部分页面之间共享的数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="0049e-137">你可以使用动态`Page`属性来访问相同的数据，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="0049e-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="0049e-138">（布局页）呈现不在任何命名的部分内容页面的内容。</span><span class="sxs-lookup"><span data-stu-id="0049e-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="0049e-139">呈现内容的页面，使用指定的路径和可选的额外数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="0049e-140">你可以获取来自的额外参数的值`PageData`按照位置 （例如 1） 或键 （示例 2）。</span><span class="sxs-lookup"><span data-stu-id="0049e-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="0049e-141">（布局页）呈现内容的部分具有名称。</span><span class="sxs-lookup"><span data-stu-id="0049e-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="0049e-142">设置*必需*为 false 使一个节可选。</span><span class="sxs-lookup"><span data-stu-id="0049e-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="0049e-143">获取或设置 HTTP cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="0049e-144">获取当前请求过程中上载的文件。</span><span class="sxs-lookup"><span data-stu-id="0049e-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="0049e-145">获取窗体中 （作为字符串） 已发布的数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="0049e-146">`Request[key]` 检查同时`Request.Form`和`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="0049e-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="0049e-147">获取指定的 URL 查询字符串中的数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="0049e-148">`Request[key]` 检查同时`Request.Form`和`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="0049e-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="0049e-149">有选择性地禁用请求验证窗体元素、 查询字符串值、 cookie，或标头值。</span><span class="sxs-lookup"><span data-stu-id="0049e-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="0049e-150">请求验证默认处于启用状态，并且可以防止用户发布标记或其他潜在危险的内容。</span><span class="sxs-lookup"><span data-stu-id="0049e-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="0049e-151">将 HTTP 服务器标头添加到响应中。</span><span class="sxs-lookup"><span data-stu-id="0049e-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="0049e-152">将页面输出缓存指定的时间。</span><span class="sxs-lookup"><span data-stu-id="0049e-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="0049e-153">可以选择设置*滑动*重置在每次页访问的超时和*varyByParams*缓存的页面请求中每个不同的查询字符串的页的不同版本。</span><span class="sxs-lookup"><span data-stu-id="0049e-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="0049e-154">将浏览器请求重定向到新位置。</span><span class="sxs-lookup"><span data-stu-id="0049e-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="0049e-155">设置发送到浏览器的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="0049e-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="0049e-156">内容写入*数据*到具有可选的 MIME 类型的响应。</span><span class="sxs-lookup"><span data-stu-id="0049e-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="0049e-157">将响应写入的文件的内容。</span><span class="sxs-lookup"><span data-stu-id="0049e-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="0049e-158">（布局页）定义一个内容段中，有一个名称。</span><span class="sxs-lookup"><span data-stu-id="0049e-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="0049e-159">对 HTML 编码的字符串进行解码。</span><span class="sxs-lookup"><span data-stu-id="0049e-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="0049e-160">将编码的字符串中的 HTML 标记的呈现。</span><span class="sxs-lookup"><span data-stu-id="0049e-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="0049e-161">返回指定的虚拟路径的服务器物理路径。</span><span class="sxs-lookup"><span data-stu-id="0049e-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="0049e-162">将文本从 URL 解码。</span><span class="sxs-lookup"><span data-stu-id="0049e-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="0049e-163">将文本将在 URL 中的编码。</span><span class="sxs-lookup"><span data-stu-id="0049e-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="0049e-164">获取或设置一个值，用户关闭浏览器一直存在。</span><span class="sxs-lookup"><span data-stu-id="0049e-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="0049e-165">显示的字符串表示形式的对象的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="0049e-166">获取其他数据从 URL (例如， */MyPage/ExtraData*)。</span><span class="sxs-lookup"><span data-stu-id="0049e-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="0049e-167">更改指定的用户的密码。</span><span class="sxs-lookup"><span data-stu-id="0049e-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="0049e-168">确认使用帐户确认令牌的帐户。</span><span class="sxs-lookup"><span data-stu-id="0049e-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="0049e-169">使用指定的用户名和密码创建新的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="0049e-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="0049e-170">如果需要确认令牌，请将传递适用*requireConfirmationToken。*</span><span class="sxs-lookup"><span data-stu-id="0049e-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="0049e-171">获取当前登录的用户的整数标识符。</span><span class="sxs-lookup"><span data-stu-id="0049e-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="0049e-172">获取当前登录的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="0049e-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="0049e-173">生成可通过发送电子邮件给用户，以便用户可以重置密码的密码重置标记。</span><span class="sxs-lookup"><span data-stu-id="0049e-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="0049e-174">用户名中返回的用户 ID。</span><span class="sxs-lookup"><span data-stu-id="0049e-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="0049e-175">如果当前用户登录，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="0049e-176">如果用户已确认 （例如，通过确认电子邮件），则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="0049e-177">如果当前用户的名称与指定的用户名称匹配，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="0049e-178">通过在 cookie 中设置身份验证令牌记录中的用户。</span><span class="sxs-lookup"><span data-stu-id="0049e-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="0049e-179">通过删除身份验证令牌 cookie 缩小记录用户。</span><span class="sxs-lookup"><span data-stu-id="0049e-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="0049e-180">如果用户未通过身份验证，则设置的 HTTP 状态为 401 （未授权）。</span><span class="sxs-lookup"><span data-stu-id="0049e-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="0049e-181">如果当前用户不是某个指定的角色的成员，设置 HTTP 状态为 401 （未授权）。</span><span class="sxs-lookup"><span data-stu-id="0049e-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="0049e-182">如果当前用户不是按指定的用户*用户名*，将 HTTP 状态设置为 401 （未授权）。</span><span class="sxs-lookup"><span data-stu-id="0049e-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="0049e-183">如果密码重置令牌有效，请为新密码更改用户的密码。</span><span class="sxs-lookup"><span data-stu-id="0049e-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="0049e-184">数据</span><span class="sxs-lookup"><span data-stu-id="0049e-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="0049e-185">执行*SQLstatement* （带可选参数） 如 INSERT、 DELETE 或 UPDATE 并返回受影响的记录计数。</span><span class="sxs-lookup"><span data-stu-id="0049e-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="0049e-186">从最近插入的行返回的标识列。</span><span class="sxs-lookup"><span data-stu-id="0049e-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="0049e-187">打开指定的数据库文件或使用已命名的连接字符串中指定的数据库*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="0049e-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="0049e-188">打开使用连接字符串的数据库。</span><span class="sxs-lookup"><span data-stu-id="0049e-188">Opens a database using the connection string.</span></span> <span data-ttu-id="0049e-189">(这点与`Database.Open`，它使用的连接字符串名称。)</span><span class="sxs-lookup"><span data-stu-id="0049e-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="0049e-190">查询数据库使用*SQLstatement* （根据需要传递参数） 并以集合形式返回结果。</span><span class="sxs-lookup"><span data-stu-id="0049e-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="0049e-191">执行*SQLstatement* （带可选参数），并返回单个记录。</span><span class="sxs-lookup"><span data-stu-id="0049e-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="0049e-192">执行*SQLstatement* （带可选参数），并返回单个值。</span><span class="sxs-lookup"><span data-stu-id="0049e-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="0049e-193">帮助器</span><span class="sxs-lookup"><span data-stu-id="0049e-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="0049e-194">为指定的 id。 呈现 Google 分析 JavaScript 代码</span><span class="sxs-lookup"><span data-stu-id="0049e-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="0049e-195">呈现指定项目的 StatCounter 分析 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="0049e-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="0049e-196">呈现为指定的帐户的 Yahoo 分析 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="0049e-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="0049e-197">将搜索传递给必应。</span><span class="sxs-lookup"><span data-stu-id="0049e-197">Passes a search to Bing.</span></span> <span data-ttu-id="0049e-198">若要指定站点到搜索并搜索框的标题，可以设置`Bing.SiteUrl`和`Bing.SiteTitle`属性。</span><span class="sxs-lookup"><span data-stu-id="0049e-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="0049e-199">在中设置这些属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="0049e-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="0049e-200">初始化一个图表。</span><span class="sxs-lookup"><span data-stu-id="0049e-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="0049e-201">向图表添加图例。</span><span class="sxs-lookup"><span data-stu-id="0049e-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="0049e-202">向图表中添加一系列值。</span><span class="sxs-lookup"><span data-stu-id="0049e-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="0049e-203">返回指定的数据的哈希值。</span><span class="sxs-lookup"><span data-stu-id="0049e-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="0049e-204">默认算法是`sha256`。</span><span class="sxs-lookup"><span data-stu-id="0049e-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="0049e-205">允许连接到页的 Facebook 用户。</span><span class="sxs-lookup"><span data-stu-id="0049e-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="0049e-206">将文件上载呈现用户界面。</span><span class="sxs-lookup"><span data-stu-id="0049e-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="0049e-207">呈现指定的 Xbox 游戏标记。</span><span class="sxs-lookup"><span data-stu-id="0049e-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="0049e-208">呈现为指定的电子邮件地址 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="0049e-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="0049e-209">将数据对象转换为 JavaScript 对象表示法 (JSON) 格式的字符串。</span><span class="sxs-lookup"><span data-stu-id="0049e-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="0049e-210">将 JSON 编码的输入的字符串转换为可以循环访问或向数据库中插入的数据对象。</span><span class="sxs-lookup"><span data-stu-id="0049e-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="0049e-211">呈现使用指定的标题和可选的 URL 的社交网络链接。</span><span class="sxs-lookup"><span data-stu-id="0049e-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="0049e-212">将一条错误消息与窗体字段相关联。</span><span class="sxs-lookup"><span data-stu-id="0049e-212">Associates an error message with a form field.</span></span> <span data-ttu-id="0049e-213">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="0049e-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="0049e-214">将一条错误消息表单与相关联。</span><span class="sxs-lookup"><span data-stu-id="0049e-214">Associates an error message with a form.</span></span> <span data-ttu-id="0049e-215">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="0049e-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="0049e-216">如果没有任何验证错误，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="0049e-217">使用`ModelState`帮助器访问该成员。</span><span class="sxs-lookup"><span data-stu-id="0049e-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="0049e-218">呈现的属性和值的对象和任何子对象。</span><span class="sxs-lookup"><span data-stu-id="0049e-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="0049e-219">呈现 reCAPTCHA 验证测试。</span><span class="sxs-lookup"><span data-stu-id="0049e-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="0049e-220">设置 reCAPTCHA 服务的公共和私有密钥。</span><span class="sxs-lookup"><span data-stu-id="0049e-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="0049e-221">在中设置这些属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="0049e-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="0049e-222">返回 reCAPTCHA 测试的结果。</span><span class="sxs-lookup"><span data-stu-id="0049e-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="0049e-223">呈现有关 ASP.NET Web 页的状态信息。</span><span class="sxs-lookup"><span data-stu-id="0049e-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="0049e-224">呈现为指定的用户 Twitter 流。</span><span class="sxs-lookup"><span data-stu-id="0049e-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="0049e-225">呈现一个 Twitter 流以便指定的搜索文本。</span><span class="sxs-lookup"><span data-stu-id="0049e-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="0049e-226">呈现闪存视频播放器与可选的宽度和高度指定的文件。</span><span class="sxs-lookup"><span data-stu-id="0049e-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="0049e-227">呈现与可选的宽度和高度指定的文件的 Windows 媒体播放器。</span><span class="sxs-lookup"><span data-stu-id="0049e-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="0049e-228">呈现为指定的 Silverlight 播放器 *.xap*文件所需的宽度和高度。</span><span class="sxs-lookup"><span data-stu-id="0049e-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="0049e-229">返回指定的对象*密钥*，或如果找不到对象为 null。</span><span class="sxs-lookup"><span data-stu-id="0049e-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="0049e-230">删除指定的对象*密钥*从缓存。</span><span class="sxs-lookup"><span data-stu-id="0049e-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="0049e-231">放入*值*到下指定的名称缓存*密钥*。</span><span class="sxs-lookup"><span data-stu-id="0049e-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="0049e-232">创建一个新`WebGrid`对象使用查询中的数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="0049e-233">呈现标记以 HTML 表中显示数据。</span><span class="sxs-lookup"><span data-stu-id="0049e-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="0049e-234">呈现页导航`WebGrid`对象。</span><span class="sxs-lookup"><span data-stu-id="0049e-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="0049e-235">从指定的路径加载图像。</span><span class="sxs-lookup"><span data-stu-id="0049e-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="0049e-236">将指定的映像添加为水印。</span><span class="sxs-lookup"><span data-stu-id="0049e-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="0049e-237">将指定的文本添加到映像。</span><span class="sxs-lookup"><span data-stu-id="0049e-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="0049e-238">水平或垂直翻转图像。</span><span class="sxs-lookup"><span data-stu-id="0049e-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="0049e-239">加载图像，图像文件上载过程中发送到页面时。</span><span class="sxs-lookup"><span data-stu-id="0049e-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="0049e-240">调整图像。</span><span class="sxs-lookup"><span data-stu-id="0049e-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="0049e-241">将向左或向右图像的旋转。</span><span class="sxs-lookup"><span data-stu-id="0049e-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="0049e-242">将图像保存到指定的路径。</span><span class="sxs-lookup"><span data-stu-id="0049e-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="0049e-243">为 SMTP 服务器设置的密码。</span><span class="sxs-lookup"><span data-stu-id="0049e-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="0049e-244">在设置此属性通常 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="0049e-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="0049e-245">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="0049e-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="0049e-246">设置 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="0049e-246">Sets the SMTP server name.</span></span> <span data-ttu-id="0049e-247">在设置此属性通常<em>\_AppStart</em>页。</span><span class="sxs-lookup"><span data-stu-id="0049e-247">Normally you set this property in the<em>\_AppStart</em> page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="0049e-248">设置 SMTP 服务器的用户名称。</span><span class="sxs-lookup"><span data-stu-id="0049e-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="0049e-249">通常应在设置此属性 *\_AppStart*页。</span><span class="sxs-lookup"><span data-stu-id="0049e-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="0049e-250">验证</span><span class="sxs-lookup"><span data-stu-id="0049e-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="0049e-251">(v2)呈现指定字段的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="0049e-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="0049e-252">(v2)显示所有验证错误的列表。</span><span class="sxs-lookup"><span data-stu-id="0049e-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="0049e-253">(v2)注册的指定类型的验证的用户输入的元素。</span><span class="sxs-lookup"><span data-stu-id="0049e-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="0049e-254">(v2)动态呈现客户端验证的 CSS 类特性，以便你可以设置验证错误消息的格式。</span><span class="sxs-lookup"><span data-stu-id="0049e-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="0049e-255">（需要引用相应的客户端脚本库和定义 CSS 类。）</span><span class="sxs-lookup"><span data-stu-id="0049e-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="0049e-256">(v2)启用客户端验证用户输入字段。</span><span class="sxs-lookup"><span data-stu-id="0049e-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="0049e-257">（需要引用相应的客户端脚本库。）</span><span class="sxs-lookup"><span data-stu-id="0049e-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="0049e-258">(v2)如果是用于验证注册的所有用户输入的元素都包含有效的值，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="0049e-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="0049e-259">(v2)指定用户必须提供用户输入元素的值。</span><span class="sxs-lookup"><span data-stu-id="0049e-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="0049e-260">(v2)指定用户必须为每个用户输入元素提供值。</span><span class="sxs-lookup"><span data-stu-id="0049e-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="0049e-261">此方法不允许您指定的自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="0049e-261">This method does not let you specify a custom error message.</span></span>

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

<span data-ttu-id="0049e-262">(v2)当你使用指定的验证测试`Validation.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="0049e-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
