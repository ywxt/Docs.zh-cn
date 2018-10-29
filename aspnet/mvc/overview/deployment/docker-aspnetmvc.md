---
uid: mvc/overview/deployment/docker
title: 将 ASP.NET MVC 应用程序迁移到 Windows 容器
description: 了解如何利用现有 ASP.NET MVC 应用程序并在 Windows Docker 容器中运行它
keywords: Windows Containers,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 02/01/2017
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 7b34187747d3081998b8b60a72adae78cafe2c3e
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207961"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="d3173-104">将 ASP.NET MVC 应用程序迁移到 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="d3173-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="d3173-105">在 Windows 容器中运行现有的 .NET Framework 应用程序不需要对应用程序进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="d3173-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="d3173-106">若要在 Windows 容器中运行应用程序，请创建包含应用程序的 Docker 映像，然后启动容器。</span><span class="sxs-lookup"><span data-stu-id="d3173-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="d3173-107">本主题介绍了如何获取现有的 [ASP.NET MVC 应用程序](http://www.asp.net/mvc)，并在 Windows 容器中进行部署。</span><span class="sxs-lookup"><span data-stu-id="d3173-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="d3173-108">从现有的 ASP.NET MVC 应用程序入手，然后使用 Visual Studio 生成已发布的资产。</span><span class="sxs-lookup"><span data-stu-id="d3173-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="d3173-109">使用 Docker 创建包含并运行应用程序的映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="d3173-110">转到在 Windows 容器中运行的网站，验证应用程序是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="d3173-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="d3173-111">本文可确保基本了解 Docker。</span><span class="sxs-lookup"><span data-stu-id="d3173-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="d3173-112">若要了解 Docker，请参阅 [Docker 概述](https://docs.docker.com/engine/understanding-docker/)。</span><span class="sxs-lookup"><span data-stu-id="d3173-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="d3173-113">在容器中运行的应用程序是一个随机回答问题的简单网站。</span><span class="sxs-lookup"><span data-stu-id="d3173-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="d3173-114">此应用程序是一款不具备身份验证或数据库存储的基本 MVC 应用程序，让你可以专心处理将 Web 层移到容器中。</span><span class="sxs-lookup"><span data-stu-id="d3173-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="d3173-115">后续主题将演示如何在容器化应用程序中移动和管理永久性存储。</span><span class="sxs-lookup"><span data-stu-id="d3173-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="d3173-116">移动应用程序涉及以下步骤：</span><span class="sxs-lookup"><span data-stu-id="d3173-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="d3173-117">创建发布任务以生成映像资产。</span><span class="sxs-lookup"><span data-stu-id="d3173-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="d3173-118">生成将运行应用程序的 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="d3173-119">启动用于运行映像的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="d3173-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="d3173-120">使用浏览器验证应用程序。</span><span class="sxs-lookup"><span data-stu-id="d3173-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="d3173-121">[完成的应用程序](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator)位于 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="d3173-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3173-122">系统必备</span><span class="sxs-lookup"><span data-stu-id="d3173-122">Prerequisites</span></span>

<span data-ttu-id="d3173-123">在开发计算机必须具有以下软件：</span><span class="sxs-lookup"><span data-stu-id="d3173-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="d3173-124">[Windows 10 周年更新](https://www.microsoft.com/software-download/windows10/)（或更高版本） 或[Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) （或更高版本）</span><span class="sxs-lookup"><span data-stu-id="d3173-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="d3173-125">[用于 Windows 的 Docker](https://docs.docker.com/docker-for-windows/) - 稳定版 1.13.0 或 1.12 beta 版本 26（或更高版本）</span><span class="sxs-lookup"><span data-stu-id="d3173-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="d3173-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d3173-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="d3173-127">如果使用的是 Windows Server 2016，请按[容器主机部署 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment) 中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="d3173-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="d3173-128">安装并启动 Docker，右键单击托盘图标并选择后**切换到 Windows 容器**。</span><span class="sxs-lookup"><span data-stu-id="d3173-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="d3173-129">必须先这样做，才能在 Windows 上运行 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="d3173-130">此命令需要几秒钟执行：</span><span class="sxs-lookup"><span data-stu-id="d3173-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="d3173-131">![Windows 容器][windows-container]</span><span class="sxs-lookup"><span data-stu-id="d3173-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="d3173-132">发布脚本</span><span class="sxs-lookup"><span data-stu-id="d3173-132">Publish script</span></span>

<span data-ttu-id="d3173-133">将需要加载到 Docker 映像中的所有资产都汇集到一处。</span><span class="sxs-lookup"><span data-stu-id="d3173-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="d3173-134">可以使用 Visual Studio 的“**发布**”命令来创建应用程序的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="d3173-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="d3173-135">此配置文件会将所有资产汇集到同一目录树中，本教程的后面部分将介绍如何将此目录树复制到目标映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="d3173-136">**发布步骤**</span><span class="sxs-lookup"><span data-stu-id="d3173-136">**Publish Steps**</span></span>

1. <span data-ttu-id="d3173-137">在 Visual Studio 中右键单击 Web 项目，然后选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="d3173-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="d3173-138">单击“**自定义配置文件**”按钮，然后选择“**文件系统**”作为方法。</span><span class="sxs-lookup"><span data-stu-id="d3173-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="d3173-139">选择该目录。</span><span class="sxs-lookup"><span data-stu-id="d3173-139">Choose the directory.</span></span> <span data-ttu-id="d3173-140">按照约定，已下载示例将使用 `bin\Release\PublishOutput`。</span><span class="sxs-lookup"><span data-stu-id="d3173-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="d3173-141">![发布连接][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="d3173-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="d3173-142">打开“**设置**”选项卡上的“**文件发布选项**”部分。选择“在发布期间预编译”。</span><span class="sxs-lookup"><span data-stu-id="d3173-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="d3173-143">这种优化意味着，在复制预编译视图的同时，在 Docker 容器中编译视图。</span><span class="sxs-lookup"><span data-stu-id="d3173-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="d3173-144">![发布设置][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="d3173-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="d3173-145">单击“发布”，Visual Studio 会将所有所需资产复制到目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3173-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="d3173-146">生成映像</span><span class="sxs-lookup"><span data-stu-id="d3173-146">Build the image</span></span>

<span data-ttu-id="d3173-147">在 Dockerfile 中定义 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-147">Define your Docker image in a Dockerfile.</span></span> <span data-ttu-id="d3173-148">Dockerfile 包含有关基本映像、附加组件、要运行的应用程序和其他配置映像的说明。</span><span class="sxs-lookup"><span data-stu-id="d3173-148">The Dockerfile contains instructions for the base image, additional components, the app you want to run, and other configuration images.</span></span>  <span data-ttu-id="d3173-149">Dockerfile 是用于创建该映像的 `docker build` 命令的输入。</span><span class="sxs-lookup"><span data-stu-id="d3173-149">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="d3173-150">根据位于 [Docker 中心](https://hub.docker.com/r/microsoft/aspnet/) 的 `microsoft/aspnet` 映像生成映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-150">You will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="d3173-151">基本映像 `microsoft/aspnet` 为 Windows Server 映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="d3173-152">它包含 Windows Server Core、 IIS 和 ASP.NET 4.7.2。</span><span class="sxs-lookup"><span data-stu-id="d3173-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="d3173-153">在容器中运行此映像时，它会自动启动 IIS 和已安装的网站。</span><span class="sxs-lookup"><span data-stu-id="d3173-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="d3173-154">创建映像的 Dockerfile 如下所示：</span><span class="sxs-lookup"><span data-stu-id="d3173-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="d3173-155">此 Dockerfile 中不含 `ENTRYPOINT` 命令。</span><span class="sxs-lookup"><span data-stu-id="d3173-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="d3173-156">不需要该命令。</span><span class="sxs-lookup"><span data-stu-id="d3173-156">You don't need one.</span></span> <span data-ttu-id="d3173-157">运行 Windows Server 与 IIS，IIS 进程时，入口点，配置为 aspnet 基本映像中启动。</span><span class="sxs-lookup"><span data-stu-id="d3173-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="d3173-158">运行 Docker 生成命令，创建运行 ASP.NET 应用程序的映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="d3173-159">若要执行此操作，在你的项目的目录中打开 PowerShell 窗口并在解决方案目录中键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d3173-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="d3173-160">此命令将生成新映像使用 Dockerfile 中的说明命名 (-t 表示标记) 作为 mvcrandomanswers 映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="d3173-161">这样做可能还会从 [Docker 中心](http://hub.docker.com)拉取基本映像，然后将应用程序添加到基本映像中。</span><span class="sxs-lookup"><span data-stu-id="d3173-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="d3173-162">命令完成后，便可以运行 `docker images` 命令，查看有关新映像的信息：</span><span class="sxs-lookup"><span data-stu-id="d3173-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="d3173-163">计算机上的 IMAGE ID 会所不同。</span><span class="sxs-lookup"><span data-stu-id="d3173-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="d3173-164">现在，让我们来运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="d3173-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="d3173-165">启动容器</span><span class="sxs-lookup"><span data-stu-id="d3173-165">Start a container</span></span>

<span data-ttu-id="d3173-166">通过执行以下 `docker run` 命令来启动容器：</span><span class="sxs-lookup"><span data-stu-id="d3173-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="d3173-167">`-d` 参数告知 Docker 在分离模式下启动映像。</span><span class="sxs-lookup"><span data-stu-id="d3173-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="d3173-168">这意味着 Docker 映像会以断开连接当前 shell 的状态运行。</span><span class="sxs-lookup"><span data-stu-id="d3173-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="d3173-169">在多个 docker 示例中，可能会看到-p 来将容器和主机端口映射。</span><span class="sxs-lookup"><span data-stu-id="d3173-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="d3173-170">默认 aspnet 映像已配置要侦听端口 80 上并将其公开的容器。</span><span class="sxs-lookup"><span data-stu-id="d3173-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="d3173-171">`--name randomanswers` 为运行中容器命名。</span><span class="sxs-lookup"><span data-stu-id="d3173-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="d3173-172">可在大多数命令中使用此名称，而不是容器 ID。</span><span class="sxs-lookup"><span data-stu-id="d3173-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="d3173-173">`mvcrandomanswers` 是要启动的映像名称。</span><span class="sxs-lookup"><span data-stu-id="d3173-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="d3173-174">在浏览器中验证</span><span class="sxs-lookup"><span data-stu-id="d3173-174">Verify in the browser</span></span>

<span data-ttu-id="d3173-175">容器启动后，连接到正在运行的容器使用`http://localhost`中所示的示例。</span><span class="sxs-lookup"><span data-stu-id="d3173-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="d3173-176">在浏览器中键入该 URL，应该可看到正在运行的站点。</span><span class="sxs-lookup"><span data-stu-id="d3173-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="d3173-177">某 VPN 或代理软件可能会阻止你导航到站点。</span><span class="sxs-lookup"><span data-stu-id="d3173-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="d3173-178">可以暂时禁用它，确保容器正常工作。</span><span class="sxs-lookup"><span data-stu-id="d3173-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="d3173-179">GitHub 上的示例目录包含为你执行这些命令的 [PowerShell 脚本](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)。</span><span class="sxs-lookup"><span data-stu-id="d3173-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="d3173-180">打开 PowerShell 窗口，将目录更改为解决方案目录，然后键入：</span><span class="sxs-lookup"><span data-stu-id="d3173-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="d3173-181">上面的命令生成映像、 映像的列表显示在计算机上并启动的容器。</span><span class="sxs-lookup"><span data-stu-id="d3173-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="d3173-182">若要停止容器，请发出 `docker stop` 命令：</span><span class="sxs-lookup"><span data-stu-id="d3173-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="d3173-183">若要删除该容器，可发出 `docker rm` 命令：</span><span class="sxs-lookup"><span data-stu-id="d3173-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "切换到 Windows 容器"
[publish-connection]: media/aspnetmvc/PublishConnection.png "发布到文件系统"
[publish-settings]: media/aspnetmvc/PublishSettings.png "发布设置"
