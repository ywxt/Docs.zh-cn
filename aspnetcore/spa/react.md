---
title: "使用响应项目模板"
author: SteveSandersonMS
description: "了解如何开始使用 ASP.NET 核心单页面应用程序 (SPA) 发布候选项目模板用于响应和创建响应应用程序。"
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react
ms.openlocfilehash: aa70a35ad938fff6911367ee9d12aac9d575be7e
ms.sourcegitcommit: efc9e5b5fffa0e13957131a0da52cc1532a87651
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="use-the-react-project-template-release-candidate"></a><span data-ttu-id="5a61c-103">使用响应项目模板 （候选发布版）</span><span class="sxs-lookup"><span data-stu-id="5a61c-103">Use the React project template (release candidate)</span></span>

> [!NOTE]
> <span data-ttu-id="5a61c-104">本文档不是有关发布的响应项目模板。</span><span class="sxs-lookup"><span data-stu-id="5a61c-104">This documentation is not about the released React project template.</span></span> <span data-ttu-id="5a61c-105">**此文档是有关响应模板的候选发布版本。**</span><span class="sxs-lookup"><span data-stu-id="5a61c-105">**This documentation is about the release candidate of the React template.**</span></span> <span data-ttu-id="5a61c-106">我们希望在早期 2018年提供已发布的版本。</span><span class="sxs-lookup"><span data-stu-id="5a61c-106">We hope to ship the released version in early 2018.</span></span>

<span data-ttu-id="5a61c-107">已更新的响应项目模板提供了方便起点 ASP.NET Core 应用使用响应和[创建响应应用](https://github.com/facebookincubator/create-react-app)(CRA) 约定，可以实现的丰富的客户端用户界面 (UI)。</span><span class="sxs-lookup"><span data-stu-id="5a61c-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="5a61c-108">该模板是等效于创建充当 API 的后端，将 ASP.NET Core 项目和标准 CRA 做出反应项目操作作为 UI 中，但承载在能够生成和发布作为一个单元的单个应用程序项目中的便利。</span><span class="sxs-lookup"><span data-stu-id="5a61c-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="5a61c-109">创建新的应用程序</span><span class="sxs-lookup"><span data-stu-id="5a61c-109">Create a new app</span></span>

<span data-ttu-id="5a61c-110">若要开始，请确保你已[安装更新的响应项目模板](xref:spa/index#installation)。</span><span class="sxs-lookup"><span data-stu-id="5a61c-110">To get started, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span> <span data-ttu-id="5a61c-111">这些说明不适用于.NET 核心中包含的前一响应项目模板 2.0.x SDK。</span><span class="sxs-lookup"><span data-stu-id="5a61c-111">These instructions don't apply to the previous React project template included in the .NET Core 2.0.x SDK.</span></span>

<span data-ttu-id="5a61c-112">从命令提示符下使用命令创建新项目`dotnet new react`空的目录中。</span><span class="sxs-lookup"><span data-stu-id="5a61c-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="5a61c-113">例如，以下命令创建的应用程序中*我新应用*目录并切换到该目录：</span><span class="sxs-lookup"><span data-stu-id="5a61c-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="5a61c-114">从 Visual Studio 或.NET Core CLI 运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="5a61c-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5a61c-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a61c-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="5a61c-116">打开生成*.csproj*文件中，并从那里运行正常的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a61c-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="5a61c-117">生成过程还原首次运行，可能需要几分钟的 npm 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="5a61c-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="5a61c-118">后续的生成处于快得多。</span><span class="sxs-lookup"><span data-stu-id="5a61c-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="5a61c-119">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5a61c-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="5a61c-120">确保你具有调用的环境变量`ASPNETCORE_Environment`值为`Development`。</span><span class="sxs-lookup"><span data-stu-id="5a61c-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="5a61c-121">在 Windows 上 （在非 PowerShell 提示），运行`SET ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="5a61c-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="5a61c-122">在 Linux 或 macOS 上，运行`export ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="5a61c-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="5a61c-123">运行`dotnet build`以验证你的应用程序正确生成。</span><span class="sxs-lookup"><span data-stu-id="5a61c-123">Run `dotnet build` to verify your app builds correctly.</span></span> <span data-ttu-id="5a61c-124">首次在运行，生成过程还原 npm 依赖关系，可能需要几分钟。</span><span class="sxs-lookup"><span data-stu-id="5a61c-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="5a61c-125">后续的生成处于快得多。</span><span class="sxs-lookup"><span data-stu-id="5a61c-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="5a61c-126">运行`dotnet run`以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a61c-126">Run `dotnet run` to start the app.</span></span>

---

<span data-ttu-id="5a61c-127">项目模板创建一个 ASP.NET Core 应用和响应应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a61c-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="5a61c-128">ASP.NET Core 应用旨在用于数据访问、 授权和其他服务器端问题。</span><span class="sxs-lookup"><span data-stu-id="5a61c-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="5a61c-129">响应应用程序中，驻留在*ClientApp*子目录，旨在用于所有 UI 问题。</span><span class="sxs-lookup"><span data-stu-id="5a61c-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="5a61c-130">添加页面、 映像，样式、 模块、 等。</span><span class="sxs-lookup"><span data-stu-id="5a61c-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="5a61c-131">*ClientApp*目录是标准的 CRA 做出响应的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a61c-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="5a61c-132">请参阅官方[CRA 文档](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="5a61c-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="5a61c-133">略有差异通过此模板创建的响应应用程序和项目之间创建由 CRA 然后重试。但是，应用程序的功能保持不变。</span><span class="sxs-lookup"><span data-stu-id="5a61c-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="5a61c-134">由模板创建此应用程序包含[Bootstrap](https://getbootstrap.com/)-基于布局和一个基本的路由示例。</span><span class="sxs-lookup"><span data-stu-id="5a61c-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="5a61c-135">安装 npm 包</span><span class="sxs-lookup"><span data-stu-id="5a61c-135">Install npm packages</span></span>

<span data-ttu-id="5a61c-136">若要安装第三方 npm 包，使用命令提示符处， *ClientApp*子目录。</span><span class="sxs-lookup"><span data-stu-id="5a61c-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="5a61c-137">例如:</span><span class="sxs-lookup"><span data-stu-id="5a61c-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="5a61c-138">发布和部署</span><span class="sxs-lookup"><span data-stu-id="5a61c-138">Publish and deploy</span></span>

<span data-ttu-id="5a61c-139">在开发中，应用将在优化为开发人员方便起见模式下运行。</span><span class="sxs-lookup"><span data-stu-id="5a61c-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="5a61c-140">例如，JavaScript 捆绑包包括源地图 （以便在调试时，你可以看到原始源代码）。</span><span class="sxs-lookup"><span data-stu-id="5a61c-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="5a61c-141">该应用监视 JavaScript、 HTML 和 CSS 文件在磁盘上的更改自动重新编译并重新加载当它发现更改这些文件。</span><span class="sxs-lookup"><span data-stu-id="5a61c-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="5a61c-142">在生产中，提供您针对性能进行了优化的应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="5a61c-142">In production, serve a version of your app that is optimized for performance.</span></span> <span data-ttu-id="5a61c-143">这被配置为自动发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="5a61c-143">This is configured to happen automatically.</span></span> <span data-ttu-id="5a61c-144">发布时，生成配置会发出缩减，transpiled 生成的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="5a61c-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="5a61c-145">与不同的开发生成、 生产生成不需要在服务器上安装的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="5a61c-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="5a61c-146">您可以使用标准[ASP.NET Core 托管和部署方法](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="5a61c-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="5a61c-147">独立运行 CRA 服务器</span><span class="sxs-lookup"><span data-stu-id="5a61c-147">Run the CRA server independently</span></span>

<span data-ttu-id="5a61c-148">将项目配置为在开发模式下启动 ASP.NET Core 应用时在后台启动自己 CRA development server 的实例。</span><span class="sxs-lookup"><span data-stu-id="5a61c-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="5a61c-149">这很方便，因为它意味着无需手动运行单独的服务器。</span><span class="sxs-lookup"><span data-stu-id="5a61c-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="5a61c-150">没有此默认设置的缺陷。</span><span class="sxs-lookup"><span data-stu-id="5a61c-150">There is a drawback to this default setup.</span></span> <span data-ttu-id="5a61c-151">每次修改你的 C# 代码和应用程序需要重新启动，将 ASP.NET 核心 CRA 服务器重新启动。</span><span class="sxs-lookup"><span data-stu-id="5a61c-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="5a61c-152">几秒钟后需要重新启动。</span><span class="sxs-lookup"><span data-stu-id="5a61c-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="5a61c-153">如果您正在进行频繁的 C# 代码编辑，并且不希望等待 CRA 服务器重新启动，运行 CRA 服务器外部，独立于 ASP.NET 核心进程。</span><span class="sxs-lookup"><span data-stu-id="5a61c-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="5a61c-154">若要这样做：</span><span class="sxs-lookup"><span data-stu-id="5a61c-154">To do so:</span></span>

1. <span data-ttu-id="5a61c-155">在命令提示符下，切换到*ClientApp*子目录，并启动 CRA 开发服务器：</span><span class="sxs-lookup"><span data-stu-id="5a61c-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="5a61c-156">修改 ASP.NET Core 应用程序而不是启动其自身的一个使用外部 CRA 服务器实例。</span><span class="sxs-lookup"><span data-stu-id="5a61c-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="5a61c-157">在你*启动*类中，替换`spa.UseReactDevelopmentServer`替换为以下调用：</span><span class="sxs-lookup"><span data-stu-id="5a61c-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="5a61c-158">当你启动 ASP.NET Core 应用程序时，它不会启动 CRA 服务器。</span><span class="sxs-lookup"><span data-stu-id="5a61c-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="5a61c-159">将改为使用手动启动实例。</span><span class="sxs-lookup"><span data-stu-id="5a61c-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="5a61c-160">这使它能够启动并重新启动速度更快。</span><span class="sxs-lookup"><span data-stu-id="5a61c-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="5a61c-161">它不再正在等待响应应用程序，以重新生成每次。</span><span class="sxs-lookup"><span data-stu-id="5a61c-161">It's no longer waiting for your React app to rebuild each time.</span></span>
