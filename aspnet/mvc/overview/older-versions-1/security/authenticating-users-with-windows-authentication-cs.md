---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: 使用 Windows 身份验证 (C#) 的用户进行身份验证 |Microsoft 文档
author: microsoft
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 了解如何启用 Windows 身份验证在你的应用程序 web co...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 140d2232f7826e178301d1d2064e12657be23385
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875378"
---
<a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="4d537-104">使用 Windows 身份验证 (C#) 的用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="4d537-104">Authenticating Users with Windows Authentication (C#)</span></span>
====================
<span data-ttu-id="4d537-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4d537-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4d537-106">了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="4d537-107">你了解如何启用应用程序的 web 配置文件中的 Windows 身份验证以及如何使用 IIS 中配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="4d537-108">最后，你将了解如何使用 [Authorize] 属性来限制对特定 Windows 用户或组的控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="4d537-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>


<span data-ttu-id="4d537-109">本教程旨在说明如何可以充分利用的安全功能内置于 Internet Information Services 到密码保护 MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="4d537-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="4d537-110">了解如何让控制器操作只能由特定 Windows 用户或用户特定的 Windows 组成员的调用。</span><span class="sxs-lookup"><span data-stu-id="4d537-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="4d537-111">使用 Windows 身份验证时有意义，您构建了一个内部公司网站 （intranet 站点） 和您希望用户能够访问网站时使用其标准的 Windows 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="4d537-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="4d537-112">如果你在构建面向网站 （Internet 网站） 外，请考虑改为使用 Forms 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="4d537-113">启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="4d537-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="4d537-114">在创建新的 ASP.NET MVC 应用程序时，默认情况下未启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="4d537-115">窗体身份验证是启用的 MVC 应用程序的默认身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="4d537-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="4d537-116">通过修改 MVC 应用程序的 web 配置 (web.config) 文件，必须启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="4d537-117">查找&lt;身份验证&gt;部分，然后修改它以使用 Windows，而不是这样的窗体身份验证：</span><span class="sxs-lookup"><span data-stu-id="4d537-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="4d537-118">当你启用 Windows 身份验证时，你的 web 服务器将成为负责对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="4d537-119">通常，有两种不同类型的创建和部署 ASP.NET MVC 应用程序时，你使用的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4d537-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="4d537-120">首先，在开发的 MVC 应用程序时，你使用 Visual Studio 所含的 ASP.NET 开发 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4d537-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="4d537-121">默认情况下，ASP.NET 开发 Web 服务器的当前 Windows 帐户 （无论你用于登录到 Windows 帐户） 的上下文中执行所有页面。</span><span class="sxs-lookup"><span data-stu-id="4d537-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="4d537-122">ASP.NET 开发 Web 服务器还支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="4d537-123">你可以通过右键单击解决方案资源管理器窗口中的项目的名称并选择属性来启用 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="4d537-124">接下来，选择 Web 选项卡并选中 NTLM 复选框 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="4d537-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="4d537-125">**图 1 – 启用 ASP.NET 开发 Web 服务器的 NTLM 身份验证**</span><span class="sxs-lookup"><span data-stu-id="4d537-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="4d537-127">生产 web 应用程序，在手的形状，你使用 IIS 作为 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4d537-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="4d537-128">IIS 支持多种类型的身份验证包括：</span><span class="sxs-lookup"><span data-stu-id="4d537-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="4d537-129">基本身份验证 – 定义为 HTTP 1.0 协议的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d537-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="4d537-130">通过 Internet 以明文形式 (Base64 编码) 发送用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="4d537-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="4d537-131">-摘要式身份验证-发送密码，而不是本身，在 internet 上的密码哈希的值。</span><span class="sxs-lookup"><span data-stu-id="4d537-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="4d537-132">-集成 Windows (NTLM) 身份验证 – 要在使用 windows 的 intranet 环境中使用的身份验证的最佳类型。</span><span class="sxs-lookup"><span data-stu-id="4d537-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="4d537-133">-证书身份验证 – 启用身份验证使用客户端证书。</span><span class="sxs-lookup"><span data-stu-id="4d537-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="4d537-134">证书映射到 Windows 用户帐户。</span><span class="sxs-lookup"><span data-stu-id="4d537-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4d537-135">有关这些不同类型的身份验证的详细概述，请参阅[ https://msdn.microsoft.com/library/aa292114(VS.71).aspx ](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="4d537-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>


<span data-ttu-id="4d537-136">Internet Information Services 管理器可用于启用特定类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="4d537-137">请注意，所有类型的身份验证都不可用对于每个操作系统。</span><span class="sxs-lookup"><span data-stu-id="4d537-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="4d537-138">此外，如果您正在使用 Windows Vista IIS 7.0，你将需要启用 Windows 身份验证的不同类型，它们显示在 Internet Information Services 管理器中之前。</span><span class="sxs-lookup"><span data-stu-id="4d537-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="4d537-139">打开**控制面板、 程序、 程序和功能，打开或关闭 Windows 功能**，然后展开 Internet 信息服务节点 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="4d537-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="4d537-140">**图 2 – 启用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="4d537-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="4d537-142">使用 Internet Information Services，可以启用或禁用不同类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="4d537-143">例如，图 3 说明禁用匿名身份验证和启用集成 Windows (NTLM) 身份验证时使用的 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="4d537-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="4d537-144">**图 3 – 启用集成的 Windows 身份验证**</span><span class="sxs-lookup"><span data-stu-id="4d537-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="4d537-146">授权 Windows 用户和组</span><span class="sxs-lookup"><span data-stu-id="4d537-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="4d537-147">启用 Windows 身份验证后，你可以使用 [Authorize] 属性来控制对控制器或控制器操作访问。</span><span class="sxs-lookup"><span data-stu-id="4d537-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="4d537-148">此特性可以应用于整个的 MVC 控制器或特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="4d537-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="4d537-149">例如，列表 1 中的主页控制器公开名为 index （）、 CompanySecrets() 和 StephenSecrets() 的三个操作。</span><span class="sxs-lookup"><span data-stu-id="4d537-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="4d537-150">任何人都可以调用 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="4d537-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="4d537-151">但是，只有 Windows 本地管理员组的成员可以调用 CompanySecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="4d537-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="4d537-152">最后，仅指定 Stephen （在 Redmond 域中） 的 Windows 域用户可以调用 StephenSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="4d537-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="4d537-153">**列表 1 – Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="4d537-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="4d537-154">由于 Windows 用户帐户控制 (UAC)，使用 Windows Vista 或 Windows Server 2008 时，本地 Administrators 组将行为与其他组不同。</span><span class="sxs-lookup"><span data-stu-id="4d537-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="4d537-155">[Authorize] 属性不会正确识别本地 Administrators 组的成员，除非你修改你的计算机的 UAC 设置。</span><span class="sxs-lookup"><span data-stu-id="4d537-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>


<span data-ttu-id="4d537-156">完全时会发生什么情况你尝试在不正确的权限调用的控制器操作取决于启用身份验证的类型。</span><span class="sxs-lookup"><span data-stu-id="4d537-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="4d537-157">使用 ASP.NET 开发服务器时，默认情况下，你只会收到一个空白页。</span><span class="sxs-lookup"><span data-stu-id="4d537-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="4d537-158">使用提供的页面**401 未授权**HTTP 响应状态。</span><span class="sxs-lookup"><span data-stu-id="4d537-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="4d537-159">如果，另一方面，你将 IIS 用于匿名身份验证禁用和启用，基本身份验证，则不断遇到登录对话框提示你请求的受保护的页每次 （参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="4d537-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="4d537-160">**图 4 – 基本身份验证登录对话框**</span><span class="sxs-lookup"><span data-stu-id="4d537-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="4d537-162">总结</span><span class="sxs-lookup"><span data-stu-id="4d537-162">Summary</span></span>

<span data-ttu-id="4d537-163">本教程所述的 ASP.NET MVC 应用程序的上下文中，你就可以使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="4d537-164">您学习了如何启用应用程序的 web 配置文件中的 Windows 身份验证以及如何使用 IIS 中配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="4d537-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="4d537-165">最后，您学习了如何使用 [Authorize] 属性来限制对特定 Windows 用户或组的控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="4d537-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d537-166">[上一页](authenticating-users-with-forms-authentication-cs.md)
> [下一页](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="4d537-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>
