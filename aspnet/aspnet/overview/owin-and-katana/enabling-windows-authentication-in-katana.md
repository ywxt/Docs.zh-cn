---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: 启用在 Katana 中的 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 本文介绍如何启用 Windows 身份验证在 Katana 中。 它涵盖了两种方案： 使用 IIS 托管 Katana，并使用 HttpListener 自托管 Kat...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
ms.technology: ''
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: e7fbe6af323ecdc09b4d79073f506c5ee056f30f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391610"
---
<a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="b1ad2-104">在 Katana 中启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="b1ad2-104">Enabling Windows Authentication in Katana</span></span>
====================
<span data-ttu-id="b1ad2-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b1ad2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b1ad2-106">本文介绍如何启用 Windows 身份验证在 Katana 中。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="b1ad2-107">它涵盖了两种方案： 使用 IIS 托管 Katana，并使用 HttpListener 自托管 Katana 中自定义进程。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="b1ad2-108">感谢您对 Barry Dorrans、 David Matson 和 Chris Ross 对本文的审阅。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>


<span data-ttu-id="b1ad2-109">Katana 是 Microsoft 的实现[OWIN](http://owin.org/)，Open Web Interface for.NET。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="b1ad2-110">可以阅读简介 OWIN 和 Katana[此处](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="b1ad2-111">OWIN 体系结构具有多个层：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="b1ad2-112">主机： 管理的过程运行 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="b1ad2-113">Server： 打开网络套接字并侦听请求。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="b1ad2-114">中间件： 处理的 HTTP 请求和响应。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="b1ad2-115">Katana 目前提供两个服务器，都支持 Windows 集成身份验证：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="b1ad2-116">**Microsoft.Owin.Host.SystemWeb**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="b1ad2-117">使用 IIS 与 ASP.NET 管道。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="b1ad2-118">**Microsoft.Owin.Host.HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="b1ad2-119">使用[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="b1ad2-120">此服务器当前是默认选项，自托管时 Katana。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="b1ad2-121">Katana 当前不提供 OWIN 中间件进行 Windows 身份验证，因为此功能已在服务器中可用。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>


## <a name="windows-authentication-in-iis"></a><span data-ttu-id="b1ad2-122">在 IIS 中的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="b1ad2-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="b1ad2-123">使用 Microsoft.Owin.Host.SystemWeb，可以只需启用 IIS 中的 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="b1ad2-124">让我们首先创建新的 ASP.NET 应用程序，使用"ASP.NET 空 Web 应用程序"项目模板。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="b1ad2-125">接下来，添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-125">Next, add NuGet packages.</span></span> <span data-ttu-id="b1ad2-126">从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-126">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b1ad2-127">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="b1ad2-128">现在，添加一个名为类`Startup`使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="b1ad2-129">这是您需要创建 OWIN，在 IIS 上运行的"Hello world"应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="b1ad2-130">按 F5 调试该应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-130">Press F5 to debug the application.</span></span> <span data-ttu-id="b1ad2-131">你应看到"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="b1ad2-131">You should see "Hello World!"</span></span> <span data-ttu-id="b1ad2-132">在浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="b1ad2-133">接下来，我们将启用 Windows 身份验证在 IIS Express 中。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="b1ad2-134">从**视图**菜单中，选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="b1ad2-135">单击解决方案资源管理器中查看项目属性中的项目名称。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="b1ad2-136">在中**属性**窗口中，将**匿名身份验证**到**禁用**并设置**Windows 身份验证**到**启用**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="b1ad2-137">当从 Visual Studio 运行应用程序时，IIS Express 将要求用户的 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="b1ad2-138">可以使用查看这[Fiddler](http://fiddler2.com/home)或另一个 HTTP 调试工具。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="b1ad2-139">下面是示例 HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="b1ad2-140">此响应中的 Www-authenticate 标头指示该服务器支持[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)协议，使用 Kerberos 或 NTLM。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="b1ad2-141">更高版本，在部署到服务器应用程序时，请按照[这些步骤](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)要在该服务器上启用 IIS 中的 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="b1ad2-142">在 HttpListener 的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="b1ad2-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="b1ad2-143">如果使用 Microsoft.Owin.Host.HttpListener 自托管 Katana，则可以直接在上启用 Windows 身份验证**HttpListener**实例。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="b1ad2-144">首先，创建一个新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-144">First, create a new console application.</span></span> <span data-ttu-id="b1ad2-145">接下来，添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-145">Next, add NuGet packages.</span></span> <span data-ttu-id="b1ad2-146">从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-146">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b1ad2-147">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="b1ad2-148">现在，添加一个名为类`Startup`使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="b1ad2-149">此类实现的同一"Hello world"示例之前，但它还将 Windows 身份验证设置为身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="b1ad2-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="b1ad2-150">内部`Main`函数中，启动 OWIN 管道：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="b1ad2-151">在 Fiddler 来确认应用程序正在使用 Windows 身份验证中，可以发送请求：</span><span class="sxs-lookup"><span data-stu-id="b1ad2-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="b1ad2-152">相关主题</span><span class="sxs-lookup"><span data-stu-id="b1ad2-152">Related Topics</span></span>

[<span data-ttu-id="b1ad2-153">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="b1ad2-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="b1ad2-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="b1ad2-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="b1ad2-155">了解 MVC 5 中的 OWIN 窗体身份验证</span><span class="sxs-lookup"><span data-stu-id="b1ad2-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
