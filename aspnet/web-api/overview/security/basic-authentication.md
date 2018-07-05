---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用基本身份验证。
ms.author: aspnetcontent
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 035baec7c56c0bf6eaacd26ea5192faf2ed6e932
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829582"
---
<a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的基本身份验证
====================
通过[Mike Wasson](https://github.com/MikeWasson)

在中定义基本身份验证[RFC 2617、 HTTP 身份验证： 基本和摘要式访问身份验证](http://www.ietf.org/rfc/rfc2617.txt)。

缺点

- 在请求中发送用户凭据。
- 以纯文本形式发送凭据。
- 与每个请求发送凭据。
- 无法注销，除非通过浏览器会话结束。
- 易受到跨站点请求伪造 (CSRF);需要反 CSRF 的度量值。

优点

- Internet 标准。
- 支持所有主要浏览器。
- 相对简单的协议。

基本身份验证的工作方式如下：

1. 如果请求需要身份验证，则服务器将返回 401 （未经授权）。 响应包括 Www-authenticate 标头，该值指示服务器支持基本身份验证。
2. 客户端将发送另一个请求，授权标头中的客户端凭据。 凭据的格式为"名称： password"base64 编码的字符串。 未加密的凭据。

"Realm。"的上下文中执行基本身份验证 服务器 Www-authenticate 标头中包含的领域的名称。 用户的凭据是在该领域内有效。 是领域的确切的作用域是由服务器。 例如，您可能对分区资源定义几个领域。

![](basic-authentication/_static/image1.png)

因为将凭据发送未加密，基本身份验证才安全通过 HTTPS。 请参阅[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。

基本身份验证也容易受到 CSRF 攻击。 用户输入凭据后，浏览器会自动将它们发送在后续请求到同一个域中，会话的持续时间。 这包括 AJAX 请求。 请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。

## <a name="basic-authentication-with-iis"></a>使用 IIS 基本身份验证

IIS 支持基本身份验证，但需要特别注意： 用户对其 Windows 凭据进行身份验证。 这意味着用户必须具有服务器的域帐户。 对于面向公众的网站，通常需要针对 ASP.NET 成员资格提供程序进行身份验证。

若要启用使用 IIS 的基本身份验证，请将身份验证模式设置为 ASP.NET 项目的 web.config 文件中的"Windows"中：

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

在此模式下，IIS 使用 Windows 凭据进行身份验证。 此外，还必须启用基本身份验证在 IIS 中。 在 IIS 管理器中，转到功能视图中，选择身份验证，并启用基本身份验证。

![](basic-authentication/_static/image2.png)

在 Web API 项目中，添加`[Authorize]`需要进行身份验证的任何控制器操作的属性。

客户端自行进行身份验证请求中设置授权标头。 浏览器客户端自动执行此步骤。 Nonbrowser 客户端将需要设置标头。

## <a name="basic-authentication-with-custom-membership"></a>使用自定义成员资格进行基本身份验证

如前文所述，内置于 IIS 基本身份验证使用 Windows 凭据。 这意味着您需要在托管服务器上创建为你的用户帐户。 但 internet 应用程序，用户帐户通常存储在外部数据库。

下面的代码如何执行基本身份验证的 HTTP 模块。 您可以轻松地插入 ASP.NET 成员资格提供程序中通过将替换为`CheckPassword`方法，这是在此示例中的虚拟方法。

在 Web API 2 中，应考虑编写[身份验证筛选器](authentication-filters.md)或[OWIN 中间件](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模块。

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

若要启用 HTTP 模块，将以下代码添加到 web.config 文件中**system.webServer**部分：

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

"程序集名称"替换为 （不包括"dll"扩展名） 的程序集的名称。

您应该禁用其他身份验证方案，例如，窗体或 Windows 身份验证。
