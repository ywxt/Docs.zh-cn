---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: "模拟实体框架时单元测试 ASP.NET Web API 2 |Microsoft 文档"
author: tfitzmac
description: "此指南和应用程序演示如何为 Web API 2 的应用程序使用实体框架创建单元测试。 它演示如何修改..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/13/2013
ms.topic: article
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: abfde7edec85812de3560f4edefb110c3e374580
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
<a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="97b7b-104">模拟实体框架时单元测试 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="97b7b-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="97b7b-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="97b7b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="97b7b-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="97b7b-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> <span data-ttu-id="97b7b-107">此指南和应用程序演示如何为 Web API 2 的应用程序使用实体框架创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="97b7b-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="97b7b-108">它显示如何修改基架的控制器，以便传递的上下文对象，用于测试，以及如何创建测试对象，用于处理与实体框架。</span><span class="sxs-lookup"><span data-stu-id="97b7b-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
> 
> <span data-ttu-id="97b7b-109">有关使用 ASP.NET Web API 进行单元测试的简介，请参阅[使用 ASP.NET Web API 2 进行单元测试](unit-testing-with-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="97b7b-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
> 
> <span data-ttu-id="97b7b-110">本教程假定你熟悉的 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="97b7b-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="97b7b-111">有关介绍性教程，请参阅[Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="97b7b-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="97b7b-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="97b7b-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="97b7b-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="97b7b-113">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="97b7b-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="97b7b-114">Web API 2</span></span>


## <a name="in-this-topic"></a><span data-ttu-id="97b7b-115">在本主题中</span><span class="sxs-lookup"><span data-stu-id="97b7b-115">In this topic</span></span>

<span data-ttu-id="97b7b-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="97b7b-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="97b7b-117">先决条件</span><span class="sxs-lookup"><span data-stu-id="97b7b-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="97b7b-118">下载代码</span><span class="sxs-lookup"><span data-stu-id="97b7b-118">Download code</span></span>](#download)
- [<span data-ttu-id="97b7b-119">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="97b7b-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="97b7b-120">创建模型类</span><span class="sxs-lookup"><span data-stu-id="97b7b-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="97b7b-121">添加控制器</span><span class="sxs-lookup"><span data-stu-id="97b7b-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="97b7b-122">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="97b7b-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="97b7b-123">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="97b7b-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="97b7b-124">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="97b7b-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="97b7b-125">创建测试</span><span class="sxs-lookup"><span data-stu-id="97b7b-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="97b7b-126">运行测试</span><span class="sxs-lookup"><span data-stu-id="97b7b-126">Run tests</span></span>](#runtests)

<span data-ttu-id="97b7b-127">如果你已经完成中的步骤[使用 ASP.NET Web API 2 进行单元测试](unit-testing-with-aspnet-web-api.md)，你可以跳到部分[添加控制器](#controller)。</span><span class="sxs-lookup"><span data-stu-id="97b7b-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="97b7b-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="97b7b-128">Prerequisites</span></span>

<span data-ttu-id="97b7b-129">Visual Studio 2017 Community、 Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="97b7b-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="97b7b-130">下载代码</span><span class="sxs-lookup"><span data-stu-id="97b7b-130">Download code</span></span>

<span data-ttu-id="97b7b-131">下载[已完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="97b7b-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="97b7b-132">可下载的项目包含本主题和单元测试代码[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主题。</span><span class="sxs-lookup"><span data-stu-id="97b7b-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="97b7b-133">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="97b7b-133">Create application with unit test project</span></span>

<span data-ttu-id="97b7b-134">可以创建单元测试项目，创建你的应用程序时，也可以将单元测试项目添加到现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="97b7b-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="97b7b-135">本教程演示创建应用程序时创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="97b7b-136">创建一个新的 ASP.NET Web 应用程序名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="97b7b-137">在新建 ASP.NET 项目窗口中，选择**空**模板并添加文件夹和核心 Web api 的引用。</span><span class="sxs-lookup"><span data-stu-id="97b7b-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="97b7b-138">选择**添加单元测试**选项。</span><span class="sxs-lookup"><span data-stu-id="97b7b-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="97b7b-139">单元测试项目将自动命名**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="97b7b-140">你可以保留此名称。</span><span class="sxs-lookup"><span data-stu-id="97b7b-140">You can keep this name.</span></span>

![创建单元测试项目](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="97b7b-142">在创建应用程序，你将看到它包含两个项目- **StoreApp**和**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="97b7b-143">创建模型类</span><span class="sxs-lookup"><span data-stu-id="97b7b-143">Create the model class</span></span>

<span data-ttu-id="97b7b-144">在 StoreApp 项目中，添加的类文件，以便**模型**文件夹名为**Product.cs**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="97b7b-145">文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="97b7b-146">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="97b7b-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="97b7b-147">添加控制器</span><span class="sxs-lookup"><span data-stu-id="97b7b-147">Add the controller</span></span>

<span data-ttu-id="97b7b-148">右键单击 Controllers 文件夹，然后选择**添加**和**新建基架项**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="97b7b-149">选择其操作使用 Entity Framework 的 Web API 2 控制器。</span><span class="sxs-lookup"><span data-stu-id="97b7b-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![添加新控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="97b7b-151">设置下列值：</span><span class="sxs-lookup"><span data-stu-id="97b7b-151">Set the following values:</span></span>

- <span data-ttu-id="97b7b-152">控制器名称： **ProductController**</span><span class="sxs-lookup"><span data-stu-id="97b7b-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="97b7b-153">模型类：**产品**</span><span class="sxs-lookup"><span data-stu-id="97b7b-153">Model class: **Product**</span></span>
- <span data-ttu-id="97b7b-154">数据上下文类: [选择**新建数据上下文**按钮，这在如下所示的值填充]</span><span class="sxs-lookup"><span data-stu-id="97b7b-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="97b7b-156">单击**添加**以自动生成的代码创建控制器。</span><span class="sxs-lookup"><span data-stu-id="97b7b-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="97b7b-157">代码包括用于创建、 检索、 更新和删除产品类的实例方法。</span><span class="sxs-lookup"><span data-stu-id="97b7b-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="97b7b-158">下面的代码演示了方法对于添加产品。</span><span class="sxs-lookup"><span data-stu-id="97b7b-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="97b7b-159">请注意该方法返回的实例**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="97b7b-160">IHttpActionResult 是一个 Web API 2 中的新功能，它简化了单元测试开发。</span><span class="sxs-lookup"><span data-stu-id="97b7b-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="97b7b-161">在下一步的部分中，你将自定义生成的代码以简化将测试对象传递给控制器。</span><span class="sxs-lookup"><span data-stu-id="97b7b-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="97b7b-162">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="97b7b-162">Add dependency injection</span></span>

<span data-ttu-id="97b7b-163">目前，ProductController 类是硬编码为使用 StoreAppContext 类的实例。</span><span class="sxs-lookup"><span data-stu-id="97b7b-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="97b7b-164">调用依赖关系注入的模式将用于修改你的应用程序并删除该硬编码的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="97b7b-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="97b7b-165">通过打破这种依赖性，您可以传入的模拟对象测试时。</span><span class="sxs-lookup"><span data-stu-id="97b7b-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="97b7b-166">右键单击**模型**文件夹，并添加名为的新接口**IStoreAppContext**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="97b7b-167">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="97b7b-168">打开 StoreAppContext.cs 文件并进行以下突出显示的更改。</span><span class="sxs-lookup"><span data-stu-id="97b7b-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="97b7b-169">要注意的重要的更改是：</span><span class="sxs-lookup"><span data-stu-id="97b7b-169">The important changes to note are:</span></span>

- <span data-ttu-id="97b7b-170">StoreAppContext 类可实现 IStoreAppContext 接口</span><span class="sxs-lookup"><span data-stu-id="97b7b-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="97b7b-171">实现 MarkAsModified 方法</span><span class="sxs-lookup"><span data-stu-id="97b7b-171">MarkAsModified method is implemented</span></span>


[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="97b7b-172">打开 ProductController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="97b7b-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="97b7b-173">更改现有代码以匹配突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="97b7b-174">这些更改在 StoreAppContext 中断依赖项，并启用其他类来在不同对象中传递上下文类。</span><span class="sxs-lookup"><span data-stu-id="97b7b-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="97b7b-175">此更改将使你在单元测试期间在测试上下文中传递。</span><span class="sxs-lookup"><span data-stu-id="97b7b-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="97b7b-176">没有一次的多个更改，则必须在 ProductController 进行。</span><span class="sxs-lookup"><span data-stu-id="97b7b-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="97b7b-177">在**PutProduct**方法中，替换的实体状态设置为行修改通过 MarkAsModified 方法调用。</span><span class="sxs-lookup"><span data-stu-id="97b7b-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="97b7b-178">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="97b7b-178">Build the solution.</span></span>

<span data-ttu-id="97b7b-179">你现已准备好设置测试项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="97b7b-180">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="97b7b-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="97b7b-181">当你使用空模板创建应用程序时，单元测试项目 (StoreApp.Tests) 不包括任何已安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="97b7b-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="97b7b-182">其他模板，例如 Web API 模板中，将一些 NuGet 程序包包括在单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="97b7b-183">对于本教程，你必须包括实体框架包时和测试项目的 Microsoft ASP.NET Web API 2 核心程序包。</span><span class="sxs-lookup"><span data-stu-id="97b7b-183">For this tutorial, you must include the Entity Framework packge and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="97b7b-184">右键单击 StoreApp.Tests 项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="97b7b-185">必须选择要将包添加到该项目 StoreApp.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="97b7b-187">从联机程序包中，查找和安装 EntityFramework 包 （版本 6.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="97b7b-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="97b7b-188">如果显示 EntityFramework 包已安装，您可能选择 StoreApp 项目而不是 StoreApp.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![添加实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="97b7b-190">查找和安装 Microsoft ASP.NET Web API 2 核心包。</span><span class="sxs-lookup"><span data-stu-id="97b7b-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安装 web api 核心程序包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="97b7b-192">关闭管理 NuGet 包窗口。</span><span class="sxs-lookup"><span data-stu-id="97b7b-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="97b7b-193">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="97b7b-193">Create test context</span></span>

<span data-ttu-id="97b7b-194">添加一个名为类**TestDbSet**向测试项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="97b7b-195">此类用作测试数据集的基类。</span><span class="sxs-lookup"><span data-stu-id="97b7b-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="97b7b-196">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="97b7b-197">添加一个名为类**TestProductDbSet**向该测试项目，其中包含下面的代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="97b7b-198">添加一个名为类**TestStoreAppContext**和替换为以下代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="97b7b-199">创建测试</span><span class="sxs-lookup"><span data-stu-id="97b7b-199">Create tests</span></span>

<span data-ttu-id="97b7b-200">默认情况下，你的测试项目包括名为一个空的测试文件**UnitTest1.cs**。</span><span class="sxs-lookup"><span data-stu-id="97b7b-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="97b7b-201">此文件显示了用于创建测试方法的特性。</span><span class="sxs-lookup"><span data-stu-id="97b7b-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="97b7b-202">对于本教程中，您可以删除此文件，因为你将添加一个新测试类。</span><span class="sxs-lookup"><span data-stu-id="97b7b-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="97b7b-203">添加一个名为类**TestProductController**向测试项目。</span><span class="sxs-lookup"><span data-stu-id="97b7b-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="97b7b-204">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="97b7b-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="97b7b-205">运行测试</span><span class="sxs-lookup"><span data-stu-id="97b7b-205">Run tests</span></span>

<span data-ttu-id="97b7b-206">现在你就可以运行测试。</span><span class="sxs-lookup"><span data-stu-id="97b7b-206">You are now ready to run the tests.</span></span> <span data-ttu-id="97b7b-207">所有使用标记的方法**TestMethod**将测试属性。</span><span class="sxs-lookup"><span data-stu-id="97b7b-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="97b7b-208">从**测试**菜单项，运行测试。</span><span class="sxs-lookup"><span data-stu-id="97b7b-208">From the **Test** menu item, run the tests.</span></span>

![运行测试](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="97b7b-210">打开**测试资源管理器**窗口中，并注意测试的结果。</span><span class="sxs-lookup"><span data-stu-id="97b7b-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![测试结果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
