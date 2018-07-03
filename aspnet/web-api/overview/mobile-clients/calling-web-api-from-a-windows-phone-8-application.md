---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 调用 Web API 从 Windows Phone 8 应用程序 (C#) |Microsoft Docs
author: rmcmurray
description: 创建完整的端到端方案包含的 ASP.NET Web API 应用程序提供了一个 Windows Phone 8 应用程序的本书籍的目录。
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/09/2013
ms.topic: article
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: 40be2935c52e7dcab9e682d4d15e9e75c0260223
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388417"
---
<a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="98a41-103">调用 Web API 从 Windows Phone 8 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="98a41-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>
====================
<span data-ttu-id="98a41-104">通过[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="98a41-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="98a41-105">在本教程中，您将学习如何创建完整的端到端方案包含的 ASP.NET Web API 应用程序提供了一个 Windows Phone 8 应用程序的本书籍的目录。</span><span class="sxs-lookup"><span data-stu-id="98a41-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="98a41-106">概述</span><span class="sxs-lookup"><span data-stu-id="98a41-106">Overview</span></span>

<span data-ttu-id="98a41-107">如 ASP.NET Web API rESTful 服务通过抽象化为服务器端和客户端应用程序的体系结构简化面向开发人员的基于 HTTP 的应用程序的创建。</span><span class="sxs-lookup"><span data-stu-id="98a41-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="98a41-108">而不是创建一种专有的基于套接字协议进行通信，Web API 开发人员只需发布自己的应用程序的必需 HTTP 方法 (例如： GET、 POST、 PUT、 DELETE)，并且客户端应用程序开发人员只需要使用所其应用程序所需的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="98a41-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="98a41-109">在本端到端教程，您将学习如何使用 Web API 来创建以下项目：</span><span class="sxs-lookup"><span data-stu-id="98a41-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="98a41-110">在中[此教程的第一部分](#STEP1)，将创建支持所有创建、 读取、 更新和删除 (CRUD) 操作来管理书籍目录的 ASP.NET Web API 应用程序。</span><span class="sxs-lookup"><span data-stu-id="98a41-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="98a41-111">此应用程序将使用[示例 XML 文件 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx)从 MSDN。</span><span class="sxs-lookup"><span data-stu-id="98a41-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="98a41-112">在中[在本教程的第二个](#STEP2)，将创建从 Web API 应用程序中检索数据的交互式 Windows Phone 8 应用程序。</span><span class="sxs-lookup"><span data-stu-id="98a41-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="98a41-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="98a41-113">Prerequisites</span></span>

- <span data-ttu-id="98a41-114">已安装 Windows Phone 8 sdk 的 visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="98a41-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="98a41-115">Windows 8 或更高版本上安装 HYPER-V 的 64 位系统</span><span class="sxs-lookup"><span data-stu-id="98a41-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="98a41-116">有关其他要求的列表，请参阅*系统要求*部分[Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下载页。</span><span class="sxs-lookup"><span data-stu-id="98a41-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="98a41-117">如果要测试 Web API 和本地系统上的 Windows Phone 8 项目之间的连接，你将需要按照中的说明*[连接到本地的 Web API 应用程序的 Windows Phone 8 仿真程序计算机](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文，设置测试环境。</span><span class="sxs-lookup"><span data-stu-id="98a41-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>


<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="98a41-118">步骤 1： 创建 Web API 书店项目</span><span class="sxs-lookup"><span data-stu-id="98a41-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="98a41-119">本端到端教程的第一步是创建的所有 CRUD 操作; 支持的 Web API 项目请注意，将向此解决方案中添加 Windows Phone 应用程序项目[步骤 2](#STEP2)本教程。</span><span class="sxs-lookup"><span data-stu-id="98a41-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="98a41-120">打开**Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="98a41-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="98a41-121">单击**文件**，然后**新**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="98a41-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="98a41-122">当**新的项目**对话框中，展开**已安装**，然后**模板**，然后**Visual C#**，，然后**Web**。</span><span class="sxs-lookup"><span data-stu-id="98a41-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="98a41-123">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-123">Click image to expand</span></span>                                                                |


4. <span data-ttu-id="98a41-124">突出显示**ASP.NET Web 应用程序**，输入**书店**以及该项目名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="98a41-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="98a41-125">当**新建 ASP.NET 项目**对话框中，选择**Web API**模板，，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="98a41-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="98a41-126">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-126">Click image to expand</span></span>                                                                |


6. <span data-ttu-id="98a41-127">Web API 项目打开后，从项目中删除示例控制器：</span><span class="sxs-lookup"><span data-stu-id="98a41-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="98a41-128">展开**控制器**在解决方案资源管理器中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="98a41-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="98a41-129">右键单击**ValuesController.cs**文件，，然后单击**删除**。</span><span class="sxs-lookup"><span data-stu-id="98a41-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="98a41-130">单击**确定**当系统提示你确认删除。</span><span class="sxs-lookup"><span data-stu-id="98a41-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="98a41-131">将 XML 数据文件添加到 Web API 项目中;此文件包含书店目录的内容：</span><span class="sxs-lookup"><span data-stu-id="98a41-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="98a41-132">右键单击**应用程序\_数据**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="98a41-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="98a41-133">当**添加新项**对话框中，突出显示**XML 文件**模板。</span><span class="sxs-lookup"><span data-stu-id="98a41-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="98a41-134">将文件命名**Books.xml**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="98a41-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="98a41-135">当**Books.xml**打开文件，并替换的示例 XML 文件中的代码**books.xml** MSDN 上的文件：</span><span class="sxs-lookup"><span data-stu-id="98a41-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="98a41-136">保存并关闭 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="98a41-137">将书店模型添加到 Web API 项目中;此模型包含的书店应用程序的创建、 读取、 更新和删除 (CRUD) 逻辑：</span><span class="sxs-lookup"><span data-stu-id="98a41-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="98a41-138">右键单击**模型**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="98a41-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="98a41-139">当**添加新项**对话框中，将该类文件命名**BookDetails.cs**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="98a41-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="98a41-140">当**BookDetails.cs**打开文件、 文件中的代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="98a41-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="98a41-141">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="98a41-142">将书店控制器添加到 Web API 项目：</span><span class="sxs-lookup"><span data-stu-id="98a41-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="98a41-143">右键单击**控制器**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**控制器**。</span><span class="sxs-lookup"><span data-stu-id="98a41-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="98a41-144">当**添加基架**对话框中，突出显示**Web API 2 控制器-空**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="98a41-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="98a41-145">当**添加控制器**对话框中，将控制器命名**BooksController**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="98a41-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="98a41-146">当**BooksController.cs**打开文件、 文件中的代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="98a41-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="98a41-147">保存并关闭**BooksController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="98a41-148">构建 Web API 应用程序，以检查有错误。</span><span class="sxs-lookup"><span data-stu-id="98a41-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="98a41-149">步骤 2： 添加 Windows Phone 8 书店目录项目</span><span class="sxs-lookup"><span data-stu-id="98a41-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="98a41-150">此端到端方案的下一步是创建 Windows Phone 8 目录应用程序。</span><span class="sxs-lookup"><span data-stu-id="98a41-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="98a41-151">此应用程序将使用*Windows Phone 数据绑定应用*模板的默认用户界面，并且它将使用你在中创建的 Web API 应用程序[第 1 步](#STEP1)的本教程中作为数据源。</span><span class="sxs-lookup"><span data-stu-id="98a41-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="98a41-152">右键单击**书店**中的解决方案在解决方案资源管理器，然后单击**添加**，然后**新项目**。</span><span class="sxs-lookup"><span data-stu-id="98a41-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="98a41-153">当**新项目**对话框中，展开**已安装**，然后**Visual C#**，然后**Windows Phone**。</span><span class="sxs-lookup"><span data-stu-id="98a41-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="98a41-154">突出显示**Windows Phone 数据绑定应用**，输入**BookCatalog**作为名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="98a41-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="98a41-155">添加到 Json.NET NuGet 包**BookCatalog**项目：</span><span class="sxs-lookup"><span data-stu-id="98a41-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="98a41-156">右键单击**引用**有关**BookCatalog**项目在解决方案资源管理器中，然后单击**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="98a41-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="98a41-157">当**管理 NuGet 包**对话框中，展开**联机**部分，并突出显示**nuget.org**。</span><span class="sxs-lookup"><span data-stu-id="98a41-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="98a41-158">输入**Json.NET**在搜索字段，然后单击搜索图标。</span><span class="sxs-lookup"><span data-stu-id="98a41-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="98a41-159">突出显示**Json.NET**在搜索结果中，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="98a41-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="98a41-160">安装完成后，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="98a41-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="98a41-161">添加**BookDetails**模型到**BookCatalog**项目; 这包含书店类的常规模型：</span><span class="sxs-lookup"><span data-stu-id="98a41-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="98a41-162">右键单击**BookCatalog**项目在解决方案资源管理器，然后单击**添加**，然后单击**新文件夹**。</span><span class="sxs-lookup"><span data-stu-id="98a41-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="98a41-163">将新文件夹命名**模型**。</span><span class="sxs-lookup"><span data-stu-id="98a41-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="98a41-164">右键单击**模型**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="98a41-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="98a41-165">当**添加新项**对话框中，将该类文件命名**BookDetails.cs**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="98a41-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="98a41-166">当**BookDetails.cs**打开文件、 文件中的代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="98a41-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="98a41-167">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="98a41-168">更新**MainViewModel.cs**类，以包含与书店 Web API 应用程序进行通信的功能：</span><span class="sxs-lookup"><span data-stu-id="98a41-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="98a41-169">展开**Viewmodel**文件夹中的解决方案资源管理器，然后再双击**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="98a41-170">当**MainViewModel.cs**打开文件时，文件中的代码替换为以下; 请注意，你将需要更新的值`apiUrl`常量与您的 Web API 的实际 URL:</span><span class="sxs-lookup"><span data-stu-id="98a41-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="98a41-171">保存并关闭**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="98a41-172">更新**MainPage.xaml**文件以自定义应用程序名称：</span><span class="sxs-lookup"><span data-stu-id="98a41-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="98a41-173">双击**MainPage.xaml**在解决方案资源管理器中的文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="98a41-174">当**MainPage.xaml**打开文件，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="98a41-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="98a41-175">使用以下内容替换这些行：</span><span class="sxs-lookup"><span data-stu-id="98a41-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="98a41-176">保存并关闭**MainPage.xaml**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="98a41-177">更新**DetailsPage.xaml**文件以自定义显示的项：</span><span class="sxs-lookup"><span data-stu-id="98a41-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="98a41-178">双击**DetailsPage.xaml**在解决方案资源管理器中的文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="98a41-179">当**DetailsPage.xaml**打开文件，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="98a41-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="98a41-180">使用以下内容替换这些行：</span><span class="sxs-lookup"><span data-stu-id="98a41-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="98a41-181">保存并关闭**DetailsPage.xaml**文件。</span><span class="sxs-lookup"><span data-stu-id="98a41-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="98a41-182">构建 Windows Phone 应用程序，以检查有错误。</span><span class="sxs-lookup"><span data-stu-id="98a41-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="98a41-183">步骤 3： 测试端到端解决方案</span><span class="sxs-lookup"><span data-stu-id="98a41-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="98a41-184">如中所述*先决条件*本教程中，在测试 Web API 和 Windows Phone 8 之间的连接时的部分项目在本地系统上，将需要按照中的说明 *[连接到本地计算机上的 Web API 应用程序的 Windows Phone 8 仿真程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文，设置测试环境。</span><span class="sxs-lookup"><span data-stu-id="98a41-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="98a41-185">配置测试环境后，需要将 Windows Phone 应用程序设置为启动项目。</span><span class="sxs-lookup"><span data-stu-id="98a41-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="98a41-186">若要执行此操作，突出显示**BookCatalog**应用程序在解决方案资源管理器，然后单击**设为启动项目**:</span><span class="sxs-lookup"><span data-stu-id="98a41-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="98a41-187">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-187">Click image to expand</span></span> |

<span data-ttu-id="98a41-188">按 F5 时，Visual Studio 将启动这两个 Windows Phone 仿真程序，将显示&quot;稍候&quot;消息而从 Web API 中检索应用程序数据：</span><span class="sxs-lookup"><span data-stu-id="98a41-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="98a41-189">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-189">Click image to expand</span></span> |

<span data-ttu-id="98a41-190">如果所有内容均成功，应看到显示的目录：</span><span class="sxs-lookup"><span data-stu-id="98a41-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="98a41-191">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-191">Click image to expand</span></span> |

<span data-ttu-id="98a41-192">如果点击任何书籍标题时，应用程序将显示书籍说明：</span><span class="sxs-lookup"><span data-stu-id="98a41-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="98a41-193">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-193">Click image to expand</span></span> |

<span data-ttu-id="98a41-194">如果应用程序不能使用的 Web API 进行通信，将显示一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="98a41-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="98a41-195">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-195">Click image to expand</span></span> |

<span data-ttu-id="98a41-196">如果点击错误消息时，将显示有关错误的任何其他详细信息：</span><span class="sxs-lookup"><span data-stu-id="98a41-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>


| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="98a41-197">单击以展开的图像</span><span class="sxs-lookup"><span data-stu-id="98a41-197">Click image to expand</span></span>                                                                 |

