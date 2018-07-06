---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 阻止打开重定向攻击 (C#) |Microsoft Docs
author: jongalloway
description: 本教程介绍了如何在 ASP.NET MVC 应用程序中阻止打开重定向攻击。 本教程讨论所做的更改...
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 33d2d050805d9b65741c121cdb2b65a59e1ea392
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813195"
---
<a name="preventing-open-redirection-attacks-c"></a>阻止打开重定向攻击 (C#)
====================
通过[Jon Galloway](https://github.com/jongalloway)

> 本教程介绍了如何在 ASP.NET MVC 应用程序中阻止打开重定向攻击。 本教程讨论在 AccountController 中在 ASP.NET MVC 3 中所做的更改，并演示如何在现有的 ASP.NET MVC 1.0 和 2 个应用程序中应用这些更改。


## <a name="what-is-an-open-redirection-attack"></a>打开重定向攻击是什么？

将重定向到的 URL，例如查询字符串或窗体数据的请求通过指定任何 web 应用程序可以有可能被篡改，同时将用户重定向到恶意的外部 URL。 此篡改称为开放重定向攻击。

每当应用程序逻辑将重定向到指定的 URL，必须验证重定向 URL 尚未被篡改。 为 ASP.NET MVC 1.0 和 ASP.NET MVC 2 默认 AccountController 中使用的登录名是易受攻击，以打开重定向攻击。 幸运的是，很容易地更新现有的应用程序以使用从 ASP.NET MVC 3 预览版的更正。

若要了解此漏洞，让我们看一下默认 ASP.NET MVC 2 Web 应用程序项目中的登录重定向工作原理。 在此应用程序，尝试访问具有 [Authorize] 特性的控制器操作将重定向未经授权的用户到 /Account/LogOn 视图。 此重定向到 /Account/LogOn，以便用户可以返回到最初请求的 URL，它们已成功登录后将 returnUrl 查询字符串参数。

在下面的屏幕截图，我们可以看到，尝试访问 /Account/ChangePassword 视图未登录时导致重定向到 /Account/LogOn？ReturnUrl = %2faccount%2fChangePassword %2f。

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**图 01**： 支持开放重定向的登录页

由于不验证 ReturnUrl 查询字符串参数，因此攻击者可以修改它以将任何 URL 地址注入到要执行的开放重定向攻击的参数。 若要说明这一点，我们可以修改的 ReturnUrl 参数[ http://bing.com ](http://bing.com)，因此将生成的登录名 URL/帐户/登录？ReturnUrl =<http://www.bing.com/>。 在成功登录到站点后, 我们将重定向到[ http://bing.com ](http://bing.com)。 由于不验证此重定向，因此它可以改为指向恶意站点，试图欺骗用户。

### <a name="a-more-complex-open-redirection-attack"></a>更复杂的开放重定向攻击

打开重定向攻击是尤其危险，因为攻击者知道，我们正在尝试登录到特定的网站，这将使我们受到[钓鱼攻击](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)。 例如，攻击者可能发送恶意电子邮件向网站用户在尝试捕获其密码。 让我们看看这工作原理 NerdDinner 站点上。 （请注意，已更新 NerdDinner 现场开放重定向攻击。）

首先，攻击者向我们发送一个链接到 NerdDinner 包括重定向到其伪造的页面上的登录页：

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

请注意，返回 URL 指向 nerddiner.com，缺少"n"从 word dinner。 在此示例中，这是，攻击者控制的域。 当我们访问上面的链接时，我们会转到合法 NerdDinner.com 登录页。

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**图 02**: NerdDinner 的开放重定向的登录页

我们正确登录时，ASP.NET MVC AccountController 的登录操作将重我们定向到 returnUrl 查询字符串参数中指定的 URL。 在这种情况下，它是攻击者已进入，即的 URL [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)。 除非我们非常密切，它是很有可能，我们不会发现此问题，特别是因为攻击者已小心，确保其伪造的页面看起来完全一样的合法的登录页。 此登录页包括错误消息，请求我们再次登录。 不太妥当我们，我们必须有误我们的密码。

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**图 03**： 伪造 NerdDinner 登录屏幕

当我们重新键入我们的用户名和密码时，伪造的登录页会将信息保存，并向我们发送回合法 NerdDinner.com 站点。 此时，NerdDinner.com 站点具有已进行身份验证，因而伪造的登录页可以直接访问该页面将重定向。 最终结果是，攻击者有我们的用户名和密码，并且我们不知道，我们已向其提供它。

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>查看 AccountController 登录操作中的易受攻击代码

ASP.NET MVC 2 应用程序中的登录操作的代码如下所示。 请注意，一旦成功登录，将控制器返回重定向到 returnUrl。 您可以看到针对 returnUrl 参数执行任何验证。

**代码清单 1 – 在 ASP.NET MVC 2 登录操作 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

现在让我们看看对 ASP.NET MVC 3 登录操作的更改。 此代码已更改，以便通过名为 System.Web.Mvc.Url 帮助程序类中调用新方法验证 returnUrl 参数`IsLocalUrl()`。

**代码清单 2 – 在 ASP.NET MVC 3 登录操作 `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

这已更改为在 System.Web.Mvc.Url 帮助程序类中，调用新方法来验证返回 URL 参数`IsLocalUrl()`。

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>保护 ASP.NET MVC 1.0 和 MVC 2 应用程序

我们可以利用 ASP.NET MVC 3 更改我们现有的 ASP.NET MVC 1.0 和 2 个应用程序中通过添加 IsLocalUrl() 帮助器方法并更新要验证的 returnUrl 参数的登录操作。

ASP.NET Web Pages 应用程序还使用 UrlHelper IsLocalUrl() 方法实际上就调用中 System.Web.WebPages，作为此验证的方法。

**代码清单 3 – 从 ASP.NET MVC 3 UrlHelper IsLocalUrl() 方法 `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

IsUrlLocalToHost 方法包含的实际验证逻辑，如列表 4 中所示。

**列表 4 – 从 System.Web.WebPages 为 RequestExtensions 类 IsUrlLocalToHost() 方法**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

在我们的 ASP.NET MVC 1.0 或 2 个应用程序中，我们将向 AccountController 中，添加 IsLocalUrl() 方法，但最好尽可能将其添加到一个单独的帮助器类。 我们将两个较小的更改 IsLocalUrl() 的 ASP.NET MVC 3 版本，以便它将在 AccountController 中工作。 首先，我们将更改它通过公共方法为私有方法，因为控制器中的公共方法可作为控制器操作进行访问。 其次，我们将修改检查针对应用程序主机 URL 主机的调用。 调用将使用的本地 RequestContext UrlHelper 类中的字段。 而不是使用这种情况。RequestContext.HttpContext.Request.Url.Host，我们将使用它。Request.Url.Host。 下面的代码演示在 ASP.NET MVC 1.0 和 2 个应用程序与控制器类一起使用的已修改的 IsLocalUrl() 方法。

**列表 5 – IsLocalUrl() 方法，这被修改用于 MVC 控制器类**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

现在 IsLocalUrl() 方法已准备就绪，我们可以调用它从我们的登录操作来验证该 returnUrl 参数，如下面的代码中所示。

**代码清单 6 – Updated 登录方法验证 returnUrl 参数**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

现在我们可以通过尝试使用外部的返回 URL 登录测试打开重定向攻击。 让我们使用 /Account/LogOn？ReturnUrl =<http://www.bing.com/>试。

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**图 04**： 测试更新后的登录操作

已成功登录后，我们将重定向到 Home/Index 控制器操作而不是外部 URL。

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**图 05**： 犬队击败开放重定向攻击

## <a name="summary"></a>总结

重定向 Url 作为应用程序的 URL 中的参数传递时，会发生开放重定向攻击。 ASP.NET MVC 3 模板包括代码，以防止打开重定向攻击。 您可以添加此代码进行一些修改后对 ASP.NET MVC 1.0 和 2 个应用程序。 若要防止打开重定向攻击到 ASP.NET 1.0 和 2 个应用程序进行日志记录时，将 IsLocalUrl() 方法添加并验证的登录操作中的 returnUrl 参数。
