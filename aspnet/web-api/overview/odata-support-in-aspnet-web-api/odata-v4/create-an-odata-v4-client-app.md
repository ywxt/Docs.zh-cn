---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: 创建 OData v4 客户端应用程序 (C#) |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: 51a3c7b9c5b6525d6d82b9a45910f58b71268b7f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28036695"
---
<a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="875c6-102">创建 OData v4 客户端应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="875c6-102">Create an OData v4 Client App (C#)</span></span>
====================
<span data-ttu-id="875c6-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="875c6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="875c6-104">在前面的教程，你将创建可支持的 CRUD 操作的基本 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="875c6-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="875c6-105">现在让我们来创建服务的客户端。</span><span class="sxs-lookup"><span data-stu-id="875c6-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="875c6-106">启动 Visual Studio 的新实例并创建新的控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="875c6-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="875c6-107">在**新项目**对话框中，选择**已安装** &gt; **模板** &gt; **Visual C#** &gt; **Windows 桌面**，然后选择**控制台应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="875c6-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="875c6-108">将项目&quot;ProductsApp&quot;。</span><span class="sxs-lookup"><span data-stu-id="875c6-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="875c6-109">你还可以将控制台应用程序添加到包含 OData 服务的同一 Visual Studio 解决方案。</span><span class="sxs-lookup"><span data-stu-id="875c6-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>


## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="875c6-110">安装的 OData 客户端代码生成器</span><span class="sxs-lookup"><span data-stu-id="875c6-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="875c6-111">从**工具**菜单上，选择**扩展和更新**。</span><span class="sxs-lookup"><span data-stu-id="875c6-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="875c6-112">选择**联机** &gt; **Visual Studio 库**。</span><span class="sxs-lookup"><span data-stu-id="875c6-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="875c6-113">在搜索框中，搜索&quot;OData 客户端代码生成器&quot;。</span><span class="sxs-lookup"><span data-stu-id="875c6-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="875c6-114">单击**下载**安装 VSIX。</span><span class="sxs-lookup"><span data-stu-id="875c6-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="875c6-115">系统可能会提示你重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="875c6-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="875c6-116">本地运行 OData 服务</span><span class="sxs-lookup"><span data-stu-id="875c6-116">Run the OData Service Locally</span></span>

<span data-ttu-id="875c6-117">从 Visual Studio 运行 ProductService 项目。</span><span class="sxs-lookup"><span data-stu-id="875c6-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="875c6-118">默认情况下，Visual Studio 将启动浏览器访问的应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="875c6-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="875c6-119">请注意 URI;您将需要它在下一步。</span><span class="sxs-lookup"><span data-stu-id="875c6-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="875c6-120">使应用程序保持运行。</span><span class="sxs-lookup"><span data-stu-id="875c6-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="875c6-121">如果将这两个项目置于同一解决方案中，请确保运行 ProductService 项目而不调试。</span><span class="sxs-lookup"><span data-stu-id="875c6-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="875c6-122">在下一步的步骤中，你将需要使本服务运行时修改控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="875c6-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>


## <a name="generate-the-service-proxy"></a><span data-ttu-id="875c6-123">生成的服务代理</span><span class="sxs-lookup"><span data-stu-id="875c6-123">Generate the Service Proxy</span></span>

<span data-ttu-id="875c6-124">服务代理是一个.NET 类，定义用于访问 OData 服务的方法。</span><span class="sxs-lookup"><span data-stu-id="875c6-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="875c6-125">代理将转换为 HTTP 请求的方法调用。</span><span class="sxs-lookup"><span data-stu-id="875c6-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="875c6-126">将通过运行创建代理类[T4 模板](https://msdn.microsoft.com/library/bb126445.aspx)。</span><span class="sxs-lookup"><span data-stu-id="875c6-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="875c6-127">右键单击该项目。</span><span class="sxs-lookup"><span data-stu-id="875c6-127">Right-click the project.</span></span> <span data-ttu-id="875c6-128">选择**添加** &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="875c6-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="875c6-129">在**添加新项**对话框中，选择**Visual C# 项** &gt; **代码** &gt; **OData 客户端**。</span><span class="sxs-lookup"><span data-stu-id="875c6-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="875c6-130">该模板命名&quot;ProductClient.tt&quot;。</span><span class="sxs-lookup"><span data-stu-id="875c6-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="875c6-131">单击**添加**并依次单击安全警告。</span><span class="sxs-lookup"><span data-stu-id="875c6-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="875c6-132">此时，你将获得一个错误，则可以忽略。</span><span class="sxs-lookup"><span data-stu-id="875c6-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="875c6-133">Visual Studio 会自动运行该模板后，但需要某些配置设置的模板第一个。</span><span class="sxs-lookup"><span data-stu-id="875c6-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="875c6-134">打开文件 ProductClient.odata.config。在`Parameter`元素中，粘贴 ProductService 项目 （上一步） 从 URI 中。</span><span class="sxs-lookup"><span data-stu-id="875c6-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="875c6-135">例如:</span><span class="sxs-lookup"><span data-stu-id="875c6-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="875c6-136">再次运行的模板。</span><span class="sxs-lookup"><span data-stu-id="875c6-136">Run the template again.</span></span> <span data-ttu-id="875c6-137">在解决方案资源管理器，右键单击 ProductClient.tt 文件，然后选择**运行自定义工具**。</span><span class="sxs-lookup"><span data-stu-id="875c6-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="875c6-138">此模板创建一个名为 ProductClient.cs 定义代理的代码文件。</span><span class="sxs-lookup"><span data-stu-id="875c6-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="875c6-139">如果您更改 OData 终结点，你的应用，开发时，运行再次要更新代理的模板。</span><span class="sxs-lookup"><span data-stu-id="875c6-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="875c6-140">使用服务代理调用 OData 服务</span><span class="sxs-lookup"><span data-stu-id="875c6-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="875c6-141">打开文件 Program.cs 并将替换为以下的样板文件代码。</span><span class="sxs-lookup"><span data-stu-id="875c6-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="875c6-142">值替换*serviceUri*用于服务 URI 的更早版本。</span><span class="sxs-lookup"><span data-stu-id="875c6-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="875c6-143">运行应用程序时，它应输出以下各项：</span><span class="sxs-lookup"><span data-stu-id="875c6-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
