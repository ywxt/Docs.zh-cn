---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大更改 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了针对.NET Framework 版本可能会影响使用创建的应用程序的月 4 日版本的更改...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: e6d7972c333e302bb8b6b2d23ea7123b8757b2f4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842505"
---
<a name="aspnet-4-breaking-changes"></a><span data-ttu-id="3a64f-103">ASP.NET 4 重大更改</span><span class="sxs-lookup"><span data-stu-id="3a64f-103">ASP.NET 4 Breaking Changes</span></span>
====================
> <span data-ttu-id="3a64f-104">本文档介绍了针对.NET Framework 版本可能会影响使用早期版本中，其中包括 ASP.NET 4 Beta 1 和 Beta 2 版本创建的应用程序的月 4 日版本的更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-104">This document describes changes that have been made for the .NET Framework version 4 release that can potentially affect applications that were created using earlier releases, including the ASP.NET 4 Beta 1 and Beta 2 releases.</span></span>
> 
> [<span data-ttu-id="3a64f-105">下载此白皮书</span><span class="sxs-lookup"><span data-stu-id="3a64f-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)


<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a><span data-ttu-id="3a64f-106">内容</span><span class="sxs-lookup"><span data-stu-id="3a64f-106">Contents</span></span>

[<span data-ttu-id="3a64f-107">Web.config 文件中的 ControlRenderingCompatibilityVersion 设置</span><span class="sxs-lookup"><span data-stu-id="3a64f-107">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>](#0.1__Toc256770141 "_Toc256770141")  
[<span data-ttu-id="3a64f-108">ClientIDMode 更改</span><span class="sxs-lookup"><span data-stu-id="3a64f-108">ClientIDMode Changes</span></span>](#0.1__Toc256770142 "_Toc256770142")  
[<span data-ttu-id="3a64f-109">HtmlEncode 和 UrlEncode 现在编码单引号</span><span class="sxs-lookup"><span data-stu-id="3a64f-109">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>](#0.1__Toc256770143 "_Toc256770143")  
[<span data-ttu-id="3a64f-110">ASP.NET 页面 (.aspx) 分析器是 Stricter</span><span class="sxs-lookup"><span data-stu-id="3a64f-110">ASP.NET Page (.aspx) Parser is Stricter</span></span>](#0.1__Toc256770144 "_Toc256770144")  
[<span data-ttu-id="3a64f-111">更新的浏览器定义文件</span><span class="sxs-lookup"><span data-stu-id="3a64f-111">Browser Definition Files Updated</span></span>](#0.1__Toc256770145 "_Toc256770145")  
[<span data-ttu-id="3a64f-112">从根 Web 配置文件中删除 System.Web.Mobile.dll</span><span class="sxs-lookup"><span data-stu-id="3a64f-112">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>](#0.1__Toc256770146 "_Toc256770146")  
[<span data-ttu-id="3a64f-113">ASP.NET 请求验证</span><span class="sxs-lookup"><span data-stu-id="3a64f-113">ASP.NET Request Validation</span></span>](#0.1__Toc256770147 "_Toc256770147")  
[<span data-ttu-id="3a64f-114">哈希算法的默认值现在为 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="3a64f-114">Default Hashing Algorithm Is Now HMACSHA256</span></span>](#0.1__Toc256770148 "_Toc256770148")  
[<span data-ttu-id="3a64f-115">与新的 ASP.NET 4 根配置相关的配置错误</span><span class="sxs-lookup"><span data-stu-id="3a64f-115">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>](#0.1__Toc256770149 "_Toc256770149")  
[<span data-ttu-id="3a64f-116">ASP.NET 4 子应用程序启动失败的时在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序</span><span class="sxs-lookup"><span data-stu-id="3a64f-116">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>](#0.1__Toc256770150 "_Toc256770150")  
[<span data-ttu-id="3a64f-117">ASP.NET 4 网站不能在安装 SharePoint 计算机上启动</span><span class="sxs-lookup"><span data-stu-id="3a64f-117">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>](#0.1__Toc256770151 "_Toc256770151")  
[<span data-ttu-id="3a64f-118">HttpRequest.FilePath 属性不再包括 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="3a64f-118">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>](#0.1__Toc256770152 "_Toc256770152")  
[<span data-ttu-id="3a64f-119">ASP.NET 2.0 应用程序可能会生成引用 eurl.axd 的 HttpException 错误</span><span class="sxs-lookup"><span data-stu-id="3a64f-119">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>](#0.1__Toc256770153 "_Toc256770153")  
[<span data-ttu-id="3a64f-120">事件处理程序可能不会不引发在 IIS 7 或 IIS 7.5 中的默认文档集成模式下</span><span class="sxs-lookup"><span data-stu-id="3a64f-120">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>](#0.1__Toc256770154 "_Toc256770154")  
[<span data-ttu-id="3a64f-121">将更改为 ASP.NET 代码访问安全性 (CAS) 实现</span><span class="sxs-lookup"><span data-stu-id="3a64f-121">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>](#0.1__Toc256770155 "_Toc256770155")  
[<span data-ttu-id="3a64f-122">在移动 MembershipUser 中和其他类型 System.Web.Security Namespace</span><span class="sxs-lookup"><span data-stu-id="3a64f-122">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>](#0.1__Toc256770156 "_Toc256770156")  
[<span data-ttu-id="3a64f-123">输出缓存发生更改以改变\*HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="3a64f-123">Output Caching Changes to Vary \* HTTP Header</span></span>](#0.1__Toc256770157 "_Toc256770157")  
[<span data-ttu-id="3a64f-124">Passport System.Web.Security 类型可以是已过时</span><span class="sxs-lookup"><span data-stu-id="3a64f-124">System.Web.Security Types for Passport are Obsolete</span></span>](#0.1__Toc256770158 "_Toc256770158")  
[<span data-ttu-id="3a64f-125">MenuItem.PopOutImageUrl 属性将无法呈现 ASP.NET 4 中的映像</span><span class="sxs-lookup"><span data-stu-id="3a64f-125">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>](#0.1__Toc256770159 "_Toc256770159")  
[<span data-ttu-id="3a64f-126">Menu.StaticPopOutImageUrl 但 Menu.DynamicPopOutImageUrl 无法呈现图像时路径包含反斜杠</span><span class="sxs-lookup"><span data-stu-id="3a64f-126">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>](#0.1__Toc256770160 "_Toc256770160")  
[<span data-ttu-id="3a64f-127">Disclaimer</span><span class="sxs-lookup"><span data-stu-id="3a64f-127">Disclaimer</span></span>](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a><span data-ttu-id="3a64f-128">Web.config 文件中的 ControlRenderingCompatibilityVersion 设置</span><span class="sxs-lookup"><span data-stu-id="3a64f-128">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>

<span data-ttu-id="3a64f-129">ASP.NET 控件中修改了.NET Framework 版本 4 以便让您可以指定更准确地说及其呈现标记。</span><span class="sxs-lookup"><span data-stu-id="3a64f-129">ASP.NET controls have been modified in the .NET Framework version 4 in order to let you specify more precisely how they render markup.</span></span> <span data-ttu-id="3a64f-130">在以前版本的.NET Framework 中，某些控件发出了无法禁用的标记。</span><span class="sxs-lookup"><span data-stu-id="3a64f-130">In previous versions of the .NET Framework, some controls emitted markup that you had no way to disable.</span></span> <span data-ttu-id="3a64f-131">默认情况下，不能再生成 ASP.NET 4 此类型的标记。</span><span class="sxs-lookup"><span data-stu-id="3a64f-131">By default, ASP.NET 4 this type of markup is no longer generated.</span></span>

<span data-ttu-id="3a64f-132">如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，该工具会自动添加到的设置`Web.config`保留旧式呈现的文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-132">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves legacy rendering.</span></span> <span data-ttu-id="3a64f-133">但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的呈现模式。</span><span class="sxs-lookup"><span data-stu-id="3a64f-133">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new rendering mode by default.</span></span> <span data-ttu-id="3a64f-134">若要禁用新的呈现模式，添加以下设置中的`Web.config`文件：</span><span class="sxs-lookup"><span data-stu-id="3a64f-134">To disable the new rendering mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

<span data-ttu-id="3a64f-135">主要呈现更改的新行为将如下所示：</span><span class="sxs-lookup"><span data-stu-id="3a64f-135">The major rendering changes that the new behavior brings are as follows:</span></span>

- <span data-ttu-id="3a64f-136">**图像**并**ImageButton**控件不再呈现`border="0"`属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-136">The **Image** and **ImageButton** controls no longer render a `border="0"` attribute.</span></span>
- <span data-ttu-id="3a64f-137">**BaseValidator**从其派生的类和验证控件不再呈现红色文本默认情况下。</span><span class="sxs-lookup"><span data-stu-id="3a64f-137">The **BaseValidator** class and validation controls that derive from it no longer render red text by default.</span></span>
- <span data-ttu-id="3a64f-138">**HtmlForm**控件不呈现**名称**属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-138">The **HtmlForm** control does not render a **name** attribute.</span></span>
- <span data-ttu-id="3a64f-139">**表**控件不再呈现`border="0"`属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-139">The **Table** control no longer renders a `border="0"` attribute.</span></span>
- <span data-ttu-id="3a64f-140">不设计用于用户输入的控件 (例如，**标签**控件) 不再呈现`disabled="disabled"`特性及其**已启用**属性设置为**false**（或如果它们从容器控件继承此设置）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-140">Controls that are not designed for user input (for example, the **Label** control) no longer render the `disabled="disabled"` attribute if their **Enabled** property is set to **false** (or if they inherit this setting from a container control).</span></span>

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a><span data-ttu-id="3a64f-141">ClientIDMode 的更改</span><span class="sxs-lookup"><span data-stu-id="3a64f-141">ClientIDMode Changes</span></span>

<span data-ttu-id="3a64f-142">**ClientIDMode** ASP.NET 4 中的设置允许您指定 ASP.NET 如何生成**id** HTML 元素的属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-142">The **ClientIDMode** setting in ASP.NET 4 lets you specify how ASP.NET generates the **id** attribute for HTML elements.</span></span> <span data-ttu-id="3a64f-143">在以前版本的 ASP.NET，默认行为是等效于**AutoID**设置为**ClientIDMode**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-143">In previous versions of ASP.NET, the default behavior was equivalent to the **AutoID** setting of **ClientIDMode**.</span></span> <span data-ttu-id="3a64f-144">但是，默认设置是现在**可预测**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-144">However, the default setting is now **Predictable**.</span></span>

<span data-ttu-id="3a64f-145">如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，该工具会自动添加到的设置`Web.config`保留早期版本的.NET Framework 的行为的文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-145">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves the behavior of earlier versions of the .NET Framework.</span></span> <span data-ttu-id="3a64f-146">但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的模式。</span><span class="sxs-lookup"><span data-stu-id="3a64f-146">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new mode by default.</span></span> <span data-ttu-id="3a64f-147">若要禁用新的客户端 ID 模式，添加以下设置中的`Web.config`文件：</span><span class="sxs-lookup"><span data-stu-id="3a64f-147">To disable the new client ID mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a><span data-ttu-id="3a64f-148">HtmlEncode 和 UrlEncode 现在对单引号进行编码</span><span class="sxs-lookup"><span data-stu-id="3a64f-148">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>

<span data-ttu-id="3a64f-149">在 ASP.NET 4 中， **HtmlEncode**并**UrlEncode**方法**HttpUtility**并**HttpServerUtility**类已更新到按如下所示进行编码的单引号字符 （'）：</span><span class="sxs-lookup"><span data-stu-id="3a64f-149">In ASP.NET 4, the **HtmlEncode** and **UrlEncode** methods of the **HttpUtility** and **HttpServerUtility** classes have been updated to encode the single quotation mark character (') as follows:</span></span>

- <span data-ttu-id="3a64f-150">**HtmlEncode**方法将单引号的实例编码为。</span><span class="sxs-lookup"><span data-stu-id="3a64f-150">The **HtmlEncode** method encodes instances of the single quotation mark as ' .</span></span>
- <span data-ttu-id="3a64f-151">**UrlEncode**方法将单引号的实例编码为 %27。</span><span class="sxs-lookup"><span data-stu-id="3a64f-151">The **UrlEncode** method encodes instances of the single quotation mark as %27.</span></span>

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a><span data-ttu-id="3a64f-152">ASP.NET 页面 (.aspx) 分析器是 Stricter</span><span class="sxs-lookup"><span data-stu-id="3a64f-152">ASP.NET Page (.aspx) Parser is Stricter</span></span>

<span data-ttu-id="3a64f-153">ASP.NET 页的页分析器 (`.aspx`文件) 和用户控件 (`.ascx`文件) 是在 ASP.NET 4 中更严格，则将拒绝无效标记的更多实例。</span><span class="sxs-lookup"><span data-stu-id="3a64f-153">The page parser for ASP.NET pages (`.aspx` files) and user controls (`.ascx` files) is stricter in ASP.NET 4 and will reject more instances of invalid markup.</span></span> <span data-ttu-id="3a64f-154">例如，以下两个代码片段会将已成功分析在早期版本的 ASP.NET，但现在将引发在 ASP.NET 4 中的分析器错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-154">For example, the following two snippets would successfully parse in earlier releases of ASP.NET, but will now raise parser errors in ASP.NET 4.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

<span data-ttu-id="3a64f-155">请注意，末尾处的无效分号**HiddenField**标记。</span><span class="sxs-lookup"><span data-stu-id="3a64f-155">Notice the invalid semicolon at the end of the **HiddenField** tag.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

<span data-ttu-id="3a64f-156">请注意，未闭合**样式**属性，在遇到**CssClass**属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-156">Notice the unclosed **style** attribute that runs into the **CssClass** attribute.</span></span>

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a><span data-ttu-id="3a64f-157">更新的浏览器定义文件</span><span class="sxs-lookup"><span data-stu-id="3a64f-157">Browser Definition Files Updated</span></span>

<span data-ttu-id="3a64f-158">浏览器定义文件已更新，以包括有关新的和已更新的浏览器和设备的信息。</span><span class="sxs-lookup"><span data-stu-id="3a64f-158">The browser definition files have been updated to include information about new and updated browsers and devices.</span></span> <span data-ttu-id="3a64f-159">旧式浏览器和设备（如 Netscape Navigator）已被删除，并且已添加更新的浏览器和设备（如 Google Chrome 和 Apple iPhone）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-159">Older browsers and devices such as Netscape Navigator have been removed, and newer browsers and devices such as Google Chrome and Apple iPhone have been added.</span></span>

<span data-ttu-id="3a64f-160">如果应用程序包含的自定义浏览器定义继承自一个已删除的浏览器定义，将会出现错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-160">If your application contains custom browser definitions that inherit from one of the browser definitions that have been removed, you will see an error.</span></span> <span data-ttu-id="3a64f-161">例如，如果`App_Browsers`文件夹包含从 IE2 浏览器定义继承的浏览器定义，您将收到以下配置错误消息：</span><span class="sxs-lookup"><span data-stu-id="3a64f-161">For example, if the `App_Browsers` folder contains a browser definition that inherits from the IE2 browser definition, you will receive the following configuration error message:</span></span>

- <span data-ttu-id="3a64f-162">找不到 id 为 IE2 的浏览器或网关元素。</span><span class="sxs-lookup"><span data-stu-id="3a64f-162">The browser or gateway element with ID 'IE2' cannot be found.</span></span>

> [!NOTE]
> <span data-ttu-id="3a64f-163">**HttpBrowserCapabilities**对象 (这由页面的公开**Request.Browser**属性) 由浏览器定义文件驱动。</span><span class="sxs-lookup"><span data-stu-id="3a64f-163">The **HttpBrowserCapabilities** object (which is exposed by the page's **Request.Browser** property) is driven by the browser definitions files.</span></span> <span data-ttu-id="3a64f-164">因此，通过访问该对象在 ASP.NET 4 中的属性返回的信息可能不同于 ASP.NET 的早期版本中返回的信息。</span><span class="sxs-lookup"><span data-stu-id="3a64f-164">Therefore, the information returned by accessing a property of this object in ASP.NET 4 might be different than the information returned in an earlier version of ASP.NET.</span></span>


<span data-ttu-id="3a64f-165">您可以通过从以下文件夹复制浏览器定义文件还原到旧的浏览器定义文件：</span><span class="sxs-lookup"><span data-stu-id="3a64f-165">You can revert to the old browser definition files by copying the browser definition files from the following folder:</span></span>

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

<span data-ttu-id="3a64f-166">将文件复制到相应`\CONFIG\Browsers`为 ASP.NET 4 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3a64f-166">Copy the files into the corresponding `\CONFIG\Browsers` folder for ASP.NET 4.</span></span> <span data-ttu-id="3a64f-167">复制文件后，运行 Aspnet\_regbrowsers.exe 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="3a64f-167">After you copy the files, run the Aspnet\_regbrowsers.exe command-line tool.</span></span>

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a><span data-ttu-id="3a64f-168">System.Web.Mobile.dll 从根 Web 配置文件中删除</span><span class="sxs-lookup"><span data-stu-id="3a64f-168">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>

<span data-ttu-id="3a64f-169">在以前版本的 ASP.NET，对 System.Web.Mobile.dll 程序集的引用已包含在根`Web.config`文件中**程序集**部分下。</span><span class="sxs-lookup"><span data-stu-id="3a64f-169">In previous versions of ASP.NET, a reference to the System.Web.Mobile.dll assembly was included in the root `Web.config` file in the **assemblies** section under.</span></span> <span data-ttu-id="3a64f-170">为了提高性能，已删除对此程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-170">In order to improve performance, the reference to this assembly was removed.</span></span>

<span data-ttu-id="3a64f-171">System.Web.Mobile.dll 程序集包含在 ASP.NET 4 中，但不推荐使用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-171">The System.Web.Mobile.dll assembly is included in ASP.NET 4, but it is deprecated.</span></span> <span data-ttu-id="3a64f-172">如果你想要使用从 System.Web.Mobile.dll 程序集的类型，将对此程序集的引用添加到根`Web.config`文件或某个应用程序`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-172">If you want to use types from the System.Web.Mobile.dll assembly, add a reference to this assembly to either the root `Web.config` file or to an application `Web.config` file.</span></span> <span data-ttu-id="3a64f-173">例如，如果你想要使用的任何 （已弃用） 的 ASP.NET 移动控件，您必须添加对 System.Web.Mobile.dll 程序集的引用`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-173">For example, if you want to use any of the (deprecated) ASP.NET mobile controls, you must add a reference to the System.Web.Mobile.dll assembly to the `Web.config` file.</span></span>

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a><span data-ttu-id="3a64f-174">ASP.NET 请求验证</span><span class="sxs-lookup"><span data-stu-id="3a64f-174">ASP.NET Request Validation</span></span>

<span data-ttu-id="3a64f-175">在 ASP.NET 请求验证功能提供了一定的默认保护免受跨站点脚本 (XSS) 攻击。</span><span class="sxs-lookup"><span data-stu-id="3a64f-175">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="3a64f-176">在以前版本的 ASP.NET 中，默认情况下已启用请求验证。</span><span class="sxs-lookup"><span data-stu-id="3a64f-176">In previous versions of ASP.NET, request validation was enabled by default.</span></span> <span data-ttu-id="3a64f-177">但是，它仅应用于 ASP.NET 页面 (`.aspx`文件和其类文件) 和仅当这些页面执行。</span><span class="sxs-lookup"><span data-stu-id="3a64f-177">However, it applied only to ASP.NET pages (`.aspx` files and their class files) and only when those pages were executing.</span></span>

<span data-ttu-id="3a64f-178">在 ASP.NET 4 中，默认情况下启用请求验证的所有请求，因为它启用之前**BeginRequest**阶段的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="3a64f-178">In ASP.NET 4, by default, request validation is enabled for all requests, because it is enabled before the **BeginRequest** phase of an HTTP request.</span></span> <span data-ttu-id="3a64f-179">因此，请求验证适用于所有 ASP.NET 资源，而不仅仅是.aspx 页请求的请求。</span><span class="sxs-lookup"><span data-stu-id="3a64f-179">As a result, request validation applies to requests for all ASP.NET resources, not just .aspx page requests.</span></span> <span data-ttu-id="3a64f-180">这包括如 Web 服务调用和自定义 HTTP 处理程序的请求。</span><span class="sxs-lookup"><span data-stu-id="3a64f-180">This includes requests such as Web service calls and custom HTTP handlers.</span></span> <span data-ttu-id="3a64f-181">请求验证也处于活动状态的自定义 HTTP 模块将读取的 HTTP 请求内容时。</span><span class="sxs-lookup"><span data-stu-id="3a64f-181">Request validation is also active when custom HTTP modules are reading the contents of an HTTP request.</span></span>

<span data-ttu-id="3a64f-182">因此，以前未触发错误的请求可能现在会出现请求验证错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-182">As a result, request validation errors might now occur for requests that previously did not trigger errors.</span></span> <span data-ttu-id="3a64f-183">若要还原到 ASP.NET 2.0 请求验证功能的行为，添加以下设置中的`Web.config`文件：</span><span class="sxs-lookup"><span data-stu-id="3a64f-183">To revert to the behavior of the ASP.NET 2.0 request validation feature, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

<span data-ttu-id="3a64f-184">但是，我们建议你分析任何请求验证错误，以确定是否存在的处理程序、 模块或其他自定义代码访问可能不安全 HTTP 输入的可能是 XSS 攻击途径。</span><span class="sxs-lookup"><span data-stu-id="3a64f-184">However, we recommend that you analyze any request validation errors to determine whether existing handlers, modules, or other custom code accesses potentially unsafe HTTP inputs that could be XSS attack vectors.</span></span>

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a><span data-ttu-id="3a64f-185">哈希算法的默认值现在为 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="3a64f-185">Default Hashing Algorithm Is Now HMACSHA256</span></span>

<span data-ttu-id="3a64f-186">ASP.NET 使用加密算法和哈希算法来帮助保护数据（如窗体身份验证 Cookie 和视图状态）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-186">ASP.NET uses both encryption and hashing algorithms to help secure data such as forms authentication cookies and view state.</span></span> <span data-ttu-id="3a64f-187">默认情况下，ASP.NET 4 现在使用 HMACSHA256 算法对 cookie 和视图状态哈希操作。</span><span class="sxs-lookup"><span data-stu-id="3a64f-187">By default, ASP.NET 4 now uses the HMACSHA256 algorithm for hash operations on cookies and view state.</span></span> <span data-ttu-id="3a64f-188">早期版本的 ASP.NET 使用较旧的 HMACSHA1 算法。</span><span class="sxs-lookup"><span data-stu-id="3a64f-188">Earlier versions of ASP.NET used the older HMACSHA1 algorithm.</span></span>

<span data-ttu-id="3a64f-189">如果运行混合的 ASP.NET 2.0/ASP.NET 4，可能会影响你的应用程序数据，例如窗体身份验证 cookie 一定 across.NET Framework 版本的环境。</span><span class="sxs-lookup"><span data-stu-id="3a64f-189">Your applications might be affected if you run mixed ASP.NET 2.0/ASP.NET 4 environments where data such as forms authentication cookies must work across.NET Framework versions.</span></span> <span data-ttu-id="3a64f-190">若要配置 ASP.NET 4 Web 应用程序使用较旧的 HMACSHA1 算法，添加以下设置中的`Web.config`文件：</span><span class="sxs-lookup"><span data-stu-id="3a64f-190">To configure an ASP.NET 4 Web application to use the older HMACSHA1 algorithm, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a><span data-ttu-id="3a64f-191">与新的 ASP.NET 4 根配置相关的配置错误</span><span class="sxs-lookup"><span data-stu-id="3a64f-191">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>

<span data-ttu-id="3a64f-192">根配置文件 (`machine.config`文件和根`Web.config`文件) 的已更新.NET Framework 4 （以及因此 ASP.NET 4） 若要包括的大多数样本配置信息中找到 ASP.NET 3.5 中的应用程序`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-192">The root configuration files (the `machine.config` file and the root `Web.config` file) for the .NET Framework 4 (and therefore ASP.NET 4) have been updated to include most of the boilerplate configuration information that in ASP.NET 3.5 was found in the application `Web.config` files.</span></span> <span data-ttu-id="3a64f-193">由于托管 IIS 7 和 IIS 7.5 配置系统的复杂性，运行 ASP.NET 4 下以及在 IIS 7 和 IIS 7.5 的 ASP.NET 3.5 应用程序可以导致 ASP.NET 或 IIS 配置错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-193">Because of the complexity of the managed IIS 7 and IIS 7.5 configuration systems, running ASP.NET 3.5 applications under ASP.NET 4 and under IIS 7 and IIS 7.5 can result in either ASP.NET or IIS configuration errors.</span></span>

<span data-ttu-id="3a64f-194">我们建议如果可行，通过在 Visual Studio 2010 中，使用的项目升级工具升级到 ASP.NET 4 的 ASP.NET 3.5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-194">We recommend that you upgrade ASP.NET 3.5 applications to ASP.NET 4 by using the project upgrade tools in Visual Studio 2010, if practical.</span></span> <span data-ttu-id="3a64f-195">Visual Studio 2010 自动修改 ASP.NET 3.5 应用程序的`Web.config`文件以包含为 ASP.NET 4 的相应设置。</span><span class="sxs-lookup"><span data-stu-id="3a64f-195">Visual Studio 2010 automatically modifies the ASP.NET 3.5 application's `Web.config` file to contain the appropriate settings for ASP.NET 4.</span></span>

<span data-ttu-id="3a64f-196">但是，它是受支持的方案运行使用.NET Framework 4 中无需重新编译的 ASP.NET 3.5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-196">However, it is a supported scenario to run ASP.NET 3.5 applications using the .NET Framework 4 without recompilation.</span></span> <span data-ttu-id="3a64f-197">在这种情况下，您可能必须手动修改应用程序的`Web.config`文件之前运行的应用程序在.NET Framework 4 和 IIS 7 或 IIS 7.5 下。</span><span class="sxs-lookup"><span data-stu-id="3a64f-197">In that case, you might have to manually modify the application's `Web.config` file before you run the application under the .NET Framework 4 and under IIS 7 or IIS 7.5.</span></span>

<span data-ttu-id="3a64f-198">接下来的两部分介绍可能需要的软件的不同组合进行的更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-198">The next two sections describe changes that you might need to make for different combinations of software.</span></span>

<span data-ttu-id="3a64f-199">**Windows Vista SP1 或 Windows Server 2008 SP1 中，既不 KB958854 修补程序，也不 SP2 的安装位置。**</span><span class="sxs-lookup"><span data-stu-id="3a64f-199">**Windows Vista SP1 or Windows Server 2008 SP1, where neither hotfix KB958854 nor SP2 are installed.**</span></span> <span data-ttu-id="3a64f-200">在此配置中，IIS 7 配置系统错误地将应用程序的受管理的配置合并通过比较应用程序级`Web.config`文件到 ASP.NET 2.0`machine.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-200">In this configuration, the IIS 7 configuration system incorrectly merges an application's managed configuration by comparing the application-level `Web.config` file to the ASP.NET 2.0 `machine.config` files.</span></span> <span data-ttu-id="3a64f-201">由于此，应用程序级`Web.config`从.NET Framework 3.5 或更高版本的文件必须具有**system.web.extensions**为了不会导致 IIS 7 验证失败的配置节定义 （元素）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-201">Because of this, application-level `Web.config` files from the .NET Framework 3.5 or later must have a **system.web.extensions** configuration section definition (the element) in order not to cause an IIS 7 validation failure.</span></span>

<span data-ttu-id="3a64f-202">但是，手动修改应用程序级`Web.config`不精确匹配引入了 Visual Studio 2008 的原始样本配置部分中定义的文件条目将导致 ASP.NET 配置错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-202">However, manually modified application-level `Web.config` file entries that do not precisely match the original boilerplate configuration section definitions that were introduced with Visual Studio 2008 will cause ASP.NET configuration errors.</span></span> <span data-ttu-id="3a64f-203">（生成的 Visual Studio 2008 的默认配置项正常工作。）一个常见问题是手动修改`Web.config`文件省略**allowDefinition**并**requirePermission**在各种配置部分中找到的配置属性定义。</span><span class="sxs-lookup"><span data-stu-id="3a64f-203">(The default configuration entries that are generated by Visual Studio 2008 work correctly.) A common problem is that manually modified `Web.config` files leave out the **allowDefinition** and **requirePermission** configuration attributes that are found on various configuration section definitions.</span></span> <span data-ttu-id="3a64f-204">这会导致应用程序级别中的缩写的配置部分之间不匹配`Web.config`文件和 ASP.NET 4 中的完整定义`machine.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-204">This causes a mismatch between the abbreviated configuration section in application-level `Web.config` files and the complete definition in the ASP.NET 4 `machine.config` file.</span></span> <span data-ttu-id="3a64f-205">因此，在运行时，ASP.NET 4 配置系统引发配置错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-205">As a result, at run time, the ASP.NET 4 configuration system throws a configuration error.</span></span>

<span data-ttu-id="3a64f-206">**Windows Vista SP2、 Windows Server 2008 SP2、 Windows 7、 Windows Server 2008 R2，并且还使用 Windows Vista SP1 和 Windows Server 2008 SP1 安装了修补程序 KB958854。**</span><span class="sxs-lookup"><span data-stu-id="3a64f-206">**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2, and also Windows Vista SP1 and Windows Server 2008 SP1 where hotfix KB958854 is installed.**</span></span>

<span data-ttu-id="3a64f-207">在此方案中，IIS 7 和 IIS 7.5 本机配置系统将返回配置错误因为它对执行文本比较**类型**为受管理的配置节处理程序定义的属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-207">In this scenario, the IIS 7 and IIS 7.5 native configuration system returns a configuration error because it performs a text comparison on the **type** attribute that is defined for a managed configuration section handler.</span></span> <span data-ttu-id="3a64f-208">因为所有`Web.config`生成的 Visual Studio 2008 和 Visual Studio 2008 SP1 的文件具有"3.5"中的类型字符串**system.web.extensions** （和相关） 配置节处理程序，因为 ASP.NET4`machine.config`文件中具有"4.0"**类型**属性 (attribute) 同一个配置节处理程序，始终在 Visual Studio 2008 或 Visual Studio 2008 SP1 中生成的应用程序无法通过在 IIS 7 中的配置验证和IIS 7.5。</span><span class="sxs-lookup"><span data-stu-id="3a64f-208">Because all `Web.config` files that are generated by Visual Studio 2008 and Visual Studio 2008 SP1 have "3.5" in the type string for the **system.web.extensions** (and related) configuration section handlers, and because the ASP.NET 4 `machine.config` file has "4.0" in the **type** attribute for the same configuration section handlers, applications that are generated in Visual Studio 2008 or Visual Studio 2008 SP1 always fail configuration validation in IIS 7 and IIS 7.5.</span></span>

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a><span data-ttu-id="3a64f-209">解决这些问题</span><span class="sxs-lookup"><span data-stu-id="3a64f-209">Resolving These Issues</span></span>

<span data-ttu-id="3a64f-210">第一个方案的解决方法是更新应用程序级`Web.config`文件将从样板配置文本包含`Web.config`由 Visual Studio 2008 会自动生成的文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-210">The workaround for the first scenario is to update the application-level `Web.config` file by including the boilerplate configuration text from a `Web.config` file that was generated automatically by Visual Studio 2008.</span></span>

<span data-ttu-id="3a64f-211">备用解决方法的第一个方案是在计算机上安装的 Vista 或 Windows Server 2008 Service Pack 2 或安装修补程序 KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) 若要修复的不正确的配置合并行为IIS 配置系统。</span><span class="sxs-lookup"><span data-stu-id="3a64f-211">An alternative workaround for the first scenario is to install Service Pack 2 for Vista or Windows Server 2008 on your computer or to install hotfix KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) to fix the incorrect configuration-merge behavior of the IIS configuration system.</span></span> <span data-ttu-id="3a64f-212">但是，执行上述任一操作后，你的应用程序可能遇到的第二个方案所述的问题由于配置错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-212">However, after you perform either of these actions, your application will likely encounter a configuration error due to the issue described for the second scenario.</span></span>

<span data-ttu-id="3a64f-213">第二个方案的解决方法是删除或注释掉所有**system.web.extensions**配置节定义和配置节组的应用程序级定义`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-213">The workaround for the second scenario is to delete or comment out all the **system.web.extensions** configuration section definitions and configuration section group definitions from the application-level `Web.config` file.</span></span> <span data-ttu-id="3a64f-214">这些定义通常位于应用程序级别顶部`Web.config`文件，并可以由标识**configSections**元素及其子项。</span><span class="sxs-lookup"><span data-stu-id="3a64f-214">These definitions are usually at the top of the application-level `Web.config` file and can be identified by the **configSections** element and its children.</span></span>

<span data-ttu-id="3a64f-215">对于这两种方案，建议手动删除**system.codedom**部分中，虽然这不是必需。</span><span class="sxs-lookup"><span data-stu-id="3a64f-215">For both scenarios, it is recommended that you also manually delete the **system.codedom** section, although this is not required.</span></span>

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a><span data-ttu-id="3a64f-216">ASP.NET 4 子应用程序启动失败的时在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序</span><span class="sxs-lookup"><span data-stu-id="3a64f-216">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>

<span data-ttu-id="3a64f-217">由于配置或编译错误，配置为运行 ASP.NET 早期版本的应用程序子级的 ASP.NET 4 应用程序可能无法启动。</span><span class="sxs-lookup"><span data-stu-id="3a64f-217">ASP.NET 4 applications that are configured as children of applications that run earlier versions of ASP.NET might fail to start because of configuration or compilation errors.</span></span> <span data-ttu-id="3a64f-218">下面的示例显示了受影响的应用程序的目录结构。</span><span class="sxs-lookup"><span data-stu-id="3a64f-218">The following example shows a directory structure for an affected application.</span></span>

<span data-ttu-id="3a64f-219">`/parentwebapp` （配置为使用 ASP.NET 2.0 或 ASP.NET 3.5）</span><span class="sxs-lookup"><span data-stu-id="3a64f-219">`/parentwebapp` (configured to use ASP.NET 2.0 or ASP.NET 3.5)</span></span>  
<span data-ttu-id="3a64f-220">`/childwebapp` （配置为使用 ASP.NET 4）</span><span class="sxs-lookup"><span data-stu-id="3a64f-220">`/childwebapp` (configured to use ASP.NET 4)</span></span>

<span data-ttu-id="3a64f-221">中的应用程序`childwebapp`文件夹将无法启动在 IIS 7 或 IIS 7.5 上并将报表配置错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-221">The application in the `childwebapp` folder will fail to start on IIS 7 or IIS 7.5 and will report a configuration error.</span></span> <span data-ttu-id="3a64f-222">错误文本将包含一条类似于以下消息：</span><span class="sxs-lookup"><span data-stu-id="3a64f-222">The error text will include a message similar to the following:</span></span>

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`
  

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

<span data-ttu-id="3a64f-223">在 IIS 6 中的应用程序上`childwebapp`文件夹也将无法启动，但它将会报告其他错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-223">On IIS 6, the application in the `childwebapp` folder will also fail to start, but it will report a different error.</span></span> <span data-ttu-id="3a64f-224">例如，错误文本可能状态如下：</span><span class="sxs-lookup"><span data-stu-id="3a64f-224">For example, the error text might state the following:</span></span>

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

<span data-ttu-id="3a64f-225">因为，会出现这些情况中的父应用程序中的配置信息`parentwebapp`文件夹是确定使用的子站点的最后一个合并的配置设置的配置信息的层次结构的一部分应用程序中`childwebapp`文件夹。</span><span class="sxs-lookup"><span data-stu-id="3a64f-225">These scenarios occur because the configuration information from the parent application in the `parentwebapp` folder is part of the hierarchy of configuration information that determines the final merged configuration settings that are used by the child web application in the `childwebapp` folder.</span></span> <span data-ttu-id="3a64f-226">具体取决于 ASP.NET 4 Web 应用程序是否在 IIS 7 （或 IIS 7.5） 上或在 IIS 6 上运行，IIS 配置系统或 ASP.NET 4 编译系统会返回错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-226">Depending on whether the ASP.NET 4 Web application is running on IIS 7 (or IIS 7.5) or on IIS 6, either the IIS configuration system or the ASP.NET 4 compilation system will return an error.</span></span>

<span data-ttu-id="3a64f-227">若要解决此问题并获取子 ASP.NET 4 应用程序工作必须遵循的步骤取决于 ASP.NET 4 应用程序是否在 IIS 7 （或 IIS 7.5） 上运行了 IIS 6 或。</span><span class="sxs-lookup"><span data-stu-id="3a64f-227">The steps that you must follow to resolve this issue and to get the child ASP.NET 4 application to work depend on whether the ASP.NET 4 application runs on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

### <a name="step-1-iis-7-or-iis-75-only"></a><span data-ttu-id="3a64f-228">步骤 1 （IIS 7 或 IIS 7.5 仅）</span><span class="sxs-lookup"><span data-stu-id="3a64f-228">Step 1 (IIS 7 or IIS 7.5 only)</span></span>

<span data-ttu-id="3a64f-229">此步骤是必需仅在运行 IIS 7 的操作系统或 IIS 7.5，其中包括 Windows Vista、 Windows Server 2008、 Windows 7 和 Windows Server 2008 R2 上。</span><span class="sxs-lookup"><span data-stu-id="3a64f-229">This step is necessary only on operating systems that run IIS 7 or IIS 7.5, which includes Windows Vista, Windows Server 2008, Windows 7, and Windows Server 2008 R2.</span></span>

<span data-ttu-id="3a64f-230">移动**configSections**中的定义`Web.config`文件的父应用程序 （运行 ASP.NET 2.0 或 ASP.NET 3.5 的应用程序） 到根目录`Web.config`.net Framework 2.0 的文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-230">Move the **configSections** definition in the `Web.config` file of the parent application (the application that runs ASP.NET 2.0 or ASP.NET 3.5) into the root `Web.config` file for the.NET Framework 2.0.</span></span> <span data-ttu-id="3a64f-231">IIS 7 和 IIS 7.5 native 配置系统扫描**configSections**元素时合并配置文件的层次结构。</span><span class="sxs-lookup"><span data-stu-id="3a64f-231">The IIS 7 and IIS 7.5 native configuration system scans the **configSections** element when it merges the hierarchy of configuration files.</span></span> <span data-ttu-id="3a64f-232">移动**configSections**从父 Web 应用程序的定义`Web.config`根文件`Web.config`文件实际上就隐藏了所发生的子 ASP.NET 4 的配置合并过程中的元素应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-232">Moving the **configSections** definition from the parent Web application's `Web.config` file to the root `Web.config` file effectively hides the element from the configuration merge process that occurs for the child ASP.NET 4 application.</span></span>

<span data-ttu-id="3a64f-233">在 32 位操作系统上或 32 位应用程序池，根的`Web.config`ASP.NET 2.0 和 ASP.NET 3.5 中的文件通常位于以下文件夹中：</span><span class="sxs-lookup"><span data-stu-id="3a64f-233">On a 32-bit operating system or for 32-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

<span data-ttu-id="3a64f-234">在 64 位操作系统上或 64 位应用程序池，根的`Web.config`ASP.NET 2.0 和 ASP.NET 3.5 中的文件通常位于以下文件夹中：</span><span class="sxs-lookup"><span data-stu-id="3a64f-234">On a 64-bit operating system or for 64-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

<span data-ttu-id="3a64f-235">如果在 64 位计算机上运行 32 位和 64 位 Web 应用程序，则必须移动**configSections**根元素向上`Web.config`32 位和 64 位系统文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-235">If you run both 32-bit and 64-bit Web applications on a 64-bit computer, you must move the **configSections** element up into root `Web.config` files for both the 32-bit and the 64-bit systems.</span></span>

<span data-ttu-id="3a64f-236">当将**configSections**根目录中的元素`Web.config`文件中，粘贴部分后立即**配置**元素。</span><span class="sxs-lookup"><span data-stu-id="3a64f-236">When you put the **configSections** element in the root `Web.config` file, paste the section immediately after the **configuration** element.</span></span> <span data-ttu-id="3a64f-237">下面的示例演示根哪些的上半部分`Web.config`文件应如下所示完成移动元素。</span><span class="sxs-lookup"><span data-stu-id="3a64f-237">The following example shows what the top portion of the root `Web.config` file should look like when you have finished moving the elements.</span></span>

> [!NOTE]
> <span data-ttu-id="3a64f-238">在以下示例中，以提高可读性已换行。</span><span class="sxs-lookup"><span data-stu-id="3a64f-238">In the following example, lines have been wrapped for readability.</span></span>


[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a><span data-ttu-id="3a64f-239">步骤 2 （所有版本的 IIS）</span><span class="sxs-lookup"><span data-stu-id="3a64f-239">Step 2 (all versions of IIS)</span></span>

<span data-ttu-id="3a64f-240">此步骤是必需的 ASP.NET 4 子 Web 应用程序是否正在运行 IIS 6 上或在 IIS 7 （或 IIS 7.5） 上。</span><span class="sxs-lookup"><span data-stu-id="3a64f-240">This step is required whether the ASP.NET 4 child Web application is running on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

<span data-ttu-id="3a64f-241">在中`Web.config`文件中的父 Web 应用程序运行的 ASP.NET 2 或 ASP.NET 3.5 中，添加**位置**显式指定 （对于 IIS 和 ASP.NET 配置系统） 的标记的配置条目仅将应用于父 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-241">In the `Web.config` file of the parent Web application that is running ASP.NET 2 or ASP.NET 3.5, add a **location** tag that explicitly specifies (for both the IIS and ASP.NET configuration systems) that the configuration entries only apply to the parent Web application.</span></span> <span data-ttu-id="3a64f-242">下面的示例演示的语法**位置**要添加元素：</span><span class="sxs-lookup"><span data-stu-id="3a64f-242">The following example shows the syntax of the **location** element to add:</span></span>

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

<span data-ttu-id="3a64f-243">下面的示例演示如何**位置**标记用于包装开头的所有配置节**appSettings**部分，并以结尾**system.webServer**部分。</span><span class="sxs-lookup"><span data-stu-id="3a64f-243">The following example shows how the **location** tag is used to wrap all configuration sections starting with the **appSettings** section and ending with **system.webServer** section.</span></span>

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

<span data-ttu-id="3a64f-244">完成步骤 1 和 2 后，子 ASP.NET 4 Web 应用程序将启动且未出错。</span><span class="sxs-lookup"><span data-stu-id="3a64f-244">When you have completed steps 1 and 2, child ASP.NET 4 Web applications will start without errors.</span></span>

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a><span data-ttu-id="3a64f-245">ASP.NET 4 网站不能在安装 SharePoint 计算机上启动</span><span class="sxs-lookup"><span data-stu-id="3a64f-245">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>

<span data-ttu-id="3a64f-246">运行 SharePoint 的 web 服务器具有`Web.config`部署的 SharePoint 网站根目录的文件 (例如，`c:\inetpub\wwwroot\web.config`的默认 Web 站点)。</span><span class="sxs-lookup"><span data-stu-id="3a64f-246">Web servers that run SharePoint have a `Web.config` file that is deployed at the root of a SharePoint Web site (for example, `c:\inetpub\wwwroot\web.config` for Default Web Site).</span></span> <span data-ttu-id="3a64f-247">在此`Web.config`文件中，SharePoint 自定义部分信任级别设置名为 WSS\_最小。</span><span class="sxs-lookup"><span data-stu-id="3a64f-247">In this `Web.config` file, SharePoint sets a custom partial-trust level named WSS\_Minimal.</span></span>

<span data-ttu-id="3a64f-248">如果尝试为此类型的 SharePoint Web 站点的子级运行部署的 ASP.NET 4 Web 站点，您将看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="3a64f-248">If you try to run an ASP.NET 4 Web site that is deployed as a child of this type of SharePoint Web site, you will see the following error:</span></span>

`Could not find permission set named 'ASP.NET'.`

<span data-ttu-id="3a64f-249">此错误是因为 ASP.NET 4 代码访问安全性 (CAS) 基础结构会查找名为 ASP.NET 的权限集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-249">This error occurs because the ASP.NET 4 code access security (CAS) infrastructure looks for a permission set named ASP.NET.</span></span> <span data-ttu-id="3a64f-250">但是，部分信任配置文件引用的 WSS\_最小不包含具有该名称的任何权限集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-250">However, the partial trust configuration file that is referenced by WSS\_Minimal does not contain any permission sets with that name.</span></span>

<span data-ttu-id="3a64f-251">目前还没有 SharePoint 可与 ASP.NET 兼容的版本。</span><span class="sxs-lookup"><span data-stu-id="3a64f-251">Currently there is not a version of SharePoint available that is compatible with ASP.NET.</span></span> <span data-ttu-id="3a64f-252">因此，您不应尝试作为子站点下 SharePoint Web 站点运行的 ASP.NET 4 网站。</span><span class="sxs-lookup"><span data-stu-id="3a64f-252">As a result, you should not attempt to run an ASP.NET 4 Web site as a child site underneath SharePoint Web sites.</span></span>

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a><span data-ttu-id="3a64f-253">HttpRequest.FilePath 属性不再包括 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="3a64f-253">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>

<span data-ttu-id="3a64f-254">包含 ASP.NET 的早期版本**PathInfo**各种文件路径相关的属性，包括从返回的值中的值**HttpRequest.FilePath**， **HttpRequest.AppRelativeCurrentExecutionFilePath**，并**HttpRequest.CurrentExecutionFilePath**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-254">Previous versions of ASP.NET included a **PathInfo** value in the value returned from various file path-related properties, including **HttpRequest.FilePath**, **HttpRequest.AppRelativeCurrentExecutionFilePath**, and **HttpRequest.CurrentExecutionFilePath**.</span></span> <span data-ttu-id="3a64f-255">ASP.NET 4 不再包括**PathInfo**从这些属性的返回值中的值。</span><span class="sxs-lookup"><span data-stu-id="3a64f-255">ASP.NET 4 no longer includes the **PathInfo** value in the return values from these properties.</span></span> <span data-ttu-id="3a64f-256">相反， **PathInfo**中提供了信息**HttpRequest.PathInfo**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-256">Instead, the **PathInfo** information is available in **HttpRequest.PathInfo**.</span></span> <span data-ttu-id="3a64f-257">例如，假定以下 URL 片段：</span><span class="sxs-lookup"><span data-stu-id="3a64f-257">For example, imagine the following URL fragment:</span></span>

`/testapp/Action.mvc/SomeAction`

<span data-ttu-id="3a64f-258">在早期版本的 ASP.NET 中， **HttpRequest**属性具有以下值：</span><span class="sxs-lookup"><span data-stu-id="3a64f-258">In earlier versions of ASP.NET, **HttpRequest** properties have the following values:</span></span>

<span data-ttu-id="3a64f-259">**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`</span><span class="sxs-lookup"><span data-stu-id="3a64f-259">**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`</span></span>

<span data-ttu-id="3a64f-260">**HttpRequest.PathInfo**: （空）</span><span class="sxs-lookup"><span data-stu-id="3a64f-260">**HttpRequest.PathInfo**: (empty)</span></span>

<span data-ttu-id="3a64f-261">在 ASP.NET 4 中， **HttpRequest**属性改为具有以下值：</span><span class="sxs-lookup"><span data-stu-id="3a64f-261">In ASP.NET 4, **HttpRequest** properties instead have the following values:</span></span>

<span data-ttu-id="3a64f-262">**HttpRequest.FilePath**: `/testapp/Action.mvc`</span><span class="sxs-lookup"><span data-stu-id="3a64f-262">**HttpRequest.FilePath**: `/testapp/Action.mvc`</span></span>

<span data-ttu-id="3a64f-263">**HttpRequest.PathInfo**: `SomeAction`</span><span class="sxs-lookup"><span data-stu-id="3a64f-263">**HttpRequest.PathInfo**: `SomeAction`</span></span>

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a><span data-ttu-id="3a64f-264">ASP.NET 2.0 应用程序可能会生成引用 eurl.axd 的 HttpException 错误</span><span class="sxs-lookup"><span data-stu-id="3a64f-264">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>

<span data-ttu-id="3a64f-265">ASP.NET 4 启用 IIS 6 上之后，（在 Windows Server 2003 或 Windows Server 2003 R2） 的 IIS 6 运行的 ASP.NET 2.0 应用程序可能会产生如下所示的错误：</span><span class="sxs-lookup"><span data-stu-id="3a64f-265">After ASP.NET 4 has been enabled on IIS 6, ASP.NET 2.0 applications that run on IIS 6 (in either Windows Server 2003 or Windows Server 2003 R2) might generate errors such as the following:</span></span>

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

<span data-ttu-id="3a64f-266">当 ASP.NET 检测到配置的网站以使用 ASP.NET 4，ASP.NET 4 的本机组件无扩展名将 URL 传递到 ASP.NET 的托管部分进行进一步的处理会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-266">This error occurs because when ASP.NET detects that a Web site is configured to use ASP.NET 4, a native component of ASP.NET 4 passes an extensionless URL to the managed portion of ASP.NET for further processing.</span></span> <span data-ttu-id="3a64f-267">但是，如果 ASP.NET 4 Web 站点下的虚拟目录配置为使用 ASP.NET 2.0，则处理此方法会导致修改后的 URL，其中包含字符串"eurl.axd"中的无扩展名 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-267">However, if virtual directories that are below an ASP.NET 4 Web site are configured to use ASP.NET 2.0, processing the extensionless URL in this way results in a modified URL that contains the string "eurl.axd".</span></span> <span data-ttu-id="3a64f-268">然后，此修改后的 URL 被发送到 ASP.NET 2.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-268">This modified URL is then sent to the ASP.NET 2.0 application.</span></span> <span data-ttu-id="3a64f-269">ASP.NET 2.0 无法识别"eurl.axd"格式。</span><span class="sxs-lookup"><span data-stu-id="3a64f-269">ASP.NET 2.0 cannot recognize the "eurl.axd" format.</span></span> <span data-ttu-id="3a64f-270">因此，ASP.NET 2.0 将尝试查找名为的文件`eurl.axd`并执行它。</span><span class="sxs-lookup"><span data-stu-id="3a64f-270">Therefore, ASP.NET 2.0 tries to find a file named `eurl.axd` and execute it.</span></span> <span data-ttu-id="3a64f-271">因为没有这样的文件存在，则请求会失败**HttpException**异常。</span><span class="sxs-lookup"><span data-stu-id="3a64f-271">Because no such file exists, the request fails with an **HttpException** exception.</span></span>

<span data-ttu-id="3a64f-272">您可以解决此问题，使用以下选项之一。</span><span class="sxs-lookup"><span data-stu-id="3a64f-272">You can work around this issue using one of the following options.</span></span>

### <a name="option-1"></a><span data-ttu-id="3a64f-273">选项 1</span><span class="sxs-lookup"><span data-stu-id="3a64f-273">Option 1</span></span>

<span data-ttu-id="3a64f-274">如果 ASP.NET 4 不需要为了运行网站，重新映射该网站以改为使用 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="3a64f-274">If ASP.NET 4 is not required in order to run the Web site, remap the site to use ASP.NET 2.0 instead.</span></span>

### <a name="option-2"></a><span data-ttu-id="3a64f-275">选项 2</span><span class="sxs-lookup"><span data-stu-id="3a64f-275">Option 2</span></span>

<span data-ttu-id="3a64f-276">如果 ASP.NET 4 才能运行网站，移动到另一个网站映射到 ASP.NET 2.0 的所有子 ASP.NET 2.0 虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="3a64f-276">If ASP.NET 4 is required in order to run the Web site, move any child ASP.NET 2.0 virtual directories to a different Web site that is mapped to ASP.NET 2.0.</span></span>

### <a name="option-3"></a><span data-ttu-id="3a64f-277">选项 3</span><span class="sxs-lookup"><span data-stu-id="3a64f-277">Option 3</span></span>

<span data-ttu-id="3a64f-278">如果不可行，若要重新映射到 ASP.NET 2.0 网站，或若要更改虚拟目录的位置，显式禁用在 ASP.NET 4 中处理无扩展名 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-278">If it is not practical to remap the Web site to ASP.NET 2.0 or to change the location of a virtual directory, explicitly disable extensionless URL processing in ASP.NET 4.</span></span> <span data-ttu-id="3a64f-279">使用以下过程：</span><span class="sxs-lookup"><span data-stu-id="3a64f-279">Use the following procedure:</span></span>

1. <span data-ttu-id="3a64f-280">在 Windows 注册表中，打开以下节点：</span><span class="sxs-lookup"><span data-stu-id="3a64f-280">In the Windows registry, open the following node:</span></span>

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. <span data-ttu-id="3a64f-281">创建一个新**DWORD**名为值**EnableExtensionlessUrls**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-281">Create a new **DWORD** value named **EnableExtensionlessUrls**.</span></span>
2. <span data-ttu-id="3a64f-282">设置**EnableExtensionlessUrls**为 0。</span><span class="sxs-lookup"><span data-stu-id="3a64f-282">Set **EnableExtensionlessUrls** to 0.</span></span> <span data-ttu-id="3a64f-283">这将禁用无扩展名 URL 行为。</span><span class="sxs-lookup"><span data-stu-id="3a64f-283">This disables extensionless URL behavior.</span></span>
3. <span data-ttu-id="3a64f-284">保存注册表值并关闭注册表编辑器。</span><span class="sxs-lookup"><span data-stu-id="3a64f-284">Save the registry value and close the registry editor.</span></span>
4. <span data-ttu-id="3a64f-285">运行**iisreset**命令行工具，这会导致 IIS 读取新的注册表值。</span><span class="sxs-lookup"><span data-stu-id="3a64f-285">Run the **iisreset** command-line tool, which causes IIS to read the new registry value.</span></span>

> [!NOTE]
> <span data-ttu-id="3a64f-286">设置**EnableExtensionlessUrls**为 1 可启用无扩展名 URL 行为。</span><span class="sxs-lookup"><span data-stu-id="3a64f-286">Setting **EnableExtensionlessUrls** to 1 enables extensionless URL behavior.</span></span> <span data-ttu-id="3a64f-287">这是默认设置，如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="3a64f-287">This is the default setting if no value is specified.</span></span>


<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a><span data-ttu-id="3a64f-288">事件处理程序可能不会不引发在 IIS 7 或 IIS 7.5 中的默认文档集成模式下</span><span class="sxs-lookup"><span data-stu-id="3a64f-288">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>

<span data-ttu-id="3a64f-289">ASP.NET 4 中包含的更改的修改如何**操作**特性的 html**窗体**元素呈现时无扩展名 URL 解析为默认文档。</span><span class="sxs-lookup"><span data-stu-id="3a64f-289">ASP.NET 4 includes modifications that change how the **action** attribute of the HTML **form** element is rendered when an extensionless URL resolves to a default document.</span></span> <span data-ttu-id="3a64f-290">无扩展名 URL 解析为默认文档的示例将[ http://contoso.com/ ](http://contoso.com/)，从而导致对请求[ http://contoso.com/Default.aspx ](http://contoso.com/Default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3a64f-290">An example of an extensionless URL resolving to a default document would be [http://contoso.com/](http://contoso.com/), resulting in a request to [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx).</span></span>

<span data-ttu-id="3a64f-291">现在 ASP.NET 4 的 HTML 呈现**窗体**元素的**操作**属性值为空字符串，当请求时，有一个默认文档映射到它的无扩展名 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-291">ASP.NET 4 now renders the HTML **form** element's **action** attribute value as an empty string when a request is made to an extensionless URL that has a default document mapped to it.</span></span> <span data-ttu-id="3a64f-292">例如，在早期版本的 ASP.NET 中，对请求[ http://contoso.com ](http://contoso.com)会导致对请求`Default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="3a64f-292">For example, in earlier releases of ASP.NET, a request to [http://contoso.com](http://contoso.com) would result in a request to `Default.aspx`.</span></span> <span data-ttu-id="3a64f-293">在该文档中，打开**窗体**标记的呈现如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3a64f-293">In that document, the opening **form** tag would be rendered as in the following example:</span></span>

`<form action="Default.aspx" />`

<span data-ttu-id="3a64f-294">在 ASP.NET 4 中，对请求[ http://contoso.com ](http://contoso.com)也会导致对请求`Default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="3a64f-294">In ASP.NET 4, a request to [http://contoso.com](http://contoso.com) also results in a request to `Default.aspx`.</span></span> <span data-ttu-id="3a64f-295">但是，ASP.NET 现在也可以呈现 HTML 开始**窗体**标记如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3a64f-295">However, ASP.NET now renders the HTML opening **form** tag as in the following example:</span></span>

`<form action="" />`

<span data-ttu-id="3a64f-296">如何在这种差异**操作**呈现属性可能会导致细微的更改通过 IIS 和 ASP.NET 窗体发布请求的处理方式。</span><span class="sxs-lookup"><span data-stu-id="3a64f-296">This difference in how the **action** attribute is rendered can cause subtle changes in how a form post is processed by IIS and ASP.NET.</span></span> <span data-ttu-id="3a64f-297">当**操作**属性为空字符串，IIS **DefaultDocumentModule**对象将创建对的子请求`Default.aspx`。</span><span class="sxs-lookup"><span data-stu-id="3a64f-297">When the **action** attribute is an empty string, the IIS **DefaultDocumentModule** object will create a child request to `Default.aspx`.</span></span> <span data-ttu-id="3a64f-298">大多数情况下，此子请求是透明的应用程序代码和`Default.aspx`页会正常运行。</span><span class="sxs-lookup"><span data-stu-id="3a64f-298">Under most conditions, this child request is transparent to application code, and the `Default.aspx` page runs normally.</span></span>

<span data-ttu-id="3a64f-299">但托管代码和 IIS 7 或 IIS 7.5 集成模式之间可能的交互会导致托管 .aspx 页在子请求期间停止正常工作。</span><span class="sxs-lookup"><span data-stu-id="3a64f-299">However, a potential interaction between managed code and IIS 7 or IIS 7.5 Integrated mode can cause managed .aspx pages to stop working properly during the child request.</span></span> <span data-ttu-id="3a64f-300">如果发生以下情况时，对子请求`Default.aspx`文档将导致错误或意外行为：</span><span class="sxs-lookup"><span data-stu-id="3a64f-300">If the following conditions occur, the child request to a `Default.aspx` document will result in an error or in unexpected behavior:</span></span>

1. <span data-ttu-id="3a64f-301">使用浏览器发送一个.aspx 页面**窗体**元素的**操作**属性设置为""。</span><span class="sxs-lookup"><span data-stu-id="3a64f-301">An .aspx page is sent to the browser with the **form** element's **action** attribute set to "".</span></span>
2. <span data-ttu-id="3a64f-302">在窗体回发到 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="3a64f-302">The form is posted back to ASP.NET.</span></span>
3. <span data-ttu-id="3a64f-303">托管的 HTTP 模块读取实体正文的某些部分。</span><span class="sxs-lookup"><span data-stu-id="3a64f-303">A managed HTTP module reads some part of the entity body.</span></span> <span data-ttu-id="3a64f-304">例如，模块将读取**Request.Form**或**Request.Params**。</span><span class="sxs-lookup"><span data-stu-id="3a64f-304">For example, a module reads **Request.Form** or **Request.Params**.</span></span> <span data-ttu-id="3a64f-305">这会使 POST 请求的实体正文读入托管内存中。</span><span class="sxs-lookup"><span data-stu-id="3a64f-305">This causes the entity body of the POST request to be read into managed memory.</span></span> <span data-ttu-id="3a64f-306">因此，实体正文不再对在 IIS 7 或 IIS 7.5 集成模式中运行的任何本机代码模块可用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-306">As a result, the entity body is no longer available to any native code modules that are running in IIS 7 or IIS 7.5 Integrated mode.</span></span>
4. <span data-ttu-id="3a64f-307">IIS **DefaultDocumentModule**对象最终运行并创建到的子请求`Default.aspx`文档。</span><span class="sxs-lookup"><span data-stu-id="3a64f-307">The IIS **DefaultDocumentModule** object eventually runs and creates a child request to the `Default.aspx` document.</span></span> <span data-ttu-id="3a64f-308">但由于一段托管代码已读取实体正文，因此没有可发送给子请求的实体正文。</span><span class="sxs-lookup"><span data-stu-id="3a64f-308">However, because the entity body has already been read by a piece of managed code, there is no entity body available to send to the child request.</span></span>
5. <span data-ttu-id="3a64f-309">HTTP 管道子请求的处理程序的运行时`.aspx`对子阶段运行文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-309">When the HTTP pipeline runs for the child request, the handler for `.aspx` files runs during the handler-execute phase.</span></span>
6. <span data-ttu-id="3a64f-310">没有实体正文，因为有任何窗体变量和视图状态，并因此没有信息是可供.aspx 页处理程序，以确定应引发哪个事件 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-310">Because there is no entity body, there are no form variables and no view state, and therefore no information is available for the .aspx page handler to determine what event (if any) is supposed to be raised.</span></span> <span data-ttu-id="3a64f-311">因此，不会运行针对受影响 .aspx 页的任何回发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="3a64f-311">As a result, none of the postback event handlers for the affected .aspx page run.</span></span>

<span data-ttu-id="3a64f-312">您可以按以下方式来解决此行为：</span><span class="sxs-lookup"><span data-stu-id="3a64f-312">You can work around this behavior in the following ways:</span></span>

- <span data-ttu-id="3a64f-313">标识在默认文档的请求期间访问请求的实体正文的 HTTP 模块，并确定是否可以将它配置为仅针对托管请求运行。</span><span class="sxs-lookup"><span data-stu-id="3a64f-313">Identify the HTTP module that is accessing the request's entity body during default document requests and determine whether it can be configured to run only for managed requests.</span></span> <span data-ttu-id="3a64f-314">在 IIS 7 和 IIS 7.5 集成模式下，HTTP 模块可以将标记为仅针对托管请求通过将以下属性添加到模块的运行**system.webServer/modules**条目：</span><span class="sxs-lookup"><span data-stu-id="3a64f-314">In Integrated mode for both IIS 7 and IIS 7.5, HTTP modules can be marked to run only for managed requests by adding the following attribute to the module's **system.webServer/modules** entry:</span></span>

- `precondition="managedHandler"`

- <span data-ttu-id="3a64f-315">在模块中的搜索请求 IIS 7 和 IIS 7.5 确定为不符合此设置禁用管理请求。</span><span class="sxs-lookup"><span data-stu-id="3a64f-315">This setting disables the module for requests that IIS 7 and IIS 7.5 determine as not being managed requests.</span></span> <span data-ttu-id="3a64f-316">默认文档的请求，对于第一个请求都是无扩展名 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-316">For default document requests, the first request is to an extensionless URL.</span></span> <span data-ttu-id="3a64f-317">因此，IIS 不运行标记为任何托管的模块与托管处理程序的前置条件在初始请求处理过程。</span><span class="sxs-lookup"><span data-stu-id="3a64f-317">Therefore, IIS does not run any managed modules that are marked with a precondition of managed Handler during initial request processing.</span></span> <span data-ttu-id="3a64f-318">因此，托管的模块将不会意外地读取实体正文，因此实体正文仍可用，并传递给子请求和默认文档。</span><span class="sxs-lookup"><span data-stu-id="3a64f-318">As a result, managed modules will not accidentally read the entity body and thus the entity body is still available and is passed along to the child request and to the default document.</span></span>

- <span data-ttu-id="3a64f-319">如果有问题的 HTTP 模块必须运行的所有请求 (静态文件，针对无扩展名 Url 解析为的**DefaultDocumentModule**对象，用于托管的请求，等等)，显式修改按受影响的.aspx 页设置**操作**页面的属性**System.Web.UI.HtmlControls.HtmlForm**控件为非空字符串。</span><span class="sxs-lookup"><span data-stu-id="3a64f-319">If the problematic HTTP modules have to run for all requests (for static files, for extensionless URLs that resolve to the **DefaultDocumentModule** object, for managed requests, etc.), modify the affected .aspx pages by explicitly setting the **Action** property of the page's **System.Web.UI.HtmlControls.HtmlForm** control to a non-empty string.</span></span> <span data-ttu-id="3a64f-320">例如，如果默认文档是`Default.aspx`，修改页面的代码以显式设置**HtmlForm**控件的**操作**属性设置为"Default.aspx"。</span><span class="sxs-lookup"><span data-stu-id="3a64f-320">For example, if the default document is `Default.aspx`, modify the page's code to explicitly set the **HtmlForm** control's **Action** property to "Default.aspx".</span></span>

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a><span data-ttu-id="3a64f-321">对 ASP.NET 代码访问安全性 (CAS) 实现的更改</span><span class="sxs-lookup"><span data-stu-id="3a64f-321">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>

<span data-ttu-id="3a64f-322">ASP.NET 2.0 中，并通过扩展在 3.5 中，已添加的 ASP.NET 功能使用.NET Framework 1.1 和 2.0 代码访问安全性 (CAS) 模型。</span><span class="sxs-lookup"><span data-stu-id="3a64f-322">ASP.NET 2.0, and by extension the ASP.NET features that were added in 3.5, use the .NET Framework 1.1 and 2.0 code access security (CAS) model.</span></span> <span data-ttu-id="3a64f-323">但是，实质上已对 ASP.NET 4 中的 CAS 实现进行了检查。</span><span class="sxs-lookup"><span data-stu-id="3a64f-323">However, the implementation of CAS in ASP.NET 4 has been substantially overhauled.</span></span> <span data-ttu-id="3a64f-324">因此，依赖于受信任的代码在全局程序集缓存 (GAC) 中运行的部分信任 ASP.NET 应用程序可能会因各种安全异常。</span><span class="sxs-lookup"><span data-stu-id="3a64f-324">As a result, partial-trust ASP.NET applications that rely on trusted code running in the global assembly cache (GAC) might fail with various security exceptions.</span></span> <span data-ttu-id="3a64f-325">依赖于进行计算机 CAS 策略的大量修改的部分信任应用程序也可能会失败，且安全异常。</span><span class="sxs-lookup"><span data-stu-id="3a64f-325">Partial-trust applications that rely on extensive modifications to machine CAS policy might also fail with security exceptions.</span></span>

<span data-ttu-id="3a64f-326">可以还原部分信任 ASP.NET 4 应用程序的行为的 ASP.NET 1.1 和 2.0 版使用新**legacyCasModel**属性中**信任**配置元素，如下面的示例中所示:</span><span class="sxs-lookup"><span data-stu-id="3a64f-326">You can revert partial-trust ASP.NET 4 applications to the behavior of ASP.NET 1.1 and 2.0 using the new **legacyCasModel** attribute in the **trust** configuration element, as shown in the following example:</span></span>

`<trust level= "Medium" legacyCasModel="true" />`

<span data-ttu-id="3a64f-327">时还原到旧的 CAS 模型时，会启用以下旧 CA 行为：</span><span class="sxs-lookup"><span data-stu-id="3a64f-327">When you revert to the legacy CAS model, the following old CAS behaviors are enabled:</span></span>

- <span data-ttu-id="3a64f-328">遵循计算机 CAS 策略。</span><span class="sxs-lookup"><span data-stu-id="3a64f-328">Machine CAS policy is honored.</span></span>
- <span data-ttu-id="3a64f-329">允许在单个应用程序域中的多个不同的权限集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-329">Multiple different permission sets in a single application domain are allowed.</span></span>
- <span data-ttu-id="3a64f-330">显式权限断言不需要的 GAC 中程序集，只有 ASP.NET 或其他.NET Framework 代码位于堆栈上时调用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-330">Explicit permission assertions are not required for assemblies in the GAC that are invoked when only ASP.NET or other .NET Framework code is on the stack.</span></span>

<span data-ttu-id="3a64f-331">不能在.NET Framework 4 中还原一个方案： 非 Web 部分信任应用程序可以不再调用 System.Web.dll 和 System.Web.Extensions.dll 中的某些 Api。</span><span class="sxs-lookup"><span data-stu-id="3a64f-331">One scenario cannot be reverted in the .NET Framework 4: non-Web partial-trust applications can no longer call certain APIs in System.Web.dll and System.Web.Extensions.dll.</span></span> <span data-ttu-id="3a64f-332">在以前版本的.NET Framework 中，有可能使非 Web 部分信任应用程序要对其显式授予<strong>AspNetHostingPermission</strong>权限。</span><span class="sxs-lookup"><span data-stu-id="3a64f-332">In previous versions of the .NET Framework, it was possible for non-Web partial-trust applications to be explicitly granted <strong>AspNetHostingPermission</strong> permissions.</span></span> <span data-ttu-id="3a64f-333">然后可以使用这些应用程序<strong>System.Web.HttpUtility</strong>，键入<strong>System.Web.ClientServices。\</ s > \* 命名空间和类型与成员资格、 角色和配置文件。</span><span class="sxs-lookup"><span data-stu-id="3a64f-333">These applications could then use <strong>System.Web.HttpUtility</strong>, types in the <strong>System.Web.ClientServices.\</strong>\* namespaces, and types related to membership, roles, and profiles.</span></span> <span data-ttu-id="3a64f-334">在.NET Framework 4 中不再支持从非 Web 部分信任应用程序中调用这些类型。</span><span class="sxs-lookup"><span data-stu-id="3a64f-334">Calling these types from non-Web partial trust applications is no longer supported in the .NET Framework 4.</span></span>

> [!NOTE]
> <span data-ttu-id="3a64f-335">**HtmlEncode**并**HtmlDecode**的功能**System.Web.HttpUtility**类已移至新的.NET Framework 4 **System.Net.WebUtility**类。</span><span class="sxs-lookup"><span data-stu-id="3a64f-335">The **HtmlEncode** and **HtmlDecode** functionality of the **System.Web.HttpUtility** class was moved to the new .NET Framework 4 **System.Net.WebUtility** class.</span></span> <span data-ttu-id="3a64f-336">如果这是唯一使用的 ASP.NET 功能，应用程序的代码修改为使用新**WebUtility**类。</span><span class="sxs-lookup"><span data-stu-id="3a64f-336">If that was the only ASP.NET functionality that was being used, modify the application's code to use the new **WebUtility** class instead.</span></span>


<span data-ttu-id="3a64f-337">下面是对 ASP.NET 4 中的默认 CAS 实现的更改的高级摘要：</span><span class="sxs-lookup"><span data-stu-id="3a64f-337">The following is a high-level summary of the changes to the default CAS implementation in ASP.NET 4:</span></span>

- <span data-ttu-id="3a64f-338">ASP.NET 应用程序域现在是同构应用程序域。</span><span class="sxs-lookup"><span data-stu-id="3a64f-338">ASP.NET application domains are now homogeneous application domains.</span></span> <span data-ttu-id="3a64f-339">应用程序域中提供了仅部分信任和完全信任的授予集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-339">Only partial-trust and full-trust grant sets are available in an application domain.</span></span>
- <span data-ttu-id="3a64f-340">ASP.NET 部分信任的授予集是独立于任何企业级、 计算机级别或用户级 CAS 策略。</span><span class="sxs-lookup"><span data-stu-id="3a64f-340">ASP.NET partial-trust grant sets are independent from any enterprise-level, machine-level, or user-level CAS policy.</span></span>
- <span data-ttu-id="3a64f-341">ASP.NET 3.5 和 3.5 SP1 中提供的程序集已转换为使用.NET Framework 4 的透明度模型。</span><span class="sxs-lookup"><span data-stu-id="3a64f-341">ASP.NET assemblies that shipped in 3.5 and 3.5 SP1 have been converted to use the .NET Framework 4 transparency model.</span></span>
- <span data-ttu-id="3a64f-342">使用 ASP.NET **AspNetHostingPermission**大大减少了属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-342">Use of the ASP.NET **AspNetHostingPermission** attribute has been substantially reduced.</span></span> <span data-ttu-id="3a64f-343">已从公共 ASP.NET Api 中删除此属性的大多数实例。</span><span class="sxs-lookup"><span data-stu-id="3a64f-343">Most instances of this attribute have been removed from the public ASP.NET APIs.</span></span>
- <span data-ttu-id="3a64f-344">动态编译的程序集创建的 ASP.NET 生成提供程序已更新，以显式标记为透明的程序集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-344">Dynamically compiled assemblies that are created by ASP.NET build providers have been updated to explicitly mark assemblies as transparent.</span></span>
- <span data-ttu-id="3a64f-345">ASP.NET 的所有程序集现已标记 APTCA 特性可仅在 Web 托管环境的方式。</span><span class="sxs-lookup"><span data-stu-id="3a64f-345">All ASP.NET assemblies are now marked in such a way that the APTCA attribute is honored only in Web hosting environments.</span></span> <span data-ttu-id="3a64f-346">ClickOnce 等部分受信任的非 Web 宿主环境不能以调入 ASP.NET 程序集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-346">Partially trusted non-Web hosting environments like ClickOnce will not be able to call into ASP.NET assemblies.</span></span>

<span data-ttu-id="3a64f-347">有关新的 ASP.NET 4 代码访问安全性模型的详细信息，请参阅[在 ASP.NET 应用程序中使用代码访问安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="3a64f-347">For more information about the new ASP.NET 4 code access security model, see [Using Code Access Security in ASP.NET Applications](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) on the MSDN Web site.</span></span>

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a><span data-ttu-id="3a64f-348">在移动 MembershipUser 和 System.Web.Security Namespace 中的其他类型</span><span class="sxs-lookup"><span data-stu-id="3a64f-348">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>

<span data-ttu-id="3a64f-349">在 ASP.NET 成员资格中使用某些类型已从`System.Web.dll`对新 System.Web.ApplicationServices.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-349">Some types that are used in ASP.NET membership have been moved from `System.Web.dll` to the new System.Web.ApplicationServices.dll assembly.</span></span> <span data-ttu-id="3a64f-350">移动这些类型是为了解析客户端中的类型与扩展的 .NET Framework SKU 中的类型之间的体系结构层依赖关系。</span><span class="sxs-lookup"><span data-stu-id="3a64f-350">The types were moved in order to resolve architectural layering dependencies between types in the client and in extended .NET Framework SKUs.</span></span>

<span data-ttu-id="3a64f-351">网站项目没有因移动这些类型，而问题，因为 System.Web.ApplicationServices.dll 由 ASP.NET 编译系统添加到默认情况下使用的引用的程序集列表。</span><span class="sxs-lookup"><span data-stu-id="3a64f-351">Web site projects do not have problems as a result of moving these types, because System.Web.ApplicationServices.dll was added to the list of referenced assemblies that is used by default by the ASP.NET compilation system.</span></span> <span data-ttu-id="3a64f-352">如果升级通过在 Visual Studio 2010 中打开使用早期版本的 ASP.NET 到 ASP.NET 4 创建的网站项目，项目将编译错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-352">If you upgrade a Web site project that was created using an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the project will compile without errors.</span></span>

<span data-ttu-id="3a64f-353">同样，如果升级已在早期版本的 ASP.NET 到 ASP.NET 4 中通过在 Visual Studio 2010 中打开一个 Web 应用程序项目，升级过程将向项目添加对 System.Web.ApplicationServices.dll 的引用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-353">Similarly, if you upgrade a Web application project that was created in an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the upgrade process adds a reference to System.Web.ApplicationServices.dll to the project.</span></span> <span data-ttu-id="3a64f-354">因此，升级的 Web 应用程序项目也将编译未出现错误。</span><span class="sxs-lookup"><span data-stu-id="3a64f-354">Therefore, upgraded Web application projects will also compile without errors.</span></span>

<span data-ttu-id="3a64f-355">使用 ASP.NET 的早期版本创建的已编译 （二进制） 文件也将不包含错误在运行 ASP.NET 4 中，即使成员身份类型移到不同的程序集。</span><span class="sxs-lookup"><span data-stu-id="3a64f-355">Compiled (binary) files that were created using earlier versions of ASP.NET will also run without errors on ASP.NET 4, even though the membership types were moved to a different assembly.</span></span> <span data-ttu-id="3a64f-356">类型转发的信息已添加到 ASP.NET 4 版的`System.Web.dll`，会自动将这些类型的运行时引用路由到新位置的类型。</span><span class="sxs-lookup"><span data-stu-id="3a64f-356">Type forwarding information has been added to the ASP.NET 4 version of `System.Web.dll` that automatically routes run-time references for these types to the new location for the types.</span></span>

<span data-ttu-id="3a64f-357">但是，使用特定的成员身份类型和已从早期版本的 ASP.NET 中升级的类库将无法进行编译时在 ASP.NET 4 项目中使用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-357">However, class libraries that use specific membership types and that have been upgraded from earlier versions of ASP.NET will fail to compile when used in an ASP.NET 4 project.</span></span> <span data-ttu-id="3a64f-358">例如，一个类库项目可能无法编译并报告错误如下所示：</span><span class="sxs-lookup"><span data-stu-id="3a64f-358">For example, a class library project might fail to compile and report an error such as the following:</span></span>

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
  

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

<span data-ttu-id="3a64f-359">可以通过添加引用你的类库项目中对 System.Web.ApplicationServices.dll 来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="3a64f-359">You can work around this problem by adding a reference in your class library project to System.Web.ApplicationServices.dll.</span></span>

<span data-ttu-id="3a64f-360">以下列表显示*System.Web.Security*类型已从移动`System.Web.dll`对 System.Web.ApplicationServices.dll:</span><span class="sxs-lookup"><span data-stu-id="3a64f-360">The following list shows the *System.Web.Security* types that were moved from `System.Web.dll` to System.Web.ApplicationServices.dll:</span></span>

- <span data-ttu-id="3a64f-361">*System.Web.Security.MembershipCreateStatus*</span><span class="sxs-lookup"><span data-stu-id="3a64f-361">*System.Web.Security.MembershipCreateStatus*</span></span>
- <span data-ttu-id="3a64f-362">*System.Web.Security.Membership.CreateUserException*</span><span class="sxs-lookup"><span data-stu-id="3a64f-362">*System.Web.Security.Membership.CreateUserException*</span></span>
- <span data-ttu-id="3a64f-363">*System.Web.Security.MembershipPasswordException*</span><span class="sxs-lookup"><span data-stu-id="3a64f-363">*System.Web.Security.MembershipPasswordException*</span></span>
- <span data-ttu-id="3a64f-364">*System.Web.Security.MembershipPasswordFormat*</span><span class="sxs-lookup"><span data-stu-id="3a64f-364">*System.Web.Security.MembershipPasswordFormat*</span></span>
- <span data-ttu-id="3a64f-365">*System.Web.Security.MembershipProvider*</span><span class="sxs-lookup"><span data-stu-id="3a64f-365">*System.Web.Security.MembershipProvider*</span></span>
- <span data-ttu-id="3a64f-366">*System.Web.Security.MembershipProviderCollection*</span><span class="sxs-lookup"><span data-stu-id="3a64f-366">*System.Web.Security.MembershipProviderCollection*</span></span>
- <span data-ttu-id="3a64f-367">*System.Web.Security.MembershipUser*</span><span class="sxs-lookup"><span data-stu-id="3a64f-367">*System.Web.Security.MembershipUser*</span></span>
- <span data-ttu-id="3a64f-368">*System.Web.Security.MembershipUserCollection*</span><span class="sxs-lookup"><span data-stu-id="3a64f-368">*System.Web.Security.MembershipUserCollection*</span></span>
- <span data-ttu-id="3a64f-369">*System.Web.Security.MembershipValidatePasswordEventHandler*</span><span class="sxs-lookup"><span data-stu-id="3a64f-369">*System.Web.Security.MembershipValidatePasswordEventHandler*</span></span>
- <span data-ttu-id="3a64f-370">*System.Web.Security.ValidatePasswordEventArgs*</span><span class="sxs-lookup"><span data-stu-id="3a64f-370">*System.Web.Security.ValidatePasswordEventArgs*</span></span>
- <span data-ttu-id="3a64f-371">*System.Web.Security.RoleProvider*</span><span class="sxs-lookup"><span data-stu-id="3a64f-371">*System.Web.Security.RoleProvider*</span></span>
- <a id="0.1_a"></a><span data-ttu-id="3a64f-372">*System.Web.Configuration.MembershipPasswordCompatibilityMode*</span><span class="sxs-lookup"><span data-stu-id="3a64f-372">*System.Web.Configuration.MembershipPasswordCompatibilityMode*</span></span>

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a><span data-ttu-id="3a64f-373">输出缓存发生更改以改变\*HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="3a64f-373">Output Caching Changes to Vary \* HTTP Header</span></span>

<span data-ttu-id="3a64f-374">在 ASP.NET 1.0 中，bug 会导致缓存指定的页面`Location="ServerAndClient"`作为输出 – 缓存设置，以便发出`Vary:*`在响应中的 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="3a64f-374">In ASP.NET 1.0, a bug caused cached pages that specified `Location="ServerAndClient"` as an output–cache setting to emit a `Vary:*` HTTP header in the response.</span></span> <span data-ttu-id="3a64f-375">这还能起到告知客户端浏览器绝不要本地对页进行缓存的作用。</span><span class="sxs-lookup"><span data-stu-id="3a64f-375">This had the effect of telling client browsers to never cache the page locally.</span></span>

<span data-ttu-id="3a64f-376">在 ASP.NET 1.1 **System.Web.HttpCachePolicy.SetOmitVaryStar**方法的调用，禁止显示时无法调用`Vary:*`标头。</span><span class="sxs-lookup"><span data-stu-id="3a64f-376">In ASP.NET 1.1, the **System.Web.HttpCachePolicy.SetOmitVaryStar** method was added, which you could call to suppress the `Vary:*` header.</span></span> <span data-ttu-id="3a64f-377">选择此方法是因为更改发出的 HTTP 标头被视为可能影响重大的更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-377">This method was chosen because changing the emitted HTTP header was considered a potentially breaking change at the time.</span></span> <span data-ttu-id="3a64f-378">但是，开发人员感到困惑的行为在 ASP.NET 中，并且 bug 报告表明开发人员不了解现有**SetOmitVaryStar**行为。</span><span class="sxs-lookup"><span data-stu-id="3a64f-378">However, developers have been confused by the behavior in ASP.NET, and bug reports suggest that developers are unaware of the existing **SetOmitVaryStar** behavior.</span></span>

<span data-ttu-id="3a64f-379">在 ASP.NET 4 中，已做出的决定修复根本问题。</span><span class="sxs-lookup"><span data-stu-id="3a64f-379">In ASP.NET 4, the decision was made to fix the root problem.</span></span> <span data-ttu-id="3a64f-380">`Vary:*` HTTP 标头，将不再发出从指定以下指令的响应：</span><span class="sxs-lookup"><span data-stu-id="3a64f-380">The `Vary:*` HTTP header is no longer emitted from responses that specify the following directive:</span></span>

`<%@OutputCache Location="ServerAndClient" %>`

<span data-ttu-id="3a64f-381">因此， **SetOmitVaryStar**不再需要即可禁止显示`Vary:*`标头。</span><span class="sxs-lookup"><span data-stu-id="3a64f-381">As a result, **SetOmitVaryStar** is no longer needed in order to suppress the `Vary:*` header.</span></span>

<span data-ttu-id="3a64f-382">在指定的应用程序中`Location="ServerAndClient"`中 **@ OutputCache**指令在页面上，则你将看到的名称所暗示的行为**位置**属性的值-即，对页进行缓存可调用而无需在浏览器中缓存**SetOmitVaryStar**方法。</span><span class="sxs-lookup"><span data-stu-id="3a64f-382">In applications that specify `Location="ServerAndClient"` in the **@ OutputCache** directive on a page, you will now see the behavior implied by the name of the **Location** attribute's value – that is, pages will be cacheable in the browser without requiring that you call the **SetOmitVaryStar** method.</span></span>

<span data-ttu-id="3a64f-383">如果你的应用程序中的页必须发出`Vary:*`，调用**AppendHeader**方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3a64f-383">If pages in your application must emit `Vary:*`, call the **AppendHeader** method, as in the following example:</span></span>

`HttpResponse.AppendHeader("Vary","*");`

<span data-ttu-id="3a64f-384">或者，可以更改输出缓存的值**位置**属性为"Server"。</span><span class="sxs-lookup"><span data-stu-id="3a64f-384">Alternatively, you can change the value of the output caching **Location** attribute to "Server".</span></span>

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a><span data-ttu-id="3a64f-385">Passport System.Web.Security 类型可以是已过时</span><span class="sxs-lookup"><span data-stu-id="3a64f-385">System.Web.Security Types for Passport are Obsolete</span></span>

<span data-ttu-id="3a64f-386">ASP.NET 2.0 中内置的 Passport 支持已过时和不支持几年由于 Passport (现在 LiveID) 中进行了更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-386">The Passport support built into ASP.NET 2.0 has been obsolete and unsupported for a few years due to changes in Passport (now LiveID).</span></span> <span data-ttu-id="3a64f-387">五种类型中与 Passport 相关的结果， **System.Web.Security**现在被标记为与**ObsoleteAttribute**属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-387">As a result, the five types related to Passport in **System.Web.Security** are now marked with the **ObsoleteAttribute** attribute.</span></span>

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a><span data-ttu-id="3a64f-388">MenuItem.PopOutImageUrl 属性将无法呈现在 ASP.NET 4 中的图像</span><span class="sxs-lookup"><span data-stu-id="3a64f-388">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>

<span data-ttu-id="3a64f-389">在 ASP.NET 3.5 中， *MenuItem.PopOutImageUrl*属性，可以指定用于指示菜单项具有动态子菜单的菜单项中显示的图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-389">In ASP.NET 3.5, the *MenuItem.PopOutImageUrl* property lets you specify the URL for an image that is displayed in a menu item to indicate that the menu item has a dynamic submenu.</span></span> <span data-ttu-id="3a64f-390">下面的示例演示如何在 ASP.NET 3.5 中的标记中指定此属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-390">The following example shows how to specify this property in markup in ASP.NET 3.5.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

<span data-ttu-id="3a64f-391">由于 ASP.NET 4 中的设计更改，而不输出为呈现*PopOutImageUrl*如果属性设置为*MenuItem*类。</span><span class="sxs-lookup"><span data-stu-id="3a64f-391">As a result of a design change in ASP.NET 4, no output is rendered for the *PopOutImageUrl* if the property is set for the *MenuItem* class.</span></span> <span data-ttu-id="3a64f-392">相反，您必须指定图像 URL 中直接*菜单*控制使用*StaticPopOutImageUrl*属性或*DynamicPopOutImageUrl*属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-392">Instead, you must specify an image URL directly in the *Menu* control using either the *StaticPopOutImageUrl* property or the *DynamicPopOutImageUrl* property.</span></span> <span data-ttu-id="3a64f-393">在静态菜单中，使用时*Menu.StaticPopOutImageUrl*属性指定显示，以便指示静态菜单项包含子菜单，如下面的示例中所示的图像的 URL:</span><span class="sxs-lookup"><span data-stu-id="3a64f-393">When you work with a static menu, the *Menu.StaticPopOutImageUrl* property specifies the URL for an image that is displayed in order to indicate that the static menu item has a submenu, as shown in the following example:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

<span data-ttu-id="3a64f-394">如果您正在使用动态菜单，则使用*Menu.DynamicPopOutImageUrl*属性来指定，该值指示动态菜单项包含子菜单的图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="3a64f-394">If you are working with a dynamic menu, you use the *Menu.DynamicPopOutImageUrl* property to specify the URL for an image that indicates that a dynamic menu item has a submenu.</span></span> <span data-ttu-id="3a64f-395">下面的示例类似于前一个，但演示了如何设置*DynamicPopOutImageUrl*动态菜单的属性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-395">The following example is similar to the previous one, but shows how to set the *DynamicPopOutImageUrl* property for a dynamic menu.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

<span data-ttu-id="3a64f-396">如果*Menu.DynamicPopOutImageUrl*未设置属性和*Menu.DynamicEnableDefaultPopOutImage*属性设置为*false*，不显示任何图像。</span><span class="sxs-lookup"><span data-stu-id="3a64f-396">If the *Menu.DynamicPopOutImageUrl* property is not set and the *Menu.DynamicEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span> <span data-ttu-id="3a64f-397">同样，如果*StaticPopOutImageUrl*未设置属性和*StaticEnableDefaultPopOutImage*属性设置为*false*，不显示任何图像。</span><span class="sxs-lookup"><span data-stu-id="3a64f-397">Similarly, if the *StaticPopOutImageUrl* property is not set and the *StaticEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span>

<span data-ttu-id="3a64f-398">当设置这些属性的路径时，使用正斜杠 （/） 而不是反斜杠 (\)。</span><span class="sxs-lookup"><span data-stu-id="3a64f-398">When you set the paths for these properties, use a forward slash (/) instead of a backslash (\).</span></span> <span data-ttu-id="3a64f-399">有关详细信息，请参阅[Menu.StaticPopOutImageUrl 和 Menu.DynamicPopOutImageUrl 故障到呈现图像时路径包含反斜杠](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu。")</span><span class="sxs-lookup"><span data-stu-id="3a64f-399">For more information, see [Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu.")</span></span> <span data-ttu-id="3a64f-400">其他位置在本文档中。</span><span class="sxs-lookup"><span data-stu-id="3a64f-400">elsewhere in this document.</span></span>

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a><span data-ttu-id="3a64f-401">Menu.StaticPopOutImageUrl 和 Menu.DynamicPopOutImageUrl 无法呈现图像时路径包含反斜杠</span><span class="sxs-lookup"><span data-stu-id="3a64f-401">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>

<span data-ttu-id="3a64f-402">在 ASP.NET 4 中，使用指定的映像*Menu.StaticPopOutImageUrl*并*Menu.DynamicPopOutImageUrl*属性将不会呈现如果路径包含 backlashes (\)。</span><span class="sxs-lookup"><span data-stu-id="3a64f-402">In ASP.NET 4, the images that you specify using the *Menu.StaticPopOutImageUrl* and *Menu.DynamicPopOutImageUrl* properties will not render if the path contains backlashes (\).</span></span> <span data-ttu-id="3a64f-403">这是从 ASP.NET 的早期版本的更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-403">This is a change from earlier versions of ASP.NET.</span></span>

<span data-ttu-id="3a64f-404">下面的示例对*菜单*控件的标记演示*StaticPopOutImageUrl*属性设置使用的路径包含反斜杠。</span><span class="sxs-lookup"><span data-stu-id="3a64f-404">The following example of *Menu* control markup shows the *StaticPopOutImageUrl* property set using a path that contains a backslash.</span></span> <span data-ttu-id="3a64f-405">在 ASP.NET 4 中，将不会呈现在属性中指定的图像。</span><span class="sxs-lookup"><span data-stu-id="3a64f-405">In ASP.NET 4, the image specified in the property will not render.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

<span data-ttu-id="3a64f-406">若要更正此问题，请更改中指定的路径值*StaticPopOutImageUrl*并*DynamicPopOutImageUrl*属性，以使用正斜杠 （/）。</span><span class="sxs-lookup"><span data-stu-id="3a64f-406">To correct this issue, change path values that are specified in the *StaticPopOutImageUrl* and *DynamicPopOutImageUrl* properties to use forward slashes (/).</span></span> <span data-ttu-id="3a64f-407">下面的示例显示了此更改：</span><span class="sxs-lookup"><span data-stu-id="3a64f-407">The following example shows this change:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

<span data-ttu-id="3a64f-408">请注意从早期版本的 ASP.NET 到 ASP.NET 4 已迁移的应用程序可能还会受到影响，因为*MenuItem.PopOutImageUrl*属性已更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-408">Note that applications that were migrated from earlier versions of ASP.NET to ASP.NET 4 might also be affected, because the *MenuItem.PopOutImageUrl* property has been changed.</span></span> <span data-ttu-id="3a64f-409">有关详细信息，请参阅[MenuItem.PopOutImageUrl 属性将无法呈现 ASP.NET 4 中的映像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert")本文档中的其他位置。</span><span class="sxs-lookup"><span data-stu-id="3a64f-409">For more information, see [The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert") elsewhere in this document.</span></span>

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a><span data-ttu-id="3a64f-410">免责声明</span><span class="sxs-lookup"><span data-stu-id="3a64f-410">Disclaimer</span></span>

<span data-ttu-id="3a64f-411">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="3a64f-411">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="3a64f-412">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="3a64f-412">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="3a64f-413">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="3a64f-413">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="3a64f-414">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="3a64f-414">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="3a64f-415">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="3a64f-415">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="3a64f-416">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="3a64f-416">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="3a64f-417">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="3a64f-417">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="3a64f-418">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="3a64f-418">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="3a64f-419">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="3a64f-419">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="3a64f-420">除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。</span><span class="sxs-lookup"><span data-stu-id="3a64f-420">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="3a64f-421">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="3a64f-421">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="3a64f-422">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="3a64f-422">All rights reserved.</span></span>

<span data-ttu-id="3a64f-423">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="3a64f-423">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="3a64f-424">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="3a64f-424">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
