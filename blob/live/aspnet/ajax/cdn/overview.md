---
uid: ajax/cdn/overview
title: "Microsoft Ajax 内容交付网络 |Microsoft 文档"
author: rick-anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: f69f707ba64d13fc372b7bc44718c9dcf8cec6e2
ms.sourcegitcommit: 3f491f887074310fc0f145cd01a670aa63b969e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="cfc7a-102">Microsoft Ajax 内容交付网络</span><span class="sxs-lookup"><span data-stu-id="cfc7a-102">Microsoft Ajax Content Delivery Network</span></span>
====================
<span data-ttu-id="cfc7a-103">注意： Microsoft Ajax CDN 具有超越使用 Azure CDN 没有 SLA。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-103">Note: The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="cfc7a-104">目录</span><span class="sxs-lookup"><span data-stu-id="cfc7a-104">Table of Contents</span></span>

<span data-ttu-id="cfc7a-105">**[重命名为 ajax.aspnetcdn.com ajax.microsoft.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-105">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="cfc7a-106">**[Visual Studio.vsdoc 支持](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-106">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="cfc7a-107">**[使用 ASP.NET Ajax 从 CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-107">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="cfc7a-108">**[使用 jQuery 从 CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-108">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="cfc7a-109">**[使用 jQuery UI CDN。](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-109">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="cfc7a-110">**[第三方 CDN 上的文件](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="cfc7a-110">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="cfc7a-111">在 CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-111">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="cfc7a-112">jQuery CDN 上的迁移发行版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-112">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="cfc7a-113">jQuery CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-113">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="cfc7a-114">jQuery CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-114">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="cfc7a-115">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-115">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="cfc7a-116">jQuery CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-116">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="cfc7a-117">jQuery CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-117">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="cfc7a-118">jQuery CDN 上的数据表版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-118">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="cfc7a-119">在 CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-119">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="cfc7a-120">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-120">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="cfc7a-121">在 CDN 上 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-121">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="cfc7a-122">全球化 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-122">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="cfc7a-123">响应 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-123">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="cfc7a-124">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-124">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="cfc7a-125">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-125">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="cfc7a-126">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-126">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="cfc7a-127">ASP.NET Web 窗体和 CDN 上的 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-127">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="cfc7a-128">ASP.NET MVC 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="cfc7a-128">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="cfc7a-129">ASP.NET SignalR 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="cfc7a-129">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="cfc7a-130">Microsoft Ajax 内容交付网络 (CDN) 承载 jQuery 等的常用第三方 JavaScript 库，并使您能够轻松地将它们添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-130">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="cfc7a-131">例如，可以开始在此 CDN 上使用 jQuery 进行托管，只需通过添加&lt;脚本&gt;标记添加到你 ajax.aspnetcdn.com 所指向的页。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-131">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="cfc7a-132">通过利用 CDN，就可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-132">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="cfc7a-133">CDN 的内容进行缓存在世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-133">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="cfc7a-134">此外，CDN 可让浏览器重复使用缓存的第三方 JavaScript 文件位于不同域中的网站。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-134">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="cfc7a-135">如果你需要服务网页上使用安全套接字层，CDN 将支持 SSL (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-135">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="cfc7a-136">CDN 托管以下第三方脚本库也不能已上载，授权给你，由这些库的所有者：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-136">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="cfc7a-137">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-137">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="cfc7a-138">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-138">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="cfc7a-139">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-139">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="cfc7a-140">jQuery 验证 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-140">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="cfc7a-141">jQuery 周期 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-141">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="cfc7a-142">jQuery 数据表 (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="cfc7a-142">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="cfc7a-143">Microsoft Ajax CDN 还包括以下库，后者已上载的 Microsoft:</span><span class="sxs-lookup"><span data-stu-id="cfc7a-143">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="cfc7a-144">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="cfc7a-144">ASP.NET Ajax</span></span>
- <span data-ttu-id="cfc7a-145">ASP.NET MVC JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="cfc7a-145">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="cfc7a-146">ASP.NET SignalR JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="cfc7a-146">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="cfc7a-147">Microsoft 不主张对此 CDN 上承载任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-147">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-148">库的版权所有者要授权给你这些库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-148">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="cfc7a-149">仅由各自的版权所有者授予的任何可能需要下载并使用这种库的权限。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-149">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="cfc7a-150">因为这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供不保证或知识产权权限许可证 （包括任何隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-150">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="cfc7a-151">如果你想要提交你的 JavaScript 库，而你的库是顶部 JavaScript 库 （如下所列上 http://trends.builtwith.com） 或到这些库的扩展/插件之一 (a) 常用;或 (b) 有助于在 ASP.NET 上使用，则请联系AjaxCDNSubmission@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-151">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="cfc7a-152">重命名为 ajax.aspnetcdn.com ajax.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cfc7a-152">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="cfc7a-153">CDN 用于使用 microsoft.com 的域名，并且已更改为使用 aspnetcdn.com 域名。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-153">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="cfc7a-154">此更改是为了提高性能，因为当浏览器引用 microsoft.com 域它将发送任何 cookie 从该域跨网络与每个请求。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-154">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="cfc7a-155">通过重命名为 microsoft.com 之外的域名称性能可以通过增加同样可用于 25%。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-155">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="cfc7a-156">请注意 ajax.microsoft.com 将继续工作，但建议 ajax.aspnetcdn.com。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-156">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="cfc7a-157">旧格式： http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-157">Old Format: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="cfc7a-158">新的格式： http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-158">New Format: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="cfc7a-159">Visual Studio.vsdoc 支持</span><span class="sxs-lookup"><span data-stu-id="cfc7a-159">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="cfc7a-160">若要正确使用.vsdoc 文件，你需要确保你具有 VS 2008 SP1 的 Visual Studio 2008 安装和安装 vsdoc 文件的修补程序。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-160">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="cfc7a-161">你可以从此处这些：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-161">You can get these from here:</span></span>

- [<span data-ttu-id="cfc7a-162">下载 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-162">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下载 Visual Studio 2008 SP1")
- [<span data-ttu-id="cfc7a-163">下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-163">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1")

<span data-ttu-id="cfc7a-164">Visual Studio 2010 支持.vsdoc 文件而无需任何额外的修补程序。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-164">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="cfc7a-165">使用 ASP.NET Ajax 从 CDN</span><span class="sxs-lookup"><span data-stu-id="cfc7a-165">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="cfc7a-166">在使用 ASP.NET 4 时，可以将对 ASP.NET framework 脚本的所有请求重都定向到 CDN。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-166">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="cfc7a-167">从 CDN 而不是本地 web 服务器中检索脚本可以显著提高公共 ASP.NET 网站的性能。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-167">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="cfc7a-168">ScriptManager EnableCDN 属性用于将 ASP.NET framework 脚本的所有请求重都定向到 Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="cfc7a-168">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="cfc7a-169">使用 jQuery 从 CDN</span><span class="sxs-lookup"><span data-stu-id="cfc7a-169">Using jQuery from the CDN</span></span>

<span data-ttu-id="cfc7a-170">你可以使用 CDN 上托管 Web 应用程序中，通过将下面的脚本元素添加到页面的 jQuery 脚本：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-170">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="cfc7a-171">CDN 还包括对 jQuery 脚本，从而可以获取的缩减的版本使用以下元素：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-171">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="cfc7a-172">若要允许你回退到从您自己的网站上的本地路径加载 jQuery，如果 CDN 碰巧将不可用的页，请立即引用 CDN 的元素之后添加以下元素：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-172">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="cfc7a-173">下面的示例页使用 jQuery 库 （具有回退到的本地副本） 的 CDN 版本单击按钮时显示的 div 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-173">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="cfc7a-174">你可以了解有关 jQuery 和，请访问下载 jQuery 的本地副本[jQuery](http://jquery.com/) Web 站点。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-174">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="cfc7a-175">使用 jQuery UI CDN。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-175">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="cfc7a-176">CDN 还承载 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-176">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="cfc7a-177">JQuery UI 库包括一套丰富的小组件和可以在 ASP.NET 应用程序中使用的效果。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-177">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="cfc7a-178">例如，以下页演示如何使用 jQuery UI Datepicker ASP.NET Web 窗体应用程序的上下文中显示一个弹出日历：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-178">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="cfc7a-179">当你将焦点移到使用你键盘文本框中时，将显示日历：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-179">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![使用包含 Datepicker 创建弹出日历](overview/_static/image1.png)

<span data-ttu-id="cfc7a-181">请注意，你必须在上面的代码包含从 CDN 的三个文件：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-181">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="cfc7a-182">JQuery 库&mdash;jQuery UI 库依赖于 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-182">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="cfc7a-183">添加 jQuery UI 库之前，你必须 jQuery 库添加到你的页面。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-183">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="cfc7a-184">JQuery UI 库&mdash;jQuery UI 库包含的所有 jQuery 用户界面效果和小组件，如在上述页面中使用包含 Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-184">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="cfc7a-185">JQuery UI 主题&mdash;jQuery UI 支持不同的主题。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-185">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="cfc7a-186">上述页面中包含一个 CSS 文件导入 Redmond 主题的链接。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-186">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="cfc7a-187">所有标准 jQuery UI 主题位于 CDN。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-187">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="cfc7a-188">[访问此页面](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN 上")若要查看每个主题的缩略图。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-188">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="cfc7a-189">若要了解有关 jQuery UI 库的详细信息，请访问官方[jQuery UI 网站](http://jQueryUI.com "jQuery UI 网站")。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-189">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="cfc7a-190">第三方 CDN 上的文件</span><span class="sxs-lookup"><span data-stu-id="cfc7a-190">Third-Party Files on the CDN</span></span>

<span data-ttu-id="cfc7a-191">CDN 托管某些最常用的第三方 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-191">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="cfc7a-192">Microsoft 不主张对此 CDN 上承载任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-192">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-193">库的版权所有者要授权给你这些库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-193">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="cfc7a-194">仅由各自的版权所有者授予的任何可能需要下载并使用这种库的权限。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-194">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="cfc7a-195">因为这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供不保证或知识产权权限许可证 （包括任何隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-195">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-196">在 CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-196">jQuery Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-197">在 CDN 上托管的 jQuery 以下版本：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-197">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="cfc7a-198">jQuery 版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-198">jQuery version 3.3.1</span></span>
- <span data-ttu-id="cfc7a-199">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-199">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js</span></span>
- <span data-ttu-id="cfc7a-200">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-200">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js</span></span>
- <span data-ttu-id="cfc7a-201">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-201">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map</span></span>
- <span data-ttu-id="cfc7a-202">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-202">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js</span></span>
- <span data-ttu-id="cfc7a-203">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-203">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-204">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-204">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map</span></span>

#### <a name="jquery-version-321"></a><span data-ttu-id="cfc7a-205">jQuery 版本 3.2.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-205">jQuery version 3.2.1</span></span>
- <span data-ttu-id="cfc7a-206">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-206">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js</span></span>
- <span data-ttu-id="cfc7a-207">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-207">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js</span></span>
- <span data-ttu-id="cfc7a-208">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-208">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map</span></span>
- <span data-ttu-id="cfc7a-209">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-209">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js</span></span>
- <span data-ttu-id="cfc7a-210">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-210">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-211">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-211">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map</span></span>

#### <a name="jquery-version-320"></a><span data-ttu-id="cfc7a-212">jQuery 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-212">jQuery version 3.2.0</span></span>

- <span data-ttu-id="cfc7a-213">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-213">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js</span></span>
- <span data-ttu-id="cfc7a-214">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-214">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js</span></span>
- <span data-ttu-id="cfc7a-215">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-215">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map</span></span>
- <span data-ttu-id="cfc7a-216">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-216">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js</span></span>
- <span data-ttu-id="cfc7a-217">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-217">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-218">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-218">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map</span></span>

#### <a name="jquery-version-311"></a><span data-ttu-id="cfc7a-219">jQuery 版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-219">jQuery version 3.1.1</span></span>

- <span data-ttu-id="cfc7a-220">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-220">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js</span></span>
- <span data-ttu-id="cfc7a-221">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-221">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js</span></span>
- <span data-ttu-id="cfc7a-222">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-222">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map</span></span>
- <span data-ttu-id="cfc7a-223">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-223">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js</span></span>
- <span data-ttu-id="cfc7a-224">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-224">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-225">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-225">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map</span></span>

#### <a name="jquery-version-310"></a><span data-ttu-id="cfc7a-226">jQuery 版本 3.1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-226">jQuery version 3.1.0</span></span>

- <span data-ttu-id="cfc7a-227">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-227">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js</span></span>
- <span data-ttu-id="cfc7a-228">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-228">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js</span></span>
- <span data-ttu-id="cfc7a-229">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-229">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map</span></span>
- <span data-ttu-id="cfc7a-230">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-230">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js</span></span>
- <span data-ttu-id="cfc7a-231">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-231">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-232">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-232">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map</span></span>

#### <a name="jquery-version-300"></a><span data-ttu-id="cfc7a-233">jQuery 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-233">jQuery version 3.0.0</span></span>

- <span data-ttu-id="cfc7a-234">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-234">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js</span></span>
- <span data-ttu-id="cfc7a-235">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-235">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js</span></span>
- <span data-ttu-id="cfc7a-236">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-236">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map</span></span>
- <span data-ttu-id="cfc7a-237">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-237">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js</span></span>
- <span data-ttu-id="cfc7a-238">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-238">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js</span></span>
- <span data-ttu-id="cfc7a-239">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-239">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map</span></span>

#### <a name="jquery-version-224"></a><span data-ttu-id="cfc7a-240">jQuery 版本 2.2.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-240">jQuery version 2.2.4</span></span>

- <span data-ttu-id="cfc7a-241">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-241">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js</span></span>
- <span data-ttu-id="cfc7a-242">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-242">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js</span></span>
- <span data-ttu-id="cfc7a-243">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-243">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map</span></span>

#### <a name="jquery-version-223"></a><span data-ttu-id="cfc7a-244">jQuery 版本 2.2.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-244">jQuery version 2.2.3</span></span>

- <span data-ttu-id="cfc7a-245">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-245">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js</span></span>
- <span data-ttu-id="cfc7a-246">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-246">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js</span></span>
- <span data-ttu-id="cfc7a-247">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-247">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map</span></span>

#### <a name="jquery-version-222"></a><span data-ttu-id="cfc7a-248">jQuery 版本 2.2.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-248">jQuery version 2.2.2</span></span>

- <span data-ttu-id="cfc7a-249">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-249">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js</span></span>
- <span data-ttu-id="cfc7a-250">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-250">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js</span></span>
- <span data-ttu-id="cfc7a-251">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-251">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map</span></span>

#### <a name="jquery-version-221"></a><span data-ttu-id="cfc7a-252">jQuery 2.2.1 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-252">jQuery version 2.2.1</span></span>

- <span data-ttu-id="cfc7a-253">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-253">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js</span></span>
- <span data-ttu-id="cfc7a-254">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-254">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js</span></span>
- <span data-ttu-id="cfc7a-255">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-255">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map</span></span>

#### <a name="jquery-version-220"></a><span data-ttu-id="cfc7a-256">jQuery 版本 2.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-256">jQuery version 2.2.0</span></span>

- <span data-ttu-id="cfc7a-257">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-257">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js</span></span>
- <span data-ttu-id="cfc7a-258">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-258">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js</span></span>
- <span data-ttu-id="cfc7a-259">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-259">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map</span></span>

#### <a name="jquery-version-214"></a><span data-ttu-id="cfc7a-260">jQuery 版本 2.1.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-260">jQuery version 2.1.4</span></span>

- <span data-ttu-id="cfc7a-261">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-261">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js</span></span>
- <span data-ttu-id="cfc7a-262">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-262">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js</span></span>
- <span data-ttu-id="cfc7a-263">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-263">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map</span></span>

#### <a name="jquery-version-213"></a><span data-ttu-id="cfc7a-264">jQuery 版本 2.1.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-264">jQuery version 2.1.3</span></span>

- <span data-ttu-id="cfc7a-265">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-265">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js</span></span>
- <span data-ttu-id="cfc7a-266">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-266">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js</span></span>
- <span data-ttu-id="cfc7a-267">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-267">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map</span></span>

#### <a name="jquery-version-212"></a><span data-ttu-id="cfc7a-268">jQuery 版本 2.1.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-268">jQuery version 2.1.2</span></span>

- <span data-ttu-id="cfc7a-269">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-269">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js</span></span>
- <span data-ttu-id="cfc7a-270">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-270">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js</span></span>

#### <a name="jquery-version-211"></a><span data-ttu-id="cfc7a-271">jQuery 版本 2.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-271">jQuery version 2.1.1</span></span>

- <span data-ttu-id="cfc7a-272">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-272">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js</span></span>
- <span data-ttu-id="cfc7a-273">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-273">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js</span></span>
- <span data-ttu-id="cfc7a-274">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-274">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map</span></span>

#### <a name="jquery-version-210"></a><span data-ttu-id="cfc7a-275">jQuery 版本 2.1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-275">jQuery version 2.1.0</span></span>

- <span data-ttu-id="cfc7a-276">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-276">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js</span></span>
- <span data-ttu-id="cfc7a-277">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-277">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js</span></span>
- <span data-ttu-id="cfc7a-278">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-278">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-279">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-279">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map</span></span>

#### <a name="jquery-version-203"></a><span data-ttu-id="cfc7a-280">jQuery 版本 2.0.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-280">jQuery version 2.0.3</span></span>

- <span data-ttu-id="cfc7a-281">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-281">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js</span></span>
- <span data-ttu-id="cfc7a-282">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-282">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js</span></span>
- <span data-ttu-id="cfc7a-283">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-283">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-284">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-284">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map</span></span>

#### <a name="jquery-version-202"></a><span data-ttu-id="cfc7a-285">jQuery 版本 2.0.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-285">jQuery version 2.0.2</span></span>

- <span data-ttu-id="cfc7a-286">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-286">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js</span></span>
- <span data-ttu-id="cfc7a-287">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-287">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js</span></span>
- <span data-ttu-id="cfc7a-288">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-288">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-289">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-289">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map</span></span>

#### <a name="jquery-version-201"></a><span data-ttu-id="cfc7a-290">jQuery 版本 2.0.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-290">jQuery version 2.0.1</span></span>

- <span data-ttu-id="cfc7a-291">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-291">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js</span></span>
- <span data-ttu-id="cfc7a-292">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-292">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js</span></span>
- <span data-ttu-id="cfc7a-293">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-293">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-294">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-294">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map</span></span>

#### <a name="jquery-version-200"></a><span data-ttu-id="cfc7a-295">jQuery 版本 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-295">jQuery version 2.0.0</span></span>

- <span data-ttu-id="cfc7a-296">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-296">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js</span></span>
- <span data-ttu-id="cfc7a-297">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-297">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js</span></span>
- <span data-ttu-id="cfc7a-298">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-298">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-299">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-299">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map</span></span>

#### <a name="jquery-version-1124"></a><span data-ttu-id="cfc7a-300">jQuery 版本 1.12.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-300">jQuery version 1.12.4</span></span>

- <span data-ttu-id="cfc7a-301">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-301">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js</span></span>
- <span data-ttu-id="cfc7a-302">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-302">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js</span></span>
- <span data-ttu-id="cfc7a-303">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-303">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map</span></span>

#### <a name="jquery-version-1123"></a><span data-ttu-id="cfc7a-304">jQuery 版本 1.12.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-304">jQuery version 1.12.3</span></span>

- <span data-ttu-id="cfc7a-305">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-305">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js</span></span>
- <span data-ttu-id="cfc7a-306">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-306">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js</span></span>
- <span data-ttu-id="cfc7a-307">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-307">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map</span></span>

#### <a name="jquery-version-1122"></a><span data-ttu-id="cfc7a-308">jQuery 版本 1.12.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-308">jQuery version 1.12.2</span></span>

- <span data-ttu-id="cfc7a-309">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-309">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js</span></span>
- <span data-ttu-id="cfc7a-310">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-310">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js</span></span>
- <span data-ttu-id="cfc7a-311">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-311">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map</span></span>

#### <a name="jquery-version-1121"></a><span data-ttu-id="cfc7a-312">jQuery 版本 1.12.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-312">jQuery version 1.12.1</span></span>

- <span data-ttu-id="cfc7a-313">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-313">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js</span></span>
- <span data-ttu-id="cfc7a-314">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-314">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js</span></span>
- <span data-ttu-id="cfc7a-315">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-315">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map</span></span>

#### <a name="jquery-version-1120"></a><span data-ttu-id="cfc7a-316">jQuery 版本 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-316">jQuery version 1.12.0</span></span>

- <span data-ttu-id="cfc7a-317">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-317">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js</span></span>
- <span data-ttu-id="cfc7a-318">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-318">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js</span></span>
- <span data-ttu-id="cfc7a-319">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-319">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map</span></span>

#### <a name="jquery-version-1113"></a><span data-ttu-id="cfc7a-320">jQuery 版本 1.11.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-320">jQuery version 1.11.3</span></span>

- <span data-ttu-id="cfc7a-321">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-321">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js</span></span>
- <span data-ttu-id="cfc7a-322">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-322">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js</span></span>
- <span data-ttu-id="cfc7a-323">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-323">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map</span></span>

#### <a name="jquery-version-1112"></a><span data-ttu-id="cfc7a-324">jQuery 版本 1.11.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-324">jQuery version 1.11.2</span></span>

- <span data-ttu-id="cfc7a-325">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-325">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js</span></span>
- <span data-ttu-id="cfc7a-326">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-326">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js</span></span>
- <span data-ttu-id="cfc7a-327">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-327">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map</span></span>

#### <a name="jquery-version-1111"></a><span data-ttu-id="cfc7a-328">jQuery 版本 1.11.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-328">jQuery version 1.11.1</span></span>

- <span data-ttu-id="cfc7a-329">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-329">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js</span></span>
- <span data-ttu-id="cfc7a-330">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-330">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js</span></span>
- <span data-ttu-id="cfc7a-331">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-331">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map</span></span>

#### <a name="jquery-version-1110"></a><span data-ttu-id="cfc7a-332">jQuery 版本 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-332">jQuery version 1.11.0</span></span>

- <span data-ttu-id="cfc7a-333">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-333">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js</span></span>
- <span data-ttu-id="cfc7a-334">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-334">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js</span></span>
- <span data-ttu-id="cfc7a-335">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-335">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-336">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-336">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map</span></span>

#### <a name="jquery-version-1102"></a><span data-ttu-id="cfc7a-337">jQuery 版本 1.10.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-337">jQuery version 1.10.2</span></span>

- <span data-ttu-id="cfc7a-338">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-338">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js</span></span>
- <span data-ttu-id="cfc7a-339">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-339">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js</span></span>
- <span data-ttu-id="cfc7a-340">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-340">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-341">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-341">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map</span></span>

#### <a name="jquery-version-1101"></a><span data-ttu-id="cfc7a-342">jQuery 版本 1.10.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-342">jQuery version 1.10.1</span></span>

- <span data-ttu-id="cfc7a-343">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-343">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js</span></span>
- <span data-ttu-id="cfc7a-344">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-344">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js</span></span>
- <span data-ttu-id="cfc7a-345">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-345">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-346">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-346">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map</span></span>

#### <a name="jquery-version-1100"></a><span data-ttu-id="cfc7a-347">jQuery 版本 1.10.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-347">jQuery version 1.10.0</span></span>

- <span data-ttu-id="cfc7a-348">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-348">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js</span></span>
- <span data-ttu-id="cfc7a-349">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-349">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js</span></span>
- <span data-ttu-id="cfc7a-350">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-350">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-351">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-351">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map</span></span>

#### <a name="jquery-version-191"></a><span data-ttu-id="cfc7a-352">jQuery 版本 1.9.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-352">jQuery version 1.9.1</span></span>

- <span data-ttu-id="cfc7a-353">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-353">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js</span></span>
- <span data-ttu-id="cfc7a-354">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-354">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js</span></span>
- <span data-ttu-id="cfc7a-355">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-355">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-356">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-356">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map</span></span>

#### <a name="jquery-version-190"></a><span data-ttu-id="cfc7a-357">jQuery 版本 1.9.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-357">jQuery version 1.9.0</span></span>

- <span data-ttu-id="cfc7a-358">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-358">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js</span></span>
- <span data-ttu-id="cfc7a-359">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-359">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js</span></span>
- <span data-ttu-id="cfc7a-360">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-360">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-361">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-361">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map</span></span>

#### <a name="jquery-version-183"></a><span data-ttu-id="cfc7a-362">jQuery 版本 1.8.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-362">jQuery version 1.8.3</span></span>

- <span data-ttu-id="cfc7a-363">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-363">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js</span></span>
- <span data-ttu-id="cfc7a-364">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-364">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js</span></span>
- <span data-ttu-id="cfc7a-365">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-365">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js</span></span>

#### <a name="jquery-version-182"></a><span data-ttu-id="cfc7a-366">jQuery 版本 1.8.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-366">jQuery version 1.8.2</span></span>

- <span data-ttu-id="cfc7a-367">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-367">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js</span></span>
- <span data-ttu-id="cfc7a-368">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-368">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js</span></span>
- <span data-ttu-id="cfc7a-369">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-369">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js</span></span>

#### <a name="jquery-version-181"></a><span data-ttu-id="cfc7a-370">jQuery 1.8.1 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-370">jQuery version 1.8.1</span></span>

- <span data-ttu-id="cfc7a-371">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-371">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js</span></span>
- <span data-ttu-id="cfc7a-372">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-372">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js</span></span>
- <span data-ttu-id="cfc7a-373">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-373">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js</span></span>

#### <a name="jquery-version-180"></a><span data-ttu-id="cfc7a-374">jQuery 版本 1.8.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-374">jQuery version 1.8.0</span></span>

- <span data-ttu-id="cfc7a-375">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-375">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="cfc7a-376">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-376">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js</span></span>
- <span data-ttu-id="cfc7a-377">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-377">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js</span></span>

#### <a name="jquery-version-172"></a><span data-ttu-id="cfc7a-378">jQuery 版本 1.7.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-378">jQuery version 1.7.2</span></span>

- <span data-ttu-id="cfc7a-379">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-379">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js</span></span>
- <span data-ttu-id="cfc7a-380">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-380">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js</span></span>

#### <a name="jquery-version-171"></a><span data-ttu-id="cfc7a-381">jQuery 版本 1.7.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-381">jQuery version 1.7.1</span></span>

- <span data-ttu-id="cfc7a-382">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-382">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js</span></span>
- <span data-ttu-id="cfc7a-383">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-383">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js</span></span>
- <span data-ttu-id="cfc7a-384">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-384">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js</span></span>

#### <a name="jquery-version-17"></a><span data-ttu-id="cfc7a-385">jQuery 版本 1.7</span><span class="sxs-lookup"><span data-stu-id="cfc7a-385">jQuery version 1.7</span></span>

- <span data-ttu-id="cfc7a-386">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-386">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js</span></span>
- <span data-ttu-id="cfc7a-387">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-387">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js</span></span>
- <span data-ttu-id="cfc7a-388">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-388">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js</span></span>

#### <a name="jquery-version-164"></a><span data-ttu-id="cfc7a-389">jQuery 版本 1.6.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-389">jQuery version 1.6.4</span></span>

- <span data-ttu-id="cfc7a-390">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-390">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js</span></span>
- <span data-ttu-id="cfc7a-391">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-391">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js</span></span>
- <span data-ttu-id="cfc7a-392">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-392">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js</span></span>

#### <a name="jquery-version-163"></a><span data-ttu-id="cfc7a-393">jQuery 版本 1.6.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-393">jQuery version 1.6.3</span></span>

- <span data-ttu-id="cfc7a-394">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-394">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js</span></span>
- <span data-ttu-id="cfc7a-395">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-395">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js</span></span>
- <span data-ttu-id="cfc7a-396">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-396">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js</span></span>

#### <a name="jquery-version-162"></a><span data-ttu-id="cfc7a-397">jQuery 版本 1.6.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-397">jQuery version 1.6.2</span></span>

- <span data-ttu-id="cfc7a-398">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-398">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js</span></span>
- <span data-ttu-id="cfc7a-399">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-399">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js</span></span>
- <span data-ttu-id="cfc7a-400">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-400">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js</span></span>

#### <a name="jquery-version-161"></a><span data-ttu-id="cfc7a-401">jQuery 版本 1.6.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-401">jQuery version 1.6.1</span></span>

- <span data-ttu-id="cfc7a-402">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-402">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js</span></span>
- <span data-ttu-id="cfc7a-403">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-403">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js</span></span>
- <span data-ttu-id="cfc7a-404">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-404">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js</span></span>

#### <a name="jquery-version-16"></a><span data-ttu-id="cfc7a-405">jQuery 版本 1.6</span><span class="sxs-lookup"><span data-stu-id="cfc7a-405">jQuery version 1.6</span></span>

- <span data-ttu-id="cfc7a-406">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-406">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js</span></span>
- <span data-ttu-id="cfc7a-407">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-407">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js</span></span>
- <span data-ttu-id="cfc7a-408">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-408">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js</span></span>

#### <a name="jquery-version-152"></a><span data-ttu-id="cfc7a-409">jQuery 版本 1.5.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-409">jQuery version 1.5.2</span></span>

- <span data-ttu-id="cfc7a-410">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-410">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js</span></span>
- <span data-ttu-id="cfc7a-411">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-411">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js</span></span>
- <span data-ttu-id="cfc7a-412">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-412">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js</span></span>

#### <a name="jquery-version-151"></a><span data-ttu-id="cfc7a-413">jQuery 版本 1.5.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-413">jQuery version 1.5.1</span></span>

- <span data-ttu-id="cfc7a-414">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-414">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js</span></span>
- <span data-ttu-id="cfc7a-415">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-415">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js</span></span>
- <span data-ttu-id="cfc7a-416">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-416">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js</span></span>

#### <a name="jquery-version-15"></a><span data-ttu-id="cfc7a-417">jQuery 版本 1.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-417">jQuery version 1.5</span></span>

- <span data-ttu-id="cfc7a-418">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-418">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js</span></span>
- <span data-ttu-id="cfc7a-419">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-419">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js</span></span>
- <span data-ttu-id="cfc7a-420">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-420">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js</span></span>

#### <a name="jquery-version-144"></a><span data-ttu-id="cfc7a-421">jQuery 版本 1.4.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-421">jQuery version 1.4.4</span></span>

- <span data-ttu-id="cfc7a-422">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-422">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js</span></span>
- <span data-ttu-id="cfc7a-423">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-423">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js</span></span>
- <span data-ttu-id="cfc7a-424">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-424">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js</span></span>

#### <a name="jquery-version-143"></a><span data-ttu-id="cfc7a-425">jQuery 版本 1.4.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-425">jQuery version 1.4.3</span></span>

- <span data-ttu-id="cfc7a-426">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-426">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js</span></span>
- <span data-ttu-id="cfc7a-427">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-427">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js</span></span>
- <span data-ttu-id="cfc7a-428">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-428">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js</span></span>

#### <a name="jquery-version-142"></a><span data-ttu-id="cfc7a-429">jQuery 版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-429">jQuery version 1.4.2</span></span>

- <span data-ttu-id="cfc7a-430">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-430">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js</span></span>
- <span data-ttu-id="cfc7a-431">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-431">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js</span></span>
- <span data-ttu-id="cfc7a-432">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-432">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js</span></span>

#### <a name="jquery-version-141"></a><span data-ttu-id="cfc7a-433">jQuery 版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-433">jQuery version 1.4.1</span></span>

- <span data-ttu-id="cfc7a-434">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-434">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js</span></span>
- <span data-ttu-id="cfc7a-435">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-435">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js</span></span>
- <span data-ttu-id="cfc7a-436">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-436">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js</span></span>

#### <a name="jquery-version-14"></a><span data-ttu-id="cfc7a-437">jQuery 1.4 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-437">jQuery version 1.4</span></span>

- <span data-ttu-id="cfc7a-438">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-438">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js</span></span>
- <span data-ttu-id="cfc7a-439">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-439">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js</span></span>

#### <a name="jquery-version-132"></a><span data-ttu-id="cfc7a-440">jQuery 版本 1.3.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-440">jQuery version 1.3.2</span></span>

- <span data-ttu-id="cfc7a-441">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-441">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js</span></span>
- <span data-ttu-id="cfc7a-442">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-442">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js</span></span>
- <span data-ttu-id="cfc7a-443">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-443">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js</span></span>
- <span data-ttu-id="cfc7a-444">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-444">http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js</span></span>

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-445">jQuery CDN 上的迁移发行版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-445">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-446">在 CDN 上托管的 jQuery 迁移以下版本：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-446">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="cfc7a-447">jQuery 迁移 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-447">jQuery Migrate version 3.0.0</span></span>

- <span data-ttu-id="cfc7a-448">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-448">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js</span></span>
- <span data-ttu-id="cfc7a-449">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-449">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js</span></span>

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="cfc7a-450">jQuery 迁移 1.2.1 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-450">jQuery Migrate version 1.2.1</span></span>

- <span data-ttu-id="cfc7a-451">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-451">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js</span></span>
- <span data-ttu-id="cfc7a-452">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-452">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js</span></span>

<span data-ttu-id="cfc7a-453">jQuery 迁移版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-453">jQuery Migrate version 1.2.0</span></span>

- <span data-ttu-id="cfc7a-454">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-454">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js</span></span>
- <span data-ttu-id="cfc7a-455">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-455">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js</span></span>

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="cfc7a-456">jQuery 迁移版本 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-456">jQuery Migrate version 1.1.1</span></span>

- <span data-ttu-id="cfc7a-457">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-457">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js</span></span>
- <span data-ttu-id="cfc7a-458">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-458">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js</span></span>

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="cfc7a-459">jQuery 迁移 1.1.0 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-459">jQuery Migrate version 1.1.0</span></span>

- <span data-ttu-id="cfc7a-460">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-460">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js</span></span>
- <span data-ttu-id="cfc7a-461">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-461">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js</span></span>

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="cfc7a-462">jQuery 迁移版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-462">jQuery Migrate version 1.0.0</span></span>

- <span data-ttu-id="cfc7a-463">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-463">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js</span></span>
- <span data-ttu-id="cfc7a-464">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-464">http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js</span></span>

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-465">jQuery CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-465">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-466">在此 CDN 上托管以下版本的 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-466">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-467">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-467">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-468">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-468">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-469">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-469">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-470">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-470">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-471">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-471">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-472">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-472">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-473">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-473">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-474">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-474">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-475">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-475">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-476">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-476">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-477">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-477">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN 上的用户界面")
- [<span data-ttu-id="cfc7a-478">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-478">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-479">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-479">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-480">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-480">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-481">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-481">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-482">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-482">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-483">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="cfc7a-483">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-484">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="cfc7a-484">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-485">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="cfc7a-485">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-486">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="cfc7a-486">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-487">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="cfc7a-487">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-488">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="cfc7a-488">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-489">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="cfc7a-489">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-490">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="cfc7a-490">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-491">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="cfc7a-491">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-492">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="cfc7a-492">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-493">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="cfc7a-493">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-494">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="cfc7a-494">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-495">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="cfc7a-495">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-496">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="cfc7a-496">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-497">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="cfc7a-497">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-498">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="cfc7a-498">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-499">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="cfc7a-499">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-500">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="cfc7a-500">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-501">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="cfc7a-501">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-502">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-502">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-503">jQuery CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-503">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-504">在此 CDN 上托管以下版本的 jQuery 验证库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-504">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-505">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-505">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-506">jQuery 验证 1.17.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-506">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 验证 1.17.0")
- [<span data-ttu-id="cfc7a-507">jQuery 验证 1.16.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-507">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 验证 1.16.0")
- [<span data-ttu-id="cfc7a-508">jQuery 验证 1.15.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-508">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 验证 1.15.1")
- [<span data-ttu-id="cfc7a-509">jQuery 验证 1.15.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-509">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 验证 1.15.0")
- [<span data-ttu-id="cfc7a-510">jQuery 验证 1.14.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-510">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 验证 1.14.0")
- [<span data-ttu-id="cfc7a-511">jQuery 验证 1.13.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-511">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 验证 1.13.1")
- [<span data-ttu-id="cfc7a-512">jQuery 验证 1.13.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-512">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 验证 1.13.0")
- [<span data-ttu-id="cfc7a-513">jQuery 验证 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-513">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 验证 1.12.0")
- [<span data-ttu-id="cfc7a-514">jQuery 验证 1.11.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-514">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 验证 1.11.1")
- [<span data-ttu-id="cfc7a-515">jQuery 验证 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-515">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 验证 1.11.0")
- [<span data-ttu-id="cfc7a-516">jQuery 验证 1.10.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-516">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 验证 1.10.0")
- [<span data-ttu-id="cfc7a-517">jQuery 验证 1.9</span><span class="sxs-lookup"><span data-stu-id="cfc7a-517">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 版本 1.9")
- [<span data-ttu-id="cfc7a-518">jQuery 验证 1.8.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-518">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 1.8.1 版")
- [<span data-ttu-id="cfc7a-519">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="cfc7a-519">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 版本 1.8")
- [<span data-ttu-id="cfc7a-520">jQuery 验证 1.7</span><span class="sxs-lookup"><span data-stu-id="cfc7a-520">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 版本 1.7")
- [<span data-ttu-id="cfc7a-521">jQuery 验证 1.6</span><span class="sxs-lookup"><span data-stu-id="cfc7a-521">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 验证 1.6")
- [<span data-ttu-id="cfc7a-522">jQuery 验证 1.5.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-522">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 验证 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-523">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-523">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-524">在此 CDN 上托管以下版本的 jQuery Mobile 库。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-524">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-525">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-525">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-526">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-526">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-527">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-527">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-528">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-528">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-529">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-529">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-530">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-530">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-531">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-531">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-532">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-532">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-533">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-533">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-534">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-534">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-535">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-535">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-536">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-536">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-537">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-537">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-538">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-538">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-539">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-539">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="cfc7a-540">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-540">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="cfc7a-541">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-541">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="cfc7a-542">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-542">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-543">jQuery CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-543">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-544">在此 CDN 上托管以下版本的 jQuery 模板插件。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-544">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-545">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-545">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-546">jQuery 模板 Beta 1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-546">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 模板 Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-547">jQuery CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-547">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-548">在此 CDN 上托管以下版本的 jQuery 周期插件。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-548">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-549">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-549">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-550">jQuery 周期 2.99</span><span class="sxs-lookup"><span data-stu-id="cfc7a-550">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 周期 2.99")
- [<span data-ttu-id="cfc7a-551">jQuery 周期 2.94</span><span class="sxs-lookup"><span data-stu-id="cfc7a-551">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery 周期 2.94")
- [<span data-ttu-id="cfc7a-552">jQuery 周期 2.88</span><span class="sxs-lookup"><span data-stu-id="cfc7a-552">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 周期 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-553">jQuery CDN 上的数据表版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-553">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-554">在此 CDN 上托管以下版本的 jQuery 数据表插件。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-554">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="cfc7a-555">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-555">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-556">jQuery 数据表 1.10.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-556">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery 数据表 1.10.5")
- [<span data-ttu-id="cfc7a-557">jQuery 数据表 1.10.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-557">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery 数据表 1.10.4")
- [<span data-ttu-id="cfc7a-558">jQuery 数据表 1.9.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-558">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery 数据表 1.9.4")
- [<span data-ttu-id="cfc7a-559">jQuery 数据表 1.9.3 放置</span><span class="sxs-lookup"><span data-stu-id="cfc7a-559">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery 数据表 1.9.3 放置")
- [<span data-ttu-id="cfc7a-560">jQuery 数据表 1.9.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-560">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery 数据表 1.9.2")
- [<span data-ttu-id="cfc7a-561">jQuery 数据表 1.9.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-561">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery 数据表 1.9.1")
- [<span data-ttu-id="cfc7a-562">jQuery 数据表 1.9.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-562">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery 数据表 1.9.0")
- [<span data-ttu-id="cfc7a-563">jQuery 数据表 1.8.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-563">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery 数据表 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-564">在 CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-564">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-565">以下版本的[Modernizr](http://www.modernizr.com "Modernizr")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-565">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- <span data-ttu-id="cfc7a-566">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-566">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js</span></span>
- <span data-ttu-id="cfc7a-567">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-567">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js</span></span>
- <span data-ttu-id="cfc7a-568">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-568">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js</span></span>
- <span data-ttu-id="cfc7a-569">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-569">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js</span></span>
- <span data-ttu-id="cfc7a-570">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-570">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js</span></span>
- <span data-ttu-id="cfc7a-571">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-571">http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js</span></span>

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-572">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-572">JSHint Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-573">以下版本的[JSHint](http://www.jshint.com "JSHint")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-573">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- <span data-ttu-id="cfc7a-574">http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-574">http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js</span></span>

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-575">在 CDN 上 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-575">Knockout Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-576">以下版本的[Knockout](http://www.knockoutjs.com "Knockout")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-576">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- <span data-ttu-id="cfc7a-577">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-577">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js</span></span>
- <span data-ttu-id="cfc7a-578">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-578">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js</span></span>
- <span data-ttu-id="cfc7a-579">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-579">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js</span></span>
- <span data-ttu-id="cfc7a-580">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-580">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-581">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-581">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js</span></span>
- <span data-ttu-id="cfc7a-582">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-582">http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-583">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-583">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js</span></span>
- <span data-ttu-id="cfc7a-584">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-584">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-585">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-585">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js</span></span>
- <span data-ttu-id="cfc7a-586">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-586">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-587">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-587">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js</span></span>
- <span data-ttu-id="cfc7a-588">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-588">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-589">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-589">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js</span></span>
- <span data-ttu-id="cfc7a-590">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-590">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-591">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-591">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js</span></span>
- <span data-ttu-id="cfc7a-592">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-592">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js</span></span>
- <span data-ttu-id="cfc7a-593">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-593">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js</span></span>
- <span data-ttu-id="cfc7a-594">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-594">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js</span></span>
- <span data-ttu-id="cfc7a-595">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-595">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js</span></span>
- <span data-ttu-id="cfc7a-596">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-596">http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js</span></span>

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-597">全球化 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-597">Globalize Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-598">以下版本的[Globalize](https://github.com/jquery/globalize "Globalize")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-598">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="cfc7a-599">全球化版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-599">Globalize version 1.0.0</span></span>

- <span data-ttu-id="cfc7a-600">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-600">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js</span></span>
- <span data-ttu-id="cfc7a-601">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-601">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js</span></span>
- <span data-ttu-id="cfc7a-602">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-602">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js</span></span>
- <span data-ttu-id="cfc7a-603">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-603">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js</span></span>
- <span data-ttu-id="cfc7a-604">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-604">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js</span></span>
- <span data-ttu-id="cfc7a-605">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-605">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js</span></span>
- <span data-ttu-id="cfc7a-606">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-606">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js</span></span>
- <span data-ttu-id="cfc7a-607">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-607">http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js</span></span>

#### <a name="globalize-version-011"></a><span data-ttu-id="cfc7a-608">全球化版本 0.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-608">Globalize version 0.1.1</span></span>

- <span data-ttu-id="cfc7a-609">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-609">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js</span></span>
- <span data-ttu-id="cfc7a-610">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-610">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js</span></span>
- <span data-ttu-id="cfc7a-611">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-611">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js</span></span>

    - <span data-ttu-id="cfc7a-612">所有区域性</span><span class="sxs-lookup"><span data-stu-id="cfc7a-612">all cultures</span></span>
- <span data-ttu-id="cfc7a-613">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture。{区域性 code}.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-613">http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js</span></span>

    - <span data-ttu-id="cfc7a-614">"{区域性的代码}"替换为所需的区域性代码、 globalize.culture.en GB.js== Microsoft 在 CDN 上的文件例如 = = 这些库上载 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-614">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-615">响应 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-615">Respond Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-616">以下版本的[https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond")在 CDN 上托管响应：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-616">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="cfc7a-617">响应版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-617">Respond version 1.4.2</span></span>

- <span data-ttu-id="cfc7a-618">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-618">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js</span></span>
- <span data-ttu-id="cfc7a-619">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-619">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js</span></span>
- <span data-ttu-id="cfc7a-620">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-620">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="cfc7a-621">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-621">http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-141"></a><span data-ttu-id="cfc7a-622">响应版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-622">Respond version 1.4.1</span></span>

- <span data-ttu-id="cfc7a-623">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-623">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js</span></span>
- <span data-ttu-id="cfc7a-624">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-624">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js</span></span>
- <span data-ttu-id="cfc7a-625">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-625">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="cfc7a-626">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-626">http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-140"></a><span data-ttu-id="cfc7a-627">响应版本 1.4.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-627">Respond version 1.4.0</span></span>

- <span data-ttu-id="cfc7a-628">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-628">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js</span></span>
- <span data-ttu-id="cfc7a-629">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-629">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js</span></span>
- <span data-ttu-id="cfc7a-630">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-630">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js</span></span>
- <span data-ttu-id="cfc7a-631">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-631">http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js</span></span>

#### <a name="respond-version-130"></a><span data-ttu-id="cfc7a-632">响应版本 1.3.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-632">Respond version 1.3.0</span></span>

- <span data-ttu-id="cfc7a-633">http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-633">http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js</span></span>

#### <a name="respond-version-120"></a><span data-ttu-id="cfc7a-634">响应版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-634">Respond version 1.2.0</span></span>

- <span data-ttu-id="cfc7a-635">http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-635">http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js</span></span>

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-636">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-636">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-637">以下版本的[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap 托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-637">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-337"></a><span data-ttu-id="cfc7a-638">Bootstrap 版本 3.3.7</span><span class="sxs-lookup"><span data-stu-id="cfc7a-638">Bootstrap version 3.3.7</span></span>

- <span data-ttu-id="cfc7a-639">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-639">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-640">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-640">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-641">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-641">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-642">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-642">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-643">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-643">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-644">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-644">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-645">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-645">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-646">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-646">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-647">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-647">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-648">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-648">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-649">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-649">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-650">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-650">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="cfc7a-651">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-651">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-336"></a><span data-ttu-id="cfc7a-652">Bootstrap 版本 3.3.6</span><span class="sxs-lookup"><span data-stu-id="cfc7a-652">Bootstrap version 3.3.6</span></span>

- <span data-ttu-id="cfc7a-653">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-653">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-654">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-654">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-655">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-655">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-656">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-656">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-657">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-657">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-658">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-658">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-659">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-659">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-660">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-660">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-661">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-661">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-662">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-662">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-663">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-663">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-664">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-664">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="cfc7a-665">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-665">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-335"></a><span data-ttu-id="cfc7a-666">Bootstrap 版本 3.3.5 更新</span><span class="sxs-lookup"><span data-stu-id="cfc7a-666">Bootstrap version 3.3.5</span></span>

- <span data-ttu-id="cfc7a-667">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-667">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-668">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-668">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-669">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-669">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-670">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-670">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-671">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-671">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-672">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-672">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-673">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-673">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-674">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-674">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-675">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-675">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-676">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-676">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-677">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-677">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-678">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-678">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="cfc7a-679">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-679">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-334"></a><span data-ttu-id="cfc7a-680">Bootstrap 版本 3.3.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-680">Bootstrap version 3.3.4</span></span>

- <span data-ttu-id="cfc7a-681">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-681">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-682">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-682">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-683">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-683">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-684">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-684">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-685">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-685">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-686">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-686">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-687">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-687">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-688">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-688">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-689">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-689">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-690">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-690">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-691">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-691">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-692">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-692">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="cfc7a-693">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-693">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-332"></a><span data-ttu-id="cfc7a-694">Bootstrap 版本 3.3.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-694">Bootstrap version 3.3.2</span></span>

- <span data-ttu-id="cfc7a-695">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-695">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-696">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-696">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-697">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-697">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-698">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-698">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-699">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-699">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-700">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-700">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-701">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-701">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-702">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-702">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-703">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-703">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-704">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-704">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-705">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-705">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-706">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-706">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff</span></span>
- <span data-ttu-id="cfc7a-707">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-707">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2</span></span>

#### <a name="bootstrap-version-331"></a><span data-ttu-id="cfc7a-708">Bootstrap 版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-708">Bootstrap version 3.3.1</span></span>

- <span data-ttu-id="cfc7a-709">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-709">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-710">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-710">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-711">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-711">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-712">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-712">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-713">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-713">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-714">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-714">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-715">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-715">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-716">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-716">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-717">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-717">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-718">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-718">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-719">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-719">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-720">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-720">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-330"></a><span data-ttu-id="cfc7a-721">Bootstrap 版本 3.3.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-721">Bootstrap version 3.3.0</span></span>

- <span data-ttu-id="cfc7a-722">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-722">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-723">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-723">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-724">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-724">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-725">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-725">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-726">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-726">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-727">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-727">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-728">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-728">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-729">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-729">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-730">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-730">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-731">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-731">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-732">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-732">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-733">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-733">http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-320"></a><span data-ttu-id="cfc7a-734">Bootstrap 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-734">Bootstrap version 3.2.0</span></span>

- <span data-ttu-id="cfc7a-735">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-735">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-736">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-736">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-737">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-737">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-738">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-738">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-739">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-739">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-740">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-740">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-741">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-741">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-742">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-742">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-743">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-743">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-744">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-744">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-745">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-745">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-746">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-746">http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-311"></a><span data-ttu-id="cfc7a-747">Bootstrap 版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-747">Bootstrap version 3.1.1</span></span>

- <span data-ttu-id="cfc7a-748">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-748">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-749">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-749">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-750">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-750">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-751">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-751">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-752">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-752">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-753">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-753">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-754">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-754">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-755">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-755">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-756">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-756">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-757">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-757">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-758">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-758">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-759">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-759">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-310"></a><span data-ttu-id="cfc7a-760">启动 3.1.0 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-760">Bootstrap version 3.1.0</span></span>

- <span data-ttu-id="cfc7a-761">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-761">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-762">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-762">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-763">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-763">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-764">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-764">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map</span></span>
- <span data-ttu-id="cfc7a-765">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-765">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-766">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-766">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-767">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-767">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map</span></span>
- <span data-ttu-id="cfc7a-768">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-768">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-769">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-769">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-770">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-770">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-771">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-771">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-772">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-772">http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-303"></a><span data-ttu-id="cfc7a-773">启动 3.0.3 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-773">Bootstrap version 3.0.3</span></span>

- <span data-ttu-id="cfc7a-774">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-774">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-775">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-775">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-776">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-776">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-777">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-777">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-778">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-778">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-779">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-779">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-780">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-780">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-781">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-781">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-782">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-782">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-783">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-783">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-302"></a><span data-ttu-id="cfc7a-784">Bootstrap 版本 3.0.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-784">Bootstrap version 3.0.2</span></span>

- <span data-ttu-id="cfc7a-785">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-785">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-786">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-786">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-787">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-787">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-788">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-788">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-789">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-789">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-790">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-790">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-791">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-791">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-792">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-792">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-793">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-793">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-794">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-794">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-301"></a><span data-ttu-id="cfc7a-795">Bootstrap 版本 3.0.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-795">Bootstrap version 3.0.1</span></span>

- <span data-ttu-id="cfc7a-796">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-796">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-797">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-797">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-798">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-798">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-799">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-799">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-800">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-800">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-801">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-801">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-802">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-802">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-803">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-803">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-804">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-804">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-805">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-805">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-300"></a><span data-ttu-id="cfc7a-806">启动 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="cfc7a-806">Bootstrap version 3.0.0</span></span>

- <span data-ttu-id="cfc7a-807">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-807">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-808">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-808">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-809">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-809">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-810">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-810">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-811">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-811">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css</span></span>
- <span data-ttu-id="cfc7a-812">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-812">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css</span></span>
- <span data-ttu-id="cfc7a-813">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot</span><span class="sxs-lookup"><span data-stu-id="cfc7a-813">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot</span></span>
- <span data-ttu-id="cfc7a-814">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg</span><span class="sxs-lookup"><span data-stu-id="cfc7a-814">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg</span></span>
- <span data-ttu-id="cfc7a-815">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf</span><span class="sxs-lookup"><span data-stu-id="cfc7a-815">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf</span></span>
- <span data-ttu-id="cfc7a-816">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff</span><span class="sxs-lookup"><span data-stu-id="cfc7a-816">http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff</span></span>

#### <a name="bootstrap-version-232"></a><span data-ttu-id="cfc7a-817">Bootstrap 版本 2.3.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-817">Bootstrap version 2.3.2</span></span>

- <span data-ttu-id="cfc7a-818">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-818">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-819">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-819">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-820">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-820">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-821">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-821">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-822">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-822">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css</span></span>
- <span data-ttu-id="cfc7a-823">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-823">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css</span></span>
- <span data-ttu-id="cfc7a-824">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png</span><span class="sxs-lookup"><span data-stu-id="cfc7a-824">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png</span></span>
- <span data-ttu-id="cfc7a-825">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png</span><span class="sxs-lookup"><span data-stu-id="cfc7a-825">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png</span></span>

#### <a name="bootstrap-version-231"></a><span data-ttu-id="cfc7a-826">Bootstrap 版本 2.3.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-826">Bootstrap version 2.3.1</span></span>

- <span data-ttu-id="cfc7a-827">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-827">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js</span></span>
- <span data-ttu-id="cfc7a-828">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-828">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js</span></span>
- <span data-ttu-id="cfc7a-829">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-829">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css</span></span>
- <span data-ttu-id="cfc7a-830">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-830">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css</span></span>
- <span data-ttu-id="cfc7a-831">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-831">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css</span></span>
- <span data-ttu-id="cfc7a-832">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-832">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css</span></span>
- <span data-ttu-id="cfc7a-833">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png</span><span class="sxs-lookup"><span data-stu-id="cfc7a-833">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png</span></span>
- <span data-ttu-id="cfc7a-834">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png</span><span class="sxs-lookup"><span data-stu-id="cfc7a-834">http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png</span></span>

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-835">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-835">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-836">以下版本的[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel 版本位于 CDN:</span><span class="sxs-lookup"><span data-stu-id="cfc7a-836">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="cfc7a-837">启动 TouchCarousel 版本 0.8.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-837">Bootstrap TouchCarousel version 0.8.0</span></span>

- <span data-ttu-id="cfc7a-838">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css</span><span class="sxs-lookup"><span data-stu-id="cfc7a-838">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css</span></span>
- <span data-ttu-id="cfc7a-839">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-839">http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js</span></span>

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-840">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-840">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-841">以下版本的[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/")在 CDN 上托管 Hammer.js 版本：</span><span class="sxs-lookup"><span data-stu-id="cfc7a-841">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="cfc7a-842">Hammer.js 版本 2.0.4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-842">Hammer.js version 2.0.4</span></span>

- <span data-ttu-id="cfc7a-843">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-843">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js</span></span>
- <span data-ttu-id="cfc7a-844">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-844">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js</span></span>
- <span data-ttu-id="cfc7a-845">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map</span><span class="sxs-lookup"><span data-stu-id="cfc7a-845">http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map</span></span>

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-846">ASP.NET Web 窗体和 CDN 上的 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="cfc7a-846">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-847">以下版本的 ASP.NET Ajax 库位于 CDN。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-847">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="cfc7a-848">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-848">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="cfc7a-849">ASP.NET Web 窗体和 Ajax 版本 4.5.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-849">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web 窗体和 Ajax 4.5.2")
- [<span data-ttu-id="cfc7a-850">ASP.NET Web 窗体和 Ajax 版本 4</span><span class="sxs-lookup"><span data-stu-id="cfc7a-850">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web 窗体和 Ajax 4")
- [<span data-ttu-id="cfc7a-851">ASP.NET Ajax 版本 3.5</span><span class="sxs-lookup"><span data-stu-id="cfc7a-851">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-852">ASP.NET MVC 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="cfc7a-852">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-853">以下 ASP.NET MVC JavaScript 文件位于此 CDN:</span><span class="sxs-lookup"><span data-stu-id="cfc7a-853">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="cfc7a-854">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-854">ASP.NET MVC 5.2.3</span></span>

- <span data-ttu-id="cfc7a-855">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-855">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="cfc7a-856">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-856">http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="cfc7a-857">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-857">ASP.NET MVC 5.1</span></span>

- <span data-ttu-id="cfc7a-858">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-858">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="cfc7a-859">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-859">http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="cfc7a-860">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-860">ASP.NET MVC 5.0</span></span>

- <span data-ttu-id="cfc7a-861">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-861">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="cfc7a-862">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-862">http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="cfc7a-863">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-863">ASP.NET MVC 4.0</span></span>

- <span data-ttu-id="cfc7a-864">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-864">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="cfc7a-865">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-865">http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js</span></span>

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="cfc7a-866">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-866">ASP.NET MVC 3.0</span></span>

- <span data-ttu-id="cfc7a-867">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-867">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js</span></span>
- <span data-ttu-id="cfc7a-868">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-868">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js</span></span>
- <span data-ttu-id="cfc7a-869">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-869">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js</span></span>
- <span data-ttu-id="cfc7a-870">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-870">http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js</span></span>
- <span data-ttu-id="cfc7a-871">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-871">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="cfc7a-872">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-872">http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js</span></span>

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="cfc7a-873">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-873">ASP.NET MVC 2.0</span></span>

- <span data-ttu-id="cfc7a-874">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-874">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="cfc7a-875">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-875">http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js</span></span>

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="cfc7a-876">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-876">ASP.NET MVC 1.0</span></span>

- <span data-ttu-id="cfc7a-877">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-877">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js</span></span>
- <span data-ttu-id="cfc7a-878">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-878">http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js</span></span>

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="cfc7a-879">ASP.NET SignalR 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="cfc7a-879">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="cfc7a-880">以下 ASP.NET SignalR JavaScript 文件位于此 CDN:</span><span class="sxs-lookup"><span data-stu-id="cfc7a-880">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="cfc7a-881">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-881">ASP.NET SignalR 2.2.2</span></span>

- <span data-ttu-id="cfc7a-882">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-882">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js</span></span>
- <span data-ttu-id="cfc7a-883">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-883">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js</span></span>

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="cfc7a-884">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-884">ASP.NET SignalR 2.2.1</span></span>

- <span data-ttu-id="cfc7a-885">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-885">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js</span></span>
- <span data-ttu-id="cfc7a-886">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-886">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js</span></span>

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="cfc7a-887">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-887">ASP.NET SignalR 2.2.0</span></span>

- <span data-ttu-id="cfc7a-888">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-888">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js</span></span>
- <span data-ttu-id="cfc7a-889">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-889">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js</span></span>

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="cfc7a-890">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-890">ASP.NET SignalR 2.1.0</span></span>

- <span data-ttu-id="cfc7a-891">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-891">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js</span></span>
- <span data-ttu-id="cfc7a-892">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-892">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js</span></span>

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="cfc7a-893">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-893">ASP.NET SignalR 2.0.3</span></span>

- <span data-ttu-id="cfc7a-894">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-894">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js</span></span>
- <span data-ttu-id="cfc7a-895">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-895">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js</span></span>

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="cfc7a-896">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-896">ASP.NET SignalR 2.0.2</span></span>

- <span data-ttu-id="cfc7a-897">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-897">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js</span></span>
- <span data-ttu-id="cfc7a-898">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-898">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js</span></span>

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="cfc7a-899">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-899">ASP.NET SignalR 2.0.1</span></span>

- <span data-ttu-id="cfc7a-900">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-900">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js</span></span>
- <span data-ttu-id="cfc7a-901">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-901">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js</span></span>

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="cfc7a-902">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-902">ASP.NET SignalR 2.0.0</span></span>

- <span data-ttu-id="cfc7a-903">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-903">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js</span></span>
- <span data-ttu-id="cfc7a-904">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-904">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js</span></span>

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="cfc7a-905">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="cfc7a-905">ASP.NET SignalR 1.1.3</span></span>

- <span data-ttu-id="cfc7a-906">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-906">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js</span></span>
- <span data-ttu-id="cfc7a-907">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-907">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js</span></span>

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="cfc7a-908">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="cfc7a-908">ASP.NET SignalR 1.1.2</span></span>

- <span data-ttu-id="cfc7a-909">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-909">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js</span></span>
- <span data-ttu-id="cfc7a-910">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-910">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js</span></span>

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="cfc7a-911">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-911">ASP.NET SignalR 1.1.1</span></span>

- <span data-ttu-id="cfc7a-912">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-912">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js</span></span>
- <span data-ttu-id="cfc7a-913">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-913">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js</span></span>

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="cfc7a-914">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="cfc7a-914">ASP.NET SignalR 1.1.0</span></span>

- <span data-ttu-id="cfc7a-915">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-915">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js</span></span>
- <span data-ttu-id="cfc7a-916">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-916">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js</span></span>

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="cfc7a-917">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="cfc7a-917">ASP.NET SignalR 1.0.1</span></span>

- <span data-ttu-id="cfc7a-918">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-918">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js</span></span>
- <span data-ttu-id="cfc7a-919">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js</span><span class="sxs-lookup"><span data-stu-id="cfc7a-919">http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js</span></span>

<span data-ttu-id="cfc7a-920">有关为 CDN 使用条款的信息，请参阅[Microsoft Ajax CDN 使用条款](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用条款")。</span><span class="sxs-lookup"><span data-stu-id="cfc7a-920">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
