---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: 开始使用 OWIN 和 Katana |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/27/2013
ms.topic: article
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: ac0302ef1a786f6b1eef8119b3134a965f01c533
ms.sourcegitcommit: 5ab5c5f4bfdb0150f42ba84c2770eadf540cae48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
<a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="b7e12-102">开始使用 OWIN 和 Katana</span><span class="sxs-lookup"><span data-stu-id="b7e12-102">Getting Started with OWIN and Katana</span></span>
====================
<span data-ttu-id="b7e12-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b7e12-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b7e12-104">[打开.NET (OWIN) 的 Web 界面](http://owin.org/)定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="b7e12-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="b7e12-105">通过分离从应用程序的 web 服务器，OWIN 使得更轻松地创建.NET web 开发的中间件。</span><span class="sxs-lookup"><span data-stu-id="b7e12-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="b7e12-106">此外，OWIN，从而更便于端口 web 应用程序到其他主机&#8212;例如，Windows 服务或其他进程中的自承载。</span><span class="sxs-lookup"><span data-stu-id="b7e12-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="b7e12-107">OWIN 是一个社区拥有规范，未实现。</span><span class="sxs-lookup"><span data-stu-id="b7e12-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="b7e12-108">Katana 项目是一组由 Microsoft 开发的开源 OWIN 组件。</span><span class="sxs-lookup"><span data-stu-id="b7e12-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="b7e12-109">OWIN 和 Katana 的一般概述，请参阅[项目概述 Katana](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e12-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="b7e12-110">在本文中，我将直接到代码开始。</span><span class="sxs-lookup"><span data-stu-id="b7e12-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="b7e12-111">本教程使用[Visual Studio 2013 候选发布版本](https://go.microsoft.com/fwlink/?LinkId=306566)，但你也可以使用 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="b7e12-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="b7e12-112">在 Visual Studio 2012，我请注意以下几个步骤互不相同。</span><span class="sxs-lookup"><span data-stu-id="b7e12-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="b7e12-113">在 IIS 中的 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="b7e12-113">Host OWIN in IIS</span></span>

<span data-ttu-id="b7e12-114">在此部分中，我们将承载在 IIS 中的 OWIN。</span><span class="sxs-lookup"><span data-stu-id="b7e12-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="b7e12-115">此选项可让你的灵活性和可组合性的与 IIS 的成熟的功能集一起 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="b7e12-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="b7e12-116">使用此选项，在 ASP.NET 请求管道中运行的 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b7e12-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="b7e12-117">首先，创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="b7e12-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="b7e12-118">（在 Visual Studio 2012 中，使用 ASP.NET 空 Web 应用程序项目类型）。</span><span class="sxs-lookup"><span data-stu-id="b7e12-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="b7e12-119">在**新建 ASP.NET 项目**对话框中，选择**空**模板。</span><span class="sxs-lookup"><span data-stu-id="b7e12-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="b7e12-120">添加 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b7e12-120">Add NuGet Packages</span></span>

<span data-ttu-id="b7e12-121">接下来，添加所需的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b7e12-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="b7e12-122">从**工具**菜单上，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="b7e12-122">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b7e12-123">在 Package Manager Console 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b7e12-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="b7e12-124">添加一个 Startup 类</span><span class="sxs-lookup"><span data-stu-id="b7e12-124">Add a Startup Class</span></span>

<span data-ttu-id="b7e12-125">接下来，添加的 OWIN 启动类。</span><span class="sxs-lookup"><span data-stu-id="b7e12-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="b7e12-126">在解决方案资源管理器，右键单击该项目并选择**添加**，然后选择**新项**。</span><span class="sxs-lookup"><span data-stu-id="b7e12-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="b7e12-127">在**添加新项**对话框中，选择**Owin 启动类**。</span><span class="sxs-lookup"><span data-stu-id="b7e12-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="b7e12-128">有关配置 startup 类的详细信息，请参阅[OWIN 启动类检测](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e12-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="b7e12-129">将以下代码添加到 `Startup1.Configuration` 方法：</span><span class="sxs-lookup"><span data-stu-id="b7e12-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="b7e12-130">此代码将一个简单的中间件添加到 OWIN 管道，作为函数接收实现**Microsoft.Owin.IOwinContext**实例。</span><span class="sxs-lookup"><span data-stu-id="b7e12-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="b7e12-131">当服务器接收 HTTP 请求时，OWIN 管道时，将调用该中间件。</span><span class="sxs-lookup"><span data-stu-id="b7e12-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="b7e12-132">该中间件将响应的内容类型设置，并将写入响应正文。</span><span class="sxs-lookup"><span data-stu-id="b7e12-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="b7e12-133">OWIN 启动类模板是在 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="b7e12-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="b7e12-134">如果你正在使用 Visual Studio 2012，只需添加一个名为的新的空类`Startup1`，然后粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="b7e12-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="b7e12-135">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="b7e12-135">Run the Application</span></span>

<span data-ttu-id="b7e12-136">按 F5 开始调试。</span><span class="sxs-lookup"><span data-stu-id="b7e12-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="b7e12-137">Visual Studio 将打开一个浏览器窗口以`http://localhost:*port*/`。</span><span class="sxs-lookup"><span data-stu-id="b7e12-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="b7e12-138">页应如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7e12-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="b7e12-139">将 OWIN 自承载在控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="b7e12-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="b7e12-140">很容易地将此应用程序转换从到自定义过程中的自承载的 IIS 承载。</span><span class="sxs-lookup"><span data-stu-id="b7e12-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="b7e12-141">使用 IIS 承载，IIS 可以充当 HTTP 服务器和承载服务的进程。</span><span class="sxs-lookup"><span data-stu-id="b7e12-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="b7e12-142">与自承载，你的应用程序创建过程，并使用**HttpListener**与 HTTP 服务器的类。</span><span class="sxs-lookup"><span data-stu-id="b7e12-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="b7e12-143">在 Visual Studio 中，创建一个新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="b7e12-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="b7e12-144">在 Package Manager Console 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b7e12-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="b7e12-145">添加`Startup1`从本教程的第 1 部分到项目的类。</span><span class="sxs-lookup"><span data-stu-id="b7e12-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="b7e12-146">你不需要修改此类。</span><span class="sxs-lookup"><span data-stu-id="b7e12-146">You don't need to modify this class.</span></span>

<span data-ttu-id="b7e12-147">实现应用程序的`Main`方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b7e12-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="b7e12-148">运行控制台应用程序时，在服务器启动侦听`http://localhost:9000`。</span><span class="sxs-lookup"><span data-stu-id="b7e12-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="b7e12-149">如果你导航到此地址在 web 浏览器中，你将看到"Hello world"页。</span><span class="sxs-lookup"><span data-stu-id="b7e12-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="b7e12-150">添加 OWIN 诊断</span><span class="sxs-lookup"><span data-stu-id="b7e12-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="b7e12-151">Microsoft.Owin.Diagnostics 程序包包含中间件捕获未经处理的异常并显示错误详细信息的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="b7e12-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="b7e12-152">此页函数非常类似有时称为 ASP.NET 错误页"[死亡的黄色屏幕](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)"(YSOD)。</span><span class="sxs-lookup"><span data-stu-id="b7e12-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="b7e12-153">与一样 YSOD，Katana 错误页有用在开发期间，但它是在生产模式中禁用该一个好办法。</span><span class="sxs-lookup"><span data-stu-id="b7e12-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="b7e12-154">若要安装在你的项目中的诊断程序包，请在程序包管理器控制台窗口中键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="b7e12-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="b7e12-155">更改中的代码你`Startup1.Configuration`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7e12-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="b7e12-156">现在使用 CTRL + F5 运行应用程序而不进行调试，以便 Visual Studio 将不在异常上中断。</span><span class="sxs-lookup"><span data-stu-id="b7e12-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="b7e12-157">应用程序具有相同的行为和前面一样，直到你导航到`http://localhost/fail`，此时，应用程序会引发异常。</span><span class="sxs-lookup"><span data-stu-id="b7e12-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="b7e12-158">错误页中间件将捕获该异常并显示有关错误的信息的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="b7e12-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="b7e12-159">你可以单击选项卡来查看堆栈、 查询字符串、 cookie、 请求标头和 OWIN 环境变量。</span><span class="sxs-lookup"><span data-stu-id="b7e12-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="b7e12-160">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b7e12-160">Next Steps</span></span>

- [<span data-ttu-id="b7e12-161">OWIN 启动类检测</span><span class="sxs-lookup"><span data-stu-id="b7e12-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="b7e12-162">使用 OWIN 自承载 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="b7e12-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="b7e12-163">使用 OWIN 自承载 SignalR</span><span class="sxs-lookup"><span data-stu-id="b7e12-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
