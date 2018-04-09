---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 配置文件和调试使用 Glimpse 对 ASP.NET MVC 应用程序 |Microsoft 文档
author: Rick-Anderson
description: Glimpse 是一个获得成功和增长的开放源 NuGet 包的系列，提供详细的性能、 调试和诊断信息的 ASP.NET...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: 6ac23256c57116de81c7bf690d5ce743301c75ce
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="06795-103">配置文件和调试使用 Glimpse 对 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="06795-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>
====================
<span data-ttu-id="06795-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="06795-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="06795-105">Glimpse 是获得成功和增长的开放源 NuGet 包的系列，提供详细的性能、 调试和诊断信息的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="06795-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="06795-106">它是普通安装、 轻量、 超快速，并在每一页的底部显示关键性能指标。</span><span class="sxs-lookup"><span data-stu-id="06795-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="06795-107">它允许你向下钻取到你的应用时需要先找出在服务器上正在运行的内容。</span><span class="sxs-lookup"><span data-stu-id="06795-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="06795-108">Glimpse 提供更重要的信息，我们建议你在整个开发周期中，包括你的 Azure 测试环境使用。</span><span class="sxs-lookup"><span data-stu-id="06795-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="06795-109">虽然[Fiddler](http://www.telerik.com/fiddler)和[F-12 开发工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供客户端视图，Glimpse 提供从服务器的详细的视图。</span><span class="sxs-lookup"><span data-stu-id="06795-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="06795-110">本教程将着重介绍如何使用 Glimpse ASP.NET MVC 和 EF 包，但其他许多包都可用。</span><span class="sxs-lookup"><span data-stu-id="06795-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="06795-111">尽可能将链接到相应[转让文档](http://getglimpse.com/Docs/)其中我要帮助维护。</span><span class="sxs-lookup"><span data-stu-id="06795-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="06795-112">Glimpse 是一个开源项目，你太可参与源代码和文档。</span><span class="sxs-lookup"><span data-stu-id="06795-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>


- [<span data-ttu-id="06795-113">安装 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="06795-114">为本地主机启用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="06795-115">时间线选项卡</span><span class="sxs-lookup"><span data-stu-id="06795-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="06795-116">模型绑定</span><span class="sxs-lookup"><span data-stu-id="06795-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="06795-117">路由</span><span class="sxs-lookup"><span data-stu-id="06795-117">Routes</span></span>](#route)
- [<span data-ttu-id="06795-118">在 Azure 上使用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="06795-119">其他资源</span><span class="sxs-lookup"><span data-stu-id="06795-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="06795-120">安装 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-120">Installing Glimpse</span></span>

<span data-ttu-id="06795-121">你可以从 NuGet 包管理器控制台或从安装 Glimpse**管理 NuGet 包**控制台。</span><span class="sxs-lookup"><span data-stu-id="06795-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="06795-122">对于本演示中，我将的 Mvc5 和 ef6 更高版本的包进行安装：</span><span class="sxs-lookup"><span data-stu-id="06795-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![从 NuGet Dlg 安装 Glimpse](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="06795-124">搜索*Glimpse.EF*</span><span class="sxs-lookup"><span data-stu-id="06795-124">Search for *Glimpse.EF*</span></span>

![从 NuGet 安装 dlg Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="06795-126">通过选择**安装包**，你可以查看安装的 Glimpse 依赖模块：</span><span class="sxs-lookup"><span data-stu-id="06795-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![从 DLg 安装 Glimpse 包](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="06795-128">以下命令从包管理器控制台安装 Glimpse MVC5 和从 EF6 模块：</span><span class="sxs-lookup"><span data-stu-id="06795-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="06795-129">为本地主机启用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="06795-130">导航到http://localhost:&lt;端口号&gt;/glimpse.axd 和单击<strong>打开 Glimpse 上</strong>按钮。</span><span class="sxs-lookup"><span data-stu-id="06795-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Glimpse axd 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="06795-132">如果您有收藏夹栏显示，可以拖放 Glimpse 按钮，将其添加为 bookmarklets:</span><span class="sxs-lookup"><span data-stu-id="06795-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![与 Glimpse boookmarklets 的 IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="06795-134">你现在可以导航到你的应用，和**磁头向上显示**(HUD) 显示在页面底部。</span><span class="sxs-lookup"><span data-stu-id="06795-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD 联系人管理器页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="06795-136">[Glimpse HUD 页](http://getglimpse.com/Docs/Heads-up-Display)详细说明了上面所示的计时信息。</span><span class="sxs-lookup"><span data-stu-id="06795-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="06795-137">非介入式性能数据 HUD 显示可以通知你的问题立即-之前到测试周期，将出现。</span><span class="sxs-lookup"><span data-stu-id="06795-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="06795-138">单击&quot;g&quot;右下角中会显示 Glimpse 面板：</span><span class="sxs-lookup"><span data-stu-id="06795-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Glimpse 面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="06795-140">在上图中，[执行选项卡](http://getglimpse.com/Docs/Execution-Tab)选择时，它显示在管道中的操作和筛选器的计时详细信息。</span><span class="sxs-lookup"><span data-stu-id="06795-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="06795-141">你可以看到我[停止监视筛选器计时器](http://www.nuget.org/packages/StopWatch/)开始管道的阶段 6。</span><span class="sxs-lookup"><span data-stu-id="06795-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="06795-142">虽然我轻型计时器都可以提供有用的配置文件/计时数据，则它未命中所用的授权和呈现的视图的所有时间。</span><span class="sxs-lookup"><span data-stu-id="06795-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="06795-143">你可以阅读我计时器在[配置文件和时间 ASP.NET MVC 应用程序向 Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06795-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="06795-144">[选项卡](http://getglimpse.com/Docs/Tabs)页提供了每个选项卡的详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="06795-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="06795-145">时间线选项卡</span><span class="sxs-lookup"><span data-stu-id="06795-145">The Timeline tab</span></span>

<span data-ttu-id="06795-146">我已修改 Tom Dykstra 的未完成[EF 6/MVC 5 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)替换为以下代码将更改为教师控制器：</span><span class="sxs-lookup"><span data-stu-id="06795-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="06795-147">上面的代码中允许我在查询字符串中传递 (`eager`) 控制 eager 或显式加载的数据。</span><span class="sxs-lookup"><span data-stu-id="06795-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="06795-148">在下图中，使用显式加载和计时页显示中加载每个注册`Index`操作方法：</span><span class="sxs-lookup"><span data-stu-id="06795-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![Explicit Loading — 显式加载](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="06795-150">在下面的代码中，指定 eager，并且每个注册提取后`Index`视图称为：</span><span class="sxs-lookup"><span data-stu-id="06795-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![指定 eager](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="06795-152">你可以将鼠标悬停在某个时间段，可获取详细的计时信息：</span><span class="sxs-lookup"><span data-stu-id="06795-152">You can hover over a time segment to get detailed timing information:</span></span>

![悬停鼠标以查看详细的计时](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="06795-154">模型绑定</span><span class="sxs-lookup"><span data-stu-id="06795-154">Model Binding</span></span>

<span data-ttu-id="06795-155">[模型绑定选项卡](http://getglimpse.com/Docs/Model-Binding-Tab)提供丰富的信息来帮助你了解为何某些未被绑定如所料，窗体变量的绑定方式。</span><span class="sxs-lookup"><span data-stu-id="06795-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="06795-156">下面的图像显示**？**</span><span class="sxs-lookup"><span data-stu-id="06795-156">The image below shows the **?**</span></span> <span data-ttu-id="06795-157">图标，你可以单击以打开该功能的 glimpse 帮助页。</span><span class="sxs-lookup"><span data-stu-id="06795-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![glimpse 模型绑定视图](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="06795-159">路由</span><span class="sxs-lookup"><span data-stu-id="06795-159">Routes</span></span>

 <span data-ttu-id="06795-160">Glimpse 路由选项卡将可以帮助你调试和了解路由。</span><span class="sxs-lookup"><span data-stu-id="06795-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="06795-161">在下图中，将选择的产品路由 （以及它会显示为绿色，Glimpse 约定）。</span><span class="sxs-lookup"><span data-stu-id="06795-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="06795-162">![所选的产品名称](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png)路由约束、 区域和数据令牌也会显示。</span><span class="sxs-lookup"><span data-stu-id="06795-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="06795-163">请参阅[Glimpse 路由](http://getglimpse.com/Docs/Routes-Tab)和[ASP.NET MVC 5 中的属性路由](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="06795-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="06795-164">在 Azure 上使用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="06795-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="06795-165">Glimpse 默认安全策略只允许 Glimpse 数据显示本地主机。</span><span class="sxs-lookup"><span data-stu-id="06795-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="06795-166">你可以更改此安全策略，以便你可以查看此数据 （例如，在 Azure 上 web 应用程序） 的远程服务器上。</span><span class="sxs-lookup"><span data-stu-id="06795-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="06795-167">在 Azure 上的测试环境，添加到底部的突出显示的标记*web.confg*文件以启用 Glimpse:</span><span class="sxs-lookup"><span data-stu-id="06795-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.confg* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="06795-168">进行单独此更改后，任何用户都可以在远程站点上看到你 Glimpse 的数据。</span><span class="sxs-lookup"><span data-stu-id="06795-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="06795-169">考虑将上面的标记添加到发布配置文件，以便它仅部署应用时使用该发布配置文件 (例如，你 Azure 测试 proifle。)若要限制 Glimpse 数据，我们将添加`canViewGlimpseData`角色，并仅允许此角色来查看 Glimpse 数据中的用户。</span><span class="sxs-lookup"><span data-stu-id="06795-169">Consider adding the markup above to a publish profile so it's only deployed an applyed when you use that publish profile (for example, your Azure test proifle.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="06795-170">删除从注释*GlimpseSecurityPolicy.cs*文件并将更改[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)从调用`Administrator`到`canViewGlimpseData`角色：</span><span class="sxs-lookup"><span data-stu-id="06795-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="06795-171">安全-Glimpse 提供的丰富数据无法公开您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="06795-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="06795-172">Microsoft 不具有对生产应用程序用于执行 Glimpse 安全审核。</span><span class="sxs-lookup"><span data-stu-id="06795-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>


<span data-ttu-id="06795-173">有关添加角色的信息，请参阅我[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 web 应用程序部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教程。</span><span class="sxs-lookup"><span data-stu-id="06795-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="06795-174">其他资源</span><span class="sxs-lookup"><span data-stu-id="06795-174">Additional Resources</span></span>

- [<span data-ttu-id="06795-175">将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用程序部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="06795-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="06795-176">[转让配置](http://getglimpse.com/Docs/Configuration)-配置选项卡、 运行时策略、 日志记录和的详细信息的文档页。</span><span class="sxs-lookup"><span data-stu-id="06795-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
