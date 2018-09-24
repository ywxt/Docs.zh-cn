---
title: 使用命令行工具将 ASP.NET Core 应用发布到 Azure
author: camsoper
description: 了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。
ms.author: casoper
ms.custom: mvc
ms.date: 11/03/2017
services: multiple
uid: tutorials/publish-to-azure-webapp-using-cli
ms.openlocfilehash: 63a313de786b1f89e84c594cbd665d1b230e4ba3
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523241"
---
# <a name="publish-an-aspnet-core-app-to-azure-with-command-line-tools"></a><span data-ttu-id="276a1-103">使用命令行工具将 ASP.NET Core 应用发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="276a1-103">Publish an ASP.NET Core app to Azure with command line tools</span></span>

<span data-ttu-id="276a1-104">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="276a1-104">By [Cam Soper](https://twitter.com/camsoper)</span></span>

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

<span data-ttu-id="276a1-105">本教程将介绍如何使用命令行工具构建 ASP.NET Core 应用并将其部署到 Microsoft Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="276a1-105">This tutorial will show you how to build and deploy an ASP.NET Core app to Microsoft Azure App Service using command line tools.</span></span> <span data-ttu-id="276a1-106">完成后，将在作为 Azure 应用服务 Web 应用托管的 ASP.NET Core 中构建 Razor Pages Web 应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-106">When finished, you'll have a Razor Pages web app built in ASP.NET Core hosted as an Azure App Service Web App.</span></span> <span data-ttu-id="276a1-107">本教程是使用 Windows 命令行工具编写的，但也可以应用于 macOS 和 Linux 环境。</span><span class="sxs-lookup"><span data-stu-id="276a1-107">This tutorial is written using Windows command line tools, but can be applied to macOS and Linux environments, as well.</span></span>

<span data-ttu-id="276a1-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="276a1-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="276a1-109">如何使用 Azure CLI 创建 Azure App Service 网站</span><span class="sxs-lookup"><span data-stu-id="276a1-109">Create an Azure App Service website using Azure CLI</span></span>
> * <span data-ttu-id="276a1-110">使用 Git 命令行工具将 ASP.NET Core 应用部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="276a1-110">Deploy an ASP.NET Core app to Azure App Service using the Git command line tool</span></span>

## <a name="prerequisites"></a><span data-ttu-id="276a1-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="276a1-111">Prerequisites</span></span>

<span data-ttu-id="276a1-112">若要完成本教程，你需要：</span><span class="sxs-lookup"><span data-stu-id="276a1-112">To complete this tutorial, you'll need:</span></span>

* <span data-ttu-id="276a1-113">[Microsoft Azure 订阅](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="276a1-113">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* <span data-ttu-id="276a1-114">[Git](https://www.git-scm.com/) 命令行客户端</span><span class="sxs-lookup"><span data-stu-id="276a1-114">[Git](https://www.git-scm.com/) command line client</span></span>

## <a name="create-a-web-app"></a><span data-ttu-id="276a1-115">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="276a1-115">Create a web app</span></span>

<span data-ttu-id="276a1-116">为 Web 应用创建新目录，创建新的 ASP.NET Core Razor Pages 应用，然后在本地运行该网站。</span><span class="sxs-lookup"><span data-stu-id="276a1-116">Create a new directory for the web app, create a new ASP.NET Core Razor Pages app, and then run the website locally.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="276a1-117">Windows</span><span class="sxs-lookup"><span data-stu-id="276a1-117">Windows</span></span>](#tab/windows)

::: moniker range=">= aspnetcore-2.1"

```console
REM Create a new ASP.NET Core Razor Pages app
dotnet new webapp -o MyApplication

REM Change to the new directory that was just created
cd MyApplication

REM Run the app
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
REM Create a new ASP.NET Core Razor Pages app
dotnet new razor -o MyApplication

REM Change to the new directory that was just created
cd MyApplication

REM Run the app
dotnet run
```

::: moniker-end

# <a name="othertabother"></a>[<span data-ttu-id="276a1-118">其他</span><span class="sxs-lookup"><span data-stu-id="276a1-118">Other</span></span>](#tab/other)

::: moniker range=">= aspnetcore-2.1"

```bash
# Create a new ASP.NET Core Razor Pages app
dotnet new webapp -o MyApplication

# Change to the new directory that was just created
cd MyApplication

# Run the app
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```bash
# Create a new ASP.NET Core Razor Pages app
dotnet new razor -o MyApplication

# Change to the new directory that was just created
cd MyApplication

# Run the app
dotnet run
```

::: moniker-end

---

![命令行输出](publish-to-azure-webapp-using-cli/_static/new_prj.png)

<span data-ttu-id="276a1-120">通过浏览到 `http://localhost:5000` 测试应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-120">Test the app by browsing to `http://localhost:5000`.</span></span>

![本地运行的网站](publish-to-azure-webapp-using-cli/_static/app_test.png)

## <a name="create-the-azure-app-service-instance"></a><span data-ttu-id="276a1-122">创建 Azure App Service 实例</span><span class="sxs-lookup"><span data-stu-id="276a1-122">Create the Azure App Service instance</span></span>

<span data-ttu-id="276a1-123">使用 [Azure Cloud Shell](/azure/cloud-shell/quickstart)，创建资源组、App Service 计划和 App Service Web 应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-123">Using the [Azure Cloud Shell](/azure/cloud-shell/quickstart), create a resource group, App Service plan, and an App Service web app.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=tutorialApp$randomNum

# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname
```

<span data-ttu-id="276a1-124">在部署之前，使用以下命令设置帐户级部署凭据：</span><span class="sxs-lookup"><span data-stu-id="276a1-124">Before deployment, set the account-level deployment credentials using the following command:</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="276a1-125">需要使用部署 URL 来使用 Git 部署应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-125">A deployment URL is needed to deploy the app using Git.</span></span> <span data-ttu-id="276a1-126">检索类似如下的 URL。</span><span class="sxs-lookup"><span data-stu-id="276a1-126">Retrieve the URL like this.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv
```

<span data-ttu-id="276a1-127">请注意以 `.git` 结尾的已显示 URL。</span><span class="sxs-lookup"><span data-stu-id="276a1-127">Note the displayed URL ending in `.git`.</span></span> <span data-ttu-id="276a1-128">它在下一步中使用。</span><span class="sxs-lookup"><span data-stu-id="276a1-128">It's used in the next step.</span></span>

## <a name="deploy-the-app-using-git"></a><span data-ttu-id="276a1-129">使用 Git 部署应用</span><span class="sxs-lookup"><span data-stu-id="276a1-129">Deploy the app using Git</span></span>

<span data-ttu-id="276a1-130">你已准备好使用 Git 从本地计算机部署。</span><span class="sxs-lookup"><span data-stu-id="276a1-130">You're ready to deploy from your local machine using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="276a1-131">忽略 Git 中任何关于行尾的警告是安全的。</span><span class="sxs-lookup"><span data-stu-id="276a1-131">It's safe to ignore any warnings from Git about line endings.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="276a1-132">Windows</span><span class="sxs-lookup"><span data-stu-id="276a1-132">Windows</span></span>](#tab/windows)

```cmd
REM Initialize the local Git repository
git init

REM Add the contents of the working directory to the repo
git add --all

REM Commit the changes to the local repo
git commit -a -m "Initial commit"

REM Add the URL as a Git remote repository
git remote add azure <THE GIT URL YOU NOTED EARLIER>

REM Push the local repository to the remote
git push azure master
```

# <a name="othertabother"></a>[<span data-ttu-id="276a1-133">其他</span><span class="sxs-lookup"><span data-stu-id="276a1-133">Other</span></span>](#tab/other)

```bash
# Initialize the local Git repository
git init

# Add the contents of the working directory to the repo
git add --all

# Commit the changes to the local repo
git commit -a -m "Initial commit"

# Add the URL as a Git remote repository
git remote add azure <THE GIT URL YOU NOTED EARLIER>

# Push the local repository to the remote
git push azure master
```

---

<span data-ttu-id="276a1-134">Git 提示前面设置的部署凭据。</span><span class="sxs-lookup"><span data-stu-id="276a1-134">Git prompts for the deployment credentials that were set earlier.</span></span> <span data-ttu-id="276a1-135">身份验证后，应用将会推送到远程位置，然后生成并部署。</span><span class="sxs-lookup"><span data-stu-id="276a1-135">After authenticating, the app will be pushed to the remote location, built, and deployed.</span></span>

![Git 部署输出](publish-to-azure-webapp-using-cli/_static/post_deploy.png)

## <a name="test-the-app"></a><span data-ttu-id="276a1-137">测试应用</span><span class="sxs-lookup"><span data-stu-id="276a1-137">Test the app</span></span>

<span data-ttu-id="276a1-138">通过浏览到 `https://<web app name>.azurewebsites.net` 测试应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-138">Test the app by browsing to `https://<web app name>.azurewebsites.net`.</span></span> <span data-ttu-id="276a1-139">若要在 Cloud Shell（或 Azure CLI）中显示地址，请使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="276a1-139">To display the address in the Cloud Shell (or Azure CLI), use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

![在 Azure 中运行的应用](publish-to-azure-webapp-using-cli/_static/app_deployed.png)

## <a name="clean-up"></a><span data-ttu-id="276a1-141">清理</span><span class="sxs-lookup"><span data-stu-id="276a1-141">Clean up</span></span>

<span data-ttu-id="276a1-142">完成测试应用并检查代码和资源后，通过删除资源组来删除 Web 应用并制定计划。</span><span class="sxs-lookup"><span data-stu-id="276a1-142">When finished testing the app and inspecting the code and resources, delete the web app and plan by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="276a1-143">后续步骤</span><span class="sxs-lookup"><span data-stu-id="276a1-143">Next steps</span></span>

<span data-ttu-id="276a1-144">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="276a1-144">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="276a1-145">如何使用 Azure CLI 创建 Azure App Service 网站</span><span class="sxs-lookup"><span data-stu-id="276a1-145">Create an Azure App Service website using Azure CLI</span></span>
> * <span data-ttu-id="276a1-146">使用 Git 命令行工具将 ASP.NET Core 应用部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="276a1-146">Deploy an ASP.NET Core app to Azure App Service using the Git command line tool</span></span>

<span data-ttu-id="276a1-147">接下来，了解如何使用命令行来部署使用 CosmosDB 的现有 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="276a1-147">Next, learn to use the command line to deploy an existing web app that uses CosmosDB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="276a1-148">通过 .NET Core 从命令行部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="276a1-148">Deploy to Azure from the command line with .NET Core</span></span>](/dotnet/azure/dotnet-quickstart-xplat)
