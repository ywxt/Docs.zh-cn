---
title: 使用 ASP.NET Core 的 Visual Studio Tools for Docker
author: spboyer
description: 了解如何使用 Visual Studio 2017 工具和 Docker for Windows 来容器化 ASP.NET Core 应用。
ms.author: scaddie
ms.custom: mvc
ms.date: 07/18/2018
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: afa7b05820ba021c50d9c23804095f7edd8b71f1
ms.sourcegitcommit: ee2b26c7d08b38c908c668522554b52ab8efa221
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2018
ms.locfileid: "39146879"
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a><span data-ttu-id="7e891-103">使用 ASP.NET Core 的 Visual Studio Tools for Docker</span><span class="sxs-lookup"><span data-stu-id="7e891-103">Visual Studio Tools for Docker with ASP.NET Core</span></span>

<span data-ttu-id="7e891-104">[Visual Studio 2017](https://www.visualstudio.com/) 支持生成、调试和运行面向 .NET Core 的容器化 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="7e891-104">[Visual Studio 2017](https://www.visualstudio.com/) supports building, debugging, and running containerized ASP.NET Core apps targeting .NET Core.</span></span> <span data-ttu-id="7e891-105">Windows 和 Linux 容器均受支持。</span><span class="sxs-lookup"><span data-stu-id="7e891-105">Both Windows and Linux containers are supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e891-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="7e891-106">Prerequisites</span></span>

* <span data-ttu-id="7e891-107">具有“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="7e891-107">[Visual Studio 2017](https://www.visualstudio.com/) with the **.NET Core cross-platform development** workload</span></span>
* [<span data-ttu-id="7e891-108">Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="7e891-108">Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/install/)

## <a name="installation-and-setup"></a><span data-ttu-id="7e891-109">安装和设置</span><span class="sxs-lookup"><span data-stu-id="7e891-109">Installation and setup</span></span>

<span data-ttu-id="7e891-110">要安装 Docker，请查看 [Docker for Windows：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息，并安装 [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)。</span><span class="sxs-lookup"><span data-stu-id="7e891-110">For Docker installation, review the information at [Docker for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install) and install [Docker For Windows](https://docs.docker.com/docker-for-windows/install/).</span></span>

<span data-ttu-id="7e891-111">Docker for Windows 中的[共享驱动器](https://docs.docker.com/docker-for-windows/#shared-drives)必须配置为支持卷映射和调试。</span><span class="sxs-lookup"><span data-stu-id="7e891-111">**[Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)** in Docker for Windows must be configured to support volume mapping and debugging.</span></span> <span data-ttu-id="7e891-112">右键单击系统托盘中的 Docker 图标，单击“设置...”，再选择“共享驱动器”。</span><span class="sxs-lookup"><span data-stu-id="7e891-112">Right-click the System Tray's Docker icon, select **Settings...**, and select **Shared Drives**.</span></span> <span data-ttu-id="7e891-113">选择 Docker 存储文件的驱动器。</span><span class="sxs-lookup"><span data-stu-id="7e891-113">Select the drive where Docker stores files.</span></span> <span data-ttu-id="7e891-114">选择“应用”。</span><span class="sxs-lookup"><span data-stu-id="7e891-114">Select **Apply**.</span></span>

![Shared Drives](./visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> <span data-ttu-id="7e891-116">未配置共享驱动器时，Visual Studio 2017 15.6 及更高版本会发出提示。</span><span class="sxs-lookup"><span data-stu-id="7e891-116">Visual Studio 2017 versions 15.6 and later prompt when **Shared Drives** aren't configured.</span></span>

## <a name="add-docker-support-to-an-app"></a><span data-ttu-id="7e891-117">向应用添加 Docker 支持</span><span class="sxs-lookup"><span data-stu-id="7e891-117">Add Docker support to an app</span></span>

<span data-ttu-id="7e891-118">若要向 ASP.NET Core 项目添加 Docker 支持，项目必须定目标到 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="7e891-118">To add Docker support to an ASP.NET Core project, the project must target .NET Core.</span></span> <span data-ttu-id="7e891-119">同时支持 Linux 和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="7e891-119">Both Linux and Windows containers are supported.</span></span>

<span data-ttu-id="7e891-120">向项目添加 Docker 支持后，可选择 Windows 或 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="7e891-120">When adding Docker support to a project, choose either a Windows or a Linux container.</span></span> <span data-ttu-id="7e891-121">Docker 主机必须运行类型相同的容器。</span><span class="sxs-lookup"><span data-stu-id="7e891-121">The Docker host must be running the same container type.</span></span> <span data-ttu-id="7e891-122">要更改正在运行的 Docker 实例中的容器类型，请右键单击系统托盘中的 Docker 图标，再选择“切换到 Windows 容器...”或“切换到 Linux 容器...”。</span><span class="sxs-lookup"><span data-stu-id="7e891-122">To change the container type in the running Docker instance, right-click the System Tray's Docker icon and choose **Switch to Windows containers...** or **Switch to Linux containers...**.</span></span>

### <a name="new-app"></a><span data-ttu-id="7e891-123">新应用</span><span class="sxs-lookup"><span data-stu-id="7e891-123">New app</span></span>

<span data-ttu-id="7e891-124">使用“ASP.NET Core Web 应用”项目模板新建应用时，请选中“启用 Docker 支持”复选框：</span><span class="sxs-lookup"><span data-stu-id="7e891-124">When creating a new app with the **ASP.NET Core Web Application** project templates, select the **Enable Docker Support** check box:</span></span>

![“启用 Docker 支持”复选框](visual-studio-tools-for-docker/_static/enable-docker-support-check box.png)

<span data-ttu-id="7e891-126">如果目标框架是 .NET Core，可通过 OS 下拉列表选择容器类型。</span><span class="sxs-lookup"><span data-stu-id="7e891-126">If the target framework is .NET Core, the **OS** drop-down allows for the selection of a container type.</span></span>

### <a name="existing-app"></a><span data-ttu-id="7e891-127">现有应用</span><span class="sxs-lookup"><span data-stu-id="7e891-127">Existing app</span></span>

<span data-ttu-id="7e891-128">Visual Studio Tools for Docker 不支持向面向.NET Framework 的现有 ASP.NET Core 项目添加 Docker。</span><span class="sxs-lookup"><span data-stu-id="7e891-128">The Visual Studio Tools for Docker don't support adding Docker to an existing ASP.NET Core project targeting .NET Framework.</span></span> <span data-ttu-id="7e891-129">对于面向 .NET Core 的 ASP.NET Core 项目，可通过两个选项使用工具添加 Docker 支持。</span><span class="sxs-lookup"><span data-stu-id="7e891-129">For ASP.NET Core projects targeting .NET Core, there are two options for adding Docker support via the tooling.</span></span> <span data-ttu-id="7e891-130">在 Visual Studio 中打开项目，然后选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="7e891-130">Open the project in Visual Studio, and choose one of the following options:</span></span>

* <span data-ttu-id="7e891-131">从“项目”菜单中选择“Docker 支持”。</span><span class="sxs-lookup"><span data-stu-id="7e891-131">Select **Docker Support** from the **Project** menu.</span></span>
* <span data-ttu-id="7e891-132">右键单击解决方案资源管理器中的项目，然后选择“添加” > “Docker 支持”。</span><span class="sxs-lookup"><span data-stu-id="7e891-132">Right-click the project in Solution Explorer and select **Add** > **Docker Support**.</span></span>

## <a name="docker-assets-overview"></a><span data-ttu-id="7e891-133">Docker 资产概述</span><span class="sxs-lookup"><span data-stu-id="7e891-133">Docker assets overview</span></span>

<span data-ttu-id="7e891-134">Visual Studio Tools for Docker 向解决方案添加 docker-compose 项目，其中包含以下文件：</span><span class="sxs-lookup"><span data-stu-id="7e891-134">The Visual Studio Tools for Docker add a *docker-compose* project to the solution containing the following files:</span></span>

* <span data-ttu-id="7e891-135">.dockerignore：包含文件和目录模式的列表，排除生成生成上下文的时间。</span><span class="sxs-lookup"><span data-stu-id="7e891-135">*.dockerignore*: Contains a list of file and directory patterns to exclude when generating a build context.</span></span>
* <span data-ttu-id="7e891-136">docker-compose.yml：基本 [Docker Compose](https://docs.docker.com/compose/overview/) 文件，用于定义要分别通过 `docker-compose build` 和 `docker-compose run` 生成和运行的映像集合。</span><span class="sxs-lookup"><span data-stu-id="7e891-136">*docker-compose.yml*: The base [Docker Compose](https://docs.docker.com/compose/overview/) file used to define the collection of images to be built and run with `docker-compose build` and `docker-compose run`, respectively.</span></span>
* <span data-ttu-id="7e891-137">docker compose.override.yml：一个可选文件，通过 Docker Compose 读取，包含服务的配置替代。</span><span class="sxs-lookup"><span data-stu-id="7e891-137">*docker-compose.override.yml*: An optional file, read by Docker Compose, containing configuration overrides for services.</span></span> <span data-ttu-id="7e891-138">Visual Studio 执行 `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` 以合并这些文件。</span><span class="sxs-lookup"><span data-stu-id="7e891-138">Visual Studio executes `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` to merge these files.</span></span>

<span data-ttu-id="7e891-139">Dockerfile，用作创建最终 Docker 映像的方案，添加到项目根目录。</span><span class="sxs-lookup"><span data-stu-id="7e891-139">A *Dockerfile*, the recipe for creating a final Docker image, is added to the project root.</span></span> <span data-ttu-id="7e891-140">请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令。</span><span class="sxs-lookup"><span data-stu-id="7e891-140">Refer to [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for an understanding of the commands within it.</span></span> <span data-ttu-id="7e891-141">此特定 Dockerfile 使用[多阶段生成](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)，该生成包含四个不同的命名生成阶段：</span><span class="sxs-lookup"><span data-stu-id="7e891-141">This particular *Dockerfile* uses a [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) containing four distinct, named build stages:</span></span>

[!code-dockerfile[](visual-studio-tools-for-docker/samples/HelloDockerTools/HelloDockerTools/Dockerfile?highlight=1,5,14,17)]

<span data-ttu-id="7e891-142">Dockerfile 基于 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) 映像。</span><span class="sxs-lookup"><span data-stu-id="7e891-142">The *Dockerfile* is based on the [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) image.</span></span> <span data-ttu-id="7e891-143">此基础映像包括 ASP.NET Core NuGet 包，已对此包进行了预实时编译，以提高启动性能。</span><span class="sxs-lookup"><span data-stu-id="7e891-143">This base image includes the ASP.NET Core NuGet packages, which have been pre-jitted to improve startup performance.</span></span>

<span data-ttu-id="7e891-144">docker-compose.yml 文件包含项目运行时创建的映像的名称：</span><span class="sxs-lookup"><span data-stu-id="7e891-144">The *docker-compose.yml* file contains the name of the image that's created when the project runs:</span></span>

[!code-yaml[](visual-studio-tools-for-docker/samples/HelloDockerTools/docker-compose.yml?highlight=5)]

<span data-ttu-id="7e891-145">在前面的示例中，应用在“调试”模式下运行时，`image: hellodockertools` 生成映像 `hellodockertools:dev`。</span><span class="sxs-lookup"><span data-stu-id="7e891-145">In the preceding example, `image: hellodockertools` generates the image `hellodockertools:dev` when the app runs in **Debug** mode.</span></span> <span data-ttu-id="7e891-146">应用在“发布”模式下运行时，生成 `hellodockertools:latest` 映像。</span><span class="sxs-lookup"><span data-stu-id="7e891-146">The `hellodockertools:latest` image is generated when the app runs in **Release** mode.</span></span>

<span data-ttu-id="7e891-147">如果映像将推送到注册表，则需要添加 [Docker Hub](https://hub.docker.com/) 用户名（如 `dockerhubusername/hellodockertools`）作为映像名称的前缀名。</span><span class="sxs-lookup"><span data-stu-id="7e891-147">Prefix the image name with the [Docker Hub](https://hub.docker.com/) username (for example, `dockerhubusername/hellodockertools`) if the image will be pushed to the registry.</span></span> <span data-ttu-id="7e891-148">或者，更改映像名称，使其包含专用注册表 URL（如 `privateregistry.domain.com/hellodockertools`），具体取决于所用配置。</span><span class="sxs-lookup"><span data-stu-id="7e891-148">Alternatively, change the image name to include the private registry URL (for example, `privateregistry.domain.com/hellodockertools`) depending on the configuration.</span></span>

## <a name="debug"></a><span data-ttu-id="7e891-149">调试</span><span class="sxs-lookup"><span data-stu-id="7e891-149">Debug</span></span>

<span data-ttu-id="7e891-150">在工具栏的调试下拉列表中选择“Docker”，然后开始调试应用。</span><span class="sxs-lookup"><span data-stu-id="7e891-150">Select **Docker** from the debug drop-down in the toolbar, and start debugging the app.</span></span> <span data-ttu-id="7e891-151">“输出”窗口的“Docker”视图显示发生的以下操作：</span><span class="sxs-lookup"><span data-stu-id="7e891-151">The **Docker** view of the **Output** window shows the following actions taking place:</span></span>

* <span data-ttu-id="7e891-152">已获取 microsoft/aspnetcore 运行时映像（如果缓存中尚不存在）。</span><span class="sxs-lookup"><span data-stu-id="7e891-152">The *microsoft/aspnetcore* runtime image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="7e891-153">已获取 microsoft/aspnetcore-build compile/publish 映像（如果缓存中尚不存在）。</span><span class="sxs-lookup"><span data-stu-id="7e891-153">The *microsoft/aspnetcore-build* compile/publish image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="7e891-154">ASPNETCORE_ENVIRONMENT 环境变量设置为位于 `Development` 容器内。</span><span class="sxs-lookup"><span data-stu-id="7e891-154">The *ASPNETCORE_ENVIRONMENT* environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="7e891-155">端口 80 公开，并映射到 localhost 的动态分配端口。</span><span class="sxs-lookup"><span data-stu-id="7e891-155">Port 80 is exposed and mapped to a dynamically assigned port for localhost.</span></span> <span data-ttu-id="7e891-156">该端口由 Docker 主机确定，并且可以使用 `docker ps` 进行查询。</span><span class="sxs-lookup"><span data-stu-id="7e891-156">The port is determined by the Docker host and can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="7e891-157">应用已复制到容器。</span><span class="sxs-lookup"><span data-stu-id="7e891-157">The app is copied to the container.</span></span>
* <span data-ttu-id="7e891-158">默认浏览器使用动态分配端口启动，带有附加到容器的调试程序。</span><span class="sxs-lookup"><span data-stu-id="7e891-158">The default browser is launched with the debugger attached to the container using the dynamically assigned port.</span></span>

<span data-ttu-id="7e891-159">生成的 Docker 映像是应用的开发映像，而 microsoft/aspnetcore 映像则是基本映像。</span><span class="sxs-lookup"><span data-stu-id="7e891-159">The resulting Docker image is the *dev* image of the app with the *microsoft/aspnetcore* images as the base image.</span></span> <span data-ttu-id="7e891-160">在“包管理器控制台”(PMC) 窗口中运行 `docker images` 命令。</span><span class="sxs-lookup"><span data-stu-id="7e891-160">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="7e891-161">显示了计算机上的映像：</span><span class="sxs-lookup"><span data-stu-id="7e891-161">The images on the machine are displayed:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                f8f9d6c923e2        About an hour ago   391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        15 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="7e891-162">因为“调试”配置使用卷装载提供迭代体验，因此，开发映像中缺少应用内容。</span><span class="sxs-lookup"><span data-stu-id="7e891-162">The dev image lacks the app contents, as **Debug** configurations use volume mounting to provide the iterative experience.</span></span> <span data-ttu-id="7e891-163">要推送映像，请使用“发布”配置。</span><span class="sxs-lookup"><span data-stu-id="7e891-163">To push an image, use the **Release** configuration.</span></span>

<span data-ttu-id="7e891-164">在 PMC 中运行 `docker ps` 命令。</span><span class="sxs-lookup"><span data-stu-id="7e891-164">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="7e891-165">请注意，应用使用容器运行：</span><span class="sxs-lookup"><span data-stu-id="7e891-165">Notice the app is running using the container:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a><span data-ttu-id="7e891-166">编辑并继续</span><span class="sxs-lookup"><span data-stu-id="7e891-166">Edit and continue</span></span>

<span data-ttu-id="7e891-167">对静态文件和 Razor 视图的更改会自动更新，无需执行编译步骤。</span><span class="sxs-lookup"><span data-stu-id="7e891-167">Changes to static files and Razor views are automatically updated without the need for a compilation step.</span></span> <span data-ttu-id="7e891-168">进行更改，保存并在浏览器中刷新，以查看更新。</span><span class="sxs-lookup"><span data-stu-id="7e891-168">Make the change, save, and refresh the browser to view the update.</span></span>

<span data-ttu-id="7e891-169">必须在容器内编译和重启 Kestrel，才能修改代码文件。</span><span class="sxs-lookup"><span data-stu-id="7e891-169">Code file modifications require compilation and a restart of Kestrel within the container.</span></span> <span data-ttu-id="7e891-170">更改后，按 `CTRL+F5` 执行过程，并在容器内启动应用。</span><span class="sxs-lookup"><span data-stu-id="7e891-170">After making the change, use `CTRL+F5` to perform the process and start the app within the container.</span></span> <span data-ttu-id="7e891-171">未重新生成或停止 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="7e891-171">The Docker container isn't rebuilt or stopped.</span></span> <span data-ttu-id="7e891-172">在 PMC 中运行 `docker ps` 命令。</span><span class="sxs-lookup"><span data-stu-id="7e891-172">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="7e891-173">请注意，截至 10 分钟前，原始容器仍在运行：</span><span class="sxs-lookup"><span data-stu-id="7e891-173">Notice the original container is still running as of 10 minutes ago:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a><span data-ttu-id="7e891-174">发布 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="7e891-174">Publish Docker images</span></span>

<span data-ttu-id="7e891-175">完成应用的开发和调试循环后，Visual Studio Tools for Docker 可帮助创建应用的生产映像。</span><span class="sxs-lookup"><span data-stu-id="7e891-175">Once the develop and debug cycle of the app is completed, the Visual Studio Tools for Docker assist in creating the production image of the app.</span></span> <span data-ttu-id="7e891-176">将配置下拉列表更改为“发布”，然后生成应用。</span><span class="sxs-lookup"><span data-stu-id="7e891-176">Change the configuration drop-down to **Release** and build the app.</span></span> <span data-ttu-id="7e891-177">此工具生成具有“latest”标签的映像，可以将其推送到专用注册表或 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="7e891-177">The tooling produces the image with the *latest* tag, which can be pushed to the private registry or Docker Hub.</span></span>

<span data-ttu-id="7e891-178">在 PMC 中运行 `docker images` 命令，查看映像列表：</span><span class="sxs-lookup"><span data-stu-id="7e891-178">Run the `docker images` command in PMC to see the list of images:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                4cb1fca533f0        19 seconds ago      391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        16 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="7e891-179">`docker images` 命令返回存储库名称和标记标识为 \<none> （上面未列出）的中间映像。</span><span class="sxs-lookup"><span data-stu-id="7e891-179">The `docker images` command returns intermediary images with repository names and tags identified as *\<none>* (not listed above).</span></span> <span data-ttu-id="7e891-180">这些未命名映像由[多阶段生成](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile* 生成。</span><span class="sxs-lookup"><span data-stu-id="7e891-180">These unnamed images are produced by the [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*.</span></span> <span data-ttu-id="7e891-181">它们可提高生成最终映像的效率 &mdash; 发生更改时，仅重新生成必要的层。</span><span class="sxs-lookup"><span data-stu-id="7e891-181">They improve the efficiency of building the final image&mdash;only the necessary layers are rebuilt when changes occur.</span></span> <span data-ttu-id="7e891-182">不再需要中间映像时，请使用 [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) 命令将其删除。</span><span class="sxs-lookup"><span data-stu-id="7e891-182">When the intermediary images are no longer needed, delete them using the [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) command.</span></span>

<span data-ttu-id="7e891-183">可能希望生产或发布映像的大小比开发映像小。</span><span class="sxs-lookup"><span data-stu-id="7e891-183">There may be an expectation for the production or release image to be smaller in size by comparison to the *dev* image.</span></span> <span data-ttu-id="7e891-184">由于卷映射，调试程序和应用从本地计算机运行，而不在容器内运行。</span><span class="sxs-lookup"><span data-stu-id="7e891-184">Because of the volume mapping, the debugger and app were running from the local machine and not within the container.</span></span> <span data-ttu-id="7e891-185">最新映像已打包必要的应用代码，以在主机上运行应用。</span><span class="sxs-lookup"><span data-stu-id="7e891-185">The *latest* image has packaged the necessary app code to run the app on a host machine.</span></span> <span data-ttu-id="7e891-186">因此，增量是应用代码的大小。</span><span class="sxs-lookup"><span data-stu-id="7e891-186">Therefore, the delta is the size of the app code.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e891-187">其他资源</span><span class="sxs-lookup"><span data-stu-id="7e891-187">Additional resources</span></span>

* [<span data-ttu-id="7e891-188">排查使用 Docker 的 Visual Studio 2017 开发</span><span class="sxs-lookup"><span data-stu-id="7e891-188">Troubleshoot Visual Studio 2017 development with Docker</span></span>](/azure/vs-azure-tools-docker-troubleshooting-docker-errors)
* [<span data-ttu-id="7e891-189">Visual Studio Tools for Docker GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="7e891-189">Visual Studio Tools for Docker GitHub repository</span></span>](https://github.com/Microsoft/DockerTools)
