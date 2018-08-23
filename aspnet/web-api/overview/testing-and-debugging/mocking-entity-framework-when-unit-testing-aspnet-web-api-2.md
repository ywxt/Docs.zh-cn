---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 模拟 Entity Framework 时的单元测试 ASP.NET Web API 2 |Microsoft Docs
author: tfitzmac
description: 此指南和应用程序演示如何为 Web API 2 应用程序使用实体框架创建单元测试。 它演示了如何修改...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 0bc5ab59583a2be3f889ba05d26c6cda4589057d
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833488"
---
<a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="ff619-104">模拟 Entity Framework 时的单元测试 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="ff619-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="ff619-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ff619-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="ff619-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="ff619-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="ff619-107">此指南和应用程序演示如何为 Web API 2 应用程序使用实体框架创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="ff619-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="ff619-108">它显示了如何修改已搭建基架的控制器，以启用传递上下文对象进行测试，以及如何创建使用实体框架的测试对象。</span><span class="sxs-lookup"><span data-stu-id="ff619-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
> 
> <span data-ttu-id="ff619-109">使用 ASP.NET Web API 进行单元测试的简介，请参阅[Unit Testing 与 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="ff619-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
> 
> <span data-ttu-id="ff619-110">本教程假定你熟悉的 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="ff619-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="ff619-111">有关介绍性教程，请参阅[Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="ff619-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ff619-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ff619-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="ff619-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ff619-113">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="ff619-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="ff619-114">Web API 2</span></span>


## <a name="in-this-topic"></a><span data-ttu-id="ff619-115">在本主题中</span><span class="sxs-lookup"><span data-stu-id="ff619-115">In this topic</span></span>

<span data-ttu-id="ff619-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="ff619-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="ff619-117">先决条件</span><span class="sxs-lookup"><span data-stu-id="ff619-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="ff619-118">下载代码</span><span class="sxs-lookup"><span data-stu-id="ff619-118">Download code</span></span>](#download)
- [<span data-ttu-id="ff619-119">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="ff619-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="ff619-120">创建模型类</span><span class="sxs-lookup"><span data-stu-id="ff619-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="ff619-121">添加控制器</span><span class="sxs-lookup"><span data-stu-id="ff619-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="ff619-122">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="ff619-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="ff619-123">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ff619-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="ff619-124">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="ff619-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="ff619-125">创建测试</span><span class="sxs-lookup"><span data-stu-id="ff619-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="ff619-126">运行测试</span><span class="sxs-lookup"><span data-stu-id="ff619-126">Run tests</span></span>](#runtests)

<span data-ttu-id="ff619-127">如果你已完成中的步骤[Unit Testing 与 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，则可以跳到部分[添加控制器](#controller)。</span><span class="sxs-lookup"><span data-stu-id="ff619-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="ff619-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="ff619-128">Prerequisites</span></span>

<span data-ttu-id="ff619-129">Visual Studio 2017 Community、 Professional 或 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="ff619-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="ff619-130">下载代码</span><span class="sxs-lookup"><span data-stu-id="ff619-130">Download code</span></span>

<span data-ttu-id="ff619-131">下载[已完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="ff619-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="ff619-132">可下载项目包含本主题以及单元测试代码[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主题。</span><span class="sxs-lookup"><span data-stu-id="ff619-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="ff619-133">使用单元测试项目创建应用程序</span><span class="sxs-lookup"><span data-stu-id="ff619-133">Create application with unit test project</span></span>

<span data-ttu-id="ff619-134">可以创建单元测试项目，创建你的应用程序时，也可以将单元测试项目添加到现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="ff619-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="ff619-135">本教程演示创建应用程序时创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="ff619-136">创建一个新的 ASP.NET Web 应用程序名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="ff619-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="ff619-137">在新建 ASP.NET 项目窗口中，选择**空**模板和添加文件夹和核心引用有关 Web API。</span><span class="sxs-lookup"><span data-stu-id="ff619-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="ff619-138">选择**添加单元测试**选项。</span><span class="sxs-lookup"><span data-stu-id="ff619-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="ff619-139">单元测试项目将自动命名**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="ff619-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="ff619-140">可以保留此名称。</span><span class="sxs-lookup"><span data-stu-id="ff619-140">You can keep this name.</span></span>

![创建单元测试项目](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="ff619-142">创建程序后，会看到它包含两个项目- **StoreApp**并**StoreApp.Tests**。</span><span class="sxs-lookup"><span data-stu-id="ff619-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="ff619-143">创建模型类</span><span class="sxs-lookup"><span data-stu-id="ff619-143">Create the model class</span></span>

<span data-ttu-id="ff619-144">在 StoreApp 项目中，将添加到一个类文件**模型**名为文件夹**Product.cs**。</span><span class="sxs-lookup"><span data-stu-id="ff619-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="ff619-145">将以下代码替换为该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="ff619-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="ff619-146">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="ff619-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="ff619-147">添加控制器</span><span class="sxs-lookup"><span data-stu-id="ff619-147">Add the controller</span></span>

<span data-ttu-id="ff619-148">右键单击 Controllers 文件夹，然后选择**外**并**新基架项**。</span><span class="sxs-lookup"><span data-stu-id="ff619-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="ff619-149">选择 Web API 2 控制器操作使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="ff619-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![添加新的控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="ff619-151">设置下列值：</span><span class="sxs-lookup"><span data-stu-id="ff619-151">Set the following values:</span></span>

- <span data-ttu-id="ff619-152">控制器名称： **ProductController**</span><span class="sxs-lookup"><span data-stu-id="ff619-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="ff619-153">模型类：**产品**</span><span class="sxs-lookup"><span data-stu-id="ff619-153">Model class: **Product**</span></span>
- <span data-ttu-id="ff619-154">数据上下文类: [选择**新建数据上下文**按钮填充如下所示的值的]</span><span class="sxs-lookup"><span data-stu-id="ff619-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="ff619-156">单击**添加**要创建自动生成的代码使用控制器。</span><span class="sxs-lookup"><span data-stu-id="ff619-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="ff619-157">代码包括用于创建、 检索、 更新和删除产品类的实例方法。</span><span class="sxs-lookup"><span data-stu-id="ff619-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="ff619-158">下面的代码显示了该方法用于将产品。</span><span class="sxs-lookup"><span data-stu-id="ff619-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="ff619-159">请注意，该方法返回的实例**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="ff619-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="ff619-160">IHttpActionResult 是一个 Web API 2 中的新功能，这样可以简化单元测试开发。</span><span class="sxs-lookup"><span data-stu-id="ff619-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="ff619-161">在下一步部分中，您将自定义生成的代码，以便将测试对象传递给控制器。</span><span class="sxs-lookup"><span data-stu-id="ff619-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="ff619-162">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="ff619-162">Add dependency injection</span></span>

<span data-ttu-id="ff619-163">目前，ProductController 类是硬编码为使用 StoreAppContext 类的实例。</span><span class="sxs-lookup"><span data-stu-id="ff619-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="ff619-164">将使用称为依赖关系注入的模式来修改应用程序，并删除该硬编码的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="ff619-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="ff619-165">通过打破这种依赖关系，您可以传入 mock 对象测试时。</span><span class="sxs-lookup"><span data-stu-id="ff619-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="ff619-166">右键单击**模型**文件夹，并添加名为的新界面**IStoreAppContext**。</span><span class="sxs-lookup"><span data-stu-id="ff619-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="ff619-167">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="ff619-168">打开 StoreAppContext.cs 文件并进行以下突出显示的更改。</span><span class="sxs-lookup"><span data-stu-id="ff619-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="ff619-169">需要注意的重要更改是：</span><span class="sxs-lookup"><span data-stu-id="ff619-169">The important changes to note are:</span></span>

- <span data-ttu-id="ff619-170">StoreAppContext 类实现 IStoreAppContext 接口</span><span class="sxs-lookup"><span data-stu-id="ff619-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="ff619-171">实现 MarkAsModified 方法</span><span class="sxs-lookup"><span data-stu-id="ff619-171">MarkAsModified method is implemented</span></span>


[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="ff619-172">打开 ProductController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="ff619-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="ff619-173">更改现有代码，以匹配突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="ff619-174">这些更改在 StoreAppContext 破坏依赖项，并启用要传递给不同对象中的上下文类的其他类。</span><span class="sxs-lookup"><span data-stu-id="ff619-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="ff619-175">此更改将可以在单元测试期间传递测试上下文中。</span><span class="sxs-lookup"><span data-stu-id="ff619-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="ff619-176">没有一个详细的更改必须在 ProductController 中进行。</span><span class="sxs-lookup"><span data-stu-id="ff619-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="ff619-177">在中**PutProduct**方法中，将为实体状态设置为行修改为 MarkAsModified 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="ff619-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="ff619-178">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="ff619-178">Build the solution.</span></span>

<span data-ttu-id="ff619-179">你现已准备好设置测试项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="ff619-180">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ff619-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="ff619-181">当使用空模板创建的应用程序时，单元测试项目 (StoreApp.Tests) 不包括任何已安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ff619-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="ff619-182">其他模板，例如 Web API 模板中，单元测试项目中包括一些 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ff619-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="ff619-183">对于本教程，必须包括实体框架包和 Microsoft ASP.NET Web API 2 核心包到测试项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-183">For this tutorial, you must include the Entity Framework packge and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="ff619-184">右键单击 StoreApp.Tests 项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="ff619-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="ff619-185">必须选择要将包添加到该项目的 StoreApp.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="ff619-187">从联机包中，查找并安装 EntityFramework 包 （版本 6.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="ff619-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="ff619-188">如果它出现 EntityFramework 包已安装，您可能选择 StoreApp 项目而不是 StoreApp.Tests 项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![添加实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="ff619-190">查找和安装 Microsoft ASP.NET Web API 2 核心包。</span><span class="sxs-lookup"><span data-stu-id="ff619-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安装 web api core 包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="ff619-192">关闭管理 NuGet 包窗口。</span><span class="sxs-lookup"><span data-stu-id="ff619-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="ff619-193">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="ff619-193">Create test context</span></span>

<span data-ttu-id="ff619-194">添加名为的类**TestDbSet**到测试项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="ff619-195">此类用作测试数据集类的基类。</span><span class="sxs-lookup"><span data-stu-id="ff619-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="ff619-196">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="ff619-197">添加名为的类**TestProductDbSet**到测试项目中包含以下代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="ff619-198">添加名为的类**TestStoreAppContext**和现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="ff619-199">创建测试</span><span class="sxs-lookup"><span data-stu-id="ff619-199">Create tests</span></span>

<span data-ttu-id="ff619-200">默认情况下，你的测试项目包括一个名为的空测试文件**UnitTest1.cs**。</span><span class="sxs-lookup"><span data-stu-id="ff619-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="ff619-201">此文件显示了用于创建测试方法的属性。</span><span class="sxs-lookup"><span data-stu-id="ff619-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="ff619-202">对于本教程，可以删除此文件，因为您将添加新的测试类。</span><span class="sxs-lookup"><span data-stu-id="ff619-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="ff619-203">添加名为的类**TestProductController**到测试项目。</span><span class="sxs-lookup"><span data-stu-id="ff619-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="ff619-204">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ff619-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="ff619-205">运行测试</span><span class="sxs-lookup"><span data-stu-id="ff619-205">Run tests</span></span>

<span data-ttu-id="ff619-206">现在您就可以运行测试。</span><span class="sxs-lookup"><span data-stu-id="ff619-206">You are now ready to run the tests.</span></span> <span data-ttu-id="ff619-207">使用标记的方法的所有**TestMethod**属性进行测试。</span><span class="sxs-lookup"><span data-stu-id="ff619-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="ff619-208">从**测试**菜单项，运行测试。</span><span class="sxs-lookup"><span data-stu-id="ff619-208">From the **Test** menu item, run the tests.</span></span>

![运行测试](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="ff619-210">打开**测试资源管理器**窗口中，并请注意，测试结果。</span><span class="sxs-lookup"><span data-stu-id="ff619-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![测试结果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
