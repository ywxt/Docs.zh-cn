---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: "了解 ASP.NET AJAX 身份验证和配置文件应用程序服务 |Microsoft 文档"
author: scottcate
description: "身份验证服务允许用户提供凭据才能接收身份验证 cookie，并为该网关服务以便进行自定义用户..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: 182276f9f91b99beb1ce0fc40dcda1f19376669a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="94030-103">了解 ASP.NET AJAX 身份验证和配置文件应用程序服务</span><span class="sxs-lookup"><span data-stu-id="94030-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>
====================
<span data-ttu-id="94030-104">通过[Scott 类别](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="94030-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="94030-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="94030-105">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="94030-106">身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供的网关服务，以允许自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="94030-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="94030-107">ASP.NET AJAX 身份验证服务的使用是标准 ASP.NET 窗体身份验证，与兼容的因此应用程序当前使用窗体身份验证 （如使用的登录名控制） 将不会中断通过升级到 AJAX 身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="94030-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>


## <a name="introduction"></a><span data-ttu-id="94030-108">介绍</span><span class="sxs-lookup"><span data-stu-id="94030-108">Introduction</span></span>

<span data-ttu-id="94030-109">作为.NET Framework 3.5 的一部分，Microsoft 提供了相当多的环境升级报告中。不只是一个新的开发环境可用，但新的语言集成查询 (LINQ) 功能和其他语言增强功能即将推出。</span><span class="sxs-lookup"><span data-stu-id="94030-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="94030-110">此外，正在作为.NET Framework 基类库的第一类成员包含的其他工具集，值得注意的是 ASP.NET AJAX Extensions 中，一些常见的功能。</span><span class="sxs-lookup"><span data-stu-id="94030-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="94030-111">这些扩展使许多新的丰富的客户端功能，包括部分呈现页，而无需完整的页面刷新，能够通过 （包括 ASP.NET 分析 API） 的客户端脚本和广泛的客户端 API 访问 Web 服务用于镜像许多 ASP.NET 服务器端控件集中所示的控件方案。</span><span class="sxs-lookup"><span data-stu-id="94030-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="94030-112">本白皮书审视的实现和使用 ASP.NET 分析的并窗体身份验证服务当它们公开的 Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions 使窗体身份验证非常轻松地提供支持，因为它 （以及分析服务中） 通过 Web 服务代理脚本公开。</span><span class="sxs-lookup"><span data-stu-id="94030-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="94030-113">AJAX Extensions 还支持通过 AuthenticationServiceManager 类的自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="94030-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="94030-114">此白皮书基于 Visual Studio 2008 Beta 2 版本和.NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="94030-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="94030-115">此白皮书还假定你将使用 Visual Studio 2008 Beta 2，不 Visual Web Developer Express，并且将提供根据 Visual Studio 的用户界面的演练。</span><span class="sxs-lookup"><span data-stu-id="94030-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="94030-116">一些代码示例可能利用 Visual Web Developer 学习版中不可用的项目模板。</span><span class="sxs-lookup"><span data-stu-id="94030-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="94030-117">*配置文件和身份验证*</span><span class="sxs-lookup"><span data-stu-id="94030-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="94030-118">Microsoft ASP.NET 配置文件和身份验证服务由 ASP.NET 窗体身份验证系统，并且是标准的 ASP.NET 组件。</span><span class="sxs-lookup"><span data-stu-id="94030-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="94030-119">使用 ASP.NET AJAX Extensions 提供对这些服务通过脚本代理，通过在客户端 AJAX 库的 Sys.Services 命名空间下模型非常简单的脚本访问。</span><span class="sxs-lookup"><span data-stu-id="94030-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="94030-120">身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供的网关服务，以允许自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="94030-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="94030-121">ASP.NET AJAX 身份验证服务的使用是标准 ASP.NET 窗体身份验证，与兼容的因此应用程序当前使用窗体身份验证 （如使用的登录名控制） 将不会中断通过升级到 AJAX 身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="94030-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="94030-122">配置文件服务允许自动集成和根据成员资格，身份验证服务所提供的用户数据的存储。</span><span class="sxs-lookup"><span data-stu-id="94030-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="94030-123">Web.config 文件中，指定存储的数据和各种的分析服务提供程序处理的数据管理。</span><span class="sxs-lookup"><span data-stu-id="94030-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="94030-124">与身份验证服务，AJAX 配置文件服务适用于标准 ASP.NET 配置文件服务，以便不应由于包括 AJAX 支持中断当前特有的功能的 ASP.NET 配置文件服务的页。</span><span class="sxs-lookup"><span data-stu-id="94030-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="94030-125">并入应用程序的 ASP.NET 身份验证和分析服务本身是本白皮书的范围之外。</span><span class="sxs-lookup"><span data-stu-id="94030-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="94030-126">有关主题的详细信息，请参阅 MSDN 库引用文章在使用成员资格管理用户[https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94030-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="94030-127">ASP.NET 还包括一个实用工具来自动将使用 SQL Server，这是默认身份验证服务提供程序的 ASP.NET 成员身份的成员资格设置。</span><span class="sxs-lookup"><span data-stu-id="94030-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="94030-128">有关详细信息，请参阅文章 ASP.NET SQL 服务器注册工具 (Aspnet\_regsql.exe) 在[https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span><span class="sxs-lookup"><span data-stu-id="94030-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="94030-129">*使用 ASP.NET AJAX 身份验证服务*</span><span class="sxs-lookup"><span data-stu-id="94030-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="94030-130">必须在 web.config 文件中启用 ASP.NET AJAX 身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="94030-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="94030-131">身份验证服务都需要 ASP.NET 窗体身份验证启用并且需要在客户端浏览器 （一个脚本无法启用无 cookie 会话由于无 cookie 会话需要 URL 参数） 上启用的 cookie。</span><span class="sxs-lookup"><span data-stu-id="94030-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="94030-132">一旦启用了 AJAX 身份验证服务，并将其配置上，客户端脚本可以立即充分利用 Sys.Services.AuthenticationService 对象。</span><span class="sxs-lookup"><span data-stu-id="94030-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="94030-133">主要的是，客户端脚本将想要利用`login`方法和`isLoggedIn`属性。</span><span class="sxs-lookup"><span data-stu-id="94030-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="94030-134">存在几个属性对于登录方法，可以接受的参数数量大提供默认值。</span><span class="sxs-lookup"><span data-stu-id="94030-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="94030-135">*Sys.Services.AuthenticationService 成员*</span><span class="sxs-lookup"><span data-stu-id="94030-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="94030-136">*login 方法：*</span><span class="sxs-lookup"><span data-stu-id="94030-136">*login method:*</span></span>

<span data-ttu-id="94030-137">Login （） 方法开始的请求进行身份验证用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="94030-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="94030-138">此方法是异步的不会阻止执行。</span><span class="sxs-lookup"><span data-stu-id="94030-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="94030-139">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-139">*Parameters:*</span></span>

| <span data-ttu-id="94030-140">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-140">**Parameter Name**</span></span> | <span data-ttu-id="94030-141">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-142">userName</span><span class="sxs-lookup"><span data-stu-id="94030-142">userName</span></span> | <span data-ttu-id="94030-143">必须的。</span><span class="sxs-lookup"><span data-stu-id="94030-143">Required.</span></span> <span data-ttu-id="94030-144">要进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="94030-144">The username to authenticate.</span></span> |
| <span data-ttu-id="94030-145">密码</span><span class="sxs-lookup"><span data-stu-id="94030-145">password</span></span> | <span data-ttu-id="94030-146">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-146">Optional (defaults to null).</span></span> <span data-ttu-id="94030-147">用户的密码。</span><span class="sxs-lookup"><span data-stu-id="94030-147">The user's password.</span></span> |
| <span data-ttu-id="94030-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="94030-148">isPersistent</span></span> | <span data-ttu-id="94030-149">可选 （默认值为 false）。</span><span class="sxs-lookup"><span data-stu-id="94030-149">Optional (defaults to false).</span></span> <span data-ttu-id="94030-150">是否在会话之间应保持用户的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="94030-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="94030-151">如果为 false，则关闭浏览器或会话过期时用户将可以注销。</span><span class="sxs-lookup"><span data-stu-id="94030-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="94030-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="94030-152">redirectUrl</span></span> | <span data-ttu-id="94030-153">可选 （默认值为 null）。要为身份验证成功后的将浏览器重定向的 URL。</span><span class="sxs-lookup"><span data-stu-id="94030-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="94030-154">如果此参数为 null 或空字符串，则会不发生任何重定向。</span><span class="sxs-lookup"><span data-stu-id="94030-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="94030-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="94030-155">customInfo</span></span> | <span data-ttu-id="94030-156">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-156">Optional (defaults to null).</span></span> <span data-ttu-id="94030-157">此参数是当前未使用，保留待将来使用。</span><span class="sxs-lookup"><span data-stu-id="94030-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="94030-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-158">loginCompletedCallback</span></span> | <span data-ttu-id="94030-159">可选 （默认值为 null）。要在该登录名已成功完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="94030-160">如果指定，此参数将取代 defaultLoginCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="94030-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="94030-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-161">failedCallback</span></span> | <span data-ttu-id="94030-162">可选 （默认值为 null）。要在登录失败时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="94030-163">如果指定，此参数将取代 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="94030-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="94030-164">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-164">userContext</span></span> | <span data-ttu-id="94030-165">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-165">Optional (defaults to null).</span></span> <span data-ttu-id="94030-166">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="94030-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="94030-167">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="94030-167">*Return Value:*</span></span>

<span data-ttu-id="94030-168">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="94030-168">This function does not include a return value.</span></span> <span data-ttu-id="94030-169">但是，有多种行为都是调用的在完成对此函数包括：</span><span class="sxs-lookup"><span data-stu-id="94030-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="94030-170">当前页将被刷新，或者如果更改`redirectUrl`参数已既不为 null，也不为空字符串。</span><span class="sxs-lookup"><span data-stu-id="94030-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="94030-171">但是，如果参数为 null 或空字符串，`loginCompletedCallback`参数，或`defaultLoginCompletedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="94030-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="94030-172">如果对 web 服务调用失败，`failedCallback`参数`defaultFailedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="94030-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="94030-173">*注销方法：*</span><span class="sxs-lookup"><span data-stu-id="94030-173">*logout method:*</span></span>

<span data-ttu-id="94030-174">Logout （） 方法将移除凭据 cookie，并注销当前用户从 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="94030-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="94030-175">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-175">*Parameters:*</span></span>

| <span data-ttu-id="94030-176">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-176">**Parameter Name**</span></span> | <span data-ttu-id="94030-177">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="94030-178">redirectUrl</span></span> | <span data-ttu-id="94030-179">可选 （默认值为 null）。要为身份验证成功后的将浏览器重定向的 URL。</span><span class="sxs-lookup"><span data-stu-id="94030-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="94030-180">如果此参数为 null 或空字符串，则会不发生任何重定向。</span><span class="sxs-lookup"><span data-stu-id="94030-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="94030-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-181">logoutCompletedCallback</span></span> | <span data-ttu-id="94030-182">可选 （默认值为 null）。用于注销已成功完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="94030-183">如果指定，此参数将取代 defaultLogoutCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="94030-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="94030-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-184">failedCallback</span></span> | <span data-ttu-id="94030-185">可选 （默认值为 null）。要在登录失败时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="94030-186">如果指定，此参数将取代 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="94030-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="94030-187">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-187">userContext</span></span> | <span data-ttu-id="94030-188">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-188">Optional (defaults to null).</span></span> <span data-ttu-id="94030-189">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="94030-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="94030-190">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="94030-190">*Return Value:*</span></span>

<span data-ttu-id="94030-191">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="94030-191">This function does not include a return value.</span></span> <span data-ttu-id="94030-192">但是，有多种行为都是调用的在完成对此函数包括：</span><span class="sxs-lookup"><span data-stu-id="94030-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="94030-193">当前页将被刷新，或者如果更改`redirectUrl`参数已既不为 null，也不为空字符串。</span><span class="sxs-lookup"><span data-stu-id="94030-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="94030-194">但是，如果参数为 null 或空字符串，`logoutCompletedCallback`参数，或`defaultLogoutCompletedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="94030-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="94030-195">如果对 web 服务调用失败，`failedCallback`参数`defaultFailedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="94030-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="94030-196">*defaultFailedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="94030-197">此属性指定如果失败与 web 服务进行通信，则应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="94030-198">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-199">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="94030-200">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-200">*Parameters:*</span></span>

| <span data-ttu-id="94030-201">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-201">**Parameter Name**</span></span> | <span data-ttu-id="94030-202">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-203">错误</span><span class="sxs-lookup"><span data-stu-id="94030-203">error</span></span> | <span data-ttu-id="94030-204">指定的错误的信息。</span><span class="sxs-lookup"><span data-stu-id="94030-204">Specifies the error information.</span></span> |
| <span data-ttu-id="94030-205">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-205">userContext</span></span> | <span data-ttu-id="94030-206">指定提供了登录或注销函数调用时的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="94030-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="94030-207">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-207">methodName</span></span> | <span data-ttu-id="94030-208">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-208">The name of the calling method.</span></span> |

<span data-ttu-id="94030-209">*defaultLoginCompletedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="94030-210">此属性指定应在完成登录 web 服务调用时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="94030-211">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-212">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="94030-213">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-213">*Parameters:*</span></span>

| <span data-ttu-id="94030-214">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-214">**Parameter Name**</span></span> | <span data-ttu-id="94030-215">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="94030-216">validCredentials</span></span> | <span data-ttu-id="94030-217">指定用户是否提供有效凭据。</span><span class="sxs-lookup"><span data-stu-id="94030-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="94030-218">`true`如果用户成功登录;否则为`false`。</span><span class="sxs-lookup"><span data-stu-id="94030-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="94030-219">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-219">userContext</span></span> | <span data-ttu-id="94030-220">指定提供调用 login 函数时的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="94030-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="94030-221">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-221">methodName</span></span> | <span data-ttu-id="94030-222">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-222">The name of the calling method.</span></span> |

<span data-ttu-id="94030-223">*defaultLogoutCompletedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="94030-224">此属性指定应完成注销 web 服务调用时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="94030-225">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-226">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="94030-227">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-227">*Parameters:*</span></span>

| <span data-ttu-id="94030-228">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-228">**Parameter Name**</span></span> | <span data-ttu-id="94030-229">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-230">result</span><span class="sxs-lookup"><span data-stu-id="94030-230">result</span></span> | <span data-ttu-id="94030-231">此参数将始终为`null`; 它保留供将来使用。</span><span class="sxs-lookup"><span data-stu-id="94030-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="94030-232">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-232">userContext</span></span> | <span data-ttu-id="94030-233">指定提供调用 login 函数时的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="94030-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="94030-234">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-234">methodName</span></span> | <span data-ttu-id="94030-235">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-235">The name of the calling method.</span></span> |

<span data-ttu-id="94030-236">*isLoggedIn 属性 (get):*</span><span class="sxs-lookup"><span data-stu-id="94030-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="94030-237">此属性获取用户; 的当前身份验证状态它在页请求期间由 ScriptManager 对象设置。</span><span class="sxs-lookup"><span data-stu-id="94030-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="94030-238">此属性返回`true`如果用户当前登录; 否则为它将返回`false`。</span><span class="sxs-lookup"><span data-stu-id="94030-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="94030-239">*路径属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-239">*path property (get, set):*</span></span>

<span data-ttu-id="94030-240">此属性以编程方式确定身份验证 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="94030-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="94030-241">它可以用于重写默认的身份验证提供程序，以及一个在 ScriptManager 控件的认证子节点的路径属性中以声明方式设置 (有关详细信息，请参阅使用自定义身份验证服务提供程序下面的主题）。</span><span class="sxs-lookup"><span data-stu-id="94030-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="94030-242">请注意，默认身份验证服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="94030-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="94030-243">但是，ASP.NET AJAX，可指定 web 服务提供相同的类接口的 ASP.NET AJAX 身份验证服务代理的位置。</span><span class="sxs-lookup"><span data-stu-id="94030-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="94030-244">另请注意，此属性应不设置为一个值，可将脚本请求定向从当前站点中移出。</span><span class="sxs-lookup"><span data-stu-id="94030-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="94030-245">当前应用程序将不会收到的身份验证凭据，因为它可能会毫无用处;此外，技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全性异常。</span><span class="sxs-lookup"><span data-stu-id="94030-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="94030-246">此属性是`String`到身份验证 web 服务中表示该路径的对象。</span><span class="sxs-lookup"><span data-stu-id="94030-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="94030-247">*超时属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="94030-248">此属性确定失败的总时间，假定该登录请求之前等待的身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="94030-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="94030-249">如果在超时到期等待调用完成时，将调用的请求失败的回调，并调用将无法完成。</span><span class="sxs-lookup"><span data-stu-id="94030-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="94030-250">此属性是`Number`对象表示要等待的时间从身份验证服务结果的毫秒数。</span><span class="sxs-lookup"><span data-stu-id="94030-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="94030-251">*代码示例： 登录到身份验证服务*</span><span class="sxs-lookup"><span data-stu-id="94030-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="94030-252">以下标记是一个示例 ASP.NET 页通过简单的脚本调用认证类的登录和注销方法。</span><span class="sxs-lookup"><span data-stu-id="94030-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="94030-253">访问的 ASP.NET 分析数据通过 AJAX</span><span class="sxs-lookup"><span data-stu-id="94030-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="94030-254">通过使用 ASP.NET AJAX Extensions 还公开的 ASP.NET 分析服务。</span><span class="sxs-lookup"><span data-stu-id="94030-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="94030-255">由于 ASP.NET 分析服务提供丰富的细粒度的 API，用于存储和检索用户数据，这可以是一个很好的工作效率工具。</span><span class="sxs-lookup"><span data-stu-id="94030-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="94030-256">必须在 web.config; 中启用配置文件服务它不是默认情况下。</span><span class="sxs-lookup"><span data-stu-id="94030-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="94030-257">为此，请确保`profileService`子元素已启用 = true 指定在 web.config 文件中，并指定哪些属性可以读取或写入，如下所示：</span><span class="sxs-lookup"><span data-stu-id="94030-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="94030-258">此外必须配置配置文件服务。</span><span class="sxs-lookup"><span data-stu-id="94030-258">The profile service must also be configured.</span></span> <span data-ttu-id="94030-259">尽管本白皮书的范围之外是分析服务的配置，但很值得注意的是在配置文件配置设置中定义的组将组名的子属性的可访问性。</span><span class="sxs-lookup"><span data-stu-id="94030-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="94030-260">例如，使用指定的以下配置文件部分：</span><span class="sxs-lookup"><span data-stu-id="94030-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="94030-261">客户端脚本将可以访问作为页面类的属性字段的属性的名称、 Address.Line1、 Address.Line2、 Address.City、 Address.State、 Address.Zip 和 BackgroundColor。</span><span class="sxs-lookup"><span data-stu-id="94030-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="94030-262">AJAX 分析服务配置后，它可立即在页面; 例如：但是，它将需要在使用前一次加载。</span><span class="sxs-lookup"><span data-stu-id="94030-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="94030-263">*Sys.Services.ProfileService 成员*</span><span class="sxs-lookup"><span data-stu-id="94030-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="94030-264">*属性字段：*</span><span class="sxs-lookup"><span data-stu-id="94030-264">*properties field:*</span></span>

<span data-ttu-id="94030-265">属性字段将所有配置的配置文件数据公开为可由.运算符名约定引用的子属性。</span><span class="sxs-lookup"><span data-stu-id="94030-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="94030-266">属性组的子级的属性称为 GroupName.PropertyName。</span><span class="sxs-lookup"><span data-stu-id="94030-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="94030-267">在上面介绍的示例配置文件配置中，以获取状态的用户，你可以使用以下标识符：</span><span class="sxs-lookup"><span data-stu-id="94030-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="94030-268">*load 方法：*</span><span class="sxs-lookup"><span data-stu-id="94030-268">*load method:*</span></span>

<span data-ttu-id="94030-269">从服务器加载选定的列表或所有属性。</span><span class="sxs-lookup"><span data-stu-id="94030-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="94030-270">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-270">*Parameters:*</span></span>

| <span data-ttu-id="94030-271">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-271">**Parameter Name**</span></span> | <span data-ttu-id="94030-272">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="94030-273">propertyNames</span></span> | <span data-ttu-id="94030-274">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-274">Optional (defaults to null).</span></span> <span data-ttu-id="94030-275">要从服务器中加载的属性。</span><span class="sxs-lookup"><span data-stu-id="94030-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="94030-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-276">loadCompletedCallback</span></span> | <span data-ttu-id="94030-277">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-277">Optional (defaults to null).</span></span> <span data-ttu-id="94030-278">要在加载已完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="94030-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-279">failedCallback</span></span> | <span data-ttu-id="94030-280">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-280">Optional (defaults to null).</span></span> <span data-ttu-id="94030-281">要在出错时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="94030-282">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-282">userContext</span></span> | <span data-ttu-id="94030-283">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-283">Optional (defaults to null).</span></span> <span data-ttu-id="94030-284">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="94030-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="94030-285">加载函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="94030-285">The load function does not have a return value.</span></span> <span data-ttu-id="94030-286">如果已成功完成的调用，它将调用`loadCompletedCallback`参数或`defaultLoadCompletedCallback`属性。</span><span class="sxs-lookup"><span data-stu-id="94030-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="94030-287">如果调用失败，或在超时时间已`failedCallback`参数或`defaultFailedCallback`将会调用此属性。</span><span class="sxs-lookup"><span data-stu-id="94030-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="94030-288">如果`propertyNames`未提供参数，从服务器检索所有读取配置的属性。</span><span class="sxs-lookup"><span data-stu-id="94030-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="94030-289">*save 方法：*</span><span class="sxs-lookup"><span data-stu-id="94030-289">*save method:*</span></span>

<span data-ttu-id="94030-290">Save （） 方法将指定的属性列表 （或所有属性） 保存到用户的 ASP.NET 配置文件。</span><span class="sxs-lookup"><span data-stu-id="94030-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="94030-291">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-291">*Parameters:*</span></span>

| <span data-ttu-id="94030-292">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-292">**Parameter Name**</span></span> | <span data-ttu-id="94030-293">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="94030-294">propertyNames</span></span> | <span data-ttu-id="94030-295">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-295">Optional (defaults to null).</span></span> <span data-ttu-id="94030-296">要保存到服务器的属性。</span><span class="sxs-lookup"><span data-stu-id="94030-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="94030-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-297">saveCompletedCallback</span></span> | <span data-ttu-id="94030-298">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-298">Optional (defaults to null).</span></span> <span data-ttu-id="94030-299">要在保存时调用的函数已完成。</span><span class="sxs-lookup"><span data-stu-id="94030-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="94030-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="94030-300">failedCallback</span></span> | <span data-ttu-id="94030-301">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-301">Optional (defaults to null).</span></span> <span data-ttu-id="94030-302">要在出错时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="94030-303">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-303">userContext</span></span> | <span data-ttu-id="94030-304">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="94030-304">Optional (defaults to null).</span></span> <span data-ttu-id="94030-305">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="94030-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="94030-306">保存函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="94030-306">The save function does not have a return value.</span></span> <span data-ttu-id="94030-307">如果调用成功完成，它将调用`saveCompletedCallback`参数或`defaultSaveCompletedCallback`属性。</span><span class="sxs-lookup"><span data-stu-id="94030-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="94030-308">如果调用失败，或在超时时间已`failedCallback`或`defaultFailedCallback`将会调用此属性。</span><span class="sxs-lookup"><span data-stu-id="94030-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="94030-309">如果`propertyNames`参数为 null，所有配置文件属性将发送到服务器，且服务器将确定哪些属性可以保存和哪些不能。</span><span class="sxs-lookup"><span data-stu-id="94030-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="94030-310">*defaultFailedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="94030-311">此属性指定如果失败与 web 服务进行通信，则应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="94030-312">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-313">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="94030-314">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-314">*Parameters:*</span></span>

| <span data-ttu-id="94030-315">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-315">**Parameter Name**</span></span> | <span data-ttu-id="94030-316">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-317">Error</span><span class="sxs-lookup"><span data-stu-id="94030-317">Error</span></span> | <span data-ttu-id="94030-318">指定的错误的信息。</span><span class="sxs-lookup"><span data-stu-id="94030-318">Specifies the error information.</span></span> |
| <span data-ttu-id="94030-319">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-319">userContext</span></span> | <span data-ttu-id="94030-320">指定时提供的用户上下文信息负载或者保存函数进行了调用。</span><span class="sxs-lookup"><span data-stu-id="94030-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="94030-321">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-321">methodName</span></span> | <span data-ttu-id="94030-322">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-322">The name of the calling method.</span></span> |

<span data-ttu-id="94030-323">*defaultSaveCompleted 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="94030-324">此属性指定应在完成保存用户的配置文件数据时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="94030-325">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-326">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="94030-327">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-327">*Parameters:*</span></span>

| <span data-ttu-id="94030-328">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-328">**Parameter Name**</span></span> | <span data-ttu-id="94030-329">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="94030-330">numPropsSaved</span></span> | <span data-ttu-id="94030-331">指定已保存的属性的数目。</span><span class="sxs-lookup"><span data-stu-id="94030-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="94030-332">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-332">userContext</span></span> | <span data-ttu-id="94030-333">指定时提供的用户上下文信息负载或者保存函数进行了调用。</span><span class="sxs-lookup"><span data-stu-id="94030-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="94030-334">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-334">methodName</span></span> | <span data-ttu-id="94030-335">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-335">The name of the calling method.</span></span> |

<span data-ttu-id="94030-336">*defaultLoadCompleted 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="94030-337">此属性指定应用户的配置文件数据的加载完成后调用的函数。</span><span class="sxs-lookup"><span data-stu-id="94030-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="94030-338">它应接收的委托 （或函数引用）。</span><span class="sxs-lookup"><span data-stu-id="94030-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="94030-339">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="94030-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="94030-340">*参数：*</span><span class="sxs-lookup"><span data-stu-id="94030-340">*Parameters:*</span></span>

| <span data-ttu-id="94030-341">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="94030-341">**Parameter Name**</span></span> | <span data-ttu-id="94030-342">**含义**</span><span class="sxs-lookup"><span data-stu-id="94030-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="94030-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="94030-343">numPropsLoaded</span></span> | <span data-ttu-id="94030-344">指定加载的属性数目。</span><span class="sxs-lookup"><span data-stu-id="94030-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="94030-345">userContext</span><span class="sxs-lookup"><span data-stu-id="94030-345">userContext</span></span> | <span data-ttu-id="94030-346">指定时提供的用户上下文信息负载或者保存函数进行了调用。</span><span class="sxs-lookup"><span data-stu-id="94030-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="94030-347">方法名称</span><span class="sxs-lookup"><span data-stu-id="94030-347">methodName</span></span> | <span data-ttu-id="94030-348">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="94030-348">The name of the calling method.</span></span> |

<span data-ttu-id="94030-349">*路径属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-349">*path property (get, set):*</span></span>

<span data-ttu-id="94030-350">此属性以编程方式确定配置文件的 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="94030-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="94030-351">它可以用于重写默认配置文件服务提供程序，以及一个 ScriptManager 控件的页面的子节点的路径属性中以声明方式设置。</span><span class="sxs-lookup"><span data-stu-id="94030-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="94030-352">请注意，默认配置文件服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="94030-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="94030-353">但是，ASP.NET AJAX，可指定 web 服务提供相同的类接口的 ASP.NET AJAX 身份验证服务代理的位置。</span><span class="sxs-lookup"><span data-stu-id="94030-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="94030-354">另请注意，此属性应不设置为一个值，可将脚本请求定向从当前站点中移出。</span><span class="sxs-lookup"><span data-stu-id="94030-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="94030-355">技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全性异常。</span><span class="sxs-lookup"><span data-stu-id="94030-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="94030-356">此属性是`String`到配置文件的 web 服务中表示该路径的对象。</span><span class="sxs-lookup"><span data-stu-id="94030-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="94030-357">*超时属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="94030-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="94030-358">此属性确定失败的总时间假设负载之前，等待配置文件服务或保存请求。</span><span class="sxs-lookup"><span data-stu-id="94030-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="94030-359">如果在超时到期等待调用完成时，将调用的请求失败的回调，并调用将无法完成。</span><span class="sxs-lookup"><span data-stu-id="94030-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="94030-360">此属性是`Number`对象表示要等待的时间从配置文件服务结果的毫秒数。</span><span class="sxs-lookup"><span data-stu-id="94030-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="94030-361">*代码示例： 加载在页面加载配置文件数据*</span><span class="sxs-lookup"><span data-stu-id="94030-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="94030-362">下面的代码将检查是否已验证用户，而如果是这样，它将为页面中加载用户的首选的背景色。</span><span class="sxs-lookup"><span data-stu-id="94030-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="94030-363">*使用自定义身份验证服务提供程序*</span><span class="sxs-lookup"><span data-stu-id="94030-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="94030-364">ASP.NET AJAX 扩展允许您通过公开你通过自定义 web 服务的功能来创建自定义脚本身份验证服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="94030-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="94030-365">为了便于使用，你的 web 服务必须公开两种方法，`Login`和`Logout`; 这些方法都必须指定具有相同的方法签名，在默认 ASP.NET AJAX 身份验证 web 服务。</span><span class="sxs-lookup"><span data-stu-id="94030-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="94030-366">一旦你已创建自定义 web 服务，你将需要指定到其中，是以声明方式在页面上，路径，以编程方式在代码中，或通过客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="94030-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="94030-367">*若要以声明方式设置路径：*</span><span class="sxs-lookup"><span data-stu-id="94030-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="94030-368">若要以声明方式设置的路径，包括 ASP.NET 页上的 ScriptManager 对象的认证子级：</span><span class="sxs-lookup"><span data-stu-id="94030-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="94030-369">*在代码中设置路径：*</span><span class="sxs-lookup"><span data-stu-id="94030-369">*To set the path in code:*</span></span>

<span data-ttu-id="94030-370">若要以编程方式设置的路径，指定通过脚本管理器的实例的路径：</span><span class="sxs-lookup"><span data-stu-id="94030-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="94030-371">*在脚本中设置路径：*</span><span class="sxs-lookup"><span data-stu-id="94030-371">*To set the path in script:*</span></span>

<span data-ttu-id="94030-372">若要在脚本中以编程方式设置路径，利用`path`认证类的属性：</span><span class="sxs-lookup"><span data-stu-id="94030-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="94030-373">*自定义身份验证的示例 Web 服务*</span><span class="sxs-lookup"><span data-stu-id="94030-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="94030-374">摘要</span><span class="sxs-lookup"><span data-stu-id="94030-374">Summary</span></span>

<span data-ttu-id="94030-375">ASP.NET 服务-专门分析、 成员身份和身份验证服务-轻松地向 JavaScript 公开在客户端浏览器上。</span><span class="sxs-lookup"><span data-stu-id="94030-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="94030-376">这允许开发人员其客户端代码使用的身份验证机制无缝集成，而无需根据控件如 UpdatePanels 如何完成的繁重任务。</span><span class="sxs-lookup"><span data-stu-id="94030-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="94030-377">可以从客户端，通过利用 web 配置设置; 保护配置文件数据不会提供默认情况下，数据和开发人员必须选择性加入到配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="94030-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="94030-378">此外，通过使用等效方法签名中创建简化的 web 服务实现，开发人员可以创建自定义脚本提供程序这些内部函数的 ASP.NET 服务。</span><span class="sxs-lookup"><span data-stu-id="94030-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="94030-379">有关这些方法的支持简化了丰富的客户端应用程序，同时开发人员提供了各种各样的灵活性来满足特定需求的开发。</span><span class="sxs-lookup"><span data-stu-id="94030-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="94030-380">*Bio*</span><span class="sxs-lookup"><span data-stu-id="94030-380">*Bio*</span></span>

<span data-ttu-id="94030-381">Scott 类别自 1997 年以来处理与 Microsoft Web 技术，并且是 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 其中他专注于编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。</span><span class="sxs-lookup"><span data-stu-id="94030-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="94030-382">可以通过在电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或在其博客地址[ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="94030-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="94030-383">[上一页](understanding-asp-net-ajax-updatepanel-triggers.md)
[下一页](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="94030-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
