---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 分析和调试使用 Glimpse 对 ASP.NET MVC 应用程序 |Microsoft Docs
author: Rick-Anderson
description: Glimpse 是一个蓬勃发展和不断增加的开源 NuGet 包提供了详细的性能的系列内容，调试和诊断信息的 ASP.NET...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: f5d174ff6823d654a24dcb2c90f10a3cbd24f1e7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827040"
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="f9552-103">分析和调试使用 Glimpse 对 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="f9552-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>
====================
<span data-ttu-id="f9552-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f9552-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="f9552-105">Glimpse 是一个蓬勃发展和不断增加的开源 NuGet 包提供了详细的性能的系列内容，调试和诊断信息的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9552-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="f9552-106">它是容易安装、 轻量、 超快，并在每一页的底部显示关键性能指标。</span><span class="sxs-lookup"><span data-stu-id="f9552-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="f9552-107">它允许您向下钻取到你的应用时需要了解在服务器上正在运行的内容。</span><span class="sxs-lookup"><span data-stu-id="f9552-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="f9552-108">大致了解提供了我们建议使用整个开发周期，包括 Azure 测试环境很有价值的信息。</span><span class="sxs-lookup"><span data-stu-id="f9552-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="f9552-109">虽然[Fiddler](http://www.telerik.com/fiddler)并[F-12 开发工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供客户端视图，大致了解提供从服务器的详细的视图。</span><span class="sxs-lookup"><span data-stu-id="f9552-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="f9552-110">本教程将重点介绍使用 Glimpse ASP.NET MVC 和 EF 的包，但其他许多包可用。</span><span class="sxs-lookup"><span data-stu-id="f9552-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="f9552-111">在可能的情况将链接到相应[Glimpse docs](http://getglimpse.com/Docs/)我帮助维护。</span><span class="sxs-lookup"><span data-stu-id="f9552-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="f9552-112">Glimpse 是一个开放源代码项目，你也可以参与到源代码和文档。</span><span class="sxs-lookup"><span data-stu-id="f9552-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>


- [<span data-ttu-id="f9552-113">安装概述</span><span class="sxs-lookup"><span data-stu-id="f9552-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="f9552-114">为本地主机启用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="f9552-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="f9552-115">时间线选项卡</span><span class="sxs-lookup"><span data-stu-id="f9552-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="f9552-116">模型绑定</span><span class="sxs-lookup"><span data-stu-id="f9552-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="f9552-117">路由</span><span class="sxs-lookup"><span data-stu-id="f9552-117">Routes</span></span>](#route)
- [<span data-ttu-id="f9552-118">在 Azure 上使用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="f9552-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="f9552-119">其他资源</span><span class="sxs-lookup"><span data-stu-id="f9552-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="f9552-120">安装概述</span><span class="sxs-lookup"><span data-stu-id="f9552-120">Installing Glimpse</span></span>

<span data-ttu-id="f9552-121">你可以从 NuGet 包管理器控制台或安装 Glimpse**管理 NuGet 包**控制台。</span><span class="sxs-lookup"><span data-stu-id="f9552-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="f9552-122">对于此演示，我将安装 Mvc5 和 EF6 包：</span><span class="sxs-lookup"><span data-stu-id="f9552-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![从 NuGet Dlg 安装概述](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="f9552-124">搜索*Glimpse.EF*</span><span class="sxs-lookup"><span data-stu-id="f9552-124">Search for *Glimpse.EF*</span></span>

![从 NuGet 安装 dlg Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="f9552-126">通过选择**已安装的包**，可以看到安装 Glimpse 依赖模块：</span><span class="sxs-lookup"><span data-stu-id="f9552-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![从 DLg 安装 Glimpse 包](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="f9552-128">以下命令从包管理器控制台安装 Glimpse MVC5 和 EF6 模块：</span><span class="sxs-lookup"><span data-stu-id="f9552-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="f9552-129">为本地主机启用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="f9552-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="f9552-130">导航到 http://localhost:&lt; 端口号&gt;/glimpse.axd，然后单击<strong>上打开 Glimpse</strong>按钮。</span><span class="sxs-lookup"><span data-stu-id="f9552-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Glimpse axd 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="f9552-132">如果必须显示在收藏夹栏，您可以拖放 Glimpse 按钮，将其添加为 bookmarklets:</span><span class="sxs-lookup"><span data-stu-id="f9552-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![使用 Glimpse boookmarklets IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="f9552-134">你现在可以导航您的应用程序，并**Heads 平视显示**(HUD) 显示在页面底部。</span><span class="sxs-lookup"><span data-stu-id="f9552-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![联系人管理器页的 HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="f9552-136">[Glimpse HUD 页](http://getglimpse.com/Docs/Heads-up-Display)详细介绍上面所示的计时信息。</span><span class="sxs-lookup"><span data-stu-id="f9552-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="f9552-137">非介入式性能数据 HUD 显示可以立即发出通知的问题的测试周期到开始之前。</span><span class="sxs-lookup"><span data-stu-id="f9552-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="f9552-138">单击&quot;g&quot;在右下角将显示概述面板：</span><span class="sxs-lookup"><span data-stu-id="f9552-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![概述面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="f9552-140">在上面，图像中[选项卡执行](http://getglimpse.com/Docs/Execution-Tab)选择后，管道中显示的操作和筛选器的计时详细信息。</span><span class="sxs-lookup"><span data-stu-id="f9552-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="f9552-141">您可以看到我[停止监视筛选器计时器](http://www.nuget.org/packages/StopWatch/)开始管道阶段 6。</span><span class="sxs-lookup"><span data-stu-id="f9552-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="f9552-142">虽然我轻量计时器可提供有用的配置文件/计时数据，它未命中数和在授权中所用的呈现视图的所有时间。</span><span class="sxs-lookup"><span data-stu-id="f9552-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="f9552-143">你可以阅读我在计时器[配置文件和时间在 ASP.NET MVC 应用程序到 Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f9552-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="f9552-144">[选项卡](http://getglimpse.com/Docs/Tabs)页提供有关每个选项卡的详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="f9552-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="f9552-145">时间线选项卡</span><span class="sxs-lookup"><span data-stu-id="f9552-145">The Timeline tab</span></span>

<span data-ttu-id="f9552-146">我已修改 Tom Dykstra 的未完成[EF 6/MVC 5 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)用下面的代码将更改为讲师控制器：</span><span class="sxs-lookup"><span data-stu-id="f9552-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="f9552-147">上面的代码可以在查询字符串中传入 (`eager`) 控制预先或显式加载的数据。</span><span class="sxs-lookup"><span data-stu-id="f9552-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="f9552-148">在下图中，使用显式加载和计时页面将显示每个注册中加载`Index`操作方法：</span><span class="sxs-lookup"><span data-stu-id="f9552-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![Explicit Loading — 显式加载](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="f9552-150">在下面的代码中，指定预先，并且每个注册提取后`Index`视图称为：</span><span class="sxs-lookup"><span data-stu-id="f9552-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![指定预先](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="f9552-152">你可以悬停在时间段，以获取详细的计时信息：</span><span class="sxs-lookup"><span data-stu-id="f9552-152">You can hover over a time segment to get detailed timing information:</span></span>

![悬停鼠标以查看详细的计时](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="f9552-154">模型绑定</span><span class="sxs-lookup"><span data-stu-id="f9552-154">Model Binding</span></span>

<span data-ttu-id="f9552-155">[模型绑定选项卡](http://getglimpse.com/Docs/Model-Binding-Tab)提供了丰富的信息可帮助你了解如何绑定窗体变量，为什么某些不能绑定如所料。</span><span class="sxs-lookup"><span data-stu-id="f9552-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="f9552-156">下的图显示 **？**</span><span class="sxs-lookup"><span data-stu-id="f9552-156">The image below shows the **?**</span></span> <span data-ttu-id="f9552-157">图标，你可以单击以打开该功能的初步了解帮助页。</span><span class="sxs-lookup"><span data-stu-id="f9552-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![大致了解模型绑定查看](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="f9552-159">路由</span><span class="sxs-lookup"><span data-stu-id="f9552-159">Routes</span></span>

 <span data-ttu-id="f9552-160">大致了解路由选项卡将可以帮助你调试和了解路由。</span><span class="sxs-lookup"><span data-stu-id="f9552-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="f9552-161">下图中的产品路由选择 （和其显示为绿色，大致了解约定）。</span><span class="sxs-lookup"><span data-stu-id="f9552-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="f9552-162">![所选的产品名称](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png)路由约束、 区域和数据令牌也会显示。</span><span class="sxs-lookup"><span data-stu-id="f9552-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="f9552-163">请参阅[大致了解路由](http://getglimpse.com/Docs/Routes-Tab)并[ASP.NET MVC 5 中的属性路由](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="f9552-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="f9552-164">在 Azure 上使用 Glimpse</span><span class="sxs-lookup"><span data-stu-id="f9552-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="f9552-165">大致了解默认安全策略只允许要在本地主机显示的大致了解数据。</span><span class="sxs-lookup"><span data-stu-id="f9552-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="f9552-166">您可以更改此安全策略，以便您可以查看此数据 （如 Azure 上的 web 应用） 的远程服务器上。</span><span class="sxs-lookup"><span data-stu-id="f9552-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="f9552-167">在 Azure 上的测试环境，将添加到底部的突出显示的标记*web.confg*文件以启用初步了解：</span><span class="sxs-lookup"><span data-stu-id="f9552-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.confg* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="f9552-168">与此项更改就，任何用户可以在远程站点上查看你大致了解数据。</span><span class="sxs-lookup"><span data-stu-id="f9552-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="f9552-169">考虑将上面的标记添加到发布配置文件，因此它仅部署应用时使用该发布配置文件 (例如，在 Azure 测试 proifle。)若要限制大致了解数据，我们将添加`canViewGlimpseData`角色和仅允许此角色，以查看大致了解数据的用户。</span><span class="sxs-lookup"><span data-stu-id="f9552-169">Consider adding the markup above to a publish profile so it's only deployed an applyed when you use that publish profile (for example, your Azure test proifle.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="f9552-170">删除从注释*GlimpseSecurityPolicy.cs*文件，并更改[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)从调用`Administrator`到`canViewGlimpseData`角色：</span><span class="sxs-lookup"><span data-stu-id="f9552-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="f9552-171">安全性-大致了解提供的丰富数据可能会暴露您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="f9552-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="f9552-172">Microsoft 未执行安全审核的大致了解用于生产应用。</span><span class="sxs-lookup"><span data-stu-id="f9552-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>


<span data-ttu-id="f9552-173">添加角色的信息，请参阅我[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 web 应用部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教程。</span><span class="sxs-lookup"><span data-stu-id="f9552-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="f9552-174">其他资源</span><span class="sxs-lookup"><span data-stu-id="f9552-174">Additional Resources</span></span>

- [<span data-ttu-id="f9552-175">将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f9552-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="f9552-176">[Glimpse 配置](http://getglimpse.com/Docs/Configuration)-文档页上配置的选项卡中，运行时策略、 日志记录和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f9552-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
