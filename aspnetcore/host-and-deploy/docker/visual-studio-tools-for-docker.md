---
title: "使用 ASP.NET Core 的 Visual Studio Tools for Docker"
author: spboyer
description: "了解如何使用 Visual Studio 2017 工具和 Docker for Windows 来容器化 ASP.NET Core 应用。"
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/12/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: caf0e423d8e6f61fd2470d1f4ea2dd93909c3696
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a><span data-ttu-id="77e66-103">使用 ASP.NET Core 的 Visual Studio Tools for Docker</span><span class="sxs-lookup"><span data-stu-id="77e66-103">Visual Studio Tools for Docker with ASP.NET Core</span></span>

<span data-ttu-id="77e66-104">[Visual Studio 2017](https://www.visualstudio.com/) 支持生成、调试和运行面向的 .NET Framework 或 .NET Core 的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="77e66-104">[Visual Studio 2017](https://www.visualstudio.com/) supports building, debugging, and running ASP.NET Core apps targeting either .NET Framework or .NET Core.</span></span> <span data-ttu-id="77e66-105">Windows 和 Linux 容器均受支持。</span><span class="sxs-lookup"><span data-stu-id="77e66-105">Both Windows and Linux containers are supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77e66-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="77e66-106">Prerequisites</span></span>

* <span data-ttu-id="77e66-107">具有“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="77e66-107">[Visual Studio 2017](https://www.visualstudio.com/) with the **.NET Core cross-platform development** workload</span></span>
* [<span data-ttu-id="77e66-108">Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="77e66-108">Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/install/)

## <a name="installation-and-setup"></a><span data-ttu-id="77e66-109">安装和设置</span><span class="sxs-lookup"><span data-stu-id="77e66-109">Installation and setup</span></span>

<span data-ttu-id="77e66-110">要安装 Docker，请查看 [Docker for Windows：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息，并安装 [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)。</span><span class="sxs-lookup"><span data-stu-id="77e66-110">For Docker installation, review the information at [Docker for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install) and install [Docker For Windows](https://docs.docker.com/docker-for-windows/install/).</span></span>

<span data-ttu-id="77e66-111">Docker for Windows 中的[共享驱动器](https://docs.docker.com/docker-for-windows/#shared-drives)必须配置为支持卷映射和调试。</span><span class="sxs-lookup"><span data-stu-id="77e66-111">**[Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)** in Docker for Windows must be configured to support volume mapping and debugging.</span></span> <span data-ttu-id="77e66-112">右键单击系统托盘 Docker 图标，选择**设置...**，然后选择**共享驱动器**。</span><span class="sxs-lookup"><span data-stu-id="77e66-112">Right-click the System Tray's Docker icon, select **Settings...**, and select **Shared Drives**.</span></span> <span data-ttu-id="77e66-113">选择 Docker 其中存储文件的驱动器。</span><span class="sxs-lookup"><span data-stu-id="77e66-113">Select the drive where Docker stores files.</span></span> <span data-ttu-id="77e66-114">选择**应用**。</span><span class="sxs-lookup"><span data-stu-id="77e66-114">Select **Apply**.</span></span>

![Shared Drives](./visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> <span data-ttu-id="77e66-116">Visual Studio 2017 版本 15.6 及更高版本时提示**共享驱动器**未配置。</span><span class="sxs-lookup"><span data-stu-id="77e66-116">Visual Studio 2017 versions 15.6 and later prompt when **Shared Drives** aren't configured.</span></span>

## <a name="add-docker-support-to-an-app"></a><span data-ttu-id="77e66-117">向应用添加 Docker 支持</span><span class="sxs-lookup"><span data-stu-id="77e66-117">Add Docker support to an app</span></span>

<span data-ttu-id="77e66-118">支持的容器类型由 ASP.NET Core 项目的目标框架确定。</span><span class="sxs-lookup"><span data-stu-id="77e66-118">The ASP.NET Core project's target framework determines the supported container types.</span></span> <span data-ttu-id="77e66-119">面向 .NET Core 的项目同时支持 Linux 和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="77e66-119">Projects targeting .NET Core support both Linux and Windows containers.</span></span> <span data-ttu-id="77e66-120">面向 .NET Framework 的项目仅支持 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="77e66-120">Projects targeting .NET Framework only support Windows containers.</span></span>

<span data-ttu-id="77e66-121">当将 Docker 支持添加到项目中，选择 Windows 或 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="77e66-121">When adding Docker support to a project, choose either a Windows or a Linux container.</span></span> <span data-ttu-id="77e66-122">Docker 主机必须运行类型相同的容器。</span><span class="sxs-lookup"><span data-stu-id="77e66-122">The Docker host must be running the same container type.</span></span> <span data-ttu-id="77e66-123">要更改正在运行的 Docker 实例中的容器类型，请右键单击系统托盘中的 Docker 图标，再选择“切换到 Windows 容器...”或“切换到 Linux 容器...”。</span><span class="sxs-lookup"><span data-stu-id="77e66-123">To change the container type in the running Docker instance, right-click the System Tray's Docker icon and choose **Switch to Windows containers...** or **Switch to Linux containers...**.</span></span>

### <a name="new-app"></a><span data-ttu-id="77e66-124">新应用</span><span class="sxs-lookup"><span data-stu-id="77e66-124">New app</span></span>

<span data-ttu-id="77e66-125">使用 ASP.NET Core Web 应用程序项目模板创建新应用时，请选中“启用 Docker 支持”复选框：</span><span class="sxs-lookup"><span data-stu-id="77e66-125">When creating a new app with the **ASP.NET Core Web Application** project templates, select the **Enable Docker Support** checkbox:</span></span>

![“启用 Docker 支持”复选框](visual-studio-tools-for-docker/_static/enable-docker-support-checkbox.png)

<span data-ttu-id="77e66-127">如果目标框架是.NET 核心**OS**下拉列表允许针对选择的容器类型。</span><span class="sxs-lookup"><span data-stu-id="77e66-127">If the target framework is .NET Core, the **OS** drop-down allows for the selection of a container type.</span></span>

### <a name="existing-app"></a><span data-ttu-id="77e66-128">现有应用</span><span class="sxs-lookup"><span data-stu-id="77e66-128">Existing app</span></span>

<span data-ttu-id="77e66-129">Visual Studio Tools for Docker 不支持向面向.NET Framework 的现有 ASP.NET Core 项目添加 Docker。</span><span class="sxs-lookup"><span data-stu-id="77e66-129">The Visual Studio Tools for Docker don't support adding Docker to an existing ASP.NET Core project targeting .NET Framework.</span></span> <span data-ttu-id="77e66-130">对于面向 .NET Core 的 ASP.NET Core 项目，可通过两个选项使用工具添加 Docker 支持。</span><span class="sxs-lookup"><span data-stu-id="77e66-130">For ASP.NET Core projects targeting .NET Core, there are two options for adding Docker support via the tooling.</span></span> <span data-ttu-id="77e66-131">在 Visual Studio 中打开项目，然后选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="77e66-131">Open the project in Visual Studio, and choose one of the following options:</span></span>

* <span data-ttu-id="77e66-132">从“项目”菜单中选择“Docker 支持”。</span><span class="sxs-lookup"><span data-stu-id="77e66-132">Select **Docker Support** from the **Project** menu.</span></span>
* <span data-ttu-id="77e66-133">右键单击解决方案资源管理器中的项目，然后选择“添加” > “Docker 支持”。</span><span class="sxs-lookup"><span data-stu-id="77e66-133">Right-click the project in Solution Explorer and select **Add** > **Docker Support**.</span></span>

## <a name="docker-assets-overview"></a><span data-ttu-id="77e66-134">Docker 资产概述</span><span class="sxs-lookup"><span data-stu-id="77e66-134">Docker assets overview</span></span>

<span data-ttu-id="77e66-135">Visual Studio Tools for Docker 向解决方案中添加 docker-compose 项目，包括以下各项：</span><span class="sxs-lookup"><span data-stu-id="77e66-135">The Visual Studio Tools for Docker add a *docker-compose* project to the solution, containing the following:</span></span>

* <span data-ttu-id="77e66-136">.dockerignore：包含文件和目录模式的列表，排除生成生成上下文的时间。</span><span class="sxs-lookup"><span data-stu-id="77e66-136">*.dockerignore*: Contains a list of file and directory patterns to exclude when generating a build context.</span></span>
* <span data-ttu-id="77e66-137">docker-compose.yml：基本 [Docker Compose](https://docs.docker.com/compose/overview/) 文件，用于定义要分别通过 `docker-compose build` 和 `docker-compose run` 生成和运行的映像集合。</span><span class="sxs-lookup"><span data-stu-id="77e66-137">*docker-compose.yml*: The base [Docker Compose](https://docs.docker.com/compose/overview/) file used to define the collection of images to be built and run with `docker-compose build` and `docker-compose run`, respectively.</span></span>
* <span data-ttu-id="77e66-138">docker compose.override.yml：一个可选文件，通过 Docker Compose 读取，包含服务的配置替代。</span><span class="sxs-lookup"><span data-stu-id="77e66-138">*docker-compose.override.yml*: An optional file, read by Docker Compose, containing configuration overrides for services.</span></span> <span data-ttu-id="77e66-139">Visual Studio 执行 `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` 以合并这些文件。</span><span class="sxs-lookup"><span data-stu-id="77e66-139">Visual Studio executes `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` to merge these files.</span></span>

<span data-ttu-id="77e66-140">Dockerfile，用作创建最终 Docker 映像的方案，添加到项目根目录。</span><span class="sxs-lookup"><span data-stu-id="77e66-140">A *Dockerfile*, the recipe for creating a final Docker image, is added to the project root.</span></span> <span data-ttu-id="77e66-141">请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令。</span><span class="sxs-lookup"><span data-stu-id="77e66-141">Refer to [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for an understanding of the commands within it.</span></span> <span data-ttu-id="77e66-142">此特定 Dockerfile 使用[多阶段生成](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)，该生成包含四个不同的命名生成阶段：</span><span class="sxs-lookup"><span data-stu-id="77e66-142">This particular *Dockerfile* uses a [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) containing four distinct, named build stages:</span></span>

[!code-text[](visual-studio-tools-for-docker/samples/HelloDockerTools/HelloDockerTools/Dockerfile?highlight=1,5,14,17)]

<span data-ttu-id="77e66-143">Dockerfile 基于 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) 映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-143">The *Dockerfile* is based on the [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) image.</span></span> <span data-ttu-id="77e66-144">此基础映像包括 ASP.NET Core NuGet 包，已对此包进行了预实时编译，以提高启动性能。</span><span class="sxs-lookup"><span data-stu-id="77e66-144">This base image includes the ASP.NET Core NuGet packages, which have been pre-jitted to improve startup performance.</span></span>

<span data-ttu-id="77e66-145">*Docker-compose.yml*文件包含的项目运行时创建的映像的名称：</span><span class="sxs-lookup"><span data-stu-id="77e66-145">The *docker-compose.yml* file contains the name of the image that's created when the project runs:</span></span>

[!code-yaml[](visual-studio-tools-for-docker/samples/HelloDockerTools/docker-compose.yml?highlight=5)]

<span data-ttu-id="77e66-146">在前面的示例中，应用在“调试”模式下运行时，`image: hellodockertools` 生成映像 `hellodockertools:dev`。</span><span class="sxs-lookup"><span data-stu-id="77e66-146">In the preceding example, `image: hellodockertools` generates the image `hellodockertools:dev` when the app runs in **Debug** mode.</span></span> <span data-ttu-id="77e66-147">应用在“发布”模式下运行时，生成 `hellodockertools:latest` 映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-147">The `hellodockertools:latest` image is generated when the app runs in **Release** mode.</span></span>

<span data-ttu-id="77e66-148">映像名称加上前缀[Docker Hub](https://hub.docker.com/)用户名 (例如， `dockerhubusername/hellodockertools`) 如果该图像将推送到注册表。</span><span class="sxs-lookup"><span data-stu-id="77e66-148">Prefix the image name with the [Docker Hub](https://hub.docker.com/) username (for example, `dockerhubusername/hellodockertools`) if the image will be pushed to the registry.</span></span> <span data-ttu-id="77e66-149">或者，更改要包括私有注册表 URL 的映像名称 (例如， `privateregistry.domain.com/hellodockertools`) 根据配置。</span><span class="sxs-lookup"><span data-stu-id="77e66-149">Alternatively, change the image name to include the private registry URL (for example, `privateregistry.domain.com/hellodockertools`) depending on the configuration.</span></span>

## <a name="debug"></a><span data-ttu-id="77e66-150">调试</span><span class="sxs-lookup"><span data-stu-id="77e66-150">Debug</span></span>

<span data-ttu-id="77e66-151">在工具栏的调试下拉列表中选择“Docker”，然后开始调试应用。</span><span class="sxs-lookup"><span data-stu-id="77e66-151">Select **Docker** from the debug drop-down in the toolbar, and start debugging the app.</span></span> <span data-ttu-id="77e66-152">“输出”窗口的“Docker”视图显示发生的以下操作：</span><span class="sxs-lookup"><span data-stu-id="77e66-152">The **Docker** view of the **Output** window shows the following actions taking place:</span></span>

* <span data-ttu-id="77e66-153">*Microsoft/aspnetcore* （如果尚未在缓存中） 获取运行时映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-153">The *microsoft/aspnetcore* runtime image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="77e66-154">*Microsoft/aspnetcore-生成*  /发布编译的映像 （如果尚未在缓存中） 获取。</span><span class="sxs-lookup"><span data-stu-id="77e66-154">The *microsoft/aspnetcore-build* compile/publish image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="77e66-155">ASPNETCORE_ENVIRONMENT 环境变量设置为位于 `Development` 容器内。</span><span class="sxs-lookup"><span data-stu-id="77e66-155">The *ASPNETCORE_ENVIRONMENT* environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="77e66-156">已公开端口 80，并已映射为 localhost 动态分配的端口。</span><span class="sxs-lookup"><span data-stu-id="77e66-156">Port 80 is exposed and mapped to a dynamically-assigned port for localhost.</span></span> <span data-ttu-id="77e66-157">该端口由 Docker 主机确定，并且可以使用 `docker ps` 进行查询。</span><span class="sxs-lookup"><span data-stu-id="77e66-157">The port is determined by the Docker host and can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="77e66-158">应用程序复制到容器。</span><span class="sxs-lookup"><span data-stu-id="77e66-158">The app is copied to the container.</span></span>
* <span data-ttu-id="77e66-159">使用调试程序附加到使用动态分配端口容器启动默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="77e66-159">The default browser is launched with the debugger attached to the container using the dynamically-assigned port.</span></span> 

<span data-ttu-id="77e66-160">生成的 Docker 映像是*开发人员*使用应用程序的映像*microsoft/aspnetcore*作为基本映像的映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-160">The resulting Docker image is the *dev* image of the app with the *microsoft/aspnetcore* images as the base image.</span></span> <span data-ttu-id="77e66-161">在“包管理器控制台”(PMC) 窗口中运行 `docker images` 命令。</span><span class="sxs-lookup"><span data-stu-id="77e66-161">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="77e66-162">显示计算机上的映像：</span><span class="sxs-lookup"><span data-stu-id="77e66-162">The images on the machine are displayed:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                f8f9d6c923e2        About an hour ago   391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        15 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="77e66-163">开发人员映像作为缺少的应用程序内容，**调试**配置使用卷装载提供迭代的体验。</span><span class="sxs-lookup"><span data-stu-id="77e66-163">The dev image lacks the app contents, as **Debug** configurations use volume mounting to provide the iterative experience.</span></span> <span data-ttu-id="77e66-164">要推送映像，请使用“发布”配置。</span><span class="sxs-lookup"><span data-stu-id="77e66-164">To push an image, use the **Release** configuration.</span></span>

<span data-ttu-id="77e66-165">在 PMC 中运行 `docker ps` 命令。</span><span class="sxs-lookup"><span data-stu-id="77e66-165">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="77e66-166">请注意，应用使用容器运行：</span><span class="sxs-lookup"><span data-stu-id="77e66-166">Notice the app is running using the container:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a><span data-ttu-id="77e66-167">编辑并继续</span><span class="sxs-lookup"><span data-stu-id="77e66-167">Edit and continue</span></span>

<span data-ttu-id="77e66-168">对静态文件和 Razor 视图的更改会自动更新，无需执行编译步骤。</span><span class="sxs-lookup"><span data-stu-id="77e66-168">Changes to static files and Razor views are automatically updated without the need for a compilation step.</span></span> <span data-ttu-id="77e66-169">进行更改，保存并在浏览器中刷新，以查看更新。</span><span class="sxs-lookup"><span data-stu-id="77e66-169">Make the change, save, and refresh the browser to view the update.</span></span>  

<span data-ttu-id="77e66-170">对代码文件进行修改需要在容器内进行编译和重启 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="77e66-170">Modifications to code files requires compiling and a restart of Kestrel within the container.</span></span> <span data-ttu-id="77e66-171">更改后，使用 CTRL+F5 执行该过程并在容器内启动应用。</span><span class="sxs-lookup"><span data-stu-id="77e66-171">After making the change, use CTRL + F5 to perform the process and start the app within the container.</span></span> <span data-ttu-id="77e66-172">Docker 容器不重新生成或停止。</span><span class="sxs-lookup"><span data-stu-id="77e66-172">The Docker container isn't rebuilt or stopped.</span></span> <span data-ttu-id="77e66-173">在 PMC 中运行 `docker ps` 命令。</span><span class="sxs-lookup"><span data-stu-id="77e66-173">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="77e66-174">请注意，截至 10 分钟前，原始容器仍在运行：</span><span class="sxs-lookup"><span data-stu-id="77e66-174">Notice the original container is still running as of 10 minutes ago:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a><span data-ttu-id="77e66-175">发布 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="77e66-175">Publish Docker images</span></span>

<span data-ttu-id="77e66-176">应用程序的开发和调试周期完成后，Visual Studio Tools for Docker 帮助创建应用程序的生产映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-176">Once the develop and debug cycle of the app is completed, the Visual Studio Tools for Docker assist in creating the production image of the app.</span></span> <span data-ttu-id="77e66-177">将配置下拉列表更改为“发布”，然后生成应用。</span><span class="sxs-lookup"><span data-stu-id="77e66-177">Change the configuration drop-down to **Release** and build the app.</span></span> <span data-ttu-id="77e66-178">此工具生成的映像*最新*标记，可以推送到的私有注册表或 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="77e66-178">The tooling produces the image with the *latest* tag, which can be pushed to the private registry or Docker Hub.</span></span> 

<span data-ttu-id="77e66-179">在 PMC 中运行 `docker images` 命令，查看映像列表：</span><span class="sxs-lookup"><span data-stu-id="77e66-179">Run the `docker images` command in PMC to see the list of images:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                4cb1fca533f0        19 seconds ago      391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        16 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="77e66-180">`docker images` 命令返回存储库名称和标记标识为 \<none> （上面未列出）的中间映像。</span><span class="sxs-lookup"><span data-stu-id="77e66-180">The `docker images` command returns intermediary images with repository names and tags identified as *\<none>* (not listed above).</span></span> <span data-ttu-id="77e66-181">这些未命名映像由[多阶段生成](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile* 生成。</span><span class="sxs-lookup"><span data-stu-id="77e66-181">These unnamed images are produced by the [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*.</span></span> <span data-ttu-id="77e66-182">它们可提高生成最终映像的效率 &mdash; 发生更改时，仅重新生成必要的层。</span><span class="sxs-lookup"><span data-stu-id="77e66-182">They improve the efficiency of building the final image&mdash;only the necessary layers are rebuilt when changes occur.</span></span> <span data-ttu-id="77e66-183">当不再需要中间的图像时，则删除它们使用[docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/)命令。</span><span class="sxs-lookup"><span data-stu-id="77e66-183">When the intermediary images are no longer needed, delete them using the [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) command.</span></span>

<span data-ttu-id="77e66-184">可能希望生产或发布映像的大小比开发映像小。</span><span class="sxs-lookup"><span data-stu-id="77e66-184">There may be an expectation for the production or release image to be smaller in size by comparison to the *dev* image.</span></span> <span data-ttu-id="77e66-185">由于卷映射中，调试器和应用程序已运行从本地计算机和不在容器内。</span><span class="sxs-lookup"><span data-stu-id="77e66-185">Because of the volume mapping, the debugger and app were running from the local machine and not within the container.</span></span> <span data-ttu-id="77e66-186">最新映像已打包必要的应用代码，以在主机上运行应用。</span><span class="sxs-lookup"><span data-stu-id="77e66-186">The *latest* image has packaged the necessary app code to run the app on a host machine.</span></span> <span data-ttu-id="77e66-187">因此，增量是应用程序代码的大小。</span><span class="sxs-lookup"><span data-stu-id="77e66-187">Therefore, the delta is the size of the app code.</span></span>
