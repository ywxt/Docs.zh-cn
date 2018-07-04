---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 防止 ASP.NET Web API 中的跨站点请求伪造 (CSRF) 攻击 |Microsoft Docs
author: MikeWasson
description: 介绍跨站点请求伪造 (CSRF) 攻击以及如何在 ASP.NET Web API 中实施反 CSRF 度量值。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 7dfddf09a1577cfa7a52f58b37533724a8475435
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379862"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a>防止 ASP.NET Web API 中的跨站点请求伪造 (CSRF) 攻击
====================
通过[Mike Wasson](https://github.com/MikeWasson)

跨站点请求伪造 (CSRF) 是一种攻击，恶意站点发送请求到易受攻击的站点在当前登录用户

下面是 CSRF 攻击的一个例子：

1. 用户登录到`www.example.com`使用窗体身份验证。
2. 服务器对用户进行身份验证。 从服务器响应包括身份验证 cookie。
3. 而无需注销，用户访问恶意网站。 此恶意站点包含以下 HTML 窗体： 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    请注意，窗体操作发到易受攻击的站点，不到的恶意站点。 这是 CSRF 的"跨站点"部分。
4. 用户单击提交按钮。 在浏览器包括与请求的身份验证 cookie。
5. 请求与用户的身份验证上下文，在服务器上运行，并可以执行任何操作允许身份验证的用户执行的操作。

虽然此示例需要用户单击窗体按钮，但恶意页面可以同样轻松地运行自动提交窗体的脚本。 此外，使用 SSL 不会阻止实施 CSRF 攻击，因为恶意站点可以发送"https://"请求。

通常情况下，CSRF 攻击是可能对网站使用 cookie 进行身份验证，因为浏览器向目标网站发送所有相关 cookie。 但是，CSRF 攻击并不局限于利用 cookie。 例如，基本和摘要式身份验证也是易受攻击的。 之后使用基本或摘要式身份验证用户登录。 浏览器自动发送凭据，直到会话结束。

## <a name="anti-forgery-tokens"></a>防伪标记

为了帮助防止 CSRF 攻击，ASP.NET MVC 使用防伪令牌，也称为*请求验证令牌*。

1. 客户端请求包含一个窗体的 HTML 页。
2. 服务器在响应中包含两个令牌。 一个令牌作为 cookie 发送。 其他放置在隐藏窗体字段中。 因此，攻击者无法猜测值，将随机生成令牌。
3. 时客户端提交窗体，它必须将这两个令牌发送回服务器。 客户端发送的 cookie 令牌作为 cookie，然后发送窗体数据中的窗体令牌。 （浏览器客户端自动执行此要求在用户提交窗体时。）
4. 如果请求不包含这两个令牌，该服务器不允许该请求。

下面是使用隐藏的窗体标记 HTML 窗体的示例：

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

防伪标记起作用，因为恶意页面无法读取用户的令牌，由同域策略引起。 ([同域策略](http://www.w3.org/Security/wiki/Same_Origin_Policy)阻止访问彼此的内容的两个不同的站点上托管的文档。 因此在前面的示例中，恶意页可以将请求发送到 example.com，但它无法读取响应。）

若要防止 CSRF 攻击，浏览器以无提示方式发送使用任何身份验证协议使用防伪标记提供凭据后在用户登录。 这包括基于 cookie 的身份验证协议，如窗体身份验证，以及协议，例如基本和摘要式身份验证。

对于任何 nonsafe 方法 （POST、 PUT、 DELETE），应要求防伪令牌。 此外，请确保安全方法 （GET、 HEAD） 没有任何副作用。 此外，如果启用跨域支持，如 CORS 或 JSONP，甚至安全方法，如 GET 则可能容易受到 CSRF 攻击，从而允许攻击者能够读取可能敏感的数据。

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>在 ASP.NET MVC 中的防伪标记

若要将防伪标记添加到 Razor 页面，请使用**HtmlHelper.AntiForgeryToken**帮助器方法：

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

此方法将添加隐藏窗体字段，还会设置 cookie 令牌。

## <a name="anti-csrf-and-ajax"></a>反 CSRF 和 AJAX

窗体令牌可能对 AJAX 请求问题，因为 AJAX 请求可能会发送 JSON 数据，不是 HTML 窗体数据。 一种解决方案是将令牌发送自定义 HTTP 标头中。 下面的代码使用 Razor 语法生成令牌，，然后将令牌添加到 AJAX 请求。 在服务器中通过调用生成令牌**AntiForgery.GetTokens**。

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

当处理该请求时，从请求标头中提取令牌。 然后调用**AntiForgery.Validate**方法用于验证令牌。 **验证**方法将引发异常，如果令牌无效。

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
