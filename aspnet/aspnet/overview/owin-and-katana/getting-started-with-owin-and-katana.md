---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 和 Katana 入门 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 58a3d234867821d5e23cce2f01e105dfab88ac33
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826650"
---
<a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="fddca-102">OWIN 和 Katana 入门</span><span class="sxs-lookup"><span data-stu-id="fddca-102">Getting Started with OWIN and Katana</span></span>
====================
<span data-ttu-id="fddca-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fddca-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fddca-104">[打开 Web Interface for.NET (OWIN)](http://owin.org/)定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="fddca-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="fddca-105">通过分离应用程序从 web 服务器，OWIN 使得更轻松地创建.NET web 开发的中间件。</span><span class="sxs-lookup"><span data-stu-id="fddca-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="fddca-106">此外，OWIN 简化了到其他主机的端口 web 应用程序&#8212;例如，自托管 Windows 服务或其他进程中。</span><span class="sxs-lookup"><span data-stu-id="fddca-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="fddca-107">OWIN 是一个社区拥有规范，不实现。</span><span class="sxs-lookup"><span data-stu-id="fddca-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="fddca-108">Katana 项目是一组由 Microsoft 开发的开源 OWIN 组件。</span><span class="sxs-lookup"><span data-stu-id="fddca-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="fddca-109">OWIN 和 Katana 的常规概述，请参阅[项目 Katana 概述](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="fddca-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="fddca-110">在本文中，我将直接跳转到代码，以开始。</span><span class="sxs-lookup"><span data-stu-id="fddca-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="fddca-111">本教程使用[Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566)，但也可以使用 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="fddca-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="fddca-112">几个步骤是在 Visual Studio 2012，我注意到以下不同的。</span><span class="sxs-lookup"><span data-stu-id="fddca-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="fddca-113">承载在 IIS 中的 OWIN</span><span class="sxs-lookup"><span data-stu-id="fddca-113">Host OWIN in IIS</span></span>

<span data-ttu-id="fddca-114">在本部分中，我们将托管在 IIS 中的 OWIN。</span><span class="sxs-lookup"><span data-stu-id="fddca-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="fddca-115">此选项可提供灵活性和可组合性的 OWIN 管道以及 IIS 的成熟功能集。</span><span class="sxs-lookup"><span data-stu-id="fddca-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="fddca-116">使用此选项，在 ASP.NET 请求管道中运行 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fddca-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="fddca-117">首先，创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="fddca-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="fddca-118">（在 Visual Studio 2012 中，使用 ASP.NET 空 Web 应用程序项目类型）。</span><span class="sxs-lookup"><span data-stu-id="fddca-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="fddca-119">在中**新建 ASP.NET 项目**对话框中，选择**空**模板。</span><span class="sxs-lookup"><span data-stu-id="fddca-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="fddca-120">添加 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="fddca-120">Add NuGet Packages</span></span>

<span data-ttu-id="fddca-121">接下来，添加所需的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="fddca-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="fddca-122">从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="fddca-122">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="fddca-123">在包管理器控制台窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fddca-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="fddca-124">添加一个 Startup 类</span><span class="sxs-lookup"><span data-stu-id="fddca-124">Add a Startup Class</span></span>

<span data-ttu-id="fddca-125">接下来，添加 OWIN 启动类。</span><span class="sxs-lookup"><span data-stu-id="fddca-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="fddca-126">在解决方案资源管理器，右键单击该项目并选择**外**，然后选择**新项**。</span><span class="sxs-lookup"><span data-stu-id="fddca-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="fddca-127">在中**添加新项**对话框中，选择**Owin 启动类**。</span><span class="sxs-lookup"><span data-stu-id="fddca-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="fddca-128">配置启动类的详细信息，请参阅[OWIN 启动类检测](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="fddca-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="fddca-129">将以下代码添加到 `Startup1.Configuration` 方法：</span><span class="sxs-lookup"><span data-stu-id="fddca-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="fddca-130">此代码将一段简单的中间件添加到 OWIN 管道中，作为接收函数实现**Microsoft.Owin.IOwinContext**实例。</span><span class="sxs-lookup"><span data-stu-id="fddca-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="fddca-131">当服务器收到 HTTP 请求时，OWIN 管道调用中间件。</span><span class="sxs-lookup"><span data-stu-id="fddca-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="fddca-132">中间件设置响应的内容类型，并写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="fddca-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="fddca-133">OWIN Startup 类模板是 Visual Studio 2013 中可用。</span><span class="sxs-lookup"><span data-stu-id="fddca-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="fddca-134">如果正在使用 Visual Studio 2012，只需添加新的空类命名为`Startup1`，并粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="fddca-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="fddca-135">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fddca-135">Run the Application</span></span>

<span data-ttu-id="fddca-136">按 F5 开始调试。</span><span class="sxs-lookup"><span data-stu-id="fddca-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="fddca-137">Visual Studio 将打开一个浏览器窗口以`http://localhost:*port*/`。</span><span class="sxs-lookup"><span data-stu-id="fddca-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="fddca-138">页面应如以下所示：</span><span class="sxs-lookup"><span data-stu-id="fddca-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="fddca-139">在控制台应用程序中自托管 OWIN</span><span class="sxs-lookup"><span data-stu-id="fddca-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="fddca-140">很容易地从 IIS 承载到自承载自定义过程中转换此应用程序。</span><span class="sxs-lookup"><span data-stu-id="fddca-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="fddca-141">使用 IIS 承载，IIS 充当 HTTP 服务器和承载服务的进程。</span><span class="sxs-lookup"><span data-stu-id="fddca-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="fddca-142">与自托管，你的应用程序创建过程，并使用**HttpListener**类作为 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="fddca-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="fddca-143">在 Visual Studio 中，创建一个新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="fddca-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="fddca-144">在包管理器控制台窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fddca-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="fddca-145">添加`Startup1`本教程的第 1 部分中对项目的类。</span><span class="sxs-lookup"><span data-stu-id="fddca-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="fddca-146">无需修改此类。</span><span class="sxs-lookup"><span data-stu-id="fddca-146">You don't need to modify this class.</span></span>

<span data-ttu-id="fddca-147">实现应用程序的`Main`方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fddca-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="fddca-148">服务器在运行控制台应用程序时，开始侦听`http://localhost:9000`。</span><span class="sxs-lookup"><span data-stu-id="fddca-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="fddca-149">如果你导航到此地址在 web 浏览器中，您将看到"Hello world"页面。</span><span class="sxs-lookup"><span data-stu-id="fddca-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="fddca-150">添加 OWIN 诊断</span><span class="sxs-lookup"><span data-stu-id="fddca-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="fddca-151">Microsoft.Owin.Diagnostics 包中包含的捕获未经处理的异常并显示错误详细信息的 HTML 页中间件。</span><span class="sxs-lookup"><span data-stu-id="fddca-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="fddca-152">此页函数非常像有时被称为 ASP.NET 错误页"[黄色死机紫屏](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)"(YSOD)。</span><span class="sxs-lookup"><span data-stu-id="fddca-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="fddca-153">如 YSOD，Katana 错误页可在开发期间，但最好在生产模式下禁用它。</span><span class="sxs-lookup"><span data-stu-id="fddca-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="fddca-154">若要在项目中安装诊断程序包，请在包管理器控制台窗口中键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="fddca-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="fddca-155">中的代码更改在`Startup1.Configuration`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fddca-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="fddca-156">现在使用 CTRL + F5 运行应用程序而不进行调试，以便 Visual Studio 将不在异常上中断。</span><span class="sxs-lookup"><span data-stu-id="fddca-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="fddca-157">应用程序的行为相同与之前一样，直到您导航到`http://localhost/fail`，此时应用程序将引发异常。</span><span class="sxs-lookup"><span data-stu-id="fddca-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="fddca-158">错误页中间件将捕获该异常并显示有关错误的信息的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="fddca-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="fddca-159">您可以单击选项卡以查看堆栈、 查询字符串、 cookie、 请求标头和 OWIN 环境变量。</span><span class="sxs-lookup"><span data-stu-id="fddca-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="fddca-160">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fddca-160">Next Steps</span></span>

- [<span data-ttu-id="fddca-161">OWIN 启动类检测</span><span class="sxs-lookup"><span data-stu-id="fddca-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="fddca-162">使用 OWIN 自托管 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="fddca-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="fddca-163">使用 OWIN 自承载 SignalR</span><span class="sxs-lookup"><span data-stu-id="fddca-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
