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
ms.openlocfilehash: f1225f06e5218d893e3f49b2ccc67d56365b30e5
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="5313f-102">Microsoft Ajax 内容交付网络</span><span class="sxs-lookup"><span data-stu-id="5313f-102">Microsoft Ajax Content Delivery Network</span></span>
====================
<span data-ttu-id="5313f-103">注意： Microsoft Ajax CDN 具有超越使用 Azure CDN 没有 SLA。</span><span class="sxs-lookup"><span data-stu-id="5313f-103">Note: The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="5313f-104">目录</span><span class="sxs-lookup"><span data-stu-id="5313f-104">Table of Contents</span></span>

<span data-ttu-id="5313f-105">**[重命名为 ajax.aspnetcdn.com ajax.microsoft.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="5313f-105">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="5313f-106">**[Visual Studio.vsdoc 支持](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="5313f-106">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="5313f-107">**[使用 ASP.NET Ajax 从 CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="5313f-107">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="5313f-108">**[使用 jQuery 从 CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="5313f-108">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="5313f-109">**[使用 jQuery UI CDN。](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="5313f-109">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="5313f-110">**[第三方 CDN 上的文件](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="5313f-110">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="5313f-111">在 CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-111">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="5313f-112">jQuery CDN 上的迁移发行版</span><span class="sxs-lookup"><span data-stu-id="5313f-112">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="5313f-113">jQuery CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-113">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="5313f-114">jQuery CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="5313f-114">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="5313f-115">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="5313f-115">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="5313f-116">jQuery CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="5313f-116">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="5313f-117">jQuery CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="5313f-117">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="5313f-118">jQuery CDN 上的数据表版本</span><span class="sxs-lookup"><span data-stu-id="5313f-118">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="5313f-119">在 CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-119">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="5313f-120">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-120">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="5313f-121">在 CDN 上 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-121">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="5313f-122">全球化 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="5313f-122">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="5313f-123">响应 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="5313f-123">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="5313f-124">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-124">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="5313f-125">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-125">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="5313f-126">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-126">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="5313f-127">ASP.NET Web 窗体和 CDN 上的 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-127">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="5313f-128">ASP.NET MVC 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="5313f-128">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="5313f-129">ASP.NET SignalR 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="5313f-129">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="5313f-130">Microsoft Ajax 内容交付网络 (CDN) 承载 jQuery 等的常用第三方 JavaScript 库，并使您能够轻松地将它们添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5313f-130">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="5313f-131">例如，可以开始在此 CDN 上使用 jQuery 进行托管，只需通过添加&lt;脚本&gt;标记添加到你 ajax.aspnetcdn.com 所指向的页。</span><span class="sxs-lookup"><span data-stu-id="5313f-131">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="5313f-132">通过利用 CDN，就可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="5313f-132">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="5313f-133">CDN 的内容进行缓存在世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="5313f-133">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="5313f-134">此外，CDN 可让浏览器重复使用缓存的第三方 JavaScript 文件位于不同域中的网站。</span><span class="sxs-lookup"><span data-stu-id="5313f-134">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="5313f-135">如果你需要服务网页上使用安全套接字层，CDN 将支持 SSL (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="5313f-135">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="5313f-136">CDN 托管以下第三方脚本库也不能已上载，授权给你，由这些库的所有者：</span><span class="sxs-lookup"><span data-stu-id="5313f-136">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="5313f-137">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="5313f-137">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="5313f-138">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="5313f-138">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="5313f-139">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="5313f-139">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="5313f-140">jQuery 验证 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="5313f-140">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="5313f-141">jQuery 周期 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="5313f-141">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="5313f-142">jQuery 数据表 (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="5313f-142">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="5313f-143">Microsoft Ajax CDN 还包括以下库，后者已上载的 Microsoft:</span><span class="sxs-lookup"><span data-stu-id="5313f-143">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="5313f-144">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="5313f-144">ASP.NET Ajax</span></span>
- <span data-ttu-id="5313f-145">ASP.NET MVC JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="5313f-145">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="5313f-146">ASP.NET SignalR JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="5313f-146">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="5313f-147">Microsoft 不主张对此 CDN 上承载任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="5313f-147">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="5313f-148">库的版权所有者要授权给你这些库。</span><span class="sxs-lookup"><span data-stu-id="5313f-148">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="5313f-149">仅由各自的版权所有者授予的任何可能需要下载并使用这种库的权限。</span><span class="sxs-lookup"><span data-stu-id="5313f-149">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="5313f-150">因为这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供不保证或知识产权权限许可证 （包括任何隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="5313f-150">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="5313f-151">如果你想要提交你的 JavaScript 库，并且你的库是一顶部 JavaScript 库 (如上列出http://trends.builtwith.com)或扩展/插件这些库的 （a） 常用; 或 （b） 有助于在 ASP.NET 上使用，则请联系AjaxCDNSubmission@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="5313f-151">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="5313f-152">重命名为 ajax.aspnetcdn.com ajax.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="5313f-152">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="5313f-153">CDN 用于使用 microsoft.com 的域名，并且已更改为使用 aspnetcdn.com 域名。</span><span class="sxs-lookup"><span data-stu-id="5313f-153">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="5313f-154">此更改是为了提高性能，因为当浏览器引用 microsoft.com 域它将发送任何 cookie 从该域跨网络与每个请求。</span><span class="sxs-lookup"><span data-stu-id="5313f-154">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="5313f-155">通过重命名为 microsoft.com 之外的域名称性能可以通过增加同样可用于 25%。</span><span class="sxs-lookup"><span data-stu-id="5313f-155">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="5313f-156">请注意 ajax.microsoft.com 将继续工作，但建议 ajax.aspnetcdn.com。</span><span class="sxs-lookup"><span data-stu-id="5313f-156">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="5313f-157">旧格式： http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="5313f-157">Old Format: http://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="5313f-158">新格式： http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="5313f-158">New Format: http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="5313f-159">Visual Studio.vsdoc 支持</span><span class="sxs-lookup"><span data-stu-id="5313f-159">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="5313f-160">若要正确使用.vsdoc 文件，你需要确保你具有 VS 2008 SP1 的 Visual Studio 2008 安装和安装 vsdoc 文件的修补程序。</span><span class="sxs-lookup"><span data-stu-id="5313f-160">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="5313f-161">你可以从此处这些：</span><span class="sxs-lookup"><span data-stu-id="5313f-161">You can get these from here:</span></span>

- [<span data-ttu-id="5313f-162">下载 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="5313f-162">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下载 Visual Studio 2008 SP1")
- [<span data-ttu-id="5313f-163">下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="5313f-163">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1")

<span data-ttu-id="5313f-164">Visual Studio 2010 支持.vsdoc 文件而无需任何额外的修补程序。</span><span class="sxs-lookup"><span data-stu-id="5313f-164">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="5313f-165">使用 ASP.NET Ajax 从 CDN</span><span class="sxs-lookup"><span data-stu-id="5313f-165">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="5313f-166">在使用 ASP.NET 4 时，可以将对 ASP.NET framework 脚本的所有请求重都定向到 CDN。</span><span class="sxs-lookup"><span data-stu-id="5313f-166">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="5313f-167">从 CDN 而不是本地 web 服务器中检索脚本可以显著提高公共 ASP.NET 网站的性能。</span><span class="sxs-lookup"><span data-stu-id="5313f-167">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="5313f-168">ScriptManager EnableCDN 属性用于将 ASP.NET framework 脚本的所有请求重都定向到 Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="5313f-168">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="5313f-169">使用 jQuery 从 CDN</span><span class="sxs-lookup"><span data-stu-id="5313f-169">Using jQuery from the CDN</span></span>

<span data-ttu-id="5313f-170">你可以使用 CDN 上托管 Web 应用程序中，通过将下面的脚本元素添加到页面的 jQuery 脚本：</span><span class="sxs-lookup"><span data-stu-id="5313f-170">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="5313f-171">CDN 还包括对 jQuery 脚本，从而可以获取的缩减的版本使用以下元素：</span><span class="sxs-lookup"><span data-stu-id="5313f-171">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="5313f-172">若要允许你回退到从您自己的网站上的本地路径加载 jQuery，如果 CDN 碰巧将不可用的页，请立即引用 CDN 的元素之后添加以下元素：</span><span class="sxs-lookup"><span data-stu-id="5313f-172">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="5313f-173">下面的示例页使用 jQuery 库 （具有回退到的本地副本） 的 CDN 版本单击按钮时显示的 div 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="5313f-173">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="5313f-174">你可以了解有关 jQuery 和，请访问下载 jQuery 的本地副本[jQuery](http://jquery.com/) Web 站点。</span><span class="sxs-lookup"><span data-stu-id="5313f-174">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="5313f-175">使用 jQuery UI CDN。</span><span class="sxs-lookup"><span data-stu-id="5313f-175">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="5313f-176">CDN 还承载 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="5313f-176">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="5313f-177">JQuery UI 库包括一套丰富的小组件和可以在 ASP.NET 应用程序中使用的效果。</span><span class="sxs-lookup"><span data-stu-id="5313f-177">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="5313f-178">例如，以下页演示如何使用 jQuery UI Datepicker ASP.NET Web 窗体应用程序的上下文中显示一个弹出日历：</span><span class="sxs-lookup"><span data-stu-id="5313f-178">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="5313f-179">当你将焦点移到使用你键盘文本框中时，将显示日历：</span><span class="sxs-lookup"><span data-stu-id="5313f-179">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![使用包含 Datepicker 创建弹出日历](overview/_static/image1.png)

<span data-ttu-id="5313f-181">请注意，你必须在上面的代码包含从 CDN 的三个文件：</span><span class="sxs-lookup"><span data-stu-id="5313f-181">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="5313f-182">JQuery 库&mdash;jQuery UI 库依赖于 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="5313f-182">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="5313f-183">添加 jQuery UI 库之前，你必须 jQuery 库添加到你的页面。</span><span class="sxs-lookup"><span data-stu-id="5313f-183">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="5313f-184">JQuery UI 库&mdash;jQuery UI 库包含的所有 jQuery 用户界面效果和小组件，如在上述页面中使用包含 Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="5313f-184">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="5313f-185">JQuery UI 主题&mdash;jQuery UI 支持不同的主题。</span><span class="sxs-lookup"><span data-stu-id="5313f-185">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="5313f-186">上述页面中包含一个 CSS 文件导入 Redmond 主题的链接。</span><span class="sxs-lookup"><span data-stu-id="5313f-186">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="5313f-187">所有标准 jQuery UI 主题位于 CDN。</span><span class="sxs-lookup"><span data-stu-id="5313f-187">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="5313f-188">[访问此页面](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN 上")若要查看每个主题的缩略图。</span><span class="sxs-lookup"><span data-stu-id="5313f-188">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="5313f-189">若要了解有关 jQuery UI 库的详细信息，请访问官方[jQuery UI 网站](http://jQueryUI.com "jQuery UI 网站")。</span><span class="sxs-lookup"><span data-stu-id="5313f-189">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="5313f-190">第三方 CDN 上的文件</span><span class="sxs-lookup"><span data-stu-id="5313f-190">Third-Party Files on the CDN</span></span>

<span data-ttu-id="5313f-191">CDN 托管某些最常用的第三方 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="5313f-191">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="5313f-192">Microsoft 不主张对此 CDN 上承载任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="5313f-192">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="5313f-193">库的版权所有者要授权给你这些库。</span><span class="sxs-lookup"><span data-stu-id="5313f-193">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="5313f-194">仅由各自的版权所有者授予的任何可能需要下载并使用这种库的权限。</span><span class="sxs-lookup"><span data-stu-id="5313f-194">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="5313f-195">因为这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供不保证或知识产权权限许可证 （包括任何隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="5313f-195">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="5313f-196">在 CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-196">jQuery Releases on the CDN</span></span>

<span data-ttu-id="5313f-197">在 CDN 上托管的 jQuery 以下版本：</span><span class="sxs-lookup"><span data-stu-id="5313f-197">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="5313f-198">jQuery 版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="5313f-198">jQuery version 3.3.1</span></span>
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="5313f-199">jQuery 版本 3.2.1</span><span class="sxs-lookup"><span data-stu-id="5313f-199">jQuery version 3.2.1</span></span>
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="5313f-200">jQuery 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-200">jQuery version 3.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="5313f-201">jQuery 版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-201">jQuery version 3.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="5313f-202">jQuery 版本 3.1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-202">jQuery version 3.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="5313f-203">jQuery 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-203">jQuery version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="5313f-204">jQuery 版本 2.2.4</span><span class="sxs-lookup"><span data-stu-id="5313f-204">jQuery version 2.2.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="5313f-205">jQuery 版本 2.2.3</span><span class="sxs-lookup"><span data-stu-id="5313f-205">jQuery version 2.2.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="5313f-206">jQuery 版本 2.2.2</span><span class="sxs-lookup"><span data-stu-id="5313f-206">jQuery version 2.2.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="5313f-207">jQuery 2.2.1 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-207">jQuery version 2.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="5313f-208">jQuery 版本 2.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-208">jQuery version 2.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="5313f-209">jQuery 版本 2.1.4</span><span class="sxs-lookup"><span data-stu-id="5313f-209">jQuery version 2.1.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="5313f-210">jQuery 版本 2.1.3</span><span class="sxs-lookup"><span data-stu-id="5313f-210">jQuery version 2.1.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="5313f-211">jQuery 版本 2.1.2</span><span class="sxs-lookup"><span data-stu-id="5313f-211">jQuery version 2.1.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="5313f-212">jQuery 版本 2.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-212">jQuery version 2.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="5313f-213">jQuery 版本 2.1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-213">jQuery version 2.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="5313f-214">jQuery 版本 2.0.3</span><span class="sxs-lookup"><span data-stu-id="5313f-214">jQuery version 2.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="5313f-215">jQuery 版本 2.0.2</span><span class="sxs-lookup"><span data-stu-id="5313f-215">jQuery version 2.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="5313f-216">jQuery 版本 2.0.1</span><span class="sxs-lookup"><span data-stu-id="5313f-216">jQuery version 2.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="5313f-217">jQuery 版本 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5313f-217">jQuery version 2.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="5313f-218">jQuery 版本 1.12.4</span><span class="sxs-lookup"><span data-stu-id="5313f-218">jQuery version 1.12.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="5313f-219">jQuery 版本 1.12.3</span><span class="sxs-lookup"><span data-stu-id="5313f-219">jQuery version 1.12.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="5313f-220">jQuery 版本 1.12.2</span><span class="sxs-lookup"><span data-stu-id="5313f-220">jQuery version 1.12.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="5313f-221">jQuery 版本 1.12.1</span><span class="sxs-lookup"><span data-stu-id="5313f-221">jQuery version 1.12.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="5313f-222">jQuery 版本 1.12.0</span><span class="sxs-lookup"><span data-stu-id="5313f-222">jQuery version 1.12.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="5313f-223">jQuery 版本 1.11.3</span><span class="sxs-lookup"><span data-stu-id="5313f-223">jQuery version 1.11.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="5313f-224">jQuery 版本 1.11.2</span><span class="sxs-lookup"><span data-stu-id="5313f-224">jQuery version 1.11.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="5313f-225">jQuery 版本 1.11.1</span><span class="sxs-lookup"><span data-stu-id="5313f-225">jQuery version 1.11.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="5313f-226">jQuery 版本 1.11.0</span><span class="sxs-lookup"><span data-stu-id="5313f-226">jQuery version 1.11.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="5313f-227">jQuery 版本 1.10.2</span><span class="sxs-lookup"><span data-stu-id="5313f-227">jQuery version 1.10.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="5313f-228">jQuery 版本 1.10.1</span><span class="sxs-lookup"><span data-stu-id="5313f-228">jQuery version 1.10.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="5313f-229">jQuery 版本 1.10.0</span><span class="sxs-lookup"><span data-stu-id="5313f-229">jQuery version 1.10.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="5313f-230">jQuery 版本 1.9.1</span><span class="sxs-lookup"><span data-stu-id="5313f-230">jQuery version 1.9.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="5313f-231">jQuery 版本 1.9.0</span><span class="sxs-lookup"><span data-stu-id="5313f-231">jQuery version 1.9.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="5313f-232">jQuery 版本 1.8.3</span><span class="sxs-lookup"><span data-stu-id="5313f-232">jQuery version 1.8.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="5313f-233">jQuery 版本 1.8.2</span><span class="sxs-lookup"><span data-stu-id="5313f-233">jQuery version 1.8.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="5313f-234">jQuery 1.8.1 版</span><span class="sxs-lookup"><span data-stu-id="5313f-234">jQuery version 1.8.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="5313f-235">jQuery 版本 1.8.0</span><span class="sxs-lookup"><span data-stu-id="5313f-235">jQuery version 1.8.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="5313f-236">jQuery 版本 1.7.2</span><span class="sxs-lookup"><span data-stu-id="5313f-236">jQuery version 1.7.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="5313f-237">jQuery 版本 1.7.1</span><span class="sxs-lookup"><span data-stu-id="5313f-237">jQuery version 1.7.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="5313f-238">jQuery 版本 1.7</span><span class="sxs-lookup"><span data-stu-id="5313f-238">jQuery version 1.7</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="5313f-239">jQuery 版本 1.6.4</span><span class="sxs-lookup"><span data-stu-id="5313f-239">jQuery version 1.6.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="5313f-240">jQuery 版本 1.6.3</span><span class="sxs-lookup"><span data-stu-id="5313f-240">jQuery version 1.6.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="5313f-241">jQuery 版本 1.6.2</span><span class="sxs-lookup"><span data-stu-id="5313f-241">jQuery version 1.6.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="5313f-242">jQuery 版本 1.6.1</span><span class="sxs-lookup"><span data-stu-id="5313f-242">jQuery version 1.6.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="5313f-243">jQuery 版本 1.6</span><span class="sxs-lookup"><span data-stu-id="5313f-243">jQuery version 1.6</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="5313f-244">jQuery 版本 1.5.2</span><span class="sxs-lookup"><span data-stu-id="5313f-244">jQuery version 1.5.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="5313f-245">jQuery 版本 1.5.1</span><span class="sxs-lookup"><span data-stu-id="5313f-245">jQuery version 1.5.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="5313f-246">jQuery 版本 1.5</span><span class="sxs-lookup"><span data-stu-id="5313f-246">jQuery version 1.5</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="5313f-247">jQuery 版本 1.4.4</span><span class="sxs-lookup"><span data-stu-id="5313f-247">jQuery version 1.4.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="5313f-248">jQuery 版本 1.4.3</span><span class="sxs-lookup"><span data-stu-id="5313f-248">jQuery version 1.4.3</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="5313f-249">jQuery 版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="5313f-249">jQuery version 1.4.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="5313f-250">jQuery 版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="5313f-250">jQuery version 1.4.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="5313f-251">jQuery 1.4 版</span><span class="sxs-lookup"><span data-stu-id="5313f-251">jQuery version 1.4</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="5313f-252">jQuery 版本 1.3.2</span><span class="sxs-lookup"><span data-stu-id="5313f-252">jQuery version 1.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="5313f-253">jQuery CDN 上的迁移发行版</span><span class="sxs-lookup"><span data-stu-id="5313f-253">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="5313f-254">在 CDN 上托管的 jQuery 迁移以下版本：</span><span class="sxs-lookup"><span data-stu-id="5313f-254">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="5313f-255">jQuery 迁移 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-255">jQuery Migrate version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="5313f-256">jQuery 迁移 1.2.1 版</span><span class="sxs-lookup"><span data-stu-id="5313f-256">jQuery Migrate version 1.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="5313f-257">jQuery 迁移版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-257">jQuery Migrate version 1.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="5313f-258">jQuery 迁移版本 1.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-258">jQuery Migrate version 1.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="5313f-259">jQuery 迁移 1.1.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-259">jQuery Migrate version 1.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="5313f-260">jQuery 迁移版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="5313f-260">jQuery Migrate version 1.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- http://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="5313f-261">jQuery CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-261">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="5313f-262">在此 CDN 上托管以下版本的 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="5313f-262">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="5313f-263">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-263">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-264">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="5313f-264">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-265">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="5313f-265">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-266">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="5313f-266">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-267">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="5313f-267">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-268">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="5313f-268">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-269">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="5313f-269">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-270">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="5313f-270">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-271">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="5313f-271">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-272">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="5313f-272">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-273">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="5313f-273">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery 1.10.2 Microsoft Ajax CDN 上的用户界面")
- [<span data-ttu-id="5313f-274">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="5313f-274">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-275">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="5313f-275">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-276">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="5313f-276">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-277">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="5313f-277">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-278">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="5313f-278">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-279">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="5313f-279">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-280">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="5313f-280">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-281">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="5313f-281">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-282">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="5313f-282">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-283">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="5313f-283">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-284">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="5313f-284">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-285">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="5313f-285">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-286">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="5313f-286">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-287">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="5313f-287">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-288">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="5313f-288">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-289">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="5313f-289">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-290">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="5313f-290">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-291">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="5313f-291">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-292">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="5313f-292">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-293">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="5313f-293">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-294">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="5313f-294">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-295">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="5313f-295">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-296">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="5313f-296">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-297">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="5313f-297">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-298">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="5313f-298">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="5313f-299">jQuery CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="5313f-299">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="5313f-300">在此 CDN 上托管以下版本的 jQuery 验证库。</span><span class="sxs-lookup"><span data-stu-id="5313f-300">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="5313f-301">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-301">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-302">jQuery 验证 1.17.0</span><span class="sxs-lookup"><span data-stu-id="5313f-302">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 验证 1.17.0")
- [<span data-ttu-id="5313f-303">jQuery 验证 1.16.0</span><span class="sxs-lookup"><span data-stu-id="5313f-303">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 验证 1.16.0")
- [<span data-ttu-id="5313f-304">jQuery 验证 1.15.1</span><span class="sxs-lookup"><span data-stu-id="5313f-304">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 验证 1.15.1")
- [<span data-ttu-id="5313f-305">jQuery 验证 1.15.0</span><span class="sxs-lookup"><span data-stu-id="5313f-305">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 验证 1.15.0")
- [<span data-ttu-id="5313f-306">jQuery 验证 1.14.0</span><span class="sxs-lookup"><span data-stu-id="5313f-306">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 验证 1.14.0")
- [<span data-ttu-id="5313f-307">jQuery 验证 1.13.1</span><span class="sxs-lookup"><span data-stu-id="5313f-307">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 验证 1.13.1")
- [<span data-ttu-id="5313f-308">jQuery 验证 1.13.0</span><span class="sxs-lookup"><span data-stu-id="5313f-308">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 验证 1.13.0")
- [<span data-ttu-id="5313f-309">jQuery 验证 1.12.0</span><span class="sxs-lookup"><span data-stu-id="5313f-309">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 验证 1.12.0")
- [<span data-ttu-id="5313f-310">jQuery 验证 1.11.1</span><span class="sxs-lookup"><span data-stu-id="5313f-310">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 验证 1.11.1")
- [<span data-ttu-id="5313f-311">jQuery 验证 1.11.0</span><span class="sxs-lookup"><span data-stu-id="5313f-311">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 验证 1.11.0")
- [<span data-ttu-id="5313f-312">jQuery 验证 1.10.0</span><span class="sxs-lookup"><span data-stu-id="5313f-312">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 验证 1.10.0")
- [<span data-ttu-id="5313f-313">jQuery 验证 1.9</span><span class="sxs-lookup"><span data-stu-id="5313f-313">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 版本 1.9")
- [<span data-ttu-id="5313f-314">jQuery 验证 1.8.1</span><span class="sxs-lookup"><span data-stu-id="5313f-314">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 1.8.1 版")
- [<span data-ttu-id="5313f-315">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="5313f-315">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 版本 1.8")
- [<span data-ttu-id="5313f-316">jQuery 验证 1.7</span><span class="sxs-lookup"><span data-stu-id="5313f-316">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 版本 1.7")
- [<span data-ttu-id="5313f-317">jQuery 验证 1.6</span><span class="sxs-lookup"><span data-stu-id="5313f-317">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 验证 1.6")
- [<span data-ttu-id="5313f-318">jQuery 验证 1.5.5</span><span class="sxs-lookup"><span data-stu-id="5313f-318">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 验证 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="5313f-319">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="5313f-319">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="5313f-320">在此 CDN 上托管以下版本的 jQuery Mobile 库。</span><span class="sxs-lookup"><span data-stu-id="5313f-320">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="5313f-321">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-321">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-322">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="5313f-322">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-323">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="5313f-323">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-324">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="5313f-324">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-325">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="5313f-325">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-326">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="5313f-326">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-327">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="5313f-327">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-328">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="5313f-328">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-329">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-329">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-330">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="5313f-330">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-331">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-331">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-332">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-332">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-333">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="5313f-333">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-334">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="5313f-334">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-335">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-335">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 Microsoft Ajax CDN 上")
- [<span data-ttu-id="5313f-336">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="5313f-336">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="5313f-337">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="5313f-337">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="5313f-338">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="5313f-338">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 上的 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="5313f-339">jQuery CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="5313f-339">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="5313f-340">在此 CDN 上托管以下版本的 jQuery 模板插件。</span><span class="sxs-lookup"><span data-stu-id="5313f-340">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="5313f-341">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-341">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-342">jQuery 模板 Beta 1</span><span class="sxs-lookup"><span data-stu-id="5313f-342">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 模板 Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="5313f-343">jQuery CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="5313f-343">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="5313f-344">在此 CDN 上托管以下版本的 jQuery 周期插件。</span><span class="sxs-lookup"><span data-stu-id="5313f-344">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="5313f-345">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-345">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-346">jQuery 周期 2.99</span><span class="sxs-lookup"><span data-stu-id="5313f-346">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 周期 2.99")
- [<span data-ttu-id="5313f-347">jQuery 周期 2.94</span><span class="sxs-lookup"><span data-stu-id="5313f-347">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery 周期 2.94")
- [<span data-ttu-id="5313f-348">jQuery 周期 2.88</span><span class="sxs-lookup"><span data-stu-id="5313f-348">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 周期 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="5313f-349">jQuery CDN 上的数据表版本</span><span class="sxs-lookup"><span data-stu-id="5313f-349">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="5313f-350">在此 CDN 上托管以下版本的 jQuery 数据表插件。</span><span class="sxs-lookup"><span data-stu-id="5313f-350">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="5313f-351">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-351">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-352">jQuery 数据表 1.10.5</span><span class="sxs-lookup"><span data-stu-id="5313f-352">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery 数据表 1.10.5")
- [<span data-ttu-id="5313f-353">jQuery 数据表 1.10.4</span><span class="sxs-lookup"><span data-stu-id="5313f-353">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery 数据表 1.10.4")
- [<span data-ttu-id="5313f-354">jQuery 数据表 1.9.4</span><span class="sxs-lookup"><span data-stu-id="5313f-354">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery 数据表 1.9.4")
- [<span data-ttu-id="5313f-355">jQuery 数据表 1.9.3 放置</span><span class="sxs-lookup"><span data-stu-id="5313f-355">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery 数据表 1.9.3 放置")
- [<span data-ttu-id="5313f-356">jQuery 数据表 1.9.2</span><span class="sxs-lookup"><span data-stu-id="5313f-356">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery 数据表 1.9.2")
- [<span data-ttu-id="5313f-357">jQuery 数据表 1.9.1</span><span class="sxs-lookup"><span data-stu-id="5313f-357">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery 数据表 1.9.1")
- [<span data-ttu-id="5313f-358">jQuery 数据表 1.9.0</span><span class="sxs-lookup"><span data-stu-id="5313f-358">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery 数据表 1.9.0")
- [<span data-ttu-id="5313f-359">jQuery 数据表 1.8.2</span><span class="sxs-lookup"><span data-stu-id="5313f-359">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery 数据表 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="5313f-360">在 CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-360">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="5313f-361">以下版本的[Modernizr](http://www.modernizr.com "Modernizr")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="5313f-361">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- http://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="5313f-362">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-362">JSHint Releases on the CDN</span></span>

<span data-ttu-id="5313f-363">以下版本的[JSHint](http://www.jshint.com "JSHint")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="5313f-363">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="5313f-364">在 CDN 上 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-364">Knockout Releases on the CDN</span></span>

<span data-ttu-id="5313f-365">以下版本的[Knockout](http://www.knockoutjs.com "Knockout")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="5313f-365">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- http://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="5313f-366">全球化 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="5313f-366">Globalize Releases on the CDN</span></span>

<span data-ttu-id="5313f-367">以下版本的[Globalize](https://github.com/jquery/globalize "Globalize")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="5313f-367">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="5313f-368">全球化版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="5313f-368">Globalize version 1.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- http://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="5313f-369">全球化版本 0.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-369">Globalize version 0.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="5313f-370">所有区域性</span><span class="sxs-lookup"><span data-stu-id="5313f-370">all cultures</span></span>
- http://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="5313f-371">"{区域性的代码}"替换为所需的区域性代码、 globalize.culture.en GB.js== Microsoft 在 CDN 上的文件例如 = = 这些库上载 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="5313f-371">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="5313f-372">响应 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="5313f-372">Respond Releases on the CDN</span></span>

<span data-ttu-id="5313f-373">以下版本的[ https://github.com/scottjehl/Respond ] (https://github.com/scottjehl/Respond " https://github.com/scottjehl/Respond ")在 CDN 上托管响应：</span><span class="sxs-lookup"><span data-stu-id="5313f-373">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="5313f-374">响应版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="5313f-374">Respond version 1.4.2</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="5313f-375">响应版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="5313f-375">Respond version 1.4.1</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="5313f-376">响应版本 1.4.0</span><span class="sxs-lookup"><span data-stu-id="5313f-376">Respond version 1.4.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- http://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="5313f-377">响应版本 1.3.0</span><span class="sxs-lookup"><span data-stu-id="5313f-377">Respond version 1.3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="5313f-378">响应版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-378">Respond version 1.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="5313f-379">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-379">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="5313f-380">以下版本的[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap 托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="5313f-380">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-400"></a><span data-ttu-id="5313f-381">启动 4.0.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-381">Bootstrap version 4.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="5313f-382">Bootstrap 版本 3.3.7</span><span class="sxs-lookup"><span data-stu-id="5313f-382">Bootstrap version 3.3.7</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="5313f-383">Bootstrap 版本 3.3.6</span><span class="sxs-lookup"><span data-stu-id="5313f-383">Bootstrap version 3.3.6</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="5313f-384">Bootstrap 版本 3.3.5 更新</span><span class="sxs-lookup"><span data-stu-id="5313f-384">Bootstrap version 3.3.5</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="5313f-385">Bootstrap 版本 3.3.4</span><span class="sxs-lookup"><span data-stu-id="5313f-385">Bootstrap version 3.3.4</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="5313f-386">Bootstrap 版本 3.3.2</span><span class="sxs-lookup"><span data-stu-id="5313f-386">Bootstrap version 3.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="5313f-387">Bootstrap 版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="5313f-387">Bootstrap version 3.3.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="5313f-388">Bootstrap 版本 3.3.0</span><span class="sxs-lookup"><span data-stu-id="5313f-388">Bootstrap version 3.3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="5313f-389">Bootstrap 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-389">Bootstrap version 3.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="5313f-390">Bootstrap 版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-390">Bootstrap version 3.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="5313f-391">启动 3.1.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-391">Bootstrap version 3.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="5313f-392">启动 3.0.3 版</span><span class="sxs-lookup"><span data-stu-id="5313f-392">Bootstrap version 3.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="5313f-393">Bootstrap 版本 3.0.2</span><span class="sxs-lookup"><span data-stu-id="5313f-393">Bootstrap version 3.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="5313f-394">Bootstrap 版本 3.0.1</span><span class="sxs-lookup"><span data-stu-id="5313f-394">Bootstrap version 3.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="5313f-395">启动 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="5313f-395">Bootstrap version 3.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- http://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="5313f-396">Bootstrap 版本 2.3.2</span><span class="sxs-lookup"><span data-stu-id="5313f-396">Bootstrap version 2.3.2</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="5313f-397">Bootstrap 版本 2.3.1</span><span class="sxs-lookup"><span data-stu-id="5313f-397">Bootstrap version 2.3.1</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- http://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="5313f-398">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-398">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="5313f-399">以下版本的[ https://github.com/ixisio/bootstrap-touch-carousel ] (https://github.com/ixisio/bootstrap-touch-carousel " https://github.com/ixisio/bootstrap-touch-carousel ")在 CDN 上托管 Bootstrap TouchCarousel 版本：</span><span class="sxs-lookup"><span data-stu-id="5313f-399">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="5313f-400">Bootstrap TouchCarousel version 0.8.0</span><span class="sxs-lookup"><span data-stu-id="5313f-400">Bootstrap TouchCarousel version 0.8.0</span></span>

- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- http://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="5313f-401">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-401">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="5313f-402">以下版本的[ http://hammerjs.github.io/ ] (http://hammerjs.github.io/ " http://hammerjs.github.io/ ")在 CDN 上托管 Hammer.js 版本：</span><span class="sxs-lookup"><span data-stu-id="5313f-402">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="5313f-403">Hammer.js 版本 2.0.4</span><span class="sxs-lookup"><span data-stu-id="5313f-403">Hammer.js version 2.0.4</span></span>

- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- http://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="5313f-404">ASP.NET Web 窗体和 CDN 上的 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="5313f-404">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="5313f-405">以下版本的 ASP.NET Ajax 库位于 CDN。</span><span class="sxs-lookup"><span data-stu-id="5313f-405">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="5313f-406">单击每个链接以查看实际的文件列表。</span><span class="sxs-lookup"><span data-stu-id="5313f-406">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="5313f-407">ASP.NET Web 窗体和 Ajax 版本 4.5.2</span><span class="sxs-lookup"><span data-stu-id="5313f-407">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web 窗体和 Ajax 4.5.2")
- [<span data-ttu-id="5313f-408">ASP.NET Web 窗体和 Ajax 版本 4</span><span class="sxs-lookup"><span data-stu-id="5313f-408">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web 窗体和 Ajax 4")
- [<span data-ttu-id="5313f-409">ASP.NET Ajax 版本 3.5</span><span class="sxs-lookup"><span data-stu-id="5313f-409">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="5313f-410">ASP.NET MVC 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="5313f-410">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="5313f-411">以下 ASP.NET MVC JavaScript 文件位于此 CDN:</span><span class="sxs-lookup"><span data-stu-id="5313f-411">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="5313f-412">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="5313f-412">ASP.NET MVC 5.2.3</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="5313f-413">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="5313f-413">ASP.NET MVC 5.1</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="5313f-414">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="5313f-414">ASP.NET MVC 5.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="5313f-415">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="5313f-415">ASP.NET MVC 4.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="5313f-416">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="5313f-416">ASP.NET MVC 3.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="5313f-417">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-417">ASP.NET MVC 2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="5313f-418">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-418">ASP.NET MVC 1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- http://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="5313f-419">ASP.NET SignalR 释放 CDN 上</span><span class="sxs-lookup"><span data-stu-id="5313f-419">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="5313f-420">以下 ASP.NET SignalR JavaScript 文件位于此 CDN:</span><span class="sxs-lookup"><span data-stu-id="5313f-420">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="5313f-421">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="5313f-421">ASP.NET SignalR 2.2.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="5313f-422">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="5313f-422">ASP.NET SignalR 2.2.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="5313f-423">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="5313f-423">ASP.NET SignalR 2.2.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="5313f-424">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-424">ASP.NET SignalR 2.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="5313f-425">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="5313f-425">ASP.NET SignalR 2.0.3</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="5313f-426">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="5313f-426">ASP.NET SignalR 2.0.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="5313f-427">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="5313f-427">ASP.NET SignalR 2.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="5313f-428">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5313f-428">ASP.NET SignalR 2.0.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="5313f-429">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="5313f-429">ASP.NET SignalR 1.1.3</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="5313f-430">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="5313f-430">ASP.NET SignalR 1.1.2</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="5313f-431">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="5313f-431">ASP.NET SignalR 1.1.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="5313f-432">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="5313f-432">ASP.NET SignalR 1.1.0</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="5313f-433">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="5313f-433">ASP.NET SignalR 1.0.1</span></span>

- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- http://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="5313f-434">有关为 CDN 使用条款的信息，请参阅[Microsoft Ajax CDN 使用条款](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用条款")。</span><span class="sxs-lookup"><span data-stu-id="5313f-434">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
