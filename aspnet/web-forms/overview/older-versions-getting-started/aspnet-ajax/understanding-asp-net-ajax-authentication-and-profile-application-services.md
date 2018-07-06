---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 了解 ASP.NET AJAX 身份验证和配置文件应用程序服务 |Microsoft Docs
author: scottcate
description: 身份验证服务允许用户提供凭据才能接收身份验证 cookie，因此网关服务才能允许自定义用户...
ms.author: aspnetcontent
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: 6c08cffacb9ebde6f29398f53b2e568b4bd59d5d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831675"
---
<a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="1e3d4-103">了解 ASP.NET AJAX 身份验证和配置文件应用程序服务</span><span class="sxs-lookup"><span data-stu-id="1e3d4-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>
====================
<span data-ttu-id="1e3d4-104">通过[Scott Cate](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="1e3d4-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="1e3d4-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="1e3d4-105">Download PDF</span></span>](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="1e3d4-106">身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供网关服务才能允许自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="1e3d4-107">ASP.NET AJAX 身份验证服务的使用是标准的 ASP.NET 窗体身份验证与兼容，因此当前使用窗体身份验证的应用程序 （如使用的登录名控制） 将不会断开通过升级到 AJAX 身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>


## <a name="introduction"></a><span data-ttu-id="1e3d4-108">介绍</span><span class="sxs-lookup"><span data-stu-id="1e3d4-108">Introduction</span></span>

<span data-ttu-id="1e3d4-109">作为.NET Framework 3.5 的一部分，Microsoft 提供了一可调整大小的环境升级;不仅是一个新的开发环境可用，而且新的语言集成查询 (LINQ) 功能和其他语言增强功能是即将推出。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="1e3d4-110">此外，一些常见的功能的其他工具集，值得注意的是 ASP.NET AJAX Extensions，都包含为.NET Framework 基类库的一流成员。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="1e3d4-111">使用这些扩展，许多新的丰富的客户端功能，而无需整页刷新，通过客户端脚本 （包括 ASP.NET 分析 API） 和广泛的客户端 API 访问 Web 服务的功能包括部分呈现的页面用于镜像许多 ASP.NET 服务器端控件集所示的控制方案。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="1e3d4-112">本白皮书中介绍的实现和使用 ASP.NET 分析和窗体身份验证服务因为它们由公开 Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions 使窗体身份验证非常简单支持，因为它 （以及分析服务中） 通过 Web 服务代理脚本公开。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="1e3d4-113">AJAX 扩展还支持通过 AuthenticationServiceManager 类的自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="1e3d4-114">此白皮书基于 Visual Studio 2008 Beta 2 版本和.NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="1e3d4-115">本白皮书还假定你将使用 Visual Studio 2008 Beta 2，不 Visual Web Developer 速成版，并且将提供根据 Visual Studio 的用户界面的演练。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="1e3d4-116">一些代码示例可使用项目模板在 Visual Web Developer 速成版中不可用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="1e3d4-117">*配置文件和身份验证*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="1e3d4-118">Microsoft ASP.NET 配置文件和身份验证服务提供的 ASP.NET 窗体身份验证系统，和是标准的 ASP.NET 组件。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="1e3d4-119">ASP.NET AJAX Extensions 提供脚本访问这些服务通过脚本代理，通过 Sys.Services 命名空间下的客户端 AJAX 库的非常简单的模型。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="1e3d4-120">身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供网关服务才能允许自定义用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="1e3d4-121">ASP.NET AJAX 身份验证服务的使用是标准的 ASP.NET 窗体身份验证与兼容，因此当前使用窗体身份验证的应用程序 （如使用的登录名控制） 将不会断开通过升级到 AJAX 身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="1e3d4-122">配置文件服务允许自动集成和基于成员身份，如身份验证服务所提供的用户数据的存储。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="1e3d4-123">Web.config 文件中，指定存储的数据和各种分析服务提供程序处理的数据管理。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="1e3d4-124">与身份验证服务，如 AJAX 配置文件服务是符合标准的 ASP.NET 配置文件服务，以便包括 AJAX 支持的应不会损坏页当前合并 ASP.NET 配置文件服务的功能。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="1e3d4-125">将 ASP.NET 身份验证和分析服务本身合并到应用程序不在此白皮书的范围。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="1e3d4-126">本主题的详细信息，请参阅 MSDN 库参考文章在使用成员资格管理用户[ https://msdn.microsoft.com/library/tw292whz.aspx ](https://msdn.microsoft.com/library/tw292whz.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="1e3d4-127">ASP.NET 还包括一个实用工具来自动设置使用 SQL Server，这是 ASP.NET 成员资格的默认身份验证服务提供程序的成员身份。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="1e3d4-128">有关详细信息，请参阅文章 ASP.NET SQL Server 注册工具 (Aspnet\_regsql.exe) 处[ https://msdn.microsoft.com/library/ms229862(vs.80).aspx ](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="1e3d4-129">*使用 ASP.NET AJAX 身份验证服务*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="1e3d4-130">必须在 web.config 文件中启用 ASP.NET AJAX 身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="1e3d4-131">身份验证服务需要 ASP.NET 窗体身份验证启用并且 cookie 处于启用状态 （脚本不能启用无 cookie 会话由于无 cookie 会话需要 URL 参数） 的客户端浏览器上。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="1e3d4-132">AJAX 身份验证服务是已启用并配置后，客户端脚本可以立即加以利用 Sys.Services.AuthenticationService 对象。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="1e3d4-133">主要是，客户端脚本将想要充分利用`login`方法和`isLoggedIn`属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="1e3d4-134">若要为登录方法，可以接受大量参数提供默认值不存在多个属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="1e3d4-135">*Sys.Services.AuthenticationService 成员*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="1e3d4-136">*登录方法：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-136">*login method:*</span></span>

<span data-ttu-id="1e3d4-137">Login （） 方法开始的请求进行身份验证用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="1e3d4-138">此方法是异步的不会阻止执行。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="1e3d4-139">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-139">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-140">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-140">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-141">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-142">userName</span><span class="sxs-lookup"><span data-stu-id="1e3d4-142">userName</span></span> | <span data-ttu-id="1e3d4-143">必须的。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-143">Required.</span></span> <span data-ttu-id="1e3d4-144">用于进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-144">The username to authenticate.</span></span> |
| <span data-ttu-id="1e3d4-145">密码</span><span class="sxs-lookup"><span data-stu-id="1e3d4-145">password</span></span> | <span data-ttu-id="1e3d4-146">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-146">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-147">用户的密码。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-147">The user's password.</span></span> |
| <span data-ttu-id="1e3d4-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="1e3d4-148">isPersistent</span></span> | <span data-ttu-id="1e3d4-149">可选 （默认值为 false）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-149">Optional (defaults to false).</span></span> <span data-ttu-id="1e3d4-150">是否用户的身份验证 cookie 应保存各个会话中。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="1e3d4-151">如果为 false，则在浏览器已关闭或会话过期时用户将可以注销。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="1e3d4-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="1e3d4-152">redirectUrl</span></span> | <span data-ttu-id="1e3d4-153">可选 （默认值为 null）。要重定向到身份验证成功后的在浏览器的 URL。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="1e3d4-154">如果此参数为 null 或空字符串，则会不发生任何重定向。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="1e3d4-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="1e3d4-155">customInfo</span></span> | <span data-ttu-id="1e3d4-156">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-156">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-157">此参数是当前未使用，并且是保留供将来使用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="1e3d4-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-158">loginCompletedCallback</span></span> | <span data-ttu-id="1e3d4-159">可选 （默认值为 null）。要成功完成登录后调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="1e3d4-160">如果指定，此参数重写 defaultLoginCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="1e3d4-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-161">failedCallback</span></span> | <span data-ttu-id="1e3d4-162">可选 （默认值为 null）。当登录已经失败时要调用该函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="1e3d4-163">如果指定，此参数重写 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="1e3d4-164">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-164">userContext</span></span> | <span data-ttu-id="1e3d4-165">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-165">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-166">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="1e3d4-167">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-167">*Return Value:*</span></span>

<span data-ttu-id="1e3d4-168">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-168">This function does not include a return value.</span></span> <span data-ttu-id="1e3d4-169">但是，有多种行为都是调用的包含对此函数完成后：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="1e3d4-170">当前页将进行刷新，或者如果更改`redirectUrl`参数是既不为 null，也不是空字符串。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="1e3d4-171">但是，如果参数为 null 或空字符串，则`loginCompletedCallback`参数，或`defaultLoginCompletedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="1e3d4-172">如果对 web 服务的调用失败，`failedCallback`参数的`defaultFailedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="1e3d4-173">*注销方法：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-173">*logout method:*</span></span>

<span data-ttu-id="1e3d4-174">Logout （） 方法将移除凭据 cookie，并从 web 应用程序的当前用户。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="1e3d4-175">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-175">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-176">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-176">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-177">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="1e3d4-178">redirectUrl</span></span> | <span data-ttu-id="1e3d4-179">可选 （默认值为 null）。要重定向到身份验证成功后的在浏览器的 URL。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="1e3d4-180">如果此参数为 null 或空字符串，则会不发生任何重定向。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="1e3d4-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-181">logoutCompletedCallback</span></span> | <span data-ttu-id="1e3d4-182">可选 （默认值为 null）。要注销已成功完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="1e3d4-183">如果指定，此参数重写 defaultLogoutCompleted 属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="1e3d4-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-184">failedCallback</span></span> | <span data-ttu-id="1e3d4-185">可选 （默认值为 null）。当登录已经失败时要调用该函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="1e3d4-186">如果指定，此参数重写 defaultFailedCallback 属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="1e3d4-187">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-187">userContext</span></span> | <span data-ttu-id="1e3d4-188">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-188">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-189">应传递给回调函数的自定义用户上下文数据。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="1e3d4-190">*返回值：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-190">*Return Value:*</span></span>

<span data-ttu-id="1e3d4-191">此函数不包括返回值。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-191">This function does not include a return value.</span></span> <span data-ttu-id="1e3d4-192">但是，有多种行为都是调用的包含对此函数完成后：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="1e3d4-193">当前页将进行刷新，或者如果更改`redirectUrl`参数是既不为 null，也不是空字符串。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="1e3d4-194">但是，如果参数为 null 或空字符串，则`logoutCompletedCallback`参数，或`defaultLogoutCompletedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="1e3d4-195">如果对 web 服务的调用失败，`failedCallback`参数的`defaultFailedCallback`调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="1e3d4-196">*defaultFailedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="1e3d4-197">此属性指定应与 web 服务进行通信在失败时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="1e3d4-198">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-199">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="1e3d4-200">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-200">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-201">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-201">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-202">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-203">错误</span><span class="sxs-lookup"><span data-stu-id="1e3d4-203">error</span></span> | <span data-ttu-id="1e3d4-204">指定的错误信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-204">Specifies the error information.</span></span> |
| <span data-ttu-id="1e3d4-205">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-205">userContext</span></span> | <span data-ttu-id="1e3d4-206">指定登录或注销函数调用时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="1e3d4-207">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-207">methodName</span></span> | <span data-ttu-id="1e3d4-208">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-208">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-209">*defaultLoginCompletedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="1e3d4-210">此属性指定登录名的 web 服务调用完成时，应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="1e3d4-211">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-212">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="1e3d4-213">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-213">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-214">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-214">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-215">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-216">validCredentials</span><span class="sxs-lookup"><span data-stu-id="1e3d4-216">validCredentials</span></span> | <span data-ttu-id="1e3d4-217">指定是否为用户提供有效的凭据。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="1e3d4-218">`true` 如果用户成功登录;否则为`false`。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="1e3d4-219">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-219">userContext</span></span> | <span data-ttu-id="1e3d4-220">指定调用 login 函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="1e3d4-221">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-221">methodName</span></span> | <span data-ttu-id="1e3d4-222">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-222">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-223">*defaultLogoutCompletedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="1e3d4-224">此属性指定注销的 web 服务调用完成时，应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="1e3d4-225">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-226">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="1e3d4-227">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-227">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-228">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-228">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-229">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-230">result</span><span class="sxs-lookup"><span data-stu-id="1e3d4-230">result</span></span> | <span data-ttu-id="1e3d4-231">此参数将始终为`null`; 保留供将来使用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="1e3d4-232">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-232">userContext</span></span> | <span data-ttu-id="1e3d4-233">指定调用 login 函数时提供的用户上下文信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="1e3d4-234">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-234">methodName</span></span> | <span data-ttu-id="1e3d4-235">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-235">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-236">*isLoggedIn 属性 (get):*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="1e3d4-237">此属性获取用户; 的当前身份验证状态它是 ScriptManager 对象在过程中设置的页面请求。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="1e3d4-238">此属性返回`true`如果用户当前登录; 否则为它将返回`false`。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="1e3d4-239">*路径属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-239">*path property (get, set):*</span></span>

<span data-ttu-id="1e3d4-240">此属性以编程方式确定身份验证 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="1e3d4-241">它可用于重写默认身份验证提供程序，以及一个 ScriptManager 控件的 AuthenticationService 子节点的路径属性中以声明方式设置 (有关详细信息，请参阅使用自定义身份验证服务提供程序下面的主题）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="1e3d4-242">请注意，默认身份验证服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="1e3d4-243">但是，ASP.NET AJAX 允许您指定的位置提供了 ASP.NET AJAX 身份验证服务代理相同的类接口的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="1e3d4-244">另请注意，不应此属性设置为一个值，指示从当前站点的脚本请求。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="1e3d4-245">当前应用程序将不会收到身份验证凭据，因为它也将无用;此外，技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全异常。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="1e3d4-246">此属性是`String`对象，它表示身份验证 web 服务的路径。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="1e3d4-247">*timeout 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="1e3d4-248">此属性确定失败的身份验证服务的登录请求前等待的时间长度。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="1e3d4-249">如果在超时到期等待调用完成时，将调用请求失败回调，也将无法完成调用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="1e3d4-250">此属性是`Number`对象，表示要等待从身份验证服务的结果的毫秒数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="1e3d4-251">*登录到身份验证服务的代码示例：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="1e3d4-252">以下标记是通过简单的脚本调用的 AuthenticationService 类的登录和注销方法的示例 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="1e3d4-253">访问的 ASP.NET 分析数据通过 AJAX</span><span class="sxs-lookup"><span data-stu-id="1e3d4-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="1e3d4-254">通过 ASP.NET AJAX Extensions 还公开的 ASP.NET 分析服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="1e3d4-255">由于 ASP.NET 分析服务提供丰富的精细的 API，通过要存储和检索用户数据，这可以是卓越的生产效率工具。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="1e3d4-256">必须在 web.config 中; 启用配置文件服务它不是默认情况下。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="1e3d4-257">若要执行此操作，请确保`profileService`子元素已启用 = true 中指定的 web.config 文件中，并指定哪些属性可读取或写入，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="1e3d4-258">此外必须配置配置文件服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-258">The profile service must also be configured.</span></span> <span data-ttu-id="1e3d4-259">虽然分析服务的配置是本白皮书的范围之外，但值得注意，在配置文件配置设置中定义的组将组名称的子属性的可访问性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="1e3d4-260">例如，使用指定的以下配置文件部分：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="1e3d4-261">客户端脚本可以访问作为 ProfileService 类的属性字段的属性的名称、 Address.Line1、 Address.Line2、 Address.City、 Address.State、 Address.Zip 和 BackgroundColor。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="1e3d4-262">AJAX 分析服务配置后，它将可以立即在页面; 例如：但是，它必须在使用前一次加载。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="1e3d4-263">*Sys.Services.ProfileService 成员*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="1e3d4-264">*属性字段：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-264">*properties field:*</span></span>

<span data-ttu-id="1e3d4-265">属性字段公开为可由圆点运算符名称约定引用的子属性配置的配置文件的所有数据。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="1e3d4-266">属性组的子级的属性称为 GroupName.PropertyName。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="1e3d4-267">在上面介绍的示例配置文件配置中，以获取状态的用户，您可以使用以下标识符：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="1e3d4-268">*load 方法：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-268">*load method:*</span></span>

<span data-ttu-id="1e3d4-269">从服务器加载所选的列表或所有属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="1e3d4-270">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-270">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-271">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-271">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-272">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="1e3d4-273">propertyNames</span></span> | <span data-ttu-id="1e3d4-274">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-274">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-275">要从服务器加载的属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="1e3d4-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-276">loadCompletedCallback</span></span> | <span data-ttu-id="1e3d4-277">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-277">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-278">要在加载时调用的函数已完成。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="1e3d4-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-279">failedCallback</span></span> | <span data-ttu-id="1e3d4-280">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-280">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-281">如果发生错误，请调用函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="1e3d4-282">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-282">userContext</span></span> | <span data-ttu-id="1e3d4-283">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-283">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-284">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="1e3d4-285">加载函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-285">The load function does not have a return value.</span></span> <span data-ttu-id="1e3d4-286">如果已成功完成的调用，它将调用`loadCompletedCallback`参数或`defaultLoadCompletedCallback`属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="1e3d4-287">如果调用失败或超时时间已到，要么`failedCallback`参数或`defaultFailedCallback`将调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="1e3d4-288">如果`propertyNames`未提供参数，从服务器中检索所有读取配置属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="1e3d4-289">*保存方法：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-289">*save method:*</span></span>

<span data-ttu-id="1e3d4-290">Save （） 方法将指定的属性列表 （或所有属性） 保存到用户的 ASP.NET 配置文件。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="1e3d4-291">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-291">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-292">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-292">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-293">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="1e3d4-294">propertyNames</span></span> | <span data-ttu-id="1e3d4-295">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-295">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-296">要保存到服务器的属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="1e3d4-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-297">saveCompletedCallback</span></span> | <span data-ttu-id="1e3d4-298">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-298">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-299">要保存时调用的函数已完成。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="1e3d4-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="1e3d4-300">failedCallback</span></span> | <span data-ttu-id="1e3d4-301">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-301">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-302">如果发生错误，请调用函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="1e3d4-303">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-303">userContext</span></span> | <span data-ttu-id="1e3d4-304">可选 （默认值为 null）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-304">Optional (defaults to null).</span></span> <span data-ttu-id="1e3d4-305">要传递给回调函数的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="1e3d4-306">保存函数没有返回值。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-306">The save function does not have a return value.</span></span> <span data-ttu-id="1e3d4-307">如果调用成功完成，它将调用`saveCompletedCallback`参数或`defaultSaveCompletedCallback`属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="1e3d4-308">如果调用失败或超时时间已到，要么`failedCallback`或`defaultFailedCallback`将调用属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="1e3d4-309">如果`propertyNames`参数为 null，所有配置文件属性将发送到服务器，且服务器将决定可保存哪些属性以及哪些不能。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="1e3d4-310">*defaultFailedCallback 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="1e3d4-311">此属性指定应与 web 服务进行通信在失败时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="1e3d4-312">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-313">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="1e3d4-314">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-314">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-315">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-315">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-316">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-317">Error</span><span class="sxs-lookup"><span data-stu-id="1e3d4-317">Error</span></span> | <span data-ttu-id="1e3d4-318">指定的错误信息。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-318">Specifies the error information.</span></span> |
| <span data-ttu-id="1e3d4-319">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-319">userContext</span></span> | <span data-ttu-id="1e3d4-320">指定当提供的用户上下文信息加载或保存函数调用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="1e3d4-321">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-321">methodName</span></span> | <span data-ttu-id="1e3d4-322">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-322">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-323">*defaultSaveCompleted 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="1e3d4-324">此属性指定应在保存用户的配置文件数据的完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="1e3d4-325">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-326">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="1e3d4-327">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-327">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-328">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-328">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-329">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="1e3d4-330">numPropsSaved</span></span> | <span data-ttu-id="1e3d4-331">指定已保存的属性的数目。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="1e3d4-332">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-332">userContext</span></span> | <span data-ttu-id="1e3d4-333">指定当提供的用户上下文信息加载或保存函数调用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="1e3d4-334">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-334">methodName</span></span> | <span data-ttu-id="1e3d4-335">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-335">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-336">*defaultLoadCompleted 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="1e3d4-337">此属性指定的用户的配置文件数据加载完成后，应调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="1e3d4-338">它应接收的委托 （或函数参考）。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="1e3d4-339">此属性指定的函数引用应具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="1e3d4-340">*参数：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-340">*Parameters:*</span></span>

| <span data-ttu-id="1e3d4-341">**参数名称**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-341">**Parameter Name**</span></span> | <span data-ttu-id="1e3d4-342">**含义**</span><span class="sxs-lookup"><span data-stu-id="1e3d4-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1e3d4-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="1e3d4-343">numPropsLoaded</span></span> | <span data-ttu-id="1e3d4-344">指定加载的属性的数目。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="1e3d4-345">userContext</span><span class="sxs-lookup"><span data-stu-id="1e3d4-345">userContext</span></span> | <span data-ttu-id="1e3d4-346">指定当提供的用户上下文信息加载或保存函数调用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="1e3d4-347">方法名称</span><span class="sxs-lookup"><span data-stu-id="1e3d4-347">methodName</span></span> | <span data-ttu-id="1e3d4-348">调用方法的名称。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-348">The name of the calling method.</span></span> |

<span data-ttu-id="1e3d4-349">*路径属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-349">*path property (get, set):*</span></span>

<span data-ttu-id="1e3d4-350">此属性以编程方式确定配置文件 web 服务的位置。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="1e3d4-351">它可用于重写默认配置文件服务提供程序，以及一个 ScriptManager 控件的 ProfileService 子节点的路径属性中以声明方式设置。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="1e3d4-352">请注意，默认配置文件服务的位置不会更改。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="1e3d4-353">但是，ASP.NET AJAX 允许您指定的位置提供了 ASP.NET AJAX 身份验证服务代理相同的类接口的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="1e3d4-354">另请注意，不应此属性设置为一个值，指示从当前站点的脚本请求。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="1e3d4-355">技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全异常。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="1e3d4-356">此属性是`String`对象，表示配置文件 web 服务的路径。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="1e3d4-357">*timeout 属性 （get、 组）：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="1e3d4-358">此属性确定失败的负载前等待的配置文件服务或保存请求的时间长度。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="1e3d4-359">如果在超时到期等待调用完成时，将调用请求失败回调，也将无法完成调用。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="1e3d4-360">此属性是`Number`对象，表示要等待从配置文件服务的结果的毫秒数。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="1e3d4-361">*代码示例： 加载在页面加载的配置文件数据*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="1e3d4-362">下面的代码将检查是否用户进行身份验证，并且如果是这样，加载速度将用户的首选的背景色作为页面的。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="1e3d4-363">*使用自定义身份验证服务提供程序*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="1e3d4-364">ASP.NET AJAX Extensions，可以创建自定义脚本身份验证服务提供程序公开您通过自定义 web 服务的功能。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="1e3d4-365">若要使用你的 web 服务必须公开两种方法`Login`和`Logout`; 并且必须具有为默认 ASP.NET AJAX 身份验证 web 服务相同的方法签名指定这些方法。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="1e3d4-366">一旦创建自定义 web 服务后，需要指定给它以声明方式在页中，路径，以编程方式在代码中，或通过客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="1e3d4-367">*若要以声明方式设置的路径：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="1e3d4-368">若要以声明方式设置的路径，包括对您的 ASP.NET 页面的 ScriptManager 对象的 AuthenticationService 子级：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="1e3d4-369">*在代码中设置的路径：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-369">*To set the path in code:*</span></span>

<span data-ttu-id="1e3d4-370">若要以编程方式设置路径，请指定通过脚本管理器的实例的路径：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="1e3d4-371">*若要在脚本中设置路径：*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-371">*To set the path in script:*</span></span>

<span data-ttu-id="1e3d4-372">若要在脚本中以编程方式设置路径，请利用`path`AuthenticationService 类的属性：</span><span class="sxs-lookup"><span data-stu-id="1e3d4-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="1e3d4-373">*适用于自定义身份验证的示例 Web 服务*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="1e3d4-374">总结</span><span class="sxs-lookup"><span data-stu-id="1e3d4-374">Summary</span></span>

<span data-ttu-id="1e3d4-375">ASP.NET 服务-特别是分析、 成员资格和身份验证服务-轻松地向 JavaScript 公开客户端浏览器上。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="1e3d4-376">这允许开发人员及其客户端代码使用的身份验证机制无缝集成，而无需依赖等来执行繁重的工作的 Updatepanel 控件上。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="1e3d4-377">可从客户端，通过利用 web 配置设置; 保护配置文件数据不会按默认情况下，提供的任何数据和开发人员必须选择在配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="1e3d4-378">此外，通过使用等效方法签名中创建简化的 web 服务实现，开发人员可以创建自定义脚本的这些内部函数的 ASP.NET 服务的提供程序。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="1e3d4-379">对这些技术的支持简化了开发丰富的客户端应用程序，同时为开发人员提供范围广泛的灵活性来满足特定需求。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="1e3d4-380">*个人简介*</span><span class="sxs-lookup"><span data-stu-id="1e3d4-380">*Bio*</span></span>

<span data-ttu-id="1e3d4-381">Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e3d4-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="1e3d4-382">可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)</span><span class="sxs-lookup"><span data-stu-id="1e3d4-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e3d4-383">[上一页](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一页](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="1e3d4-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
