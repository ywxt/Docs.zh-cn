---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自承载 ASP.NET Web API 1 (C#) |Microsoft 文档
author: MikeWasson
description: ASP.NET Web API 不需要 IIS。 在主机过程中，你可以自承载 web API。 本教程演示如何承载 web API applic 控制台中...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2012
ms.topic: article
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 564f859e73a88ac9c5f27e9b8f7409ec126642f8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="10915-105">自承载 ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="10915-105">Self-Host ASP.NET Web API 1 (C#)</span></span>
====================
<span data-ttu-id="10915-106">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="10915-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="10915-107">ASP.NET Web API 不需要 IIS。</span><span class="sxs-lookup"><span data-stu-id="10915-107">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="10915-108">在主机过程中，你可以自承载 web API。</span><span class="sxs-lookup"><span data-stu-id="10915-108">You can self-host a web API in your own host process.</span></span> <span data-ttu-id="10915-109">本教程演示如何承载于控制台应用程序内的 web API。</span><span class="sxs-lookup"><span data-stu-id="10915-109">This tutorial shows how to host a web API inside a console application.</span></span>
> 
> <span data-ttu-id="10915-110">**新的应用程序应使用 OWIN 自承载 Web API。**</span><span class="sxs-lookup"><span data-stu-id="10915-110">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="10915-111">请参阅[使用 OWIN 自承载 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="10915-111">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="10915-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="10915-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="10915-113">Web API 1</span><span class="sxs-lookup"><span data-stu-id="10915-113">Web API 1</span></span>
> - <span data-ttu-id="10915-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="10915-114">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="10915-115">创建控制台应用程序项目</span><span class="sxs-lookup"><span data-stu-id="10915-115">Create the Console Application Project</span></span>

<span data-ttu-id="10915-116">启动 Visual Studio 并选择**新项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="10915-116">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="10915-117">或从**文件**菜单上，选择**新建**然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="10915-117">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="10915-118">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="10915-118">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="10915-119">下**Visual C#**，选择**Windows**。</span><span class="sxs-lookup"><span data-stu-id="10915-119">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="10915-120">在项目模板列表中，选择**控制台应用程序**。</span><span class="sxs-lookup"><span data-stu-id="10915-120">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="10915-121">将项目&quot;SelfHost&quot;单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="10915-121">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="10915-122">设置目标框架 (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="10915-122">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="10915-123">如果你使用的 Visual Studio 2010，更改目标框架为.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="10915-123">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="10915-124">(默认情况下，项目模板面向[.Net Framework 客户端配置文件](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)。)</span><span class="sxs-lookup"><span data-stu-id="10915-124">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="10915-125">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="10915-125">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="10915-126">在**目标框架**下拉列表中，将目标框架更改为.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="10915-126">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="10915-127">当系统提示以应用更改，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="10915-127">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="10915-128">安装 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="10915-128">Install NuGet Package Manager</span></span>

<span data-ttu-id="10915-129">NuGet 包管理器是将 Web API 程序集添加到非 ASP.NET 项目的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="10915-129">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="10915-130">若要检查是否安装了 NuGet 包管理器，请单击**工具**Visual Studio 中的菜单。</span><span class="sxs-lookup"><span data-stu-id="10915-130">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="10915-131">如果你看到一个菜单项调用**库程序包管理器**，您就可以得到 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="10915-131">If you see a menu item called **Library Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="10915-132">若要安装 NuGet 包管理器：</span><span class="sxs-lookup"><span data-stu-id="10915-132">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="10915-133">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="10915-133">Start Visual Studio.</span></span>
2. <span data-ttu-id="10915-134">从**工具**菜单上，选择**扩展和更新**。</span><span class="sxs-lookup"><span data-stu-id="10915-134">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="10915-135">在**扩展和更新**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="10915-135">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="10915-136">如果看不到"NuGet Package Manager"，请在搜索框中键入"nuget package manager"。</span><span class="sxs-lookup"><span data-stu-id="10915-136">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="10915-137">选择 NuGet 包管理器，然后单击**下载**。</span><span class="sxs-lookup"><span data-stu-id="10915-137">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="10915-138">下载完成后，系统将提示安装。</span><span class="sxs-lookup"><span data-stu-id="10915-138">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="10915-139">安装完成后，你可能会提示您重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="10915-139">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="10915-140">添加 Web API NuGet 包</span><span class="sxs-lookup"><span data-stu-id="10915-140">Add the Web API NuGet Package</span></span>

<span data-ttu-id="10915-141">安装 NuGet 包管理器后，将添加到你的项目的 Web API 自承载包。</span><span class="sxs-lookup"><span data-stu-id="10915-141">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="10915-142">从**工具**菜单上，选择**库程序包管理器**。</span><span class="sxs-lookup"><span data-stu-id="10915-142">From the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="10915-143">*请注意*： 如果你不会看到此菜单项，请确保正确安装该 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="10915-143">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="10915-144">选择**管理解决方案的 NuGet 包...**</span><span class="sxs-lookup"><span data-stu-id="10915-144">Select **Manage NuGet Packages for Solution...**</span></span>
3. <span data-ttu-id="10915-145">在**Manage NugGet Packages**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="10915-145">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="10915-146">在搜索框中，键入&quot;Microsoft.AspNet.WebApi.SelfHost&quot;。</span><span class="sxs-lookup"><span data-stu-id="10915-146">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="10915-147">选择 ASP.NET Web API Self Host 包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="10915-147">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="10915-148">该包将安装后，单击**关闭**关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="10915-148">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="10915-149">请确保安装名为 Microsoft.AspNet.WebApi.SelfHost，不 AspNetWebApi.SelfHost 的程序包。</span><span class="sxs-lookup"><span data-stu-id="10915-149">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>


![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="10915-150">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="10915-150">Create the Model and Controller</span></span>

<span data-ttu-id="10915-151">本教程使用相同的模型和控制器类[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="10915-151">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="10915-152">添加一个名为的公共类`Product`。</span><span class="sxs-lookup"><span data-stu-id="10915-152">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="10915-153">添加一个名为的公共类`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="10915-153">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="10915-154">派生此类从**System.Web.Http.ApiController**。</span><span class="sxs-lookup"><span data-stu-id="10915-154">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="10915-155">有关此控制器中的代码的详细信息，请参阅[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="10915-155">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="10915-156">此控制器定义三个 GET 操作：</span><span class="sxs-lookup"><span data-stu-id="10915-156">This controller defines three GET actions:</span></span>

| <span data-ttu-id="10915-157">URI</span><span class="sxs-lookup"><span data-stu-id="10915-157">URI</span></span> | <span data-ttu-id="10915-158">描述</span><span class="sxs-lookup"><span data-stu-id="10915-158">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10915-159">/ api/产品</span><span class="sxs-lookup"><span data-stu-id="10915-159">/api/products</span></span> | <span data-ttu-id="10915-160">获取所有产品的列表。</span><span class="sxs-lookup"><span data-stu-id="10915-160">Get a list of all products.</span></span> |
| <span data-ttu-id="10915-161">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="10915-161">/api/products/*id*</span></span> | <span data-ttu-id="10915-162">获取产品的 id。</span><span class="sxs-lookup"><span data-stu-id="10915-162">Get a product by ID.</span></span> |
| <span data-ttu-id="10915-163">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="10915-163">/api/products/?category=*category*</span></span> | <span data-ttu-id="10915-164">按类别获取产品的列表。</span><span class="sxs-lookup"><span data-stu-id="10915-164">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="10915-165">承载 Web API</span><span class="sxs-lookup"><span data-stu-id="10915-165">Host the Web API</span></span>

<span data-ttu-id="10915-166">打开文件 Program.cs 并添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="10915-166">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="10915-167">以下代码添加到**程序**类。</span><span class="sxs-lookup"><span data-stu-id="10915-167">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="10915-168">（可选）添加一个 HTTP URL Namespace 保留项</span><span class="sxs-lookup"><span data-stu-id="10915-168">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="10915-169">此应用程序侦听`http://localhost:8080/`。</span><span class="sxs-lookup"><span data-stu-id="10915-169">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="10915-170">默认情况下，侦听特定的 HTTP 地址需要管理员特权。</span><span class="sxs-lookup"><span data-stu-id="10915-170">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="10915-171">当运行本教程时，因此，可能会收到此错误:"HTTP 无法注册 URL http://+:8080/"有两种方法，若要避免此错误：</span><span class="sxs-lookup"><span data-stu-id="10915-171">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="10915-172">使用提升的管理员权限运行 Visual Studio 或</span><span class="sxs-lookup"><span data-stu-id="10915-172">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="10915-173">使用 Netsh.exe 你向帐户授予权限以保留该 URL。</span><span class="sxs-lookup"><span data-stu-id="10915-173">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="10915-174">若要使用 Netsh.exe，使用管理员特权打开命令提示符并输入以下命令： 以下命令：</span><span class="sxs-lookup"><span data-stu-id="10915-174">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="10915-175">其中*计算机 \ 用户名*是你的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="10915-175">where *machine\username* is your user account.</span></span>

<span data-ttu-id="10915-176">完成之后自承载，请务必删除保留：</span><span class="sxs-lookup"><span data-stu-id="10915-176">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="10915-177">从客户端应用程序 (C#) 调用 Web API</span><span class="sxs-lookup"><span data-stu-id="10915-177">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="10915-178">让我们来编写的简单控制台应用程序调用 web API。</span><span class="sxs-lookup"><span data-stu-id="10915-178">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="10915-179">向解决方案中添加新的控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="10915-179">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="10915-180">在解决方案资源管理器，右键单击该解决方案并选择**添加新项目**。</span><span class="sxs-lookup"><span data-stu-id="10915-180">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="10915-181">创建名为的新控制台应用&quot;ClientApp&quot;。</span><span class="sxs-lookup"><span data-stu-id="10915-181">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="10915-182">使用 NuGet 包管理器添加 ASP.NET Web API Core Libraries 包：</span><span class="sxs-lookup"><span data-stu-id="10915-182">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="10915-183">从工具菜单中，选择**库程序包管理器**。</span><span class="sxs-lookup"><span data-stu-id="10915-183">From the Tools menu, select **Library Package Manager**.</span></span>
- <span data-ttu-id="10915-184">选择**管理解决方案的 NuGet 包...**</span><span class="sxs-lookup"><span data-stu-id="10915-184">Select **Manage NuGet Packages for Solution...**</span></span>
- <span data-ttu-id="10915-185">在**管理 NuGet 包**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="10915-185">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="10915-186">在搜索框中，键入&quot;Microsoft.AspNet.WebApi.Client&quot;。</span><span class="sxs-lookup"><span data-stu-id="10915-186">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="10915-187">选择 Microsoft ASP.NET Web API 客户端库包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="10915-187">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="10915-188">添加在 ClientApp 对 SelfHost 项目的引用：</span><span class="sxs-lookup"><span data-stu-id="10915-188">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="10915-189">在解决方案资源管理器，右键单击 ClientApp 项目。</span><span class="sxs-lookup"><span data-stu-id="10915-189">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="10915-190">选择**添加引用**。</span><span class="sxs-lookup"><span data-stu-id="10915-190">Select **Add Reference**.</span></span>
- <span data-ttu-id="10915-191">在**引用管理器**对话框下**解决方案**，选择**项目**。</span><span class="sxs-lookup"><span data-stu-id="10915-191">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="10915-192">选择 SelfHost 项目。</span><span class="sxs-lookup"><span data-stu-id="10915-192">Select the SelfHost project.</span></span>
- <span data-ttu-id="10915-193">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="10915-193">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="10915-194">打开 Client/Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="10915-194">Open the Client/Program.cs file.</span></span> <span data-ttu-id="10915-195">添加以下**使用**语句：</span><span class="sxs-lookup"><span data-stu-id="10915-195">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="10915-196">添加静态**HttpClient**实例：</span><span class="sxs-lookup"><span data-stu-id="10915-196">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="10915-197">添加以下方法以按类别列出所有产品，列表按 ID、 产品和产品列表。</span><span class="sxs-lookup"><span data-stu-id="10915-197">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="10915-198">这些方法的一种都遵循相同的模式：</span><span class="sxs-lookup"><span data-stu-id="10915-198">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="10915-199">调用**HttpClient.GetAsync**将 GET 请求发送到的相应 URI。</span><span class="sxs-lookup"><span data-stu-id="10915-199">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="10915-200">调用**HttpResponseMessage.EnsureSuccessStatusCode**。</span><span class="sxs-lookup"><span data-stu-id="10915-200">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="10915-201">如果 HTTP 响应状态错误代码，此方法将引发异常。</span><span class="sxs-lookup"><span data-stu-id="10915-201">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="10915-202">调用**ReadAsAsync&lt;T&gt;** 进行反序列化的 HTTP 响应中的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="10915-202">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="10915-203">此方法是扩展方法，在中定义**System.Net.Http.HttpContentExtensions**。</span><span class="sxs-lookup"><span data-stu-id="10915-203">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="10915-204">**GetAsync**和**ReadAsAsync**方法都异步。</span><span class="sxs-lookup"><span data-stu-id="10915-204">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="10915-205">它们返回**任务**表示异步操作的对象。</span><span class="sxs-lookup"><span data-stu-id="10915-205">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="10915-206">获取**结果**属性阻止线程，直到操作完成。</span><span class="sxs-lookup"><span data-stu-id="10915-206">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="10915-207">有关使用 HttpClient，包括如何进行非阻止调用，请参阅[调用 Web API 从.NET 客户端](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="10915-207">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="10915-208">在调用这些方法之前, 设置 BaseAddress 属性对所 HttpClient 实例"`http://localhost:8080`"。</span><span class="sxs-lookup"><span data-stu-id="10915-208">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="10915-209">例如:</span><span class="sxs-lookup"><span data-stu-id="10915-209">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="10915-210">这应输出以下。</span><span class="sxs-lookup"><span data-stu-id="10915-210">This should output the following.</span></span> <span data-ttu-id="10915-211">（请记住要首先运行 SelfHost 应用程序。）</span><span class="sxs-lookup"><span data-stu-id="10915-211">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
