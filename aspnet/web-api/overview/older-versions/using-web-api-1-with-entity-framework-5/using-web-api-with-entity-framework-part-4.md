---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第 4 部分： 添加管理视图 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: cbf42f1dbd744d7b85dde7d2dcd99a13c6208a13
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879525"
---
<a name="part-4-adding-an-admin-view"></a><span data-ttu-id="126c6-102">第 4 部分： 添加管理视图</span><span class="sxs-lookup"><span data-stu-id="126c6-102">Part 4: Adding an Admin View</span></span>
====================
<span data-ttu-id="126c6-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="126c6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="126c6-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="126c6-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="126c6-105">添加管理员视图</span><span class="sxs-lookup"><span data-stu-id="126c6-105">Add an Admin View</span></span>

<span data-ttu-id="126c6-106">现在我们将转到客户端，并添加一个页，可以使用从管理控制器的数据。</span><span class="sxs-lookup"><span data-stu-id="126c6-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="126c6-107">页面将允许用户创建、 编辑或删除产品，通过将 AJAX 请求发送到的控制器。</span><span class="sxs-lookup"><span data-stu-id="126c6-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="126c6-108">在解决方案资源管理器，展开 Controllers 文件夹并打开名为 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="126c6-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="126c6-109">此文件包含一个 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="126c6-109">This file contains an MVC controller.</span></span> <span data-ttu-id="126c6-110">添加一个名为`Admin`:</span><span class="sxs-lookup"><span data-stu-id="126c6-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="126c6-111">**HttpRouteUrl**方法创建到 web API，URI 和我们将此存储在视图包为更高版本。</span><span class="sxs-lookup"><span data-stu-id="126c6-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="126c6-112">接下来，将文本光标放在`Admin`操作方法，然后右键单击并选择**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="126c6-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="126c6-113">此时会弹出**添加视图**对话框。</span><span class="sxs-lookup"><span data-stu-id="126c6-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="126c6-114">在**添加视图**对话框中，名称的视图"Admin"。</span><span class="sxs-lookup"><span data-stu-id="126c6-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="126c6-115">选择标记的复选框**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="126c6-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="126c6-116">下**模型类**，选择"Product (ProductStore.Models)"。</span><span class="sxs-lookup"><span data-stu-id="126c6-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="126c6-117">将所有其他选项保留为其默认值。</span><span class="sxs-lookup"><span data-stu-id="126c6-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="126c6-118">单击**添加**将添加名为 Admin.cshtml 视图/主页下的文件。</span><span class="sxs-lookup"><span data-stu-id="126c6-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="126c6-119">打开此文件并添加以下 HTML。</span><span class="sxs-lookup"><span data-stu-id="126c6-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="126c6-120">以下 HTML 定义页中，结构的但尚未向上有线任何功能。</span><span class="sxs-lookup"><span data-stu-id="126c6-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="126c6-121">创建指向管理页的链接</span><span class="sxs-lookup"><span data-stu-id="126c6-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="126c6-122">在解决方案资源管理器，展开视图文件夹，然后展开共享文件夹。</span><span class="sxs-lookup"><span data-stu-id="126c6-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="126c6-123">打开名为的文件\_Layout.cshtml。</span><span class="sxs-lookup"><span data-stu-id="126c6-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="126c6-124">找到**ul**元素 id ="菜单"和管理视图的操作链接：</span><span class="sxs-lookup"><span data-stu-id="126c6-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="126c6-125">在示例项目中，我进行了几个其他外观上的更改，如替换字符串"Your logo here"。</span><span class="sxs-lookup"><span data-stu-id="126c6-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="126c6-126">这些不会影响应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="126c6-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="126c6-127">可以下载项目，还可以比较文件。</span><span class="sxs-lookup"><span data-stu-id="126c6-127">You can download the project and compare the files.</span></span>


<span data-ttu-id="126c6-128">运行应用程序并单击显示在主页页面顶部的"Admin"链接。</span><span class="sxs-lookup"><span data-stu-id="126c6-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="126c6-129">管理页应如下所示：</span><span class="sxs-lookup"><span data-stu-id="126c6-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="126c6-130">右现在，页上不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="126c6-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="126c6-131">在下一步的部分中，我们将使用 Knockout.js 来创建动态 UI。</span><span class="sxs-lookup"><span data-stu-id="126c6-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="126c6-132">添加授权</span><span class="sxs-lookup"><span data-stu-id="126c6-132">Add Authorization</span></span>

<span data-ttu-id="126c6-133">管理页是当前可访问网站的任何人进行访问。</span><span class="sxs-lookup"><span data-stu-id="126c6-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="126c6-134">让我们更改此设置以限制对管理员的权限。</span><span class="sxs-lookup"><span data-stu-id="126c6-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="126c6-135">首先，通过添加的"管理员"角色和一个管理员用户。</span><span class="sxs-lookup"><span data-stu-id="126c6-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="126c6-136">在解决方案资源管理器，展开筛选器文件夹并打开名为 InitializeSimpleMembershipAttribute.cs 的文件。</span><span class="sxs-lookup"><span data-stu-id="126c6-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="126c6-137">找到`SimpleMembershipInitializer`构造函数。</span><span class="sxs-lookup"><span data-stu-id="126c6-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="126c6-138">在调用后**WebSecurity.InitializeDatabaseConnection**，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="126c6-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="126c6-139">这是添加的"管理员"角色和为角色创建一个用户应急方法。</span><span class="sxs-lookup"><span data-stu-id="126c6-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="126c6-140">在解决方案资源管理器，展开 Controllers 文件夹并打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="126c6-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="126c6-141">添加**Authorize**属性设为`Admin`方法。</span><span class="sxs-lookup"><span data-stu-id="126c6-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="126c6-142">打开 AdminController.cs 文件并添加**Authorize**属性设为整个`AdminController`类。</span><span class="sxs-lookup"><span data-stu-id="126c6-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="126c6-143">MVC 和 Web API 同时定义**Authorize**的属性，在不同的命名空间。</span><span class="sxs-lookup"><span data-stu-id="126c6-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="126c6-144">MVC 使用**System.Web.Mvc.AuthorizeAttribute**，而 Web API 使用**System.Web.Http.AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="126c6-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>


<span data-ttu-id="126c6-145">现在只有管理员可以查看管理页。</span><span class="sxs-lookup"><span data-stu-id="126c6-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="126c6-146">此外，如果将 HTTP 请求发送到管理控制器，则请求必须包含的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="126c6-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="126c6-147">如果没有，服务器发送 HTTP 401 （未经授权） 响应。</span><span class="sxs-lookup"><span data-stu-id="126c6-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="126c6-148">你可以看到此 Fiddler 中通过发送 GET 请求到`http://localhost:*port*/api/admin`。</span><span class="sxs-lookup"><span data-stu-id="126c6-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="126c6-149">[上一页](using-web-api-with-entity-framework-part-3.md)
> [下一页](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="126c6-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
