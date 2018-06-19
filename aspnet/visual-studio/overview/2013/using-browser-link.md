---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用浏览器链接 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/04/2013
ms.topic: article
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: e5a13405a303580ec8c1d4cdacafc26c6f8ff34a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28044105"
---
<a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="eb1c9-102">在 Visual Studio 2013 中使用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eb1c9-102">Using Browser Link in Visual Studio 2013</span></span>
====================
<span data-ttu-id="eb1c9-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eb1c9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="eb1c9-104">浏览器链接是在创建开发环境和一个或多个 web 浏览器之间的通信通道的 Visual Studio 2013 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="eb1c9-105">你可以使用浏览器链接刷新 web 应用程序在多个浏览器中的，这是适用于跨浏览器测试。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="eb1c9-106">刷新浏览器</span><span class="sxs-lookup"><span data-stu-id="eb1c9-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="eb1c9-107">查看浏览器链接仪表板</span><span class="sxs-lookup"><span data-stu-id="eb1c9-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="eb1c9-108">启用静态 HTML 文件的浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eb1c9-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="eb1c9-109">禁用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eb1c9-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="eb1c9-110">它是如何工作的？</span><span class="sxs-lookup"><span data-stu-id="eb1c9-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="eb1c9-111">刷新浏览器</span><span class="sxs-lookup"><span data-stu-id="eb1c9-111">Browser Refresh</span></span>

<span data-ttu-id="eb1c9-112">使用浏览器刷新，你可以刷新连接到 Visual Studio 中通过浏览器链接的多个浏览器。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="eb1c9-113">若要使用浏览器刷新，首先创建 ASP.NET 应用程序，使用任意项目模板。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="eb1c9-114">按 F5 或单击工具栏中的箭头图标调试该应用程序：</span><span class="sxs-lookup"><span data-stu-id="eb1c9-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="eb1c9-115">你可以使用下拉列表中选择用于调试的特定浏览器。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="eb1c9-116">若要调试与多个浏览器，选择**浏览**。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="eb1c9-117">在**浏览**对话框中，按住 CTRL 键选择多个浏览器。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="eb1c9-118">单击**浏览**使用所选的浏览器进行调试。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="eb1c9-119">如果你启动 Visual Studio 外部的浏览器并导航到应用程序 URL，也适用于浏览器链接。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="eb1c9-120">浏览器链接控件位于具有循环的箭头图标下拉列表。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="eb1c9-121">箭头图标是**刷新**按钮。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="eb1c9-122">若要查看连接的浏览器，将鼠标悬停**刷新**进行调试时的按钮。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="eb1c9-123">连接的浏览器显示在工具提示窗口中。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="eb1c9-124">若要刷新的已连接的浏览器，请单击**刷新**按钮或按 CTRL + ALT + ENTER。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="eb1c9-125">例如，下面的屏幕截图显示 ASP.NET 项目，我创建了使用 MVC 5 项目模板。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="eb1c9-126">你可以看到在顶部的两个浏览器中运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="eb1c9-127">在底部，项目是 Visual Studio 中打开。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="eb1c9-128">在 Visual Studio 中，我更改&lt;h1&gt;主页标题：</span><span class="sxs-lookup"><span data-stu-id="eb1c9-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="eb1c9-129">当我单击**刷新**按钮，在这两个浏览器窗口中出现过更改：</span><span class="sxs-lookup"><span data-stu-id="eb1c9-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="eb1c9-130">**备注**</span><span class="sxs-lookup"><span data-stu-id="eb1c9-130">**Notes**</span></span>

- <span data-ttu-id="eb1c9-131">若要启用浏览器链接，将设置`debug=true`中[&lt;编译&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)项目的 Web.config 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="eb1c9-132">必须在本地主机上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="eb1c9-133">应用程序必须面向.NET 4.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="eb1c9-134">查看浏览器链接仪表板</span><span class="sxs-lookup"><span data-stu-id="eb1c9-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="eb1c9-135">Browser Link 仪表板显示有关浏览器链接连接的信息。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="eb1c9-136">若要查看仪表板，请选择的浏览器链接下拉列表菜单 (旁边的小箭头**刷新**按钮)。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="eb1c9-137">然后单击**浏览器链接仪表板**。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="eb1c9-138">仪表板列出连接的浏览器和每个浏览器导航到的 URL。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="eb1c9-139">**先决条件**部分显示为该项目启用浏览器链接所需的任何步骤。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="eb1c9-140">例如，下面的屏幕截图显示一个项目在"调试"设置为 false 在 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="eb1c9-141">启用静态 HTML 文件的浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eb1c9-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="eb1c9-142">若要启用 Browser Link 用于静态 HTML 文件，将以下添加到 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="eb1c9-143">出于性能原因，删除此设置，在发布你的项目时。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="eb1c9-144">禁用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eb1c9-144">Disabling Browser Link</span></span>

<span data-ttu-id="eb1c9-145">默认情况下会启用浏览器链接。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="eb1c9-146">有几种方法可以禁用它：</span><span class="sxs-lookup"><span data-stu-id="eb1c9-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="eb1c9-147">在浏览器链接下拉菜单中，取消选中**启用 Browser Link**。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="eb1c9-148">在 Web.config 文件中，添加名为"vs: EnableBrowserLink"值"false"中的 appSettings 节的键。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="eb1c9-149">在 Web.config 文件中，将调试设置为 false。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="eb1c9-150">它是如何工作的？</span><span class="sxs-lookup"><span data-stu-id="eb1c9-150">How Does It Work?</span></span>

<span data-ttu-id="eb1c9-151">浏览器链接使用[SignalR](../../../signalr/index.md)若要创建 Visual Studio 和浏览器之间的通信通道。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="eb1c9-152">启用浏览器链接后，Visual Studio 将充当多个客户端 （浏览器） 可以连接到的 SignalR 服务器。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="eb1c9-153">浏览器链接还注册与 ASP.NET 搭配使用的 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="eb1c9-154">此模块插入特殊&lt;脚本&gt;到每个页请求从服务器的引用。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="eb1c9-155">可以通过在浏览器中选择"查看源文件"查看脚本引用。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="eb1c9-156">不会修改你的源文件。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-156">Your source files are not modified.</span></span> <span data-ttu-id="eb1c9-157">HTTP 模块动态插入脚本引用。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="eb1c9-158">由于浏览器端代码是所有 JavaScript，它可用于所有浏览器， [SignalR 支持](../../../signalr/overview/getting-started/supported-platforms.md)，而无需任何浏览器插件。</span><span class="sxs-lookup"><span data-stu-id="eb1c9-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
