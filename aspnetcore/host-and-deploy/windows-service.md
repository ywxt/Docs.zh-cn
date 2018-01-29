---
title: "在 Windows 服务中的主机"
author: tdykstra
description: "了解如何托管的 ASP.NET Core 应用程序在 Windows 服务。"
ms.author: tdykstra
manager: wpickett
ms.custom: mvc
ms.date: 03/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: host-and-deploy/windows-service
ms.openlocfilehash: 4bf64f54dd9c6d2a1706bd405b0d6d75d7573a7a
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="host-an-aspnet-core-app-in-a-windows-service"></a><span data-ttu-id="48cee-103">ASP.NET Core 应用托管在 Windows 服务</span><span class="sxs-lookup"><span data-stu-id="48cee-103">Host an ASP.NET Core app in a Windows Service</span></span>

<span data-ttu-id="48cee-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="48cee-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="48cee-105">没有使用 IIS 是在运行承载 ASP.NET Core 应用在 Windows 上的推荐的方式[Windows 服务](https://docs.microsoft.com/dotnet/framework/windows-services/introduction-to-windows-service-applications)。</span><span class="sxs-lookup"><span data-stu-id="48cee-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](https://docs.microsoft.com/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="48cee-106">这样就可以自动启动后重新启动和崩溃，而无需等待某人登录。</span><span class="sxs-lookup"><span data-stu-id="48cee-106">That way it can automatically start after reboots and crashes, without waiting for someone to log in.</span></span>

<span data-ttu-id="48cee-107">[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)([如何下载](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="48cee-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="48cee-108">请参阅[后续步骤](#next-steps)部分以了解有关如何运行它。</span><span class="sxs-lookup"><span data-stu-id="48cee-108">See the [Next Steps](#next-steps) section for instructions on how to run it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48cee-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="48cee-109">Prerequisites</span></span>

* <span data-ttu-id="48cee-110">应用程序必须在.NET Framework 运行时上运行。</span><span class="sxs-lookup"><span data-stu-id="48cee-110">The app must run on the .NET Framework runtime.</span></span>  <span data-ttu-id="48cee-111">在*.csproj*文件中，指定为相应值[TargetFramework](https://docs.microsoft.com/nuget/schema/target-frameworks)和[RuntimeIdentifier](https://docs.microsoft.com/dotnet/articles/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="48cee-111">In the *.csproj* file, specify appropriate values for [TargetFramework](https://docs.microsoft.com/nuget/schema/target-frameworks) and [RuntimeIdentifier](https://docs.microsoft.com/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="48cee-112">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="48cee-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="48cee-113">当在 Visual Studio 中创建项目，请使用**ASP.NET 核心应用程序 (.NET Framework)**模板。</span><span class="sxs-lookup"><span data-stu-id="48cee-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="48cee-114">如果应用程序接收来自 Internet （而不仅仅是从内部网络） 的请求，它必须使用[WebListener](xref:fundamentals/servers/weblistener) web 服务器而非[Kestrel](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="48cee-114">If the app receives requests from the Internet (not just from an internal network), it must use the [WebListener](xref:fundamentals/servers/weblistener) web server rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span>  <span data-ttu-id="48cee-115">边缘部署，必须向 IIS 使用 kestrel。</span><span class="sxs-lookup"><span data-stu-id="48cee-115">Kestrel must be used with IIS for edge deployments.</span></span>  <span data-ttu-id="48cee-116">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="48cee-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="getting-started"></a><span data-ttu-id="48cee-117">入门</span><span class="sxs-lookup"><span data-stu-id="48cee-117">Getting started</span></span>

<span data-ttu-id="48cee-118">本部分介绍将现有的 ASP.NET Core 项目设置为在服务中运行所需的最小更改。</span><span class="sxs-lookup"><span data-stu-id="48cee-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

* <span data-ttu-id="48cee-119">安装 NuGet 程序包[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)。</span><span class="sxs-lookup"><span data-stu-id="48cee-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

* <span data-ttu-id="48cee-120">进行中的以下更改`Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="48cee-120">Make the following changes in `Program.Main`:</span></span>
  
  * <span data-ttu-id="48cee-121">调用`host.RunAsService`而不是`host.Run`。</span><span class="sxs-lookup"><span data-stu-id="48cee-121">Call `host.RunAsService` instead of `host.Run`.</span></span>
  
  * <span data-ttu-id="48cee-122">如果代码调用`UseContentRoot`，使用而不是发布位置的路径`Directory.GetCurrentDirectory()`</span><span class="sxs-lookup"><span data-stu-id="48cee-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`</span></span> 
  
  [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

* <span data-ttu-id="48cee-123">发布应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="48cee-123">Publish the application to a folder.</span></span>

  <span data-ttu-id="48cee-124">使用[dotnet 发布](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-publish)或[Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)，它发布到的文件夹。</span><span class="sxs-lookup"><span data-stu-id="48cee-124">Use [dotnet publish](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

* <span data-ttu-id="48cee-125">通过创建和启动服务测试。</span><span class="sxs-lookup"><span data-stu-id="48cee-125">Test by creating and starting the service.</span></span>

  <span data-ttu-id="48cee-126">打开管理员命令提示符窗口，以使用[sc.exe](https://technet.microsoft.com/library/bb490995)命令行工具来创建和启动服务。</span><span class="sxs-lookup"><span data-stu-id="48cee-126">Open an administrator command prompt window to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span>  
  
  <span data-ttu-id="48cee-127">如果该服务名为 MyService，将应用发布到`c:\svc`，并在应用程序名为 AspNetCoreService，命令将如下所示：</span><span class="sxs-lookup"><span data-stu-id="48cee-127">If the service is named MyService, publish the app to `c:\svc`, and the app itself is named AspNetCoreService, the commands would look like this:</span></span>

  ```console
  sc create MyService binPath="C:\Svc\AspNetCoreService.exe"
  sc start MyService
  ```

  <span data-ttu-id="48cee-128">`binPath`值是应用程序的可执行文件，包括可执行文件名本身的路径。</span><span class="sxs-lookup"><span data-stu-id="48cee-128">The `binPath` value is the path to the app's executable, including the executable filename itself.</span></span>

  ![控制台窗口创建并启动示例](windows-service/_static/create-start.png)

  <span data-ttu-id="48cee-130">在这些命令完成后，浏览到相同的路径作为控制台应用程序运行时 (默认情况下， `http://localhost:5000`)</span><span class="sxs-lookup"><span data-stu-id="48cee-130">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`)</span></span>

  ![服务中运行](windows-service/_static/running-in-service.png)


## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="48cee-132">提供服务的外部运行的方法</span><span class="sxs-lookup"><span data-stu-id="48cee-132">Provide a way to run outside of a service</span></span>

<span data-ttu-id="48cee-133">很容易地测试和调试时运行外部服务，因此通常将调用的代码添加`host.RunAsService`仅在某些情况下。</span><span class="sxs-lookup"><span data-stu-id="48cee-133">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `host.RunAsService` only under certain conditions.</span></span>  <span data-ttu-id="48cee-134">例如，应用程序可以作为包含的控制台应用程序运行`--console`命令行自变量，或如果附加调试器。</span><span class="sxs-lookup"><span data-stu-id="48cee-134">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached.</span></span>

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="48cee-135">处理停止和启动事件</span><span class="sxs-lookup"><span data-stu-id="48cee-135">Handle stopping and starting events</span></span>

<span data-ttu-id="48cee-136">若要处理`OnStarting`， `OnStarted`，和`OnStopping`事件，进行以下其他更改：</span><span class="sxs-lookup"><span data-stu-id="48cee-136">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

* <span data-ttu-id="48cee-137">创建一个从 `WebHostService` 派生的类。</span><span class="sxs-lookup"><span data-stu-id="48cee-137">Create a class that derives from `WebHostService`.</span></span>

  [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

* <span data-ttu-id="48cee-138">创建扩展方法`IWebHost`，通过自定义`WebHostService`到`ServiceBase.Run`。</span><span class="sxs-lookup"><span data-stu-id="48cee-138">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`.</span></span>

  [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

* <span data-ttu-id="48cee-139">在`Program.Main`更改调用新的扩展方法，而不是`host.RunAsService`。</span><span class="sxs-lookup"><span data-stu-id="48cee-139">In `Program.Main` change call the new extension method instead of `host.RunAsService`.</span></span>

  [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=26)]

<span data-ttu-id="48cee-140">如果自定义`WebHostService`代码需要从 （例如记录器） 的依赖关系注入获取服务，获取从`Services`属性`IWebHost`。</span><span class="sxs-lookup"><span data-stu-id="48cee-140">If the custom `WebHostService` code needs to get a service from dependency injection (such as a logger), get it from the `Services` property of `IWebHost`.</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="next-steps"></a><span data-ttu-id="48cee-141">后续步骤</span><span class="sxs-lookup"><span data-stu-id="48cee-141">Next steps</span></span>

<span data-ttu-id="48cee-142">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)附带此文章是已被修改，前面的代码示例中所示的简单 MVC web 应用。</span><span class="sxs-lookup"><span data-stu-id="48cee-142">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) that accompanies this article is a simple MVC web app that has been modified as shown in preceding code examples.</span></span>  <span data-ttu-id="48cee-143">若要在服务中运行它，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="48cee-143">To run it in a service, do the following steps:</span></span>

* <span data-ttu-id="48cee-144">将发布到*c:\svc*。</span><span class="sxs-lookup"><span data-stu-id="48cee-144">Publish to *c:\svc*.</span></span>

* <span data-ttu-id="48cee-145">打开管理员窗口。</span><span class="sxs-lookup"><span data-stu-id="48cee-145">Open an administrator window.</span></span>

* <span data-ttu-id="48cee-146">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="48cee-146">Enter the following commands:</span></span>

  ```console
  sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
  sc start MyService
  ```

  * <span data-ttu-id="48cee-147">在浏览器中，转到 http://localhost:5000/ 以验证它正在运行。</span><span class="sxs-lookup"><span data-stu-id="48cee-147">In a browser, go to http://localhost:5000 to verify that it's running.</span></span>

<span data-ttu-id="48cee-148">如果不按预期运行时服务中运行启动应用程序，以使错误消息可访问的捷径是添加日志记录提供程序，例如[Windows 事件日志提供程序](xref:fundamentals/logging/index#eventlog)。</span><span class="sxs-lookup"><span data-stu-id="48cee-148">If the app doesn't start up as expected when running in a service, a quick way to make error messages accessible is to add a logging provider such as the [Windows EventLog provider](xref:fundamentals/logging/index#eventlog).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="48cee-149">确认</span><span class="sxs-lookup"><span data-stu-id="48cee-149">Acknowledgments</span></span>

<span data-ttu-id="48cee-150">撰写本文时的已发布的源的帮助。</span><span class="sxs-lookup"><span data-stu-id="48cee-150">This article was written with the help of sources that were already published.</span></span> <span data-ttu-id="48cee-151">最早和其中最有用了这些：</span><span class="sxs-lookup"><span data-stu-id="48cee-151">The earliest and most useful of them were these:</span></span>

* [<span data-ttu-id="48cee-152">作为 Windows 服务承载 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="48cee-152">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="48cee-153">如何托管 Windows 服务中将 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="48cee-153">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
