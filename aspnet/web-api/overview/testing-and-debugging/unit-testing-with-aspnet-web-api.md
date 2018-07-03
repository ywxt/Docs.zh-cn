---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 单元测试 ASP.NET Web API 2 |Microsoft Docs
author: tfitzmac
description: 此指南和应用程序演示了如何创建 Web API 2 应用程序的简单单元测试。 本教程演示如何包含单元测试项目...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2014
ms.topic: article
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: da56b38809faf760b7c390eb76ac9c4556d635c6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376169"
---
<a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="cda20-104">单元测试 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="cda20-104">Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="cda20-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cda20-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="cda20-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="cda20-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> <span data-ttu-id="cda20-107">此指南和应用程序演示了如何创建 Web API 2 应用程序的简单单元测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="cda20-108">本教程演示如何在解决方案中，包括单元测试项目并编写检查从控制器方法的返回的值的测试方法。</span><span class="sxs-lookup"><span data-stu-id="cda20-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
> 
> <span data-ttu-id="cda20-109">本教程假定你熟悉的 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="cda20-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="cda20-110">有关介绍性教程，请参阅[Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cda20-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
> 
> <span data-ttu-id="cda20-111">本主题中的单元测试是有意仅限使用简单的数据方案。</span><span class="sxs-lookup"><span data-stu-id="cda20-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="cda20-112">单元测试更高级的数据方案中，请参阅[模拟实体框架时单元测试 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cda20-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cda20-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="cda20-113">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="cda20-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cda20-114">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="cda20-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="cda20-115">Web API 2</span></span>


## <a name="in-this-topic"></a><span data-ttu-id="cda20-116">在本主题中</span><span class="sxs-lookup"><span data-stu-id="cda20-116">In this topic</span></span>

<span data-ttu-id="cda20-117">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="cda20-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="cda20-118">先决条件</span><span class="sxs-lookup"><span data-stu-id="cda20-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="cda20-119">下载代码</span><span class="sxs-lookup"><span data-stu-id="cda20-119">Download code</span></span>](#download)
- [<span data-ttu-id="cda20-120">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-120">Create application with unit test project</span></span>](#appwithunittest)

    - [<span data-ttu-id="cda20-121">创建应用程序时添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="cda20-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="cda20-122">将单元测试项目添加到现有应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="cda20-123">设置 Web API 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="cda20-124">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="cda20-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="cda20-125">创建测试</span><span class="sxs-lookup"><span data-stu-id="cda20-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="cda20-126">运行测试</span><span class="sxs-lookup"><span data-stu-id="cda20-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="cda20-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="cda20-127">Prerequisites</span></span>

<span data-ttu-id="cda20-128">Visual Studio 2017 Community、 Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="cda20-128">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="cda20-129">下载代码</span><span class="sxs-lookup"><span data-stu-id="cda20-129">Download code</span></span>

<span data-ttu-id="cda20-130">下载[已完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="cda20-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="cda20-131">可下载项目包含本主题以及单元测试代码[模拟实体框架时单元测试 ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)主题。</span><span class="sxs-lookup"><span data-stu-id="cda20-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="cda20-132">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-132">Create application with unit test project</span></span>

<span data-ttu-id="cda20-133">可以创建单元测试项目，创建你的应用程序时，也可以将单元测试项目添加到现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="cda20-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="cda20-134">本教程演示了这两种方法用于创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="cda20-135">若要遵循本教程中，可以使用以下两种方法。</span><span class="sxs-lookup"><span data-stu-id="cda20-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="cda20-136">创建应用程序时添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="cda20-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="cda20-137">创建一个新的 ASP.NET Web 应用程序名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="cda20-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![创建项目](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="cda20-139">在新建 ASP.NET 项目窗口中，选择**空**模板和添加文件夹和核心引用有关 Web API。</span><span class="sxs-lookup"><span data-stu-id="cda20-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="cda20-140">选择**添加单元测试**选项。</span><span class="sxs-lookup"><span data-stu-id="cda20-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="cda20-141">单元测试项目将自动命名**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="cda20-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="cda20-142">可以保留此名称。</span><span class="sxs-lookup"><span data-stu-id="cda20-142">You can keep this name.</span></span>

![创建单元测试项目](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="cda20-144">创建程序后，会看到它包含两个项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-144">After creating the application, you will see it contains two projects.</span></span>

![两个项目](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="cda20-146">将单元测试项目添加到现有应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="cda20-147">如果未创建单元测试项目时创建的应用程序，则可以添加一个在任何时间。</span><span class="sxs-lookup"><span data-stu-id="cda20-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="cda20-148">例如，假设你已有应用程序名为 StoreApp，并且你想要添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="cda20-149">若要添加单元测试项目，请右键单击解决方案并选择**外**并**新项目**。</span><span class="sxs-lookup"><span data-stu-id="cda20-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![向解决方案添加新项目](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="cda20-151">选择**测试**左窗格中，然后选择**单元测试项目**对于项目类型。</span><span class="sxs-lookup"><span data-stu-id="cda20-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="cda20-152">将项目命名**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="cda20-152">Name the project **StoreApp.Tests**.</span></span>

![添加单元测试项目](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="cda20-154">您将看到你的解决方案中的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="cda20-155">在单元测试项目中，添加对原始项目的项目引用。</span><span class="sxs-lookup"><span data-stu-id="cda20-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="cda20-156">设置 Web API 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="cda20-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="cda20-157">在 StoreApp 项目中，将添加到一个类文件**模型**名为文件夹**Product.cs**。</span><span class="sxs-lookup"><span data-stu-id="cda20-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="cda20-158">将以下代码替换为该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="cda20-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="cda20-159">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="cda20-159">Build the solution.</span></span>

<span data-ttu-id="cda20-160">右键单击 Controllers 文件夹，然后选择**外**并**新基架项**。</span><span class="sxs-lookup"><span data-stu-id="cda20-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="cda20-161">选择**Web API 2 控制器-空**。</span><span class="sxs-lookup"><span data-stu-id="cda20-161">Select **Web API 2 Controller - Empty**.</span></span>

![添加新的控制器](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="cda20-163">将控制器名称设置为**SimpleProductController**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="cda20-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![指定控制器](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="cda20-165">用下面的代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="cda20-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="cda20-166">若要简化此示例中，列表而不是数据库中存储数据。</span><span class="sxs-lookup"><span data-stu-id="cda20-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="cda20-167">此类中定义的列表表示生产数据。</span><span class="sxs-lookup"><span data-stu-id="cda20-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="cda20-168">请注意，该控制器包含一系列产品对象将作为参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="cda20-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="cda20-169">此构造函数，可将测试数据传递时单元测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="cda20-170">该控制器还包含两个**异步**方法来演示单元测试异步方法。</span><span class="sxs-lookup"><span data-stu-id="cda20-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="cda20-171">这些异步方法实现通过调用**Task.FromResult**若要最大程度减少无关的代码，但通常情况下方法应包括资源密集型操作。</span><span class="sxs-lookup"><span data-stu-id="cda20-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="cda20-172">为 getproduct 方法返回的实例**IHttpActionResult**接口。</span><span class="sxs-lookup"><span data-stu-id="cda20-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="cda20-173">IHttpActionResult 是一个 Web API 2 中的新功能，这样可以简化单元测试开发。</span><span class="sxs-lookup"><span data-stu-id="cda20-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="cda20-174">实现 IHttpActionResult 接口的类中找到[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)命名空间。</span><span class="sxs-lookup"><span data-stu-id="cda20-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="cda20-175">这些类表示操作请求中可能的响应，它们对应于 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="cda20-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="cda20-176">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="cda20-176">Build the solution.</span></span>

<span data-ttu-id="cda20-177">你现已准备好设置测试项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="cda20-178">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="cda20-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="cda20-179">当使用空模板创建的应用程序时，单元测试项目 (StoreApp.Tests) 不包括任何已安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="cda20-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="cda20-180">其他模板，例如 Web API 模板中，单元测试项目中包括一些 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="cda20-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="cda20-181">对于本教程中，必须包括 Microsoft ASP.NET Web API 2 核心包到测试项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="cda20-182">右键单击 StoreApp.Tests 项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="cda20-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="cda20-183">必须选择要将包添加到该项目的 StoreApp.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="cda20-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理包](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="cda20-185">查找和安装 Microsoft ASP.NET Web API 2 核心包。</span><span class="sxs-lookup"><span data-stu-id="cda20-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安装 web api core 包](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="cda20-187">关闭管理 NuGet 包窗口。</span><span class="sxs-lookup"><span data-stu-id="cda20-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="cda20-188">创建测试</span><span class="sxs-lookup"><span data-stu-id="cda20-188">Create tests</span></span>

<span data-ttu-id="cda20-189">默认情况下，你的测试项目包括一个名为 UnitTest1.cs 的空测试文件。</span><span class="sxs-lookup"><span data-stu-id="cda20-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="cda20-190">此文件显示了用于创建测试方法的属性。</span><span class="sxs-lookup"><span data-stu-id="cda20-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="cda20-191">对单元测试，可以使用此文件，或创建你自己的文件。</span><span class="sxs-lookup"><span data-stu-id="cda20-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="cda20-193">对于本教程中，将创建测试类。</span><span class="sxs-lookup"><span data-stu-id="cda20-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="cda20-194">您可以删除 UnitTest1.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="cda20-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="cda20-195">添加名为的类**TestSimpleProductController.cs**，并将代码替换下面的代码。</span><span class="sxs-lookup"><span data-stu-id="cda20-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="cda20-196">运行测试</span><span class="sxs-lookup"><span data-stu-id="cda20-196">Run tests</span></span>

<span data-ttu-id="cda20-197">现在您就可以运行测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-197">You are now ready to run the tests.</span></span> <span data-ttu-id="cda20-198">使用标记的方法的所有**TestMethod**属性进行测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="cda20-199">从**测试**菜单项，运行测试。</span><span class="sxs-lookup"><span data-stu-id="cda20-199">From the **Test** menu item, run the tests.</span></span>

![运行测试](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="cda20-201">打开**测试资源管理器**窗口中，并请注意，测试结果。</span><span class="sxs-lookup"><span data-stu-id="cda20-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![测试结果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="cda20-203">总结</span><span class="sxs-lookup"><span data-stu-id="cda20-203">Summary</span></span>

<span data-ttu-id="cda20-204">已完成本教程。</span><span class="sxs-lookup"><span data-stu-id="cda20-204">You have completed this tutorial.</span></span> <span data-ttu-id="cda20-205">在本教程中的数据已特意简化为专注于单元测试条件。</span><span class="sxs-lookup"><span data-stu-id="cda20-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="cda20-206">单元测试更高级的数据方案中，请参阅[模拟实体框架时单元测试 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cda20-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
