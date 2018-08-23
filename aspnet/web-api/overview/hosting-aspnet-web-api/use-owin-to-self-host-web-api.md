---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自托管 ASP.NET Web API 2 |Microsoft Docs
author: rick-anderson
description: 本教程演示如何使用 OWIN 自托管 Web API 框架的控制台应用程序中托管 ASP.NET Web API。 打开 Web Interface for.NET (OWIN) d...
ms.author: riande
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 0d16498e94ac0a66c117ed057db398c14080beaa
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833150"
---
<a name="use-owin-to-self-host-aspnet-web-api-2"></a><span data-ttu-id="10e03-104">使用 OWIN 自托管 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="10e03-104">Use OWIN to Self-Host ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="10e03-105">通过[Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span><span class="sxs-lookup"><span data-stu-id="10e03-105">by [Kanchan Mehrotra](https://twitter.com/kanchanmeh)</span></span>

> <span data-ttu-id="10e03-106">本教程演示如何使用 OWIN 自托管 Web API 框架的控制台应用程序中托管 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="10e03-106">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
> 
> <span data-ttu-id="10e03-107">[用于.NET 开放 Web 接口](http://owin.org)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="10e03-107">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="10e03-108">OWIN 将从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序的 web 应用程序中分离出来。</span><span class="sxs-lookup"><span data-stu-id="10e03-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="10e03-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="10e03-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="10e03-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) （也适用于 Visual Studio 2012）</span><span class="sxs-lookup"><span data-stu-id="10e03-110">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (also works with Visual Studio 2012)</span></span>
> - <span data-ttu-id="10e03-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="10e03-111">Web API 2</span></span>


> [!NOTE]
> <span data-ttu-id="10e03-112">您可以在本教程中找到完整的源代码[aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="10e03-112">You can find the complete source code for this tutorial at [aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="10e03-113">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="10e03-113">Create a Console Application</span></span>

<span data-ttu-id="10e03-114">上**文件**菜单上，单击**新建**，然后单击**项目**。</span><span class="sxs-lookup"><span data-stu-id="10e03-114">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="10e03-115">从**已安装的模板**，在 Visual C# 中，单击**Windows** ，然后单击**控制台应用程序**。</span><span class="sxs-lookup"><span data-stu-id="10e03-115">From **Installed Templates**, under Visual C#, click **Windows** and then click **Console Application**.</span></span> <span data-ttu-id="10e03-116">命名项目"OwinSelfhostSample"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="10e03-116">Name the project "OwinSelfhostSample" and click **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image2.png)](use-owin-to-self-host-web-api/_static/image1.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="10e03-117">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="10e03-117">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="10e03-118">从**工具**菜单上，单击**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="10e03-118">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span> <span data-ttu-id="10e03-119">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="10e03-119">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="10e03-120">这将安装 WebAPI OWIN selfhost 包和所有所需的 OWIN 包。</span><span class="sxs-lookup"><span data-stu-id="10e03-120">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="10e03-121">配置 Web API 的自托管</span><span class="sxs-lookup"><span data-stu-id="10e03-121">Configure Web API for Self-Host</span></span>

<span data-ttu-id="10e03-122">在解决方案资源管理器，右键单击项目，然后选择**外** / **类**以添加一个新类。</span><span class="sxs-lookup"><span data-stu-id="10e03-122">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="10e03-123">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="10e03-123">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="10e03-124">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="10e03-124">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="10e03-125">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="10e03-125">Add a Web API Controller</span></span>

<span data-ttu-id="10e03-126">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="10e03-126">Next, add a Web API controller class.</span></span> <span data-ttu-id="10e03-127">在解决方案资源管理器，右键单击项目，然后选择**外** / **类**以添加一个新类。</span><span class="sxs-lookup"><span data-stu-id="10e03-127">In Solution Explorer, right click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="10e03-128">将此类命名为 `ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="10e03-128">Name the class `ValuesController`.</span></span>

<span data-ttu-id="10e03-129">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="10e03-129">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-using-httpclient"></a><span data-ttu-id="10e03-130">启动 OWIN 主机并发出使用 HttpClient 请求</span><span class="sxs-lookup"><span data-stu-id="10e03-130">Start the OWIN Host and Make a Request Using HttpClient</span></span>

<span data-ttu-id="10e03-131">使用以下内容替换所有 Program.cs 文件中的样板代码：</span><span class="sxs-lookup"><span data-stu-id="10e03-131">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="running-the-application"></a><span data-ttu-id="10e03-132">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="10e03-132">Running the Application</span></span>

<span data-ttu-id="10e03-133">若要运行该应用程序，请在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="10e03-133">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="10e03-134">输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="10e03-134">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="10e03-135">其他资源</span><span class="sxs-lookup"><span data-stu-id="10e03-135">Additional Resources</span></span>

[<span data-ttu-id="10e03-136">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="10e03-136">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="10e03-137">承载在 Azure 辅助角色中的 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="10e03-137">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
