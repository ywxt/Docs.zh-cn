---
title: "使用角速度项目模板"
author: SteveSandersonMS
description: "了解如何开始使用 ASP.NET 核心单页面应用程序 (SPA) 发布候选项目模板用于角和角速度 CLI。"
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/angular
ms.openlocfilehash: b54798a43f6a448c2e2aad0613ee60805a61f303
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="use-the-angular-project-template-release-candidate"></a><span data-ttu-id="7860c-103">使用角速度项目模板 （候选发布版）</span><span class="sxs-lookup"><span data-stu-id="7860c-103">Use the Angular project template (release candidate)</span></span>

> [!NOTE]
> <span data-ttu-id="7860c-104">本文档不是有关发布的角度项目模板。</span><span class="sxs-lookup"><span data-stu-id="7860c-104">This documentation is not about the released Angular project template.</span></span> <span data-ttu-id="7860c-105">**此文档是有关的角度模板候选发布版本。**</span><span class="sxs-lookup"><span data-stu-id="7860c-105">**This documentation is about the release candidate of the Angular template.**</span></span> <span data-ttu-id="7860c-106">我们希望在早期 2018年提供已发布的版本。</span><span class="sxs-lookup"><span data-stu-id="7860c-106">We hope to ship the released version in early 2018.</span></span>

<span data-ttu-id="7860c-107">更新的角度项目模板提供了 ASP.NET Core 应用使用角速度 5 和角速度 CLI 可以实现的丰富的客户端用户界面 (UI) 的方便的起始点。</span><span class="sxs-lookup"><span data-stu-id="7860c-107">The updated Angular project template provides a convenient starting point for ASP.NET Core apps using Angular 5 and the Angular CLI to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="7860c-108">该模板是等效于创建充当 API 后端的 ASP.NET Core 项目和一个角度 CLI 项目，以充当用户界面。</span><span class="sxs-lookup"><span data-stu-id="7860c-108">The template is equivalent to creating an ASP.NET Core project to act as an API backend and an Angular CLI project to act as a UI.</span></span> <span data-ttu-id="7860c-109">模板提供承载这两种项目类型中的单个应用程序项目的便利性。</span><span class="sxs-lookup"><span data-stu-id="7860c-109">The template offers the convenience of hosting both project types in a single app project.</span></span> <span data-ttu-id="7860c-110">因此，可以生成应用程序项目并将其发布为单个单元。</span><span class="sxs-lookup"><span data-stu-id="7860c-110">Consequently, the app project can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="7860c-111">创建新的应用程序</span><span class="sxs-lookup"><span data-stu-id="7860c-111">Create a new app</span></span>

<span data-ttu-id="7860c-112">若要开始，请确保你已[安装更新的角度项目模板](xref:spa/index#installation)。</span><span class="sxs-lookup"><span data-stu-id="7860c-112">To get started, ensure you've [installed the updated Angular project template](xref:spa/index#installation).</span></span> <span data-ttu-id="7860c-113">这些说明不适用于.NET 核心中包含的上一个角度项目模板 2.0.x SDK。</span><span class="sxs-lookup"><span data-stu-id="7860c-113">These instructions don't apply to the previous Angular project template included in the .NET Core 2.0.x SDK.</span></span>

<span data-ttu-id="7860c-114">从命令提示符下使用命令创建新项目`dotnet new angular`空的目录中。</span><span class="sxs-lookup"><span data-stu-id="7860c-114">Create a new project from a command prompt using the command `dotnet new angular` in an empty directory.</span></span> <span data-ttu-id="7860c-115">例如，以下命令创建的应用程序中*我新应用*目录并切换到该目录：</span><span class="sxs-lookup"><span data-stu-id="7860c-115">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new angular -o my-new-app
cd my-new-app
```

<span data-ttu-id="7860c-116">从 Visual Studio 或.NET Core CLI 运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="7860c-116">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7860c-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7860c-117">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="7860c-118">打开生成*.csproj*文件中，并从那里运行正常的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7860c-118">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="7860c-119">生成过程还原首次运行，可能需要几分钟的 npm 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="7860c-119">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="7860c-120">后续的生成处于快得多。</span><span class="sxs-lookup"><span data-stu-id="7860c-120">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7860c-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7860c-121">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="7860c-122">确保你具有调用的环境变量`ASPNETCORE_Environment`值为`Development`。</span><span class="sxs-lookup"><span data-stu-id="7860c-122">Ensure you have an environment variable called `ASPNETCORE_Environment` with a value of `Development`.</span></span> <span data-ttu-id="7860c-123">在 Windows 上 （在非 PowerShell 提示），运行`SET ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="7860c-123">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="7860c-124">在 Linux 或 macOS 上，运行`export ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="7860c-124">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="7860c-125">运行`dotnet build`以验证该应用程序正确生成。</span><span class="sxs-lookup"><span data-stu-id="7860c-125">Run `dotnet build` to verify the app builds correctly.</span></span> <span data-ttu-id="7860c-126">首次在运行，生成过程还原 npm 依赖关系，可能需要几分钟。</span><span class="sxs-lookup"><span data-stu-id="7860c-126">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="7860c-127">后续的生成处于快得多。</span><span class="sxs-lookup"><span data-stu-id="7860c-127">Subsequent builds are much faster.</span></span>

<span data-ttu-id="7860c-128">运行`dotnet run`以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="7860c-128">Run `dotnet run` to start the app.</span></span> <span data-ttu-id="7860c-129">类似于以下的消息将记录：</span><span class="sxs-lookup"><span data-stu-id="7860c-129">A message similar to the following is logged:</span></span>

```console
Now listening on: http://localhost:<port>
```

<span data-ttu-id="7860c-130">导航到此 URL 在浏览器。</span><span class="sxs-lookup"><span data-stu-id="7860c-130">Navigate to this URL in a browser.</span></span>

<span data-ttu-id="7860c-131">应用程序启动的后台中的角度 CLI 服务器实例。</span><span class="sxs-lookup"><span data-stu-id="7860c-131">The app starts up an instance of the Angular CLI server in the background.</span></span> <span data-ttu-id="7860c-132">记录类似于以下消息： *NG Live 开发服务器正在侦听 localhost:&lt;otherport&gt;，打开浏览器上 http://localhost:&lt;otherport&gt; /*.</span><span class="sxs-lookup"><span data-stu-id="7860c-132">A message similar to the following is logged: *NG Live Development Server is listening on localhost:&lt;otherport&gt;, open your browser on http://localhost:&lt;otherport&gt;/*.</span></span> <span data-ttu-id="7860c-133">忽略此消息&mdash;它具有**不**组合 ASP.NET Core 和角速度 CLI 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="7860c-133">Ignore this message&mdash;it's **not** the URL for the combined ASP.NET Core and Angular CLI app.</span></span>

---

<span data-ttu-id="7860c-134">项目模板创建 ASP.NET Core 应用和角速度应用。</span><span class="sxs-lookup"><span data-stu-id="7860c-134">The project template creates an ASP.NET Core app and an Angular app.</span></span> <span data-ttu-id="7860c-135">ASP.NET Core 应用旨在用于数据访问、 授权和其他服务器端问题。</span><span class="sxs-lookup"><span data-stu-id="7860c-135">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="7860c-136">角度的应用程序，驻留在*ClientApp*子目录，旨在用于所有 UI 问题。</span><span class="sxs-lookup"><span data-stu-id="7860c-136">The Angular app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="7860c-137">添加页面、 映像，样式、 模块、 等。</span><span class="sxs-lookup"><span data-stu-id="7860c-137">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="7860c-138">*ClientApp*目录包含标准的角度 CLI 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7860c-138">The *ClientApp* directory contains a standard Angular CLI app.</span></span> <span data-ttu-id="7860c-139">请参阅官方[角度文档](https://github.com/angular/angular-cli/wiki)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="7860c-139">See the official [Angular documentation](https://github.com/angular/angular-cli/wiki) for more information.</span></span>

<span data-ttu-id="7860c-140">略有差异由此模板创建的角度的应用程序和创建角度 cli 本身之间 (通过`ng new`); 但是，应用程序的功能保持不变。</span><span class="sxs-lookup"><span data-stu-id="7860c-140">There are slight differences between the Angular app created by this template and the one created by Angular CLI itself (via `ng new`); however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="7860c-141">由模板创建此应用程序包含[Bootstrap](https://getbootstrap.com/)-基于布局和一个基本的路由示例。</span><span class="sxs-lookup"><span data-stu-id="7860c-141">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="run-ng-commands"></a><span data-ttu-id="7860c-142">运行 ng 命令</span><span class="sxs-lookup"><span data-stu-id="7860c-142">Run ng commands</span></span>

<span data-ttu-id="7860c-143">在命令提示符下，切换到*ClientApp*子目录：</span><span class="sxs-lookup"><span data-stu-id="7860c-143">In a command prompt, switch to the *ClientApp* subdirectory:</span></span>

```console
cd ClientApp
```

<span data-ttu-id="7860c-144">如果你有`ng`全局安装的工具，你可以运行任何其命令。</span><span class="sxs-lookup"><span data-stu-id="7860c-144">If you have the `ng` tool installed globally, you can run any of its commands.</span></span> <span data-ttu-id="7860c-145">例如，你可以运行`ng lint`， `ng test`，或任何其他[角度 CLI 命令](https://github.com/angular/angular-cli/wiki#additional-commands)。</span><span class="sxs-lookup"><span data-stu-id="7860c-145">For example, you can run `ng lint`, `ng test`, or any of the other [Angular CLI commands](https://github.com/angular/angular-cli/wiki#additional-commands).</span></span> <span data-ttu-id="7860c-146">没有无需运行`ng serve`不过，因为 ASP.NET Core 应用程序处理为服务器端和客户端部分你的应用程序提供服务。</span><span class="sxs-lookup"><span data-stu-id="7860c-146">There's no need to run `ng serve` though, because your ASP.NET Core app deals with serving both server-side and client-side parts of your app.</span></span> <span data-ttu-id="7860c-147">在内部，它使用`ng serve`开发中。</span><span class="sxs-lookup"><span data-stu-id="7860c-147">Internally, it uses `ng serve` in development.</span></span>

<span data-ttu-id="7860c-148">如果你没有`ng`工具安装，运行`npm run ng`相反。</span><span class="sxs-lookup"><span data-stu-id="7860c-148">If you don't have the `ng` tool installed, run `npm run ng` instead.</span></span> <span data-ttu-id="7860c-149">例如，你可以运行`npm run ng lint`或`npm run ng test`。</span><span class="sxs-lookup"><span data-stu-id="7860c-149">For example, you can run `npm run ng lint` or `npm run ng test`.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="7860c-150">安装 npm 包</span><span class="sxs-lookup"><span data-stu-id="7860c-150">Install npm packages</span></span>

<span data-ttu-id="7860c-151">若要安装第三方 npm 包，使用命令提示符处， *ClientApp*子目录。</span><span class="sxs-lookup"><span data-stu-id="7860c-151">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="7860c-152">例如:</span><span class="sxs-lookup"><span data-stu-id="7860c-152">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="7860c-153">发布和部署</span><span class="sxs-lookup"><span data-stu-id="7860c-153">Publish and deploy</span></span>

<span data-ttu-id="7860c-154">在开发中，应用将在优化为开发人员方便起见模式下运行。</span><span class="sxs-lookup"><span data-stu-id="7860c-154">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="7860c-155">例如，JavaScript 捆绑包包括源地图 （以便在调试时，你可以看到原始 TypeScript 代码）。</span><span class="sxs-lookup"><span data-stu-id="7860c-155">For example, JavaScript bundles include source maps (so that when debugging, you can see your original TypeScript code).</span></span> <span data-ttu-id="7860c-156">应用程序监视的磁盘上的 TypeScript、 HTML 和 CSS 文件更改自动重新编译并重新加载当它发现更改这些文件。</span><span class="sxs-lookup"><span data-stu-id="7860c-156">The app watches for TypeScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="7860c-157">在生产中，提供您针对性能进行了优化的应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="7860c-157">In production, serve a version of your app that is optimized for performance.</span></span> <span data-ttu-id="7860c-158">这被配置为自动发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="7860c-158">This is configured to happen automatically.</span></span> <span data-ttu-id="7860c-159">发布时，生成配置发出缩减，预时间的 (AoT) 编译生成的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="7860c-159">When you publish, the build configuration emits a minified, ahead-of-time (AoT) compiled build of your client-side code.</span></span> <span data-ttu-id="7860c-160">与开发内部版本，不同生产生成不需要在服务器上安装的 Node.js (除非已启用[服务器端预呈现](#server-side-rendering))。</span><span class="sxs-lookup"><span data-stu-id="7860c-160">Unlike the development build, the production build doesn't require Node.js to be installed on the server (unless you have enabled [server-side prerendering](#server-side-rendering)).</span></span>

<span data-ttu-id="7860c-161">您可以使用标准[ASP.NET Core 托管和部署方法](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="7860c-161">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-ng-serve-independently"></a><span data-ttu-id="7860c-162">独立运行"ng 提供"</span><span class="sxs-lookup"><span data-stu-id="7860c-162">Run "ng serve" independently</span></span>

<span data-ttu-id="7860c-163">将项目配置为在开发模式下启动 ASP.NET Core 应用时在后台启动自己的角度 CLI 服务器实例。</span><span class="sxs-lookup"><span data-stu-id="7860c-163">The project is configured to start its own instance of the Angular CLI server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="7860c-164">这很方便，因为无需手动运行单独的服务器。</span><span class="sxs-lookup"><span data-stu-id="7860c-164">This is convenient because you don't have to run a separate server manually.</span></span>

<span data-ttu-id="7860c-165">没有此默认设置的缺陷。</span><span class="sxs-lookup"><span data-stu-id="7860c-165">There is a drawback to this default setup.</span></span> <span data-ttu-id="7860c-166">每次修改你的 C# 代码和应用程序需要重新启动，将 ASP.NET 核心角度 CLI 服务器重新启动。</span><span class="sxs-lookup"><span data-stu-id="7860c-166">Each time you modify your C# code and your ASP.NET Core app needs to restart, the Angular CLI server restarts.</span></span> <span data-ttu-id="7860c-167">启动备份需要大约为 10 秒钟。</span><span class="sxs-lookup"><span data-stu-id="7860c-167">Around 10 seconds is required to start back up.</span></span> <span data-ttu-id="7860c-168">如果您正在进行频繁的 C# 代码编辑，并且不希望等待重新启动的角度 CLI，运行角度 CLI 服务器外部，独立于 ASP.NET 核心进程。</span><span class="sxs-lookup"><span data-stu-id="7860c-168">If you're making frequent C# code edits and don't want to wait for Angular CLI to restart, run the Angular CLI server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="7860c-169">若要这样做：</span><span class="sxs-lookup"><span data-stu-id="7860c-169">To do so:</span></span>

1. <span data-ttu-id="7860c-170">在命令提示符下，切换到*ClientApp*子目录，并启动角度 CLI 开发服务器：</span><span class="sxs-lookup"><span data-stu-id="7860c-170">In a command prompt, switch to the *ClientApp* subdirectory, and launch the Angular CLI development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7860c-171">使用`npm start`不启动的角度 CLI 开发服务器`ng serve`，以便中的配置*package.json*遵守。</span><span class="sxs-lookup"><span data-stu-id="7860c-171">Use `npm start` to launch the Angular CLI development server, not `ng serve`, so that the configuration in *package.json* is respected.</span></span> <span data-ttu-id="7860c-172">若要将附加参数传递到角度 CLI 服务器，请将它们添加到相关`scripts`行中你*package.json*文件。</span><span class="sxs-lookup"><span data-stu-id="7860c-172">To pass additional parameters to the Angular CLI server, add them to the relevant `scripts` line in your *package.json* file.</span></span>

2. <span data-ttu-id="7860c-173">修改 ASP.NET Core 应用程序而不是启动其自身的一个使用外部的角度 CLI 实例。</span><span class="sxs-lookup"><span data-stu-id="7860c-173">Modify your ASP.NET Core app to use the external Angular CLI instance instead of launching one of its own.</span></span> <span data-ttu-id="7860c-174">在你*启动*类中，替换`spa.UseAngularCliServer`替换为以下调用：</span><span class="sxs-lookup"><span data-stu-id="7860c-174">In your *Startup* class, replace the `spa.UseAngularCliServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:4200");
    ```

<span data-ttu-id="7860c-175">当你启动 ASP.NET Core 应用程序时，它不会启动角度 CLI 服务器。</span><span class="sxs-lookup"><span data-stu-id="7860c-175">When you start your ASP.NET Core app, it won't launch an Angular CLI server.</span></span> <span data-ttu-id="7860c-176">将改为使用手动启动实例。</span><span class="sxs-lookup"><span data-stu-id="7860c-176">The instance you started manually is used instead.</span></span> <span data-ttu-id="7860c-177">这使它能够启动并重新启动速度更快。</span><span class="sxs-lookup"><span data-stu-id="7860c-177">This enables it to start and restart faster.</span></span> <span data-ttu-id="7860c-178">它不再等待角度 CLI 来每次重新生成客户端应用。</span><span class="sxs-lookup"><span data-stu-id="7860c-178">It's no longer waiting for Angular CLI to rebuild your client app each time.</span></span>

## <a name="server-side-rendering"></a><span data-ttu-id="7860c-179">服务器端呈现</span><span class="sxs-lookup"><span data-stu-id="7860c-179">Server-side rendering</span></span>

<span data-ttu-id="7860c-180">作为一种性能功能，你可以选择预呈现上服务器以及运行客户端上的应用程序角度。</span><span class="sxs-lookup"><span data-stu-id="7860c-180">As a performance feature, you can choose to pre-render your Angular app on the server as well as running it on the client.</span></span> <span data-ttu-id="7860c-181">这意味着浏览器接收表示您的应用程序的初始用户界面，使其能够显示它即使在下载并执行 JavaScript 捆绑包之前的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="7860c-181">This means that browsers receive HTML markup representing your app's initial UI, so they display it even before downloading and executing your JavaScript bundles.</span></span> <span data-ttu-id="7860c-182">大部分此操作的实现调用角度功能带来[角度通用](https://universal.angular.io/)。</span><span class="sxs-lookup"><span data-stu-id="7860c-182">Most of the implementation of this comes from an Angular feature called [Angular Universal](https://universal.angular.io/).</span></span>

> [!TIP]
> <span data-ttu-id="7860c-183">启用服务器端呈现 (SSR) 引入了大量的额外复杂性同时在开发和部署过程。</span><span class="sxs-lookup"><span data-stu-id="7860c-183">Enabling server-side rendering (SSR) introduces a number of extra complications both during development and deployment.</span></span> <span data-ttu-id="7860c-184">读取[SSR 缺点](#drawbacks-of-ssr)确定 SSR 是否适合你的要求。</span><span class="sxs-lookup"><span data-stu-id="7860c-184">Read [drawbacks of SSR](#drawbacks-of-ssr) to determine if SSR is a good fit for your requirements.</span></span>

<span data-ttu-id="7860c-185">若要启用 SSR，你需要进行大量添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="7860c-185">To enable SSR, you need to make a number of additions to your project.</span></span>

<span data-ttu-id="7860c-186">在*启动*类，*后*配置行`spa.Options.SourcePath`，和*之前*调用`UseAngularCliServer`或`UseProxyToSpaDevelopmentServer`，添加以下：</span><span class="sxs-lookup"><span data-stu-id="7860c-186">In the *Startup* class, *after* the line that configures `spa.Options.SourcePath`, and *before* the call to `UseAngularCliServer` or `UseProxyToSpaDevelopmentServer`, add the following:</span></span>

[!code-csharp[](sample/AngularServerSideRendering/Startup.cs?name=snippet_Call_UseSpa&highlight=5-12)]

<span data-ttu-id="7860c-187">在开发模式下，此代码将尝试通过运行脚本创建 SSR 捆绑`build:ssr`中, 定义*ClientApp\package.json*。</span><span class="sxs-lookup"><span data-stu-id="7860c-187">In development mode, this code attempts to build the SSR bundle by running the script `build:ssr`, which is defined in *ClientApp\package.json*.</span></span> <span data-ttu-id="7860c-188">这将生成名为的角度应用`ssr`，其中尚未定义。</span><span class="sxs-lookup"><span data-stu-id="7860c-188">This builds an Angular app named `ssr`, which is not yet defined.</span></span> 

<span data-ttu-id="7860c-189">在结束`apps`数组中*ClientApp/.angular-cli.json*，定义具有名称的额外应用`ssr`。</span><span class="sxs-lookup"><span data-stu-id="7860c-189">At the end of the `apps` array in *ClientApp/.angular-cli.json*, define an extra app with name `ssr`.</span></span> <span data-ttu-id="7860c-190">使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="7860c-190">Use the following options:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/.angular-cli.json?range=24-41)]

<span data-ttu-id="7860c-191">此新 SSR 启用应用程序配置需要两个其他文件： *tsconfig.server.json*和*main.server.ts*。</span><span class="sxs-lookup"><span data-stu-id="7860c-191">This new SSR-enabled app configuration requires two further files: *tsconfig.server.json* and *main.server.ts*.</span></span> <span data-ttu-id="7860c-192">*Tsconfig.server.json*文件指定 TypeScript 编译选项。</span><span class="sxs-lookup"><span data-stu-id="7860c-192">The *tsconfig.server.json* file specifies TypeScript compilation options.</span></span> <span data-ttu-id="7860c-193">*Main.server.ts*文件期间 SSR 作为代码入口点。</span><span class="sxs-lookup"><span data-stu-id="7860c-193">The *main.server.ts* file serves as the code entry point during SSR.</span></span>

<span data-ttu-id="7860c-194">添加新的文件称为*tsconfig.server.json*内*ClientApp/src* (与现有一起*tsconfig.app.json*)，包含以下：</span><span class="sxs-lookup"><span data-stu-id="7860c-194">Add a new file called *tsconfig.server.json* inside *ClientApp/src* (alongside the existing *tsconfig.app.json*), containing the following:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/src/tsconfig.server.json)]

<span data-ttu-id="7860c-195">此文件将配置角的 AoT 编译器对于调用模块看起来`app.server.module`。</span><span class="sxs-lookup"><span data-stu-id="7860c-195">This file configures Angular's AoT compiler to look for a module called `app.server.module`.</span></span> <span data-ttu-id="7860c-196">通过创建一个新文件添加这*ClientApp/src/app/app.server.module.ts* (与现有一起*app.module.ts*) 包含以下：</span><span class="sxs-lookup"><span data-stu-id="7860c-196">Add this by creating a new file at *ClientApp/src/app/app.server.module.ts* (alongside the existing *app.module.ts*) containing the following:</span></span> 

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/app/app.server.module.ts)]

<span data-ttu-id="7860c-197">此模块继承自客户端`app.module`并定义哪些额外角度模块 SSR 中均可用。</span><span class="sxs-lookup"><span data-stu-id="7860c-197">This module inherits from your client-side `app.module` and defines which extra Angular modules are available during SSR.</span></span>

<span data-ttu-id="7860c-198">回想一下，新`ssr`中的条目*.angular cli.json*引用一个入口点文件称为*main.server.ts*。</span><span class="sxs-lookup"><span data-stu-id="7860c-198">Recall that the new `ssr` entry in *.angular-cli.json* referenced an entry point file called *main.server.ts*.</span></span> <span data-ttu-id="7860c-199">你尚未尚未添加该文件中，并现在是时候，若要这样做。</span><span class="sxs-lookup"><span data-stu-id="7860c-199">You haven't yet added that file, and now is time to do so.</span></span> <span data-ttu-id="7860c-200">创建一个新文件*ClientApp/src/main.server.ts* (与现有一起*main.ts*)，包含以下：</span><span class="sxs-lookup"><span data-stu-id="7860c-200">Create a new file at *ClientApp/src/main.server.ts* (alongside the existing *main.ts*), containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/main.server.ts)]

<span data-ttu-id="7860c-201">此文件的代码是什么 ASP.NET Core 执行每个请求运行时`UseSpaPrerendering`添加到的中间件*启动*类。</span><span class="sxs-lookup"><span data-stu-id="7860c-201">This file's code is what ASP.NET Core executes for each request when it runs the `UseSpaPrerendering` middleware that you added to the *Startup* class.</span></span> <span data-ttu-id="7860c-202">处理接收`params`从.NET 代码 （如所请求的 URL) 以及角度 SSR Api 调用以获取生成的 HTML。</span><span class="sxs-lookup"><span data-stu-id="7860c-202">It deals with receiving `params` from the .NET code (such as the URL being requested), and making calls to Angular SSR APIs to get the resulting HTML.</span></span> 

<span data-ttu-id="7860c-203">严格来讲，这不足以在开发模式下启用 SSR。</span><span class="sxs-lookup"><span data-stu-id="7860c-203">Strictly-speaking, this is sufficient to enable SSR in development mode.</span></span> <span data-ttu-id="7860c-204">若要使一个最终的更改，以便你的应用程序能否正常工作时发布至关重要。</span><span class="sxs-lookup"><span data-stu-id="7860c-204">It's essential to make one final change so that your app works correctly when published.</span></span> <span data-ttu-id="7860c-205">在您的应用程序的 main 中*.csproj*文件中，将`BuildServerSideRenderer`属性值设置为`true`:</span><span class="sxs-lookup"><span data-stu-id="7860c-205">In your app's main *.csproj* file, set the `BuildServerSideRenderer` property value to `true`:</span></span>

[!code-xml[](sample/AngularServerSideRendering/AngularServerSideRendering.csproj?name=snippet_EnableBuildServerSideRenderer)]

<span data-ttu-id="7860c-206">这会将配置生成过程运行`build:ssr`在发布过程并将 SSR 文件部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="7860c-206">This configures the build process to run `build:ssr` during publishing and deploy the SSR files to the server.</span></span> <span data-ttu-id="7860c-207">如果你不启用此功能，SSR 将在生产环境中失败。</span><span class="sxs-lookup"><span data-stu-id="7860c-207">If you don't enable this, SSR fails in production.</span></span>

<span data-ttu-id="7860c-208">你的应用程序运行时在开发或生产模式下，角度代码预先将呈现为 HTML 服务器上。</span><span class="sxs-lookup"><span data-stu-id="7860c-208">When your app runs in either development or production mode, the Angular code pre-renders as HTML on the server.</span></span> <span data-ttu-id="7860c-209">客户端代码执行正常。</span><span class="sxs-lookup"><span data-stu-id="7860c-209">The client-side code executes as normal.</span></span>

### <a name="pass-data-from-net-code-into-typescript-code"></a><span data-ttu-id="7860c-210">将数据从.NET 代码传递到 TypeScript 代码</span><span class="sxs-lookup"><span data-stu-id="7860c-210">Pass data from .NET code into TypeScript code</span></span>

<span data-ttu-id="7860c-211">在 SSR，你可能需要将每个请求数据从 ASP.NET Core 应用程序传递到应用程序角度。</span><span class="sxs-lookup"><span data-stu-id="7860c-211">During SSR, you might want to pass per-request data from your ASP.NET Core app into your Angular app.</span></span> <span data-ttu-id="7860c-212">例如，你无法传递 cookie 信息或内容从数据库读取。</span><span class="sxs-lookup"><span data-stu-id="7860c-212">For example, you could pass cookie information or something read from a database.</span></span> <span data-ttu-id="7860c-213">若要执行此操作，编辑你*启动*类。</span><span class="sxs-lookup"><span data-stu-id="7860c-213">To do this, edit your *Startup* class.</span></span> <span data-ttu-id="7860c-214">中的回调`UseSpaPrerendering`，设置的值`options.SupplyData`如下所示：</span><span class="sxs-lookup"><span data-stu-id="7860c-214">In the callback for `UseSpaPrerendering`, set a value for `options.SupplyData` such as the following:</span></span>

```csharp
options.SupplyData = (context, data) =>
{
    // Creates a new value called isHttpsRequest that is passed to TypeScript code
    data["isHttpsRequest"] = context.Request.IsHttps;
};
```

<span data-ttu-id="7860c-215">`SupplyData`回调允许传递任意、 每个请求、 JSON 序列化数据 （如字符串、 布尔值或数字）。</span><span class="sxs-lookup"><span data-stu-id="7860c-215">The `SupplyData` callback lets you pass arbitrary, per-request, JSON-serializable data (for example, strings, booleans, or numbers).</span></span> <span data-ttu-id="7860c-216">你*main.server.ts*代码接收为`params.data`。</span><span class="sxs-lookup"><span data-stu-id="7860c-216">Your *main.server.ts* code receives this as `params.data`.</span></span> <span data-ttu-id="7860c-217">例如，上面的代码示例将传递一个布尔值作为`params.data.isHttpsRequest`到`createServerRenderer`回调。</span><span class="sxs-lookup"><span data-stu-id="7860c-217">For example, the preceding code sample passes a boolean value as `params.data.isHttpsRequest` into the `createServerRenderer` callback.</span></span> <span data-ttu-id="7860c-218">你可以将传递给你的应用以支持角任何方式的其他部分。</span><span class="sxs-lookup"><span data-stu-id="7860c-218">You can pass this to other parts of your app in any way supported by Angular.</span></span> <span data-ttu-id="7860c-219">有关示例，请参阅如何*main.server.ts*传递`BASE_URL`到其构造函数声明为接收它的任何组件的值。</span><span class="sxs-lookup"><span data-stu-id="7860c-219">For example, see how *main.server.ts* passes the `BASE_URL` value to any component whose constructor is declared to receive it.</span></span>

### <a name="drawbacks-of-ssr"></a><span data-ttu-id="7860c-220">SSR 的缺点</span><span class="sxs-lookup"><span data-stu-id="7860c-220">Drawbacks of SSR</span></span>

<span data-ttu-id="7860c-221">并非所有应用都受益于 SSR。</span><span class="sxs-lookup"><span data-stu-id="7860c-221">Not all apps benefit from SSR.</span></span> <span data-ttu-id="7860c-222">主要优点是任何可察觉的性能。</span><span class="sxs-lookup"><span data-stu-id="7860c-222">The primary benefit is perceived performance.</span></span> <span data-ttu-id="7860c-223">达到你的应用程序，通过慢速网络连接或慢速的移动设备上的访问者看到初始 UI 快，即使它未采用一段时间才能提取或分析 JavaScript 捆绑包。</span><span class="sxs-lookup"><span data-stu-id="7860c-223">Visitors reaching your app over a slow network connection or on slow mobile devices see the initial UI quickly, even if it takes a while to fetch or parse the JavaScript bundles.</span></span> <span data-ttu-id="7860c-224">但是，许多 Spa 主要用于通过快速的计算机上的快速、 内部公司网络应用程序几乎立刻出现的位置。</span><span class="sxs-lookup"><span data-stu-id="7860c-224">However, many SPAs are mainly used over fast, internal company networks on fast computers where the app appears almost instantly.</span></span>

<span data-ttu-id="7860c-225">同时，没有启用 SSR 明显的缺点。</span><span class="sxs-lookup"><span data-stu-id="7860c-225">At the same time, there are significant drawbacks to enabling SSR.</span></span> <span data-ttu-id="7860c-226">它向你的开发过程的复杂性。</span><span class="sxs-lookup"><span data-stu-id="7860c-226">It adds complexity to your development process.</span></span> <span data-ttu-id="7860c-227">你的代码必须在两个不同环境中运行： 客户端和服务器端 （在 Node.js 环境中从 ASP.NET Core 调用）。</span><span class="sxs-lookup"><span data-stu-id="7860c-227">Your code must run in two different environments: client-side and server-side (in a Node.js environment invoked from ASP.NET Core).</span></span> <span data-ttu-id="7860c-228">下面是一些需要牢记的事项：</span><span class="sxs-lookup"><span data-stu-id="7860c-228">Here are some things to bear in mind:</span></span>

* <span data-ttu-id="7860c-229">SSR 要求 Node.js 安装生产服务器上。</span><span class="sxs-lookup"><span data-stu-id="7860c-229">SSR requires a Node.js installation on your production servers.</span></span> <span data-ttu-id="7860c-230">这将自动对于某些部署方案，例如 Azure 应用程序服务，但对于其他操作系统，如 Azure Service Fabric 这种情况。</span><span class="sxs-lookup"><span data-stu-id="7860c-230">This is automatically the case for some deployment scenarios, such as Azure App Services, but not for others, such as Azure Service Fabric.</span></span>
* <span data-ttu-id="7860c-231">启用`BuildServerSideRenderer`生成标志原因你*node_modules*目录发布。</span><span class="sxs-lookup"><span data-stu-id="7860c-231">Enabling the `BuildServerSideRenderer` build flag causes your *node_modules* directory to publish.</span></span> <span data-ttu-id="7860c-232">此文件夹包含 20000 多文件，这提高了部署时间。</span><span class="sxs-lookup"><span data-stu-id="7860c-232">This folder contains 20,000+ files, which increases deployment time.</span></span>
* <span data-ttu-id="7860c-233">若要在 Node.js 环境中运行你的代码，它不能依赖于是否存在特定浏览器的 JavaScript Api 例如`window`或`localStorage`。</span><span class="sxs-lookup"><span data-stu-id="7860c-233">To run your code in a Node.js environment, it can't rely on the existence of browser-specific JavaScript APIs such as `window` or `localStorage`.</span></span> <span data-ttu-id="7860c-234">如果你的代码 （或你引用某些第三方库） 尝试使用这些 Api，你将获得 SSR 期间出错。</span><span class="sxs-lookup"><span data-stu-id="7860c-234">If your code (or some third-party library you reference) tries to use these APIs, you'll get an error during SSR.</span></span> <span data-ttu-id="7860c-235">例如，不使用 jQuery 因为它引用了在多个位置的特定浏览器的 Api。</span><span class="sxs-lookup"><span data-stu-id="7860c-235">For example, don't use jQuery because it references browser-specific APIs in many places.</span></span> <span data-ttu-id="7860c-236">若要防止出现错误，您必须避免 SSR 或避免特定浏览器的 Api 或库。</span><span class="sxs-lookup"><span data-stu-id="7860c-236">To prevent errors, you must either avoid SSR or avoid browser-specific APIs or libraries.</span></span> <span data-ttu-id="7860c-237">可以将任何对此类 Api 的调用包装在检查以确保它们不在 SSR 过程中调用。</span><span class="sxs-lookup"><span data-stu-id="7860c-237">You can wrap any calls to such APIs in checks to ensure they aren't invoked during SSR.</span></span> <span data-ttu-id="7860c-238">例如，在 JavaScript 或 TypeScript 代码中使用如下所示检查：</span><span class="sxs-lookup"><span data-stu-id="7860c-238">For example, use a check such as the following in JavaScript or TypeScript code:</span></span>

    ```javascript
    if (typeof window !== 'undefined') {
        // Call browser-specific APIs here
    }
    ```
