---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: "调用 Web API，从 Windows Phone 8 应用程序 (C#) |Microsoft 文档"
author: rmcmurray
description: "创建包含的 ASP.NET Web API 应用程序提供到 Windows Phone 8 应用程序的书籍目录的完整端到端方案。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/09/2013
ms.topic: article
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: 2025f31f369153b93cd293884880c97635fc8ab8
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
<a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="869e6-103">从 Windows Phone 8 应用程序 (C#) 调用 Web API</span><span class="sxs-lookup"><span data-stu-id="869e6-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>
====================
<span data-ttu-id="869e6-104">通过[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="869e6-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="869e6-105">在本教程中，您将学习如何创建包含的 ASP.NET Web API 应用程序提供到 Windows Phone 8 应用程序的书籍目录的完整端到端方案。</span><span class="sxs-lookup"><span data-stu-id="869e6-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="869e6-106">概述</span><span class="sxs-lookup"><span data-stu-id="869e6-106">Overview</span></span>

<span data-ttu-id="869e6-107">如 ASP.NET Web API rESTful 服务通过抽取服务器端和客户端应用程序的体系结构简化的开发人员的基于 HTTP 的应用程序的创建。</span><span class="sxs-lookup"><span data-stu-id="869e6-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="869e6-108">而不是创建用于通信的专有的基于套接字协议，Web API 开发人员只需发布自己的应用程序的必备项 HTTP 方法 (例如： GET、 POST、 PUT、 DELETE)，且客户端应用程序开发人员只需要使用所需其应用程序的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="869e6-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="869e6-109">在本端到端教程，你将学习如何使用 Web API 来创建以下项目：</span><span class="sxs-lookup"><span data-stu-id="869e6-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="869e6-110">在[本教程的第一部分](#STEP1)，将创建 ASP.NET Web API 支持的应用程序的所有创建、 读取、 更新和删除 (CRUD) 操作来管理书籍目录。</span><span class="sxs-lookup"><span data-stu-id="869e6-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="869e6-111">此应用程序将使用[示例 XML 文件 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx)从 MSDN。</span><span class="sxs-lookup"><span data-stu-id="869e6-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="869e6-112">在[倒数第二次本教程的组成部分](#STEP2)，将创建一个从 Web API 应用程序中检索数据的互动的 Windows Phone 8 应用程序。</span><span class="sxs-lookup"><span data-stu-id="869e6-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="869e6-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="869e6-113">Prerequisites</span></span>

- <span data-ttu-id="869e6-114">与安装的 Windows Phone 8 SDK 的 visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="869e6-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="869e6-115">Windows 8 或更高版本上安装 HYPER-V 的 64 位系统</span><span class="sxs-lookup"><span data-stu-id="869e6-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="869e6-116">有关其他要求的列表，请参阅*系统要求*节[Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下载页。</span><span class="sxs-lookup"><span data-stu-id="869e6-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="869e6-117">如果你要测试 Web API 与您的本地系统上的 Windows Phone 8 项目之间的连接，你将需要按照中的说明*[连接到位于本地的 Web API 应用程序的 Windows Phone 8 模拟器计算机](https://go.microsoft.com/fwlink/?LinkId=324014)*文章以设置你的测试环境。</span><span class="sxs-lookup"><span data-stu-id="869e6-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>


<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="869e6-118">步骤 1： 创建 Web API Bookstore 项目</span><span class="sxs-lookup"><span data-stu-id="869e6-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="869e6-119">本端到端教程的第一步是创建支持所有的 CRUD 操作; Web API 项目请注意，会将 Windows Phone 应用程序项目添加到此解决方案中[步骤 2](#STEP2)本教程。</span><span class="sxs-lookup"><span data-stu-id="869e6-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="869e6-120">打开**Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="869e6-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="869e6-121">单击**文件**，然后**新**，，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="869e6-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="869e6-122">当**新项目**显示对话框中，展开**已安装**，然后**模板**，然后**Visual C#**，，然后**Web**。</span><span class="sxs-lookup"><span data-stu-id="869e6-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

    | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
    | --- |
    | <span data-ttu-id="869e6-123">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-123">Click image to expand</span></span> |
4. <span data-ttu-id="869e6-124">突出显示**ASP.NET Web 应用程序**，输入**BookStore**作为项目名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="869e6-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="869e6-125">当**新建 ASP.NET 项目**显示对话框中，选择**Web API**模板，，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="869e6-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

    | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
    | --- |
    | <span data-ttu-id="869e6-126">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-126">Click image to expand</span></span> |
6. <span data-ttu-id="869e6-127">当 Web API 项目打开后时，请从项目中删除示例控制器：</span><span class="sxs-lookup"><span data-stu-id="869e6-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="869e6-128">展开**控制器**在解决方案资源管理器的文件夹。</span><span class="sxs-lookup"><span data-stu-id="869e6-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="869e6-129">右键单击**ValuesController.cs**文件，，然后单击**删除**。</span><span class="sxs-lookup"><span data-stu-id="869e6-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="869e6-130">单击**确定**当系统提示确认删除。</span><span class="sxs-lookup"><span data-stu-id="869e6-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="869e6-131">将 XML 数据文件添加到 Web API 项目中;此文件包含 bookstore 目录的内容：</span><span class="sxs-lookup"><span data-stu-id="869e6-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

    1. <span data-ttu-id="869e6-132">右键单击**应用\_数据**文件夹在解决方案资源管理器，然后单击**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="869e6-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
    2. <span data-ttu-id="869e6-133">当**添加新项**显示对话框中，突出显示**XML 文件**模板。</span><span class="sxs-lookup"><span data-stu-id="869e6-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
    3. <span data-ttu-id="869e6-134">命名该文件**Books.xml**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="869e6-134">Name the file **Books.xml**, and then click **Add**.</span></span>
    4. <span data-ttu-id="869e6-135">当**Books.xml**打开文件，并将替换中的示例 XML 文件中的代码**books.xml** MSDN 上的文件：</span><span class="sxs-lookup"><span data-stu-id="869e6-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
    5. <span data-ttu-id="869e6-136">保存并关闭 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-136">Save and close the XML file.</span></span>
8. <span data-ttu-id="869e6-137">将 bookstore 模型添加到 Web API 项目中;此模型包含 bookstore 应用程序的创建、 读取、 更新和删除 (CRUD) 逻辑：</span><span class="sxs-lookup"><span data-stu-id="869e6-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

    1. <span data-ttu-id="869e6-138">右键单击**模型**文件夹在解决方案资源管理器，然后单击**添加**，然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="869e6-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
    2. <span data-ttu-id="869e6-139">当**添加新项**显示对话框中，命名类文件**BookDetails.cs**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="869e6-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
    3. <span data-ttu-id="869e6-140">当**BookDetails.cs**打开文件，将替换为以下文件中的代码：</span><span class="sxs-lookup"><span data-stu-id="869e6-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
    4. <span data-ttu-id="869e6-141">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-141">Save and close the **BookDetails.cs** file.</span></span>
9. <span data-ttu-id="869e6-142">将 bookstore 控制器添加到 Web API 项目：</span><span class="sxs-lookup"><span data-stu-id="869e6-142">Add the bookstore controller to the Web API project:</span></span>

    1. <span data-ttu-id="869e6-143">右键单击**控制器**文件夹在解决方案资源管理器，然后单击**添加**，然后单击**控制器**。</span><span class="sxs-lookup"><span data-stu-id="869e6-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
    2. <span data-ttu-id="869e6-144">当**添加基架**显示对话框中，突出显示**Web API 2 Controller-Empty**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="869e6-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
    3. <span data-ttu-id="869e6-145">当**添加控制器**显示对话框中，控制器**BooksController**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="869e6-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
    4. <span data-ttu-id="869e6-146">当**BooksController.cs**打开文件，将替换为以下文件中的代码：</span><span class="sxs-lookup"><span data-stu-id="869e6-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
    5. <span data-ttu-id="869e6-147">保存并关闭**BooksController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-147">Save and close the **BooksController.cs** file.</span></span>
10. <span data-ttu-id="869e6-148">生成的 Web API 应用程序来检查有错误。</span><span class="sxs-lookup"><span data-stu-id="869e6-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="869e6-149">步骤 2： 添加 Windows Phone 8 Bookstore 目录项目</span><span class="sxs-lookup"><span data-stu-id="869e6-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="869e6-150">此端到端方案中的下一步是创建 Windows Phone 8 目录应用程序。</span><span class="sxs-lookup"><span data-stu-id="869e6-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="869e6-151">此应用程序将使用*Windows Phone 数据绑定应用*模板默认用户界面，并且将使用的 Web API 应用程序中创建[步骤 1](#STEP1)作为数据源本教程。</span><span class="sxs-lookup"><span data-stu-id="869e6-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="869e6-152">右键单击**BookStore**中的解决方案在解决方案资源管理器，然后单击**添加**，，然后**新项目**。</span><span class="sxs-lookup"><span data-stu-id="869e6-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="869e6-153">当**新项目**显示对话框中，展开**已安装**，然后**Visual C#**，，然后**Windows Phone**。</span><span class="sxs-lookup"><span data-stu-id="869e6-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="869e6-154">突出显示**Windows Phone 数据绑定应用**，输入**BookCatalog**作为名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="869e6-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="869e6-155">向其中添加 Json.NET NuGet 包**BookCatalog**项目：</span><span class="sxs-lookup"><span data-stu-id="869e6-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="869e6-156">右键单击**引用**为**BookCatalog**项目在解决方案资源管理器，，然后单击**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="869e6-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="869e6-157">当**管理 NuGet 包**显示对话框中，展开**联机**部分，并突出显示**nuget.org**。</span><span class="sxs-lookup"><span data-stu-id="869e6-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="869e6-158">输入**Json.NET**在搜索字段，然后单击搜索图标。</span><span class="sxs-lookup"><span data-stu-id="869e6-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="869e6-159">突出显示**Json.NET**在搜索结果中，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="869e6-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="869e6-160">安装完成后，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="869e6-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="869e6-161">添加**BookDetails**模型到**BookCatalog**项目; 这包含 bookstore 类泛型模型：</span><span class="sxs-lookup"><span data-stu-id="869e6-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

    1. <span data-ttu-id="869e6-162">右键单击**BookCatalog**项目在解决方案资源管理器，然后单击**添加**，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="869e6-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
    2. <span data-ttu-id="869e6-163">将新文件夹命名**模型**。</span><span class="sxs-lookup"><span data-stu-id="869e6-163">Name the new folder **Models**.</span></span>
    3. <span data-ttu-id="869e6-164">右键单击**模型**文件夹在解决方案资源管理器，然后单击**添加**，然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="869e6-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
    4. <span data-ttu-id="869e6-165">当**添加新项**显示对话框中，命名类文件**BookDetails.cs**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="869e6-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
    5. <span data-ttu-id="869e6-166">当**BookDetails.cs**打开文件，将替换为以下文件中的代码：</span><span class="sxs-lookup"><span data-stu-id="869e6-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
    6. <span data-ttu-id="869e6-167">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-167">Save and close the **BookDetails.cs** file.</span></span>
6. <span data-ttu-id="869e6-168">更新**MainViewModel.cs**类，以包含与 BookStore Web API 应用程序进行通信的功能：</span><span class="sxs-lookup"><span data-stu-id="869e6-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

    1. <span data-ttu-id="869e6-169">展开**Viewmodel**文件夹中的解决方案资源管理器，然后双击**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
    2. <span data-ttu-id="869e6-170">当**MainViewModel.cs**打开文件时，将替换为以下文件中的代码; 请注意，你将需要更新的值`apiUrl`常量替换你的 Web API 的实际 URL:</span><span class="sxs-lookup"><span data-stu-id="869e6-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

        [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
    3. <span data-ttu-id="869e6-171">保存并关闭**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-171">Save and close the **MainViewModel.cs** file.</span></span>
7. <span data-ttu-id="869e6-172">更新**MainPage.xaml**文件以自定义应用程序名称：</span><span class="sxs-lookup"><span data-stu-id="869e6-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

    1. <span data-ttu-id="869e6-173">双击**MainPage.xaml**在解决方案资源管理器中的文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
    2. <span data-ttu-id="869e6-174">当**MainPage.xaml**打开文件，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="869e6-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
    3. <span data-ttu-id="869e6-175">这些行替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="869e6-175">Replace those lines with the following:</span></span> 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
    4. <span data-ttu-id="869e6-176">保存并关闭**MainPage.xaml**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-176">Save and close the **MainPage.xaml** file.</span></span>
8. <span data-ttu-id="869e6-177">更新**DetailsPage.xaml**文件以自定义显示的项目：</span><span class="sxs-lookup"><span data-stu-id="869e6-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

    1. <span data-ttu-id="869e6-178">双击**DetailsPage.xaml**在解决方案资源管理器中的文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
    2. <span data-ttu-id="869e6-179">当**DetailsPage.xaml**打开文件，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="869e6-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
    3. <span data-ttu-id="869e6-180">这些行替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="869e6-180">Replace those lines with the following:</span></span> 

        [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
    4. <span data-ttu-id="869e6-181">保存并关闭**DetailsPage.xaml**文件。</span><span class="sxs-lookup"><span data-stu-id="869e6-181">Save and close the **DetailsPage.xaml** file.</span></span>
9. <span data-ttu-id="869e6-182">生成 Windows Phone 应用程序，以检查有错误。</span><span class="sxs-lookup"><span data-stu-id="869e6-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="869e6-183">步骤 3： 测试端到端解决方案</span><span class="sxs-lookup"><span data-stu-id="869e6-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="869e6-184">中所述*先决条件*本教程中，当测试 Web API 和 Windows Phone 8 之间的连接部分项目在您的本地系统上，将需要按照中的说明 *[连接到本地计算机上的 Web API 应用程序的 Windows Phone 8 模拟器](https://go.microsoft.com/fwlink/?LinkId=324014)*文章以设置你的测试环境。</span><span class="sxs-lookup"><span data-stu-id="869e6-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="869e6-185">配置测试环境后，你将需要将 Windows Phone 应用程序设置为启动项目。</span><span class="sxs-lookup"><span data-stu-id="869e6-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="869e6-186">为此，请突出显示**BookCatalog**在解决方案资源管理器，然后单击应用程序**设为启动项目**:</span><span class="sxs-lookup"><span data-stu-id="869e6-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="869e6-187">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-187">Click image to expand</span></span> |

<span data-ttu-id="869e6-188">按 F5 时，Visual Studio 将启动这两个 Windows Phone 仿真程序，将显示&quot;，请稍候片刻&quot;消息时从你的 Web API 检索应用程序数据：</span><span class="sxs-lookup"><span data-stu-id="869e6-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="869e6-189">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-189">Click image to expand</span></span> |

<span data-ttu-id="869e6-190">如果所有内容均成功，你应看到显示的目录：</span><span class="sxs-lookup"><span data-stu-id="869e6-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="869e6-191">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-191">Click image to expand</span></span> |

<span data-ttu-id="869e6-192">如果你点击任何书名，应用程序将显示簿说明：</span><span class="sxs-lookup"><span data-stu-id="869e6-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="869e6-193">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-193">Click image to expand</span></span> |

<span data-ttu-id="869e6-194">如果应用程序无法与你的 Web API 通信，则将显示一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="869e6-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="869e6-195">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-195">Click image to expand</span></span> |

<span data-ttu-id="869e6-196">如果你点击错误消息，将显示有关错误的任何其他详细信息：</span><span class="sxs-lookup"><span data-stu-id="869e6-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
| --- |
| <span data-ttu-id="869e6-197">单击图像以展开</span><span class="sxs-lookup"><span data-stu-id="869e6-197">Click image to expand</span></span> |
