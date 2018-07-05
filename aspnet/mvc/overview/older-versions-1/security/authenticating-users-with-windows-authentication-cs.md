---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: 使用 Windows 身份验证 (C#) 的用户进行身份验证 |Microsoft Docs
author: microsoft
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 了解如何启用 Windows 身份验证应用程序的 web 共同中...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 0261f3b989d721e6e9aae8fa5766e02c8bca7b63
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397795"
---
<a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="2e40e-104">使用 Windows 身份验证 (C#) 的用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="2e40e-104">Authenticating Users with Windows Authentication (C#)</span></span>
====================
<span data-ttu-id="2e40e-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2e40e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2e40e-106">了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="2e40e-107">将了解如何启用应用程序的 web 配置文件中的 Windows 身份验证以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="2e40e-108">最后，您将了解如何使用 [Authorize] 特性来限制对特定 Windows 用户或组的控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="2e40e-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>


<span data-ttu-id="2e40e-109">本教程的目的是说明如何可以充分利用的安全功能内置于 Internet 信息服务为密码保护您的 MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="2e40e-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="2e40e-110">了解如何允许控制器操作只能由特定 Windows 用户或用户特定的 Windows 组成员的调用。</span><span class="sxs-lookup"><span data-stu-id="2e40e-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="2e40e-111">时生成的内部公司网站 （intranet 站点） 和你希望用户能够使用其标准的 Windows 用户名和密码访问网站时，使用 Windows 身份验证非常有用。</span><span class="sxs-lookup"><span data-stu-id="2e40e-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="2e40e-112">如果要构建面向网站 （Internet 网站） 向外应用，请考虑改为使用 Forms 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="2e40e-113">启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="2e40e-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="2e40e-114">在创建新的 ASP.NET MVC 应用程序时，默认情况下未启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="2e40e-115">窗体身份验证是启用的 MVC 应用程序的默认身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="2e40e-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="2e40e-116">通过修改 MVC 应用程序的 web 配置 (web.config) 文件，必须启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="2e40e-117">查找&lt;身份验证&gt;部分，并修改它以使用 Windows，而不是像这样的窗体身份验证：</span><span class="sxs-lookup"><span data-stu-id="2e40e-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="2e40e-118">当启用 Windows 身份验证时，你的 web 服务器将成为负责用户身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="2e40e-119">通常情况下，有两种不同类型的创建和部署 ASP.NET MVC 应用程序时使用的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2e40e-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="2e40e-120">首先，在开发的 MVC 应用程序时，使用 Visual Studio 附带的 ASP.NET 开发 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2e40e-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="2e40e-121">默认情况下，ASP.NET 开发 Web 服务器的当前 Windows 帐户 （用于登录到 Windows 任何帐户） 的上下文中执行的所有页面。</span><span class="sxs-lookup"><span data-stu-id="2e40e-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="2e40e-122">ASP.NET Development Web Server 还支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="2e40e-123">可以通过右键单击解决方案资源管理器窗口中项目的名称并选择属性启用 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="2e40e-124">接下来，选择 Web 选项卡并选中 NTLM 复选框 （见图 1）。</span><span class="sxs-lookup"><span data-stu-id="2e40e-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="2e40e-125">**图 1 – 启用 NTLM 身份验证的 ASP.NET 开发 Web 服务器**</span><span class="sxs-lookup"><span data-stu-id="2e40e-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="2e40e-127">生产 web 应用程序，在手，你使用 IIS 作为 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2e40e-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="2e40e-128">IIS 支持多种类型的身份验证包括：</span><span class="sxs-lookup"><span data-stu-id="2e40e-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="2e40e-129">基本身份验证 – 定义为 HTTP 1.0 协议的一部分。</span><span class="sxs-lookup"><span data-stu-id="2e40e-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="2e40e-130">在 Internet 上以明文形式 (Base64 编码) 发送用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="2e40e-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="2e40e-131">-摘要式身份验证 – 发送密码，而不是密码本身，在 internet 上的哈希。</span><span class="sxs-lookup"><span data-stu-id="2e40e-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="2e40e-132">-集成 Windows (NTLM) 身份验证 – 要在使用 windows 的 intranet 环境中使用的身份验证的最佳类型。</span><span class="sxs-lookup"><span data-stu-id="2e40e-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="2e40e-133">-证书身份验证 – 启用身份验证使用客户端证书。</span><span class="sxs-lookup"><span data-stu-id="2e40e-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="2e40e-134">将证书映射到 Windows 用户帐户。</span><span class="sxs-lookup"><span data-stu-id="2e40e-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2e40e-135">有关这些不同类型的身份验证的更详细概述，请参阅[ https://msdn.microsoft.com/library/aa292114(VS.71).aspx ](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e40e-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>


<span data-ttu-id="2e40e-136">可以使用 Internet 信息服务管理器以启用特定类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="2e40e-137">请注意，所有类型的身份验证都并不在每个操作系统的情况下可用。</span><span class="sxs-lookup"><span data-stu-id="2e40e-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="2e40e-138">此外，如果使用 Windows Vista 使用 IIS 7.0，您需要启用不同类型的 Windows 身份验证，才会显示在 Internet 信息服务管理器中。</span><span class="sxs-lookup"><span data-stu-id="2e40e-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="2e40e-139">打开**控制面板、 程序、 程序和功能，启用 Windows 功能打开或关闭**，展开 Internet 信息服务节点 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="2e40e-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="2e40e-140">**图 2 – 启用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="2e40e-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="2e40e-142">使用 Internet 信息服务，可以启用或禁用不同类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="2e40e-143">例如，图 3 说明禁用匿名身份验证和启用集成 Windows (NTLM) 身份验证时使用的 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="2e40e-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="2e40e-144">**图 3 – 启用集成的 Windows 身份验证**</span><span class="sxs-lookup"><span data-stu-id="2e40e-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="2e40e-146">授权 Windows 用户和组</span><span class="sxs-lookup"><span data-stu-id="2e40e-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="2e40e-147">启用 Windows 身份验证后，可以使用 [Authorize] 属性来控制对控制器或控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="2e40e-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="2e40e-148">此特性可以应用于整个 MVC 控制器或特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="2e40e-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="2e40e-149">例如，在列表 1 中的 Home 控制器将公开名为 index （）、 CompanySecrets() 和 StephenSecrets() 的三个操作。</span><span class="sxs-lookup"><span data-stu-id="2e40e-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="2e40e-150">任何人都可以调用 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="2e40e-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="2e40e-151">但是，只有 Windows 本地管理员组的成员可以调用 CompanySecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="2e40e-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="2e40e-152">最后，只有名为 Stephen （在雷德蒙德域中） 的 Windows 域用户可以调用 StephenSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="2e40e-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="2e40e-153">**代码清单 1 – Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="2e40e-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="2e40e-154">由于 Windows 用户帐户控制 (UAC)，在使用 Windows Vista 或 Windows Server 2008 时，本地 Administrators 组将行为不同于其他组。</span><span class="sxs-lookup"><span data-stu-id="2e40e-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="2e40e-155">[Authorize] 属性不会正确识别本地 Administrators 组的成员，除非您修改您的计算机的 UAC 设置。</span><span class="sxs-lookup"><span data-stu-id="2e40e-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>


<span data-ttu-id="2e40e-156">完全时会发生什么情况尝试调用控制器操作不是正确的权限取决于启用了身份验证的类型。</span><span class="sxs-lookup"><span data-stu-id="2e40e-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="2e40e-157">默认情况下，使用 ASP.NET 开发服务器时，你只收到一个空白页。</span><span class="sxs-lookup"><span data-stu-id="2e40e-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="2e40e-158">使用提供页面**401 未授权**HTTP 响应状态。</span><span class="sxs-lookup"><span data-stu-id="2e40e-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="2e40e-159">如果，但是，将 IIS 用于匿名身份验证已禁用和启用，基本身份验证，则不断收到登录对话框提示每次请求受保护的页面 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="2e40e-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="2e40e-160">**图 4 – 基本身份验证登录对话框**</span><span class="sxs-lookup"><span data-stu-id="2e40e-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="2e40e-162">总结</span><span class="sxs-lookup"><span data-stu-id="2e40e-162">Summary</span></span>

<span data-ttu-id="2e40e-163">本教程介绍了如何在 ASP.NET MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="2e40e-164">您学习了如何启用应用程序的 web 配置文件中的 Windows 身份验证以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="2e40e-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="2e40e-165">最后，您学习了如何使用 [Authorize] 特性来限制对特定 Windows 用户或组的控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="2e40e-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2e40e-166">[上一页](authenticating-users-with-forms-authentication-cs.md)
> [下一页](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2e40e-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>
