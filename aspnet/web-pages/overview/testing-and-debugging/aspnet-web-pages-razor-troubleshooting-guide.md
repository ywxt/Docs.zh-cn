---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: "ASP.NET 网页 (Razor) 故障排除指南 |Microsoft 文档"
author: tfitzmac
description: "本文介绍使用 ASP.NET Web 页 (Razor) 和一些推荐的解决方案时可能遇到的问题。 软件版本 ASP.NET Web 页的链接。..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: 72c49ed8b76b5fb5eb15bf01f57980b382607496
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="0592a-104">ASP.NET 网页 (Razor) 故障排除指南</span><span class="sxs-lookup"><span data-stu-id="0592a-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>
====================
<span data-ttu-id="0592a-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0592a-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0592a-106">本文介绍使用 ASP.NET Web 页 (Razor) 和一些推荐的解决方案时可能遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="0592a-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="0592a-107">软件版本</span><span class="sxs-lookup"><span data-stu-id="0592a-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0592a-108">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0592a-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0592a-109">本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。</span><span class="sxs-lookup"><span data-stu-id="0592a-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="0592a-110">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="0592a-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="0592a-111">问题与运行页</span><span class="sxs-lookup"><span data-stu-id="0592a-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="0592a-112">使用 Razor 代码的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="0592a-113">安全和成员身份的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="0592a-114">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="0592a-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="0592a-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="0592a-116">常规问题，请参阅[ASP.NET Web 页 (Razor) 常见问题](https://go.microsoft.com/fwlink/?LinkId=253000)。</span><span class="sxs-lookup"><span data-stu-id="0592a-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="0592a-117">问题与运行页</span><span class="sxs-lookup"><span data-stu-id="0592a-117">Issues with Running Pages</span></span>

<span data-ttu-id="0592a-118">各种问题可能会阻止*.cshtml*和*.vbhtml*页从正常运行。</span><span class="sxs-lookup"><span data-stu-id="0592a-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="0592a-119">本部分列出了常见的错误消息和可能的原因。</span><span class="sxs-lookup"><span data-stu-id="0592a-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="0592a-120">HTTP 错误 403-禁止访问： 访问被拒绝</span><span class="sxs-lookup"><span data-stu-id="0592a-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="0592a-121">*你没有权限以使用你提供的凭据查看此目录或页面。*</span><span class="sxs-lookup"><span data-stu-id="0592a-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="0592a-122">如果服务器未运行的.NET framework 的正确版本，可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="0592a-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0592a-123">请确保正在运行 server （本地或远程） 的计算机具有至少安装.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="0592a-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="0592a-124">此外请确保应用程序本身配置为运行正确版本。</span><span class="sxs-lookup"><span data-stu-id="0592a-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="0592a-125">如果本地在 WebMatrix 中工作时看到此问题，请单击**站点**工作区中，然后在树视图中单击**设置**。</span><span class="sxs-lookup"><span data-stu-id="0592a-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="0592a-126">在**选择.NET Framework 版本**列表中，选择**.NET 4 （集成）**。</span><span class="sxs-lookup"><span data-stu-id="0592a-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="0592a-127">如果已设置此版本，请尝试以管理员身份运行 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="0592a-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="0592a-128">请确保你网站的根目录具有至少一个*.cshtml*在其中的文件。</span><span class="sxs-lookup"><span data-stu-id="0592a-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="0592a-129">如果 web 服务器上的远程服务器时，你会看到此错误，请与服务器管理员联系。</span><span class="sxs-lookup"><span data-stu-id="0592a-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="0592a-130">请确保服务器具有.NET Framework 4 或更高版本安装。</span><span class="sxs-lookup"><span data-stu-id="0592a-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="0592a-131">此外请确保应用程序在配置为使用该版本的.net Framework 的应用程序池中运行。</span><span class="sxs-lookup"><span data-stu-id="0592a-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="0592a-132">如果你有对服务器的控制，请确保它正在运行的.NET framework 的正确版本。</span><span class="sxs-lookup"><span data-stu-id="0592a-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0592a-133">您还可以尝试通过运行修复安装`aspnet_regiis -iru`命令。</span><span class="sxs-lookup"><span data-stu-id="0592a-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="0592a-134">（例如，如果在安装.NET Framework 之后，你安装 IIS，IIS 将不正确配置为运行 ASP.NET 页。）有关详细信息，请参阅[ASP.NET IIS 注册工具 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="0592a-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="0592a-135">HTTP 错误 403.14-禁止访问</span><span class="sxs-lookup"><span data-stu-id="0592a-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="0592a-136">*Web 服务器被配置为不列出此目录的内容。*</span><span class="sxs-lookup"><span data-stu-id="0592a-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="0592a-137">如果请求保护的资源，可能出现此错误 (如*Web.config*文件) 或，位于受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。</span><span class="sxs-lookup"><span data-stu-id="0592a-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="0592a-138">HTTP 错误 404.17-找不到</span><span class="sxs-lookup"><span data-stu-id="0592a-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="0592a-139">*请求的内容似乎是脚本，因而将无法由静态文件处理程序。*</span><span class="sxs-lookup"><span data-stu-id="0592a-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="0592a-140">如果服务器未正确配置为使用.NET Framework 4 或更高版本，因此无法识别中的代码，可能出现此错误`@{ }`块。</span><span class="sxs-lookup"><span data-stu-id="0592a-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="0592a-141">请参阅前面的说明*HTTP 错误 403-禁止访问： 访问被拒绝*。</span><span class="sxs-lookup"><span data-stu-id="0592a-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="0592a-142">HTTP 错误 404.7-找不到</span><span class="sxs-lookup"><span data-stu-id="0592a-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="0592a-143">*请求筛选模块被配置为拒绝文件扩展名*</span><span class="sxs-lookup"><span data-stu-id="0592a-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="0592a-144">如果可能发生此错误*.cshtml*或*.vbhtml*扩展明确阻止在服务器上。</span><span class="sxs-lookup"><span data-stu-id="0592a-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="0592a-145">此问题的症状它们不包括的扩展，但包含的 Url 时该 Url 工作*.cshtml*或*.vbhtml*不起作用。</span><span class="sxs-lookup"><span data-stu-id="0592a-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="0592a-146">可能的解决方案是重新启用的站点中的扩展*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="0592a-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="0592a-147">下面的示例演示如何启用*.cshtml*扩展。</span><span class="sxs-lookup"><span data-stu-id="0592a-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="0592a-148">HTTP 错误 404.8-找不到</span><span class="sxs-lookup"><span data-stu-id="0592a-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="0592a-149">*请求筛选模块被配置为拒绝包含 hiddenSegment 节的 URL 中的路径。*</span><span class="sxs-lookup"><span data-stu-id="0592a-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="0592a-150">如果请求保护的资源，可能出现此错误 (如*Web.config*文件) 或，位于受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。</span><span class="sxs-lookup"><span data-stu-id="0592a-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="0592a-151">此类型的页是未被提供服务 （服务器错误 '/' 应用程序中）</span><span class="sxs-lookup"><span data-stu-id="0592a-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="0592a-152">请参见 HTTP 错误 404.17 前面的说明。</span><span class="sxs-lookup"><span data-stu-id="0592a-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="0592a-153">使用 Razor 代码的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="0592a-154">名称*类*当前上下文中不存在</span><span class="sxs-lookup"><span data-stu-id="0592a-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="0592a-155">通常情况下，请参阅此错误的原因在于`class`帮助器，但帮助程序不安装的引用。</span><span class="sxs-lookup"><span data-stu-id="0592a-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="0592a-156">例如，如果你尝试使用一个帮助程序，但是，如果你尚未从 NuGet 安装包，你将看到此错误。</span><span class="sxs-lookup"><span data-stu-id="0592a-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="0592a-157">在 WebMatrix 中库用于查找和安装的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="0592a-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="0592a-158">如果已安装的帮助程序，但该页仍不能识别它，请尝试添加添加`using`语句的代码。</span><span class="sxs-lookup"><span data-stu-id="0592a-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="0592a-159">在`using`语句，参考包括帮助器的命名空间。</span><span class="sxs-lookup"><span data-stu-id="0592a-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="0592a-160">例如，ASP.NET Web 帮助器包中的基本帮助器处于`System.Web.Helpers`命名空间。</span><span class="sxs-lookup"><span data-stu-id="0592a-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="0592a-161">在你想要使用的帮助器页的顶部，添加下面一行：</span><span class="sxs-lookup"><span data-stu-id="0592a-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="0592a-162">安全和成员身份的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-162">Issues with Security and Membership</span></span>

<span data-ttu-id="0592a-163">如果你使用内置安全 （成员资格） 系统中的 ASP.NET Web Pages (Razor)，你可能会遇到以下问题。</span><span class="sxs-lookup"><span data-stu-id="0592a-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="0592a-164">若要调用此方法，"Membership.Provider"属性必须为"ExtendedMembershipProvider"的实例</span><span class="sxs-lookup"><span data-stu-id="0592a-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="0592a-165">此错误可能指示没有`AspNetSqlMembershipProvider`配置类。</span><span class="sxs-lookup"><span data-stu-id="0592a-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="0592a-166">（一种症状是站点本地工作正常，但是将其发布到宿主提供程序的服务器时，会引发此错误。）此问题的一个解决方法是显式启用简单的成员身份，通过将以下内容添加到站点的*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="0592a-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="0592a-167">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="0592a-167">Issues with Sending Email</span></span>

<span data-ttu-id="0592a-168">发送电子邮件问题可能具有挑战性调试。</span><span class="sxs-lookup"><span data-stu-id="0592a-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="0592a-169">初始问题可以是你无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="0592a-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="0592a-170">如果连接成功，ASP.NET 会将消息传递到 SMTP 服务器中。</span><span class="sxs-lookup"><span data-stu-id="0592a-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="0592a-171">但是，可能会与消息本身，以防止 SMTP 服务器发送的问题。</span><span class="sxs-lookup"><span data-stu-id="0592a-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="0592a-172">如果你的应用程序不会成功发送电子邮件，请尝试以下解决方法：</span><span class="sxs-lookup"><span data-stu-id="0592a-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="0592a-173">SMTP 服务器名称通常是类似`smtp.provider.com`或`smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="0592a-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="0592a-174">但是，如果你将你的站点发布到托管提供商，SMTP 服务器名称在该点可能是`localhost`。</span><span class="sxs-lookup"><span data-stu-id="0592a-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="0592a-175">因为您已发布和提供程序的服务器上运行你的站点后，可能从你的应用程序的角度本地 SMTP 服务器，将出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="0592a-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="0592a-176">这一更改服务器名称可能意味着，你必须更改发布过程的一部分的 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="0592a-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="0592a-177">端口号通常为 25。</span><span class="sxs-lookup"><span data-stu-id="0592a-177">The port number is usually 25.</span></span> <span data-ttu-id="0592a-178">但是，某些访问接口要求你为使用端口 587 或某些其他端口。</span><span class="sxs-lookup"><span data-stu-id="0592a-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="0592a-179">咨询哪个端口号，他们希望你使用的 SMTP 服务器的所有者。</span><span class="sxs-lookup"><span data-stu-id="0592a-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="0592a-180">请确保使用正确的凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="0592a-181">如果你已将站点发布到宿主提供程序，使用提供程序专门指示适用于电子邮件的凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="0592a-182">这些凭据可能不同于用来发布的凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="0592a-183">有时则根本不需要凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="0592a-184">如果您要使用您的个人 ISP 发送电子邮件，你的电子邮件提供商可能已经知道你的凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="0592a-185">在发布后，你可能需要使用比测试本地计算机上的不同凭据。</span><span class="sxs-lookup"><span data-stu-id="0592a-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="0592a-186">如果你的电子邮件提供商使用加密，请设置`WebMail.EnableSsl`到`true`。</span><span class="sxs-lookup"><span data-stu-id="0592a-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="0592a-187">如果没有发送电子邮件时出错，可能会看到类似如下所示的标准 ASP.NET 错误消息：</span><span class="sxs-lookup"><span data-stu-id="0592a-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![ASP.NET 错误消息时使用电子邮件问题](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="0592a-189">你还可以调试通过发送电子邮件问题`try-catch`块，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="0592a-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="0592a-190">当你使用`try-catch`块中，ASP.NET 不会显示其标准错误消息。</span><span class="sxs-lookup"><span data-stu-id="0592a-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="0592a-191">相反，你可以捕获中的错误`catch`的块部分。</span><span class="sxs-lookup"><span data-stu-id="0592a-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="0592a-192">替换为相应的值`your-SMTP-server-name`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="0592a-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="0592a-193">一些你可能会看到这种方式的错误消息如下：</span><span class="sxs-lookup"><span data-stu-id="0592a-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="0592a-194">*无法发送邮件。*</span><span class="sxs-lookup"><span data-stu-id="0592a-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="0592a-195">或</span><span class="sxs-lookup"><span data-stu-id="0592a-195">-or-</span></span>

    <span data-ttu-id="0592a-196">*连接尝试失败，因为连接的方未正确响应后一段时间，或建立的连接失败，因为连接的主机未能响应*</span><span class="sxs-lookup"><span data-stu-id="0592a-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="0592a-197">此错误通常表示应用程序无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="0592a-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="0592a-198">请检查服务器名和端口号。</span><span class="sxs-lookup"><span data-stu-id="0592a-198">Check the server name and port number.</span></span>
- <span data-ttu-id="0592a-199">*邮箱不可用。服务器响应为： 5.1.0 &lt; someuser@invaliddomain &gt;发件人拒绝： 无效的发件人域*</span><span class="sxs-lookup"><span data-stu-id="0592a-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="0592a-200">此消息可以指示`From`地址不正确或缺少。</span><span class="sxs-lookup"><span data-stu-id="0592a-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="0592a-201">*指定的字符串不是所要求的电子邮件地址的形式。*</span><span class="sxs-lookup"><span data-stu-id="0592a-201">*The specified string is not in the form required for an e-mail address.*</span></span>

    <span data-ttu-id="0592a-202">此错误可能指示的值`To`或`From`属性不会识别为电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="0592a-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="0592a-203">(ASP.NET 无法检查电子邮件地址是否有效，只有它的格式正确，如 *name@domain.com* 。)</span><span class="sxs-lookup"><span data-stu-id="0592a-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="0592a-204">删除显示的错误的标记 (`@errorMessage`) 将页面发布到实时站点之前。</span><span class="sxs-lookup"><span data-stu-id="0592a-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="0592a-205">它不是让用户可以查看从服务器获取的错误消息的一个好办法。</span><span class="sxs-lookup"><span data-stu-id="0592a-205">It's not a good idea to let users see error messages that you get from a server.</span></span>


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="0592a-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="0592a-206">Additional Resources</span></span>

[<span data-ttu-id="0592a-207">ASP.NET 网页 (Razor) 常见问题解答</span><span class="sxs-lookup"><span data-stu-id="0592a-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="0592a-208">[WebMatrix 和 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 网站上的论坛</span><span class="sxs-lookup"><span data-stu-id="0592a-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
