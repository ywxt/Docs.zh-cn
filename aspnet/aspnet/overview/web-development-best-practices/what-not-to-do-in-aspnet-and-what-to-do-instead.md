---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: 不需要在 ASP.NET 中，做什么和要改为执行的操作 |Microsoft 文档
author: tfitzmac
description: 本主题介绍在 ASP.NET web 项目中的人员进行的几个常见错误。 它提供有关你应执行哪些操作来避免这些 commo 建议...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/08/2014
ms.topic: article
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 829f3a024bc15bec8b60b91193ba9bca37b78009
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28034915"
---
<a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="e7d63-104">不需要在 ASP.NET 中，做什么和要改为执行的操作</span><span class="sxs-lookup"><span data-stu-id="e7d63-104">What not to do in ASP.NET, and what to do instead</span></span>
====================
<span data-ttu-id="e7d63-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e7d63-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e7d63-106">本主题介绍在 ASP.NET web 项目中的人员进行的几个常见错误。</span><span class="sxs-lookup"><span data-stu-id="e7d63-106">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="e7d63-107">它提供了你应执行哪些操作来避免这些常见的错误的建议。</span><span class="sxs-lookup"><span data-stu-id="e7d63-107">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="e7d63-108">它基于[演示文稿](http://vimeo.com/68390507)通过**Damian Edwards**挪威语开发人员大会。</span><span class="sxs-lookup"><span data-stu-id="e7d63-108">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>


## <a name="disclaimer"></a><span data-ttu-id="e7d63-109">免责声明</span><span class="sxs-lookup"><span data-stu-id="e7d63-109">Disclaimer</span></span>

<span data-ttu-id="e7d63-110">本主题不用作完整指南，以确保你的应用程序安全且高效。</span><span class="sxs-lookup"><span data-stu-id="e7d63-110">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="e7d63-111">你仍需要遵循的安全性和性能不本主题中概述的最佳实践。</span><span class="sxs-lookup"><span data-stu-id="e7d63-111">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="e7d63-112">仅建议如何避免与.NET 类和进程相关的常见错误。</span><span class="sxs-lookup"><span data-stu-id="e7d63-112">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="e7d63-113">概述</span><span class="sxs-lookup"><span data-stu-id="e7d63-113">Overview</span></span>

<span data-ttu-id="e7d63-114">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="e7d63-114">This topic contains the following sections:</span></span>

- [<span data-ttu-id="e7d63-115">标准符合性</span><span class="sxs-lookup"><span data-stu-id="e7d63-115">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="e7d63-116">控件适配器</span><span class="sxs-lookup"><span data-stu-id="e7d63-116">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="e7d63-117">在控件上的样式属性</span><span class="sxs-lookup"><span data-stu-id="e7d63-117">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="e7d63-118">页面和控件回调</span><span class="sxs-lookup"><span data-stu-id="e7d63-118">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="e7d63-119">浏览器功能检测</span><span class="sxs-lookup"><span data-stu-id="e7d63-119">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="e7d63-120">安全性</span><span class="sxs-lookup"><span data-stu-id="e7d63-120">Security</span></span>](#security)

    - [<span data-ttu-id="e7d63-121">请求验证</span><span class="sxs-lookup"><span data-stu-id="e7d63-121">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="e7d63-122">无 cookie 窗体身份验证和会话</span><span class="sxs-lookup"><span data-stu-id="e7d63-122">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="e7d63-123">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="e7d63-123">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="e7d63-124">中等信任</span><span class="sxs-lookup"><span data-stu-id="e7d63-124">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="e7d63-125">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="e7d63-125">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="e7d63-126">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="e7d63-126">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="e7d63-127">可靠性和性能</span><span class="sxs-lookup"><span data-stu-id="e7d63-127">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="e7d63-128">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="e7d63-128">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="e7d63-129">异步页事件的 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="e7d63-129">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="e7d63-130">Fire-and-Forget Work</span><span class="sxs-lookup"><span data-stu-id="e7d63-130">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="e7d63-131">请求实体正文</span><span class="sxs-lookup"><span data-stu-id="e7d63-131">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="e7d63-132">Response.Redirect 和 Response.End</span><span class="sxs-lookup"><span data-stu-id="e7d63-132">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="e7d63-133">应和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="e7d63-133">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="e7d63-134">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="e7d63-134">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="e7d63-135">长时间运行的请求 (> 110 秒)</span><span class="sxs-lookup"><span data-stu-id="e7d63-135">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="e7d63-136">标准符合性</span><span class="sxs-lookup"><span data-stu-id="e7d63-136">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="e7d63-137">控件适配器</span><span class="sxs-lookup"><span data-stu-id="e7d63-137">Control Adapters</span></span>

<span data-ttu-id="e7d63-138">建议： 停止使用控件适配器的自适应呈现，并改为使用 CSS 媒体查询和符合标准的 HTML。</span><span class="sxs-lookup"><span data-stu-id="e7d63-138">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="e7d63-139">呈现为不同的设备和环境自定义的表示代码的.NET 2.0 中引入了控件适配器。</span><span class="sxs-lookup"><span data-stu-id="e7d63-139">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="e7d63-140">现在，此自适应呈现可以实现与 CSS 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="e7d63-140">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="e7d63-141">你应停止使用控件适配器，并转换为 CSS 和 HTML 的任何现有的适配器。</span><span class="sxs-lookup"><span data-stu-id="e7d63-141">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="e7d63-142">有关详细信息，请参阅[媒体查询](http://www.w3.org/TR/css3-mediaqueries/)和[How To： 添加移动页添加到你的 ASP.NET Web 窗体 / MVC 应用程序](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-142">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="e7d63-143">在控件上的样式属性</span><span class="sxs-lookup"><span data-stu-id="e7d63-143">Style Properties on Controls</span></span>

<span data-ttu-id="e7d63-144">建议： 停止在控件标记中，设置样式值并改为在 CSS 样式表中设置格式设置的值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-144">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="e7d63-145">Web 服务器控件包含数十个属性用于设置在行样式属性。</span><span class="sxs-lookup"><span data-stu-id="e7d63-145">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="e7d63-146">例如前, 景色属性设置为控件文本的颜色。</span><span class="sxs-lookup"><span data-stu-id="e7d63-146">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="e7d63-147">你可以实现此相同的效果更有效地通过 CSS 样式表。</span><span class="sxs-lookup"><span data-stu-id="e7d63-147">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="e7d63-148">样式表，可以集中样式值并避免设置这些值在整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="e7d63-148">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="e7d63-149">下面的示例演示 CSS 类集文本为红色。</span><span class="sxs-lookup"><span data-stu-id="e7d63-149">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="e7d63-150">下一个示例演示如何动态应用 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="e7d63-150">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="e7d63-151">页面和控件回调</span><span class="sxs-lookup"><span data-stu-id="e7d63-151">Page and Control Callbacks</span></span>

<span data-ttu-id="e7d63-152">建议： 停止使用页和控件的回调，并改为使用以下任一： AJAX、 UpdatePanel、 MVC 操作方法，Web API 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="e7d63-152">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="e7d63-153">在早期版本的 ASP.NET，页和控件的回叫方法允许你更新 web 页面上的部分，而不刷新整个页面。</span><span class="sxs-lookup"><span data-stu-id="e7d63-153">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="e7d63-154">你现在可以完成通过的部分页面更新[AJAX](../../../ajax/index.md)， [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)， [MVC](../../../mvc/index.md)， [Web API](../../../web-api/index.md)或[SignalR](../../../signalr/index.md).</span><span class="sxs-lookup"><span data-stu-id="e7d63-154">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="e7d63-155">你应该停止使用回调方法，因为它们可能会问题导致使用友好的 Url 和路由。</span><span class="sxs-lookup"><span data-stu-id="e7d63-155">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="e7d63-156">默认情况下，控件不能将回叫方法，但如果启用此功能在控件中的，应将其禁用。</span><span class="sxs-lookup"><span data-stu-id="e7d63-156">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="e7d63-157">浏览器功能检测</span><span class="sxs-lookup"><span data-stu-id="e7d63-157">Browser Capability Detection</span></span>

<span data-ttu-id="e7d63-158">建议： 停止使用静态的浏览器功能检测，并改为使用动态功能检测。</span><span class="sxs-lookup"><span data-stu-id="e7d63-158">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="e7d63-159">在早期版本的 ASP.NET，在 XML 文件存储的每个浏览器支持的功能。</span><span class="sxs-lookup"><span data-stu-id="e7d63-159">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="e7d63-160">通过静态查找的检测功能支持不是最好的方法。</span><span class="sxs-lookup"><span data-stu-id="e7d63-160">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="e7d63-161">现在，可以动态检测浏览器的支持功能，如使用功能检测框架， [Modernizr](http://modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-161">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="e7d63-162">功能检测确定通过尝试要使用的方法或属性，然后检查以查看是否浏览器生成所需的结果的支持。</span><span class="sxs-lookup"><span data-stu-id="e7d63-162">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="e7d63-163">默认情况下，Modernizr 包括在 Web 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="e7d63-163">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="e7d63-164">安全性</span><span class="sxs-lookup"><span data-stu-id="e7d63-164">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="e7d63-165">请求验证</span><span class="sxs-lookup"><span data-stu-id="e7d63-165">Request Validation</span></span>

<span data-ttu-id="e7d63-166">建议： 验证用户输入和编码的用户的输出。</span><span class="sxs-lookup"><span data-stu-id="e7d63-166">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="e7d63-167">请求验证是一项功能的 ASP.NET，检查每个请求并停止请求，如果找到一个察觉到的威胁。</span><span class="sxs-lookup"><span data-stu-id="e7d63-167">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="e7d63-168">不依赖于保护你的应用程序针对跨站点脚本攻击的请求验证。</span><span class="sxs-lookup"><span data-stu-id="e7d63-168">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="e7d63-169">相反，验证来自用户的所有输入，对输出进行编码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-169">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="e7d63-170">在某些有限的情况下，你可以使用正则表达式来验证输入，但在更复杂的情况下应验证通过使用.NET 类，以确定如果值与匹配的用户输入允许的值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-170">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="e7d63-171">下面的示例演示如何在 Uri 类使用静态方法以确定是否由用户提供的 Uri 无效。</span><span class="sxs-lookup"><span data-stu-id="e7d63-171">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="e7d63-172">但是，若要充分验证 Uri，你还应检查以确保它指定`http`或`https`。</span><span class="sxs-lookup"><span data-stu-id="e7d63-172">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="e7d63-173">下面的示例使用实例方法来验证 Uri 有效。</span><span class="sxs-lookup"><span data-stu-id="e7d63-173">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="e7d63-174">在呈现为 HTML 的用户输入或 SQL 查询中包括用户输入之前, 的值进行编码以确保恶意代码不包括。</span><span class="sxs-lookup"><span data-stu-id="e7d63-174">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="e7d63-175">你可以 HTML 编码中使用的标记值&lt;%: %&gt;语法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e7d63-175">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="e7d63-176">或者，可以在 Razor 语法中，HTML 编码与 @，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e7d63-176">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="e7d63-177">下面的示例说明如何为 HTML 编码代码隐藏文件中的值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-177">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="e7d63-178">若要安全地进行编码的 SQL 命令的值，请使用命令参数如[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-178">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="e7d63-179">无 cookie 窗体身份验证和会话</span><span class="sxs-lookup"><span data-stu-id="e7d63-179">Cookieless Forms Authentication and Session</span></span>

<span data-ttu-id="e7d63-180">建议： 需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="e7d63-180">Recommendation: Require cookies.</span></span>

<span data-ttu-id="e7d63-181">在查询字符串中传递身份验证信息并不安全。</span><span class="sxs-lookup"><span data-stu-id="e7d63-181">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="e7d63-182">如果你的应用程序包括身份验证，因此，需要 cookie。</span><span class="sxs-lookup"><span data-stu-id="e7d63-182">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="e7d63-183">如果你 cookie 存储敏感信息，请考虑要求使用 SSL 的 cookie。</span><span class="sxs-lookup"><span data-stu-id="e7d63-183">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="e7d63-184">下面的示例演示如何在 Web.config 文件中指定窗体身份验证需要通过 SSL 传输的 cookie。</span><span class="sxs-lookup"><span data-stu-id="e7d63-184">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="e7d63-185">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="e7d63-185">EnableViewStateMac</span></span>

<span data-ttu-id="e7d63-186">建议： 永远不会设置为 false。</span><span class="sxs-lookup"><span data-stu-id="e7d63-186">Recommendation: Never set to false.</span></span>

<span data-ttu-id="e7d63-187">默认情况下，设置 EnbableViewStateMac 为 true。</span><span class="sxs-lookup"><span data-stu-id="e7d63-187">By default, EnbableViewStateMac is set to true.</span></span> <span data-ttu-id="e7d63-188">即使你的应用程序未使用视图状态，请不设置 EnableViewStateMac 为 false。</span><span class="sxs-lookup"><span data-stu-id="e7d63-188">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="e7d63-189">将此值设置为 false 将使你的应用程序容易受到跨站点脚本。</span><span class="sxs-lookup"><span data-stu-id="e7d63-189">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="e7d63-190">从 ASP.NET 4.5.2 开始，运行时强制执行**EnableViewStateMac = true**。</span><span class="sxs-lookup"><span data-stu-id="e7d63-190">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="e7d63-191">即使将其设置为 false 时，运行时将忽略此值，并继续为 true 的设置的值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-191">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="e7d63-192">有关详细信息，请参阅[ASP.NET 4.5.2 和 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-192">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="e7d63-193">下面的示例演示如何将 EnableViewStateMac 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="e7d63-193">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="e7d63-194">不需要实际设置此值为 true，因为它是默认情况下则返回 true。</span><span class="sxs-lookup"><span data-stu-id="e7d63-194">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="e7d63-195">但是，如果你已将其设置为 false 在任何页上应用程序中，则必须立即更正此值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-195">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="e7d63-196">中等信任</span><span class="sxs-lookup"><span data-stu-id="e7d63-196">Medium Trust</span></span>

<span data-ttu-id="e7d63-197">建议： 不依赖于中等信任 （或任何其他信任级别） 作为安全边界。</span><span class="sxs-lookup"><span data-stu-id="e7d63-197">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="e7d63-198">部分信任不能充分保护你的应用程序和不应使用。</span><span class="sxs-lookup"><span data-stu-id="e7d63-198">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="e7d63-199">相反，使用完全信任，并将在单独的应用程序池不受信任的应用程序隔离。</span><span class="sxs-lookup"><span data-stu-id="e7d63-199">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="e7d63-200">此外，运行下一个唯一标识每个应用程序池。</span><span class="sxs-lookup"><span data-stu-id="e7d63-200">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="e7d63-201">有关详细信息，请参阅[ASP.NET 部分信任不保证应用程序隔离](https://support.microsoft.com/kb/2698981)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-201">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="e7d63-202">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="e7d63-202">&lt;appSettings&gt;</span></span>

<span data-ttu-id="e7d63-203">建议： 请不要禁用中的安全设置&lt;appSettings&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="e7d63-203">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="e7d63-204">AppSettings 元素还包含许多值所必需的安全更新。</span><span class="sxs-lookup"><span data-stu-id="e7d63-204">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="e7d63-205">你不应更改或禁用这些值。</span><span class="sxs-lookup"><span data-stu-id="e7d63-205">You should not change or disable these values.</span></span> <span data-ttu-id="e7d63-206">如果部署更新时，必须禁用这些值，请立即重新启用完成部署后。</span><span class="sxs-lookup"><span data-stu-id="e7d63-206">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="e7d63-207">有关详细信息，请参阅[ASP.NET appSettings 元素](https://msdn.microsoft.com/library/hh975440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-207">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="e7d63-208">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="e7d63-208">UrlPathEncode</span></span>

<span data-ttu-id="e7d63-209">建议： 使用[执行 UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)相反。</span><span class="sxs-lookup"><span data-stu-id="e7d63-209">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="e7d63-210">UrlPathEncode 方法已添加到.NET Framework 解决了非常具体的浏览器兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="e7d63-210">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="e7d63-211">它不会充分编码 URL，并不能防止你的应用程序跨站点脚本。</span><span class="sxs-lookup"><span data-stu-id="e7d63-211">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="e7d63-212">你决不应在你的应用程序中使用它。</span><span class="sxs-lookup"><span data-stu-id="e7d63-212">You should never use it in your application.</span></span> <span data-ttu-id="e7d63-213">请改用[执行 UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-213">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="e7d63-214">下面的示例演示如何将一个编码的 URL 作为超链接控件的查询字符串参数传递。</span><span class="sxs-lookup"><span data-stu-id="e7d63-214">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="e7d63-215">可靠性和性能</span><span class="sxs-lookup"><span data-stu-id="e7d63-215">Reliability and Performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="e7d63-216">PreSendRequestHeaders 和 PreSendRequestContent</span><span class="sxs-lookup"><span data-stu-id="e7d63-216">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="e7d63-217">建议： 不要使用托管的模块中使用这些事件。</span><span class="sxs-lookup"><span data-stu-id="e7d63-217">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="e7d63-218">相反，编写本机 IIS 模块来执行所需的任务。</span><span class="sxs-lookup"><span data-stu-id="e7d63-218">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="e7d63-219">请参阅[创建本机代码 HTTP 模块](https://msdn.microsoft.com/library/ms693629.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-219">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="e7d63-220">你可以使用[PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx)和[PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx)事件的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="e7d63-220">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="e7d63-221">不要使用`PreSendRequestHeaders`和`PreSendRequestContent`与实现的托管模块`IHttpModule`。</span><span class="sxs-lookup"><span data-stu-id="e7d63-221">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="e7d63-222">设置这些属性可能会导致具有异步请求的问题。</span><span class="sxs-lookup"><span data-stu-id="e7d63-222">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="e7d63-223">应用程序请求路由 (ARR) 和 websocket 的组合可能会导致访问冲突异常可能会导致崩溃 w3wp。</span><span class="sxs-lookup"><span data-stu-id="e7d63-223">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="e7d63-224">例如，iiscore ！W3_CONTEXT_BASE::GetIsLastNotification + 68 iiscore.dll 中的已导致访问冲突的异常 (0xC0000005)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-224">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="e7d63-225">异步页事件的 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="e7d63-225">Asynchronous Page Events with Web Forms</span></span>

<span data-ttu-id="e7d63-226">建议： 在 Web 窗体，应避免编写异步 void 方法页面生命周期事件，并改为使用[Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx)异步代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-226">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="e7d63-227">当你将标记具有的页事件**异步**和**void**，无法确定当已完成的异步代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-227">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="e7d63-228">请改用 Page.RegisterAsyncTask 使您能够跟踪其完成的方式运行的异步代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-228">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="e7d63-229">下面的示例演示一个按钮的单击处理程序，它包含异步代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-229">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="e7d63-230">此示例中包含异步，读取一个字符串值提供仅为一个异步任务的简化示例而不是建议的做法。</span><span class="sxs-lookup"><span data-stu-id="e7d63-230">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="e7d63-231">如果要使用异步任务，在 Web.config 文件中将 Http 运行时目标框架设置为 4.5。</span><span class="sxs-lookup"><span data-stu-id="e7d63-231">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 in the Web.config file.</span></span> <span data-ttu-id="e7d63-232">将设置目标框架为 4.5 将在新的同步上下文上的.NET 4.5 中添加。</span><span class="sxs-lookup"><span data-stu-id="e7d63-232">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="e7d63-233">此值在 Visual Studio 2012 中的新项目中的默认设置，但不是能设置，如果你正在使用的现有项目。</span><span class="sxs-lookup"><span data-stu-id="e7d63-233">This value is set by default in new projects in Visual Studio 2012, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="e7d63-234">Fire-and-Forget Work</span><span class="sxs-lookup"><span data-stu-id="e7d63-234">Fire-and-Forget Work</span></span>

<span data-ttu-id="e7d63-235">建议： 在处理 asp.net 请求，避免启动即发即弃工作 （此类调用 ThreadPool.QueueUserWorkItem 方法或创建重复调用委托的计时器）。</span><span class="sxs-lookup"><span data-stu-id="e7d63-235">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="e7d63-236">如果你的应用程序具有在 ASP.NET 内运行的即发即弃工作，你的应用程序可以获取同步。在任何时候，应用程序域可以销毁这意味着你正在进行的进程可能不再匹配应用程序的当前状态。</span><span class="sxs-lookup"><span data-stu-id="e7d63-236">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="e7d63-237">你应移动此类型的外部 ASP.NET 的工作。</span><span class="sxs-lookup"><span data-stu-id="e7d63-237">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="e7d63-238">可以使用在 Azure Web 作业、 Windows 服务或辅助角色，以执行正在进行的工作，并从另一个进程中运行该代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-238">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="e7d63-239">如果必须执行在 ASP.NET 中的此工作，你可以添加 Nuget 包调用[WebBackgrounder](http://www.nuget.org/packages/webbackgrounder)运行的代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-239">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="e7d63-240">请求实体正文</span><span class="sxs-lookup"><span data-stu-id="e7d63-240">Request Entity Body</span></span>

<span data-ttu-id="e7d63-241">建议： 避免读取 Request.Form 或 Request.InputStream 之前处理程序的执行事件。</span><span class="sxs-lookup"><span data-stu-id="e7d63-241">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="e7d63-242">应从 Request.Form 或 Request.InputStream 读取的最早是在处理程序的过程执行事件。</span><span class="sxs-lookup"><span data-stu-id="e7d63-242">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="e7d63-243">在 MVC 中，控制器是处理程序，从而执行事件的操作方法运行时。</span><span class="sxs-lookup"><span data-stu-id="e7d63-243">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="e7d63-244">在 Web 窗体，该页是处理程序，并且 Page.Init 事件激发时执行事件。</span><span class="sxs-lookup"><span data-stu-id="e7d63-244">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="e7d63-245">如果早于执行事件读取请求实体主体，你会妨碍对请求的处理。</span><span class="sxs-lookup"><span data-stu-id="e7d63-245">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="e7d63-246">如果你需要读取请求实体主体执行事件之前，可以使用两种[Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx)或[Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-246">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="e7d63-247">当你使用 GetBufferlessInputStream 时，您从请求时，获取原始流，并且假定负责处理整个请求。</span><span class="sxs-lookup"><span data-stu-id="e7d63-247">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="e7d63-248">后因为它们不填充 asp.net，调用 GetBufferlessInputStream、 Request.Form 和 Request.InputStream 不可用。</span><span class="sxs-lookup"><span data-stu-id="e7d63-248">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="e7d63-249">当使用 GetBufferedInputStream 时，将从请求中获取流的副本。</span><span class="sxs-lookup"><span data-stu-id="e7d63-249">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="e7d63-250">Request.Form 和 Request.InputStream 是请求更高版本中仍然可用，因为 ASP.NET 填充另一副本。</span><span class="sxs-lookup"><span data-stu-id="e7d63-250">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="e7d63-251">Response.Redirect 和 Response.End</span><span class="sxs-lookup"><span data-stu-id="e7d63-251">Response.Redirect and Response.End</span></span>

<span data-ttu-id="e7d63-252">建议： 请注意的线程之后调用的处理方式的差异[Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-252">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="e7d63-253">[Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)方法调用 Response.End 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d63-253">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="e7d63-254">在同步过程中，调用 Request.Redirect 会导致当前线程立即中止。</span><span class="sxs-lookup"><span data-stu-id="e7d63-254">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="e7d63-255">但是，在异步过程中，调用 Response.Redirect 不会中止当前线程，因此请求将继续执行代码。</span><span class="sxs-lookup"><span data-stu-id="e7d63-255">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="e7d63-256">在异步过程中，必须从要停止执行代码的方法来返回该任务。</span><span class="sxs-lookup"><span data-stu-id="e7d63-256">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="e7d63-257">在 MVC 项目中，不应调用 Response.Redirect。</span><span class="sxs-lookup"><span data-stu-id="e7d63-257">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="e7d63-258">相反，返回 RedirectResult。</span><span class="sxs-lookup"><span data-stu-id="e7d63-258">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="e7d63-259">应和 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="e7d63-259">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="e7d63-260">建议： 使用 ViewStateMode，而不是应以提供对其控件使用视图状态的精细控制。</span><span class="sxs-lookup"><span data-stu-id="e7d63-260">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="e7d63-261">当应设置为 false 在页面指令中时，视图状态禁用的页内的所有控件，并且无法启用。</span><span class="sxs-lookup"><span data-stu-id="e7d63-261">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="e7d63-262">如果你想要启用你页中的某些控件的视图状态，设置 ViewStateMode 为已禁用页。</span><span class="sxs-lookup"><span data-stu-id="e7d63-262">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="e7d63-263">然后，在实际需要的视图状态的控件上设置为已启用的 ViewStateMode。</span><span class="sxs-lookup"><span data-stu-id="e7d63-263">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="e7d63-264">通过启用仅需要它的控件的视图状态，你可以对 web 页压缩的视图状态的大小。</span><span class="sxs-lookup"><span data-stu-id="e7d63-264">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="e7d63-265">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="e7d63-265">SqlMembershipProvider</span></span>

<span data-ttu-id="e7d63-266">建议： 使用通用提供程序。</span><span class="sxs-lookup"><span data-stu-id="e7d63-266">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="e7d63-267">在当前的项目模板中，SqlMembershipProvider 已被取代[ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)，这是作为 NuGet 程序包提供。</span><span class="sxs-lookup"><span data-stu-id="e7d63-267">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="e7d63-268">如果你使用模板的较早版本生成的项目中使用 SqlMembershipProvider，您应切换到 Universal Providers。</span><span class="sxs-lookup"><span data-stu-id="e7d63-268">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="e7d63-269">通用提供程序使用实体框架支持的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="e7d63-269">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="e7d63-270">有关详细信息，请参阅[简介 ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e7d63-270">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="e7d63-271">长时间运行请求 (> 110 秒)</span><span class="sxs-lookup"><span data-stu-id="e7d63-271">Long-running Requests (>110 seconds)</span></span>

<span data-ttu-id="e7d63-272">建议： 使用[Websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx)或[SignalR](../../../signalr/index.md)连接的客户端，以及使用异步 I/O 操作。</span><span class="sxs-lookup"><span data-stu-id="e7d63-272">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="e7d63-273">长时间运行的请求可能导致不可预知的结果和性能不佳，web 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="e7d63-273">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="e7d63-274">请求的默认超时设置为 110 秒。</span><span class="sxs-lookup"><span data-stu-id="e7d63-274">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="e7d63-275">如果你将会话状态用于长时间运行请求，ASP.NET 将 110 秒后释放会话对象上的锁。</span><span class="sxs-lookup"><span data-stu-id="e7d63-275">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="e7d63-276">但是，你的应用程序可能正处于会话对象上的操作阶段中，当该锁被释放，并且可能未成功完成该操作。</span><span class="sxs-lookup"><span data-stu-id="e7d63-276">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="e7d63-277">如果运行的第一个请求时，被阻止来自用户的第二个请求，第二个请求可能访问处于不一致状态的会话对象。</span><span class="sxs-lookup"><span data-stu-id="e7d63-277">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="e7d63-278">如果你的应用程序包括锁定 （或同步） I/O 操作，该应用程序将无响应。</span><span class="sxs-lookup"><span data-stu-id="e7d63-278">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="e7d63-279">若要提高性能，请在.NET Framework 中使用异步 I/O 操作。</span><span class="sxs-lookup"><span data-stu-id="e7d63-279">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="e7d63-280">此外，用于连接到服务器的客户端使用 WebSockets 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="e7d63-280">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="e7d63-281">这些功能设计来有效地处理长时间运行的请求。</span><span class="sxs-lookup"><span data-stu-id="e7d63-281">These features are designed to efficiently handle long-running requests.</span></span>
