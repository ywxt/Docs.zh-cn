---
uid: web-pages/overview/releases/top-features-in-web-pages-2
title: ASP.NET Web Pages 2 中功能顶部 |Microsoft Docs
author: microsoft
description: 本主题提供了 ASP.NET Web Pages 2，附带 WebMatr 的轻型 web 编程框架中最新功能的概述...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: cc712e72-c3d0-4e43-bc2d-28cc09cd8f71
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/releases/top-features-in-web-pages-2
msc.type: authoredcontent
ms.openlocfilehash: 3cdb9d83e0f612ad7404bfaa9721b580916e112d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385261"
---
<a name="the-top-features-in-aspnet-web-pages-2"></a><span data-ttu-id="07c56-103">ASP.NET Web Pages 2 中的常用功能</span><span class="sxs-lookup"><span data-stu-id="07c56-103">The Top Features in ASP.NET Web Pages 2</span></span>
====================
<span data-ttu-id="07c56-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="07c56-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="07c56-105">本文提供的热门新功能在 ASP.NET Web Pages 2 RC 中，包含一个轻型 web 编程框架概述[Microsoft WebMatrix 2 RC](https://www.microsoft.com/web/)。</span><span class="sxs-lookup"><span data-stu-id="07c56-105">This article provides an overview of the top new features in the ASP.NET Web Pages 2 RC, a lightweight web programming framework that is included with [Microsoft WebMatrix 2 RC](https://www.microsoft.com/web/).</span></span>
> 
> <span data-ttu-id="07c56-106">**包含的内容：**</span><span class="sxs-lookup"><span data-stu-id="07c56-106">**What's included:**</span></span> 
> 
> - [<span data-ttu-id="07c56-107">安装 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="07c56-107">Installing WebMatrix</span></span>](#install)
> - [<span data-ttu-id="07c56-108">新的和增强功能</span><span class="sxs-lookup"><span data-stu-id="07c56-108">New and enhanced features</span></span>](#New_and_Enhanced_Features)
> 
>     - [<span data-ttu-id="07c56-109">RC 版的更改</span><span class="sxs-lookup"><span data-stu-id="07c56-109">Changes for the RC release</span></span>](#Changes_for_the_RC_Version)
>     - [<span data-ttu-id="07c56-110">Beta 版的更改</span><span class="sxs-lookup"><span data-stu-id="07c56-110">Changes for the Beta release</span></span>](#Changes_for_the_Beta_Version)
>     - [<span data-ttu-id="07c56-111">使用新的和更新站点模板</span><span class="sxs-lookup"><span data-stu-id="07c56-111">Using the New and Updated Site Templates</span></span>](#templates)
>     - [<span data-ttu-id="07c56-112">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="07c56-112">Validating User Input</span></span>](#validation)
>     - [<span data-ttu-id="07c56-113">启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名</span><span class="sxs-lookup"><span data-stu-id="07c56-113">Enabling logins from Facebook and other sites using OAuth and OpenID</span></span>](#oauthsetup)
>     - [<span data-ttu-id="07c56-114">添加映射使用映射帮助器</span><span class="sxs-lookup"><span data-stu-id="07c56-114">Adding Maps using the Maps Helper</span></span>](#maphelper)
>     - [<span data-ttu-id="07c56-115">运行 Web Pages 应用程序并排显示</span><span class="sxs-lookup"><span data-stu-id="07c56-115">Running Web Pages Applications Side by Side</span></span>](#sidebyside)
>     - [<span data-ttu-id="07c56-116">移动设备的呈现页</span><span class="sxs-lookup"><span data-stu-id="07c56-116">Rendering Pages for Mobile Devices</span></span>](#mobile)
> - [<span data-ttu-id="07c56-117">其他资源</span><span class="sxs-lookup"><span data-stu-id="07c56-117">Additional Resources</span></span>](#resources)
> 
> > [!NOTE]
> > <span data-ttu-id="07c56-118">本主题假定使用 WebMatrix 的目的用于 ASP.NET Web Pages 2 代码。</span><span class="sxs-lookup"><span data-stu-id="07c56-118">This topic assumes that you are using WebMatrix to work with your ASP.NET Web Pages 2 code.</span></span> <span data-ttu-id="07c56-119">但是，由于 Web Pages 1，您可以创建使用 Visual Studio 的 Web Pages 2 网站，后者可提供增强的 IntelliSense 功能和调试。</span><span class="sxs-lookup"><span data-stu-id="07c56-119">However, as with Web Pages 1, you can also create Web Pages 2 websites using Visual Studio, which gives you enhanced IntelliSense capabilities and debugging.</span></span> <span data-ttu-id="07c56-120">若要使用 Visual Studio 中的 Web 页，必须首先安装 Visual Studio 2010 SP1、 Visual Web Developer 速成版 2010 SP1 或 Visual Studio 11 Beta。</span><span class="sxs-lookup"><span data-stu-id="07c56-120">To work with Web Pages in Visual Studio, you must first install Visual Studio 2010 SP1, Visual Web Developer Express 2010 SP1, or Visual Studio 11 Beta.</span></span> <span data-ttu-id="07c56-121">然后安装 ASP.NET MVC 4 Beta，其中包括用于 Visual Studio 中创建 ASP.NET MVC 4 和 Web Pages 2 应用程序模板和工具。</span><span class="sxs-lookup"><span data-stu-id="07c56-121">Then install the ASP.NET MVC 4 Beta, which includes templates and tools for creating ASP.NET MVC 4 and Web Pages 2 applications in Visual Studio.</span></span>
> 
> 
> <span data-ttu-id="07c56-122">*上次更新： 2012 年 6 月 18*</span><span class="sxs-lookup"><span data-stu-id="07c56-122">*Last update: 18 June 2012*</span></span>


<a id="install"></a>
## <a name="installing-webmatrix"></a><span data-ttu-id="07c56-123">安装 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="07c56-123">Installing WebMatrix</span></span>

<span data-ttu-id="07c56-124">若要安装 Web 页，可以使用 Microsoft Web 平台安装程序，它是免费的应用程序，它可以更轻松地安装和配置与 web 相关技术。</span><span class="sxs-lookup"><span data-stu-id="07c56-124">To install Web Pages, you can use the Microsoft Web Platform Installer, which is a free application that makes it easy to install and configure web-related technologies.</span></span> <span data-ttu-id="07c56-125">将安装 WebMatrix 2 试用版，包括 Web Pages 2 Beta。</span><span class="sxs-lookup"><span data-stu-id="07c56-125">You will install the WebMatrix 2 Beta, which includes Web Pages 2 Beta.</span></span>

1. <span data-ttu-id="07c56-126">浏览到 Web 平台安装程序的最新版本的安装页面：</span><span class="sxs-lookup"><span data-stu-id="07c56-126">Browse to the installation page for the latest version of the Web Platform Installer:</span></span>

    [https://go.microsoft.com/fwlink/?LinkId=226883](https://go.microsoft.com/fwlink/?LinkId=226883)

    > [!NOTE]
    > <span data-ttu-id="07c56-127">如果已安装 WebMatrix 1，此安装会更新它为 WebMatrix 2 beta 版本。</span><span class="sxs-lookup"><span data-stu-id="07c56-127">If you already have WebMatrix 1 installed, this installation updates it to WebMatrix 2 Beta.</span></span> <span data-ttu-id="07c56-128">你可以运行在同一台计算机上使用 1 或 2 的版本创建的网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-128">You can run websites that were created using version 1 or 2 on the same computer.</span></span> <span data-ttu-id="07c56-129">详细信息，请参阅部分上[运行网页的应用程序并排](#sidebyside)。</span><span class="sxs-lookup"><span data-stu-id="07c56-129">For more information, see the section on [Running Web Pages Applications Side by Side](#sidebyside).</span></span>
2. <span data-ttu-id="07c56-130">选择**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="07c56-130">Choose **Install Now**.</span></span> 

    <span data-ttu-id="07c56-131">如果你使用 Internet Explorer，请转到下一步。</span><span class="sxs-lookup"><span data-stu-id="07c56-131">If you use Internet Explorer, go to the next step.</span></span> <span data-ttu-id="07c56-132">如果使用 Mozilla Firefox 或 Google Chrome 等不同的浏览器，系统会提示保存*Webmatrix.exe*到您的计算机的文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-132">If you use a different browser like Mozilla Firefox or Google Chrome, you are prompted to save the *Webmatrix.exe* file to your computer.</span></span> <span data-ttu-id="07c56-133">保存该文件，然后单击它以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-133">Save the file and then click it to launch the installer.</span></span>
3. <span data-ttu-id="07c56-134">运行安装程序，然后选择**安装**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-134">Run the installer and choose the **Install** button.</span></span> <span data-ttu-id="07c56-135">这会安装 WebMatrix 和 Web Pages。</span><span class="sxs-lookup"><span data-stu-id="07c56-135">This installs WebMatrix and Web Pages.</span></span>

## <a id="New_and_Enhanced_Features"></a>  <span data-ttu-id="07c56-136">新的和增强功能</span><span class="sxs-lookup"><span data-stu-id="07c56-136">New and Enhanced Features</span></span>

### <a id="Changes_for_the_RC_Version"></a>  <span data-ttu-id="07c56-137">预发布版本 (2012 年 6 月) 的更改</span><span class="sxs-lookup"><span data-stu-id="07c56-137">Changes for the RC Version (June 2012)</span></span>

<span data-ttu-id="07c56-138">2012 年 6 月中的 RC 版本发行已从已于 2012 年 3 月发布 Beta 版本刷新了一些更改。</span><span class="sxs-lookup"><span data-stu-id="07c56-138">The RC version release in June 2012 has a few changes from the Beta version refresh that was released in March 2012.</span></span> <span data-ttu-id="07c56-139">这些更改是：</span><span class="sxs-lookup"><span data-stu-id="07c56-139">These changes are:</span></span>

- <span data-ttu-id="07c56-140">一个`Validation.AddFormError`方法已添加到`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="07c56-140">A `Validation.AddFormError` method was added to the `Validation` helper.</span></span> <span data-ttu-id="07c56-141">如果手动执行验证将非常有用 （例如，验证查询字符串中传递一个值） 和你想要添加可显示的错误消息`Html.ValidationSummary`方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-141">This is useful if you perform validation manually (for example, you validate a value that is passed in the query string) and you want to add an error message that can be displayed by the `Html.ValidationSummary` method.</span></span> <span data-ttu-id="07c56-142">有关详细信息，请参阅明[验证数据，不会直接从用户](https://go.microsoft.com/fwlink/?LinkId=253002#Validating_Data_That_Doesnt_Come_Directly_from_Users)中[ASP.NET Web Pages (Razor) 站点中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)。</span><span class="sxs-lookup"><span data-stu-id="07c56-142">For more information, see the section [Validating Data That Doesn't Come Directly From Users](https://go.microsoft.com/fwlink/?LinkId=253002#Validating_Data_That_Doesnt_Come_Directly_from_Users) in [Validating User Input in ASP.NET Web Pages (Razor) Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span>
- <span data-ttu-id="07c56-143">已从核心 ASP.NET Web Pages 2 程序集删除了捆绑和缩小功能。</span><span class="sxs-lookup"><span data-stu-id="07c56-143">The functionality for bundling and minification has been removed from the core ASP.NET Web Pages 2 assemblies.</span></span> <span data-ttu-id="07c56-144">因此，`Assets`本文档后面列出的帮助器不可用。</span><span class="sxs-lookup"><span data-stu-id="07c56-144">As a consequence, the `Assets` helper listed later in this document is not available.</span></span> <span data-ttu-id="07c56-145">相反，必须安装[ASP.NET 优化](http://nuget.org/packages/Microsoft.Web.Optimization/0.1)NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="07c56-145">Instead, you must install the [ASP.NET Optimization](http://nuget.org/packages/Microsoft.Web.Optimization/0.1) NuGet package.</span></span> <span data-ttu-id="07c56-146">有关详细信息，请参阅[捆绑和缩小资产中的 ASP.NET Web Pages (Razor) 站点](https://go.microsoft.com/fwlink/?LinkId=255373)。</span><span class="sxs-lookup"><span data-stu-id="07c56-146">For more information, see [Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkId=255373).</span></span>
- <span data-ttu-id="07c56-147">添加了其他程序集以支持 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="07c56-147">Additional assemblies to support ASP.NET Web Pages 2 have been added.</span></span> <span data-ttu-id="07c56-148">此更改仅明显影响是，您可能看到的站点中的多个程序集*bin*文件夹后创建一个站点或将站点部署到托管提供商。</span><span class="sxs-lookup"><span data-stu-id="07c56-148">The only noticeable effect of this change is that you might see more assemblies in a site's *bin* folder after you create a site or deploy a site to a hosting provider.</span></span>

<a id="Changes_for_the_Beta_Version"></a>
### <a name="changes-for-the-beta-version-february-2012"></a><span data-ttu-id="07c56-149">测试版 (2012 年 2 月) 的更改</span><span class="sxs-lookup"><span data-stu-id="07c56-149">Changes for the Beta Version (February 2012)</span></span>

<span data-ttu-id="07c56-150">在 2012 年 2 月发布的测试版有一些更改仅从已于 2011 年 12 月发布 Beta 版本。</span><span class="sxs-lookup"><span data-stu-id="07c56-150">The Beta version released in February 2012 has only a few changes from the Beta version that was released in December 2011.</span></span> <span data-ttu-id="07c56-151">这些更改是：</span><span class="sxs-lookup"><span data-stu-id="07c56-151">These changes are:</span></span>

- <span data-ttu-id="07c56-152">Razor 现在支持条件属性。</span><span class="sxs-lookup"><span data-stu-id="07c56-152">Razor now supports conditional attributes.</span></span> <span data-ttu-id="07c56-153">在 HTML 元素，如果您将属性设置为一个值，解析到的服务器代码中`false`或`null`，ASP.NET 根本不会使该属性。</span><span class="sxs-lookup"><span data-stu-id="07c56-153">In an HTML element, if you set an attribute to a value that resolves in server code to `false` or `null`, ASP.NET does not render the attribute at all.</span></span> <span data-ttu-id="07c56-154">例如，假设您有一个复选框的以下标记：</span><span class="sxs-lookup"><span data-stu-id="07c56-154">For example, imagine you have the following markup for a check box:</span></span>

    [!code-html[Main](top-features-in-web-pages-2/samples/sample1.html)]

    <span data-ttu-id="07c56-155">如果的值`checked1`解析为`false`或设置为`null`，则`checked`属性不呈现。</span><span class="sxs-lookup"><span data-stu-id="07c56-155">If the value of `checked1` resolves to `false` or to `null`, the `checked` attribute is not rendered.</span></span> <span data-ttu-id="07c56-156">这是一项重大更改。</span><span class="sxs-lookup"><span data-stu-id="07c56-156">This is a breaking change.</span></span>
- <span data-ttu-id="07c56-157">`Validation.GetHtml`方法已重命名为`Validation.For`。</span><span class="sxs-lookup"><span data-stu-id="07c56-157">The `Validation.GetHtml` method has been renamed to `Validation.For`.</span></span> <span data-ttu-id="07c56-158">这是一项重大更改;`Validation.GetHtml` Beta 版本中不起。</span><span class="sxs-lookup"><span data-stu-id="07c56-158">This is a breaking change; `Validation.GetHtml` will not work in the Beta release.</span></span>
- <span data-ttu-id="07c56-159">现在可以包括`~`标记中的运算符，而无需使用引用的站点根目录`Href`函数。</span><span class="sxs-lookup"><span data-stu-id="07c56-159">You can now include the `~` operator in markup to reference the site root without using the `Href` function.</span></span> <span data-ttu-id="07c56-160">(即，Razor 分析器可以现在找到并解决`~`而无需显式方法调用运算符`Href`。)`Href`方法仍然正常工作，因此这不是一项重大更改。</span><span class="sxs-lookup"><span data-stu-id="07c56-160">(That is, the Razor parser can now find and resolve the `~` operator without requiring an explicit method call to `Href`.) The `Href` method still works, so this is not a breaking change.</span></span>

    <span data-ttu-id="07c56-161">例如，如果以前进行过标记，如下：</span><span class="sxs-lookup"><span data-stu-id="07c56-161">For example, if you previously had markup like this:</span></span>

    `<a href="@Href("~/Default.cshtml")">Home</a>`

    <span data-ttu-id="07c56-162">现在可以使用标记，如下：</span><span class="sxs-lookup"><span data-stu-id="07c56-162">You can now use markup like this:</span></span>

    `<a href="~/Default.cshtml">Home</a>`
- <span data-ttu-id="07c56-163">`Scripts`资产 （资源） 管理的帮助器替换`Assets`帮助器，具有略有不同的方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="07c56-163">The `Scripts` helper for assets (resource) management has been replaced with the `Assets` helper, which has slightly different methods, such as the following:</span></span>

  - <span data-ttu-id="07c56-164">有关`Scripts.Add`，使用 `Assets.AddScript`</span><span class="sxs-lookup"><span data-stu-id="07c56-164">For `Scripts.Add`, use `Assets.AddScript`</span></span>
  - <span data-ttu-id="07c56-165">有关`Scripts.GetScriptTags`，使用 `Assets.GetScripts`</span><span class="sxs-lookup"><span data-stu-id="07c56-165">For `Scripts.GetScriptTags`, use `Assets.GetScripts`</span></span>

    <span data-ttu-id="07c56-166">这是一项重大更改;`Scripts`类不是在 Beta 版本中可用。</span><span class="sxs-lookup"><span data-stu-id="07c56-166">This is a breaking change; the `Scripts` class is not available in the Beta release.</span></span> <span data-ttu-id="07c56-167">已进行此更改更新本文档中使用资产管理的代码示例。</span><span class="sxs-lookup"><span data-stu-id="07c56-167">The code examples in this document that use asset management have been updated with this change.</span></span>

<a id="templates"></a>
### <a name="using-the-new-and-updated-site-templates"></a><span data-ttu-id="07c56-168">使用新的和更新站点模板</span><span class="sxs-lookup"><span data-stu-id="07c56-168">Using the New and Updated Site Templates</span></span>

<span data-ttu-id="07c56-169">**入门网站**模板已经过更新，以便在 Web Pages 2 上运行默认情况下。</span><span class="sxs-lookup"><span data-stu-id="07c56-169">The **Starter Site** template has been updated so that it runs on Web Pages 2 by default.</span></span> <span data-ttu-id="07c56-170">它还包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="07c56-170">It also includes the following new capabilities:</span></span>

- <span data-ttu-id="07c56-171">适合移动页面呈现。</span><span class="sxs-lookup"><span data-stu-id="07c56-171">Mobile-friendly page rendering.</span></span> <span data-ttu-id="07c56-172">通过使用 CSS 样式并`@media`选择器中，**入门网站**较小的屏幕，其中包括移动设备屏幕上提供改进的页的呈现。</span><span class="sxs-lookup"><span data-stu-id="07c56-172">Through the use of CSS styles and the `@media` selector, the **Starter Site** provides improved rendering of pages on smaller screens, including mobile device screens.</span></span>
- <span data-ttu-id="07c56-173">改进的成员身份和身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="07c56-173">Improved membership and authentication options.</span></span> <span data-ttu-id="07c56-174">您可以让用户登录到您的网站使用其帐户从其他社交网络网站，如 Twitter、 Facebook 和 Windows Live。</span><span class="sxs-lookup"><span data-stu-id="07c56-174">You can let users log into your site using their accounts from other social networking sites, such as Twitter, Facebook, and Windows Live.</span></span> <span data-ttu-id="07c56-175">有关详细信息，请参阅[启用的登录名从 Facebook 和其他站点使用 OAuth 和 OpenID](#oauthsetup)部分。</span><span class="sxs-lookup"><span data-stu-id="07c56-175">For more information, see the [Enabling Logins from Facebook and Other Sites using OAuth and OpenID](#oauthsetup) section.</span></span>
- <span data-ttu-id="07c56-176">HTML5 元素。</span><span class="sxs-lookup"><span data-stu-id="07c56-176">HTML5 elements.</span></span>

<span data-ttu-id="07c56-177">新**个人网站**模板允许您创建包含个人博客、 照片页面和 Twitter 页面的网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-177">The new **Personal Site** template lets you create a website that contains a personal blog, a photos page, and a Twitter page.</span></span> <span data-ttu-id="07c56-178">你可以自定义基于站点**个人网站**模板执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="07c56-178">You can customize a site based on the **Personal Site** template by doing the following:</span></span>

- <span data-ttu-id="07c56-179">通过编辑布局文件来更改网站的外观 (*\_SiteLayout.cshtml*) 和样式文件 (*Site.css*)。</span><span class="sxs-lookup"><span data-stu-id="07c56-179">Change the look of the site by editing the layout file (*\_SiteLayout.cshtml*) and the styles file (*Site.css*).</span></span>
- <span data-ttu-id="07c56-180">将功能添加到你的站点的安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="07c56-180">Install NuGet packages that add functionality to your site.</span></span> <span data-ttu-id="07c56-181">有关如何安装包的信息，包括 ASP.NET Web Helpers Library，请参阅本教程[安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)。</span><span class="sxs-lookup"><span data-stu-id="07c56-181">For information about how to install packages, including the ASP.NET Web Helpers Library, see the tutorial about [installing helpers](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers).</span></span>

<span data-ttu-id="07c56-182">访问**个人网站**模板中，选择**模板**上 WebMatrix**快速启动**屏幕。</span><span class="sxs-lookup"><span data-stu-id="07c56-182">To access the **Personal Site** template, choose **Templates** on the WebMatrix **Quick Start** screen.</span></span>

<span data-ttu-id="07c56-183">[![topseven-personalsite-1](top-features-in-web-pages-2/_static/image2.png)](top-features-in-web-pages-2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-183">[![topseven-personalsite-1](top-features-in-web-pages-2/_static/image2.png)](top-features-in-web-pages-2/_static/image1.png)</span></span>

<span data-ttu-id="07c56-184">在中**模板**对话框框中，选择**个人网站**模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-184">In the **Templates** dialog box, choose the **Personal Site** template.</span></span>

<span data-ttu-id="07c56-185">[![topseven-personalsite-2](top-features-in-web-pages-2/_static/image4.png)](top-features-in-web-pages-2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-185">[![topseven-personalsite-2](top-features-in-web-pages-2/_static/image4.png)](top-features-in-web-pages-2/_static/image3.png)</span></span>

<span data-ttu-id="07c56-186">登陆页**个人网站**模板，可单击的链接可设置您的博客，Twitter 页和照片页。</span><span class="sxs-lookup"><span data-stu-id="07c56-186">The landing page of the **Personal Site** template lets you follow links to set up your blog, Twitter page, and photos page.</span></span>

<span data-ttu-id="07c56-187">[![topseven-personalsite-3](top-features-in-web-pages-2/_static/image6.png)](top-features-in-web-pages-2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-187">[![topseven-personalsite-3](top-features-in-web-pages-2/_static/image6.png)](top-features-in-web-pages-2/_static/image5.png)</span></span>

<a id="validation"></a>
### <a name="validating-user-input"></a><span data-ttu-id="07c56-188">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="07c56-188">Validating User Input</span></span>

<span data-ttu-id="07c56-189">在 Web Pages 1 来验证用户输入提交窗体，您使用`System.Web.WebPages.Html.ModelState`类。</span><span class="sxs-lookup"><span data-stu-id="07c56-189">In Web Pages 1, to validate user input on submitted forms, you use the `System.Web.WebPages.Html.ModelState` class.</span></span> <span data-ttu-id="07c56-190">(这中所示的代码示例的几个 Web Pages 1 在本教程中标题为[使用数据](../data/5-working-with-data.md)。)仍可以在 Web Pages 2 中使用此方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-190">(This is illustrated in several of the code samples in the Web Pages 1 tutorial titled [Working with Data](../data/5-working-with-data.md).) You can still use this approach in Web Pages 2.</span></span> <span data-ttu-id="07c56-191">但是，Web Pages 2 还提供了改进的工具，用于验证用户输入：</span><span class="sxs-lookup"><span data-stu-id="07c56-191">However, Web Pages 2 also offers improved tools for validating user input:</span></span>

- <span data-ttu-id="07c56-192">新的验证类，包括`System.Web.WebPages.ValidationHelper`和`System.Web.WebPages.Validator`，能够让你执行几行代码的功能强大的验证任务。</span><span class="sxs-lookup"><span data-stu-id="07c56-192">New validation classes, including `System.Web.WebPages.ValidationHelper` and `System.Web.WebPages.Validator`, that let you do powerful validation tasks with a few lines of code.</span></span>
- <span data-ttu-id="07c56-193">（可选） 客户端验证，提供即时的反馈而不是请求到服务器的往返行程用户检查验证错误。</span><span class="sxs-lookup"><span data-stu-id="07c56-193">Optionally, client-side validation, which provides immediate feedback to the user instead of requiring a round trip to the server to check for validation errors.</span></span> <span data-ttu-id="07c56-194">（出于安全原因，验证在服务器上，即使事先已在客户端中执行的检查。）</span><span class="sxs-lookup"><span data-stu-id="07c56-194">(For security reasons, validation is performed on the server even if the checks have been performed in the client beforehand.)</span></span>

<span data-ttu-id="07c56-195">若要使用新的验证功能，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="07c56-195">To use the new validation features, do the following:</span></span>

<span data-ttu-id="07c56-196">在页面的代码中，注册要使用的方法验证元素`Validation`帮助程序： `Validation.RequireField`， `Validation.RequireFields` （若要注册多个元素为必需），或`Validation.Add`。</span><span class="sxs-lookup"><span data-stu-id="07c56-196">In the page's code, register an element to be validated by using methods of the `Validation` helper: `Validation.RequireField`, `Validation.RequireFields` (to register multiple elements to be required), or `Validation.Add`.</span></span> <span data-ttu-id="07c56-197">`Add`方法允许您指定其他类型的验证检查，类似于数据类型检查、 比较不同的字段，字符串长度检查中的条目和模式 （使用正则表达式）。</span><span class="sxs-lookup"><span data-stu-id="07c56-197">The `Add` method lets you specify other types of validation checks, like data-type checking, comparing entries in different fields, string-length checks, and patterns (using regular expressions).</span></span> <span data-ttu-id="07c56-198">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="07c56-198">Here are some examples:</span></span>

[!code-html[Main](top-features-in-web-pages-2/samples/sample2.html)]

<span data-ttu-id="07c56-199">若要显示特定于字段的错误，请调用`Html.ValidationMessage`正在验证每个元素的标记中：</span><span class="sxs-lookup"><span data-stu-id="07c56-199">To display a field-specific error, call `Html.ValidationMessage` in the markup for each element being validated:</span></span>

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample3.cshtml)]

<span data-ttu-id="07c56-200">若要显示的摘要 (`<ul>`列表) 在页中，所有错误的`Html.ValidationSummary`标记中：</span><span class="sxs-lookup"><span data-stu-id="07c56-200">To display a summary (`<ul>` list) of all the errors in the page, `Html.ValidationSummary` in the markup:</span></span>

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample4.cshtml)]

<span data-ttu-id="07c56-201">这些步骤，即可实现服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="07c56-201">These steps are enough to implement server-side validation.</span></span> <span data-ttu-id="07c56-202">如果你想要添加客户端验证，请执行以下此外。</span><span class="sxs-lookup"><span data-stu-id="07c56-202">If you want to add client-side validation, do the following in addition.</span></span>

<span data-ttu-id="07c56-203">添加以下脚本文件引用内部`<head>`web 页面的部分。</span><span class="sxs-lookup"><span data-stu-id="07c56-203">Add the following script file references inside the `<head>` section of a web page.</span></span> <span data-ttu-id="07c56-204">前两个脚本引用指向内容交付网络 (CDN) 服务器上的远程文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-204">The first two script references point to remote files on a content delivery network (CDN) server.</span></span> <span data-ttu-id="07c56-205">第三个引用将指向本地脚本文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-205">The third reference points to a local script file.</span></span> <span data-ttu-id="07c56-206">当 CDN 不可用时，生产应用应实现回退。</span><span class="sxs-lookup"><span data-stu-id="07c56-206">Production apps should implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="07c56-207">测试回退。</span><span class="sxs-lookup"><span data-stu-id="07c56-207">Test the fallback.</span></span>

[!code-html[Main](top-features-in-web-pages-2/samples/sample5.html)]

<span data-ttu-id="07c56-208">若要获取的本地副本的最简单方法*jquery.validate.unobtrusive.min.js*库是创建新的 Web Pages 站点基于之一 （如入门网站） 的站点模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-208">The easiest way to get a local copy of the *jquery.validate.unobtrusive.min.js* library is to create a new Web Pages site based on one of the site templates (such as Starter Site).</span></span> <span data-ttu-id="07c56-209">由模板创建该站点包括*jquery.validate.unobtrusive.js*其 Scripts 文件夹中，从中您可以将其复制到你的站点中的文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-209">The site created by the template includes *jquery.validate.unobtrusive.js* file in its Scripts folder, from which you can copy it to your site.</span></span>

<span data-ttu-id="07c56-210">如果你的网站使用<em>\_SiteLayout</em>来控制页面布局页上，可以在该页面中包含这些脚本引用，以便验证可供所有内容页面。</span><span class="sxs-lookup"><span data-stu-id="07c56-210">If your website uses a<em>\_SiteLayout</em> page to control the page layout, you can include these script references in that page so that validation is available to all content pages.</span></span> <span data-ttu-id="07c56-211">如果你想要仅在特定页面上执行验证，您可以使用资产管理器注册仅这些页上的脚本。</span><span class="sxs-lookup"><span data-stu-id="07c56-211">If you want to perform validation only on particular pages, you can use the assets manager to register the scripts on only those pages.</span></span> <span data-ttu-id="07c56-212">若要执行此操作，调用`Assets.AddScript(path)`中你想要验证并引用每个脚本文件的页。</span><span class="sxs-lookup"><span data-stu-id="07c56-212">To do this, call `Assets.AddScript(path)` in the page that you want to validate and reference each of the script files.</span></span> <span data-ttu-id="07c56-213">然后添加对的调用`Assets.GetScripts`中 <em>\_SiteLayout</em>以便呈现的已注册`<script>`标记。</span><span class="sxs-lookup"><span data-stu-id="07c56-213">Then add a call to `Assets.GetScripts` in the <em>\_SiteLayout</em> page in order to render the registered `<script>` tags.</span></span> <span data-ttu-id="07c56-214">有关详细信息，请参阅明[与资产管理器注册脚本](#resmanagement)。</span><span class="sxs-lookup"><span data-stu-id="07c56-214">For more information, see the section [Registering Scripts with the Assets Manager](#resmanagement).</span></span>

<span data-ttu-id="07c56-215">在单个元素的标记，调用`Validation.For`方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-215">In the markup for an individual element, call the `Validation.For` method.</span></span> <span data-ttu-id="07c56-216">此方法发出属性，jQuery 可以挂接以便提供客户端验证。</span><span class="sxs-lookup"><span data-stu-id="07c56-216">This method emits attributes that jQuery can hook in order to provide client-side validation.</span></span> <span data-ttu-id="07c56-217">例如：</span><span class="sxs-lookup"><span data-stu-id="07c56-217">For example:</span></span>

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample6.cshtml)]

<span data-ttu-id="07c56-218">下面的示例显示了页面，用于验证用户输入窗体上。</span><span class="sxs-lookup"><span data-stu-id="07c56-218">The following example shows a page that validates user input on a form.</span></span> <span data-ttu-id="07c56-219">若要运行和测试此验证代码，请执行此操作：</span><span class="sxs-lookup"><span data-stu-id="07c56-219">To run and test this validation code, do this:</span></span>

1. <span data-ttu-id="07c56-220">创建新的 web 站点使用包括 WebMatrix 2 站点模板之一*脚本*文件夹，如**入门网站**模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-220">Create a new web site using one of the WebMatrix 2 site templates that includes a *Scripts* folder, such as the **Starter Site** template.</span></span>
2. <span data-ttu-id="07c56-221">在新站点中，创建一个新 *.cshtml*页和页的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="07c56-221">In the new site, create a new *.cshtml* page, and replace the contents of the page with the following code.</span></span>
3. <span data-ttu-id="07c56-222">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="07c56-222">Run the page in a browser.</span></span> <span data-ttu-id="07c56-223">输入有效和无效值，以查看上验证的效果。</span><span class="sxs-lookup"><span data-stu-id="07c56-223">Enter valid and invalid values to see the effects on validation.</span></span> <span data-ttu-id="07c56-224">例如，将必填的字段保留为空或输入的字母**信用额度**字段。</span><span class="sxs-lookup"><span data-stu-id="07c56-224">For example, leave a required field blank or enter a letter in the **Credits** field.</span></span>


[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample7.cshtml)]

<span data-ttu-id="07c56-225">以下是页，当用户提交有效的输入：</span><span class="sxs-lookup"><span data-stu-id="07c56-225">Here is the page when a user submits valid input:</span></span>

<span data-ttu-id="07c56-226">[![topSeven-valid-1](top-features-in-web-pages-2/_static/image8.png)](top-features-in-web-pages-2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-226">[![topSeven-valid-1](top-features-in-web-pages-2/_static/image8.png)](top-features-in-web-pages-2/_static/image7.png)</span></span>

<span data-ttu-id="07c56-227">当用户提交它与必填字段留空时，以下是页：</span><span class="sxs-lookup"><span data-stu-id="07c56-227">Here is the page when a user submits it with a required field left empty:</span></span>

<span data-ttu-id="07c56-228">[![topSeven-valid-2](top-features-in-web-pages-2/_static/image10.png)](top-features-in-web-pages-2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-228">[![topSeven-valid-2](top-features-in-web-pages-2/_static/image10.png)](top-features-in-web-pages-2/_static/image9.png)</span></span>

<span data-ttu-id="07c56-229">以下是页，当用户提交它内的整数非**信用额度**字段：</span><span class="sxs-lookup"><span data-stu-id="07c56-229">Here is the page when a user submits it with something other than an integer in the **Credits** field:</span></span>

<span data-ttu-id="07c56-230">[![topSeven-valid-3](top-features-in-web-pages-2/_static/image12.png)](top-features-in-web-pages-2/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-230">[![topSeven-valid-3](top-features-in-web-pages-2/_static/image12.png)](top-features-in-web-pages-2/_static/image11.png)</span></span>

<span data-ttu-id="07c56-231">有关详细信息，请参阅以下博客文章：</span><span class="sxs-lookup"><span data-stu-id="07c56-231">For more information, see the following blog posts:</span></span>

- <span data-ttu-id="07c56-232">[更新 Web Pages v2 中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2344)添加验证使用的基础知识`Validation`帮助程序 （仅服务器端）</span><span class="sxs-lookup"><span data-stu-id="07c56-232">[Updated validation in Web Pages v2](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2344) Basics of adding validation using the `Validation` helper (server-side only)</span></span>
- <span data-ttu-id="07c56-233">[更新 Web Pages v2，第 2 部分中的验证](http://www.mikepope.com/blog/DisplayBlog.aspx?permalink=2347)添加客户端验证。</span><span class="sxs-lookup"><span data-stu-id="07c56-233">[Updated validation in Web Pages v2, Part 2](http://www.mikepope.com/blog/DisplayBlog.aspx?permalink=2347) Adding client-side validation.</span></span>
- <span data-ttu-id="07c56-234">[更新 Web Pages v2，第 3 部分中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2351)格式设置验证错误。</span><span class="sxs-lookup"><span data-stu-id="07c56-234">[Updated validation in Web Pages v2, Part 3](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2351) Formatting validation errors.</span></span>

<a id="resmanagement"></a>
### <a name="registering-scripts-using-the-assets-manager"></a><span data-ttu-id="07c56-235">注册脚本使用资产管理器</span><span class="sxs-lookup"><span data-stu-id="07c56-235">Registering Scripts Using the Assets Manager</span></span>

<span data-ttu-id="07c56-236">资产管理器是一项新功能，可以使用在服务器代码中进行注册和呈现客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="07c56-236">The assets manager is a new feature that you can use in server code to register and render client scripts.</span></span> <span data-ttu-id="07c56-237">使用在运行时组合到一个页面的多个文件 （如布局页中，内容页面、 帮助程序，等等） 中的代码时，此功能很有用。</span><span class="sxs-lookup"><span data-stu-id="07c56-237">This feature is helpful when you are working with code from multiple files (such as layout pages, content pages, helpers, etc.) that are combined into a single page at run time.</span></span> <span data-ttu-id="07c56-238">资产管理器协调源代码文件，以确保正确引用脚本文件和有效地在呈现的页上，而不考虑哪些代码文件从调用的或者它们被称为多少次。</span><span class="sxs-lookup"><span data-stu-id="07c56-238">The assets manager coordinates the source files to make sure that script files are referenced correctly and efficiently on the rendered page, regardless of which code files they are called from or how many times they are called.</span></span> <span data-ttu-id="07c56-239">资产管理器还会呈现`<script>`标记在正确的位置，以便可以快速 （而无需下载脚本在呈现时） 加载此页面，以避免可能发生在呈现之前调用脚本的错误已完成。</span><span class="sxs-lookup"><span data-stu-id="07c56-239">The assets manager also renders `<script>` tags in the right place so that the page can load quickly (without downloading scripts while rendering) and to avoid errors that can occur if scripts are called before rendering is complete.</span></span>

<span data-ttu-id="07c56-240">例如，假设您创建的自定义帮助程序调用的 JavaScript 文件，并在内容页面代码中三个不同位置上调用此帮助器。</span><span class="sxs-lookup"><span data-stu-id="07c56-240">For example, suppose that you create a custom helper that calls a JavaScript file, and you call this helper at three different places in your content page code.</span></span> <span data-ttu-id="07c56-241">如果不使用的资产管理器注册该脚本调用中帮助程序，三个不同`<script>`都指向同一个脚本文件将显示在呈现页面中的标记。</span><span class="sxs-lookup"><span data-stu-id="07c56-241">If you don't use the assets manager to register the script calls in the helper, three different `<script>` tags that all point to the same script file will appear in your rendered page.</span></span> <span data-ttu-id="07c56-242">此外，具体取决于 where`<script>`标记插入到呈现的页面中，如果脚本会尝试访问某些页面元素在页面完全加载之前可能发生错误。</span><span class="sxs-lookup"><span data-stu-id="07c56-242">Plus, depending on where the `<script>` tags are inserted in the rendered page, errors may occur if the script tries to access certain page elements before the page fully loads.</span></span> <span data-ttu-id="07c56-243">如果您使用资产管理器注册的脚本，则避免这些问题。</span><span class="sxs-lookup"><span data-stu-id="07c56-243">If you use the assets manager to register the script, you avoid these problems.</span></span>

<span data-ttu-id="07c56-244">您可以使用资产管理器注册一个脚本，通过执行此操作：</span><span class="sxs-lookup"><span data-stu-id="07c56-244">You can register a script with the assets manager by doing this:</span></span>

- <span data-ttu-id="07c56-245">在代码中，需要引用该脚本，调用`Assets.AddScript`方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-245">In the code that needs to reference the script, call the `Assets.AddScript` method.</span></span>
- <span data-ttu-id="07c56-246">在中 *\_SiteLayout*页上，调用`Assets.GetScripts`方法以呈现`<script>`标记。</span><span class="sxs-lookup"><span data-stu-id="07c56-246">In a *\_SiteLayout* page, call the `Assets.GetScripts` method to render the `<script>` tags.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="07c56-247">将对的调用放`Assets.GetScripts`作为中的最后一项`<body>`的元素 *\_SiteLayout*页。</span><span class="sxs-lookup"><span data-stu-id="07c56-247">Put calls to `Assets.GetScripts` as the very last item in the `<body>` element of the *\_SiteLayout* page.</span></span> <span data-ttu-id="07c56-248">这可以帮助页面加载速度更快，并有助于避免出现脚本错误。</span><span class="sxs-lookup"><span data-stu-id="07c56-248">This helps the page load faster and can help avoid script errors.</span></span>

<span data-ttu-id="07c56-249">下面的示例显示了资产管理器工作原理。</span><span class="sxs-lookup"><span data-stu-id="07c56-249">The following example shows how the assets manager works.</span></span> <span data-ttu-id="07c56-250">代码包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="07c56-250">The code contains the following items:</span></span>

- <span data-ttu-id="07c56-251">名为的自定义帮助程序`MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="07c56-251">A custom helper named `MakeNote`.</span></span> <span data-ttu-id="07c56-252">此帮助器将呈现一个框内的字符串通过包装`div`围绕它的元素的边框以及添加已设置样式&quot;注意：&quot;到它。</span><span class="sxs-lookup"><span data-stu-id="07c56-252">This helper renders a string inside a box by wrapping a `div` element around it that's styled with a border and by adding &quot;Note:&quot; to it.</span></span> <span data-ttu-id="07c56-253">帮助器也会调用向该便笺添加运行时行为的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-253">The helper also calls a JavaScript file that adds run-time behavior to the note.</span></span> <span data-ttu-id="07c56-254">而不是引用的脚本`<script>`标记，该帮助器注册脚本通过调用`Assets.AddScript`。</span><span class="sxs-lookup"><span data-stu-id="07c56-254">Rather than reference the script with a `<script>` tag, the helper registers the script by calling `Assets.AddScript` .</span></span>
- <span data-ttu-id="07c56-255">一个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-255">A JavaScript file.</span></span> <span data-ttu-id="07c56-256">这是由帮助程序，名为的文件和临时增加了期间注意项的字体大小`mouseover`事件。</span><span class="sxs-lookup"><span data-stu-id="07c56-256">This is the file that's called by the helper, and it temporarily increases the font size of note items during a `mouseover` event.</span></span>
- <span data-ttu-id="07c56-257">内容页中，即在引用<em>\_SiteLayout</em>页上，将呈现在正文中，一些内容，然后调用`MakeNote`帮助器。</span><span class="sxs-lookup"><span data-stu-id="07c56-257">A content page, which references the<em>\_SiteLayout</em> page, renders some content in the body, and then calls the `MakeNote` helper.</span></span>
- <span data-ttu-id="07c56-258">一个 *\_SiteLayout*页。</span><span class="sxs-lookup"><span data-stu-id="07c56-258">A *\_SiteLayout* page.</span></span> <span data-ttu-id="07c56-259">本页面提供通用标头和页面布局结构。</span><span class="sxs-lookup"><span data-stu-id="07c56-259">This page provides a common header and a page layout structure.</span></span> <span data-ttu-id="07c56-260">它还包括调用`Assets.GetScripts`，这是资产管理器如何呈现脚本调用在页面中。</span><span class="sxs-lookup"><span data-stu-id="07c56-260">It also includes a call to `Assets.GetScripts`, which is how the assets manager renders script calls in a page.</span></span>

<span data-ttu-id="07c56-261">运行示例：</span><span class="sxs-lookup"><span data-stu-id="07c56-261">To run the sample:</span></span>

1. <span data-ttu-id="07c56-262">创建一个空的 Web Pages 2 网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-262">Create an empty Web Pages 2 website.</span></span> <span data-ttu-id="07c56-263">你可以使用 WebMatrix**空站点**此模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-263">You can use the WebMatrix **Empty Site** template for this.</span></span>
2. <span data-ttu-id="07c56-264">创建名为的文件夹*脚本*站点中。</span><span class="sxs-lookup"><span data-stu-id="07c56-264">Create a folder named *Scripts* in the site.</span></span>
3. <span data-ttu-id="07c56-265">在中*脚本*文件夹中，创建名为的文件*Test.js*，复制*Test.js*到该内容从该示例中，并保存该文件...</span><span class="sxs-lookup"><span data-stu-id="07c56-265">In the *Scripts* folder, create a file named *Test.js*, copy the *Test.js* content into it from the example, and save the file..</span></span>
4. <span data-ttu-id="07c56-266">创建名为的文件夹*应用程序\_代码*站点中。</span><span class="sxs-lookup"><span data-stu-id="07c56-266">Create a folder named *App\_Code* in the site.</span></span>
5. <span data-ttu-id="07c56-267">在中*应用程序\_代码*文件夹中，创建名为的文件*Helpers.cshtml*，将示例代码复制到它，并将其保存在名为的文件夹中*应用\_代码*根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="07c56-267">In the *App\_Code* folder, create a file named *Helpers.cshtml*, copy the example code into it, and save it in a folder named *App\_Code* in the root folder.</span></span>
6. <span data-ttu-id="07c56-268">在站点的根文件夹中创建名为的文件 *\_SiteLayout.cshtml，* 的示例复制到它，并保存该文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-268">In the site's root folder, create a file named *\_SiteLayout.cshtml,* copy the example into it, and save the file.</span></span>
7. <span data-ttu-id="07c56-269">在站点根目录中创建名为的文件*ContentPage.cshtml*、 添加示例代码，并将其保存。</span><span class="sxs-lookup"><span data-stu-id="07c56-269">In the site root, create a file named *ContentPage.cshtml*, add the example code, and save it.</span></span>
8. <span data-ttu-id="07c56-270">运行*ContentPage*在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="07c56-270">Run *ContentPage* in a browser.</span></span> <span data-ttu-id="07c56-271">传递给字符串`MakeNote`帮助器呈现为装箱的注意。</span><span class="sxs-lookup"><span data-stu-id="07c56-271">The string you passed to the `MakeNote` helper is rendered as a boxed note.</span></span>
9. <span data-ttu-id="07c56-272">鼠标指针经过注意。</span><span class="sxs-lookup"><span data-stu-id="07c56-272">Pass the mouse pointer over the note.</span></span> <span data-ttu-id="07c56-273">该脚本将暂时增加便笺的字体大小。</span><span class="sxs-lookup"><span data-stu-id="07c56-273">The script temporarily increases the font size of the note.</span></span>
10. <span data-ttu-id="07c56-274">查看呈现的页面上的源。</span><span class="sxs-lookup"><span data-stu-id="07c56-274">View the source of the rendered page.</span></span> <span data-ttu-id="07c56-275">由于对的调用放置`Assets.GetScripts`，呈现`<script>`调用的标记*Test.js*是页的正文中的最后一个项。</span><span class="sxs-lookup"><span data-stu-id="07c56-275">Because of where you placed the call to `Assets.GetScripts`, the rendered `<script>` tag that calls *Test.js* is the very last item in the body of the page.</span></span>

<span data-ttu-id="07c56-276">*Test.js*</span><span class="sxs-lookup"><span data-stu-id="07c56-276">*Test.js*</span></span>

[!code-javascript[Main](top-features-in-web-pages-2/samples/sample8.js)]

<span data-ttu-id="07c56-277">*Helpers.cshtml*</span><span class="sxs-lookup"><span data-stu-id="07c56-277">*Helpers.cshtml*</span></span>

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample9.cshtml)]

<span data-ttu-id="07c56-278">*\_SiteLayout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="07c56-278">*\_SiteLayout.cshtml*</span></span>

[!code-html[Main](top-features-in-web-pages-2/samples/sample10.html)]

<span data-ttu-id="07c56-279">*ContentPage.cshtml*</span><span class="sxs-lookup"><span data-stu-id="07c56-279">*ContentPage.cshtml*</span></span>

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample11.cshtml)]

<span data-ttu-id="07c56-280">以下屏幕截图显示*ContentPage.cshtml*在浏览器中当鼠标指针拖过注释：</span><span class="sxs-lookup"><span data-stu-id="07c56-280">The following screenshot shows *ContentPage.cshtml* in a browser when you hold the mouse pointer over the note:</span></span>

<span data-ttu-id="07c56-281">[![topSeven-resmgr-1](top-features-in-web-pages-2/_static/image14.png)](top-features-in-web-pages-2/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-281">[![topSeven-resmgr-1](top-features-in-web-pages-2/_static/image14.png)](top-features-in-web-pages-2/_static/image13.png)</span></span>

<a id="oauthsetup"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a><span data-ttu-id="07c56-282">启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名</span><span class="sxs-lookup"><span data-stu-id="07c56-282">Enabling Logins from Facebook and Other Sites Using OAuth and OpenID</span></span>

<span data-ttu-id="07c56-283">Web Pages 2 提供了增强的成员身份和身份验证的选项。</span><span class="sxs-lookup"><span data-stu-id="07c56-283">Web Pages 2 provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="07c56-284">主要增强功能是有的新[OAuth](http://oauth.net/)并[OpenID](http://openid.net/)提供程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-284">The main enhancement is that there are new [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="07c56-285">使用这些提供程序，可让你使用 Facebook、 Twitter、 Windows Live、 Google 和 Yahoo 从其现有凭据的站点到用户登录。</span><span class="sxs-lookup"><span data-stu-id="07c56-285">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Windows Live, Google, and Yahoo.</span></span> <span data-ttu-id="07c56-286">例如，若要使用 Facebook 帐户登录，用户可以只需选择 Facebook 图标，将它们重定向到它们在其中输入他们的用户信息的 Facebook 登录页。</span><span class="sxs-lookup"><span data-stu-id="07c56-286">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="07c56-287">它们然后可以将 Facebook 登录你的站点上与其帐户相关联。</span><span class="sxs-lookup"><span data-stu-id="07c56-287">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="07c56-288">Web Pages 成员资格功能相关的增强功能是使用你的网站上的单个帐户，用户可以将多个登录名 （包括登录名从社交网站） 相关联。</span><span class="sxs-lookup"><span data-stu-id="07c56-288">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="07c56-289">下图显示了从登录页面**入门网站**模板，用户可以在其中选择一个 Facebook、 Twitter 或 Windows Live 图标，以启用日志记录使用的外部帐户：</span><span class="sxs-lookup"><span data-stu-id="07c56-289">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, or Windows Live icon to enable logging in with an external account:</span></span>

<span data-ttu-id="07c56-290">[![topSeven-oauth-1](top-features-in-web-pages-2/_static/image16.png)](top-features-in-web-pages-2/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-290">[![topSeven-oauth-1](top-features-in-web-pages-2/_static/image16.png)](top-features-in-web-pages-2/_static/image15.png)</span></span>

<span data-ttu-id="07c56-291">你可以启用 OAuth 和 OpenID 的成员身份使用几行代码。</span><span class="sxs-lookup"><span data-stu-id="07c56-291">You can enable OAuth and OpenID membership using just a few lines of code.</span></span> <span data-ttu-id="07c56-292">您使用的方法和属性以使用 OAuth 和 OpenID 提供程序位于`WebMatrix.Security.OAuthWebSecurity`类。</span><span class="sxs-lookup"><span data-stu-id="07c56-292">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span>

<span data-ttu-id="07c56-293">但是，而不是使用代码以启用从其他站点的登录名，开始使用新的提供程序的推荐的方法是使用新**入门网站**随 WebMatrix 2 Beta 的模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-293">However, instead of using code to enable logins from other sites, a recommended way to get started with the new providers is to use the new **Starter Site** template that is included with WebMatrix 2 Beta.</span></span> <span data-ttu-id="07c56-294">**入门网站**模板包括完整的成员身份基础结构，需要让用户登录到你使用本地凭据或来自另一个站点的站点登录页、 成员资格数据库，与所有的代码完成.</span><span class="sxs-lookup"><span data-stu-id="07c56-294">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

#### <a name="how-to-enable-logins-using-the-oauth-and-openid-providers"></a><span data-ttu-id="07c56-295">如何启用登录名使用 OAuth 和 OpenID 提供程序</span><span class="sxs-lookup"><span data-stu-id="07c56-295">How to Enable Logins using the OAuth and OpenID Providers</span></span>

<span data-ttu-id="07c56-296">本部分举例说明如何让用户从外部站点 （Facebook、 Twitter、 Windows Live、 Google 或 Yahoo） 登录到基于站点**入门网站**模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-296">This section provides an example of how to let users log in from external sites (Facebook, Twitter, Windows Live, Google, or Yahoo) to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="07c56-297">在创建后入门网站，你执行操作 （详细信息按照）：</span><span class="sxs-lookup"><span data-stu-id="07c56-297">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="07c56-298">使用 OAuth 提供程序 （Facebook、 Twitter 和 Windows Live） 的站点，外部站点上创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-298">For the sites that use an OAuth provider (Facebook, Twitter, and Windows Live), create an application on the external site.</span></span> <span data-ttu-id="07c56-299">这样，您将需要为了调用这些站点的登录功能的应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="07c56-299">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span> <span data-ttu-id="07c56-300">对于使用 OpenID 提供程序 （Google、 Yahoo） 的站点，不需要创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-300">For sites that use an OpenID provider (Google, Yahoo), you do not have to create an application.</span></span> <span data-ttu-id="07c56-301">对于所有这些站点，必须具有一个帐户，以便在中记录并创建开发人员应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-301">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="07c56-302">Windows Live 应用程序仅接受工作网站的实时 URL，因此不能用于本地网站 URL 测试登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-302">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="07c56-303">编辑你的网站中的几个文件以指定适当的身份验证提供程序，并将提交到想要使用的站点的登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-303">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="07c56-304">**若要启用 Google 和 Yahoo 登录**:</span><span class="sxs-lookup"><span data-stu-id="07c56-304">**To enable Google and Yahoo logins**:</span></span>

1. <span data-ttu-id="07c56-305">在你的网站，编辑 *\_AppStart.cshtml*页上，在 Razor 代码块中调用后面添加以下两行代码`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-305">In your website, edit the *\_AppStart.cshtml* page and add the following two lines of code in the Razor code block after the call to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="07c56-306">此代码将启用 Google 和 Yahoo OpenID 提供程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-306">This code enables both the Google and Yahoo OpenID providers.</span></span> 

    [!code-css[Main](top-features-in-web-pages-2/samples/sample12.css)]
2. <span data-ttu-id="07c56-307">在中 *~/Account/Login.cshtml*页上，从下列选项中删除注释`<fieldset>`快要结束的页面的标记块。</span><span class="sxs-lookup"><span data-stu-id="07c56-307">In the *~/Account/Login.cshtml* page, remove the comments from the following `<fieldset>` block of markup near the end of the page.</span></span> <span data-ttu-id="07c56-308">若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。</span><span class="sxs-lookup"><span data-stu-id="07c56-308">To uncomment the code, remove the `@*` characters that precede and follow the `<fieldset>` block.</span></span> <span data-ttu-id="07c56-309">生成的代码块如下所示：</span><span class="sxs-lookup"><span data-stu-id="07c56-309">The resulting code block looks like this:</span></span>

    [!code-html[Main](top-features-in-web-pages-2/samples/sample13.html)]
3. <span data-ttu-id="07c56-310">添加`<input>`元素的 Google 或 Yahoo 提供程序`<fieldset>`组中 *~/Account/Login.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="07c56-310">Add an `<input>` element for the Google or Yahoo provider to the `<fieldset>` group in the *~/Account/Login.cshtml* page.</span></span> <span data-ttu-id="07c56-311">已更新`<fieldset>`组`<input>`元素 Google 和 Yahoo 看起来如以下示例：</span><span class="sxs-lookup"><span data-stu-id="07c56-311">The updated `<fieldset>` group with `<input>` elements for both Google and Yahoo looks like the following example:</span></span> 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample14.html)]
4. <span data-ttu-id="07c56-312">在中 *~/Account/AssociateServiceAccount.cshtml*页上，添加`<input>`Google 或 Yahoo 到元素`<fieldset>`组在文件末尾附近。</span><span class="sxs-lookup"><span data-stu-id="07c56-312">In the *~/Account/AssociateServiceAccount.cshtml* page, add `<input>` elements for Google or Yahoo to the `<fieldset>` group near the end of the file.</span></span> <span data-ttu-id="07c56-313">你可以复制相同`<input>`刚添加到的元素`<fieldset>`主题中 *~/Account/Login.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="07c56-313">You can copy the same `<input>` elements that you just added to the `<fieldset>` section in the *~/Account/Login.cshtml* page.</span></span> 

    <span data-ttu-id="07c56-314">*~/Account/AssociateServiceAccount.cshtml*可以使用入门网站模板中的页，如果你想要创建的用户可以将其他站点中的多个登录名关联与单个帐户在网站上的页面。</span><span class="sxs-lookup"><span data-stu-id="07c56-314">The *~/Account/AssociateServiceAccount.cshtml* page in the Starter Site template can be used if you want to create a page on which users can associate multiple logins from other sites with a single account on your website.</span></span>

<span data-ttu-id="07c56-315">现在，你可以测试 Google 和 Yahoo 登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-315">Now you can test Google and Yahoo logins.</span></span>

1. <span data-ttu-id="07c56-316">运行*default.cshtml*您的网站上，然后选择**登录**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-316">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="07c56-317">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Google**或者**Yahoo**提交按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-317">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="07c56-318">此示例使用 Google 登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-318">This example uses the Google login.</span></span> 

    <span data-ttu-id="07c56-319">Web 页面将请求重定向到 Google 登录页。</span><span class="sxs-lookup"><span data-stu-id="07c56-319">The web page redirects the request to the Google login page.</span></span>

    <span data-ttu-id="07c56-320">[![topSeven-oauth-6](top-features-in-web-pages-2/_static/image18.png)](top-features-in-web-pages-2/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-320">[![topSeven-oauth-6](top-features-in-web-pages-2/_static/image18.png)](top-features-in-web-pages-2/_static/image17.png)</span></span>
3. <span data-ttu-id="07c56-321">输入现有 Google 帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="07c56-321">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="07c56-322">如果出现要求你是否想要允许本地主机要使用帐户中的信息，请单击 Google**允许**。</span><span class="sxs-lookup"><span data-stu-id="07c56-322">If Google asks you whether you want to allow Localhost to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="07c56-323">代码使用 Google 的令牌对用户进行身份验证，然后返回到此页上你的网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-323">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="07c56-324">此页，可以将其 Google 登录名与你的网站上的现有帐户相关联的用户或用户可以在注册你将使用的外部登录名相关联的站点上的新帐户。</span><span class="sxs-lookup"><span data-stu-id="07c56-324">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    <span data-ttu-id="07c56-325">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image20.png)](top-features-in-web-pages-2/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-325">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image20.png)](top-features-in-web-pages-2/_static/image19.png)</span></span>
5. <span data-ttu-id="07c56-326">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-326">Choose the **Associate** button.</span></span> <span data-ttu-id="07c56-327">在浏览器返回到应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="07c56-327">The browser returns to your application's home page.</span></span>

    <span data-ttu-id="07c56-328">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image22.png)](top-features-in-web-pages-2/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-328">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image22.png)](top-features-in-web-pages-2/_static/image21.png)</span></span>

    <span data-ttu-id="07c56-329">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image24.png)](top-features-in-web-pages-2/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-329">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image24.png)](top-features-in-web-pages-2/_static/image23.png)</span></span>

<span data-ttu-id="07c56-330">**若要启用 Facebook 登录名**:</span><span class="sxs-lookup"><span data-stu-id="07c56-330">**To enable Facebook logins**:</span></span>

1. <span data-ttu-id="07c56-331">转到[Facebook 开发人员站点](https://developers.facebook.com/apps)（如果尚未登录，则日志）。</span><span class="sxs-lookup"><span data-stu-id="07c56-331">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="07c56-332">选择**创建新应用**按钮，然后按照提示进行命名和创建新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-332">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="07c56-333">在部分**选择如何将您的应用程序与 Facebook**，选择**网站**部分。</span><span class="sxs-lookup"><span data-stu-id="07c56-333">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="07c56-334">填写**站点 URL**字段与你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。</span><span class="sxs-lookup"><span data-stu-id="07c56-334">Fill in the **Site URL** field with the URL of your site (for example, [`http://www.example.com`](http://www.example.com)).</span></span> <span data-ttu-id="07c56-335">**域**字段是可选的; 可以使用此提供对整个域的身份验证 (如*example.com*)。</span><span class="sxs-lookup"><span data-stu-id="07c56-335">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="07c56-336">如果你使用 URL 在本地计算机上运行站点喜欢`http://localhost:12345`（其中数是本地端口号），可以添加此值设置为**站点 URL**字段用于测试你的站点。</span><span class="sxs-lookup"><span data-stu-id="07c56-336">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="07c56-337">但是，任何时候，只要你的本地站点更改的端口号，你将需要更新**站点 URL**字段的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-337">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="07c56-338">选择**保存更改**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-338">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="07c56-339">选择**应用**同样，选项卡，然后查看你的应用程序的起始页。</span><span class="sxs-lookup"><span data-stu-id="07c56-339">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="07c56-340">复制**应用程序 ID**并**应用程序密码**为应用程序的值并将其粘贴到一个临时的文本文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-340">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="07c56-341">网站代码中，会将这些值传递到 Facebook 提供程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-341">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="07c56-342">退出 Facebook 开发人员网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-342">Exit the Facebook developer site.</span></span>

<span data-ttu-id="07c56-343">现在您更改两个页面中你的网站，以便用户将能够登录到网站使用其 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="07c56-343">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="07c56-344">在你的网站，编辑 *\_AppStart.cshtml*页上，并取消注释的代码，为 Facebook OAuth 提供程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-344">In your website, edit the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="07c56-345">取消注释的代码块如以下所示：</span><span class="sxs-lookup"><span data-stu-id="07c56-345">The uncommented code block looks like the following:</span></span> 

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample15.xml)]
2. <span data-ttu-id="07c56-346">复制**应用程序 ID**从 Facebook 应用程序的值作为值`consumerKey`参数 （在引号内）。</span><span class="sxs-lookup"><span data-stu-id="07c56-346">Copy the **App ID** value from the Facebook application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
3. <span data-ttu-id="07c56-347">复制**应用程序机密**从 Facebook 应用程序作为值`consumerSecret`参数值。</span><span class="sxs-lookup"><span data-stu-id="07c56-347">Copy **App Secret** value from the Facebook application as the `consumerSecret` parameter value.</span></span>
4. <span data-ttu-id="07c56-348">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-348">Save and close the file.</span></span>
5. <span data-ttu-id="07c56-349">编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。</span><span class="sxs-lookup"><span data-stu-id="07c56-349">Edit the *~/Account/Login.cshtml* page and remove the comments from the `<fieldset>` block near the end of the page.</span></span> <span data-ttu-id="07c56-350">若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。</span><span class="sxs-lookup"><span data-stu-id="07c56-350">To uncomment the code, remove the `@*` characters that precede and follow the `<fieldset>` block.</span></span> <span data-ttu-id="07c56-351">带有注释的代码块中删除类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="07c56-351">The code block with comments removed looks like the following:</span></span> 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample16.html)]
6. <span data-ttu-id="07c56-352">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-352">Save and close the file.</span></span>

<span data-ttu-id="07c56-353">现在，你可以测试 Facebook 登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-353">Now you can test the Facebook login.</span></span>

1. <span data-ttu-id="07c56-354">运行该站点*default.cshtml*页上，然后选择**登录名**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-354">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="07c56-355">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Facebook**图标。</span><span class="sxs-lookup"><span data-stu-id="07c56-355">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="07c56-356">Web 页面将请求重定向到 Facebook 登录页。</span><span class="sxs-lookup"><span data-stu-id="07c56-356">The web page redirects the request to the Facebook login page.</span></span>

    <span data-ttu-id="07c56-357">[![topSeven-oauth-2](top-features-in-web-pages-2/_static/image26.png)](top-features-in-web-pages-2/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-357">[![topSeven-oauth-2](top-features-in-web-pages-2/_static/image26.png)](top-features-in-web-pages-2/_static/image25.png)</span></span>
3. <span data-ttu-id="07c56-358">登录到 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="07c56-358">Log into a Facebook account.</span></span> 

    <span data-ttu-id="07c56-359">代码使用 Facebook 令牌进行身份验证，然后返回到页您可以在其中将 Facebook 登录名与站点的登录名相关联。</span><span class="sxs-lookup"><span data-stu-id="07c56-359">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="07c56-360">你的用户名称或电子邮件地址填充到**电子邮件**字段在窗体上。</span><span class="sxs-lookup"><span data-stu-id="07c56-360">Your user name or email address is filled into the **Email** field on the form.</span></span>

    <span data-ttu-id="07c56-361">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image28.png)](top-features-in-web-pages-2/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-361">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image28.png)](top-features-in-web-pages-2/_static/image27.png)</span></span>
4. <span data-ttu-id="07c56-362">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-362">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="07c56-363">在浏览器返回到主页并登录。</span><span class="sxs-lookup"><span data-stu-id="07c56-363">The browser returns to the home page and you are logged in.</span></span>

    <span data-ttu-id="07c56-364">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image30.png)](top-features-in-web-pages-2/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-364">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image30.png)](top-features-in-web-pages-2/_static/image29.png)</span></span>

<span data-ttu-id="07c56-365">**若要启用 Twitter 登录名：**</span><span class="sxs-lookup"><span data-stu-id="07c56-365">**To enable Twitter logins:**</span></span> 

1. <span data-ttu-id="07c56-366">浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="07c56-366">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="07c56-367">选择**创建应用**链接，然后登录到网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-367">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="07c56-368">上**创建的应用程序**窗体中，填写**名称**并**说明**字段。</span><span class="sxs-lookup"><span data-stu-id="07c56-368">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="07c56-369">在中**网站**字段中，输入你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。</span><span class="sxs-lookup"><span data-stu-id="07c56-369">In the **WebSite** field, enter the URL of your site (for example, [`http://www.example.com`](http://www.example.com)).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="07c56-370">如果您要测试你的本地站点 (使用类似`http://localhost:12345`)，Twitter 可能不接受 URL。</span><span class="sxs-lookup"><span data-stu-id="07c56-370">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="07c56-371">但是，您可能能够使用本地环回 IP 地址 (例如`http://127.0.0.1:12345`)。</span><span class="sxs-lookup"><span data-stu-id="07c56-371">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="07c56-372">这将简化测试本地应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="07c56-372">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="07c56-373">但是，每次你的本地网站的端口号更改，你将需要更新**网站**字段的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-373">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="07c56-374">在中**回叫 URL**字段中，输入你希望用户在登录后到 Twitter 到返回的网站中的页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="07c56-374">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="07c56-375">例如，若要向用户发送到入门网站 （它将识别其登录的状态） 的主页上，输入中输入的同一个 URL**网站**字段。</span><span class="sxs-lookup"><span data-stu-id="07c56-375">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="07c56-376">接受条款，然后选择**创建 Twitter 应用程序**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-376">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="07c56-377">上**我的应用程序**登陆页上，选择你创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-377">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="07c56-378">上**详细信息**选项卡上，滚动到底部并选择**创建我的访问令牌**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-378">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="07c56-379">上**详细信息**选项卡上，复制**使用者密钥**并**使用者机密**为应用程序的值并将其粘贴到一个临时的文本文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-379">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="07c56-380">网站代码中，会将这些值传递到 Twitter 提供程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-380">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="07c56-381">退出 Twitter 网站。</span><span class="sxs-lookup"><span data-stu-id="07c56-381">Exit the Twitter site.</span></span>

<span data-ttu-id="07c56-382">现在您更改两个页面中你的网站，以便用户能够登录到使用 Twitter 帐户的站点。</span><span class="sxs-lookup"><span data-stu-id="07c56-382">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="07c56-383">在你的网站，编辑 *\_AppStart.cshtml*页面和 Twitter OAuth 提供程序取消注释的代码。</span><span class="sxs-lookup"><span data-stu-id="07c56-383">In your website, edit the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="07c56-384">取消注释的代码块如下所示：</span><span class="sxs-lookup"><span data-stu-id="07c56-384">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](top-features-in-web-pages-2/samples/sample17.cs)]
2. <span data-ttu-id="07c56-385">复制**使用者密钥**从 Twitter 应用程序的值作为值`consumerKey`参数 （在引号内）。</span><span class="sxs-lookup"><span data-stu-id="07c56-385">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
3. <span data-ttu-id="07c56-386">复制**使用者机密**从 Twitter 应用程序的值作为值`consumerSecret`参数。</span><span class="sxs-lookup"><span data-stu-id="07c56-386">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
4. <span data-ttu-id="07c56-387">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-387">Save and close the file.</span></span>
5. <span data-ttu-id="07c56-388">编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。</span><span class="sxs-lookup"><span data-stu-id="07c56-388">Edit the *~/Account/Login.cshtml* page and remove the comments from the `<fieldset>` block near the end of the page.</span></span> <span data-ttu-id="07c56-389">若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。</span><span class="sxs-lookup"><span data-stu-id="07c56-389">To uncomment the code, remove the `@*` characters that precede and follow the `<fieldset>` block.</span></span> <span data-ttu-id="07c56-390">带有注释的代码块中删除类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="07c56-390">The code block with comments removed looks like the following:</span></span> 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample18.html)]
6. <span data-ttu-id="07c56-391">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-391">Save and close the file.</span></span>

<span data-ttu-id="07c56-392">现在，你可以测试 Twitter 登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-392">Now you can test the Twitter login.</span></span>

1. <span data-ttu-id="07c56-393">运行*default.cshtml*您的网站上，然后选择**登录名**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-393">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="07c56-394">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Twitter**图标。</span><span class="sxs-lookup"><span data-stu-id="07c56-394">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="07c56-395">Web 页面将请求重定向到 Twitter 登录页面为您创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-395">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    <span data-ttu-id="07c56-396">[![topSeven-oauth-4](top-features-in-web-pages-2/_static/image32.png)](top-features-in-web-pages-2/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-396">[![topSeven-oauth-4](top-features-in-web-pages-2/_static/image32.png)](top-features-in-web-pages-2/_static/image31.png)</span></span>
3. <span data-ttu-id="07c56-397">登录到 Twitter 帐户。</span><span class="sxs-lookup"><span data-stu-id="07c56-397">Log into a Twitter account.</span></span>
4. <span data-ttu-id="07c56-398">代码使用 Twitter 令牌进行身份验证用户，然后返回到页你可以将关联您使用您网站的帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="07c56-398">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="07c56-399">名称或电子邮件地址填充到**电子邮件**字段在窗体上。</span><span class="sxs-lookup"><span data-stu-id="07c56-399">Your name or email address is filled into the **Email** field on the form.</span></span>

    <span data-ttu-id="07c56-400">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image34.png)](top-features-in-web-pages-2/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-400">[![topSeven-oauth-5](top-features-in-web-pages-2/_static/image34.png)](top-features-in-web-pages-2/_static/image33.png)</span></span>
5. <span data-ttu-id="07c56-401">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-401">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="07c56-402">在浏览器返回到主页并登录。</span><span class="sxs-lookup"><span data-stu-id="07c56-402">The browser returns to the home page and you are logged in.</span></span>

    <span data-ttu-id="07c56-403">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image36.png)](top-features-in-web-pages-2/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-403">[![topSeven-oauth-3](top-features-in-web-pages-2/_static/image36.png)](top-features-in-web-pages-2/_static/image35.png)</span></span>

<a id="maphelper"></a>
### <a name="adding-maps-using-the-maps-helper"></a><span data-ttu-id="07c56-404">添加映射使用映射帮助器</span><span class="sxs-lookup"><span data-stu-id="07c56-404">Adding Maps Using the Maps Helper</span></span>

<span data-ttu-id="07c56-405">Web Pages 2 包括添加到 ASP.NET Web Helpers Library，这是 Web Pages 站点加载项的包。</span><span class="sxs-lookup"><span data-stu-id="07c56-405">Web Pages 2 includes additions to the ASP.NET Web Helpers Library, which is a package of add-ins for a Web Pages site.</span></span> <span data-ttu-id="07c56-406">其中一种是由提供的映射组件`Microsoft.Web.Helpers.Maps`类。</span><span class="sxs-lookup"><span data-stu-id="07c56-406">One of these is a mapping component provided by the `Microsoft.Web.Helpers.Maps` class.</span></span> <span data-ttu-id="07c56-407">可以使用`Maps`类生成基于一个地址或一组的经度和纬度坐标的地图。</span><span class="sxs-lookup"><span data-stu-id="07c56-407">You can use the `Maps` class to generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="07c56-408">`Maps`类的允许您直接在包括必应、 Google、 MapQuest 和 Yahoo 的常用映射引擎调用。</span><span class="sxs-lookup"><span data-stu-id="07c56-408">The `Maps` class lets you call directly into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="07c56-409">若要使用新`Maps`类在你的网站，您必须首先安装 Web Helpers Library 版本 2。</span><span class="sxs-lookup"><span data-stu-id="07c56-409">To use the new `Maps` class in your website, you must first install the version 2 of the Web Helpers Library.</span></span> <span data-ttu-id="07c56-410">若要执行此操作，请转到用于安装当前版本的说明[ASP.NET Web Helpers Library](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)并安装版本 2。</span><span class="sxs-lookup"><span data-stu-id="07c56-410">To do this, go to the instructions for installing the currently released version of the [ASP.NET Web Helpers Library](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers) and install version 2.</span></span>

<span data-ttu-id="07c56-411">向页面添加映射的步骤是相同的调用无论哪个映射引擎的。</span><span class="sxs-lookup"><span data-stu-id="07c56-411">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="07c56-412">您只需添加对映射页的 JavaScript 文件引用，然后再添加呈现的调用`<script>`上您的页面的标记。</span><span class="sxs-lookup"><span data-stu-id="07c56-412">You just add a JavaScript file reference to your mapping page and then add a call that renders the `<script>` tags on your page.</span></span> <span data-ttu-id="07c56-413">然后在映射页中上, 调用你想要使用的映射引擎。</span><span class="sxs-lookup"><span data-stu-id="07c56-413">Then on your mapping page, call the map engine you want to use.</span></span>

<span data-ttu-id="07c56-414">下面的示例演示如何创建将基于一个地址，结构图呈现的页面和呈现地图基于经度和纬度坐标的另一页。</span><span class="sxs-lookup"><span data-stu-id="07c56-414">The following example shows how to create a page that renders a map based on an address, and another page that renders a map based on longitude and latitude coordinates.</span></span> <span data-ttu-id="07c56-415">地址映射示例使用 Google 地图和坐标映射示例使用必应地图。</span><span class="sxs-lookup"><span data-stu-id="07c56-415">The address mapping example uses Google Maps, and the coordinate mapping example uses Bing Maps.</span></span> <span data-ttu-id="07c56-416">请注意在代码中的以下元素：</span><span class="sxs-lookup"><span data-stu-id="07c56-416">Note the following elements in the code:</span></span>

- <span data-ttu-id="07c56-417">对调用`Assets.AddScript`在两个映射页的顶部。</span><span class="sxs-lookup"><span data-stu-id="07c56-417">The call to `Assets.AddScript` at the top of the two mapping pages.</span></span> <span data-ttu-id="07c56-418">此方法将添加到的引用*jquery 1.6.2.min.js*附带的文件**入门网站**模板和所要求的`Maps`类。</span><span class="sxs-lookup"><span data-stu-id="07c56-418">This method adds a reference to the *jquery-1.6.2.min.js* file that is included with the **Starter Site** template and that's required by the `Maps` class.</span></span>
- <span data-ttu-id="07c56-419">对调用`Assets.GetScripts`布局文件中的方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-419">The call to the `Assets.GetScripts` method in the layout file.</span></span> <span data-ttu-id="07c56-420">此方法将呈现`<script>`两个映射页上标记。</span><span class="sxs-lookup"><span data-stu-id="07c56-420">This method renders the `<script>` tag on the two mapping pages.</span></span>
- <span data-ttu-id="07c56-421">在调用`@Maps.GetGoogleHtml`和`@Maps.GetBingHtml`映射页中的方法。</span><span class="sxs-lookup"><span data-stu-id="07c56-421">The call to the `@Maps.GetGoogleHtml` and the `@Maps.GetBingHtml` methods in the mapping pages.</span></span> <span data-ttu-id="07c56-422">若要查找某个地址，必须传递地址字符串。</span><span class="sxs-lookup"><span data-stu-id="07c56-422">To map an address, you must pass an address string.</span></span> <span data-ttu-id="07c56-423">若要映射的坐标，必须通过经度和纬度坐标。</span><span class="sxs-lookup"><span data-stu-id="07c56-423">To map coordinates, you must pass longitude and latitude coordinates.</span></span> <span data-ttu-id="07c56-424">对于必应地图引擎中，你还必须传递一个密钥 (通过在注册获取免费[必应地图开发人员站点](https://www.microsoft.com/maps/developers/web.aspx))。</span><span class="sxs-lookup"><span data-stu-id="07c56-424">For the Bing Maps engine, you must also pass a key (which you get for free by signing up at the [Bing Maps Developers site](https://www.microsoft.com/maps/developers/web.aspx)).</span></span> <span data-ttu-id="07c56-425">其他映射引擎的方法的工作方式类似 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。</span><span class="sxs-lookup"><span data-stu-id="07c56-425">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>

<span data-ttu-id="07c56-426">若要创建映射页：</span><span class="sxs-lookup"><span data-stu-id="07c56-426">To create mapping pages:</span></span>

1. <span data-ttu-id="07c56-427">创建基于网站**入门网站**模板。</span><span class="sxs-lookup"><span data-stu-id="07c56-427">Create a website based on the **Starter Site** template.</span></span>
2. <span data-ttu-id="07c56-428">创建名为的文件*MapAddress.cshtml*站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="07c56-428">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="07c56-429">此页面将生成基于将传递给它的地址的映射。</span><span class="sxs-lookup"><span data-stu-id="07c56-429">This page will generate a map based on an address that you pass to it.</span></span>
3. <span data-ttu-id="07c56-430">将以下代码复制到文件中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-430">Copy the following code into the file, overwriting the existing content.</span></span> 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample19.cshtml)]
4. <span data-ttu-id="07c56-431">创建名为的文件 *\_MapLayout.cshtml*站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="07c56-431">Create a file named *\_MapLayout.cshtml* in the root of the site.</span></span> <span data-ttu-id="07c56-432">此页将为两个映射页的布局页。</span><span class="sxs-lookup"><span data-stu-id="07c56-432">This page will be the layout page for the two mapping pages.</span></span>
5. <span data-ttu-id="07c56-433">将以下代码复制到文件中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-433">Copy the following code into the file, overwriting the existing content.</span></span> 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample20.html)]
6. <span data-ttu-id="07c56-434">创建名为的文件*MapCoordinates.cshtml*站点的根目录中。</span><span class="sxs-lookup"><span data-stu-id="07c56-434">Create a file named *MapCoordinates.cshtml* in the root of the site.</span></span> <span data-ttu-id="07c56-435">此页面将生成基于一组向其传递的坐标的映射。</span><span class="sxs-lookup"><span data-stu-id="07c56-435">This page will generate a map based on a set of coordinates that you pass to it.</span></span>
7. <span data-ttu-id="07c56-436">将以下代码复制到文件中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-436">Copy the following code into the file, overwriting the existing content.</span></span> 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample21.cshtml)]

<span data-ttu-id="07c56-437">若要测试映射页：</span><span class="sxs-lookup"><span data-stu-id="07c56-437">To test your mapping pages:</span></span>

1. <span data-ttu-id="07c56-438">运行页*MapAddress.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="07c56-438">Run the page *MapAddress.cshtml* file.</span></span>
2. <span data-ttu-id="07c56-439">输入包括街道地址、 状态或省和邮政编码，完整地址字符串，然后选择**Map It**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-439">Enter a full address string including a street address, state or province, and postal code, and then choose the **Map It** button.</span></span> <span data-ttu-id="07c56-440">呈现地图页面，从 Google 地图：</span><span class="sxs-lookup"><span data-stu-id="07c56-440">The page renders a map from Google Maps:</span></span> 

    <span data-ttu-id="07c56-441">[![topseven-maphelper-1](top-features-in-web-pages-2/_static/image38.png)](top-features-in-web-pages-2/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-441">[![topseven-maphelper-1](top-features-in-web-pages-2/_static/image38.png)](top-features-in-web-pages-2/_static/image37.png)</span></span>
3. <span data-ttu-id="07c56-442">找到的特定位置的纬度和经度坐标集。</span><span class="sxs-lookup"><span data-stu-id="07c56-442">Find a set of latitude and longitude coordinates for a specific location.</span></span>
4. <span data-ttu-id="07c56-443">运行页*MapCoordinates.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="07c56-443">Run the page *MapCoordinates.cshtml*.</span></span> <span data-ttu-id="07c56-444">输入坐标，然后选择**Map It**按钮。</span><span class="sxs-lookup"><span data-stu-id="07c56-444">Enter the coordinates and then choose the **Map It** button.</span></span> <span data-ttu-id="07c56-445">页面从必应地图呈现地图：</span><span class="sxs-lookup"><span data-stu-id="07c56-445">The page renders a map from Bing Maps:</span></span> 

    <span data-ttu-id="07c56-446">[![topseven-maphelper-2](top-features-in-web-pages-2/_static/image40.png)](top-features-in-web-pages-2/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-446">[![topseven-maphelper-2](top-features-in-web-pages-2/_static/image40.png)](top-features-in-web-pages-2/_static/image39.png)</span></span>

<a id="sidebyside"></a>
### <a name="running-web-pages-applications-side-by-side"></a><span data-ttu-id="07c56-447">运行 Web Pages 应用程序并排显示</span><span class="sxs-lookup"><span data-stu-id="07c56-447">Running Web Pages Applications Side by Side</span></span>

<span data-ttu-id="07c56-448">Web Pages 2 添加了运行应用程序并排显示的功能。</span><span class="sxs-lookup"><span data-stu-id="07c56-448">Web Pages 2 adds the ability to run applications side by side.</span></span> <span data-ttu-id="07c56-449">这样可以继续运行 Web Pages 1 应用程序，构建新的 Web Pages 2 应用程序，并在同一台计算机上运行所有这些。</span><span class="sxs-lookup"><span data-stu-id="07c56-449">This lets you continue to run your Web Pages 1 applications, build new Web Pages 2 applications, and run all of them on the same computer.</span></span>

<span data-ttu-id="07c56-450">下面是要使用 WebMatrix 安装 Web Pages 2 试用版时，应注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="07c56-450">Here are some things to remember when you install the Web Pages 2 Beta with WebMatrix:</span></span>

- <span data-ttu-id="07c56-451">默认情况下，现有的 Web Pages 应用程序将在计算机上运行作为版本 2 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07c56-451">By default, existing Web Pages applications will run as version 2 applications on your computer.</span></span> <span data-ttu-id="07c56-452">（版本 2 的程序集安装到 GAC 中并且将自动使用。）</span><span class="sxs-lookup"><span data-stu-id="07c56-452">(The assemblies for version 2 are installed in the GAC and will be used automatically.)</span></span>
- <span data-ttu-id="07c56-453">如果你想要运行使用 Web Pages 版本 1 （而不是默认值，如下所示的上一个点） 的站点，您可以配置要执行此操作的站点。</span><span class="sxs-lookup"><span data-stu-id="07c56-453">If you want to run a site using Web Pages version 1 (instead of the default, as in the previous point), you can configure the site to do that.</span></span> <span data-ttu-id="07c56-454">如果您的网站还没有*web.config*文件位于站点的根目录中，创建一个新，并将以下 XML 复制到其中，覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-454">If your site doesn't already have a *web.config* file in the root of the site, create a new one and copy the following XML into it, overwriting the existing content.</span></span> <span data-ttu-id="07c56-455">如果站点中已包含*web.config*文件中，添加`<appSettings>`元素到如下`<configuration>`部分。</span><span class="sxs-lookup"><span data-stu-id="07c56-455">If the site already contains a *web.config* file, add an `<appSettings>` element like the following one to the `<configuration>` section.</span></span>

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample22.xml)]
  <span data-ttu-id="07c56-456">-如果未指定的版本中*web.config*文件中，将站点部署为版本 2 站点。</span><span class="sxs-lookup"><span data-stu-id="07c56-456">\`- If you do not specify a version in the *web.config* file, a site is deployed as a version 2 site.</span></span> <span data-ttu-id="07c56-457">(第 2 版程序集复制到*bin*已部署站点中的文件夹。)</span><span class="sxs-lookup"><span data-stu-id="07c56-457">(The version 2 assemblies are copied to the *bin* folder in the deployed site.)</span></span>
- <span data-ttu-id="07c56-458">Web Matrix 2 Beta 在站点中包含 Web Pages 版本 2 程序集的版本中使用的站点模板创建的新应用程序*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="07c56-458">New applications that you create using the site templates in Web Matrix version 2 Beta include the Web Pages version 2 assemblies in the site's *bin* folder.</span></span>

<span data-ttu-id="07c56-459">一般情况下，您可以始终控制 Web 页以使用你的网站，通过使用 NuGet 将相应的程序集安装到站点的哪些版本*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="07c56-459">In general, you can always control which version of Web Pages to use with your site by using NuGet to install the appropriate assemblies into the site's *bin* folder.</span></span> <span data-ttu-id="07c56-460">若要查找程序包，请访问[NuGet.org](http://NuGet.org)。</span><span class="sxs-lookup"><span data-stu-id="07c56-460">To find packages, visit [NuGet.org](http://NuGet.org).</span></span>

<a id="mobile"></a>
### <a name="rendering-pages-for-mobile-devices"></a><span data-ttu-id="07c56-461">移动设备的呈现页</span><span class="sxs-lookup"><span data-stu-id="07c56-461">Rendering Pages for Mobile Devices</span></span>

<span data-ttu-id="07c56-462">Web Pages 2 允许您移动或其他设备上创建自定义显示的呈现内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-462">Web Pages 2 lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="07c56-463">`System.Web.WebPages`命名空间包含允许您使用的显示模式的以下类： `DefaultDisplayMode`， `DisplayInfo`，和`DisplayModes`。</span><span class="sxs-lookup"><span data-stu-id="07c56-463">The `System.Web.WebPages` namespace contains the following classes that let you work with display modes: `DefaultDisplayMode`, `DisplayInfo`, and `DisplayModes`.</span></span> <span data-ttu-id="07c56-464">你可以直接使用这些类，并写入呈现特定设备的正确输出的代码。</span><span class="sxs-lookup"><span data-stu-id="07c56-464">You can use these classes directly and write code that renders the right output for specific devices.</span></span>

<span data-ttu-id="07c56-465">或者，可以通过使用此类文件命名模式创建特定于设备的页面：<em>文件名。</em><em>Mobile</em><em>.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="07c56-465">Alternatively, you can create device-specific pages by using a file-naming pattern like this: <em>FileName.</em><em>Mobile</em><em>.cshtml</em>.</span></span> <span data-ttu-id="07c56-466">例如，可以创建两个版本的页上，一个名为<em>MyFile.cshtml</em>另一个名为<em>MyFile.Mobile.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="07c56-466">For example, you can create two versions of a page, one named <em>MyFile.cshtml</em> and one named <em>MyFile.Mobile.cshtml</em>.</span></span> <span data-ttu-id="07c56-467">在运行的时，移动设备的请求时<em>MyFile.cshtml</em>，将从内容呈现在网页<em>MyFile.Mobile.cshtml</em>。</span><span class="sxs-lookup"><span data-stu-id="07c56-467">At run time, when a mobile device requests <em>MyFile.cshtml</em>, Web Pages renders the content from <em>MyFile.Mobile.cshtml</em>.</span></span> <span data-ttu-id="07c56-468">否则为<em>MyFile.cshtml</em>呈现。</span><span class="sxs-lookup"><span data-stu-id="07c56-468">Otherwise, <em>MyFile.cshtml</em> is rendered.</span></span>

<span data-ttu-id="07c56-469">下面的示例演示如何通过添加内容页的移动设备启用移动呈现。</span><span class="sxs-lookup"><span data-stu-id="07c56-469">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="07c56-470">*Page1.cshtml*包含内容，以及导航侧边栏。</span><span class="sxs-lookup"><span data-stu-id="07c56-470">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="07c56-471">*Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。</span><span class="sxs-lookup"><span data-stu-id="07c56-471">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

<span data-ttu-id="07c56-472">若要生成并运行的代码示例：</span><span class="sxs-lookup"><span data-stu-id="07c56-472">To build and run the code sample:</span></span>

1. <span data-ttu-id="07c56-473">在 Web Pages 站点中，创建名为的文件*Page1.cshtml*并复制*Page1.cshtml*到该示例的内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-473">In a Web Pages site, create a file named *Page1.cshtml* and copy the *Page1.cshtml* content into it from the example.</span></span>
2. <span data-ttu-id="07c56-474">创建名为的文件*Page1.Mobile.cshtml*并复制*Page1.Mobile.cshtml*到该示例的内容。</span><span class="sxs-lookup"><span data-stu-id="07c56-474">Create a file named *Page1.Mobile.cshtml* and copy the *Page1.Mobile.cshtml* content into it from the example.</span></span> <span data-ttu-id="07c56-475">请注意，页上的移动版本省略以便更好地呈现在较小屏幕上的导航部分。</span><span class="sxs-lookup"><span data-stu-id="07c56-475">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>
3. <span data-ttu-id="07c56-476">运行桌面浏览器并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="07c56-476">Run a desktop browser and browse to *Page1.cshtml*.</span></span>
4. <span data-ttu-id="07c56-477">运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="07c56-477">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="07c56-478">请注意，这一次 Web 页呈现页的移动版本。</span><span class="sxs-lookup"><span data-stu-id="07c56-478">Notice that this time Web Pages renders the mobile version of the page.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="07c56-479">若要测试移动页面，可以使用在桌面计算机运行的移动设备模拟器。</span><span class="sxs-lookup"><span data-stu-id="07c56-479">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="07c56-480">此工具允许您测试网页，如他们的移动设备上的外观 （即，通常使用小得多显示区域）。</span><span class="sxs-lookup"><span data-stu-id="07c56-480">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="07c56-481">模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/)Mozilla firefox，它可以模拟各种移动浏览器，从桌面版本的 Firefox。</span><span class="sxs-lookup"><span data-stu-id="07c56-481">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<span data-ttu-id="07c56-482">*Page1.cshtml*</span><span class="sxs-lookup"><span data-stu-id="07c56-482">*Page1.cshtml*</span></span>

[!code-html[Main](top-features-in-web-pages-2/samples/sample23.html)]

<span data-ttu-id="07c56-483">*Page1.Mobile.cshtml*</span><span class="sxs-lookup"><span data-stu-id="07c56-483">*Page1.Mobile.cshtml*</span></span>

[!code-html[Main](top-features-in-web-pages-2/samples/sample24.html)]

<span data-ttu-id="07c56-484">*Page1.cshtml*桌面浏览器中呈现：</span><span class="sxs-lookup"><span data-stu-id="07c56-484">*Page1.cshtml* rendered in a desktop browser:</span></span>

<span data-ttu-id="07c56-485">[![topseven-displaymodes-1](top-features-in-web-pages-2/_static/image42.png)](top-features-in-web-pages-2/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-485">[![topseven-displaymodes-1](top-features-in-web-pages-2/_static/image42.png)](top-features-in-web-pages-2/_static/image41.png)</span></span>

<span data-ttu-id="07c56-486">*Page1.Mobile.cshtml* Firefox 浏览器中的 Apple iPhone 模拟器视图中显示。</span><span class="sxs-lookup"><span data-stu-id="07c56-486">*Page1.Mobile.cshtml* displayed in an Apple iPhone simulator view in the Firefox browser.</span></span> <span data-ttu-id="07c56-487">即使该请求是对*Page1.cshtml*，应用程序呈现*Page1.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="07c56-487">Even though the request is to *Page1.cshtml*, the application renders *Page1.Mobile.cshtml*.</span></span>

<span data-ttu-id="07c56-488">[![topseven-displaymodes-2](top-features-in-web-pages-2/_static/image44.png)](top-features-in-web-pages-2/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="07c56-488">[![topseven-displaymodes-2](top-features-in-web-pages-2/_static/image44.png)](top-features-in-web-pages-2/_static/image43.png)</span></span>

<a id="resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="07c56-489">其他资源</span><span class="sxs-lookup"><span data-stu-id="07c56-489">Additional Resources</span></span>

### <a name="aspnet-web-pages-1-resources"></a><span data-ttu-id="07c56-490">ASP.NET Web Pages 1 资源</span><span class="sxs-lookup"><span data-stu-id="07c56-490">ASP.NET Web Pages 1 Resources</span></span>

> [!NOTE]
> <span data-ttu-id="07c56-491">大多数 Web Pages 1 编程和 API 资源仍适用于 Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="07c56-491">Most Web Pages 1 programming and API resources still apply to Web Pages 2.</span></span>

- [<span data-ttu-id="07c56-492">ASP.NET 网页编程简介</span><span class="sxs-lookup"><span data-stu-id="07c56-492">Introduction to ASP.NET Web Pages Programming</span></span>](https://go.microsoft.com/fwlink/?LinkId=202890)

### <a name="webmatrix-resources"></a><span data-ttu-id="07c56-493">WebMatrix 资源</span><span class="sxs-lookup"><span data-stu-id="07c56-493">WebMatrix Resources</span></span>

- [<span data-ttu-id="07c56-494">WebMatrix 2 新增功能</span><span class="sxs-lookup"><span data-stu-id="07c56-494">WebMatrix 2 What's New</span></span>](http://webmatrix.com/next)
- [<span data-ttu-id="07c56-495">Microsoft WebMatrix 站点</span><span class="sxs-lookup"><span data-stu-id="07c56-495">Microsoft WebMatrix Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=195076)
- <span data-ttu-id="07c56-496">[使用 Microsoft WebMatrix 开始 Web 开发](https://msdn.microsoft.com/en-us/library/hh145669(v=VS.99).aspx)（包括完整的示例 Web Pages 应用程序）</span><span class="sxs-lookup"><span data-stu-id="07c56-496">[Starting Web Development with Microsoft WebMatrix](https://msdn.microsoft.com/en-us/library/hh145669(v=VS.99).aspx)(includes a full-length sample Web Pages application)</span></span>
