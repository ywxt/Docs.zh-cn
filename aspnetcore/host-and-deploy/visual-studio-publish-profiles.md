---
title: 用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件
author: rick-anderson
description: 了解如何在 Visual Studio 中创建发布配置文件，并将它们用于管理针对各种目标的 ASP.NET Core 应用部署。
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: 3e626f99b06b0343360d6c46447e357890433dda
ms.sourcegitcommit: 54655f1e1abf0b64d19506334d94cfdb0caf55f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148923"
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a><span data-ttu-id="135e5-103">用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件</span><span class="sxs-lookup"><span data-stu-id="135e5-103">Visual Studio publish profiles for ASP.NET Core app deployment</span></span>

<span data-ttu-id="135e5-104">作者：[Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="135e5-104">By [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="135e5-105">本文档重点介绍如何使用 Visual Studio 2017 创建并使用发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-105">This document focuses on using Visual Studio 2017 to create and use publish profiles.</span></span> <span data-ttu-id="135e5-106">可以从 MSBuild 和 Visual Studio 2017 运行使用 Visual Studio 创建的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-106">The publish profiles created with Visual Studio can be run from MSBuild and Visual Studio 2017.</span></span> <span data-ttu-id="135e5-107">有关发布到 Azure 的说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用发布到 Azure App Service](xref:tutorials/publish-to-azure-webapp-using-vs)。</span><span class="sxs-lookup"><span data-stu-id="135e5-107">See [Publish an ASP.NET Core web app to Azure App Service using Visual Studio](xref:tutorials/publish-to-azure-webapp-using-vs) for instructions on publishing to Azure.</span></span>

<span data-ttu-id="135e5-108">使用命令 `dotnet new mvc` 创建以下项目文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-108">The following project file was created with the command `dotnet new mvc`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.9" />
  </ItemGroup>

</Project>
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore" Version="1.1.7" />
    <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="1.1.8" />
    <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="1.1.3" />
  </ItemGroup>

</Project>
```

::: moniker-end

<span data-ttu-id="135e5-109">`<Project>` 元素的 `Sdk` 属性完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="135e5-109">The `<Project>` element's `Sdk` attribute accomplishes the following tasks:</span></span>

* <span data-ttu-id="135e5-110">在开始时从 $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props 导入属性文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-110">Imports the properties file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* at the beginning.</span></span>
* <span data-ttu-id="135e5-111">在结束时从 $(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets 导入目标文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-111">Imports the targets file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets* at the end.</span></span>

<span data-ttu-id="135e5-112">`MSBuildSDKsPath`（装有 Visual Studio 2017 Enterprise）的默认位置是 %programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks 文件夹。</span><span class="sxs-lookup"><span data-stu-id="135e5-112">The default location for `MSBuildSDKsPath` (with Visual Studio 2017 Enterprise) is the *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* folder.</span></span>

<span data-ttu-id="135e5-113">`Microsoft.NET.Sdk.Web` SDK 依赖于：</span><span class="sxs-lookup"><span data-stu-id="135e5-113">The `Microsoft.NET.Sdk.Web` SDK depends on:</span></span>

* <span data-ttu-id="135e5-114">*Microsoft.NET.Sdk.Web.ProjectSystem*</span><span class="sxs-lookup"><span data-stu-id="135e5-114">*Microsoft.NET.Sdk.Web.ProjectSystem*</span></span>
* <span data-ttu-id="135e5-115">*Microsoft.NET.Sdk.Publish*</span><span class="sxs-lookup"><span data-stu-id="135e5-115">*Microsoft.NET.Sdk.Publish*</span></span>

<span data-ttu-id="135e5-116">它们会导致导入以下属性和目标：</span><span class="sxs-lookup"><span data-stu-id="135e5-116">Which causes the following properties and targets to be imported:</span></span>

* <span data-ttu-id="135e5-117">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="135e5-117">*$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props*</span></span>
* <span data-ttu-id="135e5-118">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="135e5-118">*$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets*</span></span>
* <span data-ttu-id="135e5-119">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="135e5-119">*$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props*</span></span>
* <span data-ttu-id="135e5-120">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="135e5-120">*$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets*</span></span>

<span data-ttu-id="135e5-121">发布目标将根据使用的发布方法，导入正确的目标集。</span><span class="sxs-lookup"><span data-stu-id="135e5-121">Publish targets import the right set of targets based on the publish method used.</span></span>

<span data-ttu-id="135e5-122">MSBuild 或 Visual Studio 加载项目时，执行下列高级别操作：</span><span class="sxs-lookup"><span data-stu-id="135e5-122">When MSBuild or Visual Studio loads a project, the following high-level actions occur:</span></span>

* <span data-ttu-id="135e5-123">生成项目</span><span class="sxs-lookup"><span data-stu-id="135e5-123">Build project</span></span>
* <span data-ttu-id="135e5-124">计算要发布的文件</span><span class="sxs-lookup"><span data-stu-id="135e5-124">Compute files to publish</span></span>
* <span data-ttu-id="135e5-125">将文件发布到目标</span><span class="sxs-lookup"><span data-stu-id="135e5-125">Publish files to destination</span></span>

## <a name="compute-project-items"></a><span data-ttu-id="135e5-126">计算项目项</span><span class="sxs-lookup"><span data-stu-id="135e5-126">Compute project items</span></span>

<span data-ttu-id="135e5-127">加载项目时，将计算项目项（文件）。</span><span class="sxs-lookup"><span data-stu-id="135e5-127">When the project is loaded, the project items (files) are computed.</span></span> <span data-ttu-id="135e5-128">`item type` 属性确定如何处理该文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-128">The `item type` attribute determines how the file is processed.</span></span> <span data-ttu-id="135e5-129">默认情况下，.cs 文件包含在 `Compile` 项列表内。</span><span class="sxs-lookup"><span data-stu-id="135e5-129">By default, *.cs* files are included in the `Compile` item list.</span></span> <span data-ttu-id="135e5-130">会对 `Compile` 项列表中的文件进行编译。</span><span class="sxs-lookup"><span data-stu-id="135e5-130">Files in the `Compile` item list are compiled.</span></span>

<span data-ttu-id="135e5-131">除了生成输出，`Content` 项列表还包含已发布的文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-131">The `Content` item list contains files that are published in addition to the build outputs.</span></span> <span data-ttu-id="135e5-132">默认情况下，匹配模式 `wwwroot/**` 的文件将包含在 `Content` 项内。</span><span class="sxs-lookup"><span data-stu-id="135e5-132">By default, files matching the pattern `wwwroot/**` are included in the `Content` item.</span></span> <span data-ttu-id="135e5-133">`wwwroot/\*\*` [glob 模式](https://gruntjs.com/configuring-tasks#globbing-patterns) 匹配 wwwroot 文件夹及其子文件夹中的所有文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-133">The `wwwroot/\*\*` [globbing pattern](https://gruntjs.com/configuring-tasks#globbing-patterns) matches all files in the *wwwroot* folder **and** subfolders.</span></span> <span data-ttu-id="135e5-134">若要将文件显式添加到发布列表，请直接在 .csproj 文件中添加文件，如[包含文件](#include-files)中所示。</span><span class="sxs-lookup"><span data-stu-id="135e5-134">To explicitly add a file to the publish list, add the file directly in the *.csproj* file as shown in [Include Files](#include-files).</span></span>

<span data-ttu-id="135e5-135">在 Visual Studio 中选择“发布”按钮时或从命令行发布时：</span><span class="sxs-lookup"><span data-stu-id="135e5-135">When selecting the **Publish** button in Visual Studio or when publishing from the command line:</span></span>

* <span data-ttu-id="135e5-136">计算属性/项目（需要生成的文件）。</span><span class="sxs-lookup"><span data-stu-id="135e5-136">The properties/items are computed (the files that are needed to build).</span></span>
* <span data-ttu-id="135e5-137">仅限 Visual Studio：还原 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="135e5-137">**Visual Studio only**: NuGet packages are restored.</span></span> <span data-ttu-id="135e5-138">（用户需要在 CLI 上执行显式还原。）</span><span class="sxs-lookup"><span data-stu-id="135e5-138">(Restore needs to be explicit by the user on the CLI.)</span></span>
* <span data-ttu-id="135e5-139">生成项目。</span><span class="sxs-lookup"><span data-stu-id="135e5-139">The project builds.</span></span>
* <span data-ttu-id="135e5-140">计算发布项（需要发布的文件）。</span><span class="sxs-lookup"><span data-stu-id="135e5-140">The publish items are computed (the files that are needed to publish).</span></span>
* <span data-ttu-id="135e5-141">文件已发布（计算的文件将被复制到发布目标）。</span><span class="sxs-lookup"><span data-stu-id="135e5-141">The project is published (the computed files are copied to the publish destination).</span></span>

<span data-ttu-id="135e5-142">当 ASP.NET Core 项目在项目文件中引用 `Microsoft.NET.Sdk.Web` 时，会将 app_offline.htm 文件放在 Web 应用目录的根目录下。</span><span class="sxs-lookup"><span data-stu-id="135e5-142">When an ASP.NET Core project references `Microsoft.NET.Sdk.Web` in the project file, an *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="135e5-143">该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-143">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="135e5-144">有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)。</span><span class="sxs-lookup"><span data-stu-id="135e5-144">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#app_offlinehtm).</span></span>

## <a name="basic-command-line-publishing"></a><span data-ttu-id="135e5-145">基本命令行发布</span><span class="sxs-lookup"><span data-stu-id="135e5-145">Basic command-line publishing</span></span>

<span data-ttu-id="135e5-146">命令行发布适用于所有支持 .NET Core 的平台，而且不需要 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="135e5-146">Command-line publishing works on all .NET Core-supported platforms and doesn't require Visual Studio.</span></span> <span data-ttu-id="135e5-147">在下面的示例中，从项目目录（其中包含 .csproj 文件）运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令。</span><span class="sxs-lookup"><span data-stu-id="135e5-147">In the samples below, the [dotnet publish](/dotnet/core/tools/dotnet-publish) command is run from the project directory (which contains the *.csproj* file).</span></span> <span data-ttu-id="135e5-148">如果不在项目文件夹中，则可以在项目文件路径中显式传递。</span><span class="sxs-lookup"><span data-stu-id="135e5-148">If not in the project folder, explicitly pass in the project file path.</span></span> <span data-ttu-id="135e5-149">例如:</span><span class="sxs-lookup"><span data-stu-id="135e5-149">For example:</span></span>

```console
dotnet publish C:\Webs\Web1
```

<span data-ttu-id="135e5-150">运行以下命令以创建并发布 Web 应用：</span><span class="sxs-lookup"><span data-stu-id="135e5-150">Run the following commands to create and publish a web app:</span></span>

::: moniker range=">= aspnetcore-2.0"

```console
dotnet new mvc
dotnet publish
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```console
dotnet new mvc
dotnet restore
dotnet publish
```

::: moniker-end

<span data-ttu-id="135e5-151">[dotnet publish](/dotnet/core/tools/dotnet-publish) 命令生成类似下面的输出：</span><span class="sxs-lookup"><span data-stu-id="135e5-151">The [dotnet publish](/dotnet/core/tools/dotnet-publish) command produces output similar to the following:</span></span>

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

<span data-ttu-id="135e5-152">默认发布文件夹为 `bin\$(Configuration)\netcoreapp<version>\publish`。</span><span class="sxs-lookup"><span data-stu-id="135e5-152">The default publish folder is `bin\$(Configuration)\netcoreapp<version>\publish`.</span></span> <span data-ttu-id="135e5-153">`$(Configuration)` 的默认值为 Debug。</span><span class="sxs-lookup"><span data-stu-id="135e5-153">The default for `$(Configuration)` is *Debug*.</span></span> <span data-ttu-id="135e5-154">在上述示例中，`<TargetFramework>` 是 `netcoreapp2.0`。</span><span class="sxs-lookup"><span data-stu-id="135e5-154">In the preceding sample, the `<TargetFramework>` is `netcoreapp2.0`.</span></span>

<span data-ttu-id="135e5-155">`dotnet publish -h` 显示用于发布的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="135e5-155">`dotnet publish -h` displays help information for publish.</span></span>

<span data-ttu-id="135e5-156">以下命令指定 `Release` 生成和发布目录：</span><span class="sxs-lookup"><span data-stu-id="135e5-156">The following command specifies a `Release` build and the publishing directory:</span></span>

```console
dotnet publish -c Release -o C:\MyWebs\test
```

<span data-ttu-id="135e5-157">[dotnet publish](/dotnet/core/tools/dotnet-publish) 命令调用 MSBuild，它调用 `Publish` 目标。</span><span class="sxs-lookup"><span data-stu-id="135e5-157">The [dotnet publish](/dotnet/core/tools/dotnet-publish) command calls MSBuild, which invokes the `Publish` target.</span></span> <span data-ttu-id="135e5-158">任何传递给 `dotnet publish` 的参数都将传递给 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="135e5-158">Any parameters passed to `dotnet publish` are passed to MSBuild.</span></span> <span data-ttu-id="135e5-159">`-c` 参数映射到 `Configuration` MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="135e5-159">The `-c` parameter maps to the `Configuration` MSBuild property.</span></span> <span data-ttu-id="135e5-160">`-o` 参数映射到 `OutputPath`。</span><span class="sxs-lookup"><span data-stu-id="135e5-160">The `-o` parameter maps to `OutputPath`.</span></span>

<span data-ttu-id="135e5-161">可以使用以下任一格式来传递 MSBuild 属性：</span><span class="sxs-lookup"><span data-stu-id="135e5-161">MSBuild properties can be passed using either of the following formats:</span></span>

* ` p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

<span data-ttu-id="135e5-162">以下命令将 `Release` 版本发布到网络共享：</span><span class="sxs-lookup"><span data-stu-id="135e5-162">The following command publishes a `Release` build to a network share:</span></span>

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

<span data-ttu-id="135e5-163">网络共享通过正斜杠指定 (//r8/) 并适用于所有支持 .NET Core 的平台。</span><span class="sxs-lookup"><span data-stu-id="135e5-163">The network share is specified with forward slashes (*//r8/*) and works on all .NET Core supported platforms.</span></span>

<span data-ttu-id="135e5-164">确认用于部署的发布应用未在运行。</span><span class="sxs-lookup"><span data-stu-id="135e5-164">Confirm that the published app for deployment isn't running.</span></span> <span data-ttu-id="135e5-165">如果应用正在运行，publish 文件夹中的文件会被锁定。</span><span class="sxs-lookup"><span data-stu-id="135e5-165">Files in the *publish* folder are locked when the app is running.</span></span> <span data-ttu-id="135e5-166">部署不会发生，因为无法复制锁定的文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-166">Deployment can't occur because locked files can't be copied.</span></span>

## <a name="publish-profiles"></a><span data-ttu-id="135e5-167">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="135e5-167">Publish profiles</span></span>

<span data-ttu-id="135e5-168">本部分使用 Visual Studio 2017 创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-168">This section uses Visual Studio 2017 to create a publishing profile.</span></span> <span data-ttu-id="135e5-169">创建后，可以从 Visual Studio 或命令行中发布。</span><span class="sxs-lookup"><span data-stu-id="135e5-169">Once created, publishing from Visual Studio or the command line is available.</span></span>

<span data-ttu-id="135e5-170">发布配置文件可以简化发布过程，并且可以存在任意数量的配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-170">Publish profiles can simplify the publishing process, and any number of profiles can exist.</span></span> <span data-ttu-id="135e5-171">通过选择以下路径之一在 Visual Studio 中创建发布配置文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-171">Create a publish profile in Visual Studio by choosing one of the following paths:</span></span>

* <span data-ttu-id="135e5-172">在解决方案资源管理器中右键单击该项目，然后选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="135e5-172">Right-click the project in Solution Explorer and select **Publish**.</span></span>
* <span data-ttu-id="135e5-173">可以从“生成”菜单中选择发布 &lt;project_name&gt;。</span><span class="sxs-lookup"><span data-stu-id="135e5-173">Select **Publish &lt;project_name&gt;** from the **Build** menu.</span></span>

<span data-ttu-id="135e5-174">随即显示应用程序容量页的“发布”选项卡。</span><span class="sxs-lookup"><span data-stu-id="135e5-174">The **Publish** tab of the app capacities page is displayed.</span></span> <span data-ttu-id="135e5-175">如果项目缺少发布配置文件，将显示以下页面：</span><span class="sxs-lookup"><span data-stu-id="135e5-175">If the project lacks a publish profile, the following page is displayed:</span></span>

![随即显示应用程序容量页的“发布”选项卡](visual-studio-publish-profiles/_static/az.png)

<span data-ttu-id="135e5-177">当选择“文件夹”时，指定一个文件夹路径来存储发布的资产。</span><span class="sxs-lookup"><span data-stu-id="135e5-177">When **Folder** is selected, specify a folder path to store the published assets.</span></span> <span data-ttu-id="135e5-178">默认文件夹是 bin\Release\PublishOutput。</span><span class="sxs-lookup"><span data-stu-id="135e5-178">The default folder is *bin\Release\PublishOutput*.</span></span> <span data-ttu-id="135e5-179">单击“创建配置文件”按钮即可完成。</span><span class="sxs-lookup"><span data-stu-id="135e5-179">Click the **Create Profile** button to finish.</span></span>

<span data-ttu-id="135e5-180">创建发布配置文件后，“发布”选项卡将更改。</span><span class="sxs-lookup"><span data-stu-id="135e5-180">Once a publish profile is created, the **Publish** tab changes.</span></span> <span data-ttu-id="135e5-181">新创建的配置文件显示在下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="135e5-181">The newly created profile appears in a drop-down list.</span></span> <span data-ttu-id="135e5-182">单击“创建新配置文件”以创建其他新配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-182">Click **Create new profile** to create another new profile.</span></span>

![显示 FolderProfile 的应用程序容量页的“发布”选项卡](visual-studio-publish-profiles/_static/create_new.png)

<span data-ttu-id="135e5-184">发布向导支持以下发布目标：</span><span class="sxs-lookup"><span data-stu-id="135e5-184">The Publish wizard supports the following publish targets:</span></span>

* <span data-ttu-id="135e5-185">Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="135e5-185">Azure App Service</span></span>
* <span data-ttu-id="135e5-186">Azure 虚拟机</span><span class="sxs-lookup"><span data-stu-id="135e5-186">Azure Virtual Machines</span></span>
* <span data-ttu-id="135e5-187">IIS、FTP 等（适用于任何 Web 服务器）</span><span class="sxs-lookup"><span data-stu-id="135e5-187">IIS, FTP, etc. (for any web server)</span></span>
* <span data-ttu-id="135e5-188">文件夹</span><span class="sxs-lookup"><span data-stu-id="135e5-188">Folder</span></span>
* <span data-ttu-id="135e5-189">导入配置文件</span><span class="sxs-lookup"><span data-stu-id="135e5-189">Import Profile</span></span>

<span data-ttu-id="135e5-190">有关详细信息，请参阅[哪些发布选项适合我](/visualstudio/ide/not-in-toc/web-publish-options)。</span><span class="sxs-lookup"><span data-stu-id="135e5-190">For more information, see [What publishing options are right for me](/visualstudio/ide/not-in-toc/web-publish-options).</span></span>

<span data-ttu-id="135e5-191">使用 Visual Studio 创建发布配置文件时，将创建 Properties/PublishProfiles/&lt;profile_name&gt;.pubxml MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-191">When creating a publish profile with Visual Studio, a *Properties/PublishProfiles/&lt;profile_name&gt;.pubxml* MSBuild file is created.</span></span> <span data-ttu-id="135e5-192">此 .pubxml 文件为 MSBuild 文件，包含发布配置设置。</span><span class="sxs-lookup"><span data-stu-id="135e5-192">The *.pubxml* file is a MSBuild file and contains publish configuration settings.</span></span> <span data-ttu-id="135e5-193">可以更改此文件以自定义生成和发布过程。</span><span class="sxs-lookup"><span data-stu-id="135e5-193">This file can be changed to customize the build and publish process.</span></span> <span data-ttu-id="135e5-194">通过发布过程读取此文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-194">This file is read by the publishing process.</span></span> <span data-ttu-id="135e5-195">`<LastUsedBuildConfiguration>` 比较特殊，因为它是一个全局属性，不应出现在导入生成的任何文件中。</span><span class="sxs-lookup"><span data-stu-id="135e5-195">`<LastUsedBuildConfiguration>` is special because it's a global property and shouldn't be in any file that's imported in the build.</span></span> <span data-ttu-id="135e5-196">有关详细信息，请参阅 [MSBuild：如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)。</span><span class="sxs-lookup"><span data-stu-id="135e5-196">See [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) for more information.</span></span>

<span data-ttu-id="135e5-197">发布到 Azure 目标时，.pubxml 文件包含 Azure 订阅标识符。</span><span class="sxs-lookup"><span data-stu-id="135e5-197">When publishing to an Azure target, the *.pubxml* file contains your Azure subscription identifier.</span></span> <span data-ttu-id="135e5-198">不建议使用该目标类型将此文件添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="135e5-198">With that target type, adding this file to source control is discouraged.</span></span> <span data-ttu-id="135e5-199">发布到非 Azure 目标时，签入 .pubxml 文件是安全的。</span><span class="sxs-lookup"><span data-stu-id="135e5-199">When publishing to a non-Azure target, it's safe to check in the *.pubxml* file.</span></span>

<span data-ttu-id="135e5-200">敏感信息（如发布密码）在每个用户/机器级别均进行加密。</span><span class="sxs-lookup"><span data-stu-id="135e5-200">Sensitive information (like the publish password) is encrypted on a per user/machine level.</span></span> <span data-ttu-id="135e5-201">它存储在 Properties/PublishProfiles/&lt;profile_name&gt;.pubxml.user 文件中。</span><span class="sxs-lookup"><span data-stu-id="135e5-201">It's stored in the *Properties/PublishProfiles/&lt;profile_name&gt;.pubxml.user* file.</span></span> <span data-ttu-id="135e5-202">由于此文件可以存储敏感信息，因此不应将其签入源代码管理。</span><span class="sxs-lookup"><span data-stu-id="135e5-202">Because this file can store sensitive information, it shouldn't be checked into source control.</span></span>

<span data-ttu-id="135e5-203">有关如何在 ASP.NET Core 上发布 Web 应用的概述，请参阅[托管和部署](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="135e5-203">For an overview of how to publish a web app on ASP.NET Core, see [Host and deploy](xref:host-and-deploy/index).</span></span> <span data-ttu-id="135e5-204">发布 ASP.NET Core 应用程序所需的 MSBuild 任务和目标是开放源代码，位于： https://github.com/aspnet/websdk。</span><span class="sxs-lookup"><span data-stu-id="135e5-204">The MSBuild tasks and targets necessary to publish an ASP.NET Core app are open-source at https://github.com/aspnet/websdk.</span></span>

<span data-ttu-id="135e5-205">`dotnet publish` 可以使用文件夹、MSDeploy 和 [Kudu](https://github.com/projectkudu/kudu/wiki) 发布配置文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-205">`dotnet publish` can use folder, MSDeploy, and [Kudu](https://github.com/projectkudu/kudu/wiki) publish profiles:</span></span>

<span data-ttu-id="135e5-206">文件夹（跨平台工作）：</span><span class="sxs-lookup"><span data-stu-id="135e5-206">Folder (works cross-platform):</span></span>

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>
```

<span data-ttu-id="135e5-207">MSDeploy（当前仅适用于 Windows，因为 MSDeploy 不是跨平台的）：</span><span class="sxs-lookup"><span data-stu-id="135e5-207">MSDeploy (currently this only works in Windows since MSDeploy isn't cross-platform):</span></span>

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

<span data-ttu-id="135e5-208">MSDeploy 包（当前仅适用于 Windows，因为 MSDeploy 不是跨平台的）：</span><span class="sxs-lookup"><span data-stu-id="135e5-208">MSDeploy package (currently this only works in Windows since MSDeploy isn't cross-platform):</span></span>

```console
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

<span data-ttu-id="135e5-209">在前面示例中，不会将 `deployonbuild` 传递到 `dotnet publish`。</span><span class="sxs-lookup"><span data-stu-id="135e5-209">In the preceding samples, **don't** pass `deployonbuild` to `dotnet publish`.</span></span>

<span data-ttu-id="135e5-210">有关详细信息，请参阅 [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)。</span><span class="sxs-lookup"><span data-stu-id="135e5-210">For more information, see [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish).</span></span>

<span data-ttu-id="135e5-211">`dotnet publish` 支持 Kudu API 从任何平台发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="135e5-211">`dotnet publish` supports Kudu APIs to publish to Azure from any platform.</span></span> <span data-ttu-id="135e5-212">Visual Studio 发布支持 Kudu API，但 WebSDK 支持其跨平台发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="135e5-212">Visual Studio publish supports the Kudu APIs, but it's supported by WebSDK for cross-platform publish to Azure.</span></span>

<span data-ttu-id="135e5-213">向“属性/发布配置文件”文件夹添加包含以下内容的发布配置文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-213">Add a publish profile to the *Properties/PublishProfiles* folder with the following content:</span></span>

```xml
<Project>
  <PropertyGroup>
    <PublishProtocol>Kudu</PublishProtocol>
    <PublishSiteName>nodewebapp</PublishSiteName>
    <UserName>username</UserName>
    <Password>password</Password>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="135e5-214">运行以下命令将会压缩发布内容并将其发布到使用 Kudu API 的 Azure：</span><span class="sxs-lookup"><span data-stu-id="135e5-214">Run the following command to zip up the publish contents and publish it to Azure using the Kudu APIs:</span></span>

```console
dotnet publish /p:PublishProfile=Azure /p:Configuration=Release
```

<span data-ttu-id="135e5-215">使用发布配置文件时，请设置以下 MSBuild 属性：</span><span class="sxs-lookup"><span data-stu-id="135e5-215">Set the following MSBuild properties when using a publish profile:</span></span>

* `DeployOnBuild=true`
* `PublishProfile=<Publish profile name>`

<span data-ttu-id="135e5-216">发布名为 FolderProfile 的配置文件时，可以执行以下命令之一：</span><span class="sxs-lookup"><span data-stu-id="135e5-216">When publishing with a profile named *FolderProfile*, either of the commands below can be executed:</span></span>

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

<span data-ttu-id="135e5-217">调用 [dotnet build](/dotnet/core/tools/dotnet-build) 时，它调用 `msbuild` 来运行生成和发布过程。</span><span class="sxs-lookup"><span data-stu-id="135e5-217">When invoking [dotnet build](/dotnet/core/tools/dotnet-build), it calls `msbuild` to run the build and publish process.</span></span> <span data-ttu-id="135e5-218">当传递到文件夹配置文件中时，调用 `dotnet build` 或 `msbuild` 的作用是相同的。</span><span class="sxs-lookup"><span data-stu-id="135e5-218">Calling either `dotnet build` or `msbuild` is equivalent when passing in a folder profile.</span></span> <span data-ttu-id="135e5-219">在 Windows 上直接调用 MSBuild 时，将使用 MSBuild 的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="135e5-219">When calling MSBuild directly on Windows, the .NET Framework version of MSBuild is used.</span></span> <span data-ttu-id="135e5-220">MSDeploy 目前仅限于在 Windows 计算机上进行发布。</span><span class="sxs-lookup"><span data-stu-id="135e5-220">MSDeploy is currently limited to Windows machines for publishing.</span></span> <span data-ttu-id="135e5-221">在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild，并且 MSBuild 在非文件夹配置文件上使用 MSDeploy。</span><span class="sxs-lookup"><span data-stu-id="135e5-221">Calling `dotnet build` on a non-folder profile invokes MSBuild, and MSBuild uses MSDeploy on non-folder profiles.</span></span> <span data-ttu-id="135e5-222">在非文件夹配置文件上调用 `dotnet build` 时，会调用 MSBuild（使用 MSDeploy）并导致失败（即使在 Windows 平台上运行也是如此）。</span><span class="sxs-lookup"><span data-stu-id="135e5-222">Calling `dotnet build` on a non-folder profile invokes MSBuild (using MSDeploy) and results in a failure (even when running on a Windows platform).</span></span> <span data-ttu-id="135e5-223">若要使用非文件夹配置文件进行发布，请直接调用 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="135e5-223">To publish with a non-folder profile, call MSBuild directly.</span></span>

<span data-ttu-id="135e5-224">以下文件夹发布配置文件通过 Visual Studio 创建，并被发布到网络共享：</span><span class="sxs-lookup"><span data-stu-id="135e5-224">The following folder publish profile was created with Visual Studio and publishes to a network share:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework>netcoreapp1.1</PublishFramework>
    <ProjectGuid>c30c453c-312e-40c4-aec9-394a145dee0b</ProjectGuid>
    <publishUrl>\\r8\Release\AdminWeb</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="135e5-225">请注意，`<LastUsedBuildConfiguration>` 已设置为 `Release`。</span><span class="sxs-lookup"><span data-stu-id="135e5-225">Note `<LastUsedBuildConfiguration>` is set to `Release`.</span></span> <span data-ttu-id="135e5-226">从 Visual Studio 发布时，在启动发布过程后将使用该值设置 `<LastUsedBuildConfiguration>` 配置属性值。</span><span class="sxs-lookup"><span data-stu-id="135e5-226">When publishing from Visual Studio, the `<LastUsedBuildConfiguration>` configuration property value is set using the value when the publish process is started.</span></span> <span data-ttu-id="135e5-227">`<LastUsedBuildConfiguration>` 配置属性比较特殊，不应在导入的 MSBuild 文件中覆盖该属性。</span><span class="sxs-lookup"><span data-stu-id="135e5-227">The `<LastUsedBuildConfiguration>` configuration property is special and shouldn't be overridden in an imported MSBuild file.</span></span> <span data-ttu-id="135e5-228">可以从命令行覆盖此属性。</span><span class="sxs-lookup"><span data-stu-id="135e5-228">This property can be overridden from the command line.</span></span>

<span data-ttu-id="135e5-229">使用 .NET Core CLI：</span><span class="sxs-lookup"><span data-stu-id="135e5-229">Using the .NET Core CLI:</span></span>

```console
dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

<span data-ttu-id="135e5-230">使用 MSBuild：</span><span class="sxs-lookup"><span data-stu-id="135e5-230">Using MSBuild:</span></span>

```console
msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile
```

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a><span data-ttu-id="135e5-231">从命令行发布到 MSDeploy 终结点</span><span class="sxs-lookup"><span data-stu-id="135e5-231">Publish to an MSDeploy endpoint from the command line</span></span>

<span data-ttu-id="135e5-232">可以使用 .NET Core CLI 或 MSBuild 完成发布。</span><span class="sxs-lookup"><span data-stu-id="135e5-232">Publishing can be accomplished using the .NET Core CLI or MSBuild.</span></span> <span data-ttu-id="135e5-233">`dotnet publish` 在 .NET Core 的上下文中运行。</span><span class="sxs-lookup"><span data-stu-id="135e5-233">`dotnet publish` runs in the context of .NET Core.</span></span> <span data-ttu-id="135e5-234">`msbuild` 命令需要 .NET Framework，它将该命令限制到 Windows 环境。</span><span class="sxs-lookup"><span data-stu-id="135e5-234">The `msbuild` command requires .NET Framework, which limits it to Windows environments.</span></span>

<span data-ttu-id="135e5-235">使用 MSDeploy 发布的最简单的方法是，首先在 Visual Studio 2017 中创建发布配置文件，然后从命令行中使用配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-235">The easiest way to publish with MSDeploy is to first create a publish profile in Visual Studio 2017 and use the profile from the command line.</span></span>

<span data-ttu-id="135e5-236">下面的示例中创建了一个 ASP.NET Core Web应用（使用 `dotnet new mvc`），并且通过 Visual Studio 添加了一个 Azure 发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-236">In the following sample, an ASP.NET Core web app is created (using `dotnet new mvc`), and an Azure publish profile is added with Visual Studio.</span></span>

<span data-ttu-id="135e5-237">从 VS 2017 开发人员命令提示符中运行 `msbuild`。</span><span class="sxs-lookup"><span data-stu-id="135e5-237">Run `msbuild` from a **Developer Command Prompt for VS 2017**.</span></span> <span data-ttu-id="135e5-238">开发人员命令提示符在其路径中将具有正确的 msbuild.exe，并会设置一些 MSBuild 变量。</span><span class="sxs-lookup"><span data-stu-id="135e5-238">The Developer Command Prompt has the correct *msbuild.exe* in its path with some MSBuild variables set.</span></span>

<span data-ttu-id="135e5-239">MSBuild 使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="135e5-239">MSBuild uses the following syntax:</span></span>

```console
msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile> /p:Username=<USERNAME> /p:Password=<PASSWORD>
```

<span data-ttu-id="135e5-240">可以从 \<Publish name>.PublishSettings 文件获取 `Password`。</span><span class="sxs-lookup"><span data-stu-id="135e5-240">Get the `Password` from the *\<Publish name>.PublishSettings* file.</span></span> <span data-ttu-id="135e5-241">可以从以下位置下载 .PublishSettings 文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-241">Download the *.PublishSettings* file from either:</span></span>

* <span data-ttu-id="135e5-242">解决方案资源管理器：右键单击 Web 应用并选择“下载发布配置文件”。</span><span class="sxs-lookup"><span data-stu-id="135e5-242">Solution Explorer: Right-click on the Web App and select **Download Publish Profile**.</span></span>
* <span data-ttu-id="135e5-243">Azure 门户：单击 Web 应用“概述”面板上的“获取发布配置文件”。</span><span class="sxs-lookup"><span data-stu-id="135e5-243">Azure portal: Click **Get publish profile** on the Web App's **Overview** panel.</span></span>

<span data-ttu-id="135e5-244">可在发布配置文件中找到 `Username`。</span><span class="sxs-lookup"><span data-stu-id="135e5-244">`Username` can be found in the publish profile.</span></span>

<span data-ttu-id="135e5-245">以下示例使用“Web11112 - Web 部署”发布配置文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-245">The following sample uses the *Web11112 - Web Deploy* publish profile:</span></span>

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="exclude-files"></a><span data-ttu-id="135e5-246">排除文件</span><span class="sxs-lookup"><span data-stu-id="135e5-246">Exclude files</span></span>

<span data-ttu-id="135e5-247">在发布 ASP.NET Core Web 应用时，生成项目和 wwwroot 文件夹的内容包括在内。</span><span class="sxs-lookup"><span data-stu-id="135e5-247">When publishing ASP.NET Core web apps, the build artifacts and contents of the *wwwroot* folder are included.</span></span> <span data-ttu-id="135e5-248">`msbuild` 支持[通配模式](https://gruntjs.com/configuring-tasks#globbing-patterns)。</span><span class="sxs-lookup"><span data-stu-id="135e5-248">`msbuild` supports [globbing patterns](https://gruntjs.com/configuring-tasks#globbing-patterns).</span></span> <span data-ttu-id="135e5-249">例如，以下 `<Content>` 元素将从 wwwroot/content 文件夹及其所有子文件夹中排除所有文本 (.txt) 文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-249">For example, the following `<Content>` element excludes all text (*.txt*) files from the *wwwroot/content* folder and all its subfolders.</span></span>

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="135e5-250">可以将上面的标记添加到发布配置文件或 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-250">The preceding markup can be added to a publish profile or the *.csproj* file.</span></span> <span data-ttu-id="135e5-251">添加到 .csproj 文件时，会将该规则添加到项目中的所有发布配置文件中。</span><span class="sxs-lookup"><span data-stu-id="135e5-251">When added to the *.csproj* file, the rule is added to all publish profiles in the project.</span></span>

<span data-ttu-id="135e5-252">以下 `<MsDeploySkipRules>` 元素排除 wwwroot/content 文件夹中的所有文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-252">The following `<MsDeploySkipRules>` element excludes all files from the *wwwroot/content* folder:</span></span>

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="135e5-253">`<MsDeploySkipRules>` 不会从部署站点删除跳过目标。</span><span class="sxs-lookup"><span data-stu-id="135e5-253">`<MsDeploySkipRules>` won't delete the *skip* targets from the deployment site.</span></span> <span data-ttu-id="135e5-254">从部署站点中删除 `<Content>` 目标文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="135e5-254">`<Content>` targeted files and folders are deleted from the deployment site.</span></span> <span data-ttu-id="135e5-255">例如，假设部署的 Web 应用具有以下文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-255">For example, suppose a deployed web app had the following files:</span></span>

* <span data-ttu-id="135e5-256">*Views/Home/About1.cshtml*</span><span class="sxs-lookup"><span data-stu-id="135e5-256">*Views/Home/About1.cshtml*</span></span>
* <span data-ttu-id="135e5-257">*Views/Home/About2.cshtml*</span><span class="sxs-lookup"><span data-stu-id="135e5-257">*Views/Home/About2.cshtml*</span></span>
* <span data-ttu-id="135e5-258">*Views/Home/About3.cshtml*</span><span class="sxs-lookup"><span data-stu-id="135e5-258">*Views/Home/About3.cshtml*</span></span>

<span data-ttu-id="135e5-259">如果添加了以下 `<MsDeploySkipRules>` 元素，则不会在部署站点上删除这些文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-259">If the following `<MsDeploySkipRules>` elements are added, those files wouldn't be deleted on the deployment site.</span></span>

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="135e5-260">之前的 `<MsDeploySkipRules>` 元素阻止部署跳过的文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-260">The preceding `<MsDeploySkipRules>` elements prevent the *skipped* files from being deployed.</span></span> <span data-ttu-id="135e5-261">一旦部署这些文件就不会删除它们。</span><span class="sxs-lookup"><span data-stu-id="135e5-261">It won't delete those files once they're deployed.</span></span>

<span data-ttu-id="135e5-262">以下 `<Content>` 元素将在部署站点中删除目标文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-262">The following `<Content>` element deletes the targeted files at the deployment site:</span></span>

```xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="135e5-263">使用具有上述 `<Content>` 元素的命令行部署可生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="135e5-263">Using command-line deployment with the preceding `<Content>` element yields the following output:</span></span>

```console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="include-files"></a><span data-ttu-id="135e5-264">包含文件</span><span class="sxs-lookup"><span data-stu-id="135e5-264">Include files</span></span>

<span data-ttu-id="135e5-265">以下标记将项目目录外的 images 文件夹包含到发布站点的 wwwroot/images 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="135e5-265">The following markup includes an *images* folder outside the project directory to the *wwwroot/images* folder of the publish site:</span></span>

```xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

<span data-ttu-id="135e5-266">可以将标记添加到 .csproj 文件或发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-266">The markup can be added to the *.csproj* file or the publish profile.</span></span> <span data-ttu-id="135e5-267">如果将其添加到 .csproj 文件，它会包含在项目的每个发布配置文件中。</span><span class="sxs-lookup"><span data-stu-id="135e5-267">If it's added to the *.csproj* file, it's included in each publish profile in the project.</span></span>

<span data-ttu-id="135e5-268">以下突出显示的标记显示如何：</span><span class="sxs-lookup"><span data-stu-id="135e5-268">The following highlighted markup shows how to:</span></span>

* <span data-ttu-id="135e5-269">将文件从项目外部复制到 wwwroot 文件夹。</span><span class="sxs-lookup"><span data-stu-id="135e5-269">Copy a file from outside the project into the *wwwroot* folder.</span></span>
* <span data-ttu-id="135e5-270">排除 wwwroot\Content 文件夹。</span><span class="sxs-lookup"><span data-stu-id="135e5-270">Exclude the *wwwroot\Content* folder.</span></span>
* <span data-ttu-id="135e5-271">排除 Views\Home\About2.cshtml。</span><span class="sxs-lookup"><span data-stu-id="135e5-271">Exclude *Views\Home\About2.cshtml*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework />
    <ProjectGuid>afa9f185-7ce0-4935-9da1-ab676229d68a</ProjectGuid>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
  <ItemGroup>
    <ResolvedFileToPublish Include="..\ReadMe2.MD">
      <RelativePath>wwwroot\ReadMe2.MD</RelativePath>
    </ResolvedFileToPublish>

    <Content Update="wwwroot\Content\**\*" CopyToPublishDirectory="Never" />
    <Content Update="Views\Home\About2.cshtml" CopyToPublishDirectory="Never" />

  </ItemGroup>
</Project>
```

<span data-ttu-id="135e5-272">请参阅 [WebSDK 自述文件](https://github.com/aspnet/websdk)，了解更多部署示例。</span><span class="sxs-lookup"><span data-stu-id="135e5-272">See the [WebSDK Readme](https://github.com/aspnet/websdk) for more deployment samples.</span></span>

## <a name="run-a-target-before-or-after-publishing"></a><span data-ttu-id="135e5-273">在发布前或发布后运行目标</span><span class="sxs-lookup"><span data-stu-id="135e5-273">Run a target before or after publishing</span></span>

<span data-ttu-id="135e5-274">内置 `BeforePublish` 和 `AfterPublish` 目标在发布目标前/后执行目标。</span><span class="sxs-lookup"><span data-stu-id="135e5-274">The built-in `BeforePublish` and `AfterPublish` targets execute a target before or after the publish target.</span></span> <span data-ttu-id="135e5-275">将以下元素添加到发布配置文件，以在发布前/后均记录控制台消息：</span><span class="sxs-lookup"><span data-stu-id="135e5-275">Add the following elements to the publish profile to log console messages both before and after publishing:</span></span>

```xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="publish-to-a-server-using-an-untrusted-certificate"></a><span data-ttu-id="135e5-276">使用不受信任的证书发布到服务器</span><span class="sxs-lookup"><span data-stu-id="135e5-276">Publish to a server using an untrusted certificate</span></span>

<span data-ttu-id="135e5-277">将值为 `True` 的 `<AllowUntrustedCertificate>` 属性添加到发布配置文件：</span><span class="sxs-lookup"><span data-stu-id="135e5-277">Add the `<AllowUntrustedCertificate>` property with a value of `True` to the publish profile:</span></span>

```xml
<PropertyGroup>
  <AllowUntrustedCertificate>True</AllowUntrustedCertificate>
</PropertyGroup>
```

## <a name="the-kudu-service"></a><span data-ttu-id="135e5-278">Kudu 服务</span><span class="sxs-lookup"><span data-stu-id="135e5-278">The Kudu service</span></span>

<span data-ttu-id="135e5-279">要查看 Azure 应用服务 Web 应用部署中的文件，请使用 [Kudu 服务](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)。</span><span class="sxs-lookup"><span data-stu-id="135e5-279">To view the files in an Azure App Service web app deployment, use the [Kudu service](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service).</span></span> <span data-ttu-id="135e5-280">将 `scm` 令牌追加到 Web 应用名称。</span><span class="sxs-lookup"><span data-stu-id="135e5-280">Append the `scm` token to the web app name.</span></span> <span data-ttu-id="135e5-281">例如:</span><span class="sxs-lookup"><span data-stu-id="135e5-281">For example:</span></span>

| <span data-ttu-id="135e5-282">URL</span><span class="sxs-lookup"><span data-stu-id="135e5-282">URL</span></span>                                    | <span data-ttu-id="135e5-283">结果</span><span class="sxs-lookup"><span data-stu-id="135e5-283">Result</span></span>       |
| -------------------------------------- | ------------ |
| `http://mysite.azurewebsites.net/`     | <span data-ttu-id="135e5-284">Web 应用</span><span class="sxs-lookup"><span data-stu-id="135e5-284">Web App</span></span>      |
| `http://mysite.scm.azurewebsites.net/` | <span data-ttu-id="135e5-285">Kudu 服务</span><span class="sxs-lookup"><span data-stu-id="135e5-285">Kudu service</span></span> |

<span data-ttu-id="135e5-286">选择[调试控制台](https://github.com/projectkudu/kudu/wiki/Kudu-console)菜单项来查看、编辑、删除或添加文件。</span><span class="sxs-lookup"><span data-stu-id="135e5-286">Select the [Debug Console](https://github.com/projectkudu/kudu/wiki/Kudu-console) menu item to view, edit, delete, or add files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="135e5-287">其他资源</span><span class="sxs-lookup"><span data-stu-id="135e5-287">Additional resources</span></span>

* <span data-ttu-id="135e5-288">[Web 部署](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy) 简化了 Web 应用和网站到 IIS 服务器的部署。</span><span class="sxs-lookup"><span data-stu-id="135e5-288">[Web Deploy](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy) simplifies deployment of web apps and websites to IIS servers.</span></span>
* <span data-ttu-id="135e5-289">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues)：文件问题和部署的请求功能。</span><span class="sxs-lookup"><span data-stu-id="135e5-289">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): File issues and request features for deployment.</span></span>
* [<span data-ttu-id="135e5-290">从 Visual Studio 将 ASP.NET Web 应用发布到 Azure VM</span><span class="sxs-lookup"><span data-stu-id="135e5-290">Publish an ASP.NET Web App to an Azure VM from Visual Studio</span></span>](/azure/virtual-machines/windows/publish-web-app-from-visual-studio)
