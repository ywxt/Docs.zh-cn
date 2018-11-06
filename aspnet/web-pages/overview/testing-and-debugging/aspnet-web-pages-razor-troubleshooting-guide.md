---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 网页 (Razor) 故障排除指南 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍使用 ASP.NET Web Pages (Razor) 和一些建议的解决方案时可能遇到的问题。 软件版本 ASP.NET Web 页的链接...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: ec8cdda5c5b298736a650f82cd6b52d73b6dfe3d
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021191"
---
<a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="855e2-104">ASP.NET 网页 (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="855e2-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>
====================
<span data-ttu-id="855e2-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="855e2-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="855e2-106">本文介绍使用 ASP.NET Web Pages (Razor) 和一些建议的解决方案时可能遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="855e2-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="855e2-107">软件版本</span><span class="sxs-lookup"><span data-stu-id="855e2-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="855e2-108">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="855e2-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="855e2-109">本教程还适用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0。</span><span class="sxs-lookup"><span data-stu-id="855e2-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="855e2-110">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="855e2-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="855e2-111">与正在运行的页面的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="855e2-112">Razor 代码的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="855e2-113">安全和成员身份的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="855e2-114">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="855e2-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="855e2-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="855e2-116">常规问题，请参阅[ASP.NET Web Pages (Razor) 常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)。</span><span class="sxs-lookup"><span data-stu-id="855e2-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="855e2-117">与正在运行的页面的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-117">Issues with Running Pages</span></span>

<span data-ttu-id="855e2-118">各种问题可能会阻止 *.cshtml*并 *.vbhtml*中正常运行的页面。</span><span class="sxs-lookup"><span data-stu-id="855e2-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="855e2-119">本部分列出了常见的错误消息和可能的原因。</span><span class="sxs-lookup"><span data-stu-id="855e2-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="855e2-120">HTTP 错误 403-禁止访问： 访问被拒绝</span><span class="sxs-lookup"><span data-stu-id="855e2-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="855e2-121">*你没有权限查看此目录或页面使用所提供的凭据。*</span><span class="sxs-lookup"><span data-stu-id="855e2-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="855e2-122">如果服务器未运行.NET Framework 的正确版本，可以发生此错误。</span><span class="sxs-lookup"><span data-stu-id="855e2-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="855e2-123">请确保运行服务器 （本地或远程） 计算机至少具有安装.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="855e2-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="855e2-124">此外请确保应用程序本身配置为运行正确版本。</span><span class="sxs-lookup"><span data-stu-id="855e2-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="855e2-125">如果本地在 WebMatrix 中工作时看到此问题，请单击**站点**工作区中，然后在树视图中单击**设置**。</span><span class="sxs-lookup"><span data-stu-id="855e2-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="855e2-126">在中**选择.NET Framework 版本**列表中，选择 **.NET 4 （集成）**。</span><span class="sxs-lookup"><span data-stu-id="855e2-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="855e2-127">如果已设置此版本，请尝试以管理员身份运行 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="855e2-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="855e2-128">请确保你的网站的根目录具有至少一个 *.cshtml*中该文件。</span><span class="sxs-lookup"><span data-stu-id="855e2-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="855e2-129">如果远程服务器上的 web 服务器时看到此错误，请与服务器管理员联系。</span><span class="sxs-lookup"><span data-stu-id="855e2-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="855e2-130">请确保服务器具有.NET Framework 4 或更高版本安装。</span><span class="sxs-lookup"><span data-stu-id="855e2-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="855e2-131">此外请确保在配置为使用该版本的.net Framework 的应用程序池中运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="855e2-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="855e2-132">如果必须对服务器的控制，请确保它正在运行的.NET framework 的正确版本。</span><span class="sxs-lookup"><span data-stu-id="855e2-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="855e2-133">您还可以尝试通过运行修复安装`aspnet_regiis -iru`命令。</span><span class="sxs-lookup"><span data-stu-id="855e2-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="855e2-134">（例如，如果在安装.NET Framework 之后安装 IIS，IIS 将不正确配置为运行 ASP.NET 页。）有关详细信息，请参阅[ASP.NET IIS 注册工具 (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="855e2-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="855e2-135">HTTP 错误 403.14-禁止访问</span><span class="sxs-lookup"><span data-stu-id="855e2-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="855e2-136">*Web 服务器配置为不列出此目录的内容。*</span><span class="sxs-lookup"><span data-stu-id="855e2-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="855e2-137">如果请求受保护的资源，则可能出现此错误 (如*Web.config*文件) 或受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。</span><span class="sxs-lookup"><span data-stu-id="855e2-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="855e2-138">HTTP 错误 404.17-找不到</span><span class="sxs-lookup"><span data-stu-id="855e2-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="855e2-139">*请求的内容显示为脚本，并且不会提供静态文件处理程序。*</span><span class="sxs-lookup"><span data-stu-id="855e2-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="855e2-140">如果服务器未正确配置为使用.NET Framework 4 或更高版本，因此无法识别中的代码，可能出现此错误`@{ }`块。</span><span class="sxs-lookup"><span data-stu-id="855e2-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="855e2-141">请参阅前面的说明*HTTP 错误 403-禁止访问： 访问被拒绝*。</span><span class="sxs-lookup"><span data-stu-id="855e2-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="855e2-142">HTTP 错误 404.7-找不到</span><span class="sxs-lookup"><span data-stu-id="855e2-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="855e2-143">*请求筛选模块配置为拒绝文件扩展名*</span><span class="sxs-lookup"><span data-stu-id="855e2-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="855e2-144">如果发生此错误，可以 *.cshtml*或 *.vbhtml*扩展已显式阻止在服务器上。</span><span class="sxs-lookup"><span data-stu-id="855e2-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="855e2-145">此问题的症状是该 Url 工作时不包括的扩展，但包含的 Url *.cshtml*或 *.vbhtml*不起作用。</span><span class="sxs-lookup"><span data-stu-id="855e2-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="855e2-146">可能的解决方案是重新启用的站点中的扩展*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="855e2-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="855e2-147">下面的示例演示如何能够 *.cshtml*扩展。</span><span class="sxs-lookup"><span data-stu-id="855e2-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="855e2-148">HTTP 错误 404.8-找不到</span><span class="sxs-lookup"><span data-stu-id="855e2-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="855e2-149">*配置请求筛选模块拒绝包含 hiddenSegment 部分在 URL 中的路径。*</span><span class="sxs-lookup"><span data-stu-id="855e2-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="855e2-150">如果请求受保护的资源，则可能出现此错误 (如*Web.config*文件) 或受保护的文件夹中 (如*应用\_数据*或*应用\_代码*)。</span><span class="sxs-lookup"><span data-stu-id="855e2-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="855e2-151">这种类型的页未处理 （服务器错误 '/' 应用程序中）</span><span class="sxs-lookup"><span data-stu-id="855e2-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="855e2-152">请参阅 HTTP 错误 404.17 前面的说明。</span><span class="sxs-lookup"><span data-stu-id="855e2-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="855e2-153">Razor 代码的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="855e2-154">名称*类*当前上下文中不存在</span><span class="sxs-lookup"><span data-stu-id="855e2-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="855e2-155">通常情况下，请参阅此错误的原因在于`class`未安装一个帮助器，但该帮助器的引用。</span><span class="sxs-lookup"><span data-stu-id="855e2-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="855e2-156">例如，如果你尝试使用一个帮助器，但尚未从 NuGet 安装包，您将看到此错误。</span><span class="sxs-lookup"><span data-stu-id="855e2-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="855e2-157">使用 WebMatrix 中的库查找和安装的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="855e2-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="855e2-158">如果已安装该帮助器，但页面仍不能识别它，请尝试添加添加`using`语句的代码。</span><span class="sxs-lookup"><span data-stu-id="855e2-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="855e2-159">在`using`语句，包括帮助程序的命名空间的引用。</span><span class="sxs-lookup"><span data-stu-id="855e2-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="855e2-160">例如，ASP.NET Web 帮助器包中的基本帮助器位于`System.Web.Helpers`命名空间。</span><span class="sxs-lookup"><span data-stu-id="855e2-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="855e2-161">在想要使用该帮助器页的顶部，添加下面一行：</span><span class="sxs-lookup"><span data-stu-id="855e2-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="855e2-162">安全和成员身份的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-162">Issues with Security and Membership</span></span>

<span data-ttu-id="855e2-163">如果使用内置的安全 （成员资格） 系统中 ASP.NET Web Pages (Razor)，可能会遇到以下问题。</span><span class="sxs-lookup"><span data-stu-id="855e2-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="855e2-164">若要调用此方法，"Membership.Provider"属性必须是"采用 ExtendedMembershipProvider"的实例</span><span class="sxs-lookup"><span data-stu-id="855e2-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="855e2-165">此错误可能指示没有`AspNetSqlMembershipProvider`配置类。</span><span class="sxs-lookup"><span data-stu-id="855e2-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="855e2-166">（一种症状是站点本地可正常使用，但会引发此错误时将其发布到宿主提供程序的服务器。）此问题的一个解决方法是通过将以下内容添加到站点的来显式启用简单成员资格*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="855e2-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="855e2-167">发送电子邮件的问题</span><span class="sxs-lookup"><span data-stu-id="855e2-167">Issues with Sending Email</span></span>

<span data-ttu-id="855e2-168">发送电子邮件的问题可能很难调试。</span><span class="sxs-lookup"><span data-stu-id="855e2-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="855e2-169">最初的问题可能无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="855e2-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="855e2-170">如果连接成功，ASP.NET 会将消息传送到 SMTP 服务器中。</span><span class="sxs-lookup"><span data-stu-id="855e2-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="855e2-171">但是，可能会有问题，并显示消息本身，以防止将其发送 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="855e2-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="855e2-172">如果你的应用程序未成功发送电子邮件，请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="855e2-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="855e2-173">SMTP 服务器名称通常是类似于`smtp.provider.com`或`smtp.provider.net`。</span><span class="sxs-lookup"><span data-stu-id="855e2-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="855e2-174">但是，如果将站点发布到宿主提供程序，将 SMTP 服务器名此时可能`localhost`。</span><span class="sxs-lookup"><span data-stu-id="855e2-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="855e2-175">因为已发布和提供程序的服务器上运行你的站点之后，SMTP 服务器可能会在本地从你的应用程序的角度来看，将出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="855e2-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="855e2-176">此服务器名称中的更改可能意味着您必须在发布过程中更改 SMTP 服务器名称。</span><span class="sxs-lookup"><span data-stu-id="855e2-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="855e2-177">端口号通常为 25。</span><span class="sxs-lookup"><span data-stu-id="855e2-177">The port number is usually 25.</span></span> <span data-ttu-id="855e2-178">但是，某些提供程序需要使用端口 587 或某些其他端口。</span><span class="sxs-lookup"><span data-stu-id="855e2-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="855e2-179">咨询哪个端口号，他们期望您要使用的 SMTP 服务器的所有者。</span><span class="sxs-lookup"><span data-stu-id="855e2-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="855e2-180">请确保使用正确的凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="855e2-181">如果你已将站点发布到宿主提供程序，使用提供程序专门指示用于电子邮件的凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="855e2-182">这些凭据可能不同于你使用发布的凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="855e2-183">有时您根本不需要凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="855e2-184">如果要使用您个人的 ISP 来发送电子邮件，电子邮件提供商可能已经知道你的凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="855e2-185">发布后，你可能需要使用比测试本地计算机上的其他凭据。</span><span class="sxs-lookup"><span data-stu-id="855e2-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="855e2-186">如果你的电子邮件提供商使用加密，请设置`WebMail.EnableSsl`到`true`。</span><span class="sxs-lookup"><span data-stu-id="855e2-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="855e2-187">如果发送电子邮件时出错，可能会看到如下所示的标准 ASP.NET 错误消息：</span><span class="sxs-lookup"><span data-stu-id="855e2-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![ASP.NET 错误消息时使用电子邮件问题](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="855e2-189">此外可以调试使用发送电子邮件问题`try-catch`块，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="855e2-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="855e2-190">当你使用`try-catch`块中，ASP.NET 不会显示其标准错误消息。</span><span class="sxs-lookup"><span data-stu-id="855e2-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="855e2-191">相反，您可以捕获中的错误`catch`的块部分。</span><span class="sxs-lookup"><span data-stu-id="855e2-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="855e2-192">替换为相应值`your-SMTP-server-name`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="855e2-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="855e2-193">某些错误消息可能会看到这种方式包括：</span><span class="sxs-lookup"><span data-stu-id="855e2-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="855e2-194">*无法发送邮件。*</span><span class="sxs-lookup"><span data-stu-id="855e2-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="855e2-195">或</span><span class="sxs-lookup"><span data-stu-id="855e2-195">-or-</span></span>

    <span data-ttu-id="855e2-196">*连接尝试失败，因为被连接的方未正确响应时间或建立的连接失败，因为连接的主机未能响应一段时间后*</span><span class="sxs-lookup"><span data-stu-id="855e2-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="855e2-197">此错误通常意味着应用程序无法连接到 SMTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="855e2-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="855e2-198">请检查服务器名和端口号。</span><span class="sxs-lookup"><span data-stu-id="855e2-198">Check the server name and port number.</span></span>
- <span data-ttu-id="855e2-199"><em>邮箱不可用。服务器响应为： 5.1.0 &lt; someuser@invaliddomain &gt;发件人已拒绝： 无效的发件人域</em></span><span class="sxs-lookup"><span data-stu-id="855e2-199"><em>Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain</em></span></span>

    <span data-ttu-id="855e2-200">此消息可能指示`From`地址不正确或缺少。</span><span class="sxs-lookup"><span data-stu-id="855e2-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="855e2-201">*指定的字符串不是窗体所需的电子邮件地址。*</span><span class="sxs-lookup"><span data-stu-id="855e2-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="855e2-202">此错误可能指示的值`To`或`From`属性不会识别为电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="855e2-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="855e2-203">(ASP.NET 不能检查电子邮件地址是否有效，只有它的格式正确，如*name@domain.com*。)</span><span class="sxs-lookup"><span data-stu-id="855e2-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="855e2-204">删除显示的错误的标记 (`@errorMessage`) 页面发布到实时站点之前。</span><span class="sxs-lookup"><span data-stu-id="855e2-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="855e2-205">它不是一个好办法，请参阅从服务器获取的错误消息的用户。</span><span class="sxs-lookup"><span data-stu-id="855e2-205">It's not a good idea to let users see error messages that you get from a server.</span></span>


<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="855e2-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="855e2-206">Additional Resources</span></span>

[<span data-ttu-id="855e2-207">ASP.NET 网页 (Razor) 常见问题解答</span><span class="sxs-lookup"><span data-stu-id="855e2-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="855e2-208">[WebMatrix 和 ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 网站上的论坛</span><span class="sxs-lookup"><span data-stu-id="855e2-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
