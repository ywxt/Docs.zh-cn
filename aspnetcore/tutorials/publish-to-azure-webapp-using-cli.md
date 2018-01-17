---
title: "使用命令行工具将 ASP.NET Core 应用程序发布到 Azure 中 | Microsoft 文档"
description: "了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。"
services: multiple
keywords: "ASP.NET Core, Azure, 应用服务, Git, 命令行"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/03/2017
ms.topic: get-started-article
ms.prod: asp.net-core
ms.technology: aspnet
ms.custom: mvc
ms.devlang: dotnet
uid: tutorials/publish-to-azure-webapp-using-cli
ms.openlocfilehash: 6af5de584cbf8cd59d86a965592b958061014c95
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="deploy-an-aspnet-core-application-to-azure-app-service-from-the-command-line"></a><span data-ttu-id="3f185-104">从命令行将 ASP.NET Core 应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3f185-104">Deploy an ASP.NET Core application to Azure App Service from the command line</span></span>

<span data-ttu-id="3f185-105">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="3f185-105">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="3f185-106">本教程将为你介绍如何使用命令行工具生成 ASP.NET Core 应用程序并将其部署到 Microsoft Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="3f185-106">This tutorial will show you how to build and deploy an ASP.NET Core application to Microsoft Azure App Service using command line tools.</span></span>  <span data-ttu-id="3f185-107">完成后，你将拥有一个在 ASP.NET MVC Core 中构建并作为 Azure App Service Web App 托管的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f185-107">When finished, you'll have a web application built in ASP.NET MVC Core hosted as an Azure App Service Web App.</span></span>  <span data-ttu-id="3f185-108">本教程是使用 Windows 命令行工具编写的，但也可以应用于 macOS 和 Linux 环境。</span><span class="sxs-lookup"><span data-stu-id="3f185-108">This tutorial is written using Windows command line tools, but can be applied to macOS and Linux environments, as well.</span></span>  

<span data-ttu-id="3f185-109">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="3f185-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f185-110">如何使用 Azure CLI 创建 Azure App Service 网站</span><span class="sxs-lookup"><span data-stu-id="3f185-110">Create an Azure App Service website using Azure CLI</span></span>
> * <span data-ttu-id="3f185-111">如何使用 Git 命令行工具将 ASP.NET Core 应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3f185-111">Deploy an ASP.NET Core application to Azure App Service using the Git command line tool</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f185-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="3f185-112">Prerequisites</span></span>

<span data-ttu-id="3f185-113">若要完成本教程，你需要：</span><span class="sxs-lookup"><span data-stu-id="3f185-113">To complete this tutorial, you'll need:</span></span>

* <span data-ttu-id="3f185-114">[Microsoft Azure 订阅](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="3f185-114">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="3f185-115">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3f185-115">.NET Core</span></span>](https://www.microsoft.com/net/download/core)
* <span data-ttu-id="3f185-116">[Git](https://www.git-scm.com/) 命令行客户端</span><span class="sxs-lookup"><span data-stu-id="3f185-116">[Git](https://www.git-scm.com/) command line client</span></span>

## <a name="create-a-web-application"></a><span data-ttu-id="3f185-117">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="3f185-117">Create a web application</span></span>

<span data-ttu-id="3f185-118">为 Web 应用程序创建新目录，创建新的 ASP.NET Core MVC 应用程序，然后在本地运行该网站。</span><span class="sxs-lookup"><span data-stu-id="3f185-118">Create a new directory for the web application, create a new ASP.NET Core MVC application, and then run the website locally.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="3f185-119">Windows</span><span class="sxs-lookup"><span data-stu-id="3f185-119">Windows</span></span>](#tab/windows)
```cmd
REM Create a new ASP.NET Core MVC application
dotnet new razor -o MyApplication

REM Change to the new directory that was just created
cd MyApplication

REM Run the application
dotnet run
```

# <a name="othertabother"></a>[<span data-ttu-id="3f185-120">其他</span><span class="sxs-lookup"><span data-stu-id="3f185-120">Other</span></span>](#tab/other)
```bash
# Create a new ASP.NET Core MVC application
dotnet new razor -o MyApplication

# Change to the new directory that was just created
cd MyApplication

# Run the application
dotnet run
```
---

![命令行输出](publish-to-azure-webapp-using-cli/_static/new_prj.png)

<span data-ttu-id="3f185-122">通过浏览到 http://localhost:5000 测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f185-122">Test the application by browsing to http://localhost:5000.</span></span>

![本地运行的网站](publish-to-azure-webapp-using-cli/_static/app_test.png)


## <a name="create-the-azure-app-service-instance"></a><span data-ttu-id="3f185-124">创建 Azure App Service 实例</span><span class="sxs-lookup"><span data-stu-id="3f185-124">Create the Azure App Service instance</span></span>

<span data-ttu-id="3f185-125">使用 [Azure Cloud Shell](/azure/cloud-shell/quickstart)，创建资源组、App Service 计划和 App Service Web 应用。</span><span class="sxs-lookup"><span data-stu-id="3f185-125">Using the [Azure Cloud Shell](/azure/cloud-shell/quickstart), create a resource group, App Service plan, and an App Service web app.</span></span>

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

<span data-ttu-id="3f185-126">在部署之前，使用以下命令设置帐户级部署凭据：</span><span class="sxs-lookup"><span data-stu-id="3f185-126">Before deployment, set the account-level deployment credentials using the following command:</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="3f185-127">需要使用部署 URL 来使用 Git 部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f185-127">A deployment URL is needed to deploy the application using Git.</span></span>  <span data-ttu-id="3f185-128">检索类似如下的 URL。</span><span class="sxs-lookup"><span data-stu-id="3f185-128">Retrieve the URL like this.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv
```
<span data-ttu-id="3f185-129">请注意以 `.git` 结尾的已显示 URL。</span><span class="sxs-lookup"><span data-stu-id="3f185-129">Note the displayed URL ending in `.git`.</span></span> <span data-ttu-id="3f185-130">它在下一步中使用。</span><span class="sxs-lookup"><span data-stu-id="3f185-130">It's used in the next step.</span></span>

## <a name="deploy-the-application-using-git"></a><span data-ttu-id="3f185-131">使用 Git 部署应用程序</span><span class="sxs-lookup"><span data-stu-id="3f185-131">Deploy the application using Git</span></span>

<span data-ttu-id="3f185-132">你已准备好使用 Git 从本地计算机部署。</span><span class="sxs-lookup"><span data-stu-id="3f185-132">You're ready to deploy from your local machine using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="3f185-133">忽略 Git 中任何关于行尾的警告是安全的。</span><span class="sxs-lookup"><span data-stu-id="3f185-133">It's safe to ignore any warnings from Git about line endings.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="3f185-134">Windows</span><span class="sxs-lookup"><span data-stu-id="3f185-134">Windows</span></span>](#tab/windows)
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

# <a name="othertabother"></a>[<span data-ttu-id="3f185-135">其他</span><span class="sxs-lookup"><span data-stu-id="3f185-135">Other</span></span>](#tab/other)
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

<span data-ttu-id="3f185-136">Git 将提示前面设置的部署凭据。</span><span class="sxs-lookup"><span data-stu-id="3f185-136">Git will prompt for the deployment credentials that were set earlier.</span></span>  <span data-ttu-id="3f185-137">身份验证后，将应用程序推送到远程位置，然后生成并部署。</span><span class="sxs-lookup"><span data-stu-id="3f185-137">After authenticating, the application will be pushed to the remote location, built, and deployed.</span></span>

![Git 部署输出](publish-to-azure-webapp-using-cli/_static/post_deploy.png)

## <a name="test-the-application"></a><span data-ttu-id="3f185-139">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="3f185-139">Test the application</span></span>

<span data-ttu-id="3f185-140">通过浏览到 `https://<web app name>.azurewebsites.net` 测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f185-140">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="3f185-141">若要在 Cloud Shell（或 Azure CLI）中显示地址，请使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="3f185-141">To display the address in the Cloud Shell (or Azure CLI), use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

![在 Azure 中运行的应用](publish-to-azure-webapp-using-cli/_static/app_deployed.png)

## <a name="clean-up"></a><span data-ttu-id="3f185-143">清理</span><span class="sxs-lookup"><span data-stu-id="3f185-143">Clean up</span></span>

<span data-ttu-id="3f185-144">完成测试应用并检查代码和资源后，通过删除资源组来删除 Web 应用并制定计划。</span><span class="sxs-lookup"><span data-stu-id="3f185-144">When finished testing the app and inspecting the code and resources, delete the web app and plan by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="3f185-145">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3f185-145">Next steps</span></span>

<span data-ttu-id="3f185-146">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="3f185-146">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f185-147">如何使用 Azure CLI 创建 Azure App Service 网站</span><span class="sxs-lookup"><span data-stu-id="3f185-147">Create an Azure App Service website using Azure CLI</span></span>
> * <span data-ttu-id="3f185-148">如何使用 Git 命令行工具将 ASP.NET Core 应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3f185-148">Deploy an ASP.NET Core application to Azure App Service using the Git command line tool</span></span>

<span data-ttu-id="3f185-149">接下来，了解如何使用命令行来部署使用 CosmosDB 的现有 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="3f185-149">Next, learn to use the command line to deploy an existing web app that uses CosmosDB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f185-150">通过 .NET Core 从命令行部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="3f185-150">Deploy to Azure from the command line with .NET Core</span></span>](/dotnet/azure/dotnet-quickstart-xplat)
