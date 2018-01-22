---
title: "使用 dotnet watch 开发 ASP.NET Core 应用"
author: rick-anderson
description: "本教程演示如何在 ASP.NET Core 应用程序中安装和使用 .NET Core CLI 的文件观察程序 (dotnet watch) 工具。"
ms.author: riande
manager: wpickett
ms.date: 10/05/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/dotnet-watch
ms.openlocfilehash: cadd4a6a78c29e2213c39a02729b5c32a2b93ebd
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="developing-aspnet-core-apps-using-dotnet-watch"></a><span data-ttu-id="591f4-103">使用 dotnet watch 开发 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="591f4-103">Developing ASP.NET Core apps using dotnet watch</span></span>

<span data-ttu-id="591f4-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Victor Hurdugaci](https://twitter.com/victorhurdugaci)</span><span class="sxs-lookup"><span data-stu-id="591f4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Victor Hurdugaci](https://twitter.com/victorhurdugaci)</span></span>

<span data-ttu-id="591f4-105">`dotnet watch` 是一种在源文件更改时运行 [.NET Core CLI](/dotnet/core/tools) 命令的工具。</span><span class="sxs-lookup"><span data-stu-id="591f4-105">`dotnet watch` is a tool that runs a [.NET Core CLI](/dotnet/core/tools) command when source files change.</span></span> <span data-ttu-id="591f4-106">例如，文件更改可能触发编译、测试执行或部署。</span><span class="sxs-lookup"><span data-stu-id="591f4-106">For example, a file change can trigger compilation, test execution, or deployment.</span></span>

<span data-ttu-id="591f4-107">本教程中使用现有 Web API 应用，它具有两个终结点：分别返回总计和产品。</span><span class="sxs-lookup"><span data-stu-id="591f4-107">In this tutorial, we use an existing Web API app with two endpoints: one that returns a sum and one that returns a product.</span></span> <span data-ttu-id="591f4-108">产品方法中有一个 bug，我们将在本教程中修复它。</span><span class="sxs-lookup"><span data-stu-id="591f4-108">The product method contains a bug that we'll fix as part of this tutorial.</span></span>

<span data-ttu-id="591f4-109">下载[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample)。</span><span class="sxs-lookup"><span data-stu-id="591f4-109">Download the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample).</span></span> <span data-ttu-id="591f4-110">它包含两个项目：WebApp（一种 ASP.NET Core Web API）和 WebAppTests（Web API 的单元测试）。</span><span class="sxs-lookup"><span data-stu-id="591f4-110">It contains two projects: *WebApp* (an ASP.NET Core Web API) and *WebAppTests* (unit tests for the Web API).</span></span>

<span data-ttu-id="591f4-111">在命令外壳中，导航到“WebApp”文件夹并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="591f4-111">In a command shell, navigate to the *WebApp* folder and run the following command:</span></span>

```console
dotnet run
```

<span data-ttu-id="591f4-112">控制台输出会显示如下类似的消息（表示应用正在运行且正在等待请求）：</span><span class="sxs-lookup"><span data-stu-id="591f4-112">The console output shows messages similar to the following (indicating that the app is running and awaiting requests):</span></span>

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="591f4-113">在 Web 浏览器中，导航到 `http://localhost:<port number>/api/math/sum?a=4&b=5`。</span><span class="sxs-lookup"><span data-stu-id="591f4-113">In a web browser, navigate to `http://localhost:<port number>/api/math/sum?a=4&b=5`.</span></span> <span data-ttu-id="591f4-114">应该会显示结果 `9`。</span><span class="sxs-lookup"><span data-stu-id="591f4-114">You should see the result of `9`.</span></span>

<span data-ttu-id="591f4-115">导航到产品 API (`http://localhost:<port number>/api/math/product?a=4&b=5`)。</span><span class="sxs-lookup"><span data-stu-id="591f4-115">Navigate to the product API (`http://localhost:<port number>/api/math/product?a=4&b=5`).</span></span> <span data-ttu-id="591f4-116">它会返回 `9`，而不是所预期的 `20`。</span><span class="sxs-lookup"><span data-stu-id="591f4-116">It returns `9`, not `20` as you'd expect.</span></span> <span data-ttu-id="591f4-117">本教程稍后将对其进行修复。</span><span class="sxs-lookup"><span data-stu-id="591f4-117">We'll fix that later in the tutorial.</span></span>

## <a name="add-dotnet-watch-to-a-project"></a><span data-ttu-id="591f4-118">将 `dotnet watch` 添加到项目</span><span class="sxs-lookup"><span data-stu-id="591f4-118">Add `dotnet watch` to a project</span></span>

1. <span data-ttu-id="591f4-119">将 `Microsoft.DotNet.Watcher.Tools` 包引用添加到 .csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="591f4-119">Add a `Microsoft.DotNet.Watcher.Tools` package reference to the *.csproj* file:</span></span>

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup> 
    ```

1. <span data-ttu-id="591f4-120">运行以下命令，安装 `Microsoft.DotNet.Watcher.Tools` 包：</span><span class="sxs-lookup"><span data-stu-id="591f4-120">Install the `Microsoft.DotNet.Watcher.Tools` package by running the following command:</span></span>
    
    ```console
    dotnet restore
    ```

## <a name="running-net-core-cli-commands-using-dotnet-watch"></a><span data-ttu-id="591f4-121">使用 `dotnet watch` 运行 .NET Core CLI 命令</span><span class="sxs-lookup"><span data-stu-id="591f4-121">Running .NET Core CLI commands using `dotnet watch`</span></span>

<span data-ttu-id="591f4-122">`dotnet watch` 可用于运行任何 [.NET Core CLI 命令](/dotnet/core/tools#cli-commands)</span><span class="sxs-lookup"><span data-stu-id="591f4-122">Any [.NET Core CLI command](/dotnet/core/tools#cli-commands) can be run with `dotnet watch`.</span></span> <span data-ttu-id="591f4-123">例如:</span><span class="sxs-lookup"><span data-stu-id="591f4-123">For example:</span></span>

| <span data-ttu-id="591f4-124">命令</span><span class="sxs-lookup"><span data-stu-id="591f4-124">Command</span></span> | <span data-ttu-id="591f4-125">带 watch 的命令</span><span class="sxs-lookup"><span data-stu-id="591f4-125">Command with watch</span></span> |
| ---- | ----- |
| <span data-ttu-id="591f4-126">dotnet 运行</span><span class="sxs-lookup"><span data-stu-id="591f4-126">dotnet run</span></span> | <span data-ttu-id="591f4-127">dotnet watch run</span><span class="sxs-lookup"><span data-stu-id="591f4-127">dotnet watch run</span></span> |
| <span data-ttu-id="591f4-128">dotnet run -f netcoreapp2.0</span><span class="sxs-lookup"><span data-stu-id="591f4-128">dotnet run -f netcoreapp2.0</span></span> | <span data-ttu-id="591f4-129">dotnet watch run -f netcoreapp2.0</span><span class="sxs-lookup"><span data-stu-id="591f4-129">dotnet watch run -f netcoreapp2.0</span></span> |
| <span data-ttu-id="591f4-130">dotnet run -f netcoreapp2.0 -- --arg1</span><span class="sxs-lookup"><span data-stu-id="591f4-130">dotnet run -f netcoreapp2.0 -- --arg1</span></span> | <span data-ttu-id="591f4-131">dotnet watch run -f netcoreapp2.0 -- --arg1</span><span class="sxs-lookup"><span data-stu-id="591f4-131">dotnet watch run -f netcoreapp2.0 -- --arg1</span></span> |
| <span data-ttu-id="591f4-132">dotnet test</span><span class="sxs-lookup"><span data-stu-id="591f4-132">dotnet test</span></span> | <span data-ttu-id="591f4-133">dotnet watch test</span><span class="sxs-lookup"><span data-stu-id="591f4-133">dotnet watch test</span></span> |

<span data-ttu-id="591f4-134">运行“WebApp”文件夹中的 `dotnet watch run`。</span><span class="sxs-lookup"><span data-stu-id="591f4-134">Run `dotnet watch run` in the *WebApp* folder.</span></span> <span data-ttu-id="591f4-135">控制台输出指示 `watch` 已启动。</span><span class="sxs-lookup"><span data-stu-id="591f4-135">The console output indicates `watch` has started.</span></span>

## <a name="making-changes-with-dotnet-watch"></a><span data-ttu-id="591f4-136">通过 `dotnet watch` 进行更改</span><span class="sxs-lookup"><span data-stu-id="591f4-136">Making changes with `dotnet watch`</span></span>

<span data-ttu-id="591f4-137">确保 `dotnet watch` 正在运行。</span><span class="sxs-lookup"><span data-stu-id="591f4-137">Make sure `dotnet watch` is running.</span></span>

<span data-ttu-id="591f4-138">修复 MathController 的 `Product` 方法中的 bug，使其返回产品而非总和。</span><span class="sxs-lookup"><span data-stu-id="591f4-138">Fix the bug in the `Product` method of *MathController.cs* so it returns the product and not the sum:</span></span>

```csharp
public static int Product(int a, int b)
{
  return a * b;
} 
```

<span data-ttu-id="591f4-139">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="591f4-139">Save the file.</span></span> <span data-ttu-id="591f4-140">控制台输出指示 `dotnet watch` 已检测到文件更改并已重启应用。</span><span class="sxs-lookup"><span data-stu-id="591f4-140">The console output indicates that `dotnet watch` detected a file change and restarted the app.</span></span>

<span data-ttu-id="591f4-141">验证 `http://localhost:<port number>/api/math/product?a=4&b=5` 是否返回正确结果。</span><span class="sxs-lookup"><span data-stu-id="591f4-141">Verify `http://localhost:<port number>/api/math/product?a=4&b=5` returns the correct result.</span></span>

## <a name="running-tests-using-dotnet-watch"></a><span data-ttu-id="591f4-142">使用 `dotnet watch` 运行测试</span><span class="sxs-lookup"><span data-stu-id="591f4-142">Running tests using `dotnet watch`</span></span>

1. <span data-ttu-id="591f4-143">将 MathController.cs 的 `Product` 方法改回返回总和并保存文件。</span><span class="sxs-lookup"><span data-stu-id="591f4-143">Change the `Product` method of *MathController.cs* back to returning the sum and save the file.</span></span>
1. <span data-ttu-id="591f4-144">在命令外壳中，导航到“WebAppTests”文件夹。</span><span class="sxs-lookup"><span data-stu-id="591f4-144">In a command shell, navigate to the *WebAppTests* folder.</span></span>
1. <span data-ttu-id="591f4-145">运行 `dotnet restore`。</span><span class="sxs-lookup"><span data-stu-id="591f4-145">Run `dotnet restore`.</span></span>
1. <span data-ttu-id="591f4-146">运行 `dotnet watch test`。</span><span class="sxs-lookup"><span data-stu-id="591f4-146">Run `dotnet watch test`.</span></span> <span data-ttu-id="591f4-147">其输出指示测试失败且观察程序正在等待文件更改：</span><span class="sxs-lookup"><span data-stu-id="591f4-147">Its output indicates that a test failed and that watcher is awaiting file changes:</span></span>

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. <span data-ttu-id="591f4-148">修复 `Product` 方法代码，使其返回产品。</span><span class="sxs-lookup"><span data-stu-id="591f4-148">Fix the `Product` method code so it returns the product.</span></span> <span data-ttu-id="591f4-149">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="591f4-149">Save the file.</span></span>

<span data-ttu-id="591f4-150">`dotnet watch` 检测到文件更改并重新运行测试。</span><span class="sxs-lookup"><span data-stu-id="591f4-150">`dotnet watch` detects the file change and reruns the tests.</span></span> <span data-ttu-id="591f4-151">控制台输出指示测试通过。</span><span class="sxs-lookup"><span data-stu-id="591f4-151">The console output indicates the tests passed.</span></span>

## <a name="dotnet-watch-in-github"></a><span data-ttu-id="591f4-152">GitHub 中的 dotnet-watch</span><span class="sxs-lookup"><span data-stu-id="591f4-152">dotnet-watch in GitHub</span></span>

<span data-ttu-id="591f4-153">dotnet-watch 是 GitHub [DotNetTools 存储库](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch)的一部分。</span><span class="sxs-lookup"><span data-stu-id="591f4-153">dotnet-watch is part of the GitHub [DotNetTools repository](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch).</span></span>

<span data-ttu-id="591f4-154">[dotnet-watch 自述文件](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md)的 [MSBuild 部分](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch#msbuild)阐释了如何通过被监视的 MSBuild 项目文件配置 dotnet-watch。</span><span class="sxs-lookup"><span data-stu-id="591f4-154">The [MSBuild section](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch#msbuild) of the [dotnet-watch ReadMe](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md) explains how dotnet-watch can be configured from the MSBuild project file being watched.</span></span> <span data-ttu-id="591f4-155">[dotnet-watch 自述文件](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md)介绍了本教程中没有的 dotnet-watch 相关信息。</span><span class="sxs-lookup"><span data-stu-id="591f4-155">The [dotnet-watch ReadMe](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md) contains information on dotnet-watch not covered in this tutorial.</span></span>
