---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第 1 部分： 概述和创建项目 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2012
ms.topic: article
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: f9cdff0cb0cad9adad546c8f8d46ba9b010e1079
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="65b1b-102">第 1 部分： 概述和创建项目</span><span class="sxs-lookup"><span data-stu-id="65b1b-102">Part 1: Overview and Creating the Project</span></span>
====================
<span data-ttu-id="65b1b-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="65b1b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="65b1b-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="65b1b-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="65b1b-105">实体框架是一种对象/关系映射框架。</span><span class="sxs-lookup"><span data-stu-id="65b1b-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="65b1b-106">它将在代码中的域对象映射到关系数据库中的实体。</span><span class="sxs-lookup"><span data-stu-id="65b1b-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="65b1b-107">大多数情况下，你无需担心数据库层中，因为实体框架将为你对其负责。</span><span class="sxs-lookup"><span data-stu-id="65b1b-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="65b1b-108">你的代码操作对象，并更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="65b1b-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="65b1b-109">有关本教程</span><span class="sxs-lookup"><span data-stu-id="65b1b-109">About the Tutorial</span></span>

<span data-ttu-id="65b1b-110">在本教程中，你将创建一个简单应用商店应用程序。</span><span class="sxs-lookup"><span data-stu-id="65b1b-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="65b1b-111">有两个主要部分应用程序。</span><span class="sxs-lookup"><span data-stu-id="65b1b-111">There are two main parts to the application.</span></span> <span data-ttu-id="65b1b-112">正常的用户可以查看产品和创建订单：</span><span class="sxs-lookup"><span data-stu-id="65b1b-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="65b1b-113">管理员可以创建、 删除或编辑产品：</span><span class="sxs-lookup"><span data-stu-id="65b1b-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="65b1b-114">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="65b1b-114">Skills You'll Learn</span></span>

<span data-ttu-id="65b1b-115">下面是你将要掌握的内容：</span><span class="sxs-lookup"><span data-stu-id="65b1b-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="65b1b-116">如何使用 ASP.NET Web API 的实体框架。</span><span class="sxs-lookup"><span data-stu-id="65b1b-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="65b1b-117">如何使用 knockout.js 创建动态的客户端 UI。</span><span class="sxs-lookup"><span data-stu-id="65b1b-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="65b1b-118">如何与 Web API 一起使用 forms 身份验证，用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="65b1b-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="65b1b-119">虽然本教程是自包含，但你可能想要首先阅读以下教程：</span><span class="sxs-lookup"><span data-stu-id="65b1b-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="65b1b-120">你的第一个 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="65b1b-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="65b1b-121">创建一个 Web API 支持 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="65b1b-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="65b1b-122">一些了解[ASP.NET MVC](../../../../mvc/index.md)也是有帮助。</span><span class="sxs-lookup"><span data-stu-id="65b1b-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="65b1b-123">概述</span><span class="sxs-lookup"><span data-stu-id="65b1b-123">Overview</span></span>

<span data-ttu-id="65b1b-124">在高级别中，下面是应用程序的体系结构：</span><span class="sxs-lookup"><span data-stu-id="65b1b-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="65b1b-125">ASP.NET MVC 为客户端生成的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="65b1b-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="65b1b-126">ASP.NET Web API 公开的数据 （产品和 orders） 上的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="65b1b-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="65b1b-127">实体框架将转换到数据库实体使用 Web API 的 C# 模型。</span><span class="sxs-lookup"><span data-stu-id="65b1b-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="65b1b-128">下图显示了如何在应用程序的各层表示的域对象： 数据库层，对象模型中，依次连网格式，它用于传输到客户端通过 HTTP 的数据。</span><span class="sxs-lookup"><span data-stu-id="65b1b-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="65b1b-129">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="65b1b-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="65b1b-130">你可以创建教程使用 Visual Web Developer Express 或 Visual Studio 的完整版本的项目。</span><span class="sxs-lookup"><span data-stu-id="65b1b-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="65b1b-131">从**启动**页上，单击**新项目**。</span><span class="sxs-lookup"><span data-stu-id="65b1b-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="65b1b-132">在**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="65b1b-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="65b1b-133">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="65b1b-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="65b1b-134">在项目模板列表中，选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="65b1b-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="65b1b-135">将"ProductStore"的项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="65b1b-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="65b1b-136">在**新建 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="65b1b-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="65b1b-137">"Internet 应用程序"模板创建的 ASP.NET MVC 应用程序支持窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="65b1b-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="65b1b-138">如果你运行应用程序现在，它已有的某些功能：</span><span class="sxs-lookup"><span data-stu-id="65b1b-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="65b1b-139">新的用户可以注册通过单击右上角的"注册"链接。</span><span class="sxs-lookup"><span data-stu-id="65b1b-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="65b1b-140">已注册的用户可以通过单击"登录"链接进行登录。</span><span class="sxs-lookup"><span data-stu-id="65b1b-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="65b1b-141">将会自动创建的数据库中保留成员身份信息。</span><span class="sxs-lookup"><span data-stu-id="65b1b-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="65b1b-142">有关 ASP.NET mvc 的窗体身份验证的详细信息，请参阅[演练： 在 ASP.NET MVC 中使用 Forms 身份验证](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="65b1b-143">更新 CSS 文件</span><span class="sxs-lookup"><span data-stu-id="65b1b-143">Update the CSS File</span></span>

<span data-ttu-id="65b1b-144">此步骤是外观上的但它将使呈现如前面的屏幕截图的页。</span><span class="sxs-lookup"><span data-stu-id="65b1b-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="65b1b-145">在解决方案资源管理器，展开内容文件夹并打开名为 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="65b1b-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="65b1b-146">添加以下 CSS 样式：</span><span class="sxs-lookup"><span data-stu-id="65b1b-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="65b1b-147">下一篇</span><span class="sxs-lookup"><span data-stu-id="65b1b-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
