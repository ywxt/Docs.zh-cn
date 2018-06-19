---
uid: web-api/overview/security/integrated-windows-authentication
title: 集成 Windows 身份验证 |Microsoft 文档
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用集成 Windows 身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/18/2012
ms.topic: article
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: bf5f55d98d61cdfdd246a847f41a6f1c65f00bfc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508156"
---
<a name="integrated-windows-authentication"></a><span data-ttu-id="af05d-103">集成的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="af05d-103">Integrated Windows Authentication</span></span>
====================
<span data-ttu-id="af05d-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="af05d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="af05d-105">集成的 Windows 身份验证使用户能够使用其 Windows 凭据，使用 Kerberos 或 NTLM 进行登录。</span><span class="sxs-lookup"><span data-stu-id="af05d-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="af05d-106">客户端将 Authorization 标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="af05d-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="af05d-107">Windows 身份验证是最适合 intranet 环境。</span><span class="sxs-lookup"><span data-stu-id="af05d-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="af05d-108">有关详细信息，请参阅[Windows 身份验证](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。</span><span class="sxs-lookup"><span data-stu-id="af05d-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="af05d-109">优点</span><span class="sxs-lookup"><span data-stu-id="af05d-109">Advantages</span></span> | <span data-ttu-id="af05d-110">缺点</span><span class="sxs-lookup"><span data-stu-id="af05d-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="af05d-111">的内置于 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="af05d-111">- Built into IIS.</span></span> <span data-ttu-id="af05d-112">-不会在请求中发送的用户凭据。</span><span class="sxs-lookup"><span data-stu-id="af05d-112">- Does not send the user credentials in the request.</span></span> <span data-ttu-id="af05d-113">-如果客户端计算机属于域 （例如，intranet 应用程序），用户不必输入凭据。</span><span class="sxs-lookup"><span data-stu-id="af05d-113">- If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="af05d-114">-不建议用于 Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="af05d-114">- Not recommended for Internet applications.</span></span> <span data-ttu-id="af05d-115">-需要在客户端的 Kerberos 或 NTLM 支持。</span><span class="sxs-lookup"><span data-stu-id="af05d-115">- Requires Kerberos or NTLM support in the client.</span></span> <span data-ttu-id="af05d-116">-客户端必须在 Active Directory 域中。</span><span class="sxs-lookup"><span data-stu-id="af05d-116">- Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="af05d-117">如果你的应用程序托管在 Azure 上具有本地 Active Directory 域，请考虑将你的本地 AD 与 Azure Active Directory 联合。</span><span class="sxs-lookup"><span data-stu-id="af05d-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="af05d-118">这样一来，用户可以登录其本地凭据，但由 Azure AD 执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="af05d-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="af05d-119">有关详细信息，请参阅[Azure 身份验证](../../../visual-studio/overview/2012/windows-azure-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="af05d-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>


<span data-ttu-id="af05d-120">若要创建使用集成 Windows 身份验证的应用程序，请在 MVC 4 项目向导中选择"Intranet 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="af05d-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="af05d-121">此项目模板将放置在 Web.config 文件的以下设置：</span><span class="sxs-lookup"><span data-stu-id="af05d-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="af05d-122">在客户端集成 Windows 身份验证适用于任何支持的浏览器[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)身份验证方案，其中包括大多数主要的浏览器。</span><span class="sxs-lookup"><span data-stu-id="af05d-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="af05d-123">对于.NET 客户端应用程序， **HttpClient**类支持 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="af05d-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="af05d-124">Windows 身份验证是易受到跨站点请求伪造 (CSRF) 攻击。</span><span class="sxs-lookup"><span data-stu-id="af05d-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="af05d-125">请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="af05d-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
