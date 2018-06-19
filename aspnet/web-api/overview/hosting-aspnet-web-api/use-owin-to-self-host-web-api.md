---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自承载 ASP.NET Web API 2 |Microsoft 文档
author: rick-anderson
description: 本教程演示如何在控制台应用程序，使用 OWIN 自承载 Web API 框架中托管 ASP.NET Web API。 打开.NET (OWIN) d 的 Web 界面...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/09/2013
ms.topic: article
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: fda0db8155c3303907331a690af35f619b589154
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506966"
---
<a name="use-owin-to-self-host-aspnet-web-api-2"></a><span data-ttu-id="05b36-104">使用 OWIN 自承载 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="05b36-104">Use OWIN to Self-Host ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="05b36-105">通过[Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span><span class="sxs-lookup"><span data-stu-id="05b36-105">by [Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span></span>

> <span data-ttu-id="05b36-106">本教程演示如何在控制台应用程序，使用 OWIN 自承载 Web API 框架中托管 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="05b36-106">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
> 
> <span data-ttu-id="05b36-107">[打开针对.NET 的 Web 界面](http://owin.org)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="05b36-107">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="05b36-108">OWIN 将在服务器上，这使 OWIN 适合于你自己的过程，在 IIS 外部的 web 应用程序的自承载的 web 应用程序中脱离出来。</span><span class="sxs-lookup"><span data-stu-id="05b36-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="05b36-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="05b36-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="05b36-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) （也适用于 Visual Studio 2012）</span><span class="sxs-lookup"><span data-stu-id="05b36-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (also works with Visual Studio 2012)</span></span>
> - <span data-ttu-id="05b36-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="05b36-111">Web API 2</span></span>


> [!NOTE]
> <span data-ttu-id="05b36-112">你可以在本教程中找到的完整源代码[aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="05b36-112">You can find the complete source code for this tutorial at [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="05b36-113">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="05b36-113">Create a Console Application</span></span>

<span data-ttu-id="05b36-114">上**文件**菜单上，单击**新建**，然后单击**项目**。</span><span class="sxs-lookup"><span data-stu-id="05b36-114">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="05b36-115">从**已安装的模板**，在 Visual C# 中，单击**Windows** ，然后单击**控制台应用程序**。</span><span class="sxs-lookup"><span data-stu-id="05b36-115">From **Installed Templates**, under Visual C#, click **Windows** and then click **Console Application**.</span></span> <span data-ttu-id="05b36-116">将"OwinSelfhostSample"的项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="05b36-116">Name the project "OwinSelfhostSample" and click **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image2.png)](use-owin-to-self-host-web-api/_static/image1.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="05b36-117">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="05b36-117">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="05b36-118">从**工具**菜单上，单击**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="05b36-118">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span> <span data-ttu-id="05b36-119">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="05b36-119">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="05b36-120">这将安装 WebAPI OWIN selfhost 包和所需的所有 OWIN 包。</span><span class="sxs-lookup"><span data-stu-id="05b36-120">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="05b36-121">配置 Web API 的自承载</span><span class="sxs-lookup"><span data-stu-id="05b36-121">Configure Web API for Self-Host</span></span>

<span data-ttu-id="05b36-122">在解决方案资源管理器，右键单击项目，然后选择**添加** / **类**添加新类。</span><span class="sxs-lookup"><span data-stu-id="05b36-122">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="05b36-123">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="05b36-123">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="05b36-124">将所有此文件中的样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="05b36-124">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="05b36-125">添加一个 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="05b36-125">Add a Web API Controller</span></span>

<span data-ttu-id="05b36-126">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="05b36-126">Next, add a Web API controller class.</span></span> <span data-ttu-id="05b36-127">在解决方案资源管理器，右键单击项目，然后选择**添加** / **类**添加新类。</span><span class="sxs-lookup"><span data-stu-id="05b36-127">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="05b36-128">将此类命名为 `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="05b36-128">Name the class `ValuesController`.</span></span>

<span data-ttu-id="05b36-129">将所有此文件中的样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="05b36-129">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-using-httpclient"></a><span data-ttu-id="05b36-130">启动 OWIN 主机并发出一个请求，使用 HttpClient</span><span class="sxs-lookup"><span data-stu-id="05b36-130">Start the OWIN Host and Make a Request Using HttpClient</span></span>

<span data-ttu-id="05b36-131">将所有的 Program.cs 文件中的样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="05b36-131">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="running-the-application"></a><span data-ttu-id="05b36-132">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="05b36-132">Running the Application</span></span>

<span data-ttu-id="05b36-133">若要运行应用程序，请在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="05b36-133">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="05b36-134">输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="05b36-134">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="05b36-135">其他资源</span><span class="sxs-lookup"><span data-stu-id="05b36-135">Additional Resources</span></span>

[<span data-ttu-id="05b36-136">项目 Katana 事件的概述</span><span class="sxs-lookup"><span data-stu-id="05b36-136">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="05b36-137">承载在 Azure 辅助角色中的 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="05b36-137">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
