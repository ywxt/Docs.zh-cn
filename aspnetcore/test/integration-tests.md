---
title: 在 ASP.NET Core 的集成测试
author: guardrex
description: 了解如何集成测试确保应用程序的组件正常在基础结构级别，包括数据库、 文件系统和网络。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/30/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: test/integration-tests
ms.openlocfilehash: a402c3f5f6a75917eba4058e6cc6926f25b214d4
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "35217536"
---
# <a name="integration-tests-in-aspnet-core"></a><span data-ttu-id="aa4d6-103">在 ASP.NET Core 的集成测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-103">Integration tests in ASP.NET Core</span></span>

<span data-ttu-id="aa4d6-104">通过[Luke Latham](https://github.com/guardrex)和[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="aa4d6-104">By [Luke Latham](https://github.com/guardrex) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="aa4d6-105">集成测试确保应用程序的组件正常工作，其中包含应用程序的支持的基础结构，例如数据库、 文件系统和网络级别。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-105">Integration tests ensure that an app's components function correctly at a level that includes the app's supporting infrastructure, such as the database, file system, and network.</span></span> <span data-ttu-id="aa4d6-106">ASP.NET 核心支持测试 web 宿主和内存中测试服务器中使用单元测试框架的集成测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-106">ASP.NET Core supports integration tests using a unit test framework with a test web host and an in-memory test server.</span></span>

<span data-ttu-id="aa4d6-107">本主题假定单元测试的一个基本的了解。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-107">This topic assumes a basic understanding of unit tests.</span></span> <span data-ttu-id="aa4d6-108">如果测试概念不太熟悉，请参阅[在.NET 核心和标准.NET 中的单元测试](/dotnet/core/testing/)主题和其链接的内容。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-108">If unfamiliar with test concepts, see the [Unit Testing in .NET Core and .NET Standard](/dotnet/core/testing/) topic and its linked content.</span></span>

<span data-ttu-id="aa4d6-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="aa4d6-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="aa4d6-110">示例应用程序是 Razor 页应用，并假定 Razor 页的一个基本的了解。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-110">The sample app is a Razor Pages app and assumes a basic understanding of Razor Pages.</span></span> <span data-ttu-id="aa4d6-111">如果熟悉 Razor 页，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-111">If unfamiliar with Razor Pages, see the following topics:</span></span>

* [<span data-ttu-id="aa4d6-112">Razor 页面介绍</span><span class="sxs-lookup"><span data-stu-id="aa4d6-112">Introduction to Razor Pages</span></span>](xref:mvc/razor-pages/index)
* [<span data-ttu-id="aa4d6-113">Razor 页面入门</span><span class="sxs-lookup"><span data-stu-id="aa4d6-113">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="aa4d6-114">Razor 页单元测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-114">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)

## <a name="introduction-to-integration-tests"></a><span data-ttu-id="aa4d6-115">集成测试的简介</span><span class="sxs-lookup"><span data-stu-id="aa4d6-115">Introduction to integration tests</span></span>

<span data-ttu-id="aa4d6-116">集成测试评估比更广泛级别上的应用程序的组件[单元测试](/dotnet/core/testing/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-116">Integration tests evaluate an app's components on a broader level than [unit tests](/dotnet/core/testing/).</span></span> <span data-ttu-id="aa4d6-117">单元测试用于测试独立的软件组件，例如单独的类的方法。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-117">Unit tests are used to test isolated software components, such as individual class methods.</span></span> <span data-ttu-id="aa4d6-118">集成测试可确认，两个或多个应用程序组件配合工作来生成预期的结果，还可能包括完全处理某个请求所需的每个组件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-118">Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.</span></span>

<span data-ttu-id="aa4d6-119">这些更广泛测试用于测试应用程序的基础结构和整个框架，通常包括以下组件：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-119">These broader tests are used to test the app's infrastructure and whole framework, often including the following components:</span></span>

* <span data-ttu-id="aa4d6-120">数据库</span><span class="sxs-lookup"><span data-stu-id="aa4d6-120">Database</span></span>
* <span data-ttu-id="aa4d6-121">文件系统</span><span class="sxs-lookup"><span data-stu-id="aa4d6-121">File system</span></span>
* <span data-ttu-id="aa4d6-122">网络设备</span><span class="sxs-lookup"><span data-stu-id="aa4d6-122">Network appliances</span></span>
* <span data-ttu-id="aa4d6-123">请求-响应管道</span><span class="sxs-lookup"><span data-stu-id="aa4d6-123">Request-response pipeline</span></span>

<span data-ttu-id="aa4d6-124">单元测试使用制造的组件，称为*fakes*或*模拟对象*，替代基础结构组件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-124">Unit tests use fabricated components, known as *fakes* or *mock objects*, in place of infrastructure components.</span></span>

<span data-ttu-id="aa4d6-125">与单元测试集成测试：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-125">In contrast to unit tests, integration tests:</span></span>

* <span data-ttu-id="aa4d6-126">使用应用程序在生产中使用的实际组件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-126">Use the actual components that the app uses in production.</span></span>
* <span data-ttu-id="aa4d6-127">需要更多代码和数据处理。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-127">Require more code and data processing.</span></span>
* <span data-ttu-id="aa4d6-128">需要更长时间才能运行。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-128">Take longer to run.</span></span>

<span data-ttu-id="aa4d6-129">因此，限制到最重要的基础结构方案的集成测试使用。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-129">Therefore, limit the use of integration tests to the most important infrastructure scenarios.</span></span> <span data-ttu-id="aa4d6-130">使用单元测试或集成测试，可以测试行为，如果选择的单元测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-130">If a behavior can be tested using either a unit test or an integration test, choose the unit test.</span></span>

> [!TIP]
> <span data-ttu-id="aa4d6-131">不写入数据库和文件系统使用的数据和文件访问每个可能排列的集成测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-131">Don't write integration tests for every possible permutation of data and file access with databases and file systems.</span></span> <span data-ttu-id="aa4d6-132">而不考虑跨应用程序的多少位与数据库和文件系统、 集中的读取、 写入、 更新和删除集成测试通常能够充分测试数据库和文件系统组件进行交互。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-132">Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components.</span></span> <span data-ttu-id="aa4d6-133">使用单元测试的方法逻辑例程与这些组件进行交互的测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-133">Use unit tests for routine tests of method logic that interact with these components.</span></span> <span data-ttu-id="aa4d6-134">在单位测试中的基础结构使用 fakes/mock 中测试执行速度更快的结果。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-134">In unit tests, the use of infrastructure fakes/mocks result in faster test execution.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4d6-135">在讨论的集成测试，测试的项目经常称为*待测试系统*，或简称"SUT"。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-135">In discussions of integration tests, the tested project is frequently called the *system under test*, or "SUT" for short.</span></span>

## <a name="aspnet-core-integration-tests"></a><span data-ttu-id="aa4d6-136">ASP.NET 核心集成测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-136">ASP.NET Core integration tests</span></span>

<span data-ttu-id="aa4d6-137">集成测试在 ASP.NET 核心中的有以下要求：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-137">Integration tests in ASP.NET Core require the following:</span></span>

* <span data-ttu-id="aa4d6-138">测试项目用于包含并执行测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-138">A test project is used to contain and execute the tests.</span></span> <span data-ttu-id="aa4d6-139">测试项目具有对经过测试的 ASP.NET Core 项目中，调用的引用*待测试系统*(SUT)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-139">The test project has a reference to the tested ASP.NET Core project, called the *system under test* (SUT).</span></span> <span data-ttu-id="aa4d6-140">_在本主题使用"SUT"来指代经过测试的应用程序。_</span><span class="sxs-lookup"><span data-stu-id="aa4d6-140">_"SUT" is used throughout this topic to refer to the tested app._</span></span>
* <span data-ttu-id="aa4d6-141">测试项目创建 SUT 测试 web 主机，并使用测试服务器客户端以处理请求和响应 SUT。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-141">The test project creates a test web host for the SUT and uses a test server client to handle requests and responses to the SUT.</span></span>
* <span data-ttu-id="aa4d6-142">测试运行程序用于执行的测试和报告测试结果。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-142">A test runner is used to execute the tests and report the test results.</span></span>

<span data-ttu-id="aa4d6-143">集成测试遵循事件，其中包括常用序列*排列*， *Act*，和*断言*测试步骤：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-143">Integration tests follow a sequence of events that include the usual *Arrange*, *Act*, and *Assert* test steps:</span></span>

1. <span data-ttu-id="aa4d6-144">SUT 的 web 主机配置。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-144">The SUT's web host is configured.</span></span>
1. <span data-ttu-id="aa4d6-145">测试服务器客户端创建以将请求提交到应用程序。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-145">A test server client is created to submit requests to the app.</span></span>
1. <span data-ttu-id="aa4d6-146">*排列*执行测试步骤： 测试应用程序准备请求。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-146">The *Arrange* test step is executed: The test app prepares a request.</span></span>
1. <span data-ttu-id="aa4d6-147">*Act*执行测试步骤： 客户端提交该请求并接收响应。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-147">The *Act* test step is executed: The client submits the request and receives the response.</span></span>
1. <span data-ttu-id="aa4d6-148">*断言*执行测试步骤：*实际*响应进行验证*传递*或*失败*基于*预期*响应。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-148">The *Assert* test step is executed: The *actual* response is validated as a *pass* or *fail* based on an *expected* response.</span></span>
1. <span data-ttu-id="aa4d6-149">此过程将继续之前执行的所有测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-149">The process continues until all of the tests are executed.</span></span>
1. <span data-ttu-id="aa4d6-150">报告测试结果。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-150">The test results are reported.</span></span>

<span data-ttu-id="aa4d6-151">通常情况下，测试 web 主机配置以不同的方式不是测试应用程序的正常 web 主机都运行。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-151">Usually, the test web host is configured differently than the app's normal web host for the test runs.</span></span> <span data-ttu-id="aa4d6-152">例如，不同的数据库或不同的应用程序设置可用于测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-152">For example, a different database or different app settings might be used for the tests.</span></span>

<span data-ttu-id="aa4d6-153">基础结构组件，例如测试 web 主机和内存中测试服务器 ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver))、 提供或由管理[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)包。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-153">Infrastructure components, such as the test web host and in-memory test server ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)), are provided or managed by the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package.</span></span> <span data-ttu-id="aa4d6-154">测试创建和执行，从而简化了使用此包。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-154">Use of this package streamlines test creation and execution.</span></span>

<span data-ttu-id="aa4d6-155">`Microsoft.AspNetCore.Mvc.Testing`包处理以下任务：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-155">The `Microsoft.AspNetCore.Mvc.Testing` package handles the following tasks:</span></span>

* <span data-ttu-id="aa4d6-156">将复制依赖项文件 (*\*.deps*) 从入测试项目的 SUT *bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-156">Copies the dependencies file (*\*.deps*) from the SUT into the test project's *bin* folder.</span></span>
* <span data-ttu-id="aa4d6-157">请设置为 SUT 的项目根目录内容的根，静态文件和页/视图位于测试执行的时间。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-157">Sets the content root to the SUT's project root so that static files and pages/views are found when the tests are executed.</span></span>
* <span data-ttu-id="aa4d6-158">提供[WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)类来简化引导与 SUT `TestServer`。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-158">Provides the [WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) class to streamline bootstrapping the SUT with `TestServer`.</span></span>

<span data-ttu-id="aa4d6-159">[单元测试](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)文档介绍如何设置的测试项目和测试运行程序，以及如何运行测试和了解建议的名称测试和测试类的详细说明。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-159">The [unit tests](/dotnet/articles/core/testing/unit-testing-with-dotnet-test) documentation describes how to set up a test project and test runner, along with detailed instructions on how to run tests and recommendations for how to name tests and test classes.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4d6-160">在创建应用程序测试项目时，将单元测试集成测试与分开到不同的项目。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-160">When creating a test project for an app, separate the unit tests from the integration tests into different projects.</span></span> <span data-ttu-id="aa4d6-161">这有助于确保测试的基础结构组件不意外包括在单元测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-161">This helps ensure that infrastructure testing components aren't accidently included in the unit tests.</span></span> <span data-ttu-id="aa4d6-162">单元和集成测试的分离还允许控制通过的测试运行。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-162">Separation of unit and integration tests also allows control over which set of tests are run.</span></span>

<span data-ttu-id="aa4d6-163">几乎 Razor 页应用的测试的配置和 MVC 应用程序之间没有差异。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-163">There's virtually no difference between the configuration for tests of Razor Pages apps and MVC apps.</span></span> <span data-ttu-id="aa4d6-164">唯一的区别是在测试的命名方式。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-164">The only difference is in how the tests are named.</span></span> <span data-ttu-id="aa4d6-165">在 Razor 页应用中，测试页终结点通常命名页模型类 (例如，`IndexPageTests`测试索引页的组件集成)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-165">In a Razor Pages app, tests of page endpoints are usually named after the page model class (for example, `IndexPageTests` to test component integration for the Index page).</span></span> <span data-ttu-id="aa4d6-166">在 MVC 应用程序，测试通常组织由控制器类和命名它们所测试的控制器 (例如，`HomeControllerTests`测试 Home 控制器的组件集成)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-166">In an MVC app, tests are usually organized by controller classes and named after the controllers they test (for example, `HomeControllerTests` to test component integration for the Home controller).</span></span>

## <a name="test-app-prerequisites"></a><span data-ttu-id="aa4d6-167">测试应用程序的必备组件</span><span class="sxs-lookup"><span data-stu-id="aa4d6-167">Test app prerequisites</span></span>

<span data-ttu-id="aa4d6-168">测试项目必须：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-168">The test project must:</span></span>

* <span data-ttu-id="aa4d6-169">有关包引用[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-169">Have a package reference for [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/).</span></span>
* <span data-ttu-id="aa4d6-170">在项目文件中使用 Web SDK (`<Project Sdk="Microsoft.NET.Sdk.Web">`)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-170">Use the Web SDK in the project file (`<Project Sdk="Microsoft.NET.Sdk.Web">`).</span></span>

<span data-ttu-id="aa4d6-171">可在中查看这些 prerequesities[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-171">These prerequesities can be seen in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/).</span></span> <span data-ttu-id="aa4d6-172">检查*tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-172">Inspect the *tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj* file.</span></span>

## <a name="basic-tests-with-the-default-webapplicationfactory"></a><span data-ttu-id="aa4d6-173">使用默认 WebApplicationFactory 的基本测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-173">Basic tests with the default WebApplicationFactory</span></span>

<span data-ttu-id="aa4d6-174">[WebApplicationFactory&lt;TEntryPoint&gt; ](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)用于创建[TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)集成测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-174">[WebApplicationFactory&lt;TEntryPoint&gt;](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) is used to create a [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver) for the integration tests.</span></span> <span data-ttu-id="aa4d6-175">`TEntryPoint` 通常是对 sut 的入口点类`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-175">`TEntryPoint` is the entry point class of the SUT, usually the `Startup` class.</span></span>

<span data-ttu-id="aa4d6-176">测试类实现*类配件*接口 (`IClassFixture`) 以指示类包含测试和跨类中的测试提供共享的对象实例。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-176">Test classes implement a *class fixture* interface (`IClassFixture`) to indicate the class contains tests and provide shared object instances across the tests in the class.</span></span>

### <a name="basic-test-of-app-endpoints"></a><span data-ttu-id="aa4d6-177">基本应用程序终结点的测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-177">Basic test of app endpoints</span></span>

<span data-ttu-id="aa4d6-178">以下测试类， `BasicTests`，使用`WebApplicationFactory`引导 SUT 并提供[HttpClient](/dotnet/api/system.net.http.httpclient)到测试方法时， `Get_EndpointsReturnSuccessAndCorrectContentType`。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-178">The following test class, `BasicTests`, uses the `WebApplicationFactory` to bootstrap the SUT and provide an [HttpClient](/dotnet/api/system.net.http.httpclient) to a test method, `Get_EndpointsReturnSuccessAndCorrectContentType`.</span></span> <span data-ttu-id="aa4d6-179">该方法检查是否成功的响应状态代码 （200 299 的范围中的状态代码） 和`Content-Type`标头是`text/html; charset=utf-8`为多个应用程序页面。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-179">The method checks if the response status code is successful (status codes in the range 200-299) and the `Content-Type` header is `text/html; charset=utf-8` for several app pages.</span></span>

<span data-ttu-id="aa4d6-180">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)创建的实例`HttpClient`自动遵循重定向和处理 cookie。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-180">[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) creates an instance of `HttpClient` that automatically follows redirects and handles cookies.</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet1)]

### <a name="test-a-secure-endpoint"></a><span data-ttu-id="aa4d6-181">测试安全的终结点</span><span class="sxs-lookup"><span data-stu-id="aa4d6-181">Test a secure endpoint</span></span>

<span data-ttu-id="aa4d6-182">中的另一个测试`BasicTests`类将检查安全的终结点到应用程序的登录页将未经身份验证的用户重定向。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-182">Another test in the `BasicTests` class checks that a secure endpoint redirects an unauthenticated user to the app's Login page.</span></span>

<span data-ttu-id="aa4d6-183">在 SUT，`/SecurePage`页上使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)约定将[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到页。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-183">In the SUT, the `/SecurePage` page uses an [AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) convention to apply an [AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) to the page.</span></span> <span data-ttu-id="aa4d6-184">有关详细信息，请参阅[Razor 页授权约定](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-184">For more information, see [Razor Pages authorization conventions](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page).</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet1)]

<span data-ttu-id="aa4d6-185">在`Get_SecurePageRequiresAnAuthenticatedUser`测试， [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)设置为禁止重定向设置[AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect)到`false`:</span><span class="sxs-lookup"><span data-stu-id="aa4d6-185">In the `Get_SecurePageRequiresAnAuthenticatedUser` test, a [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) is set to disallow redirects by setting [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) to `false`:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet2)]

<span data-ttu-id="aa4d6-186">通过禁止客户端遵循重定向，可以进行以下检查：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-186">By disallowing the client to follow the redirect, the following checks can be made:</span></span>

* <span data-ttu-id="aa4d6-187">可以检查 SUT 返回的状态代码针对预期[HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode)不重定向到登录页上，将是之后的最终状态代码、 结果[HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span><span class="sxs-lookup"><span data-stu-id="aa4d6-187">The status code returned by the SUT can be checked against the expected [HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode) result, not the final status code after the redirect to the Login page, which would be [HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).</span></span>
* <span data-ttu-id="aa4d6-188">`Location`响应标头中的标头值进行检查以确认它开头`http://localhost/Identity/Account/Login`，不将最终的登录页响应，其中`Location`标头不会存在。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-188">The `Location` header value in the response headers is checked to confirm that it starts with `http://localhost/Identity/Account/Login`, not the final Login page response, where the `Location` header wouldn't be present.</span></span>

<span data-ttu-id="aa4d6-189">有关详细信息`WebApplicationFactoryClientOptions`，请参阅[客户端选项](#client-options)部分。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-189">For more information on `WebApplicationFactoryClientOptions`, see the [Client options](#client-options) section.</span></span>

## <a name="customize-webapplicationfactory"></a><span data-ttu-id="aa4d6-190">自定义 WebApplicationFactory</span><span class="sxs-lookup"><span data-stu-id="aa4d6-190">Customize WebApplicationFactory</span></span>

<span data-ttu-id="aa4d6-191">可以通过从继承独立于测试类创建 web 主机配置`WebApplicationFactory`创建一个或多个自定义工厂：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-191">Web host configuration can be created independently of the test classes by inheriting from `WebApplicationFactory` to create one or more custom factories:</span></span>

1. <span data-ttu-id="aa4d6-192">继承自`WebApplicationFactory`，并重写[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-192">Inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost).</span></span> <span data-ttu-id="aa4d6-193">[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)允许具有的服务集合的配置[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span><span class="sxs-lookup"><span data-stu-id="aa4d6-193">The [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) allows the configuration of the service collection with [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/CustomWebApplicationFactory.cs?name=snippet1)]

   <span data-ttu-id="aa4d6-194">数据库在种子设定[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)由执行`InitializeDbForTests`方法。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-194">Database seeding in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is performed by the `InitializeDbForTests` method.</span></span> <span data-ttu-id="aa4d6-195">该方法所述[集成测试的示例： 测试应用程序组织](#test-app-organization)部分。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-195">The method is described in the [Integration tests sample: Test app organization](#test-app-organization) section.</span></span>

2. <span data-ttu-id="aa4d6-196">使用自定义`CustomWebApplicationFactory`测试类中。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-196">Use the custom `CustomWebApplicationFactory` in test classes.</span></span> <span data-ttu-id="aa4d6-197">下面的示例使用中的工厂`IndexPageTests`类：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-197">The following example uses the factory in the `IndexPageTests` class:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet1)]

   <span data-ttu-id="aa4d6-198">示例应用程序的客户端配置为阻止`HttpClient`从以下重定向。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-198">The sample app's client is configured to prevent the `HttpClient` from following redirects.</span></span> <span data-ttu-id="aa4d6-199">中所述[测试安全的终结点](#test-a-secure-endpoint)部分中，这就允许测试以检查应用程序的第一个响应的结果。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-199">As explained in the [Test a secure endpoint](#test-a-secure-endpoint) section, this permits tests to check the result of the app's first response.</span></span> <span data-ttu-id="aa4d6-200">第一个响应是在很多与这些测试的重定向`Location`标头。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-200">The first response is a redirect in many of these tests with a `Location` header.</span></span>

3. <span data-ttu-id="aa4d6-201">典型测试使用`HttpClient`和帮助器方法来处理请求和响应：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-201">A typical test uses the `HttpClient` and helper methods to process the request and the response:</span></span>

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet2)]

<span data-ttu-id="aa4d6-202">向 SUT 任何 POST 请求必须满足 antiforgery 检查自动是由应用程序的开发[数据保护 antiforgery 系统](xref:security/data-protection/introduction)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-202">Any POST request to the SUT must satisfy the antiforgery check that's automatically made by the app's [data protection antiforgery system](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="aa4d6-203">若要安排某个测试的 POST 请求，测试应用程序必须：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-203">In order to arrange for a test's POST request, the test app must:</span></span>

1. <span data-ttu-id="aa4d6-204">请对页的请求。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-204">Make a request for the page.</span></span>
1. <span data-ttu-id="aa4d6-205">分析 antiforgery cookie 和响应的请求验证令牌。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-205">Parse the antiforgery cookie and request validation token from the response.</span></span>
1. <span data-ttu-id="aa4d6-206">到位，请使用 antiforgery 的 cookie 与请求验证的 POST 请求令牌。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-206">Make the POST request with the antiforgery cookie and request validation token in place.</span></span>

<span data-ttu-id="aa4d6-207">`SendAsync` Helper 扩展方法 (*Helpers/HttpClientExtensions.cs*) 和`GetDocumentAsync`帮助器方法 (*Helpers/HtmlHelpers.cs*) 中[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)使用[AngleSharp](https://anglesharp.github.io/)分析器以使用下列方法处理 antiforgery 检查：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-207">The `SendAsync` helper extension methods (*Helpers/HttpClientExtensions.cs*) and the `GetDocumentAsync` helper method (*Helpers/HtmlHelpers.cs*) in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/) use the [AngleSharp](https://anglesharp.github.io/) parser to handle the antiforgery check with the following methods:</span></span>

* <span data-ttu-id="aa4d6-208">`GetDocumentAsync` &ndash; 接收[HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage)并返回`IHtmlDocument`。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-208">`GetDocumentAsync` &ndash; Receives the [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) and returns an `IHtmlDocument`.</span></span> <span data-ttu-id="aa4d6-209">`GetDocumentAsync` 使用一个工厂，它准备*虚拟响应*基于原始`HttpResponseMessage`。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-209">`GetDocumentAsync` uses a factory that prepares a *virtual response* based on the original `HttpResponseMessage`.</span></span> <span data-ttu-id="aa4d6-210">有关详细信息，请参阅[AngleSharp 文档](https://github.com/AngleSharp/AngleSharp#documentation)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-210">For more information, see the [AngleSharp documentation](https://github.com/AngleSharp/AngleSharp#documentation).</span></span>
* <span data-ttu-id="aa4d6-211">`SendAsync` 扩展方法`HttpClient`撰写[HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage)并调用[SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_)将向 SUT 提交请求。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-211">`SendAsync` extension methods for the `HttpClient` compose an [HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage) and call [SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_) to submit requests to the SUT.</span></span> <span data-ttu-id="aa4d6-212">有关重载`SendAsync`接受 HTML 窗体 (`IHtmlFormElement`) 及以下：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-212">Overloads for `SendAsync` accept the HTML form (`IHtmlFormElement`) and the following:</span></span>
  - <span data-ttu-id="aa4d6-213">提交该窗体按钮 (`IHtmlElement`)</span><span class="sxs-lookup"><span data-stu-id="aa4d6-213">Submit button of the form (`IHtmlElement`)</span></span>
  - <span data-ttu-id="aa4d6-214">窗体值集合 (`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="aa4d6-214">Form values collection (`IEnumerable<KeyValuePair<string, string>>`)</span></span>
  - <span data-ttu-id="aa4d6-215">提交按钮 (`IHtmlElement`) 和窗体值 (`IEnumerable<KeyValuePair<string, string>>`)</span><span class="sxs-lookup"><span data-stu-id="aa4d6-215">Submit button (`IHtmlElement`) and form values (`IEnumerable<KeyValuePair<string, string>>`)</span></span>

> [!NOTE]
> <span data-ttu-id="aa4d6-216">[AngleSharp](https://anglesharp.github.io/)第三方分析用于演示目的，本主题和示例应用程序中的库。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-216">[AngleSharp](https://anglesharp.github.io/) is a third-party parsing library used for demonstration purposes in this topic and the sample app.</span></span> <span data-ttu-id="aa4d6-217">AngleSharp 不受支持或所需的集成测试的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-217">AngleSharp isn't supported or required for integration testing of ASP.NET Core apps.</span></span> <span data-ttu-id="aa4d6-218">其他分析程序可以使用，如[Html 灵活性包 (HAP)](http://html-agility-pack.net/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-218">Other parsers can be used, such as the [Html Agility Pack (HAP)](http://html-agility-pack.net/).</span></span> <span data-ttu-id="aa4d6-219">另一种方法是编写代码来直接处理 antiforgery 系统请求验证令牌和 antiforgery cookie。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-219">Another approach is to write code to handle the antiforgery system's request verification token and antiforgery cookie directly.</span></span>

## <a name="customize-the-client-with-withwebhostbuilder"></a><span data-ttu-id="aa4d6-220">自定义客户端与 WithWebHostBuilder</span><span class="sxs-lookup"><span data-stu-id="aa4d6-220">Customize the client with WithWebHostBuilder</span></span>

<span data-ttu-id="aa4d6-221">在测试方法中，需要其他配置时[WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder)创建一个新`WebApplicationFactory`与[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) ，通过配置进一步自定义。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-221">When additional configuration is required within a test method, [WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder) creates a new `WebApplicationFactory` with an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) that is further customized by configuration.</span></span>

<span data-ttu-id="aa4d6-222">`Post_DeleteMessageHandler_ReturnsRedirectToRoot`测试方法的[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)演示如何使用`WithWebHostBuilder`。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-222">The `Post_DeleteMessageHandler_ReturnsRedirectToRoot` test method of the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) demonstrates the use of `WithWebHostBuilder`.</span></span> <span data-ttu-id="aa4d6-223">此测试执行将记录删除触发窗体提交数据封闭在 SUT 数据库中。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-223">This test performs a record delete in the database by triggering a form submission in the SUT.</span></span>

<span data-ttu-id="aa4d6-224">因为在另一个测试`IndexPageTests`类执行的操作将删除所有数据库中的记录和之前可能会运行`Post_DeleteMessageHandler_ReturnsRedirectToRoot`方法，该数据库设置在此测试方法，以确保记录存在 SUT 若要删除的种子值。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-224">Because another test in the `IndexPageTests` class performs an operation that deletes all of the records in the database and may run before the `Post_DeleteMessageHandler_ReturnsRedirectToRoot` method, the database is seeded in this test method to ensure that a record is present for the SUT to delete.</span></span> <span data-ttu-id="aa4d6-225">选择`deleteBtn1`按钮`messages`窗体中 SUT 模拟 SUT 到请求中：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-225">Selecting the `deleteBtn1` button of the `messages` form in the SUT is simulated in the request to the SUT:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet3)]

## <a name="client-options"></a><span data-ttu-id="aa4d6-226">客户端选项</span><span class="sxs-lookup"><span data-stu-id="aa4d6-226">Client options</span></span>

<span data-ttu-id="aa4d6-227">下表显示的默认[WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)时创建可用`HttpClient`实例。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-227">The following table shows the default [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions) available when creating `HttpClient` instances.</span></span>

| <span data-ttu-id="aa4d6-228">选项</span><span class="sxs-lookup"><span data-stu-id="aa4d6-228">Option</span></span> | <span data-ttu-id="aa4d6-229">描述</span><span class="sxs-lookup"><span data-stu-id="aa4d6-229">Description</span></span> | <span data-ttu-id="aa4d6-230">默认</span><span class="sxs-lookup"><span data-stu-id="aa4d6-230">Default</span></span> |
| ------ | ----------- | ------- |
| [<span data-ttu-id="aa4d6-231">AllowAutoRedirect</span><span class="sxs-lookup"><span data-stu-id="aa4d6-231">AllowAutoRedirect</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) | <span data-ttu-id="aa4d6-232">获取或设置是否`HttpClient`实例应自动遵循重定向响应。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-232">Gets or sets whether or not `HttpClient` instances should automatically follow redirect responses.</span></span> | `true` |
| [<span data-ttu-id="aa4d6-233">BaseAddress</span><span class="sxs-lookup"><span data-stu-id="aa4d6-233">BaseAddress</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.baseaddress) | <span data-ttu-id="aa4d6-234">获取或设置的基址`HttpClient`实例。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-234">Gets or sets the base address of `HttpClient` instances.</span></span> | `http://localhost` |
| [<span data-ttu-id="aa4d6-235">HandleCookies</span><span class="sxs-lookup"><span data-stu-id="aa4d6-235">HandleCookies</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.handlecookies) | <span data-ttu-id="aa4d6-236">获取或设置是否`HttpClient`实例应处理 cookie。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-236">Gets or sets whether `HttpClient` instances should handle cookies.</span></span> | `true` |
| [<span data-ttu-id="aa4d6-237">MaxAutomaticRedirections</span><span class="sxs-lookup"><span data-stu-id="aa4d6-237">MaxAutomaticRedirections</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.maxautomaticredirections) | <span data-ttu-id="aa4d6-238">获取或设置的重定向响应的最大数目`HttpClient`实例应遵循。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-238">Gets or sets the maximum number of redirect responses that `HttpClient` instances should follow.</span></span> | <span data-ttu-id="aa4d6-239">7</span><span class="sxs-lookup"><span data-stu-id="aa4d6-239">7</span></span> |

<span data-ttu-id="aa4d6-240">创建`WebApplicationFactoryClientOptions`类并将其传递到[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)方法 （默认值代码示例所示）：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-240">Create the `WebApplicationFactoryClientOptions` class and pass it to the [CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient) method (default values are shown in the code example):</span></span>

```csharp
// Default client option values are shown
var clientOptions = new WebApplicationFactoryClientOptions();
clientOptions.AllowAutoRedirect = true;
clientOptions.BaseAddress = new Uri("http://localhost");
clientOptions.HandleCookies = true;
clientOptions.MaxAutomaticRedirections = 7;

_client = _factory.CreateClient(clientOptions);
```

## <a name="how-the-test-infrastructure-infers-the-app-content-root-path"></a><span data-ttu-id="aa4d6-241">如何测试基础结构推断的应用程序内容的根路径</span><span class="sxs-lookup"><span data-stu-id="aa4d6-241">How the test infrastructure infers the app content root path</span></span>

<span data-ttu-id="aa4d6-242">`WebApplicationFactory`构造函数通过搜索推断的应用程序内容的根路径[WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute)包含具有键等于集成测试的程序集上`TEntryPoint`程序集`System.Reflection.Assembly.FullName`.</span><span class="sxs-lookup"><span data-stu-id="aa4d6-242">The `WebApplicationFactory` constructor infers the app content root path by searching for a [WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute) on the assembly containing the integration tests with a key equal to the `TEntryPoint` assembly `System.Reflection.Assembly.FullName`.</span></span> <span data-ttu-id="aa4d6-243">如果找不到具有正确的注册表项的属性，`WebApplicationFactory`回退到搜索解决方案文件 (*\*.sln*)，并追加`TEntryPoint`到解决方案目录的程序集名称。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-243">In case an attribute with the correct key isn't found, `WebApplicationFactory` falls back to searching for a solution file (*\*.sln*) and appends the `TEntryPoint` assembly name to the solution directory.</span></span> <span data-ttu-id="aa4d6-244">（内容的根路径） 的应用程序根目录用于发现视图和内容文件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-244">The app root directory (the content root path) is used to discover views and content files.</span></span>

<span data-ttu-id="aa4d6-245">在大多数情况下，无需显式设置的应用程序内容根目录位置，如搜索逻辑通常在运行时查找正确的内容根。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-245">In most cases, it isn't necessary to explicitly set the app content root, as the search logic usually finds the correct content root at runtime.</span></span> <span data-ttu-id="aa4d6-246">在未找到的内容的根的特殊情况下使用内置的搜索算法，应用程序内容显式或通过使用自定义逻辑，可以指定根。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-246">In special scenarios where the content root isn't found using the built-in search algorithm, the app content root can be specified explicitly or by using custom logic.</span></span> <span data-ttu-id="aa4d6-247">若要将应用程序内容根目录设置在这些情况下，调用`UseSolutionRelativeContentRoot`扩展方法从[Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost)包。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-247">To set the app content root in those scenarios, call the `UseSolutionRelativeContentRoot` extension method from the [Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost) package.</span></span> <span data-ttu-id="aa4d6-248">提供解决方案的相对路径和可选的解决方案文件的名称或 glob 模式 (默认 = `*.sln`)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-248">Supply the solution's relative path and optional solution file name or glob pattern (default = `*.sln`).</span></span>

<span data-ttu-id="aa4d6-249">调用[UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot)扩展方法使用*一个*下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-249">Call the [UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot) extension method using *ONE* of the following approaches:</span></span>

* <span data-ttu-id="aa4d6-250">配置使用的测试类时`WebApplicationFactory`，提供的自定义配置[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span><span class="sxs-lookup"><span data-stu-id="aa4d6-250">When configuring test classes with `WebApplicationFactory`, provide a custom configuration with the [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):</span></span>

   ```csharp
   public IndexPageTests(
       WebApplicationFactory<RazorPagesProject.Startup> factory)
   {
       var _factory = factory.WithWebHostBuilder(builder =>
       {
           builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

           ...
       });
   }
   ```

* <span data-ttu-id="aa4d6-251">使用自定义配置的测试类时`WebApplicationFactory`，继承自`WebApplicationFactory`，并重写[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span><span class="sxs-lookup"><span data-stu-id="aa4d6-251">When configuring test classes with a custom `WebApplicationFactory`, inherit from `WebApplicationFactory` and override [ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):</span></span>

   ```csharp
   public class CustomWebApplicationFactory<TStartup>
       : WebApplicationFactory<RazorPagesProject.Startup>
   {
       protected override void ConfigureWebHost(IWebHostBuilder builder)
       {
           builder.ConfigureServices(services =>
           {
               builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

               ...
           });
       }
   }
   ```

## <a name="disable-shadow-copying"></a><span data-ttu-id="aa4d6-252">禁用卷影复制</span><span class="sxs-lookup"><span data-stu-id="aa4d6-252">Disable shadow copying</span></span>

<span data-ttu-id="aa4d6-253">卷影复制会导致要在不同的文件夹的输出文件夹中执行的测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-253">Shadow copying causes the tests to execute in a different folder than the output folder.</span></span> <span data-ttu-id="aa4d6-254">对于测试正常工作，卷影复制必须禁用。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-254">For tests to work properly, shadow copying must be disabled.</span></span> <span data-ttu-id="aa4d6-255">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)使用 xUnit，同时禁用卷影复制 xUnit 通过包括*xunit.runner.json*具有正确的配置设置文件。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-255">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) uses xUnit and disables shadow copying for xUnit by including an *xunit.runner.json* file with the correct configuration setting.</span></span> <span data-ttu-id="aa4d6-256">有关详细信息，请参阅[使用 JSON 配置 xUnit.net](https://xunit.github.io/docs/configuring-with-json.html)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-256">For more information, see [Configuring xUnit.net with JSON](https://xunit.github.io/docs/configuring-with-json.html).</span></span>

<span data-ttu-id="aa4d6-257">添加*xunit.runner.json*到具有以下内容的测试项目的根目录的文件：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-257">Add the *xunit.runner.json* file to root of the test project with the following content:</span></span>

```json
{
  "shadowCopy": false
}
```

## <a name="integration-tests-sample"></a><span data-ttu-id="aa4d6-258">集成测试示例</span><span class="sxs-lookup"><span data-stu-id="aa4d6-258">Integration tests sample</span></span>

<span data-ttu-id="aa4d6-259">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)由两个应用程序组成：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-259">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples) is composed of two apps:</span></span>

| <span data-ttu-id="aa4d6-260">应用</span><span class="sxs-lookup"><span data-stu-id="aa4d6-260">App</span></span> | <span data-ttu-id="aa4d6-261">项目文件夹</span><span class="sxs-lookup"><span data-stu-id="aa4d6-261">Project folder</span></span> | <span data-ttu-id="aa4d6-262">描述</span><span class="sxs-lookup"><span data-stu-id="aa4d6-262">Description</span></span> |
| --- | -------------- | ----------- |
| <span data-ttu-id="aa4d6-263">消息应用程序 (SUT)</span><span class="sxs-lookup"><span data-stu-id="aa4d6-263">Message app (the SUT)</span></span> | <span data-ttu-id="aa4d6-264">*src/RazorPagesProject*</span><span class="sxs-lookup"><span data-stu-id="aa4d6-264">*src/RazorPagesProject*</span></span> | <span data-ttu-id="aa4d6-265">允许用户添加、 删除其中一个，删除所有，和分析消息。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-265">Allows a user to add, delete one, delete all, and analyze messages.</span></span> |
| <span data-ttu-id="aa4d6-266">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="aa4d6-266">Test app</span></span> | <span data-ttu-id="aa4d6-267">*tests/RazorPagesProject.Tests*</span><span class="sxs-lookup"><span data-stu-id="aa4d6-267">*tests/RazorPagesProject.Tests*</span></span> | <span data-ttu-id="aa4d6-268">用于集成测试 SUT。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-268">Used to integration test the SUT.</span></span> |

<span data-ttu-id="aa4d6-269">可以使用一个 IDE 的内置测试功能，如运行测试[Visual Studio](https://www.visualstudio.com/vs/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-269">The tests can be run using the built-in test features of an IDE, such as [Visual Studio](https://www.visualstudio.com/vs/).</span></span> <span data-ttu-id="aa4d6-270">如果使用[Visual Studio Code](https://code.visualstudio.com/)或命令行中，执行以下命令在命令提示符中*tests/RazorPagesProject.Tests*文件夹：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-270">If using [Visual Studio Code](https://code.visualstudio.com/) or the command line, execute the following command at a command prompt in the *tests/RazorPagesProject.Tests* folder:</span></span>

```console
dotnet test
```

### <a name="message-app-sut-organization"></a><span data-ttu-id="aa4d6-271">消息应用程序 (SUT) 组织</span><span class="sxs-lookup"><span data-stu-id="aa4d6-271">Message app (SUT) organization</span></span>

<span data-ttu-id="aa4d6-272">SUT 是 Razor 页消息系统具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-272">The SUT is a Razor Pages message system with the following characteristics:</span></span>

* <span data-ttu-id="aa4d6-273">应用程序的索引页 (*Pages/Index.cshtml*和*Pages/Index.cshtml.cs*) 提供一个用户界面和网页模型方法，用于控制添加、 删除和分析消息 （每个消息的平均词）.</span><span class="sxs-lookup"><span data-stu-id="aa4d6-273">The Index page of the app (*Pages/Index.cshtml* and *Pages/Index.cshtml.cs*) provides a UI and page model methods to control the addition, deletion, and analysis of messages (average words per message).</span></span>
* <span data-ttu-id="aa4d6-274">一条消息都由描述`Message`类 (*Data/Message.cs*) 具有两个属性： `Id` （密钥） 和`Text`（消息）。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-274">A message is described by the `Message` class (*Data/Message.cs*) with two properties: `Id` (key) and `Text` (message).</span></span> <span data-ttu-id="aa4d6-275">`Text`属性是必需的限制为 200 个字符。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-275">The `Text` property is required and limited to 200 characters.</span></span>
* <span data-ttu-id="aa4d6-276">消息存储使用[实体框架的内存中数据库](/ef/core/providers/in-memory/)&#8224;。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-276">Messages are stored using [Entity Framework's in-memory database](/ef/core/providers/in-memory/)&#8224;.</span></span>
* <span data-ttu-id="aa4d6-277">此应用程序包含在其数据库上下文类中，数据访问层 (DAL) `AppDbContext` (*Data/AppDbContext.cs*)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-277">The app contains a data access layer (DAL) in its database context class, `AppDbContext` (*Data/AppDbContext.cs*).</span></span>
* <span data-ttu-id="aa4d6-278">如果数据库为空应用程序启动时，消息存储区初始化与三条消息。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-278">If the database is empty on app startup, the message store is initialized with three messages.</span></span>
* <span data-ttu-id="aa4d6-279">应用程序包括`/SecurePage`仅可由已经过身份验证的用户访问。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-279">The app includes a `/SecurePage` that can only be accessed by an authenticated user.</span></span>

<span data-ttu-id="aa4d6-280">&#8224;EF 主题，[测试以及 InMemory](/ef/core/miscellaneous/testing/in-memory)，说明如何使用内存中数据库来使用 MSTest 测试。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-280">&#8224;The EF topic, [Test with InMemory](/ef/core/miscellaneous/testing/in-memory), explains how to use an in-memory database for tests with MSTest.</span></span> <span data-ttu-id="aa4d6-281">本主题使用[xUnit](https://xunit.github.io/)测试框架。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-281">This topic uses the [xUnit](https://xunit.github.io/) test framework.</span></span> <span data-ttu-id="aa4d6-282">测试概念和测试跨不同的测试框架的实现是类似，但不是完全相同。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-282">Test concepts and test implementations across different test frameworks are similar but not identical.</span></span>

<span data-ttu-id="aa4d6-283">尽管应用程序不使用[存储库模式](http://martinfowler.com/eaaCatalog/repository.html)并不是有效的示例[工作单元 (UoW) 模式](https://martinfowler.com/eaaCatalog/unitOfWork.html)，Razor 页中支持的开发模式。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-283">Although the app doesn't use the [repository pattern](http://martinfowler.com/eaaCatalog/repository.html) and isn't an effective example of the [Unit of Work (UoW) pattern](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor Pages supports these patterns of development.</span></span> <span data-ttu-id="aa4d6-284">有关详细信息，请参阅[设计基础结构持久性层](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design)，[在 ASP.NET MVC 应用程序中实现的存储库和单元的工作模式](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)，和[测试控制器逻辑](/aspnet/core/mvc/controllers/testing)（此示例实现的存储库模式）。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-284">For more information, see [Designing the infrastructure persistence layer](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), and [Test controller logic](/aspnet/core/mvc/controllers/testing) (the sample implements the repository pattern).</span></span>

### <a name="test-app-organization"></a><span data-ttu-id="aa4d6-285">测试应用程序的组织</span><span class="sxs-lookup"><span data-stu-id="aa4d6-285">Test app organization</span></span>

<span data-ttu-id="aa4d6-286">测试应用程序是在一个控制台应用*tests/RazorPagesProject.Tests*文件夹。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-286">The test app is a console app inside the *tests/RazorPagesProject.Tests* folder.</span></span>

| <span data-ttu-id="aa4d6-287">测试应用程序文件夹</span><span class="sxs-lookup"><span data-stu-id="aa4d6-287">Test app folder</span></span> | <span data-ttu-id="aa4d6-288">描述</span><span class="sxs-lookup"><span data-stu-id="aa4d6-288">Description</span></span> |
| --------------- | ----------- |
| <span data-ttu-id="aa4d6-289">*BasicTests*</span><span class="sxs-lookup"><span data-stu-id="aa4d6-289">*BasicTests*</span></span> | <span data-ttu-id="aa4d6-290">*BasicTests.cs*包含路由、 访问未经身份验证的用户，通过安全页面和获取 GitHub 用户配置文件和检查配置文件的用户登录名的测试方法。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-290">*BasicTests.cs* contains test methods for routing, accessing a secure page by an unauthenticated user, and obtaining a GitHub user profile and checking the profile's user login.</span></span> |
| <span data-ttu-id="aa4d6-291">*IntegrationTests*</span><span class="sxs-lookup"><span data-stu-id="aa4d6-291">*IntegrationTests*</span></span> | <span data-ttu-id="aa4d6-292">*IndexPageTests.cs*包含使用自定义索引页的集成测试`WebApplicationFactory`类。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-292">*IndexPageTests.cs* contains the integration tests for the Index page using custom `WebApplicationFactory` class.</span></span> |
| <span data-ttu-id="aa4d6-293">*帮助器/实用程序*</span><span class="sxs-lookup"><span data-stu-id="aa4d6-293">*Helpers/Utilities*</span></span> | <ul><li><span data-ttu-id="aa4d6-294">*Utilities.cs*包含`InitializeDbForTests`方法用于设定使用测试数据的数据库的种子。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-294">*Utilities.cs* contains the `InitializeDbForTests` method used to seed the database with test data.</span></span></li><li><span data-ttu-id="aa4d6-295">*HtmlHelpers.cs*一种方法可以返回 AngleSharp`IHtmlDocument`以供测试方法。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-295">*HtmlHelpers.cs* provides a method to return an AngleSharp `IHtmlDocument` for use by the test methods.</span></span></li><li><span data-ttu-id="aa4d6-296">*HttpClientExtensions.cs*提供的重载`SendAsync`将向 SUT 提交请求。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-296">*HttpClientExtensions.cs* provide overloads for `SendAsync` to submit requests to the SUT.</span></span></li></ul> |

<span data-ttu-id="aa4d6-297">测试框架为[xUnit](https://xunit.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-297">The test framework is [xUnit](https://xunit.github.io/).</span></span> <span data-ttu-id="aa4d6-298">集成测试使用执行[Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost)，其中包括[TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-298">Integration tests are conducted using the [Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost), which includes the [TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver).</span></span> <span data-ttu-id="aa4d6-299">因为[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)包用来配置测试主机和测试服务器，`TestHost`和`TestServer`包不需要测试应用的项目文件中直接包引用或测试应用程序中的开发人员配置。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-299">Because the [Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing) package is used to configure the test host and test server, the `TestHost` and `TestServer` packages don't require direct package references in the test app's project file or developer configuration in the test app.</span></span>

<span data-ttu-id="aa4d6-300">**用于测试数据库进行种子设定**</span><span class="sxs-lookup"><span data-stu-id="aa4d6-300">**Seeding the database for testing**</span></span>

<span data-ttu-id="aa4d6-301">集成测试通常需要在测试执行之前的数据库中的小型数据集。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-301">Integration tests usually require a small dataset in the database prior to the test execution.</span></span> <span data-ttu-id="aa4d6-302">例如，删除测试数据库记录删除的调用，因此数据库必须具有至少一个记录删除请求才能成功。</span><span class="sxs-lookup"><span data-stu-id="aa4d6-302">For example, a delete test calls for a database record deletion, so the database must have at least one record for the delete request to succeed.</span></span>

<span data-ttu-id="aa4d6-303">示例应用程序设定种子的数据库中的三个消息*Utilities.cs*时它们将执行测试，可以使用：</span><span class="sxs-lookup"><span data-stu-id="aa4d6-303">The sample app seeds the database with three messages in *Utilities.cs* that tests can use when they execute:</span></span>

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/Helpers/Utilities.cs?name=snippet1)]

## <a name="additional-resources"></a><span data-ttu-id="aa4d6-304">其他资源</span><span class="sxs-lookup"><span data-stu-id="aa4d6-304">Additional resources</span></span>

* [<span data-ttu-id="aa4d6-305">单元测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-305">Unit tests</span></span>](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [<span data-ttu-id="aa4d6-306">Razor 页单元测试</span><span class="sxs-lookup"><span data-stu-id="aa4d6-306">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)
* [<span data-ttu-id="aa4d6-307">中间件</span><span class="sxs-lookup"><span data-stu-id="aa4d6-307">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="aa4d6-308">测试控制器</span><span class="sxs-lookup"><span data-stu-id="aa4d6-308">Test controllers</span></span>](xref:mvc/controllers/testing)
