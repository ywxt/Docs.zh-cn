---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 使用 ASP.NET Web 窗体的 Web API |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2012
ms.topic: article
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: af918671a8bcc97a0050ea033ccd14dd96416e73
ms.sourcegitcommit: 037d3900f739dbaa2ba14158e3d7dc81478952ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
ms.locfileid: "26536076"
---
<a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="a1f3a-102">使用 ASP.NET Web 窗体的 Web API</span><span class="sxs-lookup"><span data-stu-id="a1f3a-102">Using Web API with ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="a1f3a-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a1f3a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a1f3a-104">尽管 ASP.NET Web API 与 ASP.NET MVC 一起打包，很容易地将 Web API 添加到传统的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-104">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span> <span data-ttu-id="a1f3a-105">本教程将指导你完成的步骤。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-105">This tutorial walks you through the steps.</span></span>

## <a name="overview"></a><span data-ttu-id="a1f3a-106">概述</span><span class="sxs-lookup"><span data-stu-id="a1f3a-106">Overview</span></span>

<span data-ttu-id="a1f3a-107">若要在 Web 窗体应用程序中使用 Web API，有两个主要步骤：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-107">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="a1f3a-108">添加一个派生自的 Web API 控制器**ApiController**类。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-108">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="a1f3a-109">添加路由表的**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-109">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="a1f3a-110">创建 Web 窗体项目</span><span class="sxs-lookup"><span data-stu-id="a1f3a-110">Create a Web Forms Project</span></span>

<span data-ttu-id="a1f3a-111">启动 Visual Studio 并选择**新项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-111">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="a1f3a-112">或从**文件**菜单上，选择**新建**然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-112">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="a1f3a-113">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-113">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a1f3a-114">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-114">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a1f3a-115">在项目模板列表中，选择**ASP.NET Web 窗体应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-115">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="a1f3a-116">输入项目的名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-116">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="a1f3a-117">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="a1f3a-117">Create the Model and Controller</span></span>

<span data-ttu-id="a1f3a-118">本教程使用相同的模型和控制器类[入门](tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-118">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="a1f3a-119">首先，将一个模型类添加。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-119">First, add a model class.</span></span> <span data-ttu-id="a1f3a-120">在**解决方案资源管理器**，右键单击该项目并选择**添加类**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-120">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="a1f3a-121">命名类产品，并添加以下实现：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-121">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="a1f3a-122">接下来，将一个 Web API 控制器添加到项目中。，A*控制器*是为 Web API 处理 HTTP 请求的对象。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-122">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="a1f3a-123">在**解决方案资源管理器**，右键单击该项目。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-123">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="a1f3a-124">选择**添加新项**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-124">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="a1f3a-125">下**已安装的模板**，展开**Visual C#** 和选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-125">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="a1f3a-126">然后，从模板列表中，选择**Web API 控制器类**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-126">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="a1f3a-127">将"ProductsController"的控制器，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-127">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="a1f3a-128">**添加新项**向导将创建一个名为 ProductsController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-128">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="a1f3a-129">删除向导包括的方法，并添加以下方法：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-129">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="a1f3a-130">有关此控制器中的代码的详细信息，请参阅[入门](tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-130">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="a1f3a-131">添加路由的信息</span><span class="sxs-lookup"><span data-stu-id="a1f3a-131">Add Routing Information</span></span>

<span data-ttu-id="a1f3a-132">接下来，我们将因此添加一个路由，URI 形式的该 Uri &quot;/api/产品/&quot;路由到的控制器。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-132">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="a1f3a-133">在**解决方案资源管理器**，双击 Global.asax 以打开代码隐藏文件 Global.asax.cs。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-133">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="a1f3a-134">添加以下**使用**语句。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-134">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="a1f3a-135">然后添加以下代码到**应用程序\_启动**方法：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-135">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="a1f3a-136">有关路由表的详细信息，请参阅[路由在 ASP.NET Web API 中](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-136">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="a1f3a-137">添加客户端 AJAX</span><span class="sxs-lookup"><span data-stu-id="a1f3a-137">Add Client-Side AJAX</span></span>

<span data-ttu-id="a1f3a-138">这就是所有你需要创建的 web 客户端可以访问的 API。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-138">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="a1f3a-139">现在让我们添加 jQuery 用于调用 API 的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-139">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="a1f3a-140">请确保你的母版页 (例如， *Site.Master*) 包括`ContentPlaceHolder`与`ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="a1f3a-140">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="a1f3a-141">打开 Default.aspx 的文件。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-141">Open the file Default.aspx.</span></span> <span data-ttu-id="a1f3a-142">将主要内容部分中的样本文本替换所示：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-142">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="a1f3a-143">接下来，添加对中的 jQuery 源文件的引用`HeaderContent`部分：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-143">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="a1f3a-144">注意： 你可以轻松添加脚本引用通过拖放文件从**解决方案资源管理器**到代码编辑器窗口中。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-144">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="a1f3a-145">下面的 jQuery 脚本标记添加下面的脚本块：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-145">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="a1f3a-146">当文档加载后时，此脚本会在 AJAX 请求到&quot;api/产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-146">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="a1f3a-147">请求返回采用 JSON 格式的产品列表。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-147">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="a1f3a-148">该脚本将产品信息添加到 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="a1f3a-148">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="a1f3a-149">运行应用程序时，它应如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1f3a-149">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
