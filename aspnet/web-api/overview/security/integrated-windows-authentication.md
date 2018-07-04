---
uid: web-api/overview/security/integrated-windows-authentication
title: 集成 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用集成 Windows 身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/18/2012
ms.topic: article
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: f11b9fe5d98118a252c6c00dd2997b2ee9a3da7a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381598"
---
<a name="integrated-windows-authentication"></a><span data-ttu-id="00735-103">集成的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="00735-103">Integrated Windows Authentication</span></span>
====================
<span data-ttu-id="00735-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="00735-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="00735-105">集成的 Windows 身份验证使用户能够使用其 Windows 凭据，使用 Kerberos 或 NTLM 进行登录。</span><span class="sxs-lookup"><span data-stu-id="00735-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="00735-106">客户端将 Authorization 标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="00735-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="00735-107">Windows 身份验证是最适合 intranet 环境。</span><span class="sxs-lookup"><span data-stu-id="00735-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="00735-108">有关详细信息，请参阅[Windows 身份验证](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。</span><span class="sxs-lookup"><span data-stu-id="00735-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="00735-109">优点</span><span class="sxs-lookup"><span data-stu-id="00735-109">Advantages</span></span> | <span data-ttu-id="00735-110">缺点</span><span class="sxs-lookup"><span data-stu-id="00735-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="00735-111">-内置到 IIS。</span><span class="sxs-lookup"><span data-stu-id="00735-111">- Built into IIS.</span></span> <span data-ttu-id="00735-112">-不在请求中发送的用户凭据。</span><span class="sxs-lookup"><span data-stu-id="00735-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="00735-113">-如果客户端计算机属于域 （例如，intranet 应用程序），用户不必输入凭据。</span><span class="sxs-lookup"><span data-stu-id="00735-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="00735-114">-不建议用于 Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="00735-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="00735-115">-需要 Kerberos 或 NTLM 支持客户端中。</span><span class="sxs-lookup"><span data-stu-id="00735-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="00735-116">客户端必须位于 Active Directory 域中。</span><span class="sxs-lookup"><span data-stu-id="00735-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="00735-117">如果你的应用程序托管在 Azure 上，并且必须在本地 Active Directory 域，请考虑你的本地 AD 与 Azure Active Directory 联合。</span><span class="sxs-lookup"><span data-stu-id="00735-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="00735-118">这样一来，用户可以登录其本地凭据，但由 Azure AD 执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="00735-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="00735-119">有关详细信息，请参阅[Azure 身份验证](../../../visual-studio/overview/2012/windows-azure-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="00735-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>


<span data-ttu-id="00735-120">若要创建使用集成 Windows 身份验证的应用程序，请在 MVC 4 项目向导中选择"Intranet 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="00735-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="00735-121">此项目模板放入 Web.config 文件中的以下设置：</span><span class="sxs-lookup"><span data-stu-id="00735-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="00735-122">集成 Windows 身份验证适用于任何支持的浏览器客户端侧[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)身份验证方案，其中包括大多数主流浏览器。</span><span class="sxs-lookup"><span data-stu-id="00735-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="00735-123">对于.NET 客户端应用程序， **HttpClient**类支持 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="00735-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="00735-124">Windows 身份验证是易受到跨站点请求伪造 (CSRF) 攻击。</span><span class="sxs-lookup"><span data-stu-id="00735-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="00735-125">请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="00735-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
