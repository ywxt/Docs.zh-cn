---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: ASP.NET MVC 中使用不同版本的 IIS (C#) |Microsoft Docs
author: microsoft
description: 在本教程中，您将学习如何使用 ASP.NET MVC 中，并且 URL 路由，使用不同版本的 Internet Information Services。 了解不同的策略...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: ddf7bc4548099ba5d95b4c0bb6f94a31ab38beb6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371721"
---
<a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="20fbc-104">ASP.NET MVC 中使用不同版本的 IIS (C#)</span><span class="sxs-lookup"><span data-stu-id="20fbc-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>
====================
<span data-ttu-id="20fbc-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="20fbc-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="20fbc-106">在本教程中，您将学习如何使用 ASP.NET MVC 中，并且 URL 路由，使用不同版本的 Internet Information Services。</span><span class="sxs-lookup"><span data-stu-id="20fbc-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="20fbc-107">了解 ASP.NET MVC 中使用的 IIS 7.0 （经典模式）、 IIS 6.0 和 IIS 的早期版本不同的策略。</span><span class="sxs-lookup"><span data-stu-id="20fbc-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>


<span data-ttu-id="20fbc-108">ASP.NET MVC 框架会在 ASP.NET 路由取决于浏览器请求路由到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="20fbc-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="20fbc-109">为了充分利用 ASP.NET 路由，您可能需要在 web 服务器上执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="20fbc-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="20fbc-110">这完全取决于 Internet 信息服务 (IIS) 和请求处理你的应用程序的模式下的版本。</span><span class="sxs-lookup"><span data-stu-id="20fbc-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="20fbc-111">下面是不同版本的 IIS 的摘要：</span><span class="sxs-lookup"><span data-stu-id="20fbc-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="20fbc-112">IIS 7.0 （集成模式）-使用 ASP.NET 路由所需任何特殊配置。</span><span class="sxs-lookup"><span data-stu-id="20fbc-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="20fbc-113">IIS 7.0 （经典模式）-你需要执行特殊的配置以使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="20fbc-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="20fbc-114">IIS 6.0 或下面-你需要执行特殊的配置以使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="20fbc-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="20fbc-115">IIS 的最新版本是版本 7.5 （在 Win7)。</span><span class="sxs-lookup"><span data-stu-id="20fbc-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="20fbc-116">IIS 7 的 IIS 是包含 Windows Server 2008 和 VISTA/SP1 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="20fbc-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="20fbc-117">也可以安装任意版本的 Vista 操作系统，除 Home Basic 上的 IIS 7.0 (请参阅[ https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx ](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx))。</span><span class="sxs-lookup"><span data-stu-id="20fbc-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="20fbc-118">IIS 7.0 支持两种模式，用于处理请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="20fbc-119">可以使用集成模式下或经典模式。</span><span class="sxs-lookup"><span data-stu-id="20fbc-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="20fbc-120">您不必执行任何特殊配置步骤，使用 IIS 7.0 集成模式下时。</span><span class="sxs-lookup"><span data-stu-id="20fbc-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="20fbc-121">但是，您确实需要在经典模式下使用 IIS 7.0 时执行其他配置。</span><span class="sxs-lookup"><span data-stu-id="20fbc-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="20fbc-122">Microsoft Windows Server 2003 包括 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="20fbc-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="20fbc-123">使用 Windows Server 2003 操作系统时，您不能升级到 IIS 7.0 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="20fbc-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="20fbc-124">使用 IIS 6.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="20fbc-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="20fbc-125">Microsoft Windows XP Professional 包括 IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="20fbc-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="20fbc-126">使用 IIS 5.1 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="20fbc-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="20fbc-127">最后，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包括 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="20fbc-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="20fbc-128">使用 IIS 5.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="20fbc-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="20fbc-129">与经典模式集成</span><span class="sxs-lookup"><span data-stu-id="20fbc-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="20fbc-130">IIS 7.0 可以处理请求使用两种不同的请求处理模式： 集成和经典。</span><span class="sxs-lookup"><span data-stu-id="20fbc-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="20fbc-131">集成模式下提供更好的性能和更多的功能。</span><span class="sxs-lookup"><span data-stu-id="20fbc-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="20fbc-132">经典模式下所包含的向后与 IIS 的早期版本的兼容性。</span><span class="sxs-lookup"><span data-stu-id="20fbc-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="20fbc-133">请求处理模式取决于应用程序池。</span><span class="sxs-lookup"><span data-stu-id="20fbc-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="20fbc-134">您可以确定特定的 web 应用程序通过确定与应用程序相关联的应用程序池使用的处理模式。</span><span class="sxs-lookup"><span data-stu-id="20fbc-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="20fbc-135">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="20fbc-135">Follow these steps:</span></span>

1. <span data-ttu-id="20fbc-136">启动 Internet 信息服务管理器</span><span class="sxs-lookup"><span data-stu-id="20fbc-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="20fbc-137">在连接窗口中，选择一个应用程序</span><span class="sxs-lookup"><span data-stu-id="20fbc-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="20fbc-138">在操作窗口中，单击**基本设置**链接以打开编辑应用程序对话框 （请参见图 1）</span><span class="sxs-lookup"><span data-stu-id="20fbc-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="20fbc-139">记下所选的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="20fbc-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="20fbc-140">默认情况下，IIS 配置为支持两个应用程序池： **DefaultAppPool**并**Classic.NET AppPool**。</span><span class="sxs-lookup"><span data-stu-id="20fbc-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="20fbc-141">如果选择了 DefaultAppPool，然后在集成的请求处理模式下运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="20fbc-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="20fbc-142">如果选择了经典的.NET 应用程序池，你的应用程序在经典的请求处理模式下运行。</span><span class="sxs-lookup"><span data-stu-id="20fbc-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="20fbc-143">[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="20fbc-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="20fbc-144">**图 1**： 检测请求处理模式 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="20fbc-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="20fbc-145">请注意，您可以修改在编辑应用程序对话框中的请求处理模式。</span><span class="sxs-lookup"><span data-stu-id="20fbc-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="20fbc-146">单击选择按钮，并将更改应用程序与关联的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="20fbc-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="20fbc-147">认识到从经典部署模型的 ASP.NET 应用程序更改为集成模式下时有兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="20fbc-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="20fbc-148">有关详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="20fbc-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="20fbc-149">升级到 Windows Vista 和 Windows Server 2008--上的 IIS 7.0 的 ASP.NET 1.1 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="20fbc-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="20fbc-150">使用 IIS 7.0 的 ASP.NET 集成 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="20fbc-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="20fbc-151">如果 ASP.NET 应用程序使用 DefaultAppPool，您不需要执行任何其他步骤以获得 ASP.NET 路由 （以及因此 ASP.NET MVC） 工作。</span><span class="sxs-lookup"><span data-stu-id="20fbc-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="20fbc-152">但是，如果 ASP.NET 应用程序配置为使用 Classic.NET AppPool 然后往下读，则必须多工作要做。</span><span class="sxs-lookup"><span data-stu-id="20fbc-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="20fbc-153">通过较旧版本的 IIS 使用 ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="20fbc-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="20fbc-154">如果您需要使用 IIS 7.0 比旧版本的 IIS 使用 ASP.NET MVC 或需要在经典模式下使用 IIS 7.0，则必须使用两个选项。</span><span class="sxs-lookup"><span data-stu-id="20fbc-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="20fbc-155">首先，您可以修改要使用文件扩展名的路由表。</span><span class="sxs-lookup"><span data-stu-id="20fbc-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="20fbc-156">例如，而不是请求的 URL，如 /Store/Details，将请求的 URL，如 /Store.aspx/Details。</span><span class="sxs-lookup"><span data-stu-id="20fbc-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="20fbc-157">第二个选项是创建所谓*通配符脚本映射*。</span><span class="sxs-lookup"><span data-stu-id="20fbc-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="20fbc-158">通配符脚本映射，可将每个请求映射到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="20fbc-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="20fbc-159">如果你无权访问你的 web 服务器 (例如，应用程序托管的 Internet 服务提供商在 ASP.NET MVC) 到你将需要使用第一个选项。</span><span class="sxs-lookup"><span data-stu-id="20fbc-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="20fbc-160">如果不想要修改的 Url 中，外观，并且可以访问你的 web 服务器，您可以使用第二个选项。</span><span class="sxs-lookup"><span data-stu-id="20fbc-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="20fbc-161">我们将探讨以下各节详细地每个选项。</span><span class="sxs-lookup"><span data-stu-id="20fbc-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="20fbc-162">将扩展添加到路由表</span><span class="sxs-lookup"><span data-stu-id="20fbc-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="20fbc-163">若要获取 ASP.NET 路由，以使用较旧版本的 IIS 的最简单方法是修改您在 Global.asax 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="20fbc-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="20fbc-164">默认值，并在列表 1 中的未修改的 Global.asax 文件将配置一个名为默认路由的路由。</span><span class="sxs-lookup"><span data-stu-id="20fbc-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="20fbc-165">**代码清单 1-Global.asax （未修改）**</span><span class="sxs-lookup"><span data-stu-id="20fbc-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="20fbc-166">在列表 1 中配置的默认路由，可以如下所示的路由 Url:</span><span class="sxs-lookup"><span data-stu-id="20fbc-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="20fbc-167">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="20fbc-167">/Home/Index</span></span>

<span data-ttu-id="20fbc-168">/ 产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="20fbc-168">/Product/Details/3</span></span>

<span data-ttu-id="20fbc-169">/ 产品</span><span class="sxs-lookup"><span data-stu-id="20fbc-169">/Product</span></span>

<span data-ttu-id="20fbc-170">遗憾的是，较旧版本的 IIS 不会将这些请求传递给 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="20fbc-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="20fbc-171">因此，不会将这些请求路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="20fbc-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="20fbc-172">例如，如果浏览器请求进行 URL /Home/索引然后将图 2 中显示错误页。</span><span class="sxs-lookup"><span data-stu-id="20fbc-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="20fbc-173">[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="20fbc-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="20fbc-174">**图 2**： 接收到 404 找不到错误 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="20fbc-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="20fbc-175">较旧版本的 IIS 只能映射到 ASP.NET 框架的某些请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="20fbc-176">对于带有正确的文件扩展名的 URL 必须为该请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="20fbc-177">例如，对于 /SomePage.aspx 请求获取映射到 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="20fbc-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="20fbc-178">但是，对于 /SomePage.htm 请求却没有。</span><span class="sxs-lookup"><span data-stu-id="20fbc-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="20fbc-179">因此，若要获取以便使用 ASP.NET 路由，我们必须修改默认路由，使之包含映射到 ASP.NET 框架的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="20fbc-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="20fbc-180">这是使用名为的脚本`registermvc.wsf`。</span><span class="sxs-lookup"><span data-stu-id="20fbc-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="20fbc-181">它是 ASP.NET MVC 1 版本中附带`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`，但自 ASP.NET 2 起此脚本已被移动到 ASP.NET Futures，网址[ http://aspnet.codeplex.com/releases/view/39978 ](http://aspnet.codeplex.com/releases/view/39978)。</span><span class="sxs-lookup"><span data-stu-id="20fbc-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="20fbc-182">执行此脚本向 IIS 注册一个新的.mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="20fbc-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="20fbc-183">注册.mvc 扩展后，可以修改路由在 Global.asax 文件中的，以便路由使用.mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="20fbc-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="20fbc-184">列表 2 中已修改的 Global.asax 文件适用于较旧版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="20fbc-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="20fbc-185">**代码清单 2-Global.asax （修改与扩展）**</span><span class="sxs-lookup"><span data-stu-id="20fbc-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="20fbc-186">**重要**： 请记住要更改的 Global.asax 文件后，再次构建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="20fbc-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="20fbc-187">有两个代码清单 2 中的 Global.asax 文件的重要更改。</span><span class="sxs-lookup"><span data-stu-id="20fbc-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="20fbc-188">现在有两个路由在 Global.asax 中定义。</span><span class="sxs-lookup"><span data-stu-id="20fbc-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="20fbc-189">现在，默认路由，第一个路由的 URL 模式如下所示：</span><span class="sxs-lookup"><span data-stu-id="20fbc-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="20fbc-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="20fbc-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="20fbc-191">.Mvc 扩展添加更改的 ASP.NET 路由模块截获的文件的类型。</span><span class="sxs-lookup"><span data-stu-id="20fbc-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="20fbc-192">进行此更改后，ASP.NET MVC 应用程序现在将如下所示的请求路由：</span><span class="sxs-lookup"><span data-stu-id="20fbc-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="20fbc-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="20fbc-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="20fbc-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="20fbc-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="20fbc-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="20fbc-195">/Product.mvc/</span></span>

<span data-ttu-id="20fbc-196">第二个路由，根路由是新增的。</span><span class="sxs-lookup"><span data-stu-id="20fbc-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="20fbc-197">根路由此 URL 模式是空字符串。</span><span class="sxs-lookup"><span data-stu-id="20fbc-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="20fbc-198">此路由是必需的匹配对应用程序的根目录发出的请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="20fbc-199">例如，根路由将匹配的请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="20fbc-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="20fbc-200">路由表对这些修改后，将需要确保所有应用程序中的链接是使用这些新的 URL 模式兼容。</span><span class="sxs-lookup"><span data-stu-id="20fbc-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="20fbc-201">换而言之，请确保您的所有链接包含.mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="20fbc-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="20fbc-202">如果您使用 Html.ActionLink() 帮助器方法生成你的链接，然后不应需要进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="20fbc-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="20fbc-203">而不是使用 registermvc.wcf 脚本，可以将一个新的扩展添加到手动映射到 ASP.NET 框架的 IIS。</span><span class="sxs-lookup"><span data-stu-id="20fbc-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="20fbc-204">在自行添加一个新的扩展，请确保相应的复选框标记为**验证该文件是否存在**未选中。</span><span class="sxs-lookup"><span data-stu-id="20fbc-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="20fbc-205">托管的服务器</span><span class="sxs-lookup"><span data-stu-id="20fbc-205">Hosted Server</span></span>

<span data-ttu-id="20fbc-206">您始终没有访问你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="20fbc-206">You don't always have access to your web server.</span></span> <span data-ttu-id="20fbc-207">例如，如果托管的 ASP.NET MVC 应用程序中使用的 Internet 托管提供者，然后将不一定可以访问到 IIS。</span><span class="sxs-lookup"><span data-stu-id="20fbc-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="20fbc-208">在这种情况下，应使用一个映射到 ASP.NET framework 的现有文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="20fbc-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="20fbc-209">文件扩展名映射到 ASP.NET 的示例包括.aspx、.axd 和.ashx 扩展。</span><span class="sxs-lookup"><span data-stu-id="20fbc-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="20fbc-210">例如，修改后的 Global.asax 文件中列出的 3 使用.aspx 扩展名而不是.mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="20fbc-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="20fbc-211">**代码清单 3-Global.asax （使用.aspx 扩展修改）**</span><span class="sxs-lookup"><span data-stu-id="20fbc-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="20fbc-212">列表 3 中的 Global.asax 文件正是除外，它使用.aspx 扩展名而非.mvc 扩展这一事实的上一个 Global.asax 文件同名。</span><span class="sxs-lookup"><span data-stu-id="20fbc-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="20fbc-213">您无需使用.aspx 扩展名在远程 web 服务器上执行任何设置。</span><span class="sxs-lookup"><span data-stu-id="20fbc-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="20fbc-214">创建通配符脚本映射</span><span class="sxs-lookup"><span data-stu-id="20fbc-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="20fbc-215">如果不想要修改 ASP.NET MVC 应用程序的 Url，并且可以访问你的 web 服务器，则必须使用一个附加选项。</span><span class="sxs-lookup"><span data-stu-id="20fbc-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="20fbc-216">可以创建映射到 ASP.NET 框架的 web 服务器的所有请求的通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="20fbc-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="20fbc-217">这样一来，您可以使用默认 ASP.NET MVC 路由表与 IIS 7.0 （在经典模式下） 或 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="20fbc-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="20fbc-218">请注意，此选项会导致 IIS 以截获对 web 服务器发出的每个请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="20fbc-219">这包括图像、 经典 ASP 页中和 HTML 页面的请求。</span><span class="sxs-lookup"><span data-stu-id="20fbc-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="20fbc-220">因此，启用通配符脚本映射到 ASP.NET does 会影响性能。</span><span class="sxs-lookup"><span data-stu-id="20fbc-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="20fbc-221">下面是如何为 IIS 7.0 中启用通配符脚本映射：</span><span class="sxs-lookup"><span data-stu-id="20fbc-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="20fbc-222">在连接窗口中选择你的应用程序</span><span class="sxs-lookup"><span data-stu-id="20fbc-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="20fbc-223">请确保**功能**选择视图</span><span class="sxs-lookup"><span data-stu-id="20fbc-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="20fbc-224">双击**处理程序映射**按钮</span><span class="sxs-lookup"><span data-stu-id="20fbc-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="20fbc-225">单击**添加通配符脚本映射**链接 （请参见图 3）</span><span class="sxs-lookup"><span data-stu-id="20fbc-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="20fbc-226">将路径输入到 aspnet\_isapi.dll 文件 （这可以从 PageHandlerFactory 脚本映射中复制此路径）</span><span class="sxs-lookup"><span data-stu-id="20fbc-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="20fbc-227">输入名称 MVC</span><span class="sxs-lookup"><span data-stu-id="20fbc-227">Enter the name MVC</span></span>
7. <span data-ttu-id="20fbc-228">单击**确定**按钮</span><span class="sxs-lookup"><span data-stu-id="20fbc-228">Click the **OK** button</span></span>

<span data-ttu-id="20fbc-229">[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="20fbc-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="20fbc-230">**图 3**： 使用 IIS 7.0 创建通配符脚本映射 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="20fbc-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="20fbc-231">请按照以下步骤来使用 IIS 6.0 创建通配符脚本映射操作：</span><span class="sxs-lookup"><span data-stu-id="20fbc-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="20fbc-232">右键单击网站，然后选择属性</span><span class="sxs-lookup"><span data-stu-id="20fbc-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="20fbc-233">选择**主目录**选项卡</span><span class="sxs-lookup"><span data-stu-id="20fbc-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="20fbc-234">单击**配置**按钮</span><span class="sxs-lookup"><span data-stu-id="20fbc-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="20fbc-235">选择**映射**选项卡</span><span class="sxs-lookup"><span data-stu-id="20fbc-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="20fbc-236">单击**插入**按钮 （请参见图 4）</span><span class="sxs-lookup"><span data-stu-id="20fbc-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="20fbc-237">粘贴到 aspnet 路径\_isapi.dll 到可执行文件的字段 （.aspx 文件的脚本映射可将此路径的复制）</span><span class="sxs-lookup"><span data-stu-id="20fbc-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="20fbc-238">取消选中复选框标记为**验证该文件是否存在**</span><span class="sxs-lookup"><span data-stu-id="20fbc-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="20fbc-239">单击**确定**按钮</span><span class="sxs-lookup"><span data-stu-id="20fbc-239">Click the **OK** button</span></span>

<span data-ttu-id="20fbc-240">[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="20fbc-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="20fbc-241">**图 4**： 使用 IIS 6.0 创建通配符脚本映射 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="20fbc-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="20fbc-242">启用通配符脚本映射后，您需要修改 Global.asax 文件中的路由表，以使其包括根路由。</span><span class="sxs-lookup"><span data-stu-id="20fbc-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="20fbc-243">否则，您将收到错误页图 5 中，为你的应用程序的根页面请求时。</span><span class="sxs-lookup"><span data-stu-id="20fbc-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="20fbc-244">可以使用列表 4 中修改后的 Global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="20fbc-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="20fbc-245">[![新建项目对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="20fbc-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="20fbc-246">**图 5**： 缺少根路由错误 ([单击以查看实际尺寸的图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="20fbc-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="20fbc-247">**列表 4-Global.asax （修改根路由的情况）**</span><span class="sxs-lookup"><span data-stu-id="20fbc-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="20fbc-248">为 IIS 7.0 或 IIS 6.0 中启用通配符脚本映射后，可以发出使用默认路由表，如下所示的请求：</span><span class="sxs-lookup"><span data-stu-id="20fbc-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="20fbc-249">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="20fbc-249">/Home/Index</span></span>

<span data-ttu-id="20fbc-250">/ 产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="20fbc-250">/Product/Details/3</span></span>

<span data-ttu-id="20fbc-251">/ 产品</span><span class="sxs-lookup"><span data-stu-id="20fbc-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="20fbc-252">总结</span><span class="sxs-lookup"><span data-stu-id="20fbc-252">Summary</span></span>

<span data-ttu-id="20fbc-253">本教程的目的是说明如何使用 ASP.NET MVC 使用的较旧版本的 IIS （或在经典模式下的 IIS 7.0） 时。</span><span class="sxs-lookup"><span data-stu-id="20fbc-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="20fbc-254">我们讨论了获取以便使用较旧版本的 IIS 使用 ASP.NET 路由的两个方法： 修改默认路由表，或者创建一个通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="20fbc-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="20fbc-255">第一个选项要求您修改 ASP.NET MVC 应用程序中使用的 Url。</span><span class="sxs-lookup"><span data-stu-id="20fbc-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="20fbc-256">此第一个选项的其中一个显著优点是您无需访问 web 服务器即可修改路由表。</span><span class="sxs-lookup"><span data-stu-id="20fbc-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="20fbc-257">这意味着您可以使用此第一个选项，即使承载在 ASP.NET MVC 应用程序的 Internet 托管公司。</span><span class="sxs-lookup"><span data-stu-id="20fbc-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="20fbc-258">第二个选项是创建通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="20fbc-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="20fbc-259">此第二个选项的优点是不需要修改你的 Url。</span><span class="sxs-lookup"><span data-stu-id="20fbc-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="20fbc-260">此第二个选项的缺点是它可以对 ASP.NET MVC 应用程序的性能影响。</span><span class="sxs-lookup"><span data-stu-id="20fbc-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="20fbc-261">下一篇</span><span class="sxs-lookup"><span data-stu-id="20fbc-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
